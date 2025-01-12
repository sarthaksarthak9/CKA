- If pod is pending state, then it might be because of no scheduler
- If nodeName field is empty pod is not scheduled and if not, then a pod is assigned to a node
- To manually schedule a pod we have to modify the pod-definition file

```
apiVersion: v1
kind: Pod
metadata:
 name: nginx
 labels:
  name: nginx
spec:
 containers:
 - name: nginx
   image: nginx
   ports:
   - containerPort: 8080
 nodeName: node02
```

## Labels and Selector

- Labels define at two places. Once which is under metadata are labels of replica-set
- Labels under template sections are labels configured on the pods.
- Selector and Template labels must be matched

## LAB Manual Schedulin

-  kubectl get pods --namespace kube-system to see the status of scheduler pod. We have removed the scheduler from this Kubernetes cluster. As a result, as it stands, the pod will remain in a pending state forever.





