Based on: [https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/index.htm](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/index.htm)

# Notes
## Lab1
### Paper 1
Source: [http://www.phrack.com/issues/49/14.html#article](http://www.phrack.com/issues/49/14.html#article)

A process contains three regions: text, data, stack.
The text region includes code and read-only data and corresponds to the text section of the executable file.
The data region contains static variables and corresponds to the data-bss sections of the executable file.

> Here is an explanation about the mentioned "sections" in an executable file: [Medium article](https://medium.com/iqube-kct/know-what-is-bss-text-data-memory-segments-of-an-executable-file-in-embedded-systems-6158d92aa519).

The stack is a data type, which holds objects and has operations to manage the order of those objects, e.g. PUSH and POP. The arrangement of the objects is done in a [LIFO pattern](https://www.geeksforgeeks.org/lifo-last-in-first-out-approach-in-programming/).
The stack is also a contiguous block of data in memory. The stack pointer (SP) points to the top of the stack. The bottom of the stack is a fixed address.
The stack consists of logical stack frames that are pushed when calling a function and popped when returning.  A stack frame contains the parameters to
a function, its local variables, and the data necessary to recover the previous stack frame, including the value of the instruction pointer at the
time of the function call.

Depending on the implementation the stack will either grow down (towards lower memory addresses), or up. The stack pointer (SP) is also
implementation dependent.  It may point to the last address on the stack, or to the next free available address after the stack.

Another frame pointer (FP) is often used to point to the address of a frame, so that the distance of local variables and parameters in a function is consistent upon function calls.


