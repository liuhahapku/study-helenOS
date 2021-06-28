# delay

delay 模块只包含一个 delay 函数，函数原型为
```clike
/** Active delay
 *
 * Delay the execution for the given number
 * of microseconds (or slightly more). The delay
 * is implemented as CPU calibrated active loop.
 *
 * @param usec Number of microseconds to sleep.
 */
void delay(__u32 usec)
```

从注释可以看出，这个函数实现了主动延迟的效果。可以将执行流延迟给定的微秒数（也有可能多一些，即不一定是精确的）。延迟是根据 CPU 校准过的循环来实现的，通俗点说就是根据 CPU 的频率决定循环的次数。

具体实现 delay 功能的函数体如下

```clike
void delay(__u32 usec)
{
	ipl_t ipl;

	/*
	 * The delay loop is calibrated for each and every
	 * CPU in the system. Therefore it is necessary to
	 * call interrupts_disable() before calling the
	 * asm_delay_loop().
	 */
	ipl = interrupts_disable();
	asm_delay_loop(usec * CPU->delay_loop_const);
	interrupts_restore(ipl);
}
```
函数体中的```asm_delay_loop```函数使用汇编代码控制 CPU 进行空转的循环，以此来实现延迟。在进入这个汇编函数之前，需要关闭中断，在离开这个汇编函数之后，需要重置中断。关闭和打开中断也会花费时间，也许这就是前面提到的比实际延迟多一点的来源。中断的关闭与打开实现方式与具体的架构有关，请参考 [arch/interrupt](/arch_related/interrupt.md) 模块源码分析。


汇编函数```asm_delay_loop```定义在架构相关代码中，以 ```amd64``` 为例，函数定义在```arch/amd64/src/delay.S``` 中。函数体如下

```text
asm_delay_loop:
0:  dec %rdi
    jnz 0b
    ret
```

这个函数只有两条汇编语句，它的功能是将这两条汇编语句循环 n 次，n 就是函数的参数。```rdi```寄存器存放函数的第一个参数（即循环次数，当然是一个正整数），0处的代码```dec %rdi```表示对寄存器减一，```jnz 0b```表示如果上一条指令运算的结果不为0，那么跳转到0处。

函数```delay```中的```asm_delay_loop```的参数是```usec * CPU->delay_loop_const```，即微秒数乘以 CPU 每微秒循环的次数。

在```amd64```架构下，```CPU->delay_loop_const```的大小是由8254定时芯片控制的。具体请参考 [8254 芯片](/time_management/i8254.md)模块。
