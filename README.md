#

```txt
███████╗███████╗███╗   ██╗██╗████████╗██╗  ██╗     ██████╗ ███████╗
╚══███╔╝██╔════╝████╗  ██║██║╚══██╔══╝██║  ██║    ██╔═══██╗██╔════╝
  ███╔╝ █████╗  ██╔██╗ ██║██║   ██║   ███████║    ██║   ██║███████╗
 ███╔╝  ██╔══╝  ██║╚██╗██║██║   ██║   ██╔══██║    ██║   ██║╚════██║
███████╗███████╗██║ ╚████║██║   ██║   ██║  ██║    ╚██████╔╝███████║
╚══════╝╚══════╝╚═╝  ╚═══╝╚═╝   ╚═╝   ╚═╝  ╚═╝     ╚═════╝ ╚══════╝
```

### Unix-Inspired Mini Operating System Simulator in C/C++

---

# About Zenith OS

**ZENITH OS** is a Unix-inspired terminal-based operating system simulator developed completely in **C/C++**.
It demonstrates core Operating System concepts such as:

*  Process Management
*  Memory Management
*  File Management
*  Multithreading
*  Inter-Process Communication (IPC)
*  CPU Scheduling
*  Deadlock Detection
*  Resource Monitoring
*  Background & Foreground Task Handling

The project runs as a process on Linux and internally manages its own simulated kernel operations and application tasks.

---

#  Features

## Kernel Features

* Multi-Level Queue Scheduling
* Round Robin Scheduling
* Aging Mechanism
* PCB (Process Control Block) Management
* Resource Allocation & Reclamation
* Interrupt Handling
* Signal Handling
* Deadlock Detection System
* Logging System
* IPC using Named Pipes (FIFO)
* Background Daemon Services
* Simulated Core Management

---

## Built-in Applications

ZENITH OS contains multiple terminal applications/modules:

| #  | Module             |
| -- | ------------------ |
| 1  | Calculator         |
| 2  | Notepad            |
| 3  | Clock              |
| 4  | Calendar           |
| 5  | Create File        |
| 6  | Delete File        |
| 7  | Move File          |
| 8  | Copy File          |
| 9  | File Info          |
| 10 | Rename File        |
| 11 | Task Manager       |
| 12 | Music Player       |
| 13 | Mini Game          |
| 14 | Instruction Guide  |
| 15 | Dice Roller        |
| 16 | Text Search        |
| 17 | Alarm              |
| 18 | Stopwatch          |
| 19 | File Compression   |
| 20 | Log Viewer         |
| 21 | Mini Terminal      |
| 22 | To-Do List         |
| 23 | Resource Dashboard |
| 24 | Log Daemon         |
| 25 | System Monitor     |

---

# System Architecture

```txt
                ┌──────────────────┐
                │    ZENITH OS     │
                └────────┬─────────┘
                         │
        ┌─────────────────────────────────┐
        │                                 │
 ┌───────────────┐               ┌────────────────┐
 │ Kernel Layer  │               │ Application    │
 │               │               │ Task Layer     │
 └──────┬────────┘               └──────┬─────────┘
        │                                │
 ┌───────────────┐              ┌──────────────────┐
 │ Scheduler     │              │ Calculator       │
 │ IPC Manager   │              │ Notepad          │
 │ Memory Manager│              │ Clock            │
 │ Logger        │              │ Alarm            │
 │ Deadlock Det. │              │ Music Player     │
 │ Storage Mgmt  │              │ File Manager     │
 └───────────────┘              └──────────────────┘
```

---

# Core Concepts Used

| Concept                | Implementation                  |
| ---------------------- | ------------------------------- |
| Process Scheduling     | Multi-Level Queue + Round Robin |
| IPC                    | FIFO Named Pipes                |
| Synchronization        | Mutexes & Condition Variables   |
| Concurrency            | POSIX Threads                   |
| Deadlock Detection     | Wait-For Graph DFS              |
| Interrupts             | UNIX Signals                    |
| Resource Management    | Dynamic Allocation/Reclamation  |
| File System Simulation | `zenith_hdd/` Virtual Storage   |
| Logging                | System Event Logger             |

---

# Project Structure

```txt
ZENITH-OS/
│
├── include/
│   └── kernel/
│       ├── kernel.h
│       ├── logger.h
│       ├── scheduler.h
│       ├── memory_manager.h
│       ├── process_manager.h
│       ├── interrupt_handler.h
│       ├── ipc_manager.h
│       ├── storage_manager.h
│       └── deadlock_detector.h
│
├── src/
│   ├── kernel/
│   └── tasks/
│
├── tasks/
├── zenith_hdd/
├── obj/
├── Makefile
└── OS
```

---

# ⚙️ Technologies Used

* **C++17**
* **POSIX Threads (pthread)**
* **Linux System Calls**
* **Signals**
* **Named Pipes (FIFO)**
* **GNU Compiler (g++)**

---

# Supported Platform

- Linux
- Arch Linux
- Ubuntu
- WSL (Windows Subsystem for Linux)

---

# Compilation & Execution

## Build Project

```bash
make
```

---

## Run Zenith OS

```bash
make run
```

OR

```bash
./OS
```

---

# Example Boot Screen

```txt
ZENITH OS BOOT SEQUENCE

Initializing kernel...
RAM: 4096 MB
HDD: 10240 MB
CPU Cores: 4
Starting Scheduler...
Starting IPC Listener...
```

---

# Scheduling Strategy

ZENITH OS uses:

* **Q0 → System Queue**
* **Q1 → Interactive Queue**
* **Q2 → Background Queue**

### Scheduling Policies

| Queue | Policy              |
| ----- | ------------------- |
| Q0    | Priority Scheduling |
| Q1    | Round Robin         |
| Q2    | FCFS                |

### Aging Mechanism

Processes waiting too long automatically gain priority to prevent starvation.

---

# Deadlock Detection

The system uses:

* Wait-For Graph
* DFS Cycle Detection

to detect possible deadlocks between simulated resources and processes.

---

# IPC System

Inter-process communication is implemented using:

```txt
/tmp/zenith_pipe_PID
```

using FIFO named pipes.

Processes send:

```txt
REQ:<task>:<ram>:<hdd>
```

Kernel responds with:

```txt
GRANT
```

or

```txt
DENY
```

---

# Virtual HDD

All file operations are performed inside:

```txt
zenith_hdd/
```

which acts as the virtual storage drive of the operating system.

---

# Multithreading

ZENITH OS uses pthreads for:

* Scheduler Thread
* Aging Thread
* IPC Listener Thread
* Deadlock Detector Thread
* Interrupt Recovery Thread

---

# Logging System

System logs are stored in:

```txt
system.log
```

Logs include:

* Process creation
* Scheduling events
* Interrupts
* Resource allocation
* Deadlock alerts
* State transitions

---

# Fun Modules

ZENITH OS also contains fun interactive utilities:

* Comic Dice Roller
* Alarm System
* Mini Game
* Music Player
* Stopwatch

---

# Team Members
- Salman Shoaib
- Abdullah Nadeem
- Shoaib Altaf

---

# Educational Purpose

This project was developed for learning and demonstrating:

* Operating System Fundamentals
* Kernel Simulation
* Process Scheduling
* IPC Mechanisms
* Resource Management
* Linux System Programming

---

# Future Improvements

* GUI Version
* Better Shell Interface
* Real File Compression
* Network Stack Simulation
* Virtual Memory Paging
* User Authentication System
* Better Music Player Support

# License

This project is developed for educational purposes.

---

# Final Note

> “ZENITH OS is not just a simulator — it is a practical demonstration of how operating system concepts work together inside a real environment.”

