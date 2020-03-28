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



