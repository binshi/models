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



