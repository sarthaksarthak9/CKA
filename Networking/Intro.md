## MAC ADDR and IP ADDR

1. Different Layers of Operation: <br>
MAC Address: Operates at the Data Link Layer (Layer 2) of the OSI model. It is a hardware address embedded in the network interface card (NIC) of a device. It is used for communication within the same local network segment (e.g., Ethernet or Wi-Fi).<br>

IP Address: Operates at the Network Layer (Layer 3). It is a logical address used for routing data between different networks (e.g., across the internet).<br>

2. Purpose of MAC Address:<br>
Local Network Communication: MAC addresses are used to uniquely identify devices within the same local network. When data is sent within a local network (e.g., between your computer and your router), the MAC address ensures the data reaches the correct device.<br>

Switching: Network switches use MAC addresses to forward data to the correct port on a local network.<br>

No Two Devices Have the Same MAC Address: MAC addresses are globally unique, which prevents conflicts in local network communication.<br>

3. Purpose of IP Address:<br>
Global Routing: IP addresses are used to identify devices across different networks. They enable data to be routed across the internet or between different subnets.<br>

Logical Addressing: IP addresses can change (e.g., dynamic IP assignment via DHCP), and they are not tied to a specific hardware device.<br>

Hierarchical Structure: IP addresses are organized in a way that makes routing efficient across large networks like the internet.<br>

4. Why Both Are Needed:<br>
MAC Address for Local Delivery: When data is sent over a network, the IP address is used to route the data to the correct network, but the MAC address is used to deliver the data to the specific device within that network.<br>

Example: If you send a packet to a device on the same local network, your device uses the MAC address to ensure the packet reaches the correct device. If the device is on a different network, the IP address is used to route the packet to the correct network, and then the MAC address is used for the final delivery.<br>

5. ARP (Address Resolution Protocol):<br>
ARP is used to map IP addresses to MAC addresses within a local network. When a device wants to send data to another device on the same network, it uses ARP to find the MAC address associated with the destination IP address.<br>

Summary:<br>
MAC Address: Ensures data is delivered to the correct device within a local network.<br>

IP Address: Ensures data is routed to the correct network and device across the internet or between networks.<br>

Without MAC addresses, local network communication would not work efficiently, and without IP addresses, global communication across networks would not be possible. Both are essential for the functioning of modern networks.<br>


## Swicth
## Route
## Gateway
## DNS
## Core DNS

## Network Namespace
### route table
### arp table
### pipe
### bridge

## Docker Networking
### none network
### host network
### Port Mapping
### Nat Table (refere notebook notes)


### Nat

#### NAT Table in Linux (iptables)

Network Address Translation (NAT) is a method used to modify the source or destination IP address of packets as they pass through a router or firewall.<br>

The NAT (Network Address Translation) table in iptables is responsible for modifying packet source or destination addresses to enable communication between different networks.<br>

`Why Do We Need NAT?`

- Private IPs Can't Access the Internet → Converts local IPs (192.168.x.x) to a public IP.
- Multiple Devices Behind One Public IP → Allows many systems to share a single public IP.
- Port Forwarding & Load Balancing → Redirects traffic from one IP/port to another.


## CNI


