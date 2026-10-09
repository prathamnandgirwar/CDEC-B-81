# DAY 17 - Managing Processes and Optimizing Performance

## 📌 Overview

In Day 16, we learned about Linux processes, process states, foreground and background jobs, and basic process management.

In Day 17, we will go one step further and learn how to **monitor process performance and control process priority**.

### Topics Covered

- Process Priority
- Nice Values
- `nice` Command
- `renice` Command
- Finding Process IDs
- Process Signals
- Process States
- Job Management
- Process Tree
- `pstree` Command
- Practical Process Management

---

# 1. ⚙️ What is Process Priority?

When multiple processes are running at the same time, the Linux kernel needs to decide how CPU time should be shared between them.

This is handled by the **CPU scheduler**.

Each process has scheduling-related properties. One important property is the **nice value**.

The nice value influences how favorably a normal process is treated by the scheduler.

### Easy Example

Imagine three students waiting to use one computer:

    Student A → Normal priority
    Student B → Lower priority
    Student C → Higher priority

Similarly, Linux has multiple processes competing for CPU time:

    Linux Scheduler
           |
    +------+------+------+
    |      |      |      |
    Process A  Process B  Process C
    |      |      |
    +------+------+------+
           |
         CPU Time

> **Important:** Process priority does not mean that one process will always get the CPU first. The Linux scheduler continuously manages CPU time among runnable processes.

---

# 2. 🧠 Understanding Nice Values

Linux uses a **nice value** to influence the scheduling preference of normal processes.

The nice value range is:

    -20  → Higher scheduling priority
      0  → Default
    +19  → Lower scheduling priority

### Easy Way to Remember

    -20 -------- 0 -------- +19
     ↑                         ↑
    Higher                    Lower
    Priority                  Priority

### Important Points

- Nice value range: `-20` to `19`
- Default nice value is usually `0`
- Lower nice value means higher scheduling preference
- Higher nice value means lower scheduling preference
- Negative nice values normally require elevated privileges
- Normal users can generally increase the nice value of their own processes

---

# 3. 🎯 Why Do We Use Nice Values?

Nice values are useful when we want to control the CPU scheduling preference of normal processes.

For example, suppose a server is running:

    Application Server
    Backup Script
    Compression Process
    Database

A backup or compression process may consume significant CPU.

We can start it with a higher nice value so that it has a lower scheduling preference.

Example:

    nice -n 10 tar -czf backup.tar.gz /data

This starts the backup command with a nice value of `10`.

---

# 4. 📊 Checking Process Priority

We can use:

    top

or:

    htop

These commands allow us to monitor processes.

---

# 5. 🔍 Important Columns in top

Run:

    top

You may see columns such as:

    PID   USER   PR   NI   VIRT   RES   SHR   S   %CPU   %MEM   COMMAND

### Important Columns

| Column | Meaning |
|---|---|
| `PID` | Process ID |
| `USER` | User who owns the process |
| `PR` | Scheduling priority shown by the tool |
| `NI` | Nice value |
| `VIRT` | Virtual memory |
| `RES` | Resident memory |
| `SHR` | Shared memory |
| `S` | Process state |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `COMMAND` | Command/process name |

### Important for This Topic

    PR → Priority
    NI → Nice Value

---

# 6. 🧮 Nice Value Example

Suppose we have:

    Process A → NI = 0
    Process B → NI = 10
    Process C → NI = 15

Generally:

    NI = 0   → Higher scheduling preference
    NI = 10  → Lower scheduling preference
    NI = 15  → Even lower scheduling preference

Remember:

    Lower nice value  → Higher scheduling preference
    Higher nice value → Lower scheduling preference

---

# 7. 🚀 nice Command

The `nice` command is used to **start a new process with a specific nice value**.

### Syntax

    nice -n <nice_value> <command>

### Example

    nice -n 10 sleep 1000

This starts:

    sleep 1000

with a nice value of:

    10

---

# 8. 🔍 Verify Nice Value

Start a process in the background:

    nice -n 10 sleep 1000 &

Find the PID:

    pgrep sleep

Then check its nice value:

    ps -o pid,ni,pri,stat,cmd -p <PID>

Example:

    PID   NI   PRI   STAT   CMD
    1234  10   ...   S      sleep 1000

The exact `PRI` value can depend on the scheduler and system configuration.

For this exercise, focus mainly on the `NI` column.

---

# 9. 🔄 renice Command

The `renice` command is used to **change the nice value of an existing process**.

### Syntax

    renice <nice_value> -p <PID>

Example:

    renice 15 -p 1234

This changes the nice value of process `1234` to:

    15

---

# 10. 🧪 Practical Example Using renice

## Step 1: Start a Background Process

    sleep 1000 &

Example output:

    [1] 1234

Here:

    1    → Job ID
    1234 → PID

---

## Step 2: Check Nice Value

    ps -o pid,ni,pri,stat,cmd -p 1234

Example:

    PID   NI   PRI   STAT   CMD
    1234   0   ...   S      sleep 1000

---

## Step 3: Change Nice Value

    renice 15 -p 1234

---

## Step 4: Verify Again

    ps -o pid,ni,pri,stat,cmd -p 1234

Now the `NI` value should be:

    15

---

## Step 5: Monitor Using top

    top

Observe:

    PR
    NI
    %CPU

---

# 11. 🔐 Negative Nice Values

Negative nice values increase scheduling preference.

For example:

    sudo nice -n -10 sleep 1000

For an existing process:

    sudo renice -10 -p <PID>

### Important

Negative nice values normally require elevated privileges.

For example:

    nice -n -10 sleep 1000

may result in a permission error when run by a normal user.

Using:

    sudo nice -n -10 sleep 1000

allows an appropriately privileged user to request the negative nice value.

---

# 12. 🧠 Nice Value Rule

Remember:

    Nice Value
        |
        +---- Lower number → Higher scheduling preference
        |
        +---- Higher number → Lower scheduling preference

Example:

    -10 → Higher scheduling preference
      0 → Default
    +10 → Lower scheduling preference
    +19 → Lowest scheduling preference

---

# 13. 📋 Finding Process IDs

Every running process in Linux has a unique **PID (Process ID)**.

We can use different commands to find PIDs.

## List All Processes

    ps -e

This displays processes running on the system.

---

## Find a Process by Name

    pgrep <process_name>

Example:

    pgrep nginx

This displays the PID or PIDs of matching processes.

---

## Find PID and Command

    pgrep -a nginx

This displays matching PIDs along with the command line.

---

## Using ps and grep

    ps -ef | grep nginx

This searches the process list for `nginx`.

> **Note:** `grep` itself may appear in the output because the search command is also a process.

---

# 14. 🆚 pgrep vs ps + grep

| Command | Purpose |
|---|---|
| `pgrep nginx` | Find PID of nginx |
| `pgrep -a nginx` | Find PID and command |
| `ps -ef` | Display processes |
| `ps -ef \| grep nginx` | Search process list for nginx |

### Easy Way to Remember

    pgrep → Find process IDs by name
    ps    → Display process information
    grep  → Filter/search text

---

# 15. 📡 Sending Signals to Processes

Linux processes can receive **signals**.

A signal is a notification sent to a process asking it to perform a particular action.

Signals can be used to:

- Stop a process
- Terminate a process
- Continue a stopped process
- Interrupt a process
- Notify a process about certain events

The command commonly used to send signals is:

    kill

---

# 16. 🔔 Common Linux Signals

| Signal | Number | Purpose |
|---|---:|---|
| `SIGHUP` | 1 | Hangup; behavior depends on application |
| `SIGINT` | 2 | Interrupt |
| `SIGTERM` | 15 | Request graceful termination |
| `SIGSTOP` | 19 | Stop process |
| `SIGCONT` | 18 | Continue stopped process |
| `SIGKILL` | 9 | Forceful termination |
| `SIGTSTP` | 20 | Terminal stop |

---

# 17. 🛑 SIGTERM

`SIGTERM` is signal number:

    15

It requests a process to terminate gracefully.

Command:

    kill -15 <PID>

or simply:

    kill <PID>

By default:

    kill <PID>

sends `SIGTERM`.

### Why Prefer SIGTERM?

The application can potentially:

- Close files
- Finish cleanup
- Close database connections
- Save state
- Shut down gracefully

---

# 18. 💀 SIGKILL

`SIGKILL` is signal number:

    9

Command:

    kill -9 <PID>

This forcefully terminates the process.

### Important

`SIGKILL` cannot be caught or ignored by the target process.

Therefore, do not use it as the first option when a graceful termination is possible.

### Recommended Approach

First:

    kill <PID>

If the process does not terminate and forceful termination is justified:

    kill -9 <PID>

---

# 19. 🧠 SIGTERM vs SIGKILL

| Feature | SIGTERM | SIGKILL |
|---|---|---|
| Number | 15 | 9 |
| Purpose | Graceful termination | Forceful termination |
| Can process handle it? | Yes | No |
| Cleanup possible? | Usually | No |
| Recommended first? | Yes | No |

### Easy Way to Remember

    SIGTERM → "Please stop gracefully."

    SIGKILL → "Stop immediately."

---

# 20. 🧪 Practical Signal Example

### Step 1: Start a Process

    sleep 1000 &

---

### Step 2: Find PID

    pgrep sleep

Suppose PID is:

    1234

---

### Step 3: Send SIGTERM

    kill -15 1234

or:

    kill 1234

---

### Step 4: Check Process

    ps -p 1234

If the process has exited, it should no longer appear.

---

# 21. ⏸️ Stopping and Continuing Processes

We can stop and resume processes using signals.

### Stop

    kill -STOP <PID>

### Continue

    kill -CONT <PID>

Example:

    sleep 1000 &

Find PID:

    pgrep sleep

Stop:

    kill -STOP <PID>

Continue:

    kill -CONT <PID>

---

# 22. 🔄 Process States

Processes can exist in different states.

| State | Code | Meaning |
|---|---|---|
| Running/Runnable | `R` | Running or ready to run |
| Sleeping | `S` | Interruptible sleep |
| Uninterruptible Sleep | `D` | Usually waiting for I/O |
| Zombie | `Z` | Terminated but parent has not collected status |
| Stopped/Traced | `T` | Stopped or being traced |

---

# 23. 🟢 R – Running/Runnable

`R` represents a process that is:

- Currently running on a CPU, or
- Ready to run and waiting for CPU scheduling

Example:

    R

---

# 24. 😴 S – Sleeping

`S` means the process is in **interruptible sleep**.

It may be waiting for:

- Input
- A timer
- Network activity
- Another event

Many normal processes spend a large amount of time in this state.

---

# 25. 💾 D – Uninterruptible Sleep

`D` usually means the process is waiting for an I/O operation.

Examples:

- Disk I/O
- Storage operations
- Certain kernel operations

If a process remains in `D` state for a long time, it may indicate an I/O or storage-related problem.

---

# 26. 🧟 Z – Zombie

`Z` represents a zombie process.

The process has already terminated, but the parent has not yet collected its exit status.

A zombie is not actively executing.

Example:

    Z

---

# 27. ⏸️ T – Stopped

`T` means the process has been stopped or traced.

For example:

    kill -STOP <PID>

can put a process into a stopped state.

---

# 28. 🔍 Viewing Process States

Use:

    ps -e -o pid,stat,cmd

Example output:

    PID    STAT    CMD
    1001   S       bash
    1200   S       sleep 1000
    1300   R       python3 app.py

The `STAT` column shows process state information.

---

# . 🌳 Process Tree

Linux processes have parent-child relationships.

A process can create another process.

For example:

    systemd
       |
       +-- sshd
       |     |
       |     +-- bash
       |           |
       |           +-- vim
       |           |
       |           +-- sleep
       |
       +-- nginx
             |
             +-- worker
             |
             +-- worker

This is called a **process tree**.

---

# 36. 🌳 pstree Command

`pstree` displays processes in a tree structure.

Run:

    pstree

Example:

    systemd
     ├─sshd
     │  └─bash
     │     └─sleep
     └─nginx
        ├─nginx
        └─nginx

This makes parent-child relationships easier to understand.

---

# 37. 🔢 pstree with PIDs

Use:

    pstree -p

This displays processes along with their PIDs.

Example:

    systemd(1)
     ├─sshd(900)
     │  └─bash(1200)
     │     └─sleep(1500)
     └─nginx(2000)
        ├─nginx(2001)
        └─nginx(2002)

---

# 38. 🧠 Why is pstree Useful?

`pstree` can help us understand:

- Which process started another process
- Parent-child relationships
- Process hierarchy
- Services and their child processes
- Troubleshooting process behavior

---

# 39. 🔍 PID + PPID + Process Tree

We can inspect parent-child relationships using:

    ps -e -o pid,ppid,stat,cmd

Example:

    PID    PPID   STAT   CMD
    1000   1      S      sshd
    1200   1000   S      bash
    1500   1200   S      sleep 1000

This means:

    PID 1000
       |
       +-- PID 1200
              |
              +-- PID 1500

Or:

    Parent
       |
       +-- Child
              |
              +-- Child

---

# 40. 🔥 Practical Example: Process Investigation

Suppose a Linux server is slow.

We want to investigate which processes are consuming CPU.

### Step 1: Open top

    top

Look at:

    %CPU
    %MEM
    PID
    NI
    PR

---

### Step 2: Identify the PID

Suppose:

    PID = 1234

---

### Step 3: Inspect the Process

    ps -p 1234 -o pid,ppid,stat,ni,pri,%cpu,%mem,cmd

---

### Step 4: Check Its Parent

Look at:

    PPID

For example:

    PID    PPID
    1234   1000

This means:

    Process 1000
         |
         +-- Process 1234

---

### Step 5: View the Process Tree

    pstree -p

Find the process and examine its parent-child relationship.

---

### Step 6: Check Nice Value

    ps -o pid,ni,pri,cmd -p 1234

---

### Step 7: Change Nice Value if Required

For example:

    sudo renice 10 -p 1234

---

### Step 8: Monitor Again

    top

Observe:

    NI
    PR
    %CPU

---

# 41. 🚀 Real-World DevOps Scenario

Suppose a backup process is consuming a lot of CPU during business hours.

The backup process has:

    PID = 4567

First inspect it:

    ps -p 4567 -o pid,ppid,stat,ni,pri,%cpu,%mem,cmd

Suppose its nice value is:

    NI = 0

We may decide to make it less CPU-favorable:

    sudo renice 10 -p 4567

Then verify:

    ps -o pid,ni,pri,cmd -p 4567

And monitor:

    top

### Result

The backup process now has a higher nice value:

    0 → 10

This gives it a lower scheduling preference among normal processes when there is CPU contention.

---

# 43. 🛠️ Useful Commands

| Command | Purpose |
|---|---|
| `ps -e` | List processes |
| `ps -ef` | Full process listing |
| `ps -p PID` | Show a specific process |
| `ps -o pid,ni,pri,cmd -p PID` | Show PID, nice value, priority, command |
| `top` | Real-time process monitoring |
| `htop` | Interactive process monitoring |
| `pgrep name` | Find process IDs by name |
| `kill PID` | Send SIGTERM |
| `kill -9 PID` | Send SIGKILL |
| `kill -STOP PID` | Stop a process |
| `kill -CONT PID` | Continue a stopped process |
| `nice -n 10 command` | Start command with nice value |
| `renice 10 -p PID` | Change nice value |
| `jobs` | List shell jobs |
| `fg %1` | Bring job to foreground |
| `bg %1` | Resume job in background |
| `pstree` | Display process tree |
| `pstree -p` | Display process tree with PIDs |

---

# . 🚀 Important Commands to Remember

## View Processes

    ps -e
    ps -ef

## Find Process

    pgrep nginx
    pgrep -a nginx

## Monitor Processes

    top
    htop

## Start Process with Nice Value

    nice -n 10 sleep 1000

## Change Nice Value of Existing Process

    renice 10 -p <PID>

## Check Priority and Nice Value

    ps -o pid,ni,pri,stat,cmd -p <PID>

## Graceful Termination

    kill <PID>

## Forceful Termination

    kill -9 <PID>

## Stop Process

    kill -STOP <PID>

## Continue Process

    kill -CONT <PID>

## View Jobs

    jobs

## Foreground

    fg %1

## Background

    bg %1

## Process Tree

    pstree

## Process Tree with PIDs

    pstree -p

---

# 💡 Remember

| Command | Remember It As |
|---|---|
| `nice` | Start a new process with a nice value |
| `renice` | Change nice value of an existing process |
| `kill` | Send a signal to a process |
| `ps` | View process information |
| `top` | Monitor processes in real time |
| `pgrep` | Find process IDs |
| `pstree` | Understand parent-child process relationships |
| `jobs` | View shell jobs |
| `fg` | Bring job to foreground |
| `bg` | Run/resume job in background |

---
