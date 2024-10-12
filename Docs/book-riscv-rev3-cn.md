

# 页表






# 第五章 中断和设备驱动

> A driver is the code in an operating system that manages a particular device: it configures the device hardware, tells the device to perform operations, handles the resulting interrupts, and interacts with processes that may be waiting for I/O from the device. Driver code can be tricky because a driver executes concurrently with the device that it manages. In addition, the driver must understand the device’s hardware interface, which can be complex and poorly documented.

驱动程序是操作系统中管理特定设备的代码：它配置设备硬件，让设备执行某些操作，处理结果中断，并与可能等待设备 I/O 的进程交互。驱动程序代码可能很复杂，因为驱动程序与其管理的设备并发执行。此外，驱动程序必须理解设备的硬件接口，这可能很复杂且设备的文档不全。

> Devices that need attention from the operating system can usually be configured to generate interrupts, which are one type of trap. The kernel trap handling code recognizes when a device has raised an interrupt and calls the driver’s interrupt handler; in xv6, this dispatch happens in devintr ([kernel/trap.c:178](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/trap.c#L178)).

需要操作系统关注的设备通常可以被配置为中断源，让其产生中断，中断是一种特殊的陷阱 (trap)。当设备产生中断时，内核中处理陷阱的代码识别到中断发生，并调用相应的设备中断处理程序；在 xv6 中，这部分代码在 devintr ([kernel/trap.c:178](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/trap.c#L178)) 中。

> Many device drivers execute code in two contexts: a top half that runs in a process’s kernel thread, and a bottom half that executes at interrupt time. The top half is called via system calls such as read and write that want the device to perform I/O. This code may ask the hardware to start an operation (e.g., ask the disk to read a block); then the code waits for the operation to complete. Eventually the device completes the operation and raises an interrupt. The driver’s interrupt handler, acting as the bottom half, figures out what operation has completed, wakes up a waiting process if appropriate, and tells the hardware to start work on any waiting next operation.

许多设备驱动程序在两种上下文中执行代码：在进程的内核线程中运行的上半部分，下半部分在中断时执行。 上半部分是通过系统调用来调用的，例如希望该设备执行I/O的读写。该代码可能会要求硬件启动操作（例如，要求磁盘读取一个块）；然后代码等待操作完成。 最终，设备完成了操作并产生了中断。 驱动的中断处理程序充当下半部分，确定哪些操作已经完成，唤醒等待的进程如果需要的话，并让硬件开始下一个等待执行的操作。

## 5.1 Code: Console input

> The console driver ([kernel/console.c](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/console.c)) is a simple illustration of driver structure. The console driver accepts characters typed by a human, via the UART serial-port hardware attached to the RISC-V. The console driver accumulates a line of input at a time, processing special input characters such as backspace and control-u. User processes, such as the shell, use the read system call to fetch lines of input from the console. When you type input to xv6 in QEMU, your keystrokes are delivered to xv6 by way of QEMU’s simulated UART hardware.

控制台驱动程序 ([kernel/console.c](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/console.c)) 是驱动程序结构的一个简单示例。控制台驱动程序通过连接到 RISC-V 的 UART 串行端口硬件接受我们输入的字符。控制台驱动程序一次积累一行的输入，处理特殊的输入字符，如退格键和Ctrl-U。用户进程，如 shell，使用 read 系统调用来从控制台获取输入行。当你在 QEMU 中向 xv6 输入时，你的按键通过 QEMU 模拟的 UART 硬件传递给 xv6。

：
：

## 5.4 时钟中断

> Xv6 uses timer interrupts to maintain its clock and to enable it to switch among compute-bound processes; the yield calls in usertrap and kerneltrap cause this switching. Timer interrupts come from clock hardware attached to each RISC-V CPU. Xv6 programs this clock hardware to interrupt each CPU periodically.

Xv6 通过使用定时器中断来维护其时钟系统，并使其能够切换于计算密集型进程之间；在 usertrap 和 kerneltrap 中的 yield 调用导致了这种切换。定时器中断来自于连接到每个 RISC-V CPU 的时钟硬件。Xv6 对这个时钟硬件进行编程，使其定期地对每个 CPU 产生中断。

> RISC-V requires that timer interrupts be taken in machine mode, not supervisor mode. RISC-V machine mode executes without paging, and with a separate set of control registers, so it’s not practical to run ordinary xv6 kernel code in machine mode. As a result, xv6 handles timer interrupts completely separately from the trap mechanism laid out above.

RISC-V 要求定时器中断必须在机器模式下处理，而不是在监督模式下。RISC-V 的机器模式不使用分页，并且具有一组独立的控制寄存器，因此直接在机器模式下运行普通的 Xv6 内核代码是不现实的。因此，Xv6 完全独立于上述描述的陷阱机制来处理定时器中断。

> Code executed in machine mode in start.c, before main, sets up to receive timer interrupts ([kernel/start.c:63](https://github.com/mit-pdos/xv6-riscv/blob/riscv//kernel/start.c#L63)). Part of the job is to program the CLINT hardware (core-local interruptor) to generate an interrupt after a certain delay. Another part is to set up a scratch area, analogous to the trapframe, to help the timer interrupt handler save registers and the address of the CLINT registers. Finally, start sets mtvec to timervec and enables timer interrupts.

start.c 中的代码运行在 M-mode 下，在 main 之前，配置定时器中断([kernel/start.c:63](https://github.com/mit-pdos/xv6-riscv/blob/riscv//kernel/start.c#L63))。其中一项任务是配置 CLINT(core-local interruptor) 硬件，让其在一段时间后产生中断。另一部分是设置一个类似于 trapframe 的暂存区，以帮助定时器中断处理程序保存寄存器和 CLINT 寄存器的地址。最后，start 将 mtvec 设置为 timervec 并启用定时器中断。

> A timer interrupt can occur at any point when user or kernel code is executing; there’s no way for the kernel to disable timer interrupts during critical operations. Thus the timer interrupt handler must do its job in a way guaranteed not to disturb interrupted kernel code. The basic strategy is for the handler to ask the RISC-V to raise a “software interrupt” and immediately return. The RISC-V delivers software interrupts to the kernel with the ordinary trap mechanism, and allows the kernel to disable them. The code to handle the software interrupt generated by a timer interrupt can be seen in devintr [kernel/trap.c:205](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/trap.c#L205).

定时器中断可以在用户态或内核态代码执行时的任何点发生；内核没有办法在关键操作期间禁用定时器中断。因此，定时器中断处理程序必须以不会干扰被中断的内核代码的方式完成其工作。基本的策略是让处理程序请求 RISC-V 触发一个“软件中断”并立即返回。RISC-V 通过普通的陷阱机制将软件中断传递给内核，并允许内核禁用它们。处理由定时器中断生成的软件中断的代码可以在 devintr 中看到。

> The machine-mode timer interrupt handler is timervec ([kernel/kernelvec.S:95](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/kernelvec.S#L95)). It saves a few registers in the scratch area prepared by start, tells the CLINT when to generate the next timer interrupt, asks the RISC-V to raise a software interrupt, restores registers, and returns. There’s no C code in the timer interrupt handler.

机器模式下的定时器中断处理程序是 timervec ([kernel/kernelvec.S:95](https://github.com/mit-pdos/xv6-riscv/blob/riscv/kernel/kernelvec.S#L95))。它在 start 准备的暂存区中保存一些寄存器，告诉 CLINT 何时生成下一个定时器中断，请求 RISC-V 触发一个软件中断，恢复寄存器，然后返回。定时器中断处理程序中没有 C 代码。



# 第八章 文件系统

文件系统的目的是组织和存储数据。文件系统通常支持用户和应用程序之间的数据共享，以及持久性，以便重启后数据仍然可用。

xv6文件系统提供了类Unix的文件、目录和路径名（请参见第1章），并将其数据存储在virtio磁盘上以实现持久性。文件系统解决了几个挑战：
• 文件系统需要磁盘上的数据结构来表示命名目录和文件的树，记录保存每个文件内容的块的身份，以及记录磁盘上哪些区域是空闲的。
• 文件系统必须支持崩溃恢复。也就是说，如果发生崩溃（例如电源故障），文件系统在重启后仍必须正确工作。风险在于崩溃可能会中断一系列更新，并留下不一致的磁盘数据结构（例如，一个块既被文件使用又被标记为空闲）。
• 不同的进程可能同时操作文件系统，因此文件系统代码必须协调以维护不变量。
• 访问磁盘比访问内存慢得多，因此文件系统必须维护常用块的内存缓存。

本章的其余部分解释了xv6是如何解决这些挑战的。
