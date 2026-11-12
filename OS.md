# Operating System (OS)

> Core Operating System concepts for technical interviews. Covers processes, threads, CPU scheduling, memory management, synchronization, deadlocks, and OS architecture without Linux-specific commands.

---

# Table of Contents

1. [Operating System Fundamentals](#1-operating-system-fundamentals)
2. [Types of Operating Systems](#2-types-of-operating-systems)
3. [Kernel and OS Architecture](#3-kernel-and-os-architecture)
4. [Process Management](#4-process-management)
5. [Process vs Thread](#5-process-vs-thread)
6. [Process States](#6-process-states)
7. [Process Control Block (PCB)](#7-process-control-block-pcb)
8. [Context Switching](#8-context-switching)
9. [CPU Scheduling](#9-cpu-scheduling)
10. [Scheduling Algorithms](#10-scheduling-algorithms)
11. [Threads and Multithreading](#11-threads-and-multithreading)
12. [Thread Models](#12-thread-models)
13. [Concurrency vs Parallelism](#13-concurrency-vs-parallelism)
14. [Inter-Process Communication (IPC)](#14-inter-process-communication-ipc)
15. [CPU and Process Synchronization](#15-cpu-and-process-synchronization)
16. [Race Condition and Critical Section](#16-race-condition-and-critical-section)
17. [Mutex and Semaphore](#17-mutex-and-semaphore)
18. [Deadlocks](#18-deadlocks)
19. [Memory Management](#19-memory-management)
20. [Contiguous Memory Allocation](#20-contiguous-memory-allocation)
21. [Paging](#21-paging)
22. [Segmentation](#22-segmentation)
23. [Virtual Memory](#23-virtual-memory)
24. [Page Fault](#24-page-fault)
25. [Page Replacement Algorithms](#25-page-replacement-algorithms)
26. [Thrashing](#26-thrashing)
27. [Memory Fragmentation](#27-memory-fragmentation)
28. [File System Concepts](#28-file-system-concepts)
29. [Disk Scheduling](#29-disk-scheduling)
30. [I/O Management](#30-io-management)
31. [Interrupts and System Calls](#31-interrupts-and-system-calls)
32. [Protection and Security](#32-protection-and-security)
33. [Important OS Interview Questions](#33-important-os-interview-questions)
34. [Quick Revision Cheat Sheet](#34-quick-revision-cheat-sheet)

---

# 1. Operating System Fundamentals

## What is an Operating System?

An Operating System is system software that acts as an interface between computer hardware and application software.

It manages hardware resources and provides services required for application execution.

### Main Responsibilities

- Process management
- CPU scheduling
- Memory management
- File management
- Device management
- I/O management
- Security and protection
- Resource allocation

## What is a Program?

A program is a set of instructions stored in a file that performs a particular task.

## What is a Process?

A process is an instance of a program currently executing.

**Example:**

A browser application installed on a computer is a program. When you open it, an executing instance becomes a process.

## What is Multiprogramming?

Multiprogramming allows multiple programs to reside in memory simultaneously.

When one program waits for I/O, the CPU can execute another program.

**Goal:** Maximize CPU utilization.

## What is Multitasking?

Multitasking allows multiple tasks to make progress during overlapping periods.

The OS switches CPU execution between tasks to provide the appearance of simultaneous execution.

**Goal:** Improve responsiveness and resource utilization.

## What is Multiprocessing?

Multiprocessing uses two or more processing units or CPU cores to execute processes.

**Goal:** Improve computational performance through parallel execution.

## What is Time Sharing?

Time sharing allows multiple users or tasks to share CPU time.

Each task receives a small CPU time slice, providing interactive responsiveness.

---

# 2. Types of Operating Systems

## 2.1 Batch Operating System

Jobs are collected and executed in batches without direct interaction during execution.

Characteristics:

- Jobs are grouped together.
- User interaction is minimal.
- Suitable for repetitive processing.

Example: Payroll processing.

## 2.2 Multiprogramming Operating System

Multiple programs are kept in memory.

When one program waits for I/O, another can use the CPU.

Main objective: Increase CPU utilization.

## 2.3 Multitasking Operating System

Multiple tasks execute through CPU scheduling and context switching.

Main objective: Provide responsive execution.

## 2.4 Time-Sharing Operating System

Multiple users or processes share CPU time through time slices.

Main objective: Interactive system responsiveness.

## 2.5 Multiprocessing Operating System

Supports multiple CPUs or CPU cores.

Main objective: Execute tasks in parallel.

## 2.6 Real-Time Operating System (RTOS)

An RTOS is designed to provide predictable responses within specified timing constraints.

### Hard Real-Time System

Missing a deadline is considered a system failure.

Examples:

- Aircraft control systems
- Critical industrial control systems

### Soft Real-Time System

Missing a deadline occasionally reduces quality but does not necessarily cause system failure.

Examples:

- Multimedia applications
- Video streaming systems

## 2.7 Distributed Operating System

Manages multiple interconnected computers and may provide users with a unified system view.

## 2.8 Network Operating System

Provides services and resource sharing over a network.

Examples:

- File sharing
- Remote access
- Network authentication

---

# 3. Kernel and OS Architecture

## What is a Kernel?

The kernel is the core component of an operating system.

It manages:

- Processes
- Memory
- CPU scheduling
- Devices
- Interrupts
- System calls

## Kernel Mode vs User Mode

| Kernel Mode | User Mode |
|---|---|
| Privileged execution mode | Restricted execution mode |
| Can execute privileged instructions | Cannot execute privileged instructions |
| Access to protected system resources | Access through controlled interfaces |
| Used by kernel | Used by applications |

## Why are two modes required?

They provide protection against applications directly interfering with hardware or other applications.

## Monolithic Kernel

Most OS services execute within kernel space.

Advantages:

- High performance
- Efficient communication between kernel components

Disadvantages:

- Large kernel
- Faults in kernel components can affect the entire system

## Microkernel

Only essential services execute in kernel space.

Other services execute in user space.

Advantages:

- Better modularity
- Improved isolation
- Easier maintenance

Disadvantages:

- Communication overhead
- Potential performance cost

## Hybrid Kernel

Combines aspects of monolithic and microkernel architectures.

## System Call

A system call is an interface through which a user program requests a service from the OS kernel.

Examples:

- Process creation
- File operations
- Memory allocation
- Communication
- Process termination

---

# 4. Process Management

## What is a Process?

A process is a program in execution.

A process contains:

- Program code
- Data
- Stack
- Heap
- CPU registers
- Program counter
- Process state
- Resource information

## Process vs Program

| Program | Process |
|---|---|
| Passive entity | Active entity |
| Stored on disk | Executing in memory |
| Contains instructions | Executes instructions |
| No execution state | Has execution state |
| Can create multiple processes | Represents an execution instance |

## Process ID (PID)

A PID is an identifier assigned to a process.

## Parent Process and Child Process

A parent process can create child processes.

The child may execute the same program or a different program.

## Process Creation

A process can create another process through OS-supported process creation mechanisms.

The newly created process is called a child process.

## Process Termination

A process terminates when:

- It completes execution.
- It encounters an unrecoverable error.
- It is terminated by another process or the OS.
- It exceeds certain resource constraints.

## Process Scheduling

The OS selects processes for CPU execution according to its scheduling policy.

---

# 5. Process vs Thread

## What is a Thread?

A thread is the smallest unit of execution within a process.

A process may contain multiple threads.

## Process vs Thread

| Feature | Process | Thread |
|---|---|---|
| Definition | Program in execution | Execution unit within a process |
| Memory | Separate virtual address space | Shares process memory |
| Code | Own process code mapping | Shares process code |
| Heap | Process-specific | Shared among threads |
| Stack | Own stack | Own stack |
| Registers | Own execution context | Own execution context |
| Communication | IPC generally required | Shared memory is available |
| Creation overhead | Usually higher | Usually lower |
| Context switching | Usually more expensive | Often cheaper |
| Isolation | Stronger | Weaker |
| Failure impact | Generally isolated | Can affect entire process |

## Why are threads called lightweight processes?

Threads require fewer resources than independent processes because they share many process resources.

## Why does each thread have its own stack?

Each thread executes independently and maintains its own function calls, local variables, and return addresses.

## Why do threads share heap memory?

Threads belong to the same process and share its address space.

This allows them to access common dynamically allocated objects.

## Advantages of Multithreading

- Better responsiveness
- Improved resource sharing
- Reduced creation overhead
- Better utilization of multiple CPU cores
- Efficient concurrent execution

## Disadvantages of Multithreading

- Race conditions
- Deadlocks
- Synchronization complexity
- Difficult debugging
- Shared-memory corruption

## Example

A browser may use separate processes for isolation and multiple threads within a process for different tasks.

A multithreaded web server may use several threads to handle concurrent requests.

---

# 6. Process States

A process moves through different states during its lifecycle.

## Five-State Process Model

```text
           New
            |
            v
          Ready <----------+
            |             |
            v             |
         Running          |
        /   |   \         |
       /    |    \        |
      v     v     v       |
 Waiting  Exit  Preempted-+
```

## Process States

### 1. New

The process is being created.

### 2. Ready

The process is prepared to execute but is waiting for CPU allocation.

### 3. Running

The process is currently executing on the CPU.

### 4. Waiting / Blocked

The process is waiting for an event, such as I/O completion.

### 5. Terminated

The process has completed execution.

## State Transitions

- New → Ready: Process admitted by OS.
- Ready → Running: CPU assigned.
- Running → Ready: Preemption or time slice expiration.
- Running → Waiting: Process requests I/O or waits for an event.
- Waiting → Ready: Event or I/O completes.
- Running → Terminated: Process finishes.

## Ready vs Waiting

| Ready | Waiting |
|---|---|
| Waiting for CPU | Waiting for an event |
| Can execute immediately when scheduled | Cannot execute until event occurs |

---

# 7. Process Control Block (PCB)

## What is PCB?

A Process Control Block is a data structure maintained by the OS to store information about a process.

## PCB Contains

- Process ID
- Process state
- Program counter
- CPU registers
- CPU scheduling information
- Memory management information
- Accounting information
- I/O status information

## Why is PCB important?

The OS uses PCB information to manage processes and restore their execution context after context switching.

---

# 8. Context Switching

## What is Context Switching?

Context switching is the process of saving the execution state of one process or thread and restoring the execution state of another.

## Steps

1. Current process is interrupted or stops executing.
2. OS saves its execution context.
3. OS updates its process state.
4. Scheduler selects another process.
5. OS restores the selected process context.
6. Execution resumes.

## Why is Context Switching required?

- Multitasking
- CPU scheduling
- Interrupt handling
- Process blocking
- Time-sharing

## Context Switching Overhead

Context switching consumes CPU time without directly performing application work.

Excessive context switching can reduce overall performance.

## Process vs Thread Context Switching

Thread context switching within the same process may require less work because address-space information may remain unchanged.

However, the actual cost depends on the OS, hardware, and scheduling situation.

---

# 9. CPU Scheduling

## What is CPU Scheduling?

CPU scheduling is the process of selecting a ready process or thread for CPU execution.

## Why is CPU Scheduling required?

- Multiple processes compete for CPU.
- CPU resources must be allocated efficiently.
- Interactive applications need responsiveness.
- OS must balance fairness and performance.

## Types of Schedulers

### Long-Term Scheduler

Selects jobs to admit into the system.

Controls the degree of multiprogramming.

### Short-Term Scheduler

Selects the next ready process to execute on the CPU.

Runs frequently.

### Medium-Term Scheduler

Temporarily removes processes from memory and later restores them.

This is associated with swapping or suspension.

## Dispatcher

The dispatcher transfers CPU control to the process selected by the short-term scheduler.

It performs activities such as:

- Context switching
- Switching to user mode
- Resuming execution

## Scheduling Criteria

| Criterion | Meaning |
|---|---|
| CPU Utilization | Percentage of time CPU is busy |
| Throughput | Processes completed per unit time |
| Turnaround Time | Total time from submission to completion |
| Waiting Time | Time spent waiting in ready queue |
| Response Time | Time until first response or first CPU service |

## Important Formulas

Turnaround Time:

`Turnaround Time = Completion Time - Arrival Time`

Waiting Time:

`Waiting Time = Turnaround Time - CPU Burst Time`

Response Time:

`Response Time = First CPU Start Time - Arrival Time`

---

# 10. Scheduling Algorithms

## 10.1 First Come First Serve (FCFS)

Processes execute in arrival order.

### Advantages

- Simple
- Easy to implement
- Fair according to arrival order

### Disadvantages

- Convoy effect
- High average waiting time
- Poor responsiveness for interactive systems

## 10.2 Shortest Job First (SJF)

The process with the shortest CPU burst is selected first.

### Advantages

- Minimizes average waiting time under ideal assumptions

### Disadvantages

- Burst time must be estimated
- Long processes may starve

## 10.3 Shortest Remaining Time First (SRTF)

Preemptive version of SJF.

The process with the shortest remaining CPU burst executes.

A running process can be preempted if another process has a shorter remaining time.

## 10.4 Round Robin (RR)

Each process receives a fixed time quantum.

If the process does not finish within the quantum, it is preempted and placed back in the ready queue.

### Advantages

- Fair CPU allocation
- Good response time
- Suitable for time-sharing systems

### Disadvantages

- Very small quantum causes excessive context switching.
- Very large quantum approaches FCFS behavior.

## 10.5 Priority Scheduling

Processes are scheduled according to priority.

### Advantages

- Important tasks can receive CPU earlier.

### Disadvantages

- Low-priority processes may starve.

### Aging

Aging gradually increases the priority of waiting processes to reduce starvation.

## 10.6 Multilevel Queue Scheduling

Ready queue is divided into multiple queues based on process type.

Each queue may have its own scheduling algorithm.

## 10.7 Multilevel Feedback Queue

Processes can move between queues depending on their behavior and CPU usage.

It supports dynamic priority adjustment.

## Scheduling Algorithm Comparison

| Algorithm | Preemptive? | Main Advantage | Main Disadvantage |
|---|---|---|---|
| FCFS | No | Simple | Convoy effect |
| SJF | No | Low average waiting | Starvation |
| SRTF | Yes | Efficient waiting time | Starvation |
| Round Robin | Yes | Fairness | Context switching |
| Priority | Both | Important tasks prioritized | Starvation |
| Multilevel Queue | Usually fixed queue policy | Classification | Inflexible |
| Multilevel Feedback Queue | Usually | Adaptability | Complexity |

---

# 11. Threads and Multithreading

## What is Multithreading?

Multithreading is the execution of multiple threads within one process.

Threads share process resources but execute independently.

## User-Level Threads

Managed by a user-space thread library.

Advantages:

- Fast thread creation
- Fast switching
- No kernel involvement for every thread operation

Disadvantages:

- Blocking operations may block the entire process in some implementations.
- Kernel may not schedule individual user threads independently.

## Kernel-Level Threads

Managed directly by the operating system kernel.

Advantages:

- Threads can execute in parallel on multiple CPUs.
- Blocking one thread does not necessarily block other threads.
- Kernel schedules threads independently.

Disadvantages:

- Thread management requires kernel involvement.
- Operations can have greater overhead.

## User Threads vs Kernel Threads

| User-Level Threads | Kernel-Level Threads |
|---|---|
| Managed by user library | Managed by OS |
| Faster management | More kernel overhead |
| Kernel may not see individual threads | Kernel schedules individual threads |
| Blocking can affect multiple threads in some models | Blocking affects individual thread |

---

# 12. Thread Models

## Many-to-One

Many user threads map to one kernel thread.

- Fast user-space management
- No true parallel execution across CPU cores
- Blocking may affect all threads

## One-to-One

Each user thread maps to one kernel thread.

- Supports parallelism
- Blocking affects individual threads
- Greater kernel resource usage

## Many-to-Many

Many user threads map to multiple kernel threads.

- Supports parallelism
- Flexible thread management
- More complex implementation

---

# 13. Concurrency vs Parallelism

## Concurrency

Multiple tasks make progress during overlapping periods.

Tasks may execute by switching between them.

## Parallelism

Multiple tasks execute simultaneously.

Requires multiple execution resources, such as CPU cores.

## Concurrency vs Parallelism

| Concurrency | Parallelism |
|---|---|
| Multiple tasks progress | Multiple tasks execute simultaneously |
| Can occur on one core | Requires multiple execution resources |
| Focuses on coordination | Focuses on simultaneous execution |

---

# 14. Inter-Process Communication (IPC)

## What is IPC?

IPC allows processes to exchange information and coordinate execution.

Processes usually have separate address spaces, so IPC mechanisms enable communication.

## IPC Mechanisms

### 1. Shared Memory

Multiple processes access a common memory region.

Advantages:

- Very fast
- Suitable for large data exchange

Disadvantages:

- Requires synchronization
- Can cause race conditions

### 2. Message Passing

Processes exchange messages through OS-managed communication mechanisms.

Advantages:

- Easier isolation
- No direct shared-memory access required

Disadvantages:

- Communication overhead
- Message copying may be required

### 3. Pipes

A pipe allows data to flow between processes.

### 4. Named Pipes

Named pipes allow communication between processes through a named communication object.

### 5. Message Queues

Processes exchange messages through queues.

### 6. Sockets

Sockets support communication between processes on the same system or across systems.

## Shared Memory vs Message Passing

| Shared Memory | Message Passing |
|---|---|
| Common memory region | Exchange messages |
| Very fast | May have communication overhead |
| Requires synchronization | OS may manage synchronization |
| Suitable for large data | Suitable for structured communication |

---

# 15. CPU and Process Synchronization

## What is Synchronization?

Synchronization ensures that concurrent processes or threads access shared resources safely.

It prevents inconsistent data and coordinates execution.

## Why is Synchronization Needed?

Multiple threads may access shared data simultaneously.

Without synchronization, updates may interfere with one another.

## Example

Two threads increment a shared counter.

If both read the same value before either writes its result, one increment may be lost.

Synchronization ensures the operation executes safely.

---

# 16. Race Condition and Critical Section

## Race Condition

A race condition occurs when the outcome depends on the timing or ordering of concurrent operations.

## Critical Section

A critical section is the portion of code that accesses shared resources and must be protected from conflicting concurrent execution.

## Critical Section Problem

A correct solution should satisfy:

### 1. Mutual Exclusion

Only one process or thread can execute the protected critical section at a time.

### 2. Progress

If no process is executing the critical section, the selection of the next process should not be postponed indefinitely.

### 3. Bounded Waiting

A process should not wait indefinitely to enter the critical section after requesting access.

## Race Condition Example

Two threads increment a shared counter.

Without synchronization:

- Thread A reads 5.
- Thread B reads 5.
- Thread A writes 6.
- Thread B writes 6.

Expected result: 7.

Actual result: 6.

---

# 17. Mutex and Semaphore

## Mutex

A mutex is a synchronization mechanism that provides mutual exclusion.

Only one thread can hold the mutex at a time.

## Semaphore

A semaphore is a synchronization mechanism that uses a counter to control access to resources.

## Types of Semaphore

### Binary Semaphore

Counter typically has values 0 or 1.

### Counting Semaphore

Counter can represent multiple available resource instances.

## Mutex vs Semaphore

| Mutex | Semaphore |
|---|---|
| Provides mutual exclusion | Controls resource availability |
| Has ownership | Generally no ownership requirement |
| Usually one thread holds it | Can allow multiple concurrent accesses |
| Used to protect critical sections | Used for synchronization and resource counting |

## Semaphore Operations

### wait()

Decreases the semaphore count or blocks if the resource is unavailable.

### signal()

Increases the semaphore count and may wake a waiting process.

These operations must be atomic.

## Producer-Consumer Problem

A producer creates data and places it into a shared buffer.

A consumer removes data from the buffer.

Synchronization is needed to:

- Prevent buffer overflow
- Prevent buffer underflow
- Protect shared buffer access

---

# 18. Deadlocks

## What is Deadlock?

A deadlock occurs when two or more processes wait indefinitely for resources held by one another.

## Example

- Process A holds Resource 1 and waits for Resource 2.
- Process B holds Resource 2 and waits for Resource 1.

Both processes remain blocked.

## Four Necessary Conditions for Deadlock

All four conditions must hold simultaneously.

### 1. Mutual Exclusion

A resource cannot be shared simultaneously by multiple processes.

### 2. Hold and Wait

A process holds one resource while waiting for another.

### 3. No Preemption

Resources cannot be forcibly taken away from a process.

### 4. Circular Wait

A circular chain of processes exists, with each process waiting for a resource held by the next process.

## Deadlock Handling Methods

### Deadlock Prevention

Design the system so at least one necessary deadlock condition cannot occur.

### Deadlock Avoidance

Allocate resources only when the system remains in a safe state.

### Deadlock Detection

Allow deadlocks to occur and detect them afterward.

### Deadlock Recovery

Recover by terminating processes or reclaiming resources.

## Safe State

A system is in a safe state if there exists an order in which all processes can complete using available resources and resources released by completed processes.

## Unsafe State

An unsafe state does not guarantee that all processes can complete.

An unsafe state is not necessarily already deadlocked.

## Banker's Algorithm

Banker's Algorithm is a deadlock avoidance algorithm.

It checks whether resource allocation leaves the system in a safe state.

## Deadlock vs Starvation

| Deadlock | Starvation |
|---|---|
| Processes wait indefinitely for one another | Process waits indefinitely for resources |
| Circular waiting may exist | No circular wait required |
| Deadlocked processes cannot progress | Other processes may progress |
| Requires deadlock handling | Can be reduced using fairness and aging |

---

# 19. Memory Management

## What is Memory Management?

Memory management is the OS function responsible for allocating, tracking, protecting, and releasing memory.

## Main Responsibilities

- Allocate memory to processes
- Track memory usage
- Protect process address spaces
- Manage physical memory
- Support virtual memory
- Translate addresses

## Types of Memory

### Primary Memory

RAM directly accessible by the CPU.

### Secondary Memory

Storage devices used for persistent data.

## Logical Address

Address generated by the CPU during execution.

## Physical Address

Actual address in physical memory.

## MMU

The Memory Management Unit translates logical or virtual addresses into physical addresses and enforces memory protection.

---

# 20. Contiguous Memory Allocation

## What is Contiguous Memory Allocation?

Each process is allocated one continuous region of physical memory.

## Fixed Partitioning

Memory is divided into fixed-sized partitions.

Each partition can hold one process.

### Disadvantage

Internal fragmentation.

## Variable Partitioning

Partitions are created according to process memory requirements.

### Disadvantage

External fragmentation.

## Allocation Algorithms

### First Fit

Allocates the first available block large enough.

### Best Fit

Allocates the smallest available block that can accommodate the process.

### Worst Fit

Allocates the largest available block.

## Comparison

| Algorithm | Advantage | Disadvantage |
|---|---|---|
| First Fit | Fast | Can leave fragmented regions |
| Best Fit | Small immediate leftover | Can create many tiny fragments |
| Worst Fit | Leaves larger remaining block | May waste large blocks |

---

# 21. Paging

## What is Paging?

Paging divides virtual memory into fixed-sized pages and physical memory into fixed-sized frames.

Pages can be mapped to any available physical frames.

## Page Table

A page table stores mappings between virtual pages and physical frames.

## Advantages

- Eliminates external fragmentation in physical memory allocation.
- Allows non-contiguous memory allocation.
- Supports virtual memory.
- Provides memory protection.

## Disadvantages

- Internal fragmentation may occur.
- Page tables consume memory.
- Address translation introduces overhead.

## Page Number and Offset

A virtual address is divided into:

- Page number
- Page offset

The page number identifies the virtual page.

The offset identifies the location within the page.

## TLB

Translation Lookaside Buffer (TLB) is a cache that stores recently used address translations.

## TLB Hit

Translation is found in the TLB.

## TLB Miss

Translation is not found in the TLB, so the system must obtain it from the page table or another translation mechanism.

A TLB miss is not necessarily a page fault.

---

# 22. Segmentation

## What is Segmentation?

Segmentation divides a process's address space into logical segments.

Examples:

- Code
- Data
- Stack
- Heap

Segments can have different sizes.

## Segment Table

A segment table stores information about segments.

Typically:

- Base address
- Limit

## Advantages

- Matches logical program structure.
- Supports segment-level protection.
- Allows sharing of logical segments.

## Disadvantages

- External fragmentation.
- Memory allocation can become complex.

## Paging vs Segmentation

| Paging | Segmentation |
|---|---|
| Fixed-sized pages | Variable-sized segments |
| Physical memory management | Logical memory organization |
| Internal fragmentation possible | External fragmentation possible |
| Transparent to program structure | Reflects logical program structure |
| Page number + offset | Segment number + offset |

---

# 23. Virtual Memory

## What is Virtual Memory?

Virtual memory allows processes to execute without requiring all their memory pages to reside in physical RAM simultaneously.

It provides a virtual address space larger than or independent of physical memory availability.

## Benefits

- Process isolation
- Efficient memory utilization
- Larger virtual address spaces
- Demand loading
- Simplified memory management

## Demand Paging

Pages are loaded into physical memory only when required.

## Advantages

- Reduced initial loading time
- Lower memory usage
- More processes can remain active

## Disadvantages

- Page faults introduce overhead.
- Excessive page faults can reduce performance.

## Working Set

The working set is the collection of pages actively used by a process during a particular time interval.

A sufficient working set in memory helps reduce page faults.

---

# 24. Page Fault

## What is a Page Fault?

A page fault occurs when a process accesses a virtual memory page that requires OS handling.

## Page Fault Handling

1. CPU accesses a virtual address.
2. Hardware detects that the required mapping or access is unavailable.
3. Control transfers to the OS.
4. OS checks whether the access is valid.
5. If valid, the required page is obtained or mapped.
6. Page tables are updated.
7. The instruction is restarted.

If the access is invalid, the OS may terminate the process or raise an appropriate exception.

## Minor Page Fault

Resolved without storage I/O.

## Major Page Fault

Requires storage I/O.

## Page Fault vs TLB Miss

| Page Fault | TLB Miss |
|---|---|
| Page requires OS handling | Translation not found in TLB |
| May require disk access | Usually resolved through page table lookup |
| Can be expensive | Usually much cheaper |
| Can occur even with a TLB lookup | Does not necessarily cause a page fault |

---

# 25. Page Replacement Algorithms

When physical memory is full, the OS may need to replace a page.

## 25.1 FIFO

First In First Out.

The oldest loaded page is replaced.

### Disadvantage

May remove frequently used pages.

## 25.2 LRU

Least Recently Used.

Replaces the page that has not been used for the longest time.

### Advantage

Uses recent access history.

## 25.3 Optimal Page Replacement

Replaces the page that will not be used for the longest time in the future.

### Advantage

Produces the minimum possible page faults for a given reference sequence.

### Disadvantage

Future memory references are not known in advance.

Used mainly as a theoretical benchmark.

## 25.4 LFU

Least Frequently Used.

Replaces the page with the lowest access frequency.

## 25.5 Second Chance

FIFO-based algorithm that gives recently referenced pages another chance before replacement.

## FIFO vs LRU

| FIFO | LRU |
|---|---|
| Based on arrival time | Based on recent usage |
| Simple implementation | More tracking required |
| May remove frequently used pages | Often better reflects locality |

## Belady's Anomaly

In FIFO page replacement, increasing the number of frames can sometimes increase the number of page faults.

This is called Belady's Anomaly.

FIFO is susceptible to this anomaly.

---

# 26. Thrashing

## What is Thrashing?

Thrashing occurs when the system spends excessive time handling page faults and moving pages between memory and storage.

## Causes

- Insufficient physical memory
- Too many active processes
- Working sets exceeding available memory

## Symptoms

- High page fault rate
- Excessive storage activity
- Low useful CPU productivity
- Poor system performance

## Prevention

- Reduce degree of multiprogramming.
- Allocate sufficient memory.
- Improve working-set management.
- Use appropriate page replacement policies.

---

# 27. Memory Fragmentation

## Internal Fragmentation

Memory allocated to a process is larger than the memory it actually requires.

Unused space remains inside the allocated block.

Example:

A process requires 6 KB but receives an 8 KB partition.

Unused space: 2 KB.

## External Fragmentation

Free memory exists but is divided into small non-contiguous blocks.

A process may not receive a sufficiently large contiguous allocation despite enough total free memory.

## Internal vs External Fragmentation

| Internal | External |
|---|---|
| Waste inside allocated memory | Waste between allocated regions |
| Fixed partitioning commonly causes it | Variable partitioning commonly causes it |
| Paging may cause it | Contiguous allocation may cause it |

## Compaction

Compaction combines scattered free memory into one large contiguous region.

It can reduce external fragmentation but requires moving memory contents.

---

# 28. File System Concepts

## What is a File System?

A filesystem organizes and stores files and directories on storage.

## File Attributes

- Name
- Type
- Size
- Location
- Permissions
- Owner
- Creation or modification information

## File Operations

- Create
- Open
- Read
- Write
- Close
- Delete
- Rename

## File Access Methods

### Sequential Access

Data is accessed in sequence.

### Direct Access

Data can be accessed at a specified position.

### Indexed Access

An index helps locate data efficiently.

## Directory Structures

- Single-level directory
- Two-level directory
- Tree-structured directory
- Acyclic graph directory
- General graph directory

## Inode

An inode stores file metadata and references to file data blocks.

The filename is stored separately in directory entries.

## Hard Link

Another directory entry referencing the same inode.

## Symbolic Link

A separate filesystem object containing a pathname reference to another object.

---

# 29. Disk Scheduling

Disk scheduling determines the order in which disk I/O requests are serviced.

## 29.1 FCFS

Requests are served in arrival order.

Advantages:

- Simple
- Fair

Disadvantages:

- High seek time

## 29.2 SSTF

Shortest Seek Time First.

Serves the request closest to the current disk head position.

Advantages:

- Reduces average seek time

Disadvantages:

- Requests far away may starve

## 29.3 SCAN

Disk head moves in one direction servicing requests, then reverses direction.

Also called the elevator algorithm.

## 29.4 C-SCAN

Disk head moves in one direction only.

After reaching one end, it returns to the opposite end and continues servicing requests.

## 29.5 LOOK

Like SCAN, but reverses at the last pending request rather than going to the physical disk end.

## 29.6 C-LOOK

Like C-SCAN, but jumps between the last and first pending requests instead of reaching the physical disk ends.

## Disk Scheduling Comparison

| Algorithm | Main Idea |
|---|---|
| FCFS | Arrival order |
| SSTF | Closest request |
| SCAN | Move in both directions |
| C-SCAN | Move in one direction |
| LOOK | SCAN without reaching disk end |
| C-LOOK | C-SCAN without reaching disk end |

---

# 30. I/O Management

## What is I/O Management?

The OS manages communication between applications and hardware devices.

Examples:

- Keyboard
- Mouse
- Storage
- Network interfaces
- Printers

## Polling

CPU repeatedly checks whether a device requires attention.

Disadvantage: Can waste CPU time.

## Interrupt-Driven I/O

A device interrupts the CPU when it requires attention.

Advantages:

- Reduces unnecessary polling
- Improves CPU efficiency

## DMA

Direct Memory Access allows devices to transfer data directly to or from memory with limited CPU involvement.

Advantages:

- Efficient large data transfers
- Reduced CPU overhead

## Buffering

Temporary storage used during data transfer.

## Caching

Stores frequently accessed data for faster future access.

## Spooling

Stores jobs in a queue for later processing.

Example: Print jobs waiting for a printer.

---

# 31. Interrupts and System Calls

## What is an Interrupt?

An interrupt is an event that causes the CPU to temporarily suspend its current execution and handle an event.

## Hardware Interrupt

Generated by hardware devices.

Examples:

- Keyboard input
- Timer
- Network interface

## Software Interrupt

Generated through software mechanisms.

## Exception

An exception is an event generated during instruction execution.

Examples:

- Division by zero
- Invalid memory access
- Invalid instruction

## Interrupt vs Exception

| Interrupt | Exception |
|---|---|
| Generally external to current instruction | Generally caused by current instruction |
| Often asynchronous | Usually synchronous |
| Example: hardware timer | Example: division by zero |

## Interrupt Handling

1. Event occurs.
2. CPU transfers control to the appropriate handler.
3. OS handles the event.
4. Execution resumes when appropriate.

## System Call vs Interrupt

| System Call | Interrupt |
|---|---|
| Application requests OS service | Event requires CPU attention |
| Usually initiated intentionally by application | May be hardware-generated |
| Controlled entry into kernel | Interrupt handler processes event |

---

# 32. Protection and Security

## What is Protection?

Protection controls access to system resources.

It ensures processes access only permitted resources.

## What is Security?

Security protects the system against unauthorized access and malicious activity.

## Authentication

Verifies the identity of a user or process.

## Authorization

Determines which resources an authenticated entity may access.

## Access Control

Defines permissions for accessing resources.

## Privilege Levels

Operating systems use privilege levels to isolate applications from sensitive operations.

## Process Isolation

Each process typically has its own virtual address space.

One process cannot normally access another process's private memory directly.

## Memory Protection

The OS and hardware enforce access permissions for memory regions.

Examples:

- Read-only memory
- Executable memory
- Non-executable memory
- Restricted memory mappings

## User Mode vs Kernel Mode

User mode restricts applications from directly executing privileged operations.

Kernel mode allows the OS to manage protected resources.

---

# 33. Important OS Interview Questions

## OS Fundamentals

1. What is an Operating System?
2. What are the responsibilities of an OS?
3. What is a kernel?
4. What is the difference between kernel and OS?
5. What is user mode and kernel mode?
6. What is a system call?
7. What is multiprogramming?
8. What is multitasking?
9. What is multiprocessing?
10. What is time sharing?
11. What is a real-time operating system?
12. What is the difference between hard and soft real-time systems?
13. What is a monolithic kernel?
14. What is a microkernel?

## Process Management

15. What is a process?
16. What is the difference between a program and a process?
17. What is a PCB?
18. What are the different process states?
19. What is a context switch?
20. What is a parent process?
21. What is a child process?
22. What is a zombie process?
23. What is an orphan process?
24. What is the difference between zombie and orphan processes?
25. What is process scheduling?
26. What is a dispatcher?
27. What is the difference between ready and waiting states?

## Threads

28. What is a thread?
29. What is the difference between process and thread?
30. Why are threads called lightweight processes?
31. Why does each thread have its own stack?
32. What are the advantages of multithreading?
33. What are the disadvantages of multithreading?
34. What are user-level threads?
35. What are kernel-level threads?
36. What is the difference between user and kernel threads?
37. Explain many-to-one threading.
38. Explain one-to-one threading.
39. Explain many-to-many threading.
40. What is concurrency?
41. What is parallelism?
42. What is the difference between concurrency and parallelism?

## CPU Scheduling

43. What is CPU scheduling?
44. What is preemptive scheduling?
45. What is non-preemptive scheduling?
46. What is FCFS scheduling?
47. What is SJF scheduling?
48. What is SRTF scheduling?
49. What is Round Robin scheduling?
50. What is priority scheduling?
51. What is starvation?
52. What is aging?
53. What is the convoy effect?
54. What is a time quantum?
55. What is turnaround time?
56. What is waiting time?
57. What is response time?
58. What is throughput?
59. What is CPU utilization?
60. What is the difference between long-term and short-term schedulers?

## Synchronization

61. What is process synchronization?
62. What is a race condition?
63. What is a critical section?
64. What is the critical section problem?
65. What are the three requirements of a critical section solution?
66. What is a mutex?
67. What is a semaphore?
68. What is the difference between mutex and semaphore?
69. What is a binary semaphore?
70. What is a counting semaphore?
71. What are wait and signal operations?
72. What is the producer-consumer problem?
73. What is a deadlock?
74. What are the four necessary conditions for deadlock?
75. What is deadlock prevention?
76. What is deadlock avoidance?
77. What is deadlock detection?
78. What is deadlock recovery?
79. What is Banker's Algorithm?
80. What is a safe state?
81. What is the difference between deadlock and starvation?
82. What is livelock?

## Memory Management

83. What is memory management?
84. What is logical address?
85. What is physical address?
86. What is an MMU?
87. What is contiguous memory allocation?
88. What is fixed partitioning?
89. What is variable partitioning?
90. What is internal fragmentation?
91. What is external fragmentation?
92. What is compaction?
93. What is paging?
94. What is a page?
95. What is a frame?
96. What is a page table?
97. What is a TLB?
98. What is a TLB hit?
99. What is a TLB miss?
100. What is segmentation?
101. What is the difference between paging and segmentation?
102. What is virtual memory?
103. What is demand paging?
104. What is a page fault?
105. What is the difference between minor and major page faults?
106. What is page replacement?
107. Explain FIFO page replacement.
108. Explain LRU page replacement.
109. Explain Optimal page replacement.
110. What is Belady's Anomaly?
111. What is thrashing?
112. What is the working set of a process?

## File Systems and I/O

113. What is a filesystem?
114. What is an inode?
115. What is the difference between hard link and symbolic link?
116. What are file access methods?
117. What are directory structures?
118. What is disk scheduling?
119. Explain FCFS disk scheduling.
120. Explain SSTF.
121. Explain SCAN.
122. Explain C-SCAN.
123. What is DMA?
124. What is interrupt-driven I/O?
125. What is polling?
126. What is buffering?
127. What is caching?
128. What is spooling?

## Advanced Concepts

129. What is IPC?
130. What is shared memory?
131. What is message passing?
132. What is the difference between shared memory and message passing?
133. What is an interrupt?
134. What is an exception?
135. What is the difference between interrupt and exception?
136. What is process isolation?
137. What is memory protection?
138. What is authentication?
139. What is authorization?
140. What is the difference between protection and security?

---

# 34. Quick Revision Cheat Sheet

| Concept | One-Line Definition |
|---|---|
| OS | Software that manages hardware and applications |
| Kernel | Core component of an OS |
| Process | Program in execution |
| Thread | Execution unit within a process |
| PCB | Data structure containing process information |
| Context Switching | Switching CPU execution between processes or threads |
| Ready State | Waiting for CPU |
| Waiting State | Waiting for an event |
| Zombie | Terminated process awaiting exit-status collection |
| Orphan | Running process whose original parent has exited |
| Multiprogramming | Multiple programs kept in memory |
| Multitasking | Multiple tasks make progress through scheduling |
| Multiprocessing | Execution using multiple CPUs or cores |
| Concurrency | Multiple tasks make progress during overlapping periods |
| Parallelism | Multiple tasks execute simultaneously |
| FCFS | Executes in arrival order |
| SJF | Selects shortest CPU burst |
| SRTF | Selects shortest remaining CPU burst |
| Round Robin | Each process gets a time quantum |
| Starvation | Process waits indefinitely for resources |
| Aging | Gradually increases waiting process priority |
| Race Condition | Result depends on concurrent execution order |
| Critical Section | Code accessing shared resources |
| Mutex | Mutual exclusion lock |
| Semaphore | Counter-based synchronization mechanism |
| Deadlock | Processes wait indefinitely for one another |
| Paging | Memory divided into fixed-sized pages |
| Segmentation | Memory divided into logical segments |
| Virtual Memory | Virtual address space independent of physical RAM layout |
| Page Fault | Memory access requires OS handling |
| TLB | Cache of address translations |
| Internal Fragmentation | Waste inside allocated memory |
| External Fragmentation | Free memory scattered across regions |
| Thrashing | Excessive paging reduces useful execution |
| DMA | Device transfers data directly to/from memory |
| IPC | Communication between processes |
| System Call | Application requests OS service |
| Interrupt | Event requiring CPU attention |
| MMU | Translates addresses and enforces memory protection |

---

## Most Important Topics for OS Interviews

If preparing for fresher software engineering, backend, or Cloud/DevOps interviews, prioritize these topics:

1. Process vs Thread
2. Process States
3. PCB and Context Switching
4. CPU Scheduling Algorithms
5. Preemptive vs Non-Preemptive Scheduling
6. Multithreading and Thread Models
7. Concurrency vs Parallelism
8. Race Conditions and Critical Sections
9. Mutex vs Semaphore
10. Deadlock and Its Four Conditions
11. Deadlock Prevention vs Avoidance
12. Paging vs Segmentation
13. Virtual Memory
14. Page Faults
15. Page Replacement Algorithms
16. Internal vs External Fragmentation
17. Thrashing
18. IPC Mechanisms
19. Interrupts vs System Calls
20. User Mode vs Kernel Mode

**Recommended preparation order:** Process Management → Threads → CPU Scheduling → Synchronization → Deadlocks → Memory Management → Virtual Memory → IPC → File Systems → I/O Management.

