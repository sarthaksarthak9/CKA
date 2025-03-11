## Application Failure
Q2)
- port: The port that the Service exposes internally within the cluster.
- targetPort: The port on the Pod where the actual MySQL database is running.

## ControlPlane Failure
Q4) Something is wrong with scaling again. We just tried scaling the deployment to 3 replicas. But it's not happening.

- Check the volume mount path in kube-controller-manager manifest file at /etc/kubernetes/manifests.
Just as we did in the previous question, inspect the logs of the kube-controller-manager pod:

root@controlplane:/etc/kubernetes/manifests# kubectl -n kube-system logs kube-controller-manager-controlplane
I0916 13:17:27.452539       1 serving.go:348] Generated self-signed cert in-memory
unable to load client CA provider: open /etc/kubernetes/pki/ca.crt: no such file or directory

root@controlplane:/etc/kubernetes/manifests# 
It appears the path /etc/kubernetes/pki is not mounted from the controlplane to the kube-controller-manager pod. If we inspect the pod manifest file, we can see that the incorrect hostPath is used for the volume:

WRONG:

- hostPath:
      path: /etc/kubernetes/WRONG-PKI-DIRECTORY
      type: DirectoryOrCreate
CORRECT:

- hostPath: 
    path: /etc/kubernetes/pki 
    type: DirectoryOrCreate 

## WorkNode Failure
Q1) Fix the broken cluster 

- Step1. Check the status of services on the nodes.

- Step2. Check the service logs using journalctl -u kubelet.

- Step3. If it's stopped then start the stopped services.

- Step 2: SSH to node01 and check the status of the container runtime (containerd, in this case) and the kubelet service

Q3) The cluster is broken again. Investigate and fix the issue.

- Check the kubelet.conf file at /etc/kubernetes/kubelet.conf.   server: https://controlplane:6443
- Restart the kubelet service after this change.

## Networking Failure


