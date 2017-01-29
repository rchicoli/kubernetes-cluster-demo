# Kubernetes Cluster Demo

## Creating a Custom Cluster from Scratch

### Download a release

A Kubernetes binary release includes all the Kubernetes binaries as well as the supported release of etcd. Download the binaries from the official kubernetes release.

https://console.cloud.google.com/storage/browser/kubernetes-release/release/v1.5.2/bin/linux/amd64/

### Enabling shell autocompletion

```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
```

## Running Kubernetes Locally via Minikube

Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.

https://github.com/kubernetes/minikube/releases

### Minikube Features

  - Minikube supports Kubernetes features such as:
    - DNS
    - NodePorts
    - ConfigMaps and Secrets
    - Dashboards
    - Container Runtime: Docker, and rkt
    - Enabling CNI (Container Network Interface)
    - Ingress

### Quickstart

To create a kubernetes cluster, run the following command:

```bash
$ minikube start --vm-driver=virtualbox
```
