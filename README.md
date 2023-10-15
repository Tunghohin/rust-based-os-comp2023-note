# rust-based-os-comp2023-note
Learning Record

# Week 1 (2023-10-08 ~ 2023-10-15)
## Day 1
前几天看了一部分rust圣经，开始刷 rustlings，第一天大概刷了四五十题这样，前面的题没碰到什么难的地方。
## Day 2
大概到 60 多题之后，开始有些复杂知识点的题，边写边查，写题速度骤降。学了一些迭代器的用法 https://zhuanlan.zhihu.com/p/346583098 。
## Day 3
test 后面几题涉及到了编译链接的知识，了解到了 rust 编译后的代码默认是 mangled 的 https://os.phil-opp.com/freestanding-rust-binary/#linker-arguments
今天完成了 rustlings 的 100 题。
## Day 4
感觉光看不练容易忘，尝试从代码中学习。

开始看 rCore Tutorial, 今天把环境配好了，折腾了一下 nvim 的 rust-analyzer 在 riscv 开发环境的 LSP 设置。
## Day 5
尝试复现 ch1 libos，边研究边调试，了解了程序的执行环境的概念和 sbi 对 os 的支持。
## Day 6 
尝试复现 ch2 批处理系统，上午看得有点头晕，不太理解是如何从 os 态切换到用户态的。

晚上梳理了一下 trap 的流程。
![Screenshot from 2023-10-15 22-57-47](https://github.com/Tunghohin/rust-based-os-comp2023-note/assets/88049360/a2f2ef95-525a-456b-b9b4-1c4c93fad1d3)

实际上 os 切换到用户态依赖一个 trap context，将其压到内核栈中，并把返回地址调成用户态程序的起始地址，再将 sp 修改成用户栈即可完成切换，中间 cpu 模式的转换依赖一些硬件支持。
## Day 7
完成批处理系统的复现，开始看 ch3 多道程序与分时多任务。

晚上看完了多道程序协作式调度，实际上多到程序的切换就是把 TaskContext 的返回地址设置成 __restore, 利用 __restore 跳到用户态，原理跟批处理系统差不多。

## Day 8
看了分时多任务，并且成功复现。
