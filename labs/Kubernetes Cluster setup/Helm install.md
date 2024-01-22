# Helm Installation

This guide demonstrates how to install the Helm CLI, which allows you to manage charts and deploy applications on Kubernetes clusters. Helm can be installed in various ways, including binary releases, installation scripts, and package managers.

### Community-Supported Package Managers

The Helm community offers methods to install Helm through various operating system package managers. Please note that these methods are not officially supported by the Helm project and are considered third-party installations.

#### From Homebrew (macOS)

The Helm community maintains a Homebrew formula for Helm, which is generally up to date. You can install Helm on macOS using:

```bash
brew install helm
```

#### From Chocolatey (Windows)

For Windows users, the Helm community provides a Helm package for Chocolatey, which is typically kept up to date:

```bash
choco install kubernetes-helm
```

#### From Scoop (Windows)

Another option for Windows users is to install Helm via Scoop, a command-line installer:

```bash
scoop install helm
```

#### From Apt (Debian/Ubuntu)

Debian/Ubuntu users can install Helm through Apt with the following commands:

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

#### From dnf/yum (Fedora)

Starting from Fedora 35, Helm is available in the official repository. You can install Helm on Fedora with the following command:

```bash
sudo dnf install helm
```

#### From Snap

The Snapcrafters community maintains a Snap package for Helm, which can be installed as follows:

```bash
sudo snap install helm --classic
```

#### From pkg (FreeBSD)

FreeBSD users can install Helm from the FreeBSD Ports Collection using:

```bash
pkg install helm
```
