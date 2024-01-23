# Kubectl Guide

## Overview

`kubectl` is a command-line tool used for interacting with Kubernetes clusters. It is a part of the Kubernetes ecosystem and serves as the primary interface for managing containerized applications within Kubernetes clusters. With `kubectl`, you can perform various operations, such as deploying and scaling applications, inspecting cluster resources, and debugging issues.

## Cheat Sheet - Common `kubectl` Commands

Here's a quick reference for some common `kubectl` commands:

### Cluster Information

- Get cluster information:
  ```
  kubectl cluster-info
  ```

- Display the current context:
  ```
  kubectl config current-context
  ```

### Pods

- List all pods in the current namespace:
  ```
  kubectl get pods
  ```

- Describe a pod:
  ```
  kubectl describe pod <pod-name>
  ```

- Tail the logs of a pod:
  ```
  kubectl logs -f <pod-name>
  ```

### Deployments

- List all deployments in the current namespace:
  ```
  kubectl get deployments
  ```

- Scale a deployment:
  ```
  kubectl scale deployment <deployment-name> --replicas=<desired-replicas>
  ```

- Update a deployment's image:
  ```
  kubectl set image deployment/<deployment-name> <container-name>=<new-image>
  ```

### Services

- List all services in the current namespace:
  ```
  kubectl get services
  ```

- Expose a deployment as a service:
  ```
  kubectl expose deployment <deployment-name> --port=<port>
  ```

### Common Errors

### 1. [OOMKilled (Out of Memory Killed)](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubectl%20lab/OOMKilled/OOMKilled.md)

OOMKilled occurs when a container consumes all available memory resources and is terminated by the kernel. To resolve this issue, you can:

- Increase the memory limit for the container.
- Optimize the application's memory usage.
- Add more resources to the cluster if needed.

### 2.[CrashLoopBackOff](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubectl%20lab/CrashLoopBackOff/CrashLoopBackOff.md)

CrashLoopBackOff indicates that a container repeatedly crashes immediately after starting. To troubleshoot:

- Check the container logs with `kubectl logs`.
- Review the container's configuration and environment variables.
- Ensure that required resources are available.

### 3.[CreateContainerConfigError](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubectl%20lab/CreateContainerConfigError/CreateContainerConfigError.md)

CreateContainerConfigError occurs when there is an issue with the container's configuration. To address this:

- Verify the container's configuration settings, including image, command, and volume mounts.
- Check for typos or syntax errors in your YAML files.

### 4.[CreateContainerError](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubectl%20lab/CreateContainerError/CreateContainerError.md)

CreateContainerError occurs when Kubernetes fails to create a container. To resolve this:

- Check the image name and availability in your container registry.
- Verify that the image pull policy is correctly set.
- Examine the pod's resource requests and limits.

## Conclusion

`kubectl` is a powerful tool for managing Kubernetes clusters and applications. Understanding common commands and how to troubleshoot errors can help streamline your Kubernetes operations.
