+++
title = 'Chapter 14'
date = 2024-12-21T23:04:58-06:00
draft = true
+++

# **Quality of Service (QoS)**



###### 1. What are the leading causes of QOS?
{{% expand title="Answer" %}}
The leading causes of quality issues:
- Lack of bandwidth
- Latency and jitter
- Packet loss
{{% /expand %}}


###### 2. What are the most common causes of network latency?
{{% expand title="Answer" %}}
The most common causes of network latency are:
- **Propagation delay (fixed)**
- **Serialization delay (fixed)**:
    is the time it takes to place all the bits of a packet onto a link.
- **Processing delay (fixed)**: is the fixed amount of time it takes for a networking device to take the packet from an input interface and place the packet onto the output queue of the output interface. The processing delay depends on factors such as the following:
    - CPU speed (for software-based platforms)
    - CPU utilization (load)
    - IP packet switching mode (process switching, software CEF, or hardware CEF)
    - Router architecture (centralized or distributed)
    - Configured features on both input and output interfaces
- **Delay variation (variable)**: also referred to as jitter, is the difference in the latency between packets in a single flow.
{{% /expand %}}


###### 3. What are the different QoS implementation models?
{{% expand title="Answer" %}}
there are 3 QoS implementation models:
- **Best effort**: QoS is not enabled for this model. It is used for traffic that does not require any special treatment.
- **Integrated Services (IntServ)**: Applications signal the network to make a bandwidth reservation and to indicate that they require special QoS treatment.
- **Differentiated Services (DiffServ)**: The network identifies classes that require special QoS treatment.
{{% /expand %}}


###### 4. What is MQC?
{{% expand title="Answer" %}}
Modular QoS CLI (MQC) is Cisco’s approach to implementing QoS on Cisco routers. It provides a modular CLI framework to create QoS policies that are used to perform traffic classification and QoS actions such as marking, policing, shaping, congestion management, and congestion avoidance.
{{% /expand %}}


###### 5. How do you implement MQC policies?
{{% expand title="Answer" %}}
MQC policies are implemented by using the following three MQC components:

- **Class maps**: These maps define the traffic classification criteria by identifying the type of traffic that needs QoS treatment (for example, matching voice traffic, matching video traffic).
- **Policy maps**: These maps provide QoS actions for each traffic class defined by the class maps.
- **Service policies**: These policies are used to apply policy maps to interfaces in an inbound and/or outbound direction.
{{% /expand %}}


###### 6. What are the different type of class-based QoS that MQC can apply to traffic?
{{% expand title="Answer" %}}
- Class-based weighted fair queuing (CBWFQ)
- Class-based policing
- Class-based shaping
- Class-based marking
{{% /expand %}}


###### 7. What is packet classification?
{{% expand title="Answer" %}}
Packet classification is a QoS mechanism responsible for distinguishing between different traffic streams.
- It uses traffic descriptors to categorize an IP packet within a specific class. 
- Packet classification should take place at the network edge, as close to the source of the traffic as possible.
{{% /expand %}}


###### 8. What are the traffic  descriptors used for packet classification ?
{{% expand title="Answer" %}}
The following traffic descriptors are used for traffic classification:
- **Internal**: QoS groups (locally significant to a router)
- **Layer 1**: Physical interface, subinterface, or port
- **Layer 2**: MAC address and 802.1Q/p class of service (CoS) bits
- **Layer 2.5**: MPLS experimental (EXP) bits
- **Layer 3**: Differentiated Services Code Points (DSCP), IP Precedence (IPP), and source/destination IP address
- **Layer 4**: TCP or UDP ports
- **Layer 7**: Next-Generation Network-Based Application Recognition (NBAR2)
{{% /expand %}}


###### 9. What is packet marking?
{{% expand title="Answer" %}}
*Packet marking* is a QoS mechanism that colors a packet by changing a field within a packet or a frame header with a traffic descriptor so it is distinguished from other packets during the application of other QoS mechanisms (such as re-marking, policing, queuing, or congestion avoidance).
{{% /expand %}}


###### 10. What are the traffic descriptors used for packet marking ?
{{% expand title="Answer" %}}
The following traffic descriptors are used for marking traffic:
- **Internal**: QoS groups
- **Layer 2**: 802.1Q/p class of service (CoS) bits
- **Layer 2.5**: MPLS experimental (EXP) bits
- **Layer 3**: Differentiated Services Code Points (DSCP) and IP Precedence (IPP)
{{% /expand %}}


###### 11. What is the difference between Policing and Shaping?
{{% expand title="Answer" %}}
Traffic **policers** and **shapers** are traffic-conditioning QoS mechanisms used to control the flow of traffic, but they differ in their implementation:
- **Policers**: Transmit or re-mark incoming or outgoing traffic that conforms to the desired traffic rate, and drop or mark down incoming or outgoing traffic that goes beyond the desired traffic rate.
- **Shapers**: Buffer and delay egress traffic rates that momentarily peak above the desired rate until the egress traffic rate drops below the defined traffic rate. If the egress traffic rate is below the desired rate, the traffic is sent immediately.
{{% /expand %}}


###### 12. What are fundamental reasons behind link congestion?
{{% expand title="Answer" %}}
Congestion can occur for one of these two reasons:
- The input or ingress interface is a higher speed than the output or egress interface
    - For example, when packets are received on a 100 Gbps input interface and transmitted out of a 10 Gbps egress interface.
- Multiple input or ingress interfaces forwarding packets to a single output or egress interface that is a lower speed than the sum of the speeds of the input or ingress interfaces 
    - For example, when packets are received on twenty 10 Gbps input interfaces simultaneously (summing up to 200 Gbps) and transmitted out of a single 100 Gbps egress interface.
{{% /expand %}}


###### 13. What is congestion management ?
{{% expand title="Answer" %}}
Congestion management is a combination of **queuing**(buffering) and **scheduling** algorithm.
When congestion is taking place, the queues fill up, and packets can be reordered by some of the **queuing algorithms** so that higher-priority packets exit the output interface sooner than lower-priority ones. At this point, a **scheduling algorithm** decides which packet to transmit next
{{% /expand %}}


###### 14. What are the different Queuing algorithms out there?
{{% expand title="Answer" %}}
- **First-in, first-out queuing (FIFO)**: FIFO involves a single queue where the first packet to be placed on the output interface queue is the first packet to leave the interface (first come, first served). In FIFO queuing, all traffic belongs to the same class.

- **Round robin**: queues are serviced in sequence one after the other, and each queue processes one packet only. No queues starve with round robin because every queue gets an opportunity to send one packet every round. No queue has priority over others, and if the packet sizes from all queues are about the same, the interface bandwidth is shared equally across the round robin queues. A limitation of round robin is that it does not include a mechanism to prioritize traffic.

- **Weighted round robin (WRR)**: WRR was developed to provide prioritization capabilities for round robin. It allows a weight to be assigned to each queue, and based on that weight, each queue effectively receives a portion of the interface bandwidth that is not necessarily equal to the other queues’ portions.

- **Custom queuing (CQ)**: CQ is a Cisco implementation of WRR that involves a set of 16 queues with a round-robin scheduler and FIFO queuing within each queue. Each queue can be customized with a portion of the link bandwidth for each selected traffic type. If a particular type of traffic is not using the bandwidth reserved for it, other traffic types may use the unused bandwidth. CQ causes long delays and also suffers from all the same problems as FIFO within each of the 16 queues that it uses for traffic classification.

- **Priority queuing (PQ)**: With PQ, four queues in a set (high, medium, normal, and low) are served in strict-priority order, with FIFO queuing within each queue. The high-priority queue is always serviced first, and lower-priority queues are serviced only when all higher-priority queues are empty. For example, the medium queue is serviced only when the high-priority queue is empty. The normal queue is serviced only when the high and medium queues are empty; finally, the low queue is serviced only when all the other queues are empty. At any point in time, if a packet arrives for a higher queue, the packet from the higher queue is processed before any packets in lower-level queues. For this reason, if the higher-priority queues are continuously being serviced, the lower-priority queues are starved.

- **Weighted fair queuing (WFQ)**: The WFQ algorithm automatically divides the interface bandwidth by the number of flows (weighted by IP Precedence) to allocate bandwidth fairly among all flows. This method provides better service for high-priority real-time flows but can’t provide a fixed-bandwidth guarantee for any particular flow.

- **Class-based weighted fair queuing (CBWFQ)**: CBWFQ enables the creation of up to 256 queues, serving up to 256 traffic classes. Each queue is serviced based on the bandwidth assigned to that class. It extends WFQ functionality to provide support for user-defined traffic classes. With CBWFQ, packet classification is done based on traffic descriptors such as QoS markings, protocols, ACLs, and input interfaces. After a packet is classified as belonging to a specific class, it is possible to assign bandwidth, weight, queue limit, and maximum packet limit to it. The bandwidth assigned to a class is the minimum bandwidth delivered to the class during congestion. The queue limit for that class is the maximum number of packets allowed to be buffered in the class queue. After a queue has reached the configured queue limit, excess packets are dropped. CBWFQ by itself does not provide a latency guarantee and is only suitable for non-real-time data traffic.

- **Low-latency queuing (LLQ)**: LLQ is CBWFQ combined with priority queuing (PQ), and it was developed to meet the requirements of real-time traffic, such as voice. Traffic assigned to the strict-priority queue is serviced up to its assigned bandwidth before other CBWFQ queues are serviced. All real-time traffic should be configured to be serviced by the priority queue. Multiple classes of real-time traffic can be defined, and separate bandwidth guarantees can be given to each, but a single priority queue schedules all the combined traffic. If a traffic class is not using the bandwidth assigned to it, it is shared among the other classes.
{{% /expand %}}


###### 15. What are the recommended queuing algorithm for rich media network (voice and video traffic)?
{{% expand title="Answer" %}}
- **Class-based weighted fair queuing (CBWFQ)**
- **Low-latency queuing (LLQ)**
{{% /expand %}}


###### 16. What is congestion-avoidance  ?
{{% expand title="Answer" %}}
Congestion-avoidance techniques monitor network traffic loads to anticipate and avoid congestion by dropping packets. The packet dropping algorithms are:
- **Tail drop**: treats all traffic equally and does not differentiate between classes of service. With tail drop, when the output queue buffers are full, all packets trying to enter the queue are dropped, regardless of their priority, until congestion clears up and the queue is no longer full.

- **random early detection (RED)**: RED provides congestion avoidance by randomly dropping packets before the queue buffers are full. Randomly dropping packets instead of dropping them all at once, as with tail drop, avoids global synchronization of TCP sessions. RED monitors the buffer depth and performs early drops on random packets when the minimum defined queue threshold is exceeded.

- **weighted RED (WRED)**. The difference between RED and WRED is that the randomness of packet drops can be manipulated by traffic weights denoted by either IP Precedence (IPP) or DSCP. Packets with a lower IPP value are dropped more aggressively than are higher IPP values
{{% /expand %}}