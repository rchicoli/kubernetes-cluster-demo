# Kubernetes Cluster Demo

#### Kubernetes Concepts

`Cluster:` A cluster is a set of physical or virtual machines and other infrastructure resources used by Kubernetes to run your applications.

`Node:` A node is a physical or virtual machine running Kubernetes, onto which pods can be scheduled.

`Pod:` A pod is a co-located group of containers and volumes.

`Label:` A label is a key/value pair that is attached to a resource, such as a pod, to convey a user-defined identifying attribute. Labels can be used to organize and to select subsets of resources.

`Selector:` A selector is an expression that matches labels in order to identify related resources, such as which pods are targeted by a load-balanced service.

`Replication Controller:` A replication controller ensures that a specified number of pod replicas are running at any one time. It both allows for easy scaling of replicated systems and handles re-creation of a pod when the machine it is on reboots or otherwise fails.

`Service:` A service defines a set of pods and a means by which to access them, such as single stable IP address and corresponding DNS name.

`Volume:` A volume is a directory, possibly with some data in it, which is accessible to a Container as part of its filesystem. Kubernetes volumes build upon Docker Volumes, adding provisioning of the volume directory and/or device.

`Secret:` A secret stores sensitive data, such as authentication tokens, which can be made available to containers upon request.

`Name:` A user- or client-provided name for a resource.

`Namespace:` A namespace is like a prefix to the name of a resource. Namespaces help different projects, teams, or customers to share a cluster, such as by preventing name collisions between unrelated teams.

`Annotation:` A key/value pair that can hold larger (compared to a label), and possibly not human-readable, data, intended to store non-identifying auxiliary data, especially data manipulated by tools and system extensions. Efficient filtering by annotation values is not supported.

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

```bash
$ kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
```

```bash
kubectl expose deployment hello-minikube --type=NodePort
```

```bash
$ kubectl get pod
```

```bash
$ curl $(minikube service hello-minikube --url)
```
