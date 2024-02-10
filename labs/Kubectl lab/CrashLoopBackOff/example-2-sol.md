# Troubleshooting Kubernetes Pod: CrashLoopBackOff Error

## Problem Description
In this scenario, we have a Kubernetes Pod definition with the following details:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crashloop-error-2
spec:
  containers:
    - name: container-1
      image: nginx:latest
      ports:
        - containerPort: 8080 # Incorrect port, NGINX default is 80
```

When attempting to create this Pod, it enters a `CrashLoopBackOff` state. Let's identify the issue and troubleshoot it step by step.

## Error Identification

The issue in the YAML file that causes the `CrashLoopBackOff` error is the incorrect `containerPort` specified for the container. The NGINX default port is 80, but in the YAML file, it's set to `8080`.

## Troubleshooting Steps

To resolve the `CrashLoopBackOff` error, follow these troubleshooting steps:

### 1. Review the YAML File

- Open the YAML file used to create the Pod.
- Identify the `containerPort` field within the `ports` section.

### 2. Understand the Issue

- Recognize that NGINX by default listens on port 80 for incoming traffic. Setting an incorrect port may prevent NGINX from functioning correctly.

### 3. Determine the Desired Port

- Decide which port the container should listen on.
- If the container should listen on the default NGINX port (80), remove the `containerPort` field or set it to `80`.

Modified YAML:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crashloop-error-2
spec:
  containers:
    - name: container-1
      image: nginx:latest
```

### 4. Apply the Changes

- Save the modified YAML file.
- Apply the changes using the `kubectl apply -f <filename.yaml>` command.

### 5. Verify Pod Status

- Check the status of the Pod using `kubectl get pods`.
- Ensure that the Pod transitions from `CrashLoopBackOff` to a running or ready state.

## Conclusion

By understanding the issue and making the necessary changes to the `containerPort` field in the YAML file, you can troubleshoot and resolve the `CrashLoopBackOff` error, allowing the container to listen on the desired port and function as intended.

