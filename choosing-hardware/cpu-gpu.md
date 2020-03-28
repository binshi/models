# CPUs and Integrated GPUs {#cpu-basics}

# CPU Basics {#cpu-basics}

Over the next few pages, we'll look at some of the main types of Intel CPUs and how they differ in performance. To understand the differences between the processors, it's important to first have a solid grasp of some fundamental terms and concepts that we'll go over on this page.

> A**CPU**or**Central Processing Unit**is the electronic circuitry that executes the instructions of a computer program.

Here's a diagram of an Intel CPU:

![](/assets/Screenshot 2020-03-28 at 8.16.08 AM.png)Multiple Cores—and a GPU

If you look closely at the above image, you may notice something a little confusing: We referred to this picture as the "CPU", but did you notice that there are four smaller squares inside of it that are also labeled "CPU"? And another one labeled "GPU"?

This is simply a quirk of terminology. Originally, the physical chip for a processor had only_one\_central processing unit \(CPU\) on it. But now, almost all chips contain multiple CPUs or\_cores_. Confusingly, the whole chip \(with multiple CPUs\) is still frequently referred to as "the CPU".

> A **multicore processor **is a computer chip that has multiple CPUs \(called **cores**\). Confusingly, a multicore processor is often simply called a "CPU", even though it contains multiple CPUs.

And as we mentioned, all Intel processors also contain a **GPU **or **Graphics Processing Unit**. You may be more used to thinking of a GPU as a separate component, such as the "video card" in your PC. In this case, the GPU is located on the same chip and shares the same memory with the CPUs.

> An **integrated GPU **is a GPU that is located on a processor alongside the CPU cores and shares memory with them.

But all of this leads us to a new question: Why do we want to have multiple cores on a single processor? To understand this, we first need to understand _processes and threads_

# Threads and Processes {#threads-and-processes}

Recall our definition of a CPU:

> A **CPU **or **Central Processing Unit **is the electronic circuitry that executes the instructions of a computer program.

Note that when we talk about a computer **program**, the code for this program is simply a set of instructions;_it is not necessarily active_. You could print out a computer program and leave it sitting on your coffee table, never to be actually executed by any computer. Thus, we need a term that we can use to refer to a program that is being actively executed. Most commonly, this is referred to as a_process_.

> A **process **is a copy of a computer program that is being actively executed by the CPU.

Of course, each program or process is made up of many smaller sequences of instructions that need to be carried out. These smaller sequences of execution are called _threads_.

> A **thread **or **thread of execution **is a stream of instructions. A thread is a _subprocess_, in the sense that a single process is typically made up of multiple threads.

# Multithreading and Multiprocessing {#multithreading-and-multiprocessing}

Now we can return to our question from the previous page: Why do we want to have multiple cores on a single processor? The advantage of having multiple cores is that the CPU can execute multiple processes simultaneously. Put another way, having multiple cores enables the CPU to do_multiprocessing_.

> **Multiprocessing**is the act of executing multiple processes simultaneously.

In addition to_multiprocessing_, you may have also heard the term_multithreading_. This is a very similar concept to multiprocessing.

> **Multithreading**is the act of executing multiple threads simultaneously.

## One thing at a time… {#one-thing-at-a-time-}

A key concept you should understand is that each core of a CPU can only really be executing_one set of instructions at a time_. That means it can only be running one process \(or one thread of execution\) at a time.

For example, suppose that you have two processes that you want to run. If you have a CPU with only one core, this CPU would have to switch back and forth between running the two processes—thus leading to a decrease in performance. To the user, it may seem like the processes are running "at the same time", but the reality is that the CPU must split its resources switching from one to the next.

On the other hand, if you have a CPU with two cores, each core can be running its own separate process. Thus, you can genuinely have both processes running at the same time, with no decrease in performance. To distinguish between these scenarios, we use the terms_concurrency\_and\_parallelism_. If two processes are running in**parallel**, this means that they are_truly running at the same time_. In contrast, if two processes are running**concurrently**, this means that the CPU is cycling through them and only giving the\_appearance\_that the processes are running at the same time.

## A Note on Multithreading and True Parallelism {#a-note-on-multithreading-and-true-parallelism}

If you recall from above, we defined multithreading like this:

> **Multithreading**is the act of executing multiple threads simultaneously.

But in reality, when people use the term "multithreading", what they really mean is that the threads are being run_concurrently_—that is, the CPU is actually cycling through the threads and giving the\_appearance\_that they are being run at the same time. Although the threads are not truly running in parallel, this can nevertheless be very useful.

For example, suppose that a particular thread starts running, but then requires some data before it can continue. You don't want your whole application to stall while waiting for this data. By cycling through multiple threads \(i.e.,_multithreading_\), you can keep other parts of the application running. Thus, you can ensure that, for instance, the interface remains responsive to the user, even while one of the application's threads is getting the required data.

Different languages handle multiprocessing and multithreading differently. But often you will see that multiprocessing refers to true_parallelism_, while multithreading refers to_concurrency_.

If you'd like to read more about these distinctions, we recommend the following articles:

* [A gentle introduction to multithreading](https://www.internalpointers.com/post/gentle-introduction-multithreading)
* [Multithreading vs. multiprocessing in Python](https://medium.com/contentsquare-engineering-blog/multithreading-vs-multiprocessing-in-python-ece023ad55a)

# Intel CPU Architecture {#intel-cpu-architecture}

Now let's go over some of the specifications and features of Intel processors, and talk about how these features affect their performance. As you watch this next video, notice that some of the differences in performance revolve around how the CPUs handle processes and threads—for example, through _multiprocessing \_and \_hyperthreading_.

## Compatibility {#compatibility}

Each new generation of Intel processors is a superset of its predecessors, providing backward compatibility with older chips and older software, while also adding new or enhanced features. This compatibility allows engineers, programmers, and development teams to reuse the software and software-development tools from earlier projects, protecting their investment in time and talent.

## Multicore Performance {#multicore-performance}

Most Intel processors now ship with 4 or more cores, which allows better performance and parallelism of tasks. As we discussed earlier in this lesson, having multiple cores allows for_multiprocessing_—the act of executing multiple processes simultaneously. Each core can be running a different process at the same time.

## Hyperthreading {#hyperthreading}

In addition to standard multiprocessing, you should be aware that Intel processors also have an ability to perform something called_hyperthreading_.

> **Hyperthreading**divides each physical core into two_virtual cores_.

For example, a CPU with four physical cores will be recognized \(by the computer's OS\) as having eight virtual cores. The virtual cores allow multiple threads of execution to be run on a single physical core at the same time.

Hyperthreading can lead to a performance increase, although this improvement is not as great as if you used a CPU that had the equivalent number of real, physical cores.

For example, a CPU that has four physical cores and uses hyperthreading would have**eight virtual cores**. If you were to run this system side-by-side with a CPU that has**eight physical cores**, the latter would likely have higher performance. Even though the four-core processor with hyperthreading has eight virtual cores, it is still limited to the resources of four physical cores—whereas the eight-core processor has twice the underlying resources.

> **Note:**It's important to understand that the improvements in performance that come from multiprocessing and hyperthreading don't happen automatically—software developers must specifically write their code to take advantage of these hardware features.

## Instruction Sets and Instruction Set Extensions {#instruction-sets-and-instruction-set-extensions}

Every processor has an\_instruction set\_that provides the set of all instructions supported by that processor.

> An **instruction set **is the set of instructions supported by a given processor.

Put another way, we can say that _every CPU is an implementation of a particular instruction set architecture_. For example, a CPU will need to be able to accept an instruction to add two integers, and this would be specified in the instruction set. An example of a common instruction set is the [x86 instruction set](https://en.wikipedia.org/wiki/X86_instruction_listings#x87_floating-point_instructions), which has been in use since 1978.

In addition to the basic instruction set, new processors can include [instruction set extensions](https://software.intel.com/en-us/isa-extensions) that, as the name implies, extend the set with additional instructions. These extensions can be used to improve the performance of specialized operations. For example, recent additions to the XEON Scalable line of processors include Vector Neural Net Instructions \(VNNIs\) that help speed up common Convolutional Neural Network \(CNN\) operations.

# Specifications of CPUs {#specifications-of-cpus}

Now that you have seen the different CPU architectures, let us try understanding what sort of factors plays a role in choosing the processor for your problem statement?

1. **Clock Speed and the number of Cores**: Each processor chip comes with its own set of cores. It is important to choose the right number of cores for each application. Ideally, you want a processor with a greater number of cores, but at the same time, it should support a higher clock speed. Clock speed or clock rate is the frequency at which your processor can generate pulses. While choosing your processor, the number of cores is given higher preference, and then comes the clock speed.
2. **Cost**: Each application or problem statement will be accompanied by its own set of budgetary constraints. It is important that you choose the best processor given your cost range while not compromising performance.
3. **TDP**: Thermal Design Power is another important consideration. CPU chips with higher TDPs will consume more power and dissipate greater heat. If your application has power constraints, then you need to choose a processor with lower TDPs.

# Integrated Graphics Processing Unit {#integrated-graphics-processing-unit}

In this section, we will learn about the integrated GPU. In this type of computing model, a CPU and GPU are integrated on the same die. This causes both the CPU and GPU to share memory and common address space. We will learn how this shared computing model works and how we can use it to run deep learning models.

The architecture of Integrated GPUs. In short, they are:

1. **Execution Unit**: They are compute processors optimised for multi-threading.
2. **Slice**: Slice is a collection of 24 EUs.
3. **Unslice**: This is the part of the CPU that supports media functions like MFX and VQE

The characteristics of the Integrated GPU are:

1. **Configurable Power Supply**: The slice section in a GPU can run at a different clock rate that the unslice section. This means that unused sections in a GPU can be powered down to reduce power consumption
2. **Model Precision**: GPUs use FP16 model precision. Using half the precision that CPUs run on \(FP32\), GPUs can be faster since twice as many operands can be processed at the same time.
3. **Shared Components**: Since the CPU and Int. GPU is present on the same die, they share the same system memory, higher-level caches and a memory controller. This reduces memory latency by speeding up data transfer between the two devices
4. **Applications of Computer Vision**: One of the broad areas of application in deep learning is Image and Video Processing. The ability to provide a specific chip to perform operations targeted to such use cases helps the system to increase the overall performance

### Advantages of such a model over an external GPU support: {#advantages-of-such-a-model-over-an-external-gpu-support-}

1. **Improvement in Performance**
   : No explicit data transfers are required between the CPU and GPU model.
2. **Simpler Programming**
   : With no separate hardware support for GPU, the programming becomes easier since explicit code management is not required
3. **System Development**
   : Having both computing models on the same die reduces communication costs and increased bandwidth, thus enabling better optimisation. Reduce data transfer
4. **Cost Savings**
   : Due to shared component model, it will help to reduce cost and thereby implementation would be easier. This is one of the vital benefits since the laptops or PCs with discrete graphics card would cost more.
5. **Longer Battery Life**
   : Better system management and the ability to segregate workloads, leads to an increased battery life low power instead

### Now that we have seen the characteristics of an Integrated GPU, let us try and understand why we use these chips for the purposes of deep learning. {#now-that-we-have-seen-the-characteristics-of-an-integrated-gpu-let-us-try-and-understand-why-we-use-these-chips-for-the-purposes-of-deep-learning-}

1. **Applications of Computer Vision**
   : One of the broad areas of application in deep learning is Image and Video Processing. The ability to provide a specific chip to perform operations targeted to such use cases helps the system to increase the overall performance Powerful and flexible
2. **Instruction Set Architecture \(ISA\)**
   : The Instruction Set Architecture or the ISA, of the Processor Graphics SIMD execution units, is well suited to Deep Learning. This ISA offers rich data type support for 32-bit FP, 16-bit FP, 32-bit integer, a 16-bit integer with SIMD multiply-accumulate instructions. The ISA provides efficient memory block loads to quickly load data tiles for optimized convolution or optimized generalized matrix multiply implementations.
3. **Memory Architecture**
   : If you were to use an external graphics memory, for every epoch or iteration of data into your model, you would have to transfer memory from your system to the discrete one. This would increase latency and the power required by the system.



