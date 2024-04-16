**Getting Started with Prometheus Monitoring**

**Prerequisites**

* A running Kubernetes cluster (Kind is a great choice for this experiment).
* Basic understanding of Kubernetes concepts (pods, services).

**Environment Setup**

1. **Deploy a Sample Application:**

   ```bash
   kubectl create deployment nginx --image=nginx
   kubectl expose deployment nginx --port=80 --type=NodePort
   ```

2. **Install Prometheus using Helm:**

   (Assuming Helm is already installed)

   ```bash
   helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   helm repo update
   kubectl create namespace monitoring 
   helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring 
   ```

**Accessing the Prometheus Dashboard**

1. **Find NodePort:**

   ```bash
   kubectl get service prometheus-server --namespace monitoring 
   ```
   (Note the NodePort under the PORT column)

2. **Access in Browser:**

   Open `http://<Node-IP>:<NodePort>` in your browser (replace with actual values).

**Practice Problems**

1. **Basic Metrics Exploration**

   * In the Prometheus expression browser, search for "up". Explain what this metric represents.
   * Try graphing `container_memory_usage_bytes`. What does it show?

2. **Understanding PromQL**

   * Calculate the total CPU usage across all pods in the "default" namespace.  (Hint: use the `sum by()` function).
   * Find HTTP requests returning a status code of 500 or higher. (Hint: Look for `http_requests_total` metric). 

3. **Creating a Basic Alert**

   * Set up an alert that triggers if the average memory usage of any Nginx pod exceeds 80% of its limit. (Hint: Look into the `avg_over_time()` function and Prometheus' alerting rules).

