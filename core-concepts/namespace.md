## Namespaces
It provide a mechanism to isolate group of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.)

### Kubernetes starts with four initial namespaces:

- default
Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace.

- kube-node-lease
This namespace holds Lease objects associated with each node. Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure.

- kube-public
This namespace is readable by all clients (including those not authenticated). This namespace is mostly reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.

- kube-system
kubernetes create a set of pods, services for it internal purpose such as those req by networking solutions, dns svc, etc. To isolate them from user and prevent you to modify svc, kubernetes creates it under another ns name kube-system

###### format = nameofsvc.ns.sub-domainforsvc.domain (when a svc is created a dns entry is added automatically in this format)

## Commands

- **To change ns:** kubectl config set - context $(kubectl config current-context) -- namespace = dev


