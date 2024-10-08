+++
title = 'Chapter 6'
date = 2024-10-05T09:03:50-05:00
draft = false
weight = 6
+++
# **IP routing Essentials**

###### 1) What is an AS?
{{% expand title="Answer" %}}
An **AS** or **Autonomous System** (AS) is a connected group of IP networks managed by a single administrative entity, such as a university, government or a commercial organization.
{{% /expand %}}

###### 2) What is an IGP?
{{% expand title="Answer" %}}
An **IGP** or **Interior Gateway Protocol** is protocol that works best for the communication between IP networks within a single AS.

*E.g:* RIP, OSPF, EIFRP, ISIS
{{% /expand %}}

###### 3) What is an EGP?
{{% expand title="Answer" %}}
An *EGP* or **Exterior Gateway Protocol** is protocol that is suited for the communication between ASs.
{{% /expand %}}

###### 4) What is the primary function of an IP routing protocol?
{{% expand title="Answer" %}}
The primary function of an IP routing protocol is ensuring data packets can travel efficiently from source to destination.
{{% /expand %}}

###### 5) Can you explain the difference between distance vector and link-state routing protocols?
{{% expand title="Answer" %}}
|#|Categories|Distance Vector|Link-State|
|-|----------|---------------|----------|
|1|Algorithm Used|Uses the **Bellman-Ford algorithm** to calculate the best path based on distance (usually hop count) from a router to the destination.|Uses **Dijkstra’s algorithm** to compute the shortest path based on a complete map of the network.|
|2|Routing Information|Routers only share information with directly connected neighbors, and routers do not have a full view of the network. Instead, they rely on cumulative information passed through the network.|Each router has a complete view of the network by building and maintaining a full topology map of all routers within the network.|
|3|Updates |Routers periodically send updates whether there is a change on the network or not. Each update always contains the entire routing table to their neighbors.|Routers only send updates when there is a change in the network topology (link state updates), and they only send the changed information, not the entire routing table.|
|4|Convergence Time|Generally slower to converge due to periodic updates and reliance on incremental changes from neighbors.|Faster convergence as routers have a complete view of the network and can independently calculate the shortest paths when a change occurs.|
|5|Scalability|Less scalable, especially in large networks, because it doesn’t have a full view of the topology and relies on periodic updates.|More scalable in large networks due to faster convergence and efficient, event-driven updates.|
|6|Loop Prevention|Requires mechanisms like **split horizon**, **route poisoning**, and **hold-down timers** to prevent routing loops.|Since routers have a full network map, routing loops are naturally prevented.|
|7|Resource Usage|Less CPU and memory intensive, as routers maintain only neighbor information and routing tables.|More resource-intensive, requiring more memory and CPU to maintain and process the entire network topology.|
|8|Examples|**RIP** (Routing Information Protocol). **EIGRP** (Enhanced Interior Gateway Routing Protocol) – Cisco proprietary but adds advanced|**OSPF** (Open Shortest Path First), **IS-IS** (Intermediate System to Intermediate System)|
|9|Route Calculation|Routers rely on neighbors to calculate routes. Each router trusts the information received from its neighbors without verifying the entire network topology.|Each router calculates routes independently based on the complete network topology, resulting in a more accurate and reliable route selection.|
|10|Network Type Suitability|Suitable for smaller or less complex networks where simplicity and minimal resource usage are prioritized.|Better suited for large, complex networks where fast convergence and scalability are required.|
{{% /expand %}}

###### 6) What algorithm is used by distance vector routing protocols to determine the best path?
{{% expand title="Answer" %}}
The Bellman-Ford algorithm.
{{% /expand %}}

###### 7) How does the link-state routing algorithm work, and which protocols typically use it?
{{% expand title="Answer" %}}
It uses Dijkstra's algorithm to calculate the shortest path by constructing a full map of the network.
{{% /expand %}}

###### 8) Define a path vector algorithm and provide an example of a protocol that uses it.
{{% expand title="Answer" %}}
The path vector algorithm is used to determine the best route to a destination by tracking the entire path that routing information has traversed from source to destination. BGP uses a path vector algorithm called **AS_PATH**.
{{% /expand %}}

###### 9) What is the significance of prefix length in routing?
{{% expand title="Answer" %}}
It defines the size of the network portion of an IP address and helps in selecting the most specific route for packet forwarding.
{{% /expand %}}

###### 10) How does a router use administrative distance (AD) to select the best route?
{{% expand title="Answer" %}}
Administrative distance is a value that indicates the trustworthiness of a route source. In other words, when you have multiple protocol running on the same router and each learning a path towards a specific destination, the RIB (Router Iformation Base) table will only accept the route from the protocol with the lowest AD as it is deemed the most trustworthy.

|Route Origin|Default Administrative Distance|
|------------|-------------------------------|
|Directly connected interface|0|
|Static route|1|
|EIGRP Summary route|5|
|External BGP (eBGP) route|20|
|EIGRP Internal route|90|
|OSPF route|110|
|IS-IS route|115|
|RIPv2 route|120|
|EIGRP (External) route|170|
|Internal BGP (iBGP) route|200|
{{% /expand %}}

###### 11) What factors contribute to a route’s metric, and why is it important in path selection?
{{% expand title="Answer" %}}
Factors include bandwidth, delay, load, and hop count; the metric determines the "cost" of a route, helping the router choose the most efficient path.
{{% /expand %}}

###### 12) Describe the concept of static routing and when it is typically used in a network.
{{% expand title="Answer" %}}
Static routing involves manually configuring routes; it’s used in small, simple networks, for backup routes in larger networks or on device with low ressouces.
{{% /expand %}}

###### 13) What is a floating static route, and how does it differ from a regular static route?
{{% expand title="Answer" %}}
A floating static route is a static route for which the default AD of 1 has been changed to a value higher than that of the primary route to serve as a backup route.
{{% /expand %}}

###### 14) How is a static route configured to direct traffic to a null interface?
{{% expand title="Answer" %}}
This command  which discards traffic, often for security or summarization purposes.
```
ip route <destination> <mask> null0
```
{{% /expand %}}

###### 15) What are some advantages of using IPv6 static routes over IPv4 static routes?
{{% expand title="Answer" %}}
IPv6 provides simplified routing with auto-configuration features, larger address space, and better hierarchical network design.
{{% /expand %}}

###### 16) Explain the concept of policy-based routing (PBR) and provide a real-world example of its use.
{{% expand title="Answer" %}}
By default, the router makes forwarding decisions based on the destination IP address. But with PBR, the router can make forwarding decisions based on other factors such as:
- source IP address
- protocol type (ICMP, TCP, UDP, etc...)
- destination IP address
{{% /expand %}}

###### 17) What role does Virtual Routing and Forwarding (VRF) play in modern networks?
{{% expand title="Answer" %}}
VRF  is a technology used in networking to create multiple, isolated instances of a routing table within the same router or Layer 3 device. Each VRF instance operates as a separate and independent logical router, allowing different networks or tenants to use the same IP address ranges without interfering with each other. VRF is commonly used in multi-tenant environments, service provider networks, and large enterprise networks.
{{% /expand %}}

###### 18) In what scenarios would you implement static routes to null interfaces?
{{% expand title="Answer" %}}
To prevent routing loops or to discard unwanted traffic, typically in route summarization or security implementations.
{{% /expand %}}

###### 19) What steps are involved in configuring a basic static route?
{{% expand title="Answer" %}}
Identify the destination network, subnet mask, and next-hop address or exit interface, then configure with the `ip route` command.
{{% /expand %}}

###### 20) How does floating static routing provide redundancy?
{{% expand title="Answer" %}}
It offers a backup route with a higher administrative distance that becomes active only when the primary route fails.
{{% /expand %}}

###### 21) Why is the administrative distance of a route important in the context of static routing?
{{% expand title="Answer" %}}
It determines the preference of routes when multiple routes to the same destination exist, ensuring the most reliable one is used.
{{% /expand %}}

###### 22) What are some common issues that might arise when implementing policy-based routing, and how can they be resolved?
{{% expand title="Answer" %}}
Misconfigurations leading to traffic being incorrectly routed; resolving requires careful review of access lists and route-maps.
{{% /expand %}}

###### 23) How does IP routing interact with VRF to enable multiple virtual routing tables within a single router?
{{% expand title="Answer" %}}
Each VRF maintains a separate routing table, allowing the router to handle different routing domains without overlap.
{{% /expand %}}