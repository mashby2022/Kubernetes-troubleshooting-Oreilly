# Understanding OOMKilled Error in Kubernetes

The **OOMKilled** error in Kubernetes indicates that a container or pod has been terminated because it has used more memory than it has been allocated. The acronym OOM stands for **"Out Of Memory."**

## Overview

OOMKilled, commonly known as **Exit Code 137**, is a type of error that originated in Linux. The **OOM** (Out of Memory) Manager is a tool on Linux systems that keeps track of memory usage by processes. When the system is about to run out of memory, the **OOM Killer** intervenes and begins killing processes to free up memory and avoid a crash. Its purpose is to free up as much RAM as possible while killing as few processes as feasible.

Kubernetes allows pods to restrict the amount of resources their containers can use on the host computer. A pod can set a memory limit (the maximum amount of memory the container can use) and a memory request (the minimum amount of memory the container should consume). If a container exceeds its memory limit, it is terminated with an **OOMKilled** status. Moreover, if the total memory usage across all containers or pods on a node exceeds a certain threshold, one or more pods may be terminated.

## Types of OOMKilled Errors

There are two types of **OOMKilled** errors in Kubernetes:

### OOMKilled: Limit Overcommit

This error occurs when the sum of pod limits is greater than the available memory on the node. Kubernetes will not allocate pods that require more RAM than the node has available. However, limits can be higher than requests, leading to overcommitment, where the total of all limits exceeds the node's capacity.

### OOMKilled: Container Limit Reached

This error is more specific and affects only one pod. When a pod exceeds its configured memory limit, Kubernetes kills it with the **OOMKilled — Container Limit Reached**error. This often results in a container dying, one pod becoming unhealthy, and Kubernetes restarting that pod.

## Troubleshooting OOMKilled Errors

### Diagnosis

To diagnose OOMKilled errors:

1. **Gather Information**: Run the command `kubectl describe pod [name]` and save the output to a text file for future use.

2. **Check for Exit Code 137**: Inspect the events section of the describe pod text file. The container was terminated with Exit Code 137 because it ran out of memory.

### Solutions

#### If the Pod Was Terminated Due to a Container Limit

- Check if your application truly needs more memory. If so, increase the memory limit for the container in the pod specification.

- Investigate for memory leaks in the application if memory usage unexpectedly increases. Debug the app to find the source of the memory leak. Increasing the memory limit will consume more resources.

#### If the Pod Was Terminated Due to Overcommit on the Node

- Understand why Kubernetes killed the pod and adjust limit values and memory requests to prevent overcommitment.

- Constantly monitor your environment, grasp the memory behavior of pods and containers, and review settings to diagnose and resolve Kubernetes memory issues.

## Conclusion

In conclusion, the Kubernetes OOMKilled error, rooted in Linux, aids Kubernetes in managing memory when scheduling pods and deciding which pods to kill when resources become scarce. Understanding both types of OOMKilled errors (Container Limit Reached and Limit Overcommit) is essential for effective troubleshooting and reducing the chances of encountering this error in the future.
