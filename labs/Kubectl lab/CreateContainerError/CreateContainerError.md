# CreateContainerError (Incorrect Image Specification or Runtime Error): Causes and Resolution

## Diagnosis

CreateContainerError occurs when a container is transitioning from pending to running. To identify it, use the `kubectl get pods` command and check the pod status.

## Common Causes and Resolutions

Here's a summary of the main causes of CreateContainerError and how to resolve them, mostly related to YAML configuration errors:

| CAUSE                                  | RESOLUTION                                         |
| --------------------------------------| --------------------------------------------------|
| Incorrect image specification          | Add a valid command to start the container.       |
| Runtime error                         | Identify the error and modify image specification to resolve it. |
| Insufficient resources                | Retrieve kubelet logs and resolve or reinstall the node. |
| Missing mounted object                | Create the missing mounted object in the namespace. |

## Diagnosis and Resolution Steps

Follow these steps to diagnose the cause of CreateContainerError and resolve it:

**Step 1: Gather Information**

Run the following command and save the content to a text file for future reference:

```shell
kubectl describe pod [name] > /tmp/troubleshooting_describe_pod.txt
```

**Step 2: Examine Pod Events Output**

Check the Events section of the describe pod text file for messages such as:

- `no command specified`
- `starting container process caused`
- `container name [...] is already in use by container`
- `is waiting to start`

**Step 3: Troubleshoot**

If the error is **"no command specified"**:

- Both image and pod configurations didn't specify a valid command to start the container.
- Edit the configurations and add a valid command to start the container.

If the error is **"starting container process caused"**:

- Identify the error message following the "container process caused" message. This indicates the error that occurred when starting the container.
- Modify the image or the container start command to resolve the error. For example, if the error is "executable file not found," ensure the file exists in the image with the correct path and name.

If the error is **"container name [...] is already in use by container"**:

- The container runtime didn't clean up an older container with the same name.
- Sign in with root access on the node and check the kubelet log, usually located at `/var/log/kubelet.log`.
- Identify the issue in the kubelet log and resolve it, which may involve reinstalling the container runtime, kubelet, and re-registering the node with the cluster.

If the error is **"waiting to start"**:

- This indicates that an object mounted by the container is missing, which could be a storage volume or other required object.
- Review the pod manifest and check all objects mounted by the pod or container. Verify their availability in the same namespace. Create them if missing or adjust the manifest to point to an available object.

Please note that these procedures address the most common causes of CreateContainerError. If none of the quick fixes work, a more complex diagnosis procedure may be required to identify and resolve the issue within the Kubernetes environment.
