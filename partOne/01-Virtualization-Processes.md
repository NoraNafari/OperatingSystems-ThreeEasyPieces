###Virtualization-Processes

**Process:** Abstraction provided by the OS of a running program.

**How to provide the illusion of many CPUs?** By virtualizing. By running one process, stopping it,
then running another process, the CPU will create the illusion that many CPUs exist.

**Implementing virtualization:** 
- Low-level machinery => mechanisms: low level methods or protocols that implement a needed piece of functionality.
The answer to _how_ does an OS perform sth?
- High-level intelligence

**Time Sharing:** allowing one entity to use resources for a while and another entity for another while (CPU).
**Space Sharing:** Resource is divided among those who wish for it (disk space). 
**Policies:** Algorithms for making these decisions within the OS. (Which program should run among some choices?)

**Machine State:** (of a program) what a program can read or update when it's running.

**Components of machine state:**
- **Memory:** The memory that a process can address is it's **address space**.
- **Registers:** Instructions that read and update registers (Like program counters-PCs or instruction pointers-IPs)
- **Stack pointer and its related frame pointer:** used to manage the stack of the function parameters, local variables, etx
- **I/O information:** Like the files that the program has open

###Process APIs in OS:
- Create
- Destroy
- Wait
- Miscellaneous Control
- Status

**How does the OS get a program up and running?**
- Load code and static data into memory.
  - Some memory must be allocated for the program's runtime stack.
  - Some memory must be allocated for the program's heap. Heap is explicitly requested for dynamically-allocated data.
- I/O setup (in UNIX systems: file descriptors (in detail later))
- Start main() to transfer the control of the CPU to the newly created processes
 

A Process can be in one of these three states:
- **Running:** executing instructions
- **Ready:** for some reason OS has not chosen to run it now.
- **Blocked:** not ready to run until sth is finished.

**Running ==> Descheduled ==> Ready**

**Ready ==> Scheduled ==> Running**

**Running ==> I/O initiate ==> Blocked**

**Blocked ==> I/O done ==> Ready**

**OS data structures:** 
- process list also called the task list.
- The individual structure that stores data about a process: Process Control Block _OR_ process descriptor.
