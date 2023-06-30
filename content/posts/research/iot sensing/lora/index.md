---
title: LoRa radio sensing
weight: 210
menu:
  sidebar:
    name: LoRa radio sensing
    identifier: lora
    parent: iot sensing
    weight: 10
---
> Main contributors from the group: Chaojie Gu (topic coordinator), Linshan Jiang, Dongfang Guo

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/LPWAN_0.jpg" align="center">}}

{{< vs 3 >}}

(https://www.smart-energy.com/magazine-article/licensed-spectrum-key-to-success-of-lpwa-networks/)

Low-power wide-area networks (LPWANs) form an important class of wireless networks for many geographically distributed Internet-of-Things (IoT) objects. LPWANs form a new pole in the spectrum of power consumption versus communication ranges, as shown in the figure below. LPWANs’ long-range communication capabilities will increase the degree of connectivity of IoT and enable deep penetration of networked intelligence into urban territories (e.g., wide areas, buildings, and underground structures) that have challenged the existing low-power short-range wireless technologies. Among various LPWAN technologies, we primarily focus on LoRaWAN due to its various advantages, such as the use of license-free industrial, scientific, and medical (ISM) frequency band, open data link layer specification, and low cost (several US dollars per unit).

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/LPWAN_1.png" align="center">}}

{{< vs 3 >}}


### One-hop out-of-band control planes using LoRaWAN

Many IoT networks will still be based on low-power multi-hop wireless networks. In the last decade, many wireless sensor networks are Zigbee-based multi-hop wireless networks. The recently announced Bluetooth 5 has added support of mesh network topology. However, from an engineering point-of-view, multi-hop wireless networks are often fragile and difficult to manage. To improve the network performance and manageability, some multi-hop wireless networks, especially those deployed for mission-critical tasks, have adopted centralized network controls. WirelessHART and ISA100.11a are examples. However, these networks still adopt in-band control planes, that is, the control-plane messages such as network status reports and routing schedules are delivered by the data-plane networks. The coupling between the control and data planes in the in-band scheme may lead to undesirable consequences. For example, when the data plane loses key routing nodes (e.g., due to node hardware/software fault and depletion of battery) or the control plane makes wrong control decisions (e.g., due to design defects or erroneous human operations), the data-plane network may fall apart to disconnected partitions. As a result, restorative network control commands in the control plane may not be able to reach the destination nodes.

A number of recent IoT node platforms are equipped with both short-range radio and LPWAN. For example, the OpenMote B platform and the TI CC1350 integrate both Zigbee and sub-GHz LPWAN radios; the TI CC1352R provides both BLE and sub-GHz LPWAN radios. Therefore, we propose to build one-hop out-of-band control planes using LPWAN and we choose LoRaWAN as the LPWAN technology to prototype our system called LoRaCP. The one-hop control planes will not be subject to the feasibility and manageability issues faced by the multi-hop data-plane networks. In addition, as the control-plane network only deliver key network status information and control commands, the bandwidth provision of LPWAN can meet the traffic demand of control-plane networks.

      



||||
| ---- | -- | ---- |
|{{< img src="/posts/research/images/lora/LoRaCP_0.png" alt="image alt" width="320px" position="center">}}|&nbsp;|{{< img src="/posts/research/images/lora/LoRaCP_1.png" alt="image alt" width="450px" position="center">}}|

The above figure shows our prototype LoRaCP end node and controller node, both providing Zigbee and LoRaWAN radios. We developed a software stack for LoRaCP to construct the control-plane network based on LoRaWAN radios. Our initial profiling experiments show that the TI CC1352R shown below (which is the CC1352R launchpad) can also support our approach of one-hop out-of-band control planes. The work of porting our software stack to CC1352R (the ported version can be called subG-CP) is in our plan.

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/CC1352R.png" align="center">}}

{{< vs 3 >}}


On a testbed of 16 LoRaCP nodes, we apply LoRaCP to separate the control-plane network of the Collection Tree Protocol (CTP) from its Zigbee-based data-plane network. LoRaCP brings substantial benefits such as increased frame delivery ratio in the presence of intensive Wi-Fi interference. This research was published on IEEE INFOCOM’18 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/LoRaCP-infocom.pdf)) and ACM Transactions on Sensor Networks ([PDF](https://personal.ntu.edu.sg/tanrui/pub/LoRaCP-TOSN.pdf)).

### Attack-aware data timestamping in LoRaWAN

LoRaWAN is promising for the applications of collecting low-rate data. Data samples need timestamps to make sense. In the traditional wireless sensor networks, the sensor nodes’ clocks are synchronized first, and then used to timestamp generated data. To tightly synchronize the sensor clocks, more network traffic for clock synchronization will be generated. This is bad for bandwidth-limited LoRaWAN. We showed that, since LoRaWAN follows a one-hop star network topology, the timestamping can be performed by the gateway upon the arrival of the data frame. This greatly saves the network bandwidth from the frequent clock synchronization.

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/LoRaTS_0.png" align="center">}}

{{< vs 3 >}}


However, this gateway-side timestamping is vulnerable to a frame delay attack that can be launched in three steps as shown in the above figure: (1) frame collision and eavesdropping, (2) data transfer, and (3) delay injection and frame replay. We conducted experiments in a campus network, and showed that, by setting up two attack devices (collider and eavesdropper) as shown in the below figure, all LoRaWAN end devices in the yellow polygon with an estimated area of 50,000 square meters will be affected by the attack.

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/real_attack.png" align="center">}}

{{< vs 3 >}}


***Vulnerable area of a campus LoRaWAN. (Satellite image credit: Google Map)***

To preserve the bandwidth efficiency of the gateway-side timestamping and develop awareness of the delay attack to avoid being misled unknowingly by the attack, we integrate a low-power listen-only software-defined radio (RTL-SDR) with the commercial-off-the-shelf LoRaWAN gateway to form our LoRaTS gateway, as shown in the left part of the figure below. We develop a software stack, as shown in the right part of the figure below, consisting of various radio signal processing algorithms to detect the carrier frequency biases introduced by the replay steps of the frame delay attack. Overall, LoRaTS is a solution that strikes a satisfactory trade-off between network efficiency and the security level required by typical LoRaWAN applications in implementing data timestamping. This research was published on IEEE ICDCS’20 ([PDF](https://github.com/tanrui/www/blob/master/pub/timestamping-ICDCS20.pdf)).

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/LoRaTS_1.png" align="center">}}

{{< vs 3 >}}



### In-Hall Localization with Standard LoRaWAN Uplink Frames

While LoRaWAN is mainly designed for establishing connectivity, being able to localize LoRaWAN devices unobtrusively using their uplink frames is desirable. The unobtrusiveness here means that no special software instrumentation is needed for the LoRaWAN end devices. As such, the localization service is free from entanglement with any other applications running on the LoRaWAN devices; the already deployed LoRaWANs can develop the localization capability seamlessly.

We design and evaluate a time difference of arrival (TDoA)-based, unobtrusive in-hall LoRaWAN localization (ILLOC) system for any off-the-shelf LoRaWAN end devices. ILLOC deploys multiple software-defined radio (SDR)-based anchors with known positions and estimates the position of an end device based on the anchors’ TDoA measurements regarding any single uplink frame from the end device. The design of ILLOC faces two challenges: (1) Narrowband: LoRa signals use narrow frequency bands, thus are long and smooth in time domain. Without special treatment, the uncertainty of arrival time estimation with 125 kHz bandwidth is up to 8 microseconds, which is translated to 2.4 km distance in ranging. (2) Inter-anchor clock skews: tight synchronization of the anchors’ clocks (ideally, to nanoseconds accuracy) is a basis of TDoA-based multilateration. However, implementing highly accurate clock synchronization via cabling can incur large deployment overhead.

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/illoc_system.png" align="center">}}

{{< vs 3 >}}



To address these technical challenges, we propose the ILLOC system featuring two LoRaWAN-specific techniques: (1) the cross-correlation among the differential phase sequences (DPS) received by two anchors to estimate TDoA, exploiting LoRa's CCS characteristic; and (2) the just-in-time (JIT) synchronization enabled by a specially deployed LoRaWAN end device providing time reference upon detecting a target device’s transmission, using LoRa’s Channel Activity Detection (CAD) feature. In a long tunnel corridor, a 70 × 32 sqm sports hall, and a 110 × 70 sqm indoor plaza with extensive non-line-of-sight (NLOS) propagation paths, ILLOC achieves median localization errors of 6 m (with 2 anchors), 8.36 m (with 6 anchors), and 15.16 m (with 6 anchors and frame fusion), respectively. The achieved accuracy makes ILLOC useful for applications including zone-level asset tracking, misplacement detection, airport trolley management, and cybersecurity enforcement like detecting impersonation attacks launched by remote radios. This research was published on ACM IMWUT/UbiComp'22 ([PDF](https://tanrui.github.io/pub/ILLOC-final.pdf)).

{{< vs 3 >}}

{{< img src="/posts/research/images/lora/illoc_plaza,png" align="center">}}

{{< vs 3 >}}


***The indoor plaza deployment (with extensive NLOS paths). The crosses in the call-out figure are the localization results for position 5.***





### Bibliography

#### Our research

[1] One-Hop Out-of-Band Control Planes for Low-Power Multi-Hop Wireless Networks. Chaojie Gu, Rui Tan, Xin Lou, Dusit Niyato. *The 37th Annual IEEE International Conference on Computer Communications (INFOCOM)*, April 15 - 19, 2018, Honolulu, HI.  
[2] One-hop Out-of-band Control Planes for Multi-hop Wireless Sensor Networks. Chaojie Gu, Rui Tan, Xin Lou. *ACM Transactions on Sensor Networks (TOSN)*. July 2019, Article No. 40.  
[3] Attack-Aware Data Timestamping in Low-Power Synchronization-Free LoRaWAN. Chaojie Gu, Linshan Jiang, Rui Tan, Mo Li, Jun Huang. *The 40th IEEE International Conference on Distributed Computing Systems (ICDCS)*, July 8-10, 2020, Singapore.  
[4] LoRa-Based Localization: Opportunities and Challenges. Chaojie Gu, Linshan Jiang, Rui Tan. *The 1st Workshop on Low Power Wide Area Networks for Internet of Things (LPNET), co-located with EWSN'19*, Feb 25, 2019, Beijing, China. Invited paper.
[5] ILLOC: In-Hall Localization with Standard LoRaWAN Uplink Frames. Dongfang Guo, Chaojie Gu, Linshan Jiang, Wenjie Luo, Rui Tan. *Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies (IMWUT)*, March, 2022.