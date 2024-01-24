# Deploying Prometheus on a Kind cluster using Helm

## Prerequisites: [Setting up kind cluster](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubernetes%20Cluster%20setup/Kind%20setup.md)

## Kube-Prometheus-stack

Kube-prometheus stack is a collection of Kubernetes manifests and Prometheus rules, providing easy-to-operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Helm must be installed to use the charts [Helm installation](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/Kubernetes%20Cluster%20setup/Helm%20install.md)

### 1. Helm Repository

Add prometheus and stable repo to the local helm repository

```bash
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo add stable https://charts.helm.sh/stable
$ helm repo update
```

### 2. Create namespace monitoring to deploy all services in that namespace.

```bash
$ kubectl create namespace monitoring
namespace/monitoring created
```

### 3. Install kube-prometheus stack. The services will be exposed on NodePort:

- Prometheus: 30000
- AlertManager: 32000

```bash
#helm install [RELEASE_NAME] prometheus-community/kube-prometheus-stack
$ helm install kind-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set prometheus.service.type=NodePort --set alertmanager.service.nodePort=32000 --set alertmanager.service.type=NodePort --set prometheus-node-exporter.service.nodePort=32001 --set prometheus-node-exporter.service.type=NodePort
```

### 4. Validate kube-prometheus-stack has been installed.

**Step 1:** Check its status by running:

```bash
$ kubectl --namespace monitoring get pods -l release=kind-prometheus
```

**Step 2:** Check all the components in the stack:

```bash
$ kubectl get all --namespace monitoring
```


The following services can also be exposed using NodePort during install using helm by specifying the NodePort

- kube-prometheus-stack-operator
- kube-state-metrics
- prometheus-node-exporter
