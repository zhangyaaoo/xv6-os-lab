**xv6** 是一个教学用的操作系统，运行在模拟器 **QEMU** 中。

# 运行xv6

运行 **xv6**：在 xv6-riscv 目录下，输入 `make qemu`。

# 退出xv6

如果你想退出 **xv6**，有两种方式可以实现：

1.  **直接终止 QEMU 进程**：

    *   按下 **Ctrl + a**，然后再按下 **x**。这将直接终止 **QEMU** 进程，并将你带回到 shell 界面。

2.  **先回到QEMU的console界面，然后再退出**：

    *   按下 **Ctrl + a**，然后再按下 **c**。这将退出 **xv6** 的 shell 界面，进入 **QEMU** 的监视器界面。
    *   在监视器界面中，输入 **q** 并按回车键，即可完全退出 **QEMU**。


# 调试xv6

*   在 xv6-riscv 目录下执行 `make qemu-gdb`，进程会阻塞。
*   另开一个终端，在 xv6-riscv 目录下执行 `riscv64-unknown-elf-gdb`。
*   如果出现 `.gdbinit` 相关的错误，将 `add-auto-load-safe-path /home/xxx/xv6-riscv/.gdbinit` 添加到 `/home/xxx/.gdbinit` 文件中。xv6-riscv 下，有`.gdbinit` 的文件，启动GDB时，会自动执行该脚本中的命令，比如加载被调试文件的命令。

# GDB常用命令

## 执行流控制

在 **GDB** 中，这些命令用于控制程序的执行流程和单步调试：

1.  `continue`（或缩写为 `c`）：

    *   `c` 命令用于继续执行程序，直到遇到下一个断点或程序结束。
    *   示例：`(gdb) c`
2.  `next`（或缩写为 `n`）：

    *   `n` 命令执行当前行的代码，并跳到下一行。如果当前行包含函数调用，它会执行整个函数并跳到函数返回的下一行。
    *   示例：`(gdb) n`
3.  `step`（或缩写为 `s`）：

    *   `s` 命令也是单步执行，但与 `n` 不同，如果当前行包含函数调用，它会进入该函数内部并在函数的第一行停止执行。
    *   示例：`(gdb) s`
4.  `stepi`（或缩写为 `si`）：

    *   `si` 命令类似于 `s`，但它是单步执行汇编指令。它会执行当前汇编指令并进入下一条指令。
    *   示例：`(gdb) si`

## 断点

在 **GDB** 中，断点是一项关键的调试功能。它允许你在程序的特定位置暂停执行，以便查看变量、函数调用过程和其他状态。以下是一些常用的断点设置和管理命令：

1.  **设置断点**：

    *   `break function`（或缩写为 `b`）：在指定函数内设置断点。
    *   `break line_number`：在指定行号设置断点。
    *   `break filename:line_number`：在指定源文件的特定行号设置断点。
    *   `break *address`：在指定内存地址设置断点。
2.  **查看断点信息**：

    *   `info breakpoints`（或缩写为 `i b`）：显示当前设置的断点信息。
    *   `info break`：列出断点的详细信息，包括编号、位置和状态。
3.  **删除断点**：

    *   `delete breakpoint_number`：删除指定编号的断点。
    *   `clear`：删除所有断点。
    *   `disable breakpoint_number`：禁用指定编号的断点。
    *   `enable breakpoint_number`：启用指定编号的断点。
4.  **临时断点**：

    *   `tbreak function`：在指定函数内设置临时断点，只会生效一次。

## 运行调试

当你使用 **GDB** 进行程序调试时，以下是一些常用的命令和它们的解释：

1.  **启动 GDB**：

    *   `gdb filename`：启动未运行的程序进行调试（需要运行 `run` 命令）。
    *   `gdb attach pid`：对已经运行的程序进行调试，使用 `detach` 命令可以让 GDB 调试器与程序分离。
2.  **设置断点**：

    *   `break function`：在指定函数中设置一个断点。
    *   `clear`：删除一个断点。
    *   `run [arglist]`：运行你的程序（如果指定了 `arglist`，则将其作为参数运行程序）。
3.  **单步执行**：

    *   `step`（缩写为 `s`）：单步执行，进入函数调用。
    *   `next`（缩写为 `n`）：执行下一行的源代码。
    *   `continue`（缩写为 `c`）：继续运行程序到下一个断点处。
4.  **查看变量和信息**：

    *   `print expr`：打印表达式的值。
    *   `info break`（缩写为 `i b`）：查看断点信息。
    *   `info thread`（缩写为 `i thread`）：列出线程信息。
5.  **其他常用命令**：

    *   `quit`：退出 GDB 调试。
    *   `display`：在断点停止的地方，显示指定的表达式的值。
    *   `set`：设置变量的值，例如 `set nval=54`。

## 监视变量
