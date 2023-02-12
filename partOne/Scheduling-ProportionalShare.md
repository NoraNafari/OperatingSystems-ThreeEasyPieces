###Scheduling: Proportional Share

**Proportional** _or_ **fair share** scheduler = trying to guarantee that each job obtain a certain 
percentage of CPU time.

**Lottery scheduling:** tickets: used to represent the share of a resource that a process should receive.
The percent of tickets that a process has, represents its share of the system resource needed.

The use of randomness in lottery scheduling leads to probabilistic correctness in meeting
the desired proportion, but no guarantee.

You can also manipulate tickets: like by using the concept of **ticket currency**.

**Ticket currency** allows a user to share tickets among their own jobs in whatever currency they would like.
Then the system automatically converts said currency into the global value.

**Ticket transfer:** can be used to hand off tickets to another process. e.g. a client hands off some
tickets to the server and tries to maximize its performance while the server is handling the client's request.


**Ticket inflation:** a process can temporarily raise or lower the number of tickets it owns.
It can only happen in a group of processes that trust one another.

---
**Implementing Lottery Scheduling**

What you need:
- random number generator
- data structure to track the processes of a system
- total number of tickets

If we sort the list in descending order, it'll take less time to traverse the list.

---

**Stride scheduling:** Each job in the system has a stride which is inverse in proportion to the number of 
tickets it has. Each time a process runs, we will increment its value one by its _stride_.
We will run the job which has the least stride.

---

**The Linux Completely Fair Scheduler**

To achieve its efficiency goals, CFS aims to spend very little time making scheduling decisions.

It uses a counting based technique known as **virtual runtime (vruntime)**.

In the most basic case, each process's vruntime increases at same rate, in proportion with physical time.

If CFS switches too often, fairness is increased.

**sched_latency**: How long one process should run before considering a switch.
CFU divides the value by number of processes to determine the time slice for a process.

The time slice can't be less than a value named **min_granularity.**

CFS also enables control over process priority using **niceness** which can be from -20 to +19 (default 0). 

**positive** means _lower_ priority and **negative** means _higher_ priority (When you're too nice, 
you just won't get as much attention).

---

CFS don't use a list. It uses a **red-black tree**. Only running processes are stored in this tree,
If a process goes to sleep, it is removed from the tree.

If we want to insert a new job in a sorted list, it has O(n) time complexity.
But is a red-black tree, it's O(log n) => insertion and deletion.

What if a long-slept job want's to take the CPU? Will other jobs starve?
CFS handles this by altering the vruntime of a job when it wakes up and set it to the **minimum value found in the tree**.

Problem: jobs that sleep frequently do not ever get their fair share of the CPU.


