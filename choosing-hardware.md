As IoT devices become more common in our daily lives, an increasing number of industries—from advanced medical research and personalized healthcare to smart transportation and retail—are relying on video for critical insights and competitive growth. Traditionally, AI and Machine Learning algorithms have been run either on cloud servers or on desktop systems with add-in GPUs, but there is an increasing need to process data on local hardware devices.

Today, there are many different options for edge hardware. But which hardware should you choose? How can you know if a particular piece of hardware is the right one for a particular need? Since the costs of different pieces of hardware can vary widely, this is a critical question—and exactly the question we'll be tackling in this course.

we'll cover four main hardware types:

* CPU
* GPU
* VPU
* FPGA

We'll discuss not only the specifications for these hardware types, but also:

* How to figure out which devices are the best fit for your application.
* How to determine what hardware to use with the
  _OpenVino Toolkit_
  and match up the hardware,
  _inference model_
  , and the
  _inference rate_
  needed by your application.

Finally, we will introduce the[Intel DevCloud](https://devcloud.intel.com/edge/)for the edge, where you can test your application on a large range of hardware, including various CPUs, GPUs, VPUs, and a FPGA. Using the DevCloud will allow you to determine which hardware types best fit your needs and budget.

Choosing the best hardware for our edge computing system

* * Development system
  * Deployment system
* Product development flow
* Choosing an AI Model
* Basic Terminology
  * CPUs
  * AI Accelerators
* Intel DevCloud for the Edge

![](/assets/Screenshot 2020-03-27 at 4.14.03 PM.png)

When you start a deep-learning project, you will usually follow these 5 steps:

1. Data Collection
2. Data Processing
3. Model Selection and Training \(Compute Intensive\)
4. Application Development
5. Deploy and Improve

To pick the right hardware, you will need to be able to strike a balance between the different specifications and requirements of the system that you are building. Throughout this course, we will learn about the different devices and their characteristics, helping you to choose the right hardware for your next edge device.

# Design of Edge AI Systems {#design-of-edge-ai-systems}

## Stakeholders {#stakeholders}

In designing Edge AI systems, there are multiple stakeholders that are part of the product design process. In this course, we focus on the role played by the IoT engineer—but it's important to understand how you as the engineer would interact with the other stakeholders. Typical stakeholders are:

* Data Scientists
* Engineers or Software Developers
* End-Users

Let's talk about these roles and how they interact.

In the design of Edge AI systems, the AI models are first developed and trained by**data scientists**. Because this step is computationally expensive, it is typically performed on high-end servers \(not edge devices\). These models are then available to the IoT**engineer**, who works with the**end user**to determine their needs and design a system that will work well for their particular problem. The engineer's job is to understand the constraints and requirements of the user and figure out which model and hardware will best fit their needs.

## Basic Approach to Developing a Product {#basic-approach-to-developing-a-product}

Generally speaking, the development of Edge AI systems can be viewed as a cycle that involves five steps:

1. Analyze
2. Design
3. Develop
4. Test
5. Deploy

We'll first do a brief overview of the cycle and then go into more detail about each step over the coming pages.

![](/assets/Screenshot 2020-03-27 at 4.18.24 PM.png)![](/assets/Screenshot 2020-03-27 at 4.20.37 PM.png)

# Analyze {#analyze}

In developing an Edge AI system, the first phase is to **analyze **the problem.

During this phase, you \(as the IoT engineer\) work with the end-user to understand what they are wanting to do and to get all of the requirements and constraints involved. For example, you might be working with a client who has a self-checkout system at a supermarket. They might be using cameras to record the customers, and want to run inference on the video feed to check that the number of items scanned matches the number of items detected in the video feed, in order to detect possible theft.

The client will have certain constraints—for example, maybe they have four cameras, a limited budget, and a PC running in the office that they can potentially use to do the inference. Understanding all of these needs and constraints is a critical step if you want to present an effective solution to the customer.

# Design {#design}

In the next stage of the process, you work out the overall **design **of the system, including the different components and how the data will flow from one to the next. In the example, we've been discussing, the cameras would be recording video, which would be sent to the edge device where the inference would be run. The output from the edge device might then be sent to a staff member's device to notify them of possible theft.

At this stage, you as the engineer will probably have a good hypothesis about what hardware solution is most appropriate. For example, in the scenario described above, maybe you have a guess that the CPU in the client's existing PC will be sufficient. But you don't know for sure until you test it.

Let's revisit the example from the previous page and discuss the design of the system in more detail. \(You don't need to understand every detail of this design—we're showing it to you so that you have an idea of the sort of thing that goes into the design phase of the development cycle.\)

![](/assets/Screenshot 2020-03-27 at 4.27.04 PM.png)

# Develop {#develop}

In the next stage of the process, you'll **develop **a prototype application, using the OpenVINO Toolkit. You'll select which AI models you think might work best to conduct the inference. And similarly, you'll decide which hardware types are potential candidates.

![](/assets/Screenshot 2020-03-27 at 4.29.41 PM.png)

![](/assets/Screenshot 2020-03-27 at 4.30.56 PM.png)

# Test and Deploy {#test-and-deploy}

## Test {#test}

At this point, you may have a pretty good idea of what hardware you think will work best—but you really can't know until you**test**it. Actually purchasing the hardware to test your system would be prohibitively expensive and isn't necessary—your laptop or a virtual machine can provide a starting point. In this course, we'll be showing you how to use the Intel DevCloud to try out a variety of different devices, so that you can develop your system without having to first spend money on any actual hardware yourself.

## Deploy {#deploy}

Now that you've tested your design and selected your hardware, the last step is to actually**deploy**the system for the client. But your work is not over at this point. Despite all of the design work and testing you've done, there will probably be room for improvement based on real-world usage. For example, maybe you thought a fanless, closed CPU system was good—but once the system is actually deployed, discover that the system overheats during the summer months. Based on this data, you can create a revised set of requirements and constraints—and feed this back into the beginning of the development process, analyzing and redesigning to improve the system.

# Basic Terminology {#basic-terminology}

![](/assets/Screenshot 2020-03-27 at 4.35.56 PM.png)![](/assets/Screenshot 2020-03-27 at 4.36.06 PM.png)![](/assets/Screenshot 2020-03-27 at 4.38.28 PM.png)![](/assets/Screenshot 2020-03-27 at 4.39.51 PM.png) 

#### _CPU \(Central Processing Unit\)_ {#cpu-central-processing-unit-}

The actual subset of the device that performs the basic operations of running the operating system or reading and writing from memory or interfaces with other devices. Often used synonymously with microprocessor or core.

---

#### _GPU \(Graphics Processing Unit\)_ {#gpu-graphics-processing-unit-}

Normally used for displaying videos or adjusting photos; can also be used to run inference on OpenVino models.

---

#### _AI Accelerators_ {#ai-accelerators-}

Hardware specifically designed to handle AI requirements and speed up processes used in AI and machine learning.

---

#### _VPU \(Vision Processing Unit\)_ {#vpu-vision-processing-unit-}

A processor specifically optimized for running the types of calculations that occur frequently in convolutional neural networks. Myriad X and Google's TPU are examples of VPUs.

---

#### _NCS-2 \(Neural Compute Stick 2\)_ {#ncs-2-neural-compute-stick-2-}

A specific implementation of a VPU \(in this case the Myriad-X\) with 4GB of memory and a USB3 form factor. This is the lowest cost and lowest performing type of accelerator.

---

#### _FPGA \(Field Programmable Gate Array\)_ {#fpga-field-programmable-gate-array-}

OpenVino supports several boards from different manufacturers with an Arria-10 device to run AI models. These are generally the highest performing type of accelerator, but they also tend to support the smallest number of layers. FPGAs are therefore often run in**Hetero**mode to specify a fallback device - typically the CPU - to handle any unsupported layers.

---

#### _HDDL/VAD \(High Density Deep Learning / Vision Accelerator Design\)_ {#hddl-vad-high-density-deep-learning-vision-accelerator-design-}

Devices with multiple Myriad-X chips \(either 4 or 8\), which appear to the system as if you plugged in multiple USB NCS-2s

---

#### _TDP \(Thermal Design Power\)_ {#tdp-thermal-design-power-}

The maximum amount of heat generated by a processor that the cooling system is designed to dissipate under any workload.

---

#### _Hetero_ {#hetero}

API option that allows you to specify more than one hardware device to run the inference. Hetero mode is often used with an FPGA and a CPU. Since FPGAs do not support all of the layers of every kernel or model, the Hetero mode specifies a 'fallback' device to use for these unsupported layers.

---

#### _Multi_ {#multi}

API option that is run when you want to run multiple copies of the same inference. One inference will run on each of the specified devices.

---

#### _SYNC mode_ {#sync-mode}

API option that causes the application to wait for inference to complete.

---

#### _ASYNC mode_ {#async-mode}

API option that allows inference and the application to run simultaneously.

  


