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

video content

| Type | Myriad 2 Processor | Myriad X Processor |
| :--- | :--- | :--- |
| Vector Processors | 12 | 16 |
| Size of Transistors | 28 nm | 16nm |
| Hardware Accelerator Kernel | Median Filter, Edge Detection and Harris filter | Depth stereo estimation. Optical flow |
| Size of the Package | 5mm x 5mm, 6.5mm x 6.5 mm, 8mm x 9.5 mm | 8.1mm x 8.8mm |
| Operating Frequency |  |  |
| Hardware Used In | Intel NCS Stick | Intel NCS Stick2 |



