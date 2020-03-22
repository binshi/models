## Why Optimize? {#why-optimize-}

Remember, two common reasons for doing software optimization are:

1. To get better performance without changing the existing design or hardware
2. To use less system resources, in order to free them up for another application running on the same hardware

## Course Outline {#course-outline}

We'll be covering a wide range of tools and concepts that can help us achieve these optimization goals. Here's the outline we went over in the video, just for your reference:

* Performance Metrics
* Reducing Model Operations
  * Calculating Model Complexity
  * Using Efficient Layers
  * Comparing Layerwise Performance
  * Model Pruning
* Reducing Model Size
  * Quantization
  * Quantizing using DL Workbench
  * Model Compression
  * Knowledge Distillation
* Other Optimization Techniques
  * VTune Amplifier
  * Packaging your Application

## What You'll Build {#what-you-ll-build}

At the end of the course, you'll have the opportunity to demonstrate your new optimization skills by building an application to control your computer mouse pointer using your eye gaze. You'll start with video input of a person looking at different locations on the screen—either from your webcam or from a pre-recorded file that we'll provide. You'll then use multiple pre-trained models to track the eye movements and control the mouse pointer. The project will demonstrate your ability to work with multiple models in OpenVINO and your ability to benchmark and optimize your Inference Engine application.

---

What is Software Optimization?

* Why do we Need Software Optimization?
* Types of Software Optimization
* When to use Optimization Techniques
* Metrics to Measure Performance
* Other Metrics
  * Power
  * Cost
* When do we do Software Optimization?

**This course is all about **_**optimization**_**or improving the**_**performance**_**of a system.**

> **Performance **is a measure of how efficiently a system is performing its task. Typically, performance is measured in terms of the accuracy, inference speed, or energy efficiency of the system.

In our efforts to improve the performance of a system, there are generally two approaches we can take. The first is_hardware optimization_:

> **Hardware optimization **can be as simple as changing to a new hardware platform or as complicated as building a custom hardware specifically designed to increase the performance of a particular application.

And the second approach is _software optimization_:

> **Software optimization **involves making changes to your code or model to improve your application's performance. As applied to Edge computing, this will involve techniques and algorithms that reduce the computational complexity of the models.

# Types of Software Optimization {#types-of-software-optimization}

In most deep learning applications, loading and performing inference on a model takes up the most time. For this reason, many of the techniques that have been developed \(and many that we'll discuss in this course\) focus on **model optimization**.

> **Note:**Unless otherwise specified, whenever we talk about software optimization in this course, we are referring to optimizing the**model**and**not**the code.

Broadly speaking, there are two ways to optimize our model, based on how the model is changed. We can:

* **Reduce the size of the model**: This will reduce the time it takes to load the model and perform inference by removing unimportant or redundant parameters from our network.
* **Reduce the number of operations**: This will reduce the time taken to perform inference by reducing the number of operations or calculations needed to execute the network. This can be done by using more efficient layers and by removing connections in between neurons in our model.

Not all the algorithms mentioned only have one of the desired effects. For instance, while using separable convolutions reduces the number of operations we need to perform, a side-effect is that it also reduces the size of our model \(we will talk more about how it does that in the next lesson\). In later lessons, you will also see how we can further optimize our model by combining multiple techniques.

![](/assets/Screenshot 2020-03-22 at 5.52.36 PM.png)

![](/assets/Screenshot 2020-03-22 at 5.54.44 PM.png)

![](/assets/Screenshot 2020-03-22 at 5.55.42 PM.png)

![](/assets/Screenshot 2020-03-22 at 5.56.31 PM.png)

![](/assets/Screenshot 2020-03-22 at 5.59.04 PM.png)

# Performance Metrics {#performance-metrics}

So far in the course we have mentioned that software optimization helps increase performance, and also introduced a few algorithms that can be used to improve performance. However, performance is a very vague term. In this concept, we will learn some of the key metrics that we can use to measure the performance of our model.

> A**metric**is a quantity or an attribute of a system that can be measured. A metric should help us infer useful information about a system.

In the case of an Edge AI system, we want to measure two kinds of performance:

* **Software Performance**
  : This is used to understand the properties of our model and application. Model accuracy is a good example of a metric used to measure software performance.
* **Hardware Performance**
  : This is used to understand the properties of the device our model is running on. For instance, power consumption is a hardware metric that can be used to decide the size of battery our system will require.

![](/assets/Screenshot 2020-03-22 at 6.03.47 PM.png)

![](/assets/Screenshot 2020-03-22 at 6.05.53 PM.png)

| Operation |
| :--- |


|  | Energy \[pJ\] | Relative Cost |
| :--- | :--- | :--- |
| 32 bit int ADD | 0.1 | 1 |
| 32 bit float ADD | 0.9 | 9 |
| 32 bit Register File | 1 | 10 |
| 32 bit int MULT | 3.1 | 31 |
| 32 bit float MULT | 3.7 | 37 |
| 32 bit SRAM Cache | 5 | 50 |
| **32 bit DRAM Memory** | **640** | **6400** |

_Energy table for 45nm CMOS process._  
Adapted from Figure 1 of [Learning both Weights and Connections for Efficient Neural Networks \(Han et al., 2015\)](https://arxiv.org/pdf/1506.02626.pdf).

From the table, you can see that the energy taken to access memory is far greater than to perform operations. This is why we need to reduce the size of our model.

## Latency and Throughput {#latency-and-throughput}

Latency and throughput are closely related metrics but\_not\_the same thing.

> **Latency**is the time taken from when an image is available for inference until the result for that image is produced.
>
> **Throughput**is the amount of data that is processed in a given interval of time.

![](/assets/Screenshot 2020-03-22 at 6.14.34 PM.png)

![](/assets/Screenshot 2020-03-22 at 6.15.02 PM.png)

Some other Performance Metrics

In the last section we saw some of the important metrics that need to be optimized for an edge computing project. In this section, we will look at some other metrics that are also worth keeping in mind when designing your edge computing system.

![](/assets/Screenshot 2020-03-22 at 6.20.50 PM.png)

## FLOPs {#flops}

One way to measure inference time for your model is to calculate the total number of computations the model will have to perform. And a common metric for measuring the number of computations is the_FLOP_.

> Any operation on a float value is called a**F**loating**P**oint**O**peration or**FLOP**.

This could be an addition, subtraction, division, multiplication, or—again—any operation that involves a floating point value. By calculating the total**FLOPs**\(**F**loating**P**oint**O**peration**s**\) in a model, we can get a rough estimate of how computationally complex our model is and how long it might take to run an inference on that model.

## MACs {#macs}

Computations in neural networks typically involve a_multiplication_and then an_addition_. For instance, in a dense layer, we_multiply_the activation of a neuron with the weight for that neuron connection and then_add_it to another similar product:

Layer\_{output} = W\_{1}\*A\_{1}+W\_{2}\*A\_{2}+...+W\_{n}\*A\_{n}Layeroutput​=W1​∗A1​+W2​∗A2​+...+Wn​∗An​

> Since these operations involve performing a**multiplication**and then an**addition**, they are called**M**ultiply-**Ac**cumulate operation**s**or simply**MACs**.

Since each MAC involves two operations \(a multiplication and an addition\), this means that we can generally think of one MAC as involving two FLOPs:

> 1 MAC = 2 FLOPs

Actually, in some hardware \(especially hardware that is optimized for running many MACs\), the multiplication and addition are fused into a single operation. But for the purposes of this course, we'll assume the above \(1 MAC = 2 FLOPs\) is true when performing calculations.

# When do we do Software Optimization? {#when-do-we-do-software-optimization-}

Before you actually do software optimization, it is important to know when it will not give you the results you are looking for.

> _Premature optimization is the root of all evil_- Donald Knuth



