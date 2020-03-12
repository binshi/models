### **Model Optimizer supported frameworks**

The supported frameworks with the OpenVINO™ Toolkit are:

* [Caffe](https://caffe.berkeleyvision.org/)
* [TensorFlow](https://www.tensorflow.org/)
* [MXNet](https://mxnet.apache.org/)
* [ONNX](https://onnx.ai/) \(which can support PyTorch and Apple ML models through another conversion step
* [Kaldi](https://kaldi-asr.org/doc/dnn.html)

These are all open source, just like the OpenVINO™ Toolkit. Caffe is originally from UC Berkeley, TensorFlow is from Google Brain, MXNet is from Apache Software, ONNX is combined effort of Facebook and Microsoft, and Kaldi was originally an individual’s effort. Most of these are fairly multi-purpose frameworks, while Kaldi is primarily focused on speech recognition data.

There are some differences in how exactly to handle these, although most differences are handled under the hood of the OpenVINO™ Toolkit. For example, TensorFlow has some different steps for certain models, or frozen vs. unfrozen models. However, most of the functionality is shared across all of the supported frameworks.

### Intermediate Representations

Intermediate Representations \(IRs\) are the OpenVINO™ Toolkit’s standard structure and naming for neural network architectures. A`Conv2D`layer in TensorFlow,`Convolution`layer in Caffe, or`Conv`layer in ONNX are all converted into a`Convolution`layer in an IR. The Model Optimizer works almost like a translator here, making the Intermediate Representation a shared dialect of all the supported frameworks, which can be understood by the Inference Engine.

The IR is able to be loaded directly into the Inference Engine, and is actually made of two output files from the Model Optimizer: an XML file and a binary file. The XML file holds the model architecture and other important metadata, while the binary file holds weights and biases in a binary format. You need both of these files in order to run inference Any desired optimizations will have occurred while this is generated by the Model Optimizer, such as changes to precision. You can generate certain precisions with the`--data_type`argument, which is usually FP32 by default.

### Using the Model Optimizer with TensorFlow Models

Once the Model Optimizer is configured, the next thing to do with a TensorFlow model is to determine whether to use a frozen or unfrozen model. You can either freeze your model, which I would suggest, or use the separate instructions in the documentation to convert a non-frozen model. Some models in TensorFlow may already be frozen for you, so you can skip this step.

From there, you can feed the model into the Model Optimizer, and get your Intermediate Representation. However, there may be a few items specific to TensorFlow for that stage, which you’ll need to feed into the Model Optimizer before it can create an IR for use with the Inference Engine.

TensorFlow models can vary for what additional steps are needed by model type, being unfrozen or frozen, or being from the TensorFlow Detection Model Zoo. Unfrozen models usually need the`--mean_values`and`--scale`parameters fed to the Model Optimizer, while the frozen models from the Object Detection Model Zoo don’t need those parameters. However, the frozen models will need TensorFlow-specific parameters like`--tensorflow_use_custom_operations_config`and`--tensorflow_object_detection_api_pipeline_config`. Also,`--reverse_input_channels`is usually needed, as TF model zoo models are trained on RGB images, while OpenCV usually loads as BGR. Certain models, like YOLO, DeepSpeech, and more, have their own separate pages.

### TensorFlow Object Detection Model Zoo {#tensorflow-object-detection-model-zoo}

The models in the TensorFlow Object Detection Model Zoo can be used to even further extend the pre-trained models available to you. These are in TensorFlow format, so they will need to be fed to the Model Optimizer to get an IR. The models are just focused on object detection with bounding boxes, but there are plenty of different model architectures available.

### Further Research {#further-research}

* The developer documentation for Converting TensorFlow Models can be found [here](https://docs.openvinotoolkit.org/2019_R3/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_TensorFlow.html)
* TensorFlow also has additional models available in the [TensorFlow Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)
  . By converting these over to Intermediate Representations, you can expand even further on the pre-trained models available to you.

### Using the Model Optimizer with Caffe Models

The process for converting a Caffe model is fairly similar to the TensorFlow one, although there’s nothing about freezing the model this time around, since that’s a TensorFlow concept. Caffe does have some differences in the set of supported model architectures. Additionally, Caffe models need to feed both the`.caffemodel`file, as well as a`.prototxt`file, into the Model Optimizer. If they have the same name, only the model needs to be directly input as an argument, while if the`.prototxt`file has a different name than the model, it should be fed in with`--input_proto`as well.

### Further Research {#further-research}

The developer documentation for Converting Caffe Models can be found[here](https://docs.openvinotoolkit.org/2019_R3/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_Caffe.html). You’ll work through this process in the next exercise.

### Using the Model Optimizer with ONNX Models

The process for converting an ONNX model is again quite similar to the previous two, although ONNX does not have any ONNX-specific arguments to the Model Optimizer. So, you’ll only have the general arguments for items like changing the precision.

Additionally, if you are working with PyTorch or Apple ML models, they need to be converted to ONNX format first, which is done outside of the OpenVINO™ Toolkit. See the link further down on this page if you are interested in doing so.

### Further Research {#further-research}

* The developer documentation for Converting ONNX Models can be found
  [here](https://docs.openvinotoolkit.org/2019_R3/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_ONNX.html)
  . You’ll work through this process in the next exercise.
* ONNX also has additional models available in the
  [ONNX Model Zoo](https://github.com/onnx/models)
  . By converting these over to Intermediate Representations, you can expand even further on the pre-trained models available to you.

### PyTorch to ONNX {#pytorch-to-onnx}

If you are interested in converting a PyTorch model using ONNX for use with the OpenVINO™ Toolkit, check out this[link](https://michhar.github.io/convert-pytorch-onnx/)for the steps to do so. From there, you can follow the steps for ONNX models to get an Intermediate Representation.


