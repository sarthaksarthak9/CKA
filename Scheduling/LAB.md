## Lab Admission Controllers

Q3) To check the plugin which is enable 
`/etc/kubernetes/manifests/kube-apiserver.yaml`


Q4) To create a pod in a namespace implicit
`k run nginx --image=nginx -n=blue`


Q5) To enable the NamespaceAutoProvision admission controllerAt /etc/kubernetes/manifests/kube-apiserver.yaml
`- --enable-admission-plugins=NodeRestriction,NamespaceAutoProvision`
`- --disable-admission-plugins=`


Q6 Since the kube-apiserver is running as pod you can check the process to see enabled and disabled plugins.

`ps -ef | grep kube-apiserver | grep admission-plugins`



### NOTE
Note that the NamespaceExists and NamespaceAutoProvision admission controllers are deprecated and now replaced by NamespaceLifecycle admission controller.<br>

The NamespaceLifecycle admission controller will make sure that requests to a non-existent namespace is rejected and that the default namespaces such as default, kube-system and kube-public cannot be deleted.


## Lab Validating and Mutating Admission Controllers

Q2) What is the flow of invocation of admission controllers?
- first mutating and then validating

Q3) To create Tls secret
`kubectl create secret tls webhook-server-tls --cert=/root/keys/webhook-server-tls.crt --key=/root/keys webhook-server-tls.key -n webhook-demo`
