# Google Kubernetes Engine Setup
## Prerequisites

### Google Cloud Platform
This tutorial leverages the [Google Cloud Platform](https://cloud.google.com/) to streamline provisioning of the compute infrastructure required to bootstrap a Kubernetes cluster from the ground up. [Sign up](https://cloud.google.com/free/) for $300 in free credits.
### Google Cloud Platform SDK

#### Install the Google Cloud SDK

Follow the Google Cloud SDK [documentation](https://cloud.google.com/sdk/) to install and configure the `gcloud` command line utility.

Verify the Google Cloud SDK version is 338.0.0 or higher:

```
gcloud version
```

#### Set a Default Compute Region and Zone

This tutorial assumes a default compute region and zone have been configured.

If you are using the `gcloud` command-line tool for the first time `init` is the easiest way to do this:

```
gcloud init
```

Then be sure to authorize gcloud to access the Cloud Platform with your Google user credentials:

```
gcloud auth login
```

Next set a default compute region and compute zone:

```
gcloud config set compute/region us-west1
```

Set a default compute zone:

```
gcloud config set compute/zone us-west1-c
```

> Use the `gcloud compute zones list` command to view additional regions and zones.

# Create a Cluster and Deploy a Workload on Google Kubernetes Engine (GKE)

Learn how to get started with Google Kubernetes Engine by creating a Kubernetes cluster and deploying a workload to the cluster.

## Overview

A Kubernetes cluster provides compute, storage, networking, and other services for applications, similar to a virtual data center. Apps and their associated services that are running in Kubernetes are called workloads.

Before you begin, make sure to enable the Kubernetes Engine API and billing for your Google Cloud project.

## Create a Cluster in GKE Autopilot Mode

In Autopilot mode, Google manages your cluster configuration, including scaling, security, and other preconfigured settings. Clusters in Autopilot mode are optimized to run most production workloads and provision compute resources based on your Kubernetes manifests.

1. Visit the Kubernetes Engine page in the Google Cloud console.
2. Create or select a project.
3. Wait for the API and related services to be enabled. This can take several minutes.
4. Make sure that billing is enabled for your Google Cloud project.

## Creating the Cluster

1. In the Google Cloud console, go to the GKE Clusters page.
   - [Go to Clusters](https://console.cloud.google.com/kubernetes/list/overview?_ga=2.39370083.1589486115.1705951100-684263645.1705951088)

2. Click Create.

3. Under Cluster basics, do the following:
   - In the Name field, enter "hello-world-cluster".
   - Keep the default values for the rest of the settings and click Create to start creating the cluster.

4. When you're redirected back to the Kubernetes clusters page, click "hello-world-cluster" in the Name column.

5. You can watch the progress of your cluster as it is being configured, deployed, and verified.

6. Wait until you see a check mark next to the "hello-world-cluster" page title.

## Deploying a Sample App to Your Cluster

1. In the Google Cloud console, go to the GKE Workloads page.
   - [Go to Workloads](https://console.cloud.google.com/kubernetes/workload/overview?_ga=2.39370083.1589486115.1705951100-684263645.1705951088)

2. Click Deploy.

3. Leave "Existing container image" selected, and in Image path enter the following path:
   - `us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0`

4. Click Continue to move to the Configuration section.

5. In Deployment name, enter "hello-world-app".

6. In Kubernetes Cluster, select "hello-world-cluster".

7. Click Continue.

8. In the Expose section, create a load balancing Kubernetes Service to direct external requests to your app:
   - Select "Expose deployment as a new service".
   - Leave Port 1 set to 80.
   - In Target port 1, enter 8080.

9. Click Deploy.

10. GKE automatically assigns an available external IP address to the Service.

11. Wait until the deployment completes, and you see the Deployment details page.

This completes the process of creating a GKE cluster and deploying a workload to it.
