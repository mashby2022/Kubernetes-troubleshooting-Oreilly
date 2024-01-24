# Botkube Kubernetes Actions Automation Guide

1. [Action Configuration](#1-action-configuration)
2. [Predefined Actions](#2-predefined-actions)
3. [Action Output](#3-action-output)
4. [Command Templates](#4-command-templates)
5. [Syntax](#5-syntax)

## 1. Action Configuration

Action configuration in Botkube allows you to automate your Kubernetes workflow by defining commands that are executed when specific events occur. This is achieved by defining event sources (command triggers) using source bindings and specifying how the commands are executed using executor bindings.

## 2. Predefined Actions

Botkube provides two predefined actions that serve as templates for automation:

### a. describe-created-resource

This action describes a newly created resource in your Kubernetes cluster.

### b. show-logs-on-error

This action prints logs for Pods, StatefulSets, DaemonSets, or Deployments when an error occurs.

Both of these actions are disabled by default, and you can enable them as needed.

## 3. Action Output

The output of the command defined in an action is sent to communication platforms that have the same source bindings. If there are no communication platforms with matching source bindings, the action is still executed, but the output is ignored.

## 4. Command Templates

Each action in Botkube defines a `command` property that specifies the command to be executed. These command templates support Go template syntax and are rendered before actual execution. You can use the following variable in your templates:

- `{{ .Event }}`: Represents the event object that triggered the action. You can find all available event properties in the `event.go` file.

Botkube also supports multiple helper functions provided by the templating engine. To learn more about these functions, you can refer to the documentation on the Slim-Sprig library page.

## 5. Syntax

Below is an example of the syntax used to configure actions in Botkube:

```yaml
# Map of actions. Action contains configuration for automation based on observed events.
# The property name under `actions` object is an alias for a given configuration. You can define multiple actions configuration with different names.
#
# Format: actions.{alias}
actions:
  "describe-created-resource":
    # If true, enables the action.
    enabled: false
    # Action display name posted in the channels bound to the same source bindings.
    displayName: "Describe created resource"
    # Command to execute when the action is triggered. You can use Go template syntax together with helper functions from the Slim-Sprig library.
    # You can use the `{{ .Event }}` variable, which contains the event object that triggered the action. See all available event properties on GitHub.
    command: "kubectl describe {{ .Event.TypeMeta.Kind | lower }}{{ if .Event.Namespace }} -n {{ .Event.Namespace }}{{ end }} {{ .Event.Name }}"

    # Bindings for a given action.
    bindings:
      # Event sources that trigger a given action.
      sources:
        - k8s-create-events
      # Executors configuration used to execute a configured command.
      executors:
        - k8s-default-tools
  "show-logs-on-error":
    # If true, enables the action.
    enabled: false

    # Action display name posted in the channels bound to the same source bindings.
    displayName: "Show logs on error"
    # Command to execute when the action is triggered. You can use Go template syntax together with helper functions from the Slim-Sprig library.
    # You can use the `{{ .Event }}` variable, which contains the event object that triggered the action. See all available event properties on GitHub.
    command: "kubectl logs {{ .Event.TypeMeta.Kind | lower }}/{{ .Event.Name }} -n {{ .Event.Namespace }}"

    # Bindings for a given action.
    bindings:
      # Event sources that trigger a given action.
      sources:
        - k8s-err-with-logs-events
      # Executors configuration used to execute a configured command.
      executors:
        - k8s-default-tools
```

That concludes our guide on creating Go automations for Botkube Kubernetes actions. You can customize these actions and their commands to suit your specific Kubernetes workflow automation needs.
