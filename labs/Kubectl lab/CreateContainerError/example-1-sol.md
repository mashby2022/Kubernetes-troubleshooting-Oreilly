# Troubleshooting CreateContainerError - Incorrect Image Name

In this exercise, we will identify and troubleshoot a `CreateContainerError` related to an incorrect image name in a Kubernetes Pod configuration YAML file.

## YAML File Description

YAML File 2 represents a Kubernetes Pod configuration with an incorrect image name specification. Here's the YAML file:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: create-container-error-2
spec:
  containers:
    - name: container-1
      image: my-app  # Missing image tag
```

### Error Identification

The error in this YAML file is that the image name is provided without a tag (e.g., my-app instead of my-app:latest or a specific tag). This incomplete image specification will lead to a `CreateContainerError` because Kubernetes cannot determine which image version to use.

## Troubleshooting Steps

To troubleshoot and resolve the `CreateContainerError` caused by an incorrect image name, follow these steps:

### 1. Add Image Tag

Edit the YAML file and provide a specific image tag or version. For example, change `image: my-app` to `image: my-app:latest` or specify a valid tag.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: create-container-error-2
spec:
  containers:
    - name: container-1
      image: my-app:latest  # Provide a valid image tag
```

### 2. Apply the Updated YAML

Save the changes to the YAML file and apply it using `kubectl apply -f <filename.yaml>`. This will create the pod with the corrected image specification.

```bash
kubectl apply -f <filename.yaml>
```

### 3. Verify the Pod Status

Check the status of the pod to ensure it has been created successfully without any `CreateContainerError`.

```bash
kubectl get pods
```


## Conclusion

By following these troubleshooting steps, you can correct the incorrect image name issue that leads to a `CreateContainerError` in your Kubernetes Pod configuration.

Remember to always provide a valid image name and tag to ensure successful container creation.
```

