# Time Management

## 通用时间管理模块 generic/time


通用时间管理模块包含3个部分，源文件结构如下
```text
generic/include/time/
├── clock.h
├── delay.h
└── timeout.h

generic/src/time/
├── clock.c
├── delay.c
└── timeout.c
```
其中
+ delay 用于将CPU上的任务暂停一段时间，具体见 [delay](/time_management/delay.md) 模块。


+ timeout 用于维护每个CPU上的定时器队列，具体见 [timeout](/time_management/timeout.md) 模块。

+ clock 用于处理定时器到时及线程的抢占等，具体见 [clock](/time_management/clock.md) 模块。


## 架构相关时间管理

### 8254 芯片

8254 芯片是 amd64 架构下常用的定时计数器芯片，为 HelenOS 的时间管理模块提供了硬件支持。具体参考[8254芯片](/time_management/8254_chip.md)模块。
