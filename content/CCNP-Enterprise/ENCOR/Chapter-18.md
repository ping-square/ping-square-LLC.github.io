+++
title = 'Chapter 18'
date = 2025-01-08T21:13:29-06:00
draft = true
+++
# **Wireless Infrastructure**

###### 1. What is a **BSS**?
{{% expand title="Answer" %}}
BSS stands for **Basic Service Set*
{{% /expand %}}


###### 2. What is a **SSID**?
{{% expand title="Answer" %}}
SSID = Service Set Identifier
{{% /expand %}}


###### 3. What is **Split-MAC architecture**?
{{% expand title="Answer" %}}
**Split-MAC architecture** is when Cisco AP has to join a WLC to become fully functional.
{{% /expand %}}


###### 4. What is **CAPWAP**?
{{% expand title="Answer" %}}
**CAPWAP** are logical tunnels joining an AP to a WLC. They transport control and data traffic and can extend through the wired network. 
{{% /expand %}}


###### 5. What is a **Rogue AP**?
{{% expand title="Answer" %}}
A **Rogue AP** is a AP that has been installed on a secure network without explicit authorization from a local network administration.
{{% /expand %}}


###### 6. What are the different modes a Cisco AP can have on a WLC?
{{% expand title="Answer" %}}
- **Local mode**: The default lightweight mode that offers one or more functioning BSSs on a specific channel. In other words, an AP in local mode serves wireless clients. During times when it is not transmitting, the AP scans the other channels to measure the level of noise, measure interference, discover rogue devices, and match against intrusion detection system (IDS) events.

- **FlexConnect mode**: An AP at a remote site maintains a control CAPWAP tunnel to a central WLC while forwarding data normally, without a CAPWAP tunnel. If the remote site’s WAN link goes down, taking the control CAPWAP tunnel down too.

- **Monitor mode**: The AP does not transmit at all, but its receiver is enabled to act as a dedicated sensor. The AP checks for IDS events, detects rogue access points, and determines the position of stations through location-based services.

- **Sniffer mode**: An AP dedicates its radios to receiving 802.11 traffic from other sources, much like a sniffer or packet capture device. The captured traffic is then forwarded to a PC running network analyzer software such as Wireshark, where it can be analyzed further.

- **Rogue detector mode**: An AP dedicates itself to detecting rogue devices by correlating MAC addresses heard on the wired network with those heard over the air. Rogue devices are those that appear on both networks.

- **Bridge mode**: An AP becomes a dedicated bridge (point-to-point or point-to-multipoint) between two networks. Two APs in bridge mode can be used to link two locations separated by a distance. Multiple APs in bridge mode can form an indoor or outdoor mesh network.

- **Flex+Bridge mode**: FlexConnect operation is enabled on a mesh AP.

- **SE-Connect mode**: The AP dedicates its radios to spectrum analysis on all wireless channels. You can remotely connect a PC running software such as MetaGeek Chanalyzer or Cisco Spectrum Expert to the AP to collect and analyze the spectrum analysis data to discover sources of interference.
{{% /expand %}}


###### 7. What are the different types of  **Cisco Wireless deployments**?
{{% expand title="Answer" %}}
There are 3 main categories of Cisco Wireless deployments:
- **Lightweithg Wireless deployment**- there is no controller involved and the AP operates in **local mode** only. they act like natural extension of switch network
- **Controller-less Wireless deployment**- the WLC is a software embedded in the AP. the AP that hosts the WLC forms a CAPWAP tunnel with the WLC. EWC typically supports up to 100 APs and up to 2,000 wireless clients.
- **Controller-based Wireless deployment**- The entire wireless network infrastructure is managed from a standalone WLC. There are 3 types of Controller-based Wireless deployment:
    - **centralized wireless LAN deployment**: The WLC is placed in a central location, in a data center or near the network core, in order the maximise the number of AP that can join to it. A typical centralized WLC meant for a large enterprise can support up to 6000 APs and up to 64,000 wireless clients.
    - **cloud-based wireless LAN deployment**: In this case the centralized WLC is located either in a public cloud or in a private cloud. Cloud-based controllers can typically support up to 6000 APs and up to 64,000 wireless clients.
    - **distributed wireless deployment**: WLC can be located further down in the network hierarchy, for example at the distribution layer associated with multiple remote sites. Distributed controllers are commonly smaller standalone models that can support up to 250 APs and 5,000 wireless clients.
{{% /expand %}}


###### 8. What is a **state machine**?
{{% expand title="Answer" %}}
a **state machine** is a sequence of states the lightweight AP goes through from the time it powers up to the time it becomes fully functional.
{{% /expand %}}


###### 9. What are the different states of the **state machine**?
{{% expand title="Answer" %}}
- **AP boots**: After an AP receives power, it boots on a small IOS image so that it can work through the remaining states and communicate over its network connection. The AP must also receive an IP address from either a Dynamic Host Configuration Protocol (DHCP) server or a static configuration so that it can communicate over the network.
- **WLC discovery**: The AP goes through a series of steps to find one or more controllers that it might join. 
- **CAPWAP tunnel**: The AP attempts to build a CAPWAP tunnel with one or more controllers. The tunnel will provide a secure Datagram Transport Layer Security (DTLS) channel for subsequent AP-WLC control messages. The AP and WLC authenticate each other through an exchange of digital certificates.
- **WLC join**: The AP selects a WLC from a list of candidates and then sends a CAPWAP Join Request message to it. The WLC replies with a CAPWAP Join Response message.
- **Download image**: The WLC informs the AP of its software release. If the AP’s own software is a different release, the AP downloads a matching image from the controller, reboots to apply the new image, and then returns to step 1. If the two are running identical releases, no download is needed.
- **Download config**: The AP pulls configuration parameters down from the WLC and can update existing values with those sent from the controller. Settings include RF, service set identifier (SSID), security, and quality of service (QoS) parameters.
- **Run state**: Once the AP is fully initialized, the WLC places it in the “*run*” state. The AP and WLC then begin providing a BSS and begin accepting wireless clients.
- **Reset**: If an AP is reset by the WLC, it tears down existing client associations and any CAPWAP tunnels to WLCs. The AP then reboots and starts through the entire state machine again.
{{% /expand %}}


###### 10. What is the goal of WLC discovery?
{{% expand title="Answer" %}}
The goal of WLC discovery is just to build a list of live WLC candidate controllers that are available in case the AP needs any of them.
{{% /expand %}}


###### 11. What are different WLC discovery methods?
{{% expand title="Answer" %}}
- Prior knowledge of WLCs
    - The AP may already have the WLC's IP address manually configured or provisioned.
- Plug-and-play with Cisco DNA Center
    - Cisco DNA automates the provisioning of APs and WLCs.
    - DNA enables a PnP onboarding process for APs. When an AP is added to the network, DNA Center recognizes it, assigns policies, and connects it to the appropriate WLC automatically.
- DHCP and DNS information to suggest some controllers
    - **Step 1**.The DHCP server that supplies the AP with an IP address can also send DHCP option 43 to suggest a list of WLC addresses.
    - **Step 2**.The AP attempts to resolve the name CISCO-CAPWAP-CONTROLLER. localdomain with a DNS request (where localdomain is the domain name learned from DHCP). If the name resolves to an IP address, the AP attempts to contact a WLC at that address.
- Broadcast on the local subnet to solicit controllers
    - **Step 1**.The AP broadcasts a *CAPWAP Discovery Request* on its local wired subnet. Any WLCs that also exist on the subnet answer with a *CAPWAP Discovery Response*.
    - **Step 2**.An AP can be “primed” with up to three controllers—a primary, a secondary, and a tertiary. These are stored in nonvolatile memory so that the AP can remember them after a reboot or power failure. 
    - **Step 3**.The DHCP server that supplies the AP with an IP address can also send DHCP option 43 to suggest a list of WLC addresses.
    - **Step 4**.The AP attempts to resolve the name CISCO-CAPWAP-CONTROLLER. localdomain with a DNS request (where localdomain is the domain name learned from DHCP). If the name resolves to an IP address, the AP attempts to contact a WLC at that address.
    - **Step 5**.If none of the steps have been successful, the AP resets itself and starts the discovery process all over again.
{{% /expand %}}


###### 12. How an AP selects a WLC?
{{% expand title="Answer" %}}
When an AP has finished the discovery process, it should have built a list of live candidate controllers. Now it must begin a separate process to select one WLC and attempt to join it. The WLC selection process consists of the following three steps:
    - **step 1**.If the AP has previously joined a controller and has been configured or “primed” with a primary, secondary, and tertiary controller, it tries to join those controllers in succession.
    - **Step 2**.If the AP does not know of any candidate controller, it tries to discover one. If a controller has been configured as a master controller, it responds to the AP’s request.
    - **Step 3**.The AP attempts to join the least-loaded WLC, in an effort to load balance APs across a set of controllers. During the discovery phase, each controller reports its load—the ratio of the number of currently joined APs to the total AP capacity. The least-loaded WLC is the one with the lowest ratio.
{{% /expand %}}


###### 13. How does an AP is aware of the status of a WLC?
{{% expand title="Answer" %}}
After an AP joins a controller, it sends keepalive (also called heartbeat) messages to the controller over the wired network at regular intervals. By default, keepalives are sent every 30 seconds. The controller is expected to answer each keepalive as evidence that it is still alive and working. If a keepalive is not answered, an AP escalates the test by sending four more keepalives at 3-second intervals. If the controller answers, all is well; if it does not answer, the AP presumes that the controller has failed. The AP then moves quickly to find a successor to join.
{{% /expand %}}


###### 14. How can you guaranti HA with WLC?
{{% expand title="Answer" %}}
 If a controller full of 1000 APs fails, all 1000 APs must detect the failure, discover other candidate controllers, and then select the least-loaded one to join. During that time, wireless clients can be left stranded with no connectivity. There are 2 methods that can be used to guaranti HA with the WLC design:
 - An AP can be “primed” with up to three controllers—a primary, a secondary, and a tertiary. These are stored in nonvolatile memory so that the AP can remember them after a reboot or power failure.
 - WLCs also support high availability (HA) with stateful switchover (SSO) redundancy.
{{% /expand %}}


###### 15. What is **Client density**?
{{% expand title="Answer" %}}
Client density is essentially the number of devices per AP. 
{{% /expand %}}


###### 16. What is **RSS**?
{{% expand title="Answer" %}}
**RSS**: Received Signal Strength
{{% /expand %}}


###### 16. What is **"**?
{{% expand title="Answer" %}}
yes
{{% /expand %}}
