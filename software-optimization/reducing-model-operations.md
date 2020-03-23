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

