# HelenOS 0.2.0 源码分析项目

## 概述

HelenOS 0.2.0 版本发布于 2006 年。作为一个实验性和研究性的操作系统，HelenOS 可以说是不够完美的。0.2.0 版本与现有 0.11.0 版本相比又那么老，肯定有非常多需要优化的地方。但我们选择 0.2.0 版本源码进行分析是有理由的：

+ 当下我们对 OS 的理论及组成模块有了一定的理论认知，但是对 OS 的具体实现细节以及硬件相关的部分的细节缺乏深入的了解。亟需深入研究一款 OS 的源码，来获得对 OS 的实操性认知。
+ 现有的知识水平以及时间不足以支撑我们去研究完整地研究 Linux 内核，甚至 Nuttx 对我们来说都太大了。我们需要的是一款短小精悍又结构清晰、模块完整的 OS，来尽快夯实我们对 OS 的深入理解。

相信在研究完 HelenOS 后，我们接下来想要设计一款完整的 OS 时，在 OS 的架构组成、各个模块的耦合方面上会有更大的掌控力，在 OS 的设计创新方面也会有更好的方向性。

## 为什么选择 amd64 架构来阅读

实际上，HelenOS 支持多种架构。理论上来说，选择任何一种都可以。因为 OS 所需的硬件的支持是类似的。但 amd64 是不错的研究对象，因为这个架构使用最为广泛，相关资料丰富，能给我们带来不少便利。

## HelenOS 0.2.0 版针对 amd64 裁剪过的源码

源码下载地址：https://github.com/liuhahapku/helenos0.2.0amd64_reading

## 模块列表

+ [时间管理 (Time Management)](/time_management/time_management.md)
+ [异常与中断(Exception And Interrupt)](/exception_and_interrupt/exception_and_interrupt.md)
