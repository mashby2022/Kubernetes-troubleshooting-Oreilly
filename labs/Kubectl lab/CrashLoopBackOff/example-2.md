# Exercise: Identify the CrashLoopBackOff Error

## YAML File Description

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

## Task
1. Review the provided YAML file.
2. Identify the issue in the file that would result in a `CrashLoopBackOff` error when attempting to create the Pod.
3. Describe what is causing the error and why it leads to a `CrashLoopBackOff`.
4. Suggest a possible fix or correction for the issue.
