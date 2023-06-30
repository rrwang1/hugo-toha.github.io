---
title: Secure sensing in AIoT
weight: 210
menu:
  sidebar:
    name: Secure sensing in AIoT
    identifier: secure
    parent: security
    weight: 10
---
> Main contributors from the group: Qun Song (topic coordinator), Zhenyu Yan

{{< vs 3 >}}

{{< img src="/posts/research/images/secure/img1.png" align="center">}}

{{< vs 3 >}}

> Image modified from [this](https://www.nbcnews.com/news/world/giant-pandas-are-no-longer-endangered-n643336), credit goes to the source. Also refer to [this paper](https://arxiv.org/pdf/1412.6572.pdf) for background

By 2025, it is estimated that there will be more than [41.6 billion](https://www.statista.com/statistics/1017863/worldwide-iot-connected-devices-data-size/) networked IoT devices. These IoT devices generate [79.4 zettabyes](https://www.statista.com/statistics/1017863/worldwide-iot-connected-devices-data-size/) data yearly, which is almost twice of today’s whole Internet ([44 zettabytes](https://www.weforum.org/agenda/2019/04/how-much-data-is-generated-each-day-cf4bddf29f/)). Transmitting such massive IoT data to the clouds for centralized processing will face communication bandwidth bottleneck. In addition, the communication networks will introduce uncertain time delays that are undesirable for many applications. To cope with these grand challenges, edge computing moves the computation on the IoT data closer to the data sources. Specifically, the IoT sensors and the last-mile data aggregators, acting as edge nodes, will undertake a significant portion of the computation on the IoT data; only data summaries and commands will be exchanged between the edge nodes and the cloud servers through the Internet when needed. As such, a hybrid computing paradigm consisting of edge computing at the front end and cloud computing at the back end will prevail along with the formation of IoT as a global infrastructure.

Deep neural network training and inference will be important forms of the computation at the edge. In particular, deep neural networks have good potential in bringing significant technological advancements for autonomous systems with a closed loop of sensing, decision, and actuation, among which the sensing step with high accuracy and high resilience is often thought most challenging. Recent research has provided various technical solutions to enable the training and inference at resource-constrained edge devices. However, the resilience (including security) aspect of edge AI has not been investigated adequately. The resilience studies in the general context of machine learning do not consider the specific constraints of edge AI, leading to difficulties in the edge AI deployment. The group is interested in studying the resilience issues of edge AI systems. As a preliminary study in this space, we have developed a moving target defense against adversarial example attacks on embedded visual sensing.

### DeepMTD

Recent studies show that deep models (e.g., multilayer perceptrons and convolutional neural networks) are vulnerable to adversarial examples, which are inputs formed by applying small but crafted perturbations to the clean examples in order to make the victim deep model yield wrong classification results. Systematic approaches have been developed to generate adversarial examples as long as the attackers acquire the deep model, where the attackers may know the internals of the model or not. Thus, adversarial examples present an immediate and real threat to deep visual sensing systems. Existing countermeasures are often designed to address certain adversarial examples and build their security on the attackers’ ignorance of the defense mechanisms. Thus, they do not address adaptive attackers.

{{< vs 3 >}}

{{< img src="/posts/research/images/secure/img2.png" align="center">}}

{{< vs 3 >}}

> Traffic sign adversarial examples constructed by [Carlini and Wagner’s approach](https://arxiv.org/abs/1608.04644). The two samples with red frames are clean examples; all other samples shown above will be misclassified by a deep neural network.

Beyond the static defense, we consider a [moving target defense (MTD)](https://www.sciencedirect.com/topics/computer-science/moving-target-defense) strategy. The figure below illustrates the workflow of our DeepMTD system. Specifically, it starts from a well-trained base model. When the system has spare computing resources, it adds independent perturbations to the parameters of the base model to generate multiple fork models. Each fork model is then used as the starting point of a retraining process. The retrained fork models are then commissioned for the visual sensing task. At run time, an input, which may be an adversarial example constructed based on the base model, is fed into each fork model. If the degree of inconsistency among the fork models’ outputs exceeds a predefined level, the input is detected as an adversarial example. The majority of the fork models’ outputs is yielded as the final result of the sensing task. If the system operates in the human-in-the-loop mode, the human will be requested to classify detected adversarial examples. We have implemented DeepMTD on edge computing platforms, [NVIDIA Jetson AGX Xavier](https://developer.nvidia.com/embedded/jetson-agx-xavier-developer-kit) and [NVIDIA Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit), with techniques to reduce the computing overhead (e.g., serial fusion with an early stopping mechanism). The detailed description of DeepMTD and the evaluation results can be found in our paper published on ACM SenSys’19 ([PDF](https://personal.ntu.edu.sg/tanrui/pub/deepMTD.pdf)).

{{< vs 3 >}}

{{< img src="/posts/research/images/secure/img3.png" align="center">}}

{{< vs 3 >}}

### Bibliography

#### Our research

\[1\] Moving Target Defense for Embedded Deep Visual Sensing against Adversarial Examples. Qun Song, Zhenyu Yan, Rui Tan. *The 17th ACM Conference on Embedded Networked Sensor Systems (SenSys), November 10-13, 2019, New York, NY, USA.*
