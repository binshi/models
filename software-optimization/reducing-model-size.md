Different techniques for benchmarking model size and reducing model size. Here are the main topics we'll discuss:

* Quantization
* DL Workbench
  * Benchmark Models
  * Quantize Models
* Weight Sharing
  * Zip a model
* Knowledge Distillation

# Quantization {#quantization}

In this lesson, we will be learning about one of the most widely used and researched techniques for reducing model size:_quantization_.

> Broadly speaking,**quantization**is the process of mapping values from a larger set to a smaller one. In quantization, we might start off with a continuous \(and perhaps infinite\) number of possible values, and map these to a smaller \(finite\) set of values. In other words, quantization is the process of reducing large numbers of continuous values down into a limited number of discrete quantities.

In the present context, we can use quantization to map very large numbers of high-precision weight values to a lower number of lower-precision weight values—thus reducing the size of the model by reducing the number of bits we use to store each weight.

This lesson will explore the basics and discuss the two broad categories of quantization. We will be talking about how to quantize a network in a later lesson.

  
Here's the paper we referred to in the video, in case you want to check it out:

* [XNOR-Net: ImageNet Classification Using Binary Convolutional Neural Networks \(Rastegari et al., 2016\)](https://video.udacity-data.com/topher/2020/March/5e6e8859_xnor-net-imagenet-classification-using-binary-convolutional-neural-networks/xnor-net-imagenet-classification-using-binary-convolutional-neural-networks.pdf)

In the video you saw the different methods of quantization. Before we actually look at how networks are quantized, let's see the performance difference between a quantized model and a model with high-precision weights.

![](/assets/Screenshot 2020-03-23 at 3.28.20 PM.png)

![](/assets/Screenshot 2020-03-23 at 3.29.22 PM.png)

