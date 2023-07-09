---
title: Powerline radiation sensing
weight: 4
date: 2023-07-01
menu:
  sidebar:
    name: Powerline radiation sensing
    identifier: powerline
    parent: iot sensing
    weight: 4
hero: /images/section/emr.png
---
> Main contributors from the group: Zhenyu Yan(topic coordinator), Qun Song, Rongrong Wang, Xu Liu, Linshan Jiang

{{< vs 3 >}}

Electric power distribution networks penetrate into all civil infrastructures. The service powerlines emit both electric fields and magnetic fields. The electric fields are induced by the voltages of the powerlines, and the magnetic fields are induced by the currents going through the powerlines. Because the power networks provide alternating currents at a nominal frequency (e.g., 50Hz in Singapore), the electric and magnetic fields emitted from the service powerlines also oscillate at the nominal frequency.

The electric and magnetic fields from the powerlines can be easily captured by sensors. In our research, we use a resonant circuit to sense the oscillating magnetic field. Precisely measuring the potential in an electric field is technically difficult. However, if we only want to capture the periodic variation of the electric field, it is easy: we simply sample an analog-to-digital converter (ADC) placed in the electric field, and the measurement is the difference between the potentials at ADC's input pin and ground pin. Connecting a conductor wire to the input pin will further amplify the ADC's measurement, because the conductor wire increases the equivalent distance between the ADC's input and ground pins in the electric field with gradients.

Therefore, instrumenting IoT devices with the powerline electric and magnetic fields sensing capability is not difficult. In our research, we study how to exploit the powerline electric and magnetic fields that are pervasive in indoor spaces to address various challenges faced by indoor IoT applications.

### Clock synchronization among wearable devices

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/floram.png" align="center">}}

{{< vs 3 >}}

Tightly synchronizing wearable devices is useful for a range of applications such as analyzing body movement, delivering audio streams synchronously using two wireless earphones, etc. The Network Time Protocol (NTP) implementation is subject to delays from the operating systems and the media access control protocols. Normally, NTP over a wireless connection can achieve sub-second accuracy only. To achieve high synchronization accuracy, the synchronization program will need low-level access to the radio hardware. However, this is difficult given that the wearable platforms and wearable operating systems are becoming heterogeneous.

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/sync_process.png" align="center">}}

{{< vs 3 >}}

Wearables are generally equipped with ADC to interface with various sensors. We use the ADC to capture the electric potential on the wearer’s body, which is induced by the ambient electric field emitted from the indoor power networks. The human body can effectively amplify the electric potential, such that the ADC can sense it without needing any amplification circuit. We integrate the periodic electric potential signal with the principle of NTP to develop a new clock synchronization protocol for wearables. We can achieve a synchronization accuracy of a few milliseconds among the wearable devices on the same human body. Moreover, our protocol can be also used to synchronize the wearable devices on multiple users who are located at different places in the same power grid. This research was published on ACM SenSys 2017 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/touchsync.pdf)) and IEEE Transactions on Mobile Computing ([PDF](https://personal.ntu.edu.sg/tanrui/pub/touchsync-TMC.pdf)).

### Natural timestamps in powerline electromagnetic radiation

The power grid frequency is not exactly the nominal frequency. Instead, it fluctuates around the nominal frequency, depending on the instantaneous status regarding the balance between the power generation and consumption in the grid. In particular, the power grid frequency is almost identical everywhere in the grid. Prior work has shown that the power grid frequency fluctuation trace of a certain length in time forms a natural timestamp, because the fluctuation trace is unique over time.

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/rtss_system.png" align="center">}}

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/island.jpg" align="center">}}

{{< vs 3 >}}

We design two types of sensors to capture the minute power grid frequency fluctuations. As shown in the above figure, the sensors of the first type are plugged into the power outlets to directly capture the voltage and extract the voltage’s cycle length at microsecond granularity. The sensors of the second type (shown in the below figure) are based on a resonant circuit to capture the magnetic field from the powerlines and extract the power grid frequency fluctuation. Our experiments show that the natural timestamps captured by the two types of sensors achieve microseconds and sub-second accuacies across the Singapore island. Based on the natural timestamps, we develop a number of IoT system functions such as timestamp recovery and secure clock synchronization protocols. This research was published on IEEE RTSS’16 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/grid-sync.pdf)), ACM/IEEE IPSN’17 (best paper award) ([PDF](https://personal.ntu.edu.sg/tanrui/pub/ipsn17-EMR.pdf)), and two papers on ACM Transactions on Sensor Networks ([PDF1,](https://personal.ntu.edu.sg/tanrui/pub/EMR-tosn.pdf) [PDF2](https://personal.ntu.edu.sg/tanrui/pub/sync-tosn.pdf)).

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/ipsn_system.png" align="center">}}

{{< vs 3 >}}

The clock synchronization based on the natural timestamps may have synchronization faults when there are localized disturbances in the power networks. We develop a network clock synchronization protocol to cross-check the peer-to-peer synchronization results and correct the faults. We analyzed the bounds of the fault correction capability and achieved a number of fundamental analytic results, applicable not only to our natural-timestamp-based systems, but also the general clock synchronization systems. This research was published on IEEE ICPADS’18 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/sync-resilience.pdf)) and ACM Transactions on Sensor Networks (accepted, in press).

### Location sensing using powerline electromagnetic radiation

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/mobicom_system.png" align="center">}}

{{< vs 3 >}}

Based on our work of wearables clock synchronization, we further inquire whether two wearables can perform same-body detection (i.e., the determination of whether they are on the same human body). We found that the electric potentials at two close locations on the same human body are similar, whereas those from different human bodies are distinct. Therefore, we achieved high same-body detection accuracy. This capability can be applied to develop a range of interesting system features for touchable IoT objects. For instance, in a home with multiple residents, when a user wearing his token turns on a TV set using a smart remote control, the control obtains the user identity from the token and instructs the TV set to list the user’s favorite channels. The user can also touch other smart objects to personalize them, e.g., touch a music player for the favorite music, switch on a light that automatically tunes to the user’s favorite color temperature or hue, etc. If the user can protect the personal wearable token well, the touch-to-access device authentication can also be used in more access-critical scenarios. For example, a touch on a smartphone or tablet unlocks the device’s screen automatically, allows in-app purchases, passes the parental controls, etc. Beyond the above use scenarios for improved convenience in access control, the touch-to-access scheme can also enhance the security of various systems. For instance, it can be used with fingerprint scanning to form a two-factor authentication against fake fingerprints. A wireless reader can access a worn medical sensor only if the reader has physical contact with the wearer’s skin. The contact enforces the wearer’s awareness regarding the access and prevents remote wireless attacks with stolen credentials. This research was published on ACM MobiCom’19 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/mobicom022-yanA.pdf)).

{{< vs 3 >}}

{{< img src="/posts/research/images/emr/mobicom_env.png" align="center">}}

{{< vs 3 >}}

The team also collaborates with researchers at University of Oxford to study the use of the magnetic field emitted from the powerlines for simultaneous localization and mapping (SLAM). The results were published on ACM MobiCom’18 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/com006-luA.pdf)).

### Bibliography

#### Our research

[1] Wearables Clock Synchronization Using Skin Electric Potentials. Zhenyu Yan, Rui Tan, Yang Li, Jun Huang. *IEEE Transactions on Mobile Computing (TMC).* Vol. 18, No. 12, Dec 2019.<br>

[2] Application-Layer Clock Synchronization for Wearables Using Skin Electric Potentials Induced by Powerline Radiation. Zhenyu Yan, Yang Li, Rui Tan, Jun Huang. *The 15th ACM Conference on Embedded Networked Sensor Systems (SenSys)*, November 5-8, 2017, Delft, The Netherlands.<br>

[3] Exploiting Electrical Grid for Accurate and Secure Clock Synchronization. Sreejaya Viswanathan, Rui Tan, David Yau.
*ACM Transactions on Sensor Networks (TOSN)*. Vol. 14, No. 2, July 2018.<br>

[4] Natural Timestamps in Powerline Electromagnetic Radiation. Yang Li, Rui Tan, David Yau. *ACM Transactions on Sensor Networks (TOSN)*. Vol. 14, No. 2, July 2018.<br>

[5] Natural Timestamping Using Powerline Electromagnetic Radiation. Yang Li, Rui Tan, David Yau. *The 16th ACM/IEEE International Conference on Information Processing in Sensor Networks (IPSN)*, April 18-21, 2017, Pittsburgh, PA, USA.<br>

[6] Exploiting Power Grid for Accurate and Secure Clock Synchronization in Industrial IoT. *The 37th IEEE Real-Time Systems Symposium (RTSS)*, November 29 - December 2, 2016, Porto Portugal.<br>

[7] Towards Touch-to-Access Device Authentication Using Induced Body Electric Potentials. Zhenyu Yan, Qun Song, Rui Tan, Yang Li, and Adams Wai Kin Kong. *The 25th Annual International Conference on Mobile Computing and Networking (MobiCom).* October 21-25, 2019, Los Cabos, Mexico.<br>

[8] Simultaneous Localization and Mapping with Power Network Electromagnetic Field. Chris Xiaoxuan Lu, Yang Li, Peijun Zhao, Changhao Chen, Linhai Xie, Hongkai Wen, Rui Tan, Niki Trigoni.
*The 24th Annual International Conference on Mobile Computing and Networking (MobiCom)*, October 29-November 2, 2018, New Delhi, India.<br>

[9] Resilient Clock Synchronization using Power Grid Voltage. Dima Rabadi, Rui Tan, David Yau, Sreejaya Viswanathan, Hao Zheng, Peng Cheng. *ACM Transactions on Cyber-Physical Systems (TCPS)*. Aug 2019, Article No. 31.<br>

[10] Taming Asymmetric Network Delays for Clock Synchronization using Power Grid Voltage. Dima Rabadi, Rui Tan, David Yau, Sreejaya Viswanathan. *The 12th ACM Asia Conference on Computer and Communications Security (ASIACCS)*, April 2-6, 2017, Abu Dhabi, UAE.<br>

[11] Resilience Bounds of Sensing-Based Network Clock Synchronization. Rui Tan, Linshan Jiang, Arvind Easwaran, Jothi Prasanna Shanmuga Sundaram. *The 24th IEEE International Conference on Parallel and Distributed Systems (ICPADS)*, December 11-13, 2018, Sentosa, Singapore.<br>

[12] Resilience Bounds of Network Clock Synchronization with Fault Correction. Linshan Jiang, Rui Tan, Arvind Easwaran. *ACM Transactions on Sensor Networks (TOSN)*. Accepted, in press.

#### Background

[1] Low-power clock synchronization using electromagnetic energy radiating from ac power lines. Anthony Rowe, Vikram Gupta, Ragunathan (Raj) Rajkumar. *The 7th ACM Conference on Embedded Networked Sensor Systems (SenSys ’09)*.<br>

[2] Flight: Clock calibration using fluorescent lighting. Zhenjiang Li, Cheng Li, Wenwei Chen, Jingyao Dai, Mo Li, Xiang-Yang Li, Yunhao Liu. *The 18th annual international conference on Mobile computing and networking (Mobicom ’12)*.<br>

[3] Applications of ENF criterion in forensic audio, video, computer and telecommunication analysis. Grigoras, Catalin. *Forensic science international 167.2-3 (2007): 136-145.*<br>

[4] Digital audio authenticity using the electric network frequency. Sanders, Richard W. *Audio Engineering Society 33rd International Conference: Audio Forensics-Theory and Practice*.<br>

[5] Seeing ENF: natural time stamp for digital video via optical sensing and signal processing. Garg, Ravi, Avinash L. Varna, and Min Wu. *The 19th ACM international conference on Multimedia*.<br>

[6] Electrisense: single-point sensing using EMI for electrical event detection and classification in the home.<br>

[7] The humming hum: Background noise as a carrier of ENF artifacts in mobile device audio recordings. Gupta, Sidhant, Matthew S. Reynolds, and Shwetak N. Patel. *The 12th ACM international conference on Ubiquitous computing.*<br>

[8] Exploring the use of ENF for multimedia synchronization. Su, Hui, Adi Hajj-Ahmad, Min Wu, and Douglas W. Oard. *In 2014 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP).*<br>

[9] An ultra-low-power human body motion sensor using static electric field sensing。 Cohn G, Gupta S, Lee TJ, Morris D, Smith JR, Reynolds MS, Tan DS, Patel SN. *The 2012 ACM Conference on Ubiquitous Computing.*<br>

[10] Humantenna: using the body as an antenna for real-time whole-body interaction. Cohn, Gabe, Daniel Morris, Shwetak Patel, and Desney Tan. *The SIGCHI Conference on Human Factors in Computing System*. 2012.<br>

[11] Your noise is my command: sensing gestures using the body as an antenna. Cohn, Gabe, Daniel Morris, Shwetak N. Patel, and Desney S. Tan. *The SIGCHI Conference on Human Factors in Computing Systems.* 2011.<br>

[12] Design and implementation of a new thin cost-effective ac hum based touch sensing keyboard. Elfekey, Hatem M., and Hany Ayad Bastawrous. *2013 IEEE International Conference on Consumer Electronics (ICCE).*<br>

[13] Platypus: Indoor Localization and Identification Through Sensing of Electric Potential Changes in Human Bodies. Grosse-Puppendahl, Tobias, Xavier Dellangnol, Christian Hatzfeld, Biying Fu, Mario Kupnik, Arjan Kuijper, Matthias R. Hastall, James Scott, and Marco Gruteser. *The 14th Annual International Conference on Mobile Systems, Applications, and Services*<br>

[14] Finding common ground: A survey of capacitive sensing in human-computer interaction. Grosse-Puppendahl, Tobias, Christian Holz, Gabe Cohn, Raphael Wimmer, Oskar Bechtold, Steve Hodges, Matthew S. Reynolds, and Joshua R. Smith. T*he 2017 CHI Conference on Human Factors in Computing Systems*.<br>

[15] Biometric Touch Sensing: Seamlessly Augmenting Each Touch with Continuous Authentication. Holz, Christian, and Marius Knaust. *The 28th Annual ACM Symposium on User Interface Software & Technology*.<br>

[16] EM-Sense: Touch Recognition of Uninstrumented, Electrical and Electromechanical Objects. Laput, Gierad, Chouchang Yang, Robert Xiao, Alanson Sample, and Chris Harrison. *The 28th Annual ACM Symposium on User Interface Software & Technology.*<br>

[17] Remote detection of human electrophysiological signals using electric potential sensors. R. J. Prancea, S. T. Beardsmore-Rust, P. Watson, C. J. Harland, and H. Prance. *Applied Physics Letters 93.3 (2008): 033906.*<br>

[18] Device Pairing at the Touch of an Electrode. Roeschlin, Marc, Ivan Martinovic, and Kasper Bonne Rasmussen. *NDSS.* Vol. 18. 2018.<br>

[19] EM-ID: Tag-less identification of electrical devices via electromagnetic emissions. Yang, Chouchang, and Alanson P. Sample. *2016 IEEE International Conference on RFID (RFID).*<br>

[20] EM-Comm: Touch-based Communication via Modulated Electromagnetic Emissions. Yang, Chouchang Jack, and Alanson P. Sample. *The ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies.* 1.3 (2017): 1-24.<br>

[21] Wideband Powerline Positioning for Indoor Localization. Erich P. Stuntebeck, Shwetak N. Patel, Thomas Robertson, Matthew S. Reynolds, and Gregory D. Abowd. *The 10th international conference on Ubiquitous computing.* 2008<br>


(Disclaimer: This list may not be complete. Please contact us if you think some other papers should appear in this list due to the relevance to powerline electromagnetic sensing.)
