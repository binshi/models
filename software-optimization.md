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

