# ML and OpenCV

#### Edge Application {#edge-application}

Applications with inference run on local hardware, sometimes without network connections, such as Internet of Things \(IoT\) devices, as opposed to the cloud. Less data needs to be streamed over a network connection, and real-time decisions can be made.

#### OpenVINO™ Toolkit {#openvino-toolkit}

The[Intel® Distribution of OpenVINO™ Toolkit](https://software.intel.com/en-us/openvino-toolkit)enables deep learning inference at the edge by including both neural network optimizations for inference as well as hardware-based optimizations for Intel® hardware.

#### Pre-Trained Model {#pre-trained-model}

Computer Vision and/or AI models that are already trained on large datasets and available for use in your own applications. These models are often trained on datasets like[ImageNet](https://en.wikipedia.org/wiki/ImageNet). Pre-trained models can either be used as is or used in transfer learning to further fine-tune a model. The OpenVINO™ Toolkit provides a number of[pre-trained models](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models)that are already optimized for inference.

#### Transfer Learning {#transfer-learning}

The use of a pre-trained model as a basis for further training of a neural network. Using a pre-trained model can help speed up training as the early layers of the network have feature extractors that work in a wide variety of applications, and often only late layers will need further fine-tuning for your own dataset. OpenVINO™ does not deal with transfer learning, as all training should occur prior to using the Model Optimizer.

#### Image Classification {#image-classification}

A form of inference in which an object in an image is determined to be of a particular class, such as a cat vs. a dog.

#### Object Detection {#object-detection}

A form of inference in which objects within an image are detected, and a bounding box is output based on where in the image the object was detected. Usually, this is combined with some form of classification to also output which class the detected object belongs to.

#### Semantic Segmentation {#semantic-segmentation}

A form of inference in which objects within an image are detected and classified on a pixel-by-pixel basis, with all objects of a given class given the same label.

#### Instance Segmentation {#instance-segmentation}

Similar to semantic segmentation, this form of inference is done on a pixel-by-pixel basis, but different objects of the same class are separately identified.

#### [SSD](https://arxiv.org/abs/1512.02325) {#ssd}

A neural network combining object detection and classification, with different feature extraction layers directly feeding to the detection layer, using default bounding box sizes and shapes/

#### [YOLO](https://arxiv.org/abs/1506.02640) {#yolo}

One of the original neural networks to only take a single look at an input image, whereas earlier networks ran a classifier multiple times across a single image at different locations and scales.

#### [Faster R-CNN](https://arxiv.org/abs/1506.01497) {#faster-r-cnn}

A network, expanding on[R-CNN](https://arxiv.org/pdf/1311.2524.pdf)and[Fast R-CNN](https://arxiv.org/pdf/1504.08083.pdf), that integrates advances made in the earlier models by adding a Region Proposal Network on top of the Fast R-CNN model for an integrated object detection model.

#### [MobileNet](https://arxiv.org/abs/1704.04861) {#mobilenet}

A neural network architecture optimized for speed and size with minimal loss of inference accuracy through the use of techniques like[1x1 convolutions](https://stats.stackexchange.com/questions/194142/what-does-1x1-convolution-mean-in-a-neural-network). As such, MobileNet is more useful in mobile applications that substantially larger and slower networks.

#### [ResNet](https://arxiv.org/abs/1512.03385) {#resnet}

A very deep neural network that made use of residual, or “skip” layers that pass information forward by a couple of layers. This helped deal with the[vanishing gradient problem](https://towardsdatascience.com/the-vanishing-gradient-problem-69bf08b15484)experienced by deeper neural networks.

#### [Inception](https://arxiv.org/pdf/1409.4842.pdf) {#inception}

A neural network making use of multiple different convolutions at each “layer” of the network, such as 1x1, 3x3 and 5x5 convolutions. The top architecture from the original paper is also known as GoogLeNet, an homage to[LeNet](http://yann.lecun.com/exdb/publis/pdf/lecun-01a.pdf), an early neural network used for character recognition.

#### Inference Precision {#inference-precision}

Precision refers to the level of detail to weights and biases in a neural network, whether in floating point precision or integer precision. Lower precision leads to lower accuracy, but with a positive trade-off for network speed and size.

### Quantization {#quantization}

Quantization is related to the topic of precision I mentioned before, or how many bits are used to represent the weights and biases of the model. During training, having these very accurate numbers can be helpful, but it’s often the case in inference that the precision can be reduced without substantial loss of accuracy. Quantization is the process of reducing the precision of a model.

With the OpenVINO™ Toolkit, models usually default to FP32, or 32-bit floating point values, while FP16 and INT8, for 16-bit floating point and 8-bit integer values, are also available \(INT8 is only currently available in the Pre-Trained Models; the Model Optimizer does not currently support that level of precision\). FP16 and INT8 will lose some accuracy, but the model will be smaller in memory and compute times faster. Therefore, quantization is a common method used for running models at the edge.

[https://nervanasystems.github.io/distiller/quantization.html](https://nervanasystems.github.io/distiller/quantization.html)

### Freezing {#freezing}

Freezing in this context is used for TensorFlow models. Freezing TensorFlow models will remove certain operations and metadata only needed for training, such as those related to backpropagation. Freezing a TensorFlow model is usually a good idea whether before performing direct inference or converting with the Model Optimizer.

### Fusion {#fusion}

Fusion relates to combining multiple layer operations into a single operation. For example, a batch normalization layer, activation layer, and convolutional layer could be combined into a single operation. This can be particularly useful for GPU inference, where the separate operations may occur on separate GPU kernels, while a fused operation occurs on one kernel, thereby incurring less overhead in switching from one kernel to the next.

### OpenCV

OpenCV is an open-source library for various image processing and computer vision techniques that runs on a highly optimized C++ back-end, although it is available for use with Python and Java as well. It’s often helpful as part of your overall edge applications, whether using it’s built-in computer vision techniques or handling image processing.

### Uses of OpenCV {#uses-of-opencv}

There’s a lot of uses of OpenCV. In your case, you’ll largely focus on its ability to capture and read frames from video streams, as well as different pre-processing techniques, such as resizing an image to the expected input size of your model. It also has other pre-processing techniques like converting from one color space to another, which may help in extracting certain features from a frame. There are also plenty of computer vision techniques included, such as Canny Edge detection, which helps to extract edges from an image, and it extends even to a suite of different machine learning classifiers for tasks like face detection.

### Useful OpenCV function {#useful-opencv-function}

* `VideoCapture`
  - can read in a video or image and extract a frame from it for processing
* `resize`
  is used to resize a given frame
* `cvtColor`
  can convert between color spaces.
  * You may remember from awhile back that TensorFlow models are usually trained with RGB images, while OpenCV is going to load frames as BGR. There was a technique with the Model Optimizer that would build the TensorFlow model to appropriately handle BGR. If you did not add that additional argument at the time, you could use this function to convert each image to RGB, but that’s going to add a little extra processing time.
* `rectangle`
  - useful for drawing bounding boxes onto an output image
* `imwrite`
  - useful for saving down a given image

See the link further down below for more tutorials on OpenCV if you want to dive deeper.

### Further Research {#further-research}

OpenCV has some[pretty extensive tutorials](https://docs.opencv.org/master/d9/df8/tutorial_root.html)available if you want to dive deeper into this useful computer vision library. We'll look at some of the relevant material on handling camera and video inputs next.



