# Download a release

Kubernetes binaries:

https://console.cloud.google.com/storage/browser/kubernetes-release/release/v1.5.2/bin/linux/amd64/

Minikube: 

https://github.com/kubernetes/minikube/releases

# Enabling shell autocompletion

echo "source <(kubectl completion bash)" >> ~/.bashrc

# Minikube Features

  - Minikube supports Kubernetes features such as:
    - DNS
    - NodePorts
    - ConfigMaps and Secrets
    - Dashboards
    - Container Runtime: Docker, and rkt
    - Enabling CNI (Container Network Interface)
    - Ingress

# Quickstart

To create a kubernetes cluster, run the following command:

```bash
$ minikube start --vm-driver=virtualbox
```
