###Mechanism: Limited Direct Execution

There are _two_ main challenges in building virtualization machinery:
- performance
- control

**Direct execution:** The program will run directly on the CPU with its own memory, stack, etc.

Problems with this method:
- What if the process wishes to perform some kind of restricted operation (like I/O)? Then it would have to get access 
to system resources. 

In order to avoid the problem of accessing everything in an OS, we introduce **user mode** and **kernel mode**.

The hardware assists the OS by providing different modes of execution.
in **user mode** applications do not have full access to hardware resources.
in **kernel mode** the OS has access to full resources with special instructions to **trap**
into the kernel and **return-from-trap** back to user-mode programs as well as where the **trap table** resides in memory.

When a program needs to execute a system call:
- A program must execute a special trap instruction
- This instruction jumps into the kernel and raises the privilege level to kernel
- The system can now perform the operation needed
- When finished, the OS calls a special **return-from-trap** instructions
- (The system must make sure to save enough of the caller's registers in order to return correctly)
- The **return-from-trap** returns into the calling user program while reducing the privilege back to user mode

The kernel sets up a **trap table** at boot time, telling the hardware what code to run when certain exception occures.

To specify an exact system call, a **system-call number** is assigned to each system call.
OS checks if the number is valid and then handles it.

---
**How can a CPU switch between processes?**

The cooperative approach is for the system to _trust_ the process of a program to behave reasonably.
Processes are assumed to give up the CPU periodically (e.g. by having a system call or when they do sth illegal)

If the program gets in an infinite loop, you have to restart the machine.

The non-cooperative approach is using a **timer interrupt** to raise an interrupt every few milliseconds.
The OS informs the hardware of which code to run when a timer interrupt occurred. it also should start the timer att boot time.

---
When the OS has regained control, it should make a decision to continue the currently running application or switch to another one.
The decision is made by **scheduler**.
If the decision is made, the OS executes a low-level code which is called a **context switch**.
It saves some current register values of the program and execute another process and when the process is finished, restores them
and returns to the previous process-restoring the previous state of the program.