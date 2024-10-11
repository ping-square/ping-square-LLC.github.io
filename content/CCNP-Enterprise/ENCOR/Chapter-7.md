+++
title = 'Chapter 7'
date = 2024-10-05T15:18:51-05:00
draft = false
weight = 7
+++
# **EIGRP**


###### 1. **What does EIGRP stand for, and what type of routing protocol is it?**
{{% expand title="Answer" %}}
   EIGRP stands for Enhanced Interior Gateway Routing Protocol. It is an advanced distance vector routing protocol that includes features of both distance vector and link-state protocols.
{{% /expand %}}

###### 2. **How does EIGRP differ from traditional distance vector protocols like RIP?**
   **Answer:** Unlike RIP, EIGRP uses the Diffusing Update Algorithm (DUAL) to achieve faster convergence and supports variable-length subnet masks (VLSMs), classless inter-domain routing (CIDR), and unequal-cost load balancing.

###### 3. **What are the key metrics that EIGRP uses to calculate the best path?**
   **Answer:** EIGRP uses bandwidth, delay, load, reliability, and MTU as its key metrics. However, by default, only bandwidth and delay are used for route calculation.

###### 4. **What is the purpose of the Diffusing Update Algorithm (DUAL) in EIGRP?**
   **Answer:** DUAL is used by EIGRP to provide fast convergence by maintaining a loop-free topology and ensuring that backup routes are available when a primary route fails.

###### 5. **Explain the concept of a feasible successor in EIGRP.**
   **Answer:** A feasible successor is a backup route that is considered loop-free and meets the feasibility condition, meaning its reported distance is less than the feasible distance of the current best path.

###### 6. **What is the significance of the EIGRP autonomous system (AS) number?**
   **Answer:** The AS number is used to define the scope of an EIGRP routing domain, allowing multiple instances of EIGRP to run on the same router, each with its own routing table.

###### 7. **How does EIGRP handle unequal-cost load balancing?**
   **Answer:** EIGRP can perform unequal-cost load balancing by using the `variance` command, which allows it to use multiple routes with different metrics to balance traffic.

###### 8. **What is the role of EIGRP Hello packets?**
   **Answer:** Hello packets are used to establish and maintain neighbor relationships between EIGRP routers. They are sent periodically to detect link failures.

###### 9. **What is the default Hello interval and hold time for EIGRP?**
   **Answer:** The default Hello interval is 5 seconds, and the hold time is 15 seconds on most interfaces. On low-bandwidth networks (e.g., T1 or slower), the default Hello interval is 60 seconds, and the hold time is 180 seconds.

###### 10. **What is the purpose of the EIGRP metric weights command?**
   **Answer:** The `metric weights` command allows administrators to change the influence of different metrics (bandwidth, delay, load, reliability, MTU) in the EIGRP route selection process.

###### 11. **How does EIGRP handle route summarization?**
   **Answer:** EIGRP supports both manual and automatic route summarization. Automatic summarization occurs at network boundaries, but it can be disabled using the `no auto-summary` command.

###### 12. **What is the administrative distance (AD) of EIGRP for internal and external routes?**
   **Answer:** The AD for internal EIGRP routes is 90, while the AD for external EIGRP routes (routes redistributed into EIGRP) is 170.

###### 13. **Explain the concept of EIGRP split horizon and its impact on routing updates.**
   **Answer:** Split horizon prevents a router from sending routing information back out of the interface through which it was received, helping to prevent routing loops.

###### 14. **What is the purpose of route filtering in EIGRP, and how can it be achieved?**
   **Answer:** Route filtering in EIGRP controls which routes are advertised or accepted. It can be done using access lists, prefix lists, or route maps.

###### 15. **How does EIGRP detect a link failure?**
   **Answer:** EIGRP detects a link failure when it no longer receives Hello packets from a neighbor within the hold time interval. It then uses DUAL to find an alternative route.

###### 16. **What is the difference between a feasible distance (FD) and reported distance (RD) in EIGRP?**
   **Answer:** The feasible distance is the metric from the local router to the destination, while the reported distance is the metric advertised by a neighboring router for a route




Here are 20 sample comprehension questions based on Chapter 7 (EIGRP) from the book "CCNP and CCIE Enterprise Core ENCOR 350-401 Official Cert Guide, 2nd Edition":

1. **What does EIGRP stand for, and what kind of routing protocol is it?**
2. **Explain how EIGRP's "hybrid" nature distinguishes it from other types of routing protocols.**
3. **What are the main advantages of EIGRP over traditional distance-vector routing protocols?**
4. **Describe the role of the Diffusing Update Algorithm (DUAL) in EIGRP.**
5. **What metric components does EIGRP use to determine the best path to a destination?**
6. **How does EIGRP use composite metrics, and what factors can be adjusted to influence path selection?**
7. **What is the default administrative distance of EIGRP, and how does it compare to other routing protocols like OSPF and RIP?**
8. **Explain the concept of a successor and a feasible successor in EIGRP.**
9. **What is the significance of the "feasible distance" and "reported distance" in EIGRP's route calculations?**
10. **How does EIGRP handle unequal-cost load balancing, and which command enables this feature?**
11. **What is the purpose of EIGRP Hello packets, and what is the default Hello interval?**
12. **Explain how EIGRP forms neighbor relationships and the significance of the neighbor table.**
13. **What types of packets are used in EIGRP, and what is the function of each type?**
14. **Describe the process of EIGRP route summarization and its benefits.**
15. **What is the difference between manual and automatic route summarization in EIGRP?**
16. **How does EIGRP support IPv6, and what differences exist between EIGRP for IPv4 and EIGRP for IPv6?**
17. **What role does the EIGRP topology table play, and how does it differ from the routing table?**
18. **Explain the purpose of the "passive interface" feature in EIGRP, and when would you use it?**
19. **What command would you use to verify EIGRP neighbor relationships, and what key information should you look for in the output?**
20. **What troubleshooting steps would you take if EIGRP neighbors are not forming as expected?**


==============================================================================

Here are detailed answers to the questions:

1. **What is EIGRP, and how does it differ from other routing protocols like OSPF and RIP?**
   - **EIGRP (Enhanced Interior Gateway Routing Protocol)** is a Cisco-proprietary advanced distance-vector routing protocol that combines the benefits of distance-vector and link-state protocols. Unlike **RIP**, which has a slow convergence time and uses hop count as its metric, EIGRP is more efficient, supports faster convergence, and uses a composite metric based on bandwidth, delay, load, and reliability. Unlike **OSPF**, which is purely a link-state protocol and maintains a complete map of the network, EIGRP only exchanges information about paths and has lower overhead in large networks.

2. **Can you explain the main advantages of using EIGRP in a network?**
   - The main advantages of EIGRP include **fast convergence** due to the use of the Diffusing Update Algorithm (DUAL), **scalability** in large networks, support for **unequal-cost load balancing**, **classless routing** (supporting VLSM), and its ability to reduce unnecessary traffic by sending partial updates instead of full ones like RIP.

3. **What type of routing protocol is EIGRP, and what does "hybrid" mean in the context of EIGRP?**
   - EIGRP is a **hybrid** routing protocol, meaning it combines the characteristics of both **distance-vector** and **link-state** protocols. It uses the distance-vector approach of sharing routes with neighbors but with the added ability to calculate more complex metrics and maintain a topology table like link-state protocols. This results in efficient route calculation and faster convergence.

4. **What is the purpose of the Diffusing Update Algorithm (DUAL) in EIGRP, and how does it work?**
   - The **Diffusing Update Algorithm (DUAL)** is used by EIGRP to ensure **loop-free** and **fast convergence**. It calculates the best path to a destination and maintains backup routes. DUAL continuously monitors the network and, if a failure occurs, it can rapidly switch to a feasible successor (backup route) without recalculating the entire topology.

5. **How does EIGRP handle route recalculations when there is a change in the network topology?**
   - EIGRP recalculates routes using DUAL. When a topology change occurs, EIGRP checks if there is a **feasible successor** (backup route). If one exists, the route change is immediate. If no feasible successor exists, DUAL triggers the process of recalculating a new path from available route updates from neighbors.

6. **What are the key metric components used by EIGRP to determine the best path to a destination?**
   - EIGRP uses a **composite metric** based on several factors:
     1. **Bandwidth** (minimum bandwidth along the path),
     2. **Delay** (cumulative delay along the path),
     3. **Reliability** (measured based on historical link quality),
     4. **Load** (current traffic load on the link).
   By default, only bandwidth and delay are considered unless manually modified.

7. **Can you explain how EIGRP performs unequal-cost load balancing, and how is it enabled?**
   - EIGRP supports **unequal-cost load balancing**, allowing traffic to be distributed across multiple paths with different metrics. This is enabled using the **variance** command, which multiplies the metric of the best path and allows other paths with a lower or equal metric (within the variance range) to be included in load balancing.

8. **What is the default administrative distance of EIGRP, and how does it compare to other routing protocols like OSPF and BGP?**
   - The default **administrative distance (AD)** for internal EIGRP routes is **90**, which is lower (more preferred) than OSPF (110) and RIP (120), but higher than BGP external routes (20). For EIGRP external routes, the AD is **170**.

9. **What are the differences between a successor and a feasible successor in EIGRP?**
   - A **successor** is the primary route to a destination, which has the lowest cost and is installed in the routing table. A **feasible successor** is a backup route that meets the feasibility condition (its reported distance is lower than the current feasible distance), and is kept in the topology table but not in the routing table unless the successor route fails.

10. **How do feasible distance and reported distance impact EIGRP route selection?**
    - The **feasible distance (FD)** is the lowest calculated metric to reach a destination from the local router. The **reported distance (RD)** is the metric reported by a neighbor router for a particular route. For a route to be considered a feasible successor, its RD must be lower than the FD of the current successor, ensuring that no routing loops will occur.

11. **Explain the role of the EIGRP topology table, and how does it differ from the routing table?**
    - The **topology table** contains all the known routes to a destination, including both successors and feasible successors. It keeps a complete record of all possible paths. The **routing table**, on the other hand, only contains the best (successor) routes that will be used for forwarding traffic.

12. **What are EIGRP Hello packets used for, and how often are they sent by default?**
    - EIGRP **Hello packets** are used to establish and maintain neighbor relationships. They are sent at regular intervals to check if neighbors are reachable. By default, Hello packets are sent every **5 seconds** on most networks and every **60 seconds** on low-bandwidth networks like non-broadcast multi-access (NBMA) links.

13. **Describe how EIGRP forms neighbor relationships and maintains neighbor stability.**
    - EIGRP forms neighbor relationships by exchanging Hello packets. When two routers exchange Hello packets and agree on common parameters (such as AS number, K-values, etc.), they establish a neighbor relationship and begin sharing route updates. Stability is maintained by continuously exchanging Hello packets to monitor link health.

14. **What are the five types of EIGRP packets, and what are the purposes of each?**
    - The five types of EIGRP packets are:
      1. **Hello**: Used to establish and maintain neighbor relationships.
      2. **Update**: Used to send routing information to neighbors.
      3. **Query**: Sent when a router needs to find an alternative path to a destination.
      4. **Reply**: Sent in response to a Query packet with information about an alternative path.
      5. **Acknowledgment (ACK)**: Confirms receipt of Update, Query, and Reply packets.

15. **How does EIGRP handle route summarization, and what are the advantages of using route summarization in a network?**
    - EIGRP supports both **manual and automatic route summarization**. Summarization reduces the size of the routing table by representing multiple networks with a single summary route, which reduces bandwidth usage for route updates and improves network efficiency.

16. **What is the difference between manual and automatic route summarization in EIGRP, and how do you configure both?**
    - **Automatic summarization** (enabled by default in older versions of EIGRP) automatically summarizes routes at major network boundaries, whereas **manual summarization** allows more granular control by letting administrators specify summary routes at any point in the network. Automatic summarization can be disabled using `no auto-summary`, and manual summarization is configured with the `ip summary-address` command.

17. **How does EIGRP handle route filtering, and what commands are used to configure route filtering?**
    - EIGRP supports **route filtering** to control which routes are advertised or received. Filtering can be done using **prefix lists**, **access control lists (ACLs)**, or **route maps**. Commands like `distribute-list` are used to apply filtering.

18. **Can you explain the purpose of the passive interface feature in EIGRP, and in which scenarios would you use it?**
    - The **passive interface** feature prevents a router from sending Hello packets on an interface, effectively disabling EIGRP neighbor relationships on that interface while still allowing the network to be advertised. It is used in scenarios where a router is connected to a network but does not need to form EIGRP neighbor relationships, such as connecting to end-user devices.

19. **How does EIGRP support IPv6, and what are the differences between EIGRP for IPv4 and EIGRP for IPv6?**
    - **EIGRP for IPv6** works similarly to EIGRP for IPv4, but it operates using IPv6 addresses and interfaces. One major difference is that, in IPv6, EIGRP does not rely on network statements and uses the `ipv6 eigrp` command to enable it directly on interfaces.

20. **What command would you use to view the EIGRP topology table, and what information does it provide?**
    - The command `show ip eigrp topology` (or `show ipv6 eigrp topology` for IPv6) displays the EIGRP topology table, showing all the known routes, their feasible and reported distances, successors, and feasible successors.

21. **What troubleshooting steps would you take if EIGRP neighbors are not forming as expected?**
    - To troubleshoot EIGRP neighbor issues:
      1. Verify matching AS numbers on both ends using `show ip eigrp interfaces`.
      2. Check the interface configurations and ensure both are not passive.
      3. Verify that Hello packets are being exchanged (`debug eigrp

 packets hello`).
      4. Ensure there are no mismatched EIGRP K-values (`show ip protocols`).
      5. Check for proper authentication (if enabled).

22. **How do you verify EIGRP neighbor relationships, and what information can you gather from the `show ip eigrp neighbors` command?**
    - The `show ip eigrp neighbors` command shows the state of EIGRP neighbor relationships, including the interface used, the neighbor's IP address, the hold time, uptime, and queue counts. This information helps confirm that the neighbors are stable and functioning properly.

23. **What are the common reasons for EIGRP neighbor adjacency failures, and how can they be resolved?**
    - Common reasons include:
      - **AS number mismatch**.
      - **K-value mismatch**.
      - **Passive interfaces** preventing neighbor formation.
      - **Authentication mismatch**.
      - **Layer 2 connectivity issues** (e.g., link failures).
    - Solutions involve checking and correcting these parameters and ensuring proper network connectivity.

24. **How do you enable and configure EIGRP authentication, and why is authentication important in EIGRP?**
    - EIGRP authentication is enabled using **MD5 authentication** to secure EIGRP updates and prevent unauthorized routers from joining the EIGRP domain. Configuration steps include creating a key chain and applying it to the EIGRP interfaces with the `ip authentication mode eigrp` and `ip authentication key-chain eigrp` commands.

25. **What are the limitations of EIGRP, and in what scenarios would you avoid using EIGRP as the primary routing protocol?**
    - EIGRP is Cisco-proprietary, meaning it is not ideal for multi-vendor environments. It also does not scale as well as OSPF or BGP in very large networks. Scenarios where EIGRP would be avoided include:
      - **Multi-vendor networks** requiring open standards.
      - **Large, hierarchical networks** where link-state protocols like OSPF or BGP are more efficient.

26. In **EIGRP**, there are **three main tables** that interact to facilitate the routing process:

    1. **Neighbor Table**:
    - This table stores information about all the EIGRP neighbors that have been discovered on directly connected links. 
    - The neighbor relationship is established through the exchange of Hello packets, and this table maintains details such as the IP address of the neighbor, the interface through which the neighbor is reachable, and the hold time (the maximum time the router will wait before declaring a neighbor unreachable if Hello packets are not received).
    - Command to view: `show ip eigrp neighbors`

    2. **Topology Table**:
    - The topology table stores all the routes learned from EIGRP neighbors, including both feasible successors (backup routes) and successors (primary routes).
    - Each entry includes the **feasible distance** (the best metric to reach a destination), the **reported distance** (the metric reported by the neighboring router), and details about feasible successors, which are potential backup routes.
    - The topology table is essential for EIGRP's Diffusing Update Algorithm (DUAL), which determines the best path (successor) and any feasible successors for each destination.
    - Command to view: `show ip eigrp topology`

    3. **Routing Table**:
    - The routing table contains the best routes (successors) that are chosen by EIGRP and installed in the global routing table of the router.
    - EIGRP picks the best route from the topology table based on the lowest metric (feasible distance) and installs it into the routing table.
    - Only the routes that are deemed as the best (successors) are moved to the routing table.
    - Command to view: `show ip route`

    ### Interaction Between the Tables:
    - **Neighbor Table**: Keeps track of directly connected EIGRP neighbors.
    - **Topology Table**: Receives routing updates from neighbors and stores multiple potential routes. It uses the DUAL algorithm to identify the best route (successor) and feasible successors.
    - **Routing Table**: Once the best route is identified, it is installed in the routing table for actual forwarding of packets.

In summary, the neighbor table keeps track of neighboring routers, the topology table stores all potential routes learned from these neighbors, and the routing table holds the most optimal routes that are actively used for packet forwarding.
These answers cover a wide range of EIGRP topics that are critical for both technical interviews and certification exams.