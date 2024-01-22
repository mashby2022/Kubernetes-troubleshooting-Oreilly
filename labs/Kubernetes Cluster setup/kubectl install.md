# kubectl - Kubernetes Command-line Tool

The Kubernetes command-line tool, kubectl, is a powerful utility that enables you to interact with Kubernetes clusters efficiently. Whether you want to deploy applications, manage cluster resources, inspect configurations, or view logs, kubectl provides the necessary commands to get the job done.
## Installation

To start using kubectl, you need to install it on your system. It is available for a variety of operating systems, including Linux, macOS, and Windows. Follow the installation instructions based on your preferred platform:

- [Install kubectl on macOS](#installing-and-setting-up-kubectl-on-macos)
- [Install kubectl on Linux](#installing-and-setting-up-kubectl-on-linux)
- [Install kubectl on Windows](#installing-and-setting-up-kubectl-on-windows)

## Installing and Setting Up kubectl on macOS

### Prerequisites
Before you begin, ensure that you use a kubectl version that is within one minor version difference of your Kubernetes cluster. Using the latest compatible version of kubectl helps avoid unforeseen issues.

### Method 1: Install with Homebrew on macOS
If you are using the Homebrew package manager on macOS, you can easily install kubectl with the following command:

```bash
brew install kubectl
```

#### Test to ensure the installed version is up-to-date
```bash
kubectl version --client
```

### Method 2: Install kubectl binary with curl on macOS

#### Intel (x86_64)
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"
```

**Note**: To download a specific version, replace the `$(curl -L -s https://dl.k8s.io/release/stable.txt)` portion of the command with the specific version. For example, to download version 1.29.1 on Intel macOS, use:

```bash
curl -LO "https://dl.k8s.io/release/v1.29.1/bin/darwin/amd64/kubectl"
```

#### Make the kubectl binary executable
```bash
chmod +x ./kubectl
```

#### Move the kubectl binary to a file location on your system PATH
```bash
sudo mv ./kubectl /usr/local/bin/kubectl
sudo chown root: /usr/local/bin/kubectl
```

**Note**: Ensure that `/usr/local/bin` is in your PATH environment variable.

#### Test to ensure the installed version is up-to-date
```bash
kubectl version --client
```

#### Method 3: Install with Macports on macOS
If you are using the Macports package manager on macOS, you can install kubectl with the following commands:

```bash
sudo port selfupdate
sudo port install kubectl
```

#### Test to ensure the installed version is up-to-date
```bash
kubectl version --client
```

After installing and validating kubectl, you can safely delete the checksum file:

```bash
rm kubectl.sha256
```

You have successfully installed and set up kubectl on macOS. You can now use it to interact with your Kubernetes clusters.
## Installing and Setting Up kubectl on Linux

### Before you begin
You must use a kubectl version that is within one minor version difference of your cluster. For example, a v1.29 client can communicate with v1.28, v1.29, and v1.30 control planes. Using the latest compatible version of kubectl helps avoid unforeseen issues.

### Install kubectl on Linux
The following methods exist for installing kubectl on Linux:

#### Install kubectl binary with curl on Linux
Download the latest release with the command:

- x86-64

   ```
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   ```

   Note:
   To download a specific version, replace the `$(curl -L -s https://dl.k8s.io/release/stable.txt)` portion of the command with the specific version.

   For example, to download version 1.29.1 on Linux x86-64, type:

   ```
   curl -LO https://dl.k8s.io/release/v1.29.1/bin/linux/amd64/kubectl
   ```

- ARM64

   ```
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
   ```

   Validate the kubectl binary against the checksum file:

   ```
   echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
   ```

   If valid, the output is:

   ```
   kubectl: OK
   ```

   If the check fails, `sha256` exits with nonzero status and prints output similar to:

   ```
   kubectl: FAILED
   sha256sum: WARNING: 1 computed checksum did NOT match
   ```

   Note: Download the same version of the binary and checksum.

#### Install kubectl

```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Note:
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:

```
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
# and then append (or prepend) ~/.local/bin to $PATH
```

Test to ensure the version you installed is up-to-date:

```
kubectl version --client
```

Or use this for a detailed view of the version:

```
kubectl version --client --output=yaml
```

#### Install using native package management
- Debian-based distributions
- Red Hat-based distributions
- SUSE-based distributions

Update the apt package index and install packages needed to use the Kubernetes apt repository:

```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
```

Download the public signing key for the Kubernetes package repositories. The same signing key is used for all repositories so you can disregard the version in the URL:

```
# If the folder `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

Note: In releases older than Debian 12 and Ubuntu 22.04, folder `/etc/apt/keyrings` does not exist by default, and it should be created before the curl command.

Add the appropriate Kubernetes apt repository. If you want to use Kubernetes version different than v1.29, replace v1.29 with the desired minor version in the command below:

```
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Note: To upgrade kubectl to another minor release, you'll need to bump the version in `/etc/apt/sources.list.d/kubernetes.list` before running `apt-get update` and `apt-get upgrade`. This procedure is described in more detail in Changing The Kubernetes Package Repository.

Update apt package index, then install kubectl:

```
sudo apt-get update
sudo apt-get install -y kubectl
```

#### Install using other package management
- Homebrew

If you are on Linux and using Homebrew package manager, kubectl is available for installation.

```
brew install kubectl
kubectl version --client
```
## Installing and Setting Up kubectl on Windows

Before you begin, ensure that you use a kubectl version that is within one minor version difference of your cluster to avoid compatibility issues.

### Install kubectl binary with curl on Windows

You can download the latest kubectl binary for Windows using the following command:

```shell
curl.exe -LO "https://dl.k8s.io/release/v1.29.1/bin/windows/amd64/kubectl.exe"
```

You can also validate the binary and verify its checksum for security:

```shell
curl.exe -LO "https://dl.k8s.io/v1.29.1/bin/windows/amd64/kubectl.exe.sha256"

# Manually compare CertUtil's output to the checksum file downloaded:
CertUtil -hashfile kubectl.exe SHA256
type kubectl.exe.sha256

# Or use PowerShell to automate the verification:
$(Get-FileHash -Algorithm SHA256 .\kubectl.exe).Hash -eq $(Get-Content .\kubectl.exe.sha256)
```

After downloading and validating, add the folder containing the kubectl binary to your PATH environment variable.

To check the installed kubectl version, run:

```shell
kubectl version --client
```

### Install kubectl on Windows using Package Managers

You can also install kubectl on Windows using package managers like Chocolatey, Scoop, or winget:

#### Chocolatey:

```shell
choco install kubernetes-cli
```

#### Scoop:

```shell
scoop install kubectl
```

#### winget:

```shell
winget install -e --id Kubernetes.kubectl
```

To ensure the version you installed is up-to-date, run:

```shell
kubectl version --client
```

After installation, you can configure kubectl by creating a `.kube` directory in your home directory and a `config` file within it. Edit the `config` file as needed to use a remote Kubernetes cluster.
