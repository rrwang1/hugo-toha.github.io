---
title: Acoustic and imagery sensing
weight: 210
menu:
  sidebar:
    name: Acoustic and imagery sensing
    identifier: acoustic
    parent: iot sensing
    weight: 10
---
> Main contributors from the group: Wenjie Luo (topic coordinator), Qun Song, Chaojie Gu, Zhenyu Yan, Duc Van Le, Siyuan Zhou, Jiale Chen, Qiping (Joy) Yang

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/cover.png" align="center">}}

{{< vs 3 >}}
(https://trajectorymagazine.com/generating-synthetic-data-for-remote-sensing/)

The acoustic and imagery sensing modalities provide abundant information about the sensed target. As a result, the volume of an acoustic/imagery signal sample is often high and the data processing to extract useful information requires intensive computing. Such characteristics introduce various system challenges in data acquisition, computing, storage, and network transmission on networked sensing platforms with constrained processing capabilities, network bandwidth, and bounded energy supply.

Dr. Rui Tan’s early research designed efficient systems for 1) networked seismic sensing that introduces similar challenges [1, 2, 3] and 2) robotic fish’s visual sensing for monitoring aquatic debris [4] and harmful aquatic processes (e.g., oil spill and harmful algal blooms) [5]. The group is currently developing an acoustic echolocation system based on deep learning and networked imagery sensing for inspection tasks in manufacturing systems. This page briefly describes a completed preliminary work of using inaudible echos for room recognition.

### Room recognition using inaudible echos

Location awareness is increasingly needed by mobile applications. As of November 2017, 62% of the top 100 free Android Apps on Google Play require location services. While GPS can provide outdoor locations with satisfactory accuracy, determining indoor locations has been a hard problem. Our work designs a practical room-level localization approach for off-the-shelf smartphones using their built-in audio systems only. Room-level localization is desirable in a range of ubiquitous computing applications. For instance, in a hospital, knowing which room that a patient is in is important to responsive medical aid when the patient develops an emergent condition (e.g., falling in a faint). In a museum, knowing which exhibition chamber that a tourist is in can largely assist the automation of her multimedia guide that is often provided as a mobile App nowadays. In a smart building, the room-level localization of the residents can assist the automation of illumination and air conditioning to improve energy efficiency and occupant comfort.

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/fig_3.png" align="center">}}

{{< vs 3 >}}

In our approach, a smartphone uses its loudspeaker to transmit a 2-millisecond narrowband acoustic signal at a frequency (e.g., 20kHz) beyond human’s hearing limit and uses its microphone to capture the reverberation from the indoor environment (typically, a room) for 100 milliseconds. Based on the spectrogram of the 100-millisecond reverbnation, our approach can recognize the indoor environment via a machine learning algorithm. The short audio recording time (i.e., 100 milliseconds) helps preserve the user’s privacy. However, the environment’s response to such a short-term and band-limited acoustic excitation may contain limited information about the environment. To address this, we employ deep learning to train a convolutional neural network for the room recognition.

We conducted extensive experiments to evaluate our approach. Results show 99.7%, 97.7%, 99%, and 89% accuracy in differentiating 22 and 50 residential/office rooms, 19 spots in a quiet museum, and 15 spots in a crowded museum, respectively. The below figures show several example room types and university tutorial rooms having similar appearance that are employed in our evaluation experiments, as well as the 19 and 15 spots in the two different museums that we experimented with. The results were published on ACM Ubicomp’18 [(PDF)](https://personal.ntu.edu.sg/tanrui/pub/RoomRecognize.pdf).

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/fig_12.png" align="center">}}

{{< vs 3 >}}

|                          |                                                                                                            |        |                                                                                                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------- |
| &nbsp;&nbsp;&nbsp;&nbsp; | {{< img src="/posts/research/images/sensing/fig_24.png" alt="image alt" width="480px" position="center">}} | &nbsp; | {{< img src="/posts/research/images/sensing/fig_25.png" alt="image alt" width="200px" position="center">}} |

### Imagery sensing for manufacturing system

Computer vision has become an essential component of the automated inspection processes in smart manufacturing systems. We design and implement an Edge-Fog Camera (EFCam) system that can adapt its configuration with deep reinforcement learning. EFCam leverages the off-the-shelf battery-powered wireless camera called ESP32-CAM at the edge and fog node (e.g., Raspberry Pi) to achieve cordless and energy-efficient operations in industrial systems. The wireless cameras can offer various benefits such as easy deployment, mobility support, and unobtrusiveness to the ongoing industrial processes. Additionally, wall-powered wireless fog node with sufficient computing resources is used to support the camera in facilitating deep learning (DL)-based image processing with short jitters and delays.

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/fig_efcam.png" align="center">}}

{{< vs 3 >}}

In our EFCam system, the wireless camera performs image pre-processing, and then transmits the data to a resourceful edge-fog node for advanced DL-based visual processing. The EFCam also applies the deep reinforcement learning (DRL) to adapt the camera configuration to maintain the desired visual sensing performance with the minimum energy consumption under dynamic variations of industrial application requirement and wireless channel conditions at the factory. The detailed design of EFCam can be found in our IEEE SECON’21 paper[(PDF)](https://github.com/tanrui/www/blob/master/pub/EFCam-SECON21.pdf) and its extended version in TMC[(PDF)](https://tanrui.github.io/pub/EFCam-TMC.pdf).

We have applied EFCam to improve the quality control of the ink cartridge manufacturing lines at the factories of Hewlett-Packard (HP) Inc. Our target application is HP’s ink extraction testing (IET), the ﬁnal quality control procedure used to detect any defective batch in which the ink cartridges’ performance deviates from the speciﬁcation. The IET machine controls a stepper motor pump to extract ink from the cartridge and uses a liquid pressure sensor continuously measures the pressure in the tube. The measured pressure profile is assessed to determine the performance of the tested cartridge. However, formation of air bubbles with a sufﬁciently large volume can affect the liquid pressure measurement and cause many false alarms.

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/fig_iet.png" align="center">}}

{{< vs 3 >}}

To reduce the recall rate in detecting the defective cartridges, we apply EFCam to monitor the air bubbles at the Y-joint of tube. The camera applies a two-step image processing pipeline. The first step runs the convolutional neural network to detect the presence of the air bubbles. The second step measures the volume of the detected air bubbles using a computer vision (CV)-based image processing framework. The details of this application can be found in our IEEE SECON’21 paper[(PDF)](https://tanrui.github.io/pub/IET-SECON21.pdf).

### Rescuing speech recognition from microphone heterogeneity

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/phyaug.png" align="center">}}

{{< vs 3 >}}

Run-time domain shifts from training-phase domains are common in sensing systems designed with deep learning. The shifts can be caused by sensor characteristic variations and/or discrepancies between the design-phase model and the actual model of the sensed physical process. In the cyber-physical sensing applications, both the monitored physical processes and the sensing apparatus are often governed by certain first principles. In this paper, we investigate the approach to exploit such first principles as a form of prior knowledge to reduce the demand on target-domain data for model transfer. We propose a new approach called physics-directed data augmentation (PhyAug). Specifically, we use a minimum amount of data collected from the target domain to estimate the parameters of the first principle governing the domain shift process and then use the parametric first principle to generate augmented target-domain training data. Finally, the augmented target-domain data samples are used to transfer or retrain the source-domain DNN.

In this paper, we apply PhyAug two acoustic sensing applications and quantify the performance gains compared with other transfer learning approaches. The first and the second case studies aim to adapt DNNs for keyword spotting (KWS) and automatic speech recognition (ASR) respectively to individual deployed microphones. The domain shifts are mainly from microphone’s hardware characteristics. Our tests show that the microphone can lead to 15% to 35% absolute accuracy drops, depending on the microphone quality. Instead of collecting training data using the target microphone, PhyAug uses a smartphone to play a 5-second white noise and then estimates the frequency response curve of the microphone based on its received noise data. Then, using the estimated curve, the existing samples in the factory training dataset are transformed into new training data samples, which are used to transfer the DNN to the target domain of the microphone by a retraining process. Experiment results show that PhyAug recovers the microphone-induced accuracy loss by 53%-72% and 37%-70% in KWS and ASR, respectively. PhyAug also outperforms the existing approaches including [FADA](https://papers.nips.cc/paper/2017/file/21c5bba1dd6aed9ab48c2b34c1a0adde-Paper.pdf) that is a domain adaptation approach based on adversarial learning and [Mic2Mic](https://arxiv.org/pdf/2003.12425.pdf) and [CDA](https://dl.acm.org/doi/10.1109/IPSN.2018.00048) that are designed specifically to address microphone heterogeneity. Note that KWS and ASR diﬀer significantly in DNN model depth and complexity. Specifically, we use DeepSpeech2 ASR model, it has 86.6 million weights, which is 175 times larger than the KWS CNN in terms of the weight amount.

{{< vs 3 >}}

{{< img src="/posts/research/images/sensing/phy.png" align="center">}}

{{< vs 3 >}}

### Bibliography

#### Our research

[1] Quality-driven Volcanic Earthquake Detection using Wireless Sensor Networks. Rui Tan, Guoliang Xing, Jinzhu Chen, Wen-Zhan Song, Renjie Huang. *The 31st IEEE Real-Time Systems Symposium (RTSS)*, pp. 271-280, Nov 30 - Dec 3, 2010, San Diego, CA, USA.
[2] Volcanic Earthquake Timing using Wireless Sensor Networks. Guojin Liu, Rui Tan; Ruogu Zhou; Guoliang Xing; Wen-Zhan Song; Jonathan M. Lees. *The 12th ACM/IEEE Conference on Information Processing in Sensor Networks (IPSN)*, April 8-11, 2013, Philadelphia, PA, USA. CPS Week 2013. (The first two authors are listed in alphabetic order.)
[3] ORBIT: A Smartphone-Based Platform for Data-Intensive Embedded Sensing Applications. Mohammad-Mahdi Moazzami, Dennis E. Phillips, Rui Tan, Guoliang Xing. *IEEE Transactions on Mobile Computing (TMC)*. Vol. 16, No. 3, pp. 801-815, March 2017.
[4] Aquatic Debris Monitoring Using Smartphone-Based Robotic Sensors. Yu Wang, Rui Tan, Guoliang Xing, Jianxun Wang, Xiaobo Tan, Xiaoming Liu, Xiangmao Chang. *The 13th ACM/IEEE International Conference on Information Processing in Sensor Networks (IPSN)*, April 15-17, 2014, Berlin, Germany.
[5] Samba: A Smartphone-Based Robot System for Energy-Efficient Aquatic Environment Monitoring. Yu Wang, Rui Tan, Guoliang Xing, Jianxun Wang, Xiaobo Tan, Xiaoming Liu. *The 14th ACM/IEEE International Conference on Information Processing in Sensor Networks (IPSN)*, April 13-17, 2015, Seattle, WA, USA.
[6] Deep Room Recognition Using Inaudible Echos. Qun Song, Chaojie Gu, Rui Tan. *Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies (IMWUT)*. *The ACM International Joint Conference on Pervasive and Ubiquitous Computing (Ubicomp)*, October 8-12, 2018, Singapore.
[7] EFCam: Configuration-Adaptive Fog-Assisted Wireless Cameras with Reinforcement Learning. Siyuan Zhou, Duc Van Le, Joy Qiping Yang, Rui Tan, Daren Ho. *International Conference on Sensing, Communication and Networking (SECON)*, July 6-9, 2021, held online.
[8] Configuration-Adaptive Wireless Visual Sensing System with Deep Reinforcement Learning. Siyuan Zhou, Duc Van Le, Rui Tan, Joy Qiping Yang, Daren Ho. *IEEE Transactions on Mobile Computing (TMC)*
[9] Improving Quality Control with Industrial AIoT at HP Factories: Experiences and Learned Lessons. Joy Qiping Yang, Siyuan Zhou; Duc Van Le; Daren Ho; Rui Tan. *International Conference on Sensing, Communication and Networking (SECON)*, July 6-9, 2021, held online.
