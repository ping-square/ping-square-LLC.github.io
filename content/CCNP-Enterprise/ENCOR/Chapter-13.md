+++
title = 'Chapter 13'
date = 2024-10-06T12:12:13-05:00
draft = true
weight = 13
+++
# **Multicast**

###### 1. What protocol are used by the multicast technology?
{{% expand title="Answer" %}}
multicast technology relies on 2 protocols:
- Internet Group Management Protocol (IGMP) for its operation in Layer 2 networks 
- Protocol Independent Multicast (PIM) for its operation in Layer 3 networks.
{{% /expand %}}

###### 3. What is the primary function of VLAN Trunking Protocol (VTP)?
{{% expand title="Answer" %}}
test
{{% /expand %}}

###### 2. What IPv4 address range is reserved for multicast traffic?
{{% expand title="Answer" %}}
 Internet Assigned Numbers Authority (IANA) assigned the IP Class D address space 224.0.0.0/4 for multicast addressing; it includes addresses ranging from 224.0.0.0 to 239.255.255.255. The first 4 bits of this whole range start with 1110.
{{% /expand %}}

###### 3. What does a receiver do to request a specific multicast feed?
{{% expand title="Answer" %}}
When a receiver wants to receive a specific multicast feed, it sends an **IGMP join** to the local router using the multicast IP group address for that feed. The receiver reprograms its interface to accept the multicast MAC group address that correlates to the group address. 
{{% /expand %}}

###### 4. What is IGMP?
{{% expand title="Answer" %}}
Internet Group Management Protocol (IGMP) is the protocol that receivers use to join multicast groups and start receiving traffic from those groups.
{{% /expand %}}

###### 5. What is the difference bewteen IGMPv2 and IGMPv3?
{{% expand title="Answer" %}}
IGMPv3 is used to provide source filtering for Source Specific Multicast (SSM) while IGMPv2 cannot provide source filtering. In other words, when a receiver sends a membership report using IGMPv2 (**IGMP join**) to join a multicast group, it does not specify which source it would like to receive multicast traffic from but IGMPv3 does.
{{% /expand %}}

###### 6. What is IGMP snooping?
{{% expand title="Answer" %}}
When the switch receives a multicast frame destined for a multicast group, it forwards the packet only out the ports where IGMP joins were received for that specific multicast group. IGMP snooping is the most widely used method which consists in examining IGMP joins sent by receivers and maintaining a table of interfaces to IGMP joins.
{{% /expand %}}

###### 7. What is the difference between PIM and IGMP protocols?
{{% expand title="Answer" %}}
test
{{% /expand %}}

###### 8. What is the primary function of VLAN Trunking Protocol (VTP)?
{{% expand title="Answer" %}}
test
{{% /expand %}}