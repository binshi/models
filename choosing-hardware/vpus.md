## VPU

* The Architecture of VPUs

* The characteristics of the Myriad-X processor \(which is a type of VPU\)
* The characteristics of the Neural Compute Stick 2 \(which uses the Myriad-X Processor\)
* How to access the NCS2 on the DevCloud
* How to run the same model on multiple devices at once using the Mult Device Plugin
* How to use the Multi Device Plugin on the DevCloud



The Neural Compute Stick is an accelerator and cannot run on it's own. It needs a CPU to coordicate the flow of data to and from the NCS. The CPU need not be a powerful one, since it will not actually be doing any calculations. So we can use a simple Atom Processor or even a Raspberry Pi.

![](/assets/Screenshot 2020-03-28 at 5.03.17 PM.png)

