# lec1: 操作系统概述

---

## **提前准备**

（请在上课前完成）

* 完成lec1的视频学习和提交对应的在线练习
* git pull ucore\_os\_lab, ucore\_os\_docs, os\_tutorial\_lab, os\_course\_exercises in github repos。这样可以在本机上完成课堂练习。
* 知道OS课程的入口网址，会使用在线视频平台，在线练习/实验平台，在线提问平台\(piazza\)
  * [http://os.cs.tsinghua.edu.cn/oscourse/OS2019spring](http://os.cs.tsinghua.edu.cn/oscourse/OS2019spring)


* 会使用linux shell命令，如ls, rm, mkdir, cat, less, more, gcc等，也会使用linux系统的基本操作。
* 在piazza上就学习中不理解问题进行提问。



# 思考题

## 填空题

* 当前常见的操作系统主要用**C**编程语言编写。
* "Operating system"这个单词起源于**Operator** 。
* 在计算机系统中，控制和管理**硬件和计算机资源** 、有效地组织**用户程序**运行的系统软件称作**操作系统** 。
* 允许多用户将若干个作业提交给计算机系统集中处理的操作系统称为**批处理**操作系统
* 你了解的当前世界上使用最多的操作系统是**Linux** 。
* 应用程序通过**系统调用**接口获得操作系统的服务。
* 现代操作系统的特征包括**并发** ，**共享**， **虚拟** ，**异步** 。
* 操作系统内核的架构包括**硬件抽象层** ， **系统调用接口** ， **命令行程序** 。


## 问答题

- 请总结你认为操作系统应该具有的特征有什么？并对其特征进行简要阐述。

我认为具有下列特征：

* 安全性：用户程序无法修改操作系统代码、未授权用户无法访问未授权的应用、内存。
* 高效性：通过并发、异步等方式保证操作系统有足够高的效率
* 易用性：通过虚拟、共享等方式简化开发、使得应用程序开发者不需要过分了解操作系统的底层实现

- 为什么现在的操作系统基本上用C语言来实现？为什么没有人用python，java来实现操作系统？

有如下原因：

* 由于C语言在效率、灵活性方面仅次于汇编语言，而在开发效率上面远高于汇编语言。
* 操作系统是直接与硬件交互的，这三个语言中只有C语言可以编译成为机器可识别的汇编代码，另两个语言都需要运行在专有的解释器下。
* 只有C语言可以直接修改指定的内存位置的信息。

---

## 可选练习题

---

- 请分析并理解[v9\-computer](https://github.com/chyyuu/os_tutorial_lab/blob/master/v9_computer/docs/v9_computer.md)以及模拟v9\-computer的em.c。理解：在v9\-computer中如何实现时钟中断的；v9 computer的CPU指令，关键变量描述有误或不全的情况；在v9\-computer中的跳转相关操作是如何实现的；在v9\-computer中如何设计相应指令，可有效实现函数调用与返回；OS程序被加载到内存的哪个位置,其堆栈是如何设置的；在v9\-computer中如何完成一次内存地址的读写的；在v9\-computer中如何实现分页机制。


- 请编写一个小程序，在v9-cpu下，能够输出字符


```c
#include <../tools/u.h>

void write_char(c)  { asm(LL,8); asm(LBL,16); asm(BOUT); }
# halt v9 system
halt(val)       { asm(LL,8); asm(HALT); }

char c = '!';
main()
{
        write_char(1, c);
  halt(0);
}
```

- 输入的字符并输出你输入的字符


```c
#include <../tools/u.h>

char in(port)    { asm(LL,8); asm(BIN); }
# output a char to screen
out(port, val)  { asm(LL,8); asm(LBL,16); asm(BOUT); }
# halt v9 system
halt(val)       { asm(LL,8); asm(HALT); }

char c;
main()
{
        c = in(1);
        out(1, c); out(1, '\n');
        halt(0);
}
```

- 请编写一个小程序，在v9-cpu下，能够产生各种异常/中断


- 请编写一个小程序，在v9-cpu下，能够统计并显示内存大小



- 请分析并理解[RISC-V CPU](http://www.riscvbook.com/chinese/)以及会使用模拟RISC\-V(简称RV)的qemu工具。理解：RV的特权指令，CSR寄存器和在RV中如何实现时钟中断和IO操作；OS程序如何被加载运行的；在RV中如何实现分页机制。
  - 请编写一个小程序，在RV下，能够输出字符
  - 输入的字符并输出你输入的字符
  - 请编写一个小程序，在RV下，能够产生各种异常/中断
  - 请编写一个小程序，在RV下，能够统计并显示内存大小
