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