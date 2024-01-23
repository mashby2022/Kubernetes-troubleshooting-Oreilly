
### Exercise: Identify the Type of OOMKilled Error

Consider the following YAML configuration:

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

Based on the provided YAML configuration, analyze and determine the type of OOMKilled error that may occur. To do this, consider the following questions:

After analyzing the YAML configuration, provide your assessment of the type of OOMKilled error that may occur and briefly explain why based on the information in the YAML.
