###Interlude: Process API

**How to create a process in UNIX?**

Use **fork()** method => creates two processes, The parent comes to life as it has called the fork() itself.

The scheduler may create the parent or the child first.
It is non-deterministic how the process creation is handled.

If you want a parent to wait for a child to accomplish its task: **waitpid()**

Calling wait() can make the code deterministic.

**exec()**: when you want to run a program that is different from the current running program.

It _transforms_ the current running program. It does _not_ create a new process.

**UNIX pipe():** the output of one process is the input of another.

In UNIX shells there are certain shortcut keys that send a signal to a proces.

**SIGINT (Interrupt) : ctrl+c**

**SIGTSTP (stop) : ctrl + z**

Who is able to send a signal to a process? A certain authenticated **user**

**ps** command is used to see which processes are running.
**top** command to see processes and resources