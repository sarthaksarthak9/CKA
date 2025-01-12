## Static Pods

The pods created by kubelet on its own without the intervention from the API Server or rest of the kubernetes cluster components 

## Path (kubelet.service)

The designated directory can be any directory on the host and the location of that directory is passed in to the kubelet as an option while running the service.

The option is named as --pod-manifest-path.


## To find static pod

Run the command **kubectl get pods --all-namespaces** and look for those with -controlplane appended in the name

## Tips 

- Identify the in which node static pods running
- To delete static pod, rm the static pod definition file 

## kubelet.service path

- /etc/systemd/system/kubelet.service


## config file path

- /var/lib/kubelet