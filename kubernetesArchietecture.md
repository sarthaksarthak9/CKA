## Cluster Architecture
A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods.
The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

![image](https://github.com/user-attachments/assets/1e864d6a-4589-492b-a388-c48ac0cec871)

## Control plane components
The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a Deployment's replicas field is unsatisfied).

### kube-apiserver 
The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.
It is responsible for authenticating and validating req, retreving and updating data in etcd and ** it is the only component that directly interact with etcd data store **

The main implementation of a Kubernetes API server is kube-apiserver. kube-apiserver is designed to scale horizontally—that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.

### etcd
Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

** Listen on (2739) port **

### kube-controller-manager
It monitors the state of various components within the system and work towards to bringing the whole system to the desired functioning state.

** each controller ** is a seprate process but for simpilicity they are all compiled into a single binary and run in a single process.

some of the controller : 1. Node controller 2. Replication controller

controllers are packaged into a single process called kubernetes-control-manager

### kube-Scheduler
it responsible for ** deciding ** which pod goes on which node, it doesn't place pod on the node and that's the job of kubelet

## Node Component

### kubelet

it is like a captain of a ship. They lead all the activities. They do all the paper ** work necessary to become part of the cluster. ** It is the ** sole point of contact from the mastership. ** Load and Unload container as ** instructed by scheduler. ** It also send back reports at regular interval about ** status of conatiner. **

###### we always manually install kubelet on our worker node.

### Kube-Proxy
it is a process that runs on each node in a kubernetes cluter, its job to look for new services, & every time when a service is created, it create appropriate rules on each node to forward traffic to backend.

### Pods
containers encapsulated inside the pod. It is the smallest object that we can create in kubernetes. A pod can have multiple distinct container.

### Container runtime
A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.
Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface).





