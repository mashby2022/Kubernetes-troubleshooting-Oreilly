# Exercise: Identify the OOMKilled Error

In this exercise, you will analyze a Kubernetes YAML configuration and identify the type of OOMKilled error it may encounter.

### YAML File 2:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: oom-pod-2
spec:
  containers:
    - name: container-1
      image: nginx
      resources:
        limits:
          memory: "10Mi"
```

**Instructions:**

1. Examine the provided YAML configuration (`oom-pod-2.yaml`) for a Kubernetes pod.

2. Identify any characteristics in the YAML file that might lead to an OOMKilled error.

3. Specifically, focus on the following aspects:
   - Container configuration
   - Memory limits


**Note:** The YAML file represents a Kubernetes pod configuration, and the goal is to identify potential issues related to memory consumption that could lead to an OOMKilled error.
```
