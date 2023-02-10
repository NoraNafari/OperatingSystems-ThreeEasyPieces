###Scheduling: The Multi-Level Feedback Queue

What issues does MLFQ address?
- Optimize turnaround time
- Minimize response time

**MLFQ: Basic Rules**

- Rule1: if Priority(A)>Priority(B) ==> A runs (B doesn't)
- Rule2: if Priority(A)=Priority(B) ==> Round Robin scheduling between the jobs.

MLFQ varies the priority of a job based on its observed behaviour. (uses the _history_ to predict the _future_)

- Rule3: When a job enters the system, it's placed at the highest priority.
- Rule4a: If a job uses and entire time slice while running, its priority is _reduced_.
- Rule4b: If a job gives up the CPU before the time slice is up, it stays at the same priority level.

So when a new job enters the queue, the OS will assume that it is going to be a _short_ job and give it a high priority.

**Problems with the current design:**
- Too many interactive jobs in the system will consume all CPU time and the long-running jobs will starve.
- A smart writer may _game the scheduler_ meaning that it can write something sneaky to trick the scheduler into
giving you more than you fair share of resources (e.g. issue an I/O operation before the time slice is over)
- A program may change its behavior over time.

- Rule5: After some time period _S_, move all the jobs in the system to the topmost queue.
**Problem:** We will never know the right value for S.

In order to prevent gaming ot the resources we have to keep a track of CPU time at each level.

- Rule4: Once a job uses up its time allotment at a given level (regardless of how many times it has given up the CPU),
its priority is reduced (moves down the queue).

