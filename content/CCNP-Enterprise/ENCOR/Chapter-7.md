+++
title = 'Chapter 7'
date = 2024-10-05T15:18:51-05:00
draft = true
weight = 7
+++
# **EIGRP**

Here are 30 sample comprehension questions based on Chapter 7 (EIGRP) from the "CCNP and CCIE Enterprise Core ENCOR 350-401 Official Cert Guide, 2nd Edition":

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

These questions are designed to cover the key concepts and mechanisms of EIGRP as discussed in Chapter 7 of the ENCOR guide.