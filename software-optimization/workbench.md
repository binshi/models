# Benchmarking Model Performance {#benchmarking-model-performance}

**Deep Learning Workbench \(DL Workbench\)**is a graphical user interface \(GUI\) for OpenVINO that you can use to benchmark your models and perform optimizations on them. In this section, we'll walk through the basics of how to use DL Workbench to benchmark model performance.

To be able to follow along, you'll need to first download and install the DL Workbench. Detailed instructions can be found[here](https://docs.openvinotoolkit.org/latest/_docs_Workbench_DG_Install_Workbench.html).

> **⚠️ Important note:**Unfortunately, DL Workbench cannot currently be installed on Windows Home edition. If you are using a Windows machine, you will need to upgrade to Windows Pro/Education or switch to a different OS \(such as Ubuntu\).

In short, you will need to:

* Download
  `docker`
  \(for Ubuntu 16.04 and 18.04\) or
  `Docker Desktop`
  \(for Windows\).
* Run the
  `docker`
  command found
  [here](https://docs.openvinotoolkit.org/latest/_docs_Workbench_DG_Install_from_Docker_Hub.html#install_dl_workbench_from_docker_hub_on_windows_os)
* You can also start the DL Workbench using your OpenVINO toolkit package. Instructions for that can be found
  [here](https://docs.openvinotoolkit.org/latest/_docs_Workbench_DG_Install_from_Package.html)

The model that we will be benchmarking is a`Mobilenet V1`model. You can download the model from[here](http://download.tensorflow.org/models/mobilenet_v1_2018_02_22/mobilenet_v1_1.0_224.tgz)and you can find the model documentation [here](https://github.com/opencv/open_model_zoo/tree/master/models/public/mobilenet-v1-1.0-224). For AWS run as below:

Give docker command sudo powers

```
[ec2-user]$ sudo usermod -a -G docker ec2-user
[ec2-user]$ exit
```

Launch workbench docker

```
docker run -p 5665:5665 \
                 -e PROXY_HOST_ADDRESS=0.0.0.0 \
                 -e PORT=5665 \
                 -it openvino/workbench:latest
```

# How Quantization is Done {#how-quantization-is-done}

Let's get into some concrete examples of quantization, so that you can get an idea of how it is done. Remember, quantization simply refers to a mapping that reduces a larger number of values to a smaller number of values—so it can potentially be done in many different ways.

That said, the simplest form of quantization is**weight quantization**, in which we reduce the amount of space required for the weight values—such as by reducing our weight values from 32 bits to 8 bits.

In the video, we will see one way in which this can be done. We will be quantizing some value to an unsigned INT8 \(or uint8\) range. The range of values in uint8 is from 0 to 2^8-1, which is 255.

![](/assets/Screenshot 2020-03-24 at 9.13.52 AM.png)

To summarize, to map the weight values, we need to know:

* The range of the current set of values
* The range of the values we are mapping to
* The precision of the output values

The quantization method discussed in the video is one of the simplest methods to quantize a neural network, but, as we saw, it has some limitations. Since then, many other quantization techniques have been proposed. If you're interested in learning more, we recommend checking out the paper,[A Survey on Methods and Theories of Quantized Neural Networks](https://arxiv.org/pdf/1808.04752.pdf)by Yunhui Guo, in which he goes over some of these techniques.

OpenVINO uses MKL-DNN, a math kernel library, to quantize their neural networks. You can find information about their quantization workflow[here](https://intel.github.io/mkl-dnn/ex_int8_simplenet.html).

# Model Compression {#model-compression}

One important—but often forgotten—metric that we should optimize is memory. We can do this using_model compression_.

> **Model compression**refers to a group of algorithms that help us reduce the amount of memory needed to store our model, and also make our models more compact \(in terms of the number of parameters\).

In fact, you have already learned about a model-compression algorithm, quantization, where we reduce the number of bits required to represent each weight.

## Weight Sharing {#weight-sharing}

Another way to compress our model is to reduce the number of weights that we store. This is known as_weight sharing_.

> In**weight sharing**, the goal is for multiple weights to share the same value. This reduces the number of unique weights that need to be stored, thus saving memory and reducing model size.

Here are the articles we referenced in the video, in case you want to check them out:

* [Deep Compression: Compressing Deep Neural Networks with Pruning, Trained Quantization and Huffman Coding \(Han et al., 2016\)](https://video.udacity-data.com/topher/2020/March/5e6e9c50_deep-compression-compressing-deep-neural-networks-with-pruning-trained-quantization-and-huffman-coding/deep-compression-compressing-deep-neural-networks-with-pruning-trained-quantization-and-huffman-coding.pdf)
* [Compressing Neural Networks with the Hashing Trick \(Chen et al, 2015\)](https://video.udacity-data.com/topher/2020/March/5e6e9c9f_compressing-neural-networks-with-the-hashing-trick/compressing-neural-networks-with-the-hashing-trick.pdf)

# Knowledge Distillation {#knowledge-distillation}

_Knowledge distillation_is a relatively newer technique to perform model compression.

> **Knowledge distillation**is a method where we try to transfer the knowledge learned by a large, accurate model \(the_teacher_model\) to a smaller and computationally less expensive model \(the_student_model\).

Through knowledge distillation, the student model can achieve nearly the same accuracies as the teacher model by mimicking the internal representation learned by the teacher.

* Knowledge Distillation is simple, but recent works have shown that it can be a very powerful method of learning. In a recent paper, researchers showed that by making some small changes to the knowledge distillation algorithm, they could improve the Top-1% Accuracy on ImageNet by 2% over the state of the art while using a model with 349M fewer parameters! If you're curious, you can check out the full paper here:

  * [Self-training with Noisy Student improves ImageNet classification \(Xie et al., 2020\)](https://video.udacity-data.com/topher/2020/March/5e6ea044_self-training-with-noisy-student-improves-imagenet-classification/self-training-with-noisy-student-improves-imagenet-classification.pdf)

  Note that the aim of the authors was actually_not_to compress a model, but to improve accuracy. The reduction in parameters came from using the_EfficientNet_architecture.



