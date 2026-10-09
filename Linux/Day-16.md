# Day 16: Managing Processes and Optimizing Performance in Linux

## 📌 Overview

In this session, we will learn about **Linux Processes, Process Management, Job Control, Process States, and Performance Monitoring**.

Process management is an important Linux skill for DevOps engineers because applications, services, scripts, and commands all run as processes.

We will learn:

- What is a process?
- Why process management is important
- Process lifecycle
- Foreground and background processes
- Jobs and job control
- Process states
- `ps` command
- `top` command
- `htop` command
- `kill` and `killall`
- Starting and managing background jobs
- Stopping and resuming jobs
- Understanding PIDs and PPIDs

---

# 1. ⚙️ What is a Process?

A **process is a running instance of a program**.

Whenever you execute a command or start an application, Linux creates a process to execute it.

For example:

    ls

When you run:

    ls

Linux creates a process to execute the `ls` command.

Similarly:

    vim file.txt

starts a process for the Vim editor.

A web server, database server, Docker container process, Jenkins process, and shell script can also involve processes.

---

# 2. 🧠 Program vs Process

This is an important concept.

## Program

A **program** is a file containing instructions.

Example:

    /usr/bin/python3

## Process

A **process** is the running instance of that program.

Example:

    python3 app.py

So:

    Program
       ↓
    Execute
       ↓
    Process

### Easy Example

Think about a music player.

The music player application installed on your computer is a:

    Program

When you open it and start playing music, it becomes a:

    Process

---

# 3. 💡 Why Do We Manage Processes?

Process management is important because Linux systems may run hundreds or thousands of processes simultaneously.

### 1. Resource Allocation

Processes consume:

- CPU
- Memory
- Disk I/O
- Network resources

### 2. System Stability

We can identify and control processes that consume excessive resources.

### 3. Performance Monitoring

We can identify:

- High CPU processes
- High memory processes
- Slow processes
- Processes waiting for I/O

### 4. Troubleshooting

Process management helps troubleshoot:

- Hanging applications
- Applications not responding
- High CPU usage
- High memory usage
- Failed services

### 5. Automation

We can run scripts and commands in the background.

---

# 4. 🔢 Process ID (PID)

Every running process in Linux has a unique number called a:

**PID → Process ID**

Example:

    PID
    1234

We can use the PID to identify and manage a process.

For example:

    kill 1234

This sends a signal to the process with PID `1234`.

---

# 5. 👨‍👦 Parent Process and Child Process

Linux processes have relationships.

A process can create another process.

The process that creates another process is called the:

**Parent Process**

The newly created process is called the:

**Child Process**

Example:

    Parent Process
          │
          ├── Child Process
          │
          └── Child Process

---

# 6. PPID – Parent Process ID

`PPID` stands for:

**Parent Process ID**

It identifies the process that created the current process.

Example:

    PID     PPID
    2000    1500

Here:

    PID  → 2000
    PPID → 1500

This means process `1500` is the parent of process `2000`.

---

# 7. 🔄 Process Lifecycle

A process generally goes through several stages.

## 1. Creation

The process is created by the system.

Linux commonly creates new processes using mechanisms such as `fork()` and `exec()`.

## 2. Ready

The process is ready to run and waits for CPU scheduling.

## 3. Running

The process is executing instructions on the CPU.

## 4. Waiting

The process may wait for:

- Disk I/O
- Network I/O
- User input
- Another event

## 5. Termination

The process finishes or is terminated.

## 6. Cleanup

The kernel releases the resources associated with the process.

---

# 8. 🔄 Process Lifecycle Diagram

    New
     ↓
    Ready
     ↓
    Running
     ↓
    Waiting
     ↓
    Ready
     ↓
    Running
     ↓
    Terminated
     ↓
    Cleanup

A process may move between **Running** and **Waiting** multiple times during its lifetime.

---

# 9. 🏃 Types of Processes

There are different ways to classify processes.

## 1. Foreground Process

A foreground process runs interactively with the terminal.

The shell normally waits for the foreground command to finish before giving you another prompt.

Examples:

    ls

    nano file.txt

    vim file.txt

    gcc program.c

### Characteristics

- Interactive
- Connected to the terminal
- User normally waits for completion
- Can often be interrupted using `Ctrl+C`

---

# 10. 🌙 Background Process

A background process runs without blocking the shell prompt.

Example:

    sleep 800 &

The `&` starts the command as a background job.

You can continue using the terminal while the command runs.

### Characteristics

- Runs in the background
- Shell can accept new commands
- Useful for long-running tasks
- Can be managed using job-control commands

---

# 11. 🧟 Zombie Process

A **zombie process** is a process that has already terminated, but its parent process has not yet collected its exit status.

The process is no longer executing, but a small entry remains in the process table.

### Why Does It Happen?

The child process terminates.

The parent should collect its exit status using `wait()` or a related mechanism.

Until that happens, the child may appear as:

    Z

### Important

A zombie process is **not a running process consuming CPU**.

It mainly represents a process-table entry waiting for its parent to handle it.

---

# 12. 📌 Process vs Job

These terms are related but different.

## Process

A process is an executing program managed by the operating system.

It has a:

    PID

## Job

A job is a shell's way of managing commands started from that shell.

A job has a:

    Job ID

Example:

    sleep 800 &

The shell may show:

    [1] 1234

Here:

    1    → Job ID
    1234 → PID

So:

    Job ID → Shell-level identification
    PID    → Operating-system process identification

---

# 13. 🖥️ Types of Jobs

## 1. Foreground Job

A foreground job currently controls the terminal.

Example:

    vim file.txt

The terminal is occupied by Vim until you exit it.

---

## 2. Background Job

A background job runs without controlling the terminal interactively.

Example:

    sleep 800 &

The shell prompt becomes available again.

---

## 3. Stopped Job

A stopped job is temporarily suspended.

For example:

    sleep 800

Press:

    Ctrl+Z

The job becomes stopped.

It can later be resumed using:

    fg

or:

    bg

---

# 14. 🔍 Viewing Processes

Linux provides several commands for viewing processes.

The most common are:

    ps
    top
    htop

---

# 15. 📋 ps Command

`ps` stands for:

**Process Status**

It displays information about processes.

---

## Basic ps

    ps

By default, this shows processes associated with the current shell/session in a basic view.

Example:

    PID TTY          TIME CMD
    1200 pts/0    00:00:00 bash
    1450 pts/0    00:00:00 ps

---

# 16. ps aux

Use:

    ps aux

This displays a detailed list of processes running on the system.

Important columns include:

| Column | Meaning |
|---|---|
| `USER` | User who owns the process |
| `PID` | Process ID |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `VSZ` | Virtual memory size |
| `RSS` | Resident memory |
| `TTY` | Terminal |
| `STAT` | Process state |
| `START` | Start time |
| `TIME` | CPU time used |
| `COMMAND` | Command used to start the process |

---

# 17. ps -ef

Another common command is:

    ps -ef

It provides a full-format process listing.

Important columns include:

| Column | Meaning |
|---|---|
| `UID` | User ID/name |
| `PID` | Process ID |
| `PPID` | Parent Process ID |
| `C` | CPU utilization indicator |
| `STIME` | Start time |
| `TTY` | Terminal |
| `TIME` | CPU time |
| `CMD` | Command |

---

# 18. ps -p

To view a specific process:

    ps -p 1234

Replace `1234` with the actual PID.

For example:

    ps -p 1234 -o pid,ppid,stat,cmd

This displays selected information about the process.

---

# 19. 🔴 top Command

`top` is a real-time process monitoring tool.

Run:

    top

It continuously updates process information.

It helps us monitor:

- CPU usage
- Memory usage
- Running processes
- Process states
- Load information
- System activity

---

## Important top Columns

| Column | Meaning |
|---|---|
| `PID` | Process ID |
| `USER` | Process owner |
| `PR` | Priority |
| `NI` | Nice value |
| `VIRT` | Virtual memory |
| `RES` | Resident memory |
| `SHR` | Shared memory |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `TIME+` | CPU time |
| `COMMAND` | Process/command name |

---

# 20. 🟢 htop Command

`htop` is an interactive process viewer.

Run:

    htop

It is often easier to read and interact with than `top`.

If it is not installed, install it using the package manager appropriate for your Linux distribution.

For Debian/Ubuntu:

    sudo apt install htop

Then:

    htop

---

# 21. 🛑 Controlling Processes

Linux allows us to control processes using signals.

The most common command is:

    kill

---

# 22. kill Command

Despite its name, `kill` does not always mean "forcefully terminate."

It sends a **signal** to a process.

### Basic Syntax

    kill PID

Example:

    kill 1234

By default, this sends:

    SIGTERM

which asks the process to terminate gracefully.

---

# 23. Common Signals

| Signal | Number | Meaning |
|---|---:|---|
| `SIGTERM` | 15 | Request graceful termination |
| `SIGKILL` | 9 | Force termination |
| `SIGSTOP` | 19 | Stop/suspend process |
| `SIGCONT` | 18 | Continue stopped process |


---

# 24. Gracefully Stop a Process

Use:

    kill 1234

This sends `SIGTERM`.

It gives the application an opportunity to clean up resources and exit properly.

### Recommended Approach

Try:

    kill 1234

before using:

    kill -9 1234

---

# 25. Forcefully Kill a Process

Use:

    kill -9 1234

This sends:

    SIGKILL

The process cannot catch or ignore `SIGKILL`.

### Important

Do not use `kill -9` as the first option unless necessary.

Prefer:

    kill 1234

and use:

    kill -9 1234

when the process does not terminate normally.

---

# 26. Stop and Continue a Process

### Stop Process

    kill -STOP 1234

This suspends the process.

### Continue Process

    kill -CONT 1234

This allows the stopped process to continue.

---

# 27. killall Command

`killall` can send a signal to processes based on their process name.

Example:

    killall nginx

This sends the default termination signal to matching `nginx` processes.

### Force Kill

    killall -9 nginx

### Important

Use process names carefully because multiple processes with the same name may be affected.

---

# 28. 🧠 Process States

A process can be in different states during its lifecycle.

| State | Code | Description |
|---|---|---|
| Running / Runnable | `R` | Running or ready to run |
| Sleeping | `S` | Interruptible sleep |
| Uninterruptible Sleep | `D` | Usually waiting for I/O |
| Stopped | `T` | Stopped by a signal/job control |
| Zombie | `Z` | Terminated but parent has not collected its status |

---

# 29. 🟢 Running State – R

`R` means:

**Running or Runnable**

The process may currently be executing on a CPU or waiting in the run queue to be scheduled.

Example:

    R

---

# 30. 😴 Sleeping State – S

`S` means:

**Interruptible Sleep**

The process is waiting for an event or resource.

For example:

- Waiting for input
- Waiting for a timer
- Waiting for another event

This is normal for many processes.

---

# 31. 💾 Uninterruptible Sleep – D

`D` generally means:

**Uninterruptible Sleep**

The process is usually waiting for an I/O operation to complete.

For example:

- Disk I/O
- Storage device operation
- Certain kernel-level operations

A process stuck in `D` state for a long time may indicate an I/O or hardware/storage problem.

---

# 32. ⏸️ Stopped State – T

`T` means the process is stopped.

For example, when you run:

    sleep 800

and press:

    Ctrl+Z

the job becomes stopped.

---

# 33. 🧟 Zombie State – Z

`Z` means:

**Zombie**

The process has already terminated, but the parent has not yet collected its exit status.

Example:

    Z

A large number of zombie processes may indicate a problem in the parent application's process-management logic.

---

# 34. 🔄 Process State Transitions

A simplified process flow is:

    New
      ↓
    Ready
      ↓
    Running
      ↓
    Waiting
      ↓
    Ready
      ↓
    Running
      ↓
    Terminated
      ↓
    Cleanup

A process may move between states multiple times during its lifetime.

---

# 35. 🎮 Job Control

Job control allows us to manage multiple commands from the same shell session.

We can:

- Start jobs in the background
- Stop jobs
- Resume jobs
- Move jobs between foreground and background
- List jobs
- Terminate jobs

---

# 36. ▶️ Start a Background Job

Use `&` at the end of a command.

Example:

    sleep 800 &

The command starts in the background.

The shell may display something like:

    [1] 1234

Here:

    [1] → Job ID
    1234 → PID

---

# 37. 📋 jobs Command

To list jobs associated with the current shell:

    jobs

Example:

    [1]+  Running    sleep 800 &

---

## jobs -l

Use:

    jobs -l

This displays the job along with its PID.

Example:

    [1]+  1234 Running    sleep 800 &

---

# 38. ⏸️ Stop a Foreground Job

Run:

    sleep 800

Now press:

    Ctrl+Z

The shell may display:

    [1]+  Stopped    sleep 800

The job is now suspended.

---

# 39. 🔙 Bring Job to Foreground

Use:

    fg

This resumes the most recent stopped/background job in the foreground.

You can also specify a job:

    fg %1

Here:

    %1

means Job ID 1.

---

# 40. 🌙 Continue Job in Background

Use:

    bg

This resumes a stopped job in the background.

Or specify the job:

    bg %1

---

# 41. 🛑 Kill a Job

You can terminate a shell job using its job ID:

    kill %1

Here:

    %1

means Job ID 1.

---

# 42. 🔄 Complete Job Control Example

### Step 1: Start a command

    sleep 800

### Step 2: Press

    Ctrl+Z

The job is stopped.

### Step 3: Check jobs

    jobs

### Step 4: Resume in background

    bg %1

### Step 5: Check again

    jobs

### Step 6: Bring it to foreground

    fg %1

### Step 7: Stop it if required

    Ctrl+Z

### Step 8: Kill it

    kill %1

---

# 43. 🆚 Foreground vs Background

| Feature | Foreground | Background |
|---|---|---|
| Terminal control | Yes | No interactive control |
| Shell prompt | Usually unavailable until completion | Available |
| User interaction | Usually possible | Usually limited |
| Example | `vim file.txt` | `sleep 800 &` |
| Job control | Yes | Yes |

---

# 44. 🆚 Process vs Job

| Feature | Process | Job |
|---|---|---|
| Managed by | Operating system | Shell |
| Identifier | PID | Job ID |
| Example | PID `1234` | `%1` |
| Scope | System-wide | Current shell/session |
| Commands | `ps`, `kill` | `jobs`, `fg`, `bg` |

---

# 48. 📊 Useful Process Commands

| Command | Purpose |
|---|---|
| `ps` | Show processes associated with the shell |
| `ps aux` | Show detailed process information |
| `ps -ef` | Full-format process listing |
| `ps -p PID` | Show a specific process |
| `top` | Real-time process monitoring |
| `htop` | Interactive process monitoring |
| `kill PID` | Send SIGTERM |
| `kill -9 PID` | Send SIGKILL |
| `kill -STOP PID` | Stop a process |
| `kill -CONT PID` | Continue a stopped process |
| `killall name` | Signal processes by name |
| `jobs` | Show shell jobs |
| `jobs -l` | Show jobs with PIDs |
| `fg %1` | Bring job to foreground |
| `bg %1` | Resume job in background |



