# Kubernetes Cluster Demo

```bash
# TODO
Kubernetes master is running at https://172.32.128.10:443
Elasticsearch is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/elasticsearch-logging/proxy
Heapster is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/heapster/proxy
Kibana is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/kibana-logging/proxy
KubeDNS is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/kube-dns/proxy
Grafana is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/monitoring-grafana/proxy
InfluxDB is running at https://172.32.128.10:443/api/v1/namespaces/kube-system/services/monitoring-influxdb/proxy
```

#### Kubernetes Concepts

  `Cluster:` A cluster is a set of physical or virtual machines and other infrastructure resources used by Kubernetes to run your applications.

  `Node:` A node is a physical or virtual machine running Kubernetes, onto which pods can be scheduled.

  `Pod:`A pod is a co-located group of containers and volumes.

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

$ kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

$ kubectl expose deployment hello-minikube --type=NodePort

$ kubectl get pods

$ curl $(minikube service hello-minikube --url)
```

## Playground

1. Creating a namespace with the specified name:

```bash
$ kubectl create namespace brazil
```

2. Switching the context:

```bash
$ kubectl config set-context minikube-brazil --namespace=brazil --cluster=minikube --user=minikube
$ config use-context minikube-brazil
```

3. Creating a service:

```bash
$ kubectl create -f redis-master-service.yaml
```

4. Creating a deployment:

```bash
$ kubectl create -f redis-master-deployment.yaml
```

## Notes

### Creating a Service and its Replications Controller

It's typically best to create a service before corresponding replication controllers, so that the scheduler can spread the pods comprising the service.

### Best Practices

  - Don't use `hostPort` (which specifies the port number to expose on the host) unless absolutely necessary. When you bind a `Pod` to a `hostPort`, there are a limited number of places that pod can be scheduled, due to port conflicts.
  - Avoid using `hostNetwork`, for the same reasons as `hostPort`.
  - Use headless services for easy service discovery when you don’t need kube-proxy load balancing.

### Deleting a ReplicationController and its Pods

To delete a ReplicationController and all its pods, use kubectl delete. Kubectl will scale the ReplicationController to zero and wait for it to delete each pod before deleting the ReplicationController itself. If this kubectl command is interrupted, it can be restarted.

When using the REST API or go client library, you need to do the steps explicitly (scale replicas to 0, wait for pod deletions, then delete the ReplicationController).
Deleting just a ReplicationController

### Deleting just a ReplicationController

You can delete a ReplicationController without affecting any of its pods.

Using `kubectl`, specify the `--cascade=false` option to kubectl delete.

When using the REST API or go client library, simply delete the ReplicationController object.

Once the original is deleted, you can create a new ReplicationController to replace it. As long as the old and new .spec.selector are the same, then the new one will adopt the old pods. However, it will not make any effort to make existing pods match a new, different pod template. To update pods to a new spec in a controlled way, use a rolling update.
Isolating pods from a ReplicationController

### Isolating pods from a ReplicationController

Pods may be removed from a ReplicationController's target set by changing their labels. This technique may be used to remove pods from service for debugging, data recovery, etc. Pods that are removed in this way will be replaced automatically (assuming that the number of replicas is not also changed).
Com

### Deleting Deployments

When you want to kill your application, delete your Deployment, as in the Quick start:

```bash
$ kubectl delete deployment my-nginx
deployment "my-nginx" deleted
```

By default, this will also cause the pods managed by the Deployment to be deleted. If there were a large number of pods, this may take a while to complete. If you want to leave the pods running instead, specify --cascade=false.

If you try to delete the pods before deleting the Deployments, it will just replace them, as it is supposed to do.

## Sources

  - https://kubernetes.io/docs/user-guide/
  - https://kubernetes.io/docs/api-reference/v1/definitions/
  - https://kubernetes.io/docs/getting-started-guides/scratch/
  - https://kubernetes.io/docs/user-guide/deploying-applications/
  - https://kubernetes.io/docs/user-guide/config-best-practices/
