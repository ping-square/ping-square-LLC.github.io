+++
title = 'Understanding OSPF'  
date = 2024-10-06T12:11:43-05:00
draft = false
weight = 8
+++
So you think you know the OSPF protocol? Let's find out!

**RFC 2328**
- [RFC 2328](https://datatracker.ietf.org/doc/html/rfc2328)
- [RFC 2328](https://www.tech-invite.com/y20/tinv-ietf-rfc-2328.html)

**RFC 5340**
- [RFC 5340](https://datatracker.ietf.org/doc/html/rfc5340)
- [RFC 5340](https://www.tech-invite.com/y50/tinv-ietf-rfc-5340.html)

###### 1) What does OSPF stand for and what is its primary function?
{{% expand title="Answer" %}}
OSPF stands for **Open Shortest Path First**. It is an open standard link-state routing protocol used for finding the best path between the source and the destination router using the shortest path first algorithm.
{{% /expand %}}

###### 2) What are the different types of OSPF packets?
{{% expand title="Answer" %}}
- **Hello packets**: These packets are sent periodically on all interfaces (including virtual links) in order to establish and maintain neighbor relationships.

- **Database description (DBD) Packets**: These packets are exchanged when an adjacency is being initialized.  They describe the contents of the link-state database.

- **Link-state request (LSR) packets**: After exchanging Database Description packets with a neighboring router, a router may find that parts of its link-state database are out-of-date. The Link State Request packet is used to request the pieces of the neighbor's database that are more up-to-date.

- **Link-state update (LSU) packets**: These packets are for database updates. This is an explicit LSA for a specific network link and normally is sent in direct response to an LSR.

- **Link-state acknowledgement (LSA) packets**: These packets are for flooding acknowledgments. These packets are sent in response to the flooding of LSAs, thus making flooding a reliable transport feature.
{{% /expand %}}

###### 3) Can you list the data contained in an Hello which are used to negotiate neighbor relationships?
{{% expand title="Answer" %}}
- **Router ID (RID)** - is an address by which an OSPF router identifies itself.  It is either:
    - the numerically highest IP address of all router's loopback interfaces,
    - Or if no loopback interfaces are configured, it is the numerically highest IP address of all the router's LAN interfaces..
- **Authentication options** - A field that allows secure communication between OSPF routers to prevent malicious activity. Options are:
    - none
    - clear text
    - Message Digest 5 (MD5) authentication.
- **Area ID** - The OSPF area that the OSPF interface belongs to.
- **Interface address mask** - The network mask for the primary IP address for the interface out which the hello is sent.
- **Interface priority** - The router interface priority for DR elections.
- **Hello interval** - The time span, in seconds, that a router sends out hello packets on the interface.
- **Dead interval** - The time span, in seconds, that a router waits to hear a hello from a neighbor router before it declares that router down.
- **Designated router** - The IP address of the DR.
- **backup designated router** - The IP address of the BDR.
- **Active neighbor** - The RIDs of each router from whom valid Hello packets have been seen recently on the network.  Recently means in the last RouterDeadInterval seconds.
{{% /expand %}}

###### 4) What is the significance of Designated Router (DR) in OSPF?
{{% expand title="Answer" %}}
The Designated Router (DR) minimizes the number of adjacencies by acting as a central point for exchanges of routing information between OSPF routers in the same broadcast network.
{{% /expand %}}

###### 5) How does the DR election works"
{{% expand title="Answer" %}}
In the DR election process:
- the router with the **highest priority** is elected as the DR.
-  if there is a tie, then the router with the **highest RID** (Router ID)wins
    - RID is by default the highest IP address of a loopback interface
    - If there is no interface, then it is highest IP address of a physical interface
    - By default, OSPF priorities are set to 1. A priority of 0 prevents a router from participating in the DR/BDR election. You can manually set priorities to influence the election outcome.
    - OSPF DR elections are non-preemptive, meaning that once a DR and BDR are elected, they remain as such until one of them fails or the network segment is reset. If the DR fails, the BDR takes over, and a new BDR election occurs among the remaining routers.
    - Adjacency: Once the DR and BDR are elected, all other routers form adjacencies only with the DR and BDR, significantly reducing the number of adjacencies in the network.
{{% /expand %}}

###### 6) what is the difference between an OSPF neighbor router and OSPF adjacent router?
{{% expand title="Answer" %}}
- **An OSPF neighbor router** is a router that shares a common OSPF-enabled network link. They are discovered OSPF hello packets. 
- **An OSPF adjacent router** is an OSPF neighbor that shares a synchronized OSPF database between the two neighbors.
Two routers can be neighbors without neccessary becoming adjacents. For example, in a broadcast networks all router can only be adjacents to the DR and BDR.
{{% /expand %}}

###### 7) For OSPF neigbor routers to become adjacent, The neigbor relationship has to evolve through different states. What are those OSPF neighbor states?
{{% expand title="Answer" %}}
- **Down** - This is the initial state of a neighbor relationship. It indicates that the router has not received any OSPF hello packets.
- **Attempt** - This state is relevant to NBMA networks that do not support broadcast and require explicit neighbor configuration. This state indicates that no information has been received recently, but the router is still attempting communication.
- **Init** - This state indicates that a hello packet has been received from another router, but bidirectional communication has not been established.
- **2-Way** - Bidirectional communication has been established. If a DR or BDR is needed, the election occurs during this state.
- **ExStart** - This is the first state in forming an adjacency. Routers identify which router will be the primary or secondary for the LSDB synchronization.
- **Exchange** - During this state, routers are exchanging link states headers by using DBD packets.
- **Loading** - LSR packets are sent to the neighbor, asking for the more recent LSAs that have been discovered (but not received) in the Exchange state.
- **Full** - Neighboring routers are fully adjacent.
{{% /expand %}}

###### 8) What are the type of OSPF networks?
{{% expand title="Answer" %}}
- **Broadcast network**: 
    - There is a DR and BDR election 
    - OSPF updates are sent to the address AllDRouters (224.0.0.6). The DR in turn multicasts an Update packet containing the LSA to all adjacent routers on the network using the address AllSPFRouters. All routers then flood the LSA out all other interfaces. Although the BDR hears and records LSAs multicast from DRothers, it does not reflood or acknowledge them unless the DR fails to do so.
    - Hello interval = 10 sec
- **Non-broadcast multi-access (NBMA) networks**: 
    - There is a DR and BDR election 
    - OSPF  updates are unicast from DRothers to the DR and BDR, and the DR unicasts a copy of the LSA to all adjacent neighbors.
    - Hello interval = 30 sec
- **Point-to-point networks**: direct connection between 2 routers. 
    - No need for a DR and BDR election.
    - OSPF update packets are sent to the multicast ALLSPFRouters address 224.0.0.5
    - Hello interval = 30 sec
- **Point-to-multipoint networks**: 
    - no DR and BDR election, and the virtual point-to-point links occupy the same channel through the use of PVC.
    - Hello interval = 30 sec
    - OSPF update packets are unicast to the directly connected neighbor.
- **Virtual links**: 
    - it is a link connecting 2 areas not directly connected to the backbone area.
    - OSPF update packets are unicast to the directly connected neighbor.
{{% /expand %}}

###### 9) What are OSPF interface roles?
{{% expand title="Answer" %}}
- **DR** - In this state, the router is the DR on the attached network and will establish adjacencies with the other routers on the multi-access network.
- **BDR** - In this state, the router is the BDR on the attached network, and will establish adjacencies with the other routers on the multi-access network.
- **DROTHER** - In this state, the router is neither the DR nor the BDR on the attached network. It will form adjacencies only with the DR and BDR, although it will track all neighbors on the network.
- **Loopback** - In this state, the interface is looped back via software or hardware. Although packets cannot transit an interface in this state, the interface address is still advertised in Router LSAs so that test packets can find their way to the interface.
- **Point-to-point** - This state is applicable only to interfaces connected to point-to-point, point-to-multipoint, and virtual link network types. When an interface transitions to this state, it is fully functional. It will begin sending Hello packets every Hello Interval and will attempt to establish an adjacency with the neighbor at the other end of the link.
- **Waiting** - This state is applicable only to interfaces connected to broadcast and NBMA network types. When an interface transitions to this state, it will begin sending and receiving Hello packets and will set the wait timer. The router will attempt to identify the network’s DR and BDR while in this state.
- **Down** - This is the initial state.
{{% /expand %}}

###### 10) What is a passive interface in OSPF?
{{% expand title="Answer" %}}
Making the network interface passive still adds the network segment into the LSDB but prohibits the interface from forming OSPF adjacencies
{{% /expand %}}

###### 11) What happens when OSPF priority is setup to zero?
{{% expand title="Answer" %}}
When OSPF priority is setup to zero on a router, that router will not be able to enter into DR/BDR election.
To configure interface priority, please use the following commands:
- `interface GigabitEthernet 0/1`
- `ip ospf priority 0`
{{% /expand %}}

###### 12) What are OSPF multicast addresses
{{% expand title="Answer" %}}
- **224.0.0.5** - this is an *All OSPF routers*  address is used to send Hello packets to all OSPF routers on a network segment. 
- **224.0.0.6** - this is an *All designated routers* address is used to send OSPF routing information to designated routers on a network segment.
{{% /expand %}}

###### 13) What is an OSPF area?
{{% expand title="Answer" %}}
An OSPF area is a logical grouping of routers or (more specifically, a logical grouping of router interfaces) within which all routers have an identical link state database.
{{% /expand %}}

###### 14) Why would you have an OSPF achitecture with multiple areas?
{{% expand title="Answer" %}}
The primary purpose of OSPF areas is to optimize the OSPF routing process and to scale large networks by:
- minimizing the frequency of routing table calculations 
- minimizing the size of LSDB table
- making route summarization possible.
{{% /expand %}}

###### 15) What is an OSPF backbone area?
{{% expand title="Answer" %}}
The OSPF backbone area (Area 0) is the core of an OSPF network to which all other areas must connect, either directly or through virtual links. All other areas must send their INTER-area traffic through the backbone
{{% /expand %}}

###### 16) What is a partitioned area?
{{% expand title="Answer" %}}
A partitioned area is an area connected through a backbone area. That is an area where intra-area communication has to go through the backbone area.
{{% /expand %}}

###### 17) What is a link state database?
{{% expand title="Answer" %}}
It is where the router stores all the OSPF LSAs it knows of, including its own.
{{% /expand %}}

###### 18) What are the different types of OSPF routers
{{% expand title="Answer" %}}
1- **Internal router**: 
- All OSPF interfaces belong to the same area.
- router Computes an SPF tree for a single area

2- **Backbone router**: 
- at least one interface belongs to the core area (that is area 0).
- router Computes an SPF tree for the backbone area.

3- **ABR**: 
- at least 2 interfaces belong to 2 different areas of the same domain, one of which is the backbone area.
- router Computes an SPF tree for a each area in which they have an interface.

4- **ASBR**: 
- at least 2 interfaces belong to 2 different areas, one of which belong to a different AS. 
- router Computes an SPF tree for a each area in which they have an interface.
- An ASBR cannot be located within a stub areas.
{{% /expand %}}

###### 19) What are the different types of LSA used by IPv4?
{{% expand title="Answer" %}}
1- **Type 1** (router LSA)
- Every OSPF router advertises a type 1 LSA.
- advertises LSA originating within an area, and contains the following
    - Router's active interfaces.
    - IP addresses.
    - neighbors. 
    - the cost.

2- **Type 2** 
- (Network LSA): Type 2 LSA is sent out by the DR and lists all the routers on the segment it is adjacent to. Type 2 LSA are flooded only within an area.

3- **Type 3** (Summary LSA): 
- they are generated by the ABR.
- They tell the internal area which destination the ABR can reach.
- It is used by the internal area to advertise its destination to the backbone area.
- Advertises default routes external to the area but internal to the OSPF domain.

4- **Type 4** (ASBR Summary LSA): 
- are generated by ABR 
- It contains routes to ASBRs.
- The destination advertised is not a network, but a host address (ASBR)

5- **Type 5** (External LSA): 
- generated by ASBRs 
- and contain routes to network that are external to current AS.
- Or a default route external to the OSPF domain.

6- **Type 7** (NSSA LSA):  
- Is generated by ASBR inside a NSSA to describe the router redistributed into the NSSA.
{{% /expand %}}

###### 20) What are the different types of areas and how they differ?
{{% expand title="Answer" %}}
1- Regular area

2- Backbone area

3- stub area: 
- A default route is injected into that area by ABR for external communication through  type 3 LSA.
- Can contain only type 1, 2 and 3 LSAs
- No virtual link allowed
- No ASBR.

4- totally stubby area: 
- Can only contain type 1 and 2 LSAs.
- Can contain a single type 3 LSA to advertise the default route to External networks.
- A default route is injected into that area by ABR for external communication.
- It only allows advertisement of internal routes in that area.

5- not-so-stubby area: 
- no type 5 LSA are sent by the ABR.
- implement stub or totally stubby functionality yet contain an ASBR. Type 7 LSAs generated by the ASBR are converted to type 5 by ABRs to be flooded to the rest of the OSPF domain.

6- Totally NSSA:
- Along with type 4 & type 5 LSA, type 3 LSA will also be filtered.
{{% /expand %}}

###### 21) What is the default Hello Interval?
{{% expand title="Answer" %}}
10 sec on Broadcast networks
30 sec on Non-broadcast networks
{{% /expand %}}

###### 22) What is the default RouterDeadInterval?
{{% expand title="Answer" %}}
It is 4 times the Hello Interval: 
- 40 sec on Broadcast networks
- 120 sec on Non-broadcast networks
{{% /expand %}}

###### 23) How often LSAs are transmitted?
{{% expand title="Answer" %}}
Every 30 minute by default
{{% /expand %}}

###### 24) What is MaxAge?
{{% expand title="Answer" %}}
It is the age at which an LSA is considered obsolete. It is 1 hour.
{{% /expand %}}

###### 25) What are the different type of OSPF paths/routes?
{{% expand title="Answer" %}}
 1. **Intra-area path**: 
    - path within the same area. 
    - Represented in the routing table by a "**O**"

 2. **Inter-area path**: 
    - path between 2 different areas of the same AS. 
    - Represented in the routing table by a "**O IA**"

3. **E1 (External Type 1)**:
   - An E1 route is an external route that includes both the cost to reach the ASBR (Autonomous System Boundary Router) within the OSPF domain and the cost of the external path from the ASBR to the destination network.
   -  Represented in the RIB as "**O E1**".
   
4. **E2 (External Type 2)**:
   - An E2 route is an external route where the cost of the path to the ASBR (Within the OSPF domain) is not included in the metric calculation. Only the external cost, as configured by the ASBR, is considered.
   - By default, redistributed routes in OSPF are E2, with a fixed cost that doesn’t change as the route propagates through the OSPF domain.
   - Represented in the RIB as "**O E2**".

5. **N1 (NSSA External Type 1)**:
   - An N1 route is similar to E1 but specifically used within an NSSA (Not-So-Stubby Area). It combines both the external and internal costs, just like E1.
   - The N1 route type is chosen when you want the external metric to be cumulative and reflective of the entire path, including internal OSPF costs, within an NSSA.
   - Represented in the RIB as "**O N1**".

6. **N2 (NSSA External Type 2)**:
   - An N2 route, like E2, includes only the external cost, disregarding the internal OSPF costs to reach the ASBR.
   - This type is also specific to NSSAs and is used to keep the cost of an external route constant as it propagates within the NSSA area.
   - Represented in the RIB as "**O N2**".
{{% /expand %}}

###### 26) What are the route preference order in OSPF?
{{% expand title="Answer" %}}
Intra-area route (O) >> Inter-area routes (O IA) >> External type 1 route (O E1) >> External Type 2 (O E2) >> NSSA-1 (O N1) >> NSSA-2 (O N2) 
{{% /expand %}}

###### 27) What are the main differences between E-routes an N-routes?
{{% expand title="Answer" %}}
N-Routes are routes found only within an NSSA area that are advertised by LSA 7. They are converted to E-routes when advertised out of the NSSA domain to the rest of the OSPF domain, that is using LSA type 5.
{{% /expand %}}

###### 28) What is the OSPF Metric used to compute the best path?
{{% expand title="Answer" %}}
The OSPF metric used is the cost 
{{% /expand %}}

###### 29) How do you compute the cost of a route?
{{% expand title="Answer" %}}
The cost of a route is the sum of the costs of all the outgoing interfaces to a destination.
{{% /expand %}}

###### 30) How does a Cisco router calculate the outgoing cost of an interface?
{{% expand title="Answer" %}}
Cisco IOS calculate the outgoing cost of an interface as 10^8/BW
{{% /expand %}}

###### 31) How do we manage the cost when the bandwidth of the link (like Gigabit Ethernet link) is higher than the reference bandwidth?
{{% expand title="Answer" %}}
There is a command which can be used which allows the default reference bandwidth to be changed:
- `auto-cost reference-bandwidth`
{{% /expand %}}

###### 32) Explain the process of route summarization in OSPF.
{{% expand title="Answer" %}}
Route summarization in OSPF is done at area border routers (ABRs), where routes from one area are summarized before being advertised into another area to reduce the size of routing tables.
{{% /expand %}}

###### 33) What are the advantages of summarization?
{{% expand title="Answer" %}} 
- Reduces the amount of information stored in a routing table.
- Allocates an existing pool of addresses more economically
- Lessens the load on router processor  and memory resources
- Less number of update messages
- Less bandwidth utilization
{{% /expand %}}

###### 34) What is the default redistribution cost into OSPF?
{{% expand title="Answer" %}}
- Redistribution from BGP to OSPF default cost = 1
- Redistribution from another OSPF process, take the source route metric.
- Redistribution from all other sources has a default cost of 20 
{{% /expand %}}


###### 35) How many table do we have in OSPF protocols?
{{% expand title="Answer" %}}
There are  4 tables in OSPF:
- **Neighbor table**
    - This are directly connected routers that have established a OSPF neighbor relationship.
        `Show ip ospf neighbor`
        
- **topology table** or **Adjacency table** or **link state database**
    - Stores all the LSAs exchanged within an area and that can be from multiple areas. In other words, it contains all the routes to a destination while the routing table contains the best route to a destination.
        `Show ip ospf database`
        
- **Routing table**
    - Contains the best path toward networks to which packets can be routed.
        `Show ip route`
        `Show ip route ospf`
        
- **Border-routers table**
    This is a separate internal router table that contains routes to ABRs and ASBRs.
        `Show ip ospf border-routers`
{{% /expand %}}

###### 36) Why is type 2 authentication preferable over type 1 authentication?
{{% expand title="Answer" %}}
Type 2 authentication uses MD5 encryption, whereas type 1 authentication uses clear-text passwords.
{{% /expand %}}