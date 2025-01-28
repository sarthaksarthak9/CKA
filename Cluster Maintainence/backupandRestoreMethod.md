/// See Notes

1. ETCD Cluster (place where all cluster related info is stored)
2. Persistant Volume (also use as a backup storage)

3. When we use decleartive approach for deploy, we store config files in github but when we use imperative approach it might be possible that a team does not document it anywhere

4. **A better way** to backing up resource config is to query KUBE-API server. <br>
Query the kube-api server directly or accessing API server directly & save all resource config for all obj created on cluster as a copy.

```k get all --all-namespace -o yaml > all-deploy-svc.yml``` backup command to get all pod, deployment, service in all namespace in yml format & storing it in a file. But it do for one resource group, there are so many.

```Velero```  it help in taking backups of kubernetes cluster using kubernetes API.

5. Etcd hosted on master node and while config ectd we specified a dir where all data would be stored, the ```data DIR```

##### To take a snapshot of etcd database
```
ETCDCTL_API=3 etcdctl | snapshot save <path/name-snapshot>
```

##### To restore backup
```
ETCDCTL_API=3 etcdctl | snapshot restore snapshot.db | --data-dir /var/lib/etcd-from-backup
```
when etcd restore, it initialize a new cluster
