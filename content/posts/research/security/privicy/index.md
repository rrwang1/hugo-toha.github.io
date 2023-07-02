---
title: Privacy-preserving sensing in AIoT
weight: 3
date: 2023-07-01
menu:
  sidebar:
    name: Privacy-preserving sensing in AIoT
    identifier: privacy
    parent: security
    weight: 3
hero: /images/section/privicy.jpg
---
> Main contributors from the group: Linshan Jiang (topic coordinator), Chaojie Gu, Mengyao Zheng (alumnus), Dixing Xu (alumnus)

### Privacy-Preserving Machine Learning in IoT

{{< vs 3 >}}

As explained in our [post](/research/secure/), a hybrid computing paradigm consisting of edge computing at the front end and cloud computing at the back end will prevail along with the formation of IoT as a global infrastructure. In addition, the deep neural network-based learning and inference will be important for improving the sensing performance of IoT systems. In a number of scenarios, the IoT edge and the cloud back end need to work together to implement AI-empowered sensing, during which privacy-sensitive data generated at the edge may be exchanged between the edge and the cloud. The group has ongoing research on designing and evaluating privacy-preserving learning and inference approaches in AIoT systems. Our challenge paper [(PDF)](https://github.com/tanrui/www/blob/master/pub/aichallengeiot19-final3.pdf) provides a taxonomy of the existing privacy-preserving learning and inference approaches.

### Privacy-preserving collaborative learning

{{< vs 3 >}}

{{< img src="/posts/research/images/privacy_preserving/collaborative_learning.png" align="center">}}

{{< vs 3 >}}

***A collaborative learning system***

Collaborative learning builds a machine learning model (e.g., a supervised classifier) based on the training data contributed by many participants. It is a desirable and empowering paradigm for AIoT systems. By leveraging on the much increased volume of training data and coverage of data patterns, collaborative learning will approach the intelligence of a crowd and improve the learning performance beyond that achieved by any single participant alone. Moreover, a resource-rich learning coordinator (e.g., a cloud computing service) allows the execution of advanced, compute-intensive machine learning algorithms to capture deeper structures in the aggregated data, whereas the participants (e.g., IoT objects) are often resource-constrained and incompetent for intensive computation. By contributing training data, the individual participants will enjoy the improved machine intelligence in return. However, the data contributed by the participants may contain privacy-sensitive information that should be protected from the curious cloud.

{{< vs 3 >}}

{{< img src="/posts/research/images/privacy_preserving/sample_1.png" align="center">}}

{{< vs 3 >}}

{{< img src="/posts/research/images/privacy_preserving/sample_2.png" align="center">}}

{{< vs 3 >}}

{{< img src="/posts/research/images/privacy_preserving/sample_3.png" align="center">}}

{{< vs 3 >}}

> Top: original data samples. Middle: obfuscated data samples using Gaussian random projection. Bottom: Additively perturbed data samples for differential privacy (epsilon=10).

[Federated learning](https://federated.withgoogle.com/) is a distributed machine learning scheme in which data remains at the individual participants and each participant will execute learning computation. However, the learning computation can be too heavyweight for resource-constrained devices such as embedded IoT sensors. **Different from the federated learning**, our work lets a participant device apply Gaussian random projection to obfuscate the data and then transmit to the cloud for training a deep neural network. The random projection introduces light computation overhead only and can be performed by mote-class IoT sensors. Every participant uses its own Gaussian matrix to prevent that the collusion between any participant and the curious cloud spoils the privacy protections for other participants. However, because of the participants’ independent projections, a pattern in the original data domain is split into N patterns in the obfuscated data domain (where N is the number of participants in the collaborative learning system). Our work systematically investigates the impact of the N on learning efficiency and also experimentally compares a number of baseline approaches on a hardware testbed, which include distributed machine learning, additive perturbation for differential privacy, and homomorphic encryption-based approach. The results are published on ACM/IEEE IoTDI’19 [(PDF)](https://personal.ntu.edu.sg/tanrui/pub/IoTDI19-final.pdf).

### Privacy-preserving remote inference

{{< vs 3 >}}

{{< img src="/posts/research/images/privacy_preserving/remote_inference.png" align="center">}}

{{< vs 3 >}}

Resource-constrained edge devices may not be able to execute very deep neural networks. In addition, deep neural networks may be intellectual properties that should remain in the cloud. To address these issues, the remote inference (i.e., the edge device transmits the inference data to the cloud for inference computation and gets the result) can be applied. But the inference data may contain privacy-sensitive information. Our work develops a **lightweight** and **unobtrusive** approach to obfuscate the inference data at the edge devices. It is lightweight in that the edge device only needs to execute a small-scale neural network; it is unobtrusive in that the edge device does not need to indicate whether obfuscation is applied. We apply our approach to three case studies of free spoken digit recognition, handwritten digit recognition, and American sign language recognition. Results show that our approach effectively protects the confidentiality of the raw forms of the inference data while preserving the cloud’s inference accuracy. The results are published in IEEE IoT Journal [(PDF)](https://arxiv.org/pdf/1912.09859.pdf).

### Bibliography

#### Our research

\[1\] Challenges of Privacy-Preserving Machine Learning in IoT. Mengyao Zheng, Dixing Xu, Linshan Jiang, Chaojie Gu, Rui Tan, Peng Cheng. *The 1st International Workshop on Challenges in Artificial Intelligence and Machine Learning for Internet of Things (AIChallengeIoT)* with SenSys'19, November 10, 2019, New York, NY, USA.
\[2\] On Lightweight Privacy-Preserving Collaborative Learning for Internet-of-Things Objects. Linshan Jiang, Rui Tan, Xin Lou, Guosheng Lin. *The 4th ACM/IEEE International Conference on Internet of Things Design and Implementation (IoTDI)*, April 16-18, 2019, Montreal, Canada. CPS-IoT Week 2019.
\[3\] Lightweight and Unobtrusive Data Obfuscation at IoT Edge for Remote Inference. Dixing Xu, Mengyao Zheng; Linshan Jiang, Chaojie Gu, Rui Tan, Peng Cheng. *IEEE Internet of Things Journal*. Special Issue on Artificial Intelligence Powered Edge Computing for Internet of Things. 2020.
