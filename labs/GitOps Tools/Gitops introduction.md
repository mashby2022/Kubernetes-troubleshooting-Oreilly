# Introduction to GitOps and GitOps Tools: Argo CD and Flux

## What is GitOps?

**GitOps** is a modern approach to managing and automating the deployment and configuration of applications in Kubernetes clusters. It leverages the principles of version control and Git repositories to ensure that the desired state of your infrastructure and applications is defined in code and kept in sync with the actual state of your Kubernetes clusters.

GitOps revolves around the following key concepts:

- **Version Control**: All configuration and deployment manifests, as well as infrastructure definitions, are stored in a Git repository. This allows teams to track changes over time, collaborate, and roll back to previous states if needed.

- **Declarative Configuration**: GitOps relies on declarative configuration, where the desired state of the system is explicitly defined in code. This declarative approach ensures that the system's configuration is well-documented and easily understandable.

- **Automation**: GitOps tools automate the process of deploying, updating, and managing applications in Kubernetes clusters based on the configurations stored in Git repositories. Any changes pushed to the repository trigger automatic synchronization with the cluster.

- **Observability**: GitOps tools provide insights into the state of applications and infrastructure in real-time. Teams can monitor deployments, track changes, and receive alerts if the actual state deviates from the desired state.

## Argo CD

**Argo CD** is a powerful GitOps tool that specializes in the continuous delivery and management of applications in Kubernetes environments. It offers the following features:

- **Declarative Git Repositories**: Argo CD watches Git repositories for changes in application configurations and ensures that the cluster's state matches the definitions in the repository.

- **Web-Based UI**: Argo CD provides a user-friendly web interface for managing applications, monitoring deployments, and configuring synchronization policies.

- **Multi-Cluster Support**: It can manage multiple Kubernetes clusters, making it suitable for complex multi-cluster deployments.

### How to Install Argo CD
Requirements:
- Installed `kubectl` command-line tool.
- Have a kubeconfig file (default location is `~/.kube/config`).
- CoreDNS. Can be enabled for microk8s by running `microk8s enable dns && microk8s stop && microk8s start`.

Installation Steps:
1. Create a new namespace for Argo CD:
   ```bash
   kubectl create namespace argocd
   ```

2. Apply the Argo CD installation manifest:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. (Optional) If you don't need UI, SSO, or multi-cluster features, you can install core Argo CD components only:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
   ```

4. Access the Argo CD API Server using one of the following methods:
   - Service Type Load Balancer
   - Ingress
   - Port Forwarding

5. Login to Argo CD using the CLI:
   ```bash
   argocd login <ARGOCD_SERVER>
   ```

6. (Optional) Register a cluster to deploy apps to.

7. Create an application from a Git repository.

8. Sync (Deploy) the application.

9. Manage your applications with Argo CD

## Flux

**Flux** is another GitOps tool that automates the deployment and updates of applications in Kubernetes clusters. Its key features include:

- **Automated Synchronization**: Flux continuously synchronizes the Git repository's contents with the Kubernetes cluster, automatically applying changes.

- **Customizable Controllers**: It supports various controllers for managing Helm charts, Kustomize overlays, and plain YAML manifests, allowing you to define your deployment patterns.

- **Image Automation**: Flux offers automated image updates, ensuring that applications use the latest container images available.

### How Flux Works
Flux works by reconciling the state of your Kubernetes cluster with the state described in your Git repository. It continuously monitors the repository for changes and applies them to the cluster.

### How to Install Flux

#### Using Brew (Homebrew):

If you're on macOS or Linux and have Homebrew installed, you can install Flux with the following command:

```bash
brew install flux
```

#### Using Bash (Shell Script):

You can use a shell script to install Flux. Here's an example:

```bash
curl -s https://fluxcd.io/install.sh | bash
```

#### Using Yay (Arch Linux Package Manager):

If you're using Arch Linux or an Arch-based distribution, you can use Yay to install Flux:

```bash
yay -S fluxctl
```

#### Using Nix (Nix Package Manager):

If you're using the Nix package manager, you can install Flux with the following command:

```bash
nix-env -iA fluxctl -f https://github.com/fluxcd/flux/releases/download/1.24.0/fluxctl_linux_amd64
```

#### Using Chocolatey (Windows Package Manager):

On Windows, you can use Chocolatey to install Flux:

```bash
choco install flux
```

