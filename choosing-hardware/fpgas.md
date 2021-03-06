### Introduction to FPGAs {#in-this-concept-we-will-look-into-the-introduction-to-fpgas}

As the name suggests, FPGAs are known for two crucial aspects. Firstly for being **field-programmable **which indicates that it is a hardware that can be configured for specific purposes. Secondly, **Gate Array**, which points to the main building blocks of this hardware, which is the Logic Gates.

Let us take an example of a pharmaceutical company. This company has a manufacturing factory in Ireland. During manufacturing drugs, an important aspect is to analyse the package when it ships off to its customers. To do so, they have a **strict time period of 30 ms **for each package. Currently, the company uses an Intel NCS2 to do image processing and identification. However, the entire process takes about 45ms.

### Reducing the image processing latency {#reducing-the-image-processing-latency}

An easy way to reduce the latency is to add another NCS2, and have the two devices process alternate frames. But for this exercise we are going to suggest using an FPGA. Arria-10 FPGA cards are a good fit for a factory, as they

* Rated for continuous operation, as most production facilities run longer than typical office hours.
* Operating ambient temperature, they have a zero to 65 degrees
* You would need hardware which unlike your current microprocessor systems does not require you to buy any new processors or parts.

![](/assets/Screenshot 2020-03-29 at 8.13.54 AM.png)Let us look into technical terminologies that correspond to the architecture we saw before.

1. **Adaptive Logic Modules**: These are tiles which is a small subset of the total number of components within a modern FPGA. This tile consists of three major blocks; Configurable Logic Blocks and Switch Blocks and I/O Programmable Blocks,

2. **Configurable Logic Blocks**: The configurable Logic blocks form the core of the FPGA. Although each of the CLB blocks is parallel to each other they meet in an external circuit Each block can implement its own function using lookup tables. These functions can include Boolean Operations like AND, OR and NOT or any other function. The logic blocks also contain flip flops, transistor pairs and multiplexers. In this tile, we have four CLB’s. The input and outputs of these CLB’S are steered by the Connection block CB and Switch Block SB.

3. **Programmable Interconnects**: CB Connection block and SB Switch Block together make up the \(Programmable Interconnects\) To administer the resource available in the given CLBs, four Connection Blocks are available per Logic Block. And each Connection Block is also connected to two switch blocks, allowing for each Logic Block to connect north, south-east or west,

4. **Programmable I/O Blocks**: The programmable I/O Blocks help connect the Interconnects and Logic Blocks to an external circuit.These external circuits, ie external to the tile, but still internal to the FPGA, can be more tiles, or DSP’s, or Memory blocks, or even more IO, for example, a PCIe interface, or SATA or other high-speed serial transceivers.

# FPGA Specifications {#fpga-specifications}

**High Performance and Low Latency**

1. **High Performance and Low Latency**: The high performance comes from the ability of the FPGA to perform many tasks at the same time. Another important specification of an FPGA is that it is a high-performance device with very little latency when it comes to executing neural networks.
2. **Flexibility**: This ability to be reprogrammed and to be able to adapt to new, evolving and custom networks is what gives the FPGA an edge over other devices. The DLA suite consists of various implementations of deep learning primitives organized in architectures of FPGA images that are tailored for different types of deep learning topologies.
3. **Ease of Development**: Intel FPGA DLA DEEP LEARNING ACCELERATION Suite allows users to take advantages of OpenVINO application portability without going through the lengthy traditional FPGA development process. This makes it easy for software programmers to hit the ground running without being bogged down by difficult implementation details. The DLA architectures implement optimized comm
4. **Support for large image size and Networks**: FPGAs can support large image sizes as input and perform inference on really large models, with up to 4 billion parameters.
5. **24/7.365 Operation**: FPGAs are devices and are specified for 100% on-time, often referred to 7 by 24 by 365 days, that is a year
6. **Long Lifespan \(8-10 years\)**: FPGAs cards that use devices from Intel’s Internet of Things have guaranteed availability of 10 years, from the start of production.

In this section, we will look into some advantages and disadvantages of FPGA over ASICs

* **Cost-Effective**: ASICs in general, are built for a specific purpose and cannot be moulded for different applications. So, keeping that in mind, an ASIC should cost less than an equivalent FPGA. But what if you need to reprogram your current hardware for a separate purpose. Would you choose new hardware? This new hardware would be accompanied by its own extra expenses. These expenses are known as Recurring Expense. But if you use an FPGA instead, the cost is NRE or Non-Recurring in nature. It is for this reason that FPGA costs are lesser than an ASIC in the longer run.
* **Risk**: During the production of new systems there is always the risk of failure with special-purpose hardware. FPGAs reduce risk, allowing prototype systems to ship to customers for field trials, while still providing the ability to make changes quickly before ramping to volume production
* **Quick to Market**: Most of the FPGA design demands user flexibility and changes, thus making the shipping quicker. The Manufacturers can ship the FPGA board as soon as they tested it. For ASIC chips the manufacturing might take months.
* **Accelerate performance**: FPGAs are excellent in off-loading tasks from a high-performance computing device like the CPU. Thus, effectively speed up the performance of the entire system.
* **Parallel Operations**: Due to individual blocks of CLBs present in the FPGA, it provides parallel operations to be performed in the hardware thereby providing greater speed and performance

However, FPGAs come with their own set of disadvantages too.

* **Single-Purpose Applications**: If your user-applications need to be built for a single and definitive purpose, an FPGA can be more costly and slow, i.e in comparison to their ASIC counterparts.
* **Power- Hungry**: Oftentimes, the power optimisation cannot be controlled by the designer of the FPGA board, thus making it more power-hungry. Thus an FPGA consumes more power than ASICs
* **Design of FPGA circuit**: Selecting the right FPGA circuit is important. If you do not choose the right number of ICs, you will have to use the same number of limited ICs for all applications. To counter these issues, we can use better design methodologies in building an FPGA for products. This process is known as a reference design, which is a layout of the product itself.

Now that we have seen the specifications, let us try and the factors that make FPGA ideal for deep learning applications

1. **Highly Parallel Architecture**: As we have seen before, the highly parallel architecture like the individual block of CLBs help to provide a programmable data path
2. **No fixed architecture**: Due to the presence of no rigid architecture, it can help to accommodate changes to your current neural network while providing greater performance
3. **Programmable Data Path**: With flexibility, also comes the use of programmable data path. This can help prevent unnecessary data movement. This results in latency reduction, and improved efficiency.
4. **Latency Reduction**: Latency Reduction can also be caused due to Tightly Coupled High-bandwidth Memory.

## Heterogeneous Plugin {#heterogeneous-plugin}

The primary reason to choose the Hetero plugin is to set a secondary device as a fallback option in case the FPGA device does not support certain layers in your model. For instance, in an FPGA based edge computing system, the bitstream files that we load on to the FPGA might not support a few layers in your model. In these cases, the unsupported layers are executed on the host device, like a CPU.

The table shows the list of supported layers for each device. You can see below that an inverse cosine layer is not supported by the FPGA, but the activation clamp layer is. With the use of HETERO PLUGIN, you can ensure that a model with unsupported layers can be run, primarily, on the FPGA.

**Note**:_For more information on the supported layers, check out the docs_[_here_](https://docs.openvinotoolkit.org/latest/_docs_IE_DG_supported_plugins_Supported_Devices.html)

| Layers | GPU | CPU | VPU | FPGA |
| :--- | :--- | :--- | :--- | :--- |
| Abs | Supported | Supported | Not Supported | Not Supported |
| Acos | Supported | Supported | Not Supported | **Not Supported** |
| Acosh | Supported | Supported | Not Supported | Not Supported |
| Activation Clamp | Supported | Supported | Supported | **Supported** |

## HETERO PLUGIN Advantages and Disadvantages {#hetero-plugin-advantages-and-disadvantages}

Here are the**advantages**of using a_HETERO PLUGIN_,

1. Set A Secondary device as a Fallback device
2. The ability to utilise all the available hardware efficiently to perform inference

However, the**disadvantages**include,

1. Transferring data and network takes time
2. Greedy Behaviour



