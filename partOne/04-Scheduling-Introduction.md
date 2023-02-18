###Scheduling: Introduction

The assumptions that we make about the workload in the system:
1. Each job runs for the same amount of time.
2. All jobs arrive at the same time.
3. Once started, each job runs to completion.
4. All jobs only use the CPU (no I/O)
5. The run-time of each job is known.

**Scheduling Metrics:**

- **Turnaroud time:** The time at which the job completes minus the time at
which the job arrived in the system.
- **Fairness**

**Scheduling methods:**
1. FIFO: problem is when the first job takes too long, the other two will have to wait in line (relax assumption number one)
2. SJF (Shortest Job First): relax assumption number two: same problem as FIFO
3. STCF (Shortest Time-To-Completion First): relax assumption number 3.
The scheduler can preempt the long-running job when a short one comes.
It is also known as **Preemptive Shortest Job First (PSJF)**

**A New Metric: Response Time:** the time from when the job arrives in a system
to the first time it is scheduled.

STCF is not good for response time.
If three jobs arrive at the same time, then the third has to wait for the first two to finish.

**Round Robin:** To solve this problem, instead of running jobs to completion,
round robin runs a job for a _time slice_ and then switches to the next job (otherwise called _time-slicing_)


When there is a fixed cost to some operation, the general technique of **amortization**
is used. e.g. if time slice is 10ms and context-switch cost is 1 ms, then 10% of time is spent 
context-switching. If we want to _amortize_ this cost, we can increase the time slice to 100ms.
Then, less than 1% of time is spent on context switching.

If we want to take turnaround time as a metric, then RR is one of the worst.

Whichever algorithm is good for turnaround, is not good for response time and vice versa.

**Incorporating I/O:** We relax assumption 4. When we have a job that initates an I/O request,
it won't be using the CPU while waiting for I/O completion.
The scheduler should schedule another job on the CPU.
It should make the decision of when the I/O will be completed, and raise an interrupt.
Doing so will allow for an _overlap_ with the CPU being used by one process while 
waiting for the I/O of another.