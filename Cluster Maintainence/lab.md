## Lab 1

```
kubectl drain node01 --ignore-daemonsets
```


question 12




## Lab 2  [question 9]

To seamlessly transition from Kubernetes v1.30 to v1.31 and gain access to the packages specific to the desired Kubernetes minor version, follow these essential steps during the upgrade process. This ensures that your environment is appropriately configured and aligned with the features and improvements introduced in Kubernetes v1.31.

##### On the controlplane node:

Use any text editor you prefer to open the file that defines the Kubernetes apt repository.

```vim /etc/apt/sources.list.d/kubernetes.list```<br>
Update the version in the URL to the next available minor release, i.e v1.31.

deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /

After making changes, save the file and exit from your text editor. 

##### Proceed with the next instruction.
```
apt update
apt-cache madison kubeadm
```
Based on the version information displayed by apt-cache madison, it indicates that for Kubernetes version 1.31.0, the available package version is 1.31.0-1.1. Therefore, to install kubeadm for Kubernetes v1.31.0, use the following command:

```
apt-get install kubeadm=1.31.0-1.1
```

##### Run the following command to upgrade the Kubernetes cluster.
```
kubeadm upgrade plan v1.31.0
kubeadm upgrade apply v1.31.0
```
Note that the above steps can take a few minutes to complete.

Now, upgrade the Kubelet version. Also, mark the node (in this case, the "controlplane" node) as schedulable.
```
apt-get install kubelet=1.31.0-1.1
```
Run the following commands to refresh the systemd configuration and apply changes to the Kubelet service:
```
systemctl daemon-reload
systemctl restart kubelet
```


## LAB 3

##### Restore ETCD data 

First Restore the snapshot:

root@controlplane:~# ETCDCTL_API=3 etcdctl  --data-dir /var/lib/etcd-from-backup \
snapshot restore /opt/snapshot-pre-boot.db


2022-03-25 09:19:27.175043 I | mvcc: restore compact to 2552
2022-03-25 09:19:27.266709 I | etcdserver/membership: added member 8e9e05c52164694d [http://localhost:2380] to cluster cdf818194e3a8c32
root@controlplane:~# 


Note: In this case, we are restoring the snapshot to a different directory but in the same server where we took the backup (the controlplane node) As a result, the only required option for the restore command is the --data-dir.



Next, update the ```/etc/kubernetes/manifests/etcd.yaml:```

We have now restored the etcd snapshot to a new path on the controlplane - /var/lib/etcd-from-backup, so, the only change to be made in the YAML file, is to change the hostPath for the volume called etcd-data from old directory (/var/lib/etcd) to the new directory (/var/lib/etcd-from-backup).

```
  volumes:
  - hostPath:
      path: /var/lib/etcd-from-backup
      type: DirectoryOrCreate
    name: etcd-data
 ```   
With this change, /var/lib/etcd on the container points to /var/lib/etcd-from-backup on the controlplane (which is what we want).

When this file is updated, the ETCD pod is automatically re-created as this is a static pod placed under the /etc/kubernetes/manifests directory.



Note 1: As the ETCD pod has changed it will automatically restart, and also kube-controller-manager and kube-scheduler. Wait 1-2 to mins for this pods to restart. You can run the command: watch "crictl ps | grep etcd" to see when the ETCD pod is restarted.

Note 2: If the etcd pod is not getting Ready 1/1, then restart it by kubectl delete pod -n kube-system etcd-controlplane and wait 1 minute.

Note 3: This is the simplest way to make sure that ETCD uses the restored data after the ETCD pod is recreated. You don't have to change anything else.



If you do change --data-dir to /var/lib/etcd-from-backup in the ETCD YAML file, make sure that the volumeMounts for etcd-data is updated as well, with the mountPath pointing to /var/lib/etcd-from-backup (THIS COMPLETE STEP IS OPTIONAL AND NEED NOT BE DONE FOR COMPLETING THE RESTORE)


## LAB 4 q5 q13

To switch between cluster
```
kubectl config use-context nameofcluster
```

Q) Take a backup of etcd on cluster1 and save it on the student-node at the path /opt/cluster1.db


On the student-node:

First set the context to cluster1:
student-node ~ ➜  kubectl config use-context cluster1
Switched to context "cluster1".
Next, inspect the endpoints and certificates used by the etcd pod. We will make use of these to take the backup.

student-node ~ ✖ kubectl describe  pods -n kube-system etcd-cluster1-controlplane  | grep advertise-client-urls
      --advertise-client-urls=https://192.160.244.10:2379

student-node ~ ➜  

student-node ~ ➜  kubectl describe  pods -n kube-system etcd-cluster1-controlplane  | grep pki
      --cert-file=/etc/kubernetes/pki/etcd/server.crt
      --key-file=/etc/kubernetes/pki/etcd/server.key
      --peer-cert-file=/etc/kubernetes/pki/etcd/peer.crt
      --peer-key-file=/etc/kubernetes/pki/etcd/peer.key
      --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
      --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
      /etc/kubernetes/pki/etcd from etcd-certs (rw)
    Path:          /etc/kubernetes/pki/etcd

student-node ~ ➜
NOTE: The IP address (192.160.244.10) shown in the above command could be different in your lab environment. Make sure to note the correct IP address before taking the backup of the cluster.

SSH to the controlplane node of cluster1 and then take the backup using the endpoints and certificates we identified above:

cluster1-controlplane ~ ➜  ETCDCTL_API=3 etcdctl --endpoints=https://192.160.244.10:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/cluster1.db
Snapshot saved at /opt/cluster1.db

cluster1-controlplane ~ ➜  
Finally, copy the backup to the student-node. To do this, go back to the student-node and use scp as shown below:

student-node ~ ➜  scp cluster1-controlplane:/opt/cluster1.db /opt
cluster1.db                                                                                                        100% 2088KB 112.3MB/s   00:00    

student-node ~ ➜