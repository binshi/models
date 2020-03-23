How to measure the performance of our model

* * Using FLOPs\(Floating Point Operations per second\) as a performance metric
  * Using MACs\(multiply-accumulate operations\) as a performance metric
* How to use efficient layers in our model
  * Separable Convolutions
  * Pooling Layers
* How to use OpenVINO to measure the layerwise performance
* Model pruning

#### Calculating Model FLOPs: Dense Layers

![](/assets/Screenshot 2020-03-23 at 8.37.52 AM.png)

## FLOPs vs. FLOPS {#flops-vs-flops}

Hardware devices are typically rated for the number of Floating Point Operations \(FLOPs\) they can perform in a _second_.

> This is referred to as **F**loating **P**oint **O**perations per **S**econd or **FLOPS**.

It is easy to get _FLOPs_\(with a lower-case "s"\) confused with _FLOPS_\(with a capital "S"\).

**FLOPs **stands for \_floating-point operations \_and refers to a **quantity**.

**FLOPS **stands for \_floating-point operations \_and refers to a **rate**.

For example, if we say "100 FLOPs", we are simply referring to the number of operations—whereas if we say, "100 FLOPS", this is referring to the number of operations a model performs in a second.

![](/assets/Screenshot 2020-03-23 at 8.44.46 AM.png)

![](/assets/Screenshot 2020-03-23 at 8.45.50 AM.png)

![](/assets/Screenshot 2020-03-23 at 8.46.40 AM.png)

![](/assets/Screenshot 2020-03-23 at 9.00.02 AM.png)

## Task 1: Calculate Model FLOPs {#Task-1:-Calculate-Model-FLOPs}

#### Layer 1: Conv2D {#Layer-1:-Conv2D}

Input shape: 1x1x28x28  
Kernel shape: 3x3  
Number of kernels: 10

Output shape: The shape for a single dimension will be = \(28-3\)+1 = 26 So our output shape will be 26x26 Because we have 10 kernels, our actual output shape will be 10x26x26

MAC =&gt; \[Total number of kernels\(10\) \* shape of our output\(26x26\) \* shape of our kernel\(3x3x1\)\] \* For FLOPS\(2\)

FLOPS: 10x26x26x3x3x1x2 = 121,680

#### Layer 2: Average Pool 2D {#Layer-2:-Average-Pool-2D}

Input Shape: 10x26x26  
Kernel Shape: 2x2

Output Shape: 10x13x13

shape of output\(13x13\) \* shape of kernel\(2x2\) \* depth of input\(10\)

FLOPS: 13x13x2x2x10 = 6,760

#### Layer 3: Conv2D {#Layer-3:-Conv2D}

Input shape: 10x13x13  
Kernel shape: 3x3  
Number of kernels: 5

Output shape: The shape for a single dimension will be = \(13-3\)+1 = 11 So our output shape will be 11x11 Because we have 5 kernels, our actual output shape will be 5x11x11

FLOPS: 5x11x11x3x3x10x2 = 108,900

#### Layer 4: Fully Connected {#Layer-4:-Fully-Connected}

Input shape: 11x11x5: 605  
Output shape: 128

FLOPS: 605x128x2 = 154,880

#### Layer 5: Fully Connected {#Layer-5:-Fully-Connected}

Input Shape: 128  
Output Shape: 10

FLOPS: 128x10x2 = 2560

Total FLOPS: 121680+6760+108900+154880+2560 = 394,780

# Using Efficient Layers: Separable Convolutions {#using-efficient-layers-separable-convolutions}

We just saw how to reduce the number of parameters flowing through our model by using pooling layers. Pooling layers allow us to reduce the operations in our model without using too many FLOPs. But at the same time, a lot of data gets lost.

While using pooling layers does solve the problem of having a lot of parameters, it does not attack the problem at its source: the convolutional layer. On this page, we will see how we can reduce the number of operations in a convolutional layer without changing the input and output shape of the layer.

