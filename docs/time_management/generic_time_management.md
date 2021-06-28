# Time Management

## generic/time
——通用时间管理模块

通用时间管理模块包含3个部分，文件结构如下
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
其中 delay 用于将CPU上的任务暂停一段时间，具体见 [delay](/time_management/delay.md) 模块源码分析


timeout 用于维护每个CPU上的定时器队列，具体见 [timeout](/time_management/timeout.md) 模块源码分析

clock 用于处理定时器到时及线程的抢占等，具体见 [clock](/time_management/clock.md) 模块源码分析
