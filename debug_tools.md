# debug tools

## Why you debug?

1. Misbehavior
2. Memory Leaks
3. Invalid/Illeagal Memory Access
4. Invalid Instructions
5. Synchrnization issues among the threads or many contexts



## x86 stack frame layout

https://eli.thegreenplace.net/2011/02/04/where-the-top-of-the-stack-is-on-x86/

## x64 stack frame layout

https://eli.thegreenplace.net/2011/09/06/stack-frame-layout-on-x86-64



| Level | Address        | Content    | Comment          |       |
| ----- | -------------- | ---------- | ---------------- | ----- |
|       |                | 0x00000000 |                  |       |
| 2     | 0x7fffffffe310 | 0x00000000 |                  |       |
|       |                | 0x00007fff |                  |       |
|       | 0x7fffffffe308 | 0xf7a2e830 | saved rip        |       |
|       |                | 0x00000000 |                  |       |
| 1     | 0x7fffffffe300 | 0x00400560 | saved rbp        |       |
|       |                | 0x00000000 |                  |       |
|       | 0x7fffffffe2f8 | 0x00400554 | saved rip        |       |
|       |                | 0x00007fff |                  |       |
|       | 0x7fffffffe2f0 | 0xffffe300 | saved rbp        | <-rbp |
|       | 0x7fffffffe2ec | 0x00000010 | local var i (16) | <-sp  |
|       |                |            |                  |       |
|       |                |            |                  |       |
| 0     | 0x7fffffffe2e0 |            |                  |       |
|       |                | 0x00000000 |                  |       |
|       | 0x7fffffffe2d8 | 0x00400543 |                  |       |
|       |                | 0x00007fff |                  |       |
|       | 0x7fffffffe2d0 | 0xffffe2f0 |                  |       |

Ulimit

objdump

## gdb

 * break

> #set breakpoint on a function
>
> break main
>
> #set breakpoint on a file:line
>
> break main.cpp:6
>
> #list breakpoints
>
> info breakpoints
>
> #disable breakpoints
>
> disable 2
>
> #skip breakpoints，2 is the breakpoint-id, 3 is the number of times to skip
>
> ignore 2 3
>
> b foo.cpp:13 thread 28 if x > lim

* scheduler
> set scheduler-locking step/on/off

* checkpoint

> #do checkpoint and back to the past
>
> checkpoint
>
> #list checkpoints
>
> info checkpoint
>
> #restart from the specified checkpoint
>
> restart <i>checkpoint-id</i>

* How to see macros

> g++ -gdwarf-2 g3 a.cpp -o prog

* x (examine memory)

> x/FMT ADDRESS
>
> #examine as a string
>
> x/s address
>
> #examine as a character
>
> x/c address
>
> #examine as 4 characters
>
> x/4c address
>
> #examine as hex
>
> x/x address

* show disassembly code

> disassemble function

* how to return from a function

> finish

bt

​	disassemble

​	info local

​	info args

​	info frame

​	info register

​	info symbol xxx

Ctrl-x-a

Ctrl-l

Ctrl-x-2

Some useful tips: <https://blogs.oracle.com/linux/8-gdb-tricks-you-should-know-v2>

