## Solutions

**Understanding the 'up' Metric**

The 'up' metric is a fundamental health indicator in Prometheus. It represents the reachability of a target (pods, services, etc.) by Prometheus itself. A value of 1 indicates the target is reachable, while a value of 0 means it's unreachable. This helps you quickly assess the overall health of your monitored components.

**PromQL Exploration**

**a. Total CPU Usage:**

```
sum by (namespace, pod) (rate(container_cpu_usage_seconds_total{namespace="default"}[1m]))
```

* **Explanation:** This PromQL query calculates the total CPU usage across all pods in the "default" namespace.
   * `sum by (namespace, pod)`: This part groups the results by namespace and pod, allowing us to see the CPU usage per pod.
   * `rate(container_cpu_usage_seconds_total{namespace="default"}[1m])`: This calculates the rate of CPU usage in seconds over the last 1 minute for all containers, filtered to only include pods in the "default" namespace.

**b. HTTP Errors:**

```
sum by (job) (increase(http_requests_total{status_code=~"5.*"}[5m]))
```

* **Explanation:** This PromQL query finds the total number of HTTP requests with a status code of 500 or higher over the last 5 minutes.
   * `sum by (job)`: This groups the results by job, which typically corresponds to your application or service.
   * `increase(http_requests_total{status_code=~"5.*"}[5m])`: This calculates the increase in the number of HTTP requests with status codes starting with "5" (like 500, 502, etc.) over the last 5 minutes. The `~` symbol allows matching patterns in PromQL.


***


### Creating a Basic Alert 


**2. Alerting Rule Introduction:**


Let's define a rule that proactively notifies us when Nginx pods approach their memory limits:

**3. YAML Code Block:**

```yaml
groups:
- name: Nginx Memory Alert
  rules:
  - alert: NginxHighMemoryUsage
    expr: avg_over_time(container_memory_usage_bytes{container_name="nginx"} / container_memory_limits_bytes{container_name="nginx"}[1m]) > 0.8
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: "Nginx pod memory usage is high (instance {{ $labels.instance }})"
      description: "Pod {{ $labels.pod }} is using over 80% of its memory limit.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```

**4. Explanation:**


**Explanation:** This YAML code defines an alerting rule that triggers if the average memory usage of any Nginx pod exceeds 80% of its memory limit for more than 2 minutes.

* **groups:** Defines a group name for better organization of alerts.
* **alert:** Specifies the name of the specific alert within the group.
* **expr:** Defines the PromQL expression that determines when the alert should trigger. Here, it calculates the average memory usage of Nginx pods as a percentage of their limits over the last 1 minute and checks if it's greater than 0.8 (80%).
* **for:** Sets the duration for which the expression needs to evaluate to `true` before the alert triggers (2 minutes in this case).
* **labels:**  Defines labels associated with the alert, like its severity (warning).
* **annotations:** Provides a human-readable summary and detailed description of the alert when it triggers. The `{{ }}` notation allows referencing dynamic values like pod names and labels. 



