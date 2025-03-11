### Manual Scaling

Q4) Can the kubectl scale command be used to scale down a statefulset in Kubernetes? <br>

The kubectl scale command can be used to scale both deployments and statefulsets. When scaling a statefulset, Kubernetes ensures that the state and order of the pods are maintained, unlike in deployments where pods can be created and destroyed in any order.<br>

Q6) When you scale a deployment to a higher number of replicas than the cluster can support due to resource constraints, Kubernetes will create as many replicas as possible within the available resources. The remaining replicas will be in a pending state until sufficient resources are freed up or added to the cluster. This behavior allows Kubernetes to manage resources dynamically while maintaining the desired state as closely as possible.


### HPA

Q9) The HPA status shows /80 for the CPU target. what could be a possible reason? <br>

If the status of the Horizontal Pod Autoscaler (HPA) target is UNKNOWN/80, it typically means that the HPA is unable to retrieve the current metrics for the specified target. Run kubectl describe hpa nginx-deployment to find more details.


Q10) `k get hpa --watch`


## VPA(2025)

Q5) `kubectl get deployments -n kube-system | grep vpa`

Q6) Here is a command that picks the name of the vpa-updater pod and prints its logs:

`kubectl logs $(kubectl get pods -n kube-system --no-headers -o custom-columns=":metadata.name" | grep vpa-updater) -n kube-system`

This command first retrieves the pod name using kubectl get pods and then pipes it to the kubectl logs command to print the logs of the vpa-updater pod.

You will see output similar to this:


## Modifying CPU resources in vpa

Q6) Capture the recommended target CPU value from the flask-app VPA and store it in /root/target.

