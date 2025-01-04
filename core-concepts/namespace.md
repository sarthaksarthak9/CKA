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

## LABS (see question 6 and 7)

1. If an application is within the same ns as svc then we can access (if a db available) a db using svc name
(In Kubernetes, Services provide a stable way to access applications running in Pods. When two applications (or components) are in the same namespace, you can use the Service name directly to communicate between them. This is because Kubernetes automatically sets up DNS resolution for Services within the same namespace.)

2. When applications and Services are in different namespaces in Kubernetes, you need to use the fully qualified domain name (FQDN) or a shorthand notation to access the Service. This is because Kubernetes DNS resolves Service names within the context of their namespace.
(svcname.ns.svc.cluster.local)

## Commands

- **To change ns:** kubectl config set-context --current --namespace=dev


