## VPU

* The Architecture of VPUs

* The characteristics of the Myriad-X processor \(which is a type of VPU\)

* The characteristics of the Neural Compute Stick 2 \(which uses the Myriad-X Processor\)

* How to access the NCS2 on the DevCloud

* How to run the same model on multiple devices at once using the Mult Device Plugin

* How to use the Multi Device Plugin on the DevCloud

The Neural Compute Stick is an accelerator and cannot run on it's own. It needs a CPU to coordicate the flow of data to and from the NCS. The CPU need not be a powerful one, since it will not actually be doing any calculations. So we can use a simple Atom Processor or even a Raspberry Pi.

![](/assets/Screenshot 2020-03-28 at 5.03.17 PM.png)![](/assets/Screenshot 2020-03-28 at 5.05.44 PM.png)A Vision Processing Unit is a coprocessor built for image and video processing applications. They help to offload tasks for inference from a computational intensive load. A typical VPU consists of the following parts:

1. **Vector Processors :**
   A typical VPU consist of an array of vector processors. Vector processors as the name suggests are processors that work on a vector or an array of 1D data. They are in contrast to scalar processors which often work on single data items. In general with single data items, instructions are executed in a sequential manner. This would increase the time for execution. Instead, the processors now pipeline the instructions. In order to do that, they break up a complex instruction and then execute a lot of instructions in a parallel manner.
2. **Interface Unit:**
   A interface Unit is a part of the VPU that interacts with the Host device. This device could be a CPU or any other processing device. We would train our machine learning models on the Host Device and then run the inference on the VPU.
3. **Hardware Accelerators:**
   The Hardware Accelerator has specific kernels which are used for image processing operations. These operations can include simple techniques of denoising to even algorithms for edge detection in images. 

![](/assets/Screenshot 2020-03-28 at 5.12.41 PM.png)The Characteristics of a **Myriad X** Processor Includes

* **Vector Processors**: The number of SHAVE processor in a Myriad X increases to 16. Thus providing a greater increase in floating-point operations.
* **Chip Size**: One would assume that with the increase in processors would result in greater chip size. But this Myriad chip comes with smaller transistors of 16 nm as opposed to the 28 nm transistors present in the Myriad 2 chip.
* **Hardware Accelerators**: There different hardware accelerators available on the Myriad X chip processor. These include kernels for depth estimation, optical flow and motion estimation
* **Dedicated Neural Compute Engine**: Contrary to the development of the previous Myriad 2 processor, deep learning frameworks have become common and easy to use. Thus the Myriad X processor has a dedicated on-chip accelerator for neural networks. This delivers up to 1 TFLOPS of operations
* **Frameworks Supported**: Myriad 2 processors The chip supports only CAFE framework whereas the Myriad X chip supports Tensorflow
* **Energy Consumption**: With all these features, this chip has only a moderate increase in clock speed with little increase in overall power consumption

Now that we have an overview of how a typical VPU architecture looks like, let us look into the characteristics of an actual VPU chip, **Myriad 2**.

The Myriad 2 MA2x5x family is a 28 nm processor which offers computer vision applications in low power devices. It is the chip used in the Neural Compute Deep Learning stick.

1. Vector Processors: The vector Processors present on the Myriad chip are known as SHAVE processors. SHAVE stands for Streaming Hybrid Architecture Vector Engines. There are 12 SHAVE processors present on the chip which perform highly parallel operations. The SHAVE processor is a type of VLIW Vector Processor. This enables it to support different integer and floating-point operations. Currently, the Myriad 2 Processor supports the 16/32-bit floating point and 8/16/32-bit integer operations.
2. SIPP\(Streaming Image Processing Pipeline\): The hardware accelerator kernels on the Myriad 2 Processor support two different kinds of accelerators namely the image and signal processing kernels. The various operations supported by these kernels include
   * Harris
   * Median filter,
   * Edge filter
   * 2X scaler
3. CPU and Interface Unit: Similar to the VPU architecture, the Myriad 2 processor chip has an Interface Unit and two RISC processors present on board

The Characteristics of a Myriad X Processor Includes

* **Vector Processors**: The number of SHAVE processor in a Myriad X increases to 16. Thus providing a greater increase in floating-point operations.
* **Chip Size**: One would assume that with the increase in processors would result in greater chip size. But this Myriad chip comes with smaller transistors of 16 nm as opposed to the 28 nm transistors present in the Myriad 2 chip.
* **Hardware Accelerators**: There different hardware accelerators available on the Myriad X chip processor. These include kernels for depth estimation, optical flow and motion estimation
* **Dedicated Neural Compute Engine**: Contrary to the development of the previous Myriad 2 processor, deep learning frameworks have become common and easy to use. Thus the Myriad X processor has a dedicated on-chip accelerator for neural networks. This delivers up to 1 TFLOPS of operations
* **Frameworks Supported**: Myriad 2 processors The chip supports only CAFE framework whereas the Myriad X chip supports Tensorflow
* **Energy Consumption**: With all these features, this chip has only a moderate increase in clock speed with little increase in overall power consumption

| Type | Myriad 2 Processor | Myriad X Processor |
| :--- | :--- | :--- |
| Vector Processors | 12 | 16 |
| Size of Transistors | 28 nm | 16nm |
| Hardware Accelerator Kernel | Median Filter, Edge Detection and Harris filter | Depth stereo estimation. Optical flow |
| Size of the Package | 5mm x 5mm, 6.5mm x 6.5 mm, 8mm x 9.5 mm | 8.1mm x 8.8mm |
| Operating Frequency |  |  |
| Hardware Used In | Intel NCS Stick | Intel NCS Stick2 |

# Intel Neural Compute Stick {#intel-neural-compute-stick}

The Intel Neural Compute Stick 2 or the Intel NCS2 is a plug and play development kit for AI Inferencing. The following are the product features of the Intel NCS2 stick.

* **VPU**: The VPU supported by Intel NCS2 stick is Myriad X Processor, that we learnt about in the concept before.It provides SoC implementation of the Myriad X Processor
* **Software development kit**: With the integration of OpenVino Toolkit the Intel NCS2 offers pre-trained models to be run on the stick. This allows ease in the use of the hardware
* **Operating System**: Currently the Intel NCS2 stick supports the Ubuntu _16.04.3 LTS \(64 bit\), Windows® 10 \(64 bit\), or CentOS_
  7.4 \(64 bit\).

All of these features come in a small size of 72.5mm X 27mm X 14mm with the looks of standard thumb drive making it ideal for an easy plug-in into CPU, Raspberry Pi or any computing device with a USB port

# Multi-Device Plugins {#multi-device-plugins}

## Myriad Form Factors {#myriad-form-factors}

The Myriad X chip is present of various form factors

1. Single-Chip Mini-PCIe
2. Dual chip M 2.280
3. Four-way PCI express card
4. Eight-way PCI express card

These often to the system as different USB sticks plugged in and users can use applications that use them via OpenVino.

One of these features is the **Multi-Device Plugin**

## Multi-Device Plugin {#multi-device-plugin}

![](/assets/Screenshot 2020-03-28 at 6.31.54 PM.png)

Multi-Device plugin automatically assigns inference requests to available computational devices to execute the requests in parallel. There are several reasons to choose a Multi-Device Plugin

### Reasons to choose a Multi-Device Plugin: {#reasons-to-choose-a-multi-device-plugin-}

* **Distribute inference requests across multiple devices**: Having multiple NCS's will help distribute the load across all the devices. OpenVINO handles the distribution of the load internally and prevents any one of the device from becoming too busy.

* **Increase the throughput of your entire system**: The volume of data that can be processed in a given time is known as the throughput of the system. While latency can be reduced by using faster hardware, an easy way to increase throughput is to have multiple devices share the load of the incoming data. In OpenVINO, this can be implemented by using the Multi plugin. Single devices are good for decreasing the latency but they cannot handle the inference of a large volume of data at a time. When using a single device, you are limited by the amount of load that that device can handle. This is where using multiple devices can help.

### Reasons for not choosing Multi-Device Plugin {#reasons-for-not-choosing-multi-device-plugin}

* **Devices are kept busy all the time**: One factor that you need to keep in mind when using a multi-device plugin is to keep all the devices busy most of the time. If your devices are left idle or enough data is not sent to the devices for inference, then you will not see any significant improvements in throughput.

* **Minimal Increase in Performance in a few Cases**: Multi-Device Plugins might not always improve the performance of your system, especially if the devices do not get enough inference requests to execute.

# VPU Specifications {#vpu-specifications}

VPU's have many advantages like better thermal characteristics and less power usage. In this page, you will learn about the various specifications of the VPU that make them ideal for using in an edge device.

**Heat Generation**: With larger models, the number of layers increases in a neural network. Each layer of the neural network needs to perform a particular MAC operation which needs to access the CPU logic blocks. Thus with more complex layers, different blocks need to be accessed, causing improper use of CPU, which leads to more heat generation inside the CPU. Therefore, by introducing an accelerator for the CPU for a specific purpose, it helps to decrease the thermal dissipation inside the HPC.

**Power Consumption: **With the increase in layers, the power consumption for larger models also increases. Power consumption is one of the main bottlenecks in larger scale processors. For example, the TDP of a CPU ranges from 40-100 watts. Whereas in a Myriad processor can reduce up to 8 times in comparison.

**Cost**: The cost is dependent on the operating frequency. The operating frequency for a VPU is 600 Mhz. A VPU costs around 100$ for each device. Quadratic in power to linear increase in operating frequerncy

**Throughput:**The Throughput is calculated as follows:

```
Throughput = Images per Second/ TDP
```

The combination of higher image per second to the lower power consumed gives a higher throughput.![](/assets/Screenshot 2020-03-28 at 6.51.42 PM.png)![](/assets/Screenshot 2020-03-28 at 6.54.55 PM.png)

