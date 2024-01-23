# Troubleshooting OOMKilled Error in Kubernetes

## Problem Description

In this scenario, we have a YAML file (`oom-pod-1.yaml`) that defines a Kubernetes pod. The pod runs a container named `container-1` with a specific command that consumes memory continuously. The memory limit is set to `100Mi`, which is relatively low. As a result, the container is terminated with an OOMKilled error due to exceeding the memory limit.

### YAML File 1:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: oom-pod-1
spec:
  containers:
    - name: container-1
      image: busybox
      command: ["/bin/sh"]
      args: ["-c", "dd if=/dev/zero of=/dev/null"]
      resources:
        limits:
          memory: "100Mi"
```

## Identifying the Error

1. **Container Configuration**: The container is configured to run the `dd` command, which continuously consumes memory by copying data from `/dev/zero` to `/dev/null`.

2. **Memory Limit**: The memory limit for the container is set to `100Mi`, indicating that the container cannot consume more than 100 megabytes of memory.

3. **OOMKilled Error**: Since the `dd` command consumes memory continuously without bound, it quickly exceeds the memory limit of `100Mi`. When this happens, the kernel terminates the container, and an OOMKilled error occurs.

## Troubleshooting Steps

To troubleshoot and address the OOMKilled error in this scenario, follow these steps:

### Step 1: Review Pod Configuration

- Check the YAML file (`oom-pod-1.yaml`) to ensure that the pod and container configurations are accurate.

### Step 2: Increase Memory Limit

- Consider whether the container's memory limit (`100Mi`) is appropriate for your workload. If the application requires more memory, increase the memory limit accordingly.

### Step 3: Optimize the Command

- Review the command executed by the container (`dd if=/dev/zero of=/dev/null`). Determine if some optimizations or changes can reduce memory consumption.

