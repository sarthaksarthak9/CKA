## PV lab

Q5

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-log
spec:
  persistentVolumeReclaimPolicy: Retain
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/log
```

Q9

Q11 You requested for 50Mi, how much capacity is now available to the PVC?

Q14 What happen to pv when pvc delete?

Q16 The PVC was still being used by the webapp pod when we issued the delete command. Until the pod is deleted, the PVC will remain in a terminating state.

## Storage Classes

Q3) What is the name of the Storage Class that does not support dynamic volume provisioning? 

The local-storage storage class makes use of the no-provisioner and currently does not support dynamic provisioning.

Refer to the tab above the terminal (called Local Storage) to read more about it.

Q9) The StorageClass used by the PVC uses WaitForFirstConsumer volume binding mode. This means that the persistent volume will not bind to the claim until a pod makes use of the PVC to request storage.