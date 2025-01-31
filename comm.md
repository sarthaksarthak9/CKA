# Commands

1. kubectl create -f yml file
2. kubectl edit
3. kubectl replace -f yml file
4. k replace --force -f yml file

## Namespace
1. k get ns
2. k get pods -n=nameofns
3. k run <podname> --image=redis -n=nameofns
4. k create ns/namespace nameofns

## SVC
1. k expose pod pod-name --port=port-number --name=svc-name

## Deployment
1. k create deployment deployment-name --image=img-name --replicas=nofreplica

## Expose a Pod as a service

1. k run httpd --image=httpd:alpine --port=80  <br>
Then <br>
k expose pod httpd --type=ClusterIP --target-port=80 <br>
            or <br>
 kubectl run httpd --image=httpd:alpine --port=80 --expose

## Scheduler

1. k taint node node-name key=value:taint-effect
2. **To remove the taint (impt)** : k taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
3. k label node node01 color=blue

## Static Pods
1. docker ps (to view it as kubectl use api server)

2. **To find static Pod:** Run the command kubectl get pods --all-namespaces and look for those with -controlplane appended in the name

## Metrics-Server
kubectl top is a command in Kubernetes that provides resource usage statistics (CPU and memory) for nodes and pods in your cluster <br>

1. kubectl top pod 

2.  kubectl top node explain

3. To view the logs

```
kubectl logs -f <pod-name>
```
If there are multiple containers in a pod then you must specify the name of the container explicitly in the command.

```
kubectl logs -f <pod-name> <container-name>
```  

## Rollout 

- k rollout status deployment/deploy-name
- k rollout history deployment/deploy-name
- k rollout undo deployment/myapp-deployment
- k set image deployment/myapp-deployment nginx=nginx:1.9.1

## Env variable

1. k run webapp-green --image=kodecloud/webapp -- --color green // -- separates kubectl arguments from arguments passed to the container

# ConfigMap

1. kubectl create configmap my-config \
  --from-literal=ENV_VAR_NAME=value \
  --from-literal=ANOTHER_VAR=another_value \
  --from-file=app-config.properties

2. kubectl create configmap  webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard


## Secrets 



## Cluster-Maintainence

1. You can purposefully drain the node of all the workloads so that the workloads are moved to other nodes.
```
kubectl drain node-1
```

2. The node is also cordoned or marked as unschedulable.
```
k cordon node-1
```

3. When the node is back online after a maintenance, it is still unschedulable. You then need to uncordon it.
```
kubectl uncordon node-1
```


## Os-Upgrades 

1. kubeadm upgrade plans // to see the lastest v available
2. apt-get upgrade -y kubeadm=1.12.0 // to upgrade to a version
                    or
   kubeadm upgrade apply v1.12.0

3. apt-get upgrade -y kubelet=1.12.0

4. kubectl drain node01 --ignore-daemonsets

##### To take a snapshot of etcd database
```
ETCDCTL_API=3 etcdctl | snapshot save <path/name-snapshot>
```

##### To restore backup
```
ETCDCTL_API=3 etcdctl | snapshot restore snapshot.db | --data-dir /var/lib/etcd-from-backup
```
when etcd restore, it initialize a new cluster

#### To switch between cluster
```
kubectl config use-context nameofcluster
```

Q) What is the IP address of the External ETCD datastore used in cluster2?

you can inspect the process on the controlplane node on cluster2 as shown below:
```
ssh cluster2-controlplane ps -ef | grep --color=auto etcd
```
Alternatively, inspect the kube-apiserver pod and look at the value used for --etcd-servers

Q2) How many nodes are part of the ETCD cluster that etcd-server is a part of?


Check the members of the cluster:

etcd-server ~ ➜  ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/etcd/pki/ca.pem \
  --cert=/etc/etcd/pki/etcd.pem \
  --key=/etc/etcd/pki/etcd-key.pem \
   member list
59ee55985632d394, started, etcd-server, https://192.160.244.3:2380, https://192.160.244.3:2379, false

etcd-server ~ ➜  
This shows that there is only one member in this cluster.



Q3)







