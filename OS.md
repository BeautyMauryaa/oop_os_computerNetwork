# 2. Operating Systems (OS)

## 2.1 What is an Operating System?

An Operating System is system software that manages computer hardware and software resources and provides an environment for executing applications.

Examples:

- Windows
- Linux
- macOS
- Android

Main responsibilities:

- Process management
- Memory management
- File management
- CPU scheduling
- Device management
- Security and resource allocation

## 2.2 Program vs Process vs Thread

These three are extremely important.

### Program

A program is a set of instructions stored on disk.

Example: Your Node.js application file.

### Process

A process is a program currently executing.

A process has:

- Process ID (PID)
- Memory space
- Resources
- Program code
- Execution state

Example: Running a Node.js server.

### Thread

A thread is the smallest unit of CPU execution within a process.

Multiple threads can exist within one process and share its memory.

[Part 10: Threads & Concurrency | Computer Architecture & OS Mastery - Wasil Zafar](https://images.openai.com/static-rsc-4/vXg47x_FO3JzRxV1Qz-afWl0cPPdkQCj4r2ROe20URnN1fUOMtoSaO3Xsbu3YGOiTiltoomzEN-Wcpqm_0XyctYCzMHjAuK_28pYa7yJSE7qGsghii0EVE0oUe-WJaoMLbj1mbKsxCbl4ABh7jVzTrxh-C7QICEyRWeLAfjpQ90?purpose=inline)

[wasilzafar.com](https://www.wasilzafar.com/pages/series/computer-architecture/comp-arch-threads-concurrency.html?utm_source=chatgpt.com)

### Process vs Thread

| Process                       | Thread                                        |
| ----------------------------- | --------------------------------------------- |
| Independent execution unit    | Execution unit within a process               |
| Separate address space        | Shares process memory                         |
| Higher creation overhead      | Lower creation overhead                       |
| Communication is more complex | Communication is easier through shared memory |
| Failure is generally isolated | A thread failure can affect the whole process |

Backend example:

Suppose you run two separate Node.js server processes.

They have separate process memory.

Within a process, multiple operations can be handled concurrently using the event loop and asynchronous I/O.

Important: Node.js JavaScript execution is primarily single-threaded per event loop, but Node.js also uses worker threads and a libuv thread pool for certain operations.

## 2.3 Process states

A process moves through different states during execution.

[\[운영체제(OS)\] 3. 프로세스(Process)](https://images.openai.com/static-rsc-4/_Ah9KSvTufvqXYpIfp93LZqN0I5CgJdnzOlbOXvrGrNpOy9qevJatv56HiUJMHXf6MaUUXg1dB_I7NLxZKlcruwILGikn3_rrQjYBcxGAkxtgVxTZ3chCbPqDeZSRC5VHvsm_kAITHzcr36Cn9HoWVsA5uM4dJQQQopoDEq1v7E?purpose=inline)

[rebro.kr](https://rebro.kr/172?utm_source=chatgpt.com)

| State           | Meaning                     |
| --------------- | --------------------------- |
| New             | Process is being created    |
| Ready           | Waiting for CPU             |
| Running         | Currently executing         |
| Waiting/Blocked | Waiting for an event or I/O |
| Terminated      | Execution completed         |

Important MCQ: A process waiting for I/O is in the blocked/waiting state, not the ready state.

## 2.4 CPU Scheduling

CPU scheduling determines which ready process gets CPU time.

Important algorithms:

| Algorithm           | Explanation                             |
| ------------------- | --------------------------------------- |
| FCFS                | First Come First Served                 |
| SJF                 | Shortest Job First                      |
| SRTF                | Shortest Remaining Time First           |
| Round Robin         | Each process gets a fixed time quantum  |
| Priority Scheduling | Higher-priority processes execute first |

### Important differences

FCFS

- Simple.
- Non-preemptive.
- Can cause convoy effect.

SJF

- Selects the process with the shortest burst time.
- Can be preemptive or non-preemptive.
- Gives minimum average waiting time under ideal assumptions when burst times are known.

Round Robin

- Uses time quantum.
- Commonly used in time-sharing systems.
- If quantum is too small, context-switching overhead increases.

Priority Scheduling

- Higher-priority processes execute first.
- Can cause starvation.
- Aging helps prevent starvation.

### Important terms

| Term              | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| Waiting time      | Time spent waiting in the ready queue                      |
| Turnaround time   | Completion time − Arrival time                             |
| Response time     | First CPU allocation time − Arrival time                   |
| Context switching | Switching CPU execution from one process/thread to another |

## 2.5 Deadlock

Definition: Deadlock occurs when two or more processes are permanently waiting for resources held by each other.

Example:

- Process A holds Resource 1 and waits for Resource 2.
- Process B holds Resource 2 and waits for Resource 1.
- Neither can proceed.

[CPU Scheduling Algorithms in OS (Operating System)](https://images.openai.com/static-rsc-4/7Bl_UYDYH01K0EVcEIRLFKcKYfJ2imisUNJuEeLPHlPflG_Nm7lAjdFmrfNpafPNnUJnf9Hdz7VPq4e2MqWdirBLM9dchzbTI1E5Tr0FglX0jnj39dcfw_kylyxjWhH7DodHxaevcaRyfM9MYr9i7qv3e4PDk8OnkvX1QG4GB7c?purpose=inline)

[almabetter.com](https://www.almabetter.com/bytes/articles/cpu-scheduling-in-os?utm_source=chatgpt.com)

### Four necessary conditions of deadlock

All four must hold simultaneously.

| Condition           | Meaning                                            |
| ------------------- | -------------------------------------------------- |
| 1. Mutual Exclusion | Resource cannot be shared simultaneously           |
| 2. Hold and Wait    | Process holds a resource while waiting for another |
| 3. No Preemption    | Resource cannot be forcibly taken away             |
| 4. Circular Wait    | Circular chain of resource waiting                 |

Memory trick: M-H-N-C.

If any one of these four conditions is prevented, deadlock cannot occur.

### Deadlock handling

- Prevention: Ensure at least one necessary condition cannot hold.
- Avoidance: Allocate resources safely, e.g. Banker's algorithm.
- Detection: Detect deadlocks after they occur.
- Recovery: Terminate processes or reclaim resources.

Backend scenario: Two database transactions lock rows in opposite order, causing a database deadlock.

Example:

- Transaction A locks row 1, then requests row 2.
- Transaction B locks row 2, then requests row 1.

The database may detect the deadlock and abort one transaction.

## 2.6 Memory Management

OS manages RAM and allocates memory to processes.

### Main memory areas

| Area      | Purpose                            |
| --------- | ---------------------------------- |
| Code/Text | Program instructions               |
| Data      | Global/static variables            |
| Heap      | Dynamically allocated memory       |
| Stack     | Function calls and local variables |

### Stack vs Heap

| Stack                                     | Heap                      |
| ----------------------------------------- | ------------------------- |
| Function call management                  | Dynamic memory allocation |
| Usually automatic allocation/deallocation | Managed dynamically       |
| Typically faster allocation               | Typically more flexible   |
| Limited size                              | Generally larger          |

Example: Local function variables commonly live in stack frames, while dynamically allocated objects generally live in heap memory. Exact implementation depends on language and runtime.

### Paging

Paging divides:

- Physical memory into fixed-size frames.
- Virtual memory into fixed-size pages.

Pages can be mapped to physical frames.

Advantages:

- Avoids external fragmentation.
- Supports virtual memory.
- Simplifies memory allocation.

Important: Paging can still cause internal fragmentation.

### Segmentation

Segmentation divides memory into variable-sized logical sections.

Examples:

- Code segment
- Data segment
- Stack segment

| Paging                           | Segmentation                    |
| -------------------------------- | ------------------------------- |
| Fixed-size blocks                | Variable-size blocks            |
| Physical memory management model | Logical memory division         |
| Internal fragmentation possible  | External fragmentation possible |

### Virtual Memory

Virtual memory allows processes to use a virtual address space larger than the currently available physical RAM.

It uses secondary storage as backing for pages that aren't currently in physical memory.

Page fault: Occurs when a process accesses a virtual memory page that is not currently mapped to physical RAM and requires OS handling.

Thrashing: Excessive paging activity that significantly reduces system performance.

### Fragmentation

- Internal fragmentation: Wasted space inside an allocated memory block.
- External fragmentation: Free memory exists but is scattered in small non-contiguous blocks.

## 2.7 Synchronization and Concurrency

These are useful additional OS concepts.

| Term             | Meaning                                                 |
| ---------------- | ------------------------------------------------------- |
| Race condition   | Result depends on timing/order of concurrent operations |
| Critical section | Code accessing shared resources                         |
| Mutex            | Mutual exclusion lock                                   |
| Semaphore        | Synchronization mechanism using permits/counters        |
| Starvation       | A process waits indefinitely for resources              |
| Livelock         | Processes keep reacting but make no progress            |

Mutex vs Semaphore

- Mutex: Generally one owner locks it at a time.
- Semaphore: Controls access through a counter and permits.