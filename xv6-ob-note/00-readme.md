MIT 6.s081 OS Labs

官方课程资源：[6.S081/2023/schedule](https://pdos.csail.mit.edu/6.S081/2023/schedule.html)

视频教程：[MIT 公开课 MIT6.S081精译](https://www.bilibili.com/video/BV1rS4y1n7y1/?spm_id_from=333.999.0.0&vd_source=5fc9d3a9044a95a2e4960e3b99616e6e)

视频教程的文字版：[GitHub - huihongxiao/MIT6.S081](https://github.com/huihongxiao/MIT6.S081)

中文资料: [CS自学指南-6.S081](https://csdiy.wiki/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/MIT6.S081/)

可参考的其他资料：

[B站LAB视频](https://space.bilibili.com/28086502/channel/collectiondetail?sid=674585)

[LAB视频对应的笔记](https://cactus-agenda-c84.notion.site/XV6-labs-2021-0894f931b3324edea30dca7826c01a97)

[fanxiao's blog](https://fanxiao.tech/)

[操作系统2023秋](http://hitsz-cslab.gitee.io/os-labs/)

# 环境搭建

[参考网址](https://pdos.csail.mit.edu/6.S081/2021/tools.html)

主要包括编译工具链，qemu，gdb以及依赖的各种工具库。

`gdb-multiarch`无法单步调试`ecall`进入内核，这个问题没有找到解决办法。

于是自己编译安装`riscv64-unknown-elf-gdb`。[参考1](https://zhuanlan.zhihu.com/p/638731320)、[参考2](http://rcore-os.cn/rCore-Tutorial-deploy/docs/pre-lab/gdb.html)

如果自己安装工具链， 过程参考[6.S081/2023/tools](https://pdos.csail.mit.edu/6.S081/2023/tools.html)、[汪辰老师的博客](https://gitee.com/aosp-riscv/working-group/blob/master/articles/20220721-riscv-gcc.md)或者[这个博客](https://zhuanlan.zhihu.com/p/72862396)。

**环境测试：**

在工程主目录下，执行`make qemu`开始编译代码，并开始运行qemu，进入xv6的命令行。`Ctrl A+X`可退出xv6的命令行。

`make qemu-gdb`，并在另一个窗口（也需要在工程主目录下），执行`riscv64-unknown-elf-gdb`，可使用GDB调试xv6的代码。工程主目录下，有`.gdbinit`的文件，启动GDB时，会自动执行该脚本中的命令，比如加载被调试文件的命令。

# labs: Xv6 and Unix utilities

[官方资料](https://pdos.csail.mit.edu/6.S081/2021/labs/util.html)

[环境配置-参考博客](https://zhuanlan.zhihu.com/p/428502480)

**xv6源码**: https://github.com/mit-pdos/xv6-riscv

**xv6实验源码**: `git clone git://g.csail.mit.edu/xv6-labs-2021`