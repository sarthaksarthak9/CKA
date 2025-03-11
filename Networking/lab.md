## Notes
- deploy the ingress to the same namespace where is application is deploy

### LAB Explore Env

Q3) What is the network interface configured for cluster connectivity on the controlplane node? <br>
`kubectl get nodes controlplane -o wide`
then `ip a | grep -B2 <ip>`
or you can use `ip link`

Q4) What is the MAC address of the interface on the controlplane node?
`ip link show <interface name>`

Q5) What is the MAC address assigned to node01?
- `first check ip of node`
- `ip a | grep -B2 <ip-addr>`

`ip link show <interface name>`

- To mention all the bridge: `ip address show type bridge`

Q9) If you were to ping google from the controlplane node, which route does it take?
What is the IP address of the Default Gateway?

`ip route show default`

Q10) What is the port the kube-scheduler is listening on in the controlplane node?
`netstat -nplt | grep scheduler`

- nplt is a flag 

Q12)

Correct! That's because 2379 is the port of ETCD to which all control plane components connect to. 2380 is only for etcd peer-to-peer connectivity. When you have multiple controlplane nodes. In this case we don't.

### LAB CNI

Q1) Inspect the kubelet service and identify the container runtime endpoint value is set for Kubernetes.
- `ps -aux | grep kubelet | grep --color container-runtime-endpoint`

- /etc/cni/net.d 
- /opt/cni/bin 


### LAB networking weave

Q3) How many weave agents/peers are deployed in this cluster?
`kubectl get pods -n kube-system and count weave pods`

Q5) Identify the name of the bridge network/interface created by weave on each node.
`ip link`

Q6) What is the POD IP address range configured by weave?
`ip addr show weave`

Q7) What is the default gateway configured on the PODs scheduled on node01?
`SSH to the node01 by running the command: ssh node01 and then run the ip route command and look at the weave line.`

### LAB Service Networking (do it again)

Q1) What network range are the nodes in the cluster part of?
`ip addr and look at the IP address assigned to the eth0 interfaces`

Q2) What is the range of IP addresses configured for PODs on this cluster?
`The network is configured with weave. Check the weave pods logs using the command kubectl logs <weave-pod-name> weave -n kube-system and look for ipalloc-range.`

Q3) What is the IP Range configured for the services within the cluster?
`cat /etc/kubernetes/manifests/kube-apiserver.yaml   | grep cluster-ip-range`

Q4) What type of proxy is the kube-proxy configured to use?
`Check the logs of the kube-proxy pods. Run the command: kubectl logs <kube-proxy-pod-name> -n kube-system`

Q5) How does this Kubernetes cluster ensure that a kube-proxy pod runs on all nodes in the cluster?
`kubectl get ds -n kube-system`

### Lab CoreDNS

Q1) Identify the DNS solution implemented in this cluster.
`kubectl get pods -n kube-system and look for the DNS pods`

Q5) Where is the configuration file located for configuring the CoreDNS service?
`kubectl -n kube-system describe deployments.apps coredns | grep -A2 Args | grep Corefile`

Q6) How is corefile pass on pod?
`as a config map` 

Q8) What is the root domain/zone configured for this kubernetes cluster?
`kubectl describe configmap coredns -n kube-system`

Q10) What name can be used to access the hr web server from the test Application?

Q11) What name can be used to access the hr web server from the test Application?
`kubectl get svc after viewing the available services, write the correct service name and port.`

Q14) We just deployed a web server - webapp - that accesses a database mysql - server. However the web server is failing to connect to the database server. Troubleshoot and fix the issue.

`They could be in different namespaces. First locate the applications. The web server interface can be seen by clicking the tab Web Server at the top of your terminal.`

Q15) From the hr pod nslookup the mysql service and redirect the output to a file /root/CKA/nslookup.out
`kubectl exec -it hr -- nslookup mysql.payroll > /root/CKA/nslookup.out`

### Ingress Lab 1

Q2) Which namespace is the Ingress Controller deployed in?
`k get all -A`

Q6) Which namespace is the Ingress Resource deployed in?
`kubectl get ingress --all-namespaces`

Q8) What is the Host configured on the Ingress Resource?
`kubectl describe ingress --namespace <name of ns>`

Q11) If the requirement does not match any of the configured paths in the Ingress, to which service are the requests forwarded?

- Execute the command kubectl describe ingress --namespace app-space and examine the Default backend field. 
- If it displays <default>, proceed to inspect the ingress controller's manifest by executing kubectl get deploy ingress-nginx-controller -n ingress-nginx -o yaml. 
- In the manifest, search for the argument --default-backend-service

Q22)You are requested to make the new application available at /pay.
- Create a new Ingress for the new pay application in the critical-space namespace.

- Use the command `kubectl get svc -n critical-space` to know the service and port details.

### Ingress Lab 2


### Gateway

Q1) The Gateway resource is used to define an instance of a Gateway API implementation. It acts as an entry point for traffic into the cluster. GatewayClass defines a type of Gateway, but not an actual instance.

Q2) The allowedRoutes field determines which namespaces can bind their HTTPRoute, TCPRoute, or other routes to the Gateway. Setting namespaces.from: All allows routes from all namespaces to attach.

Q3) The Kubernetes Gateway API supports HTTP, HTTPS, TCP, UDP, and TLS protocols.

Q4) A GatewayClass is similar to an IngressClass; it defines the controller-specific behavior of a Gateway. A Gateway is an instance that references a GatewayClass to determine its underlying implementation.

Q5) 
The Gateway API provides more advanced routing capabilities than Ingress, including:

- Multi-protocol support (HTTP, TCP, UDP, etc.)
- Better extensibility with Routes and Filters
- More granular access control using AllowedRoutes
- Unlike Ingress, which is primarily HTTP-based, Gateway API is designed for flexibility across multiple protocols.

Q6)

To use the Gateway API, a controller is required. In this lab, we will install NGINX Gateway Fabric as the controller. Follow these steps to complete the installation:

Install the Gateway API resources
`kubectl kustomize "https://github.com/nginx/nginx-gateway-fabric/config/crd/gateway-api/standard?ref=v1.5.1" | kubectl apply -f -`

Deploy the NGINX Gateway Fabric CRDs
`kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/crds.yaml`

Deploy NGINX Gateway Fabric
`kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/nodeport/deploy.yaml`

Verify the Deployment
`kubectl get pods -n nginx-gateway`

View the nginx-gateway service
`kubectl get svc -n nginx-gateway nginx-gateway -o yaml`

Update the nginx-gateway service to expose ports 30080 for HTTP and 30081 for HTTPS
`kubectl patch svc nginx-gateway -n nginx-gateway --type='json' -p='[
  {"op": "replace", "path": "/spec/ports/0/nodePort", "value": 30080},
  {"op": "replace", "path": "/spec/ports/1/nodePort", "value": 30081}
]'`


Q7) Gateway 

```
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: nginx-gateway
  namespace: nginx-gateway
spec:
  gatewayClassName: nginx
  listeners:
    - name: http
      port: 80
      protocol: HTTP
      allowedRoutes: 
       namespaces: 
        from: All
```


Q8) A new pod named frontend-app and a service called frontend-svc have been deployed in the default namespace. Expose the service on the / path by utilizing an HTTPRoute named frontend-route.


```
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: frontend-route
  namespace: default
spec:
  parentRefs:
  - name: nginx-gateway
    namespace: nginx-gateway
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /
    backendRefs:
    - name: frontend-svc
      port: 80
```













