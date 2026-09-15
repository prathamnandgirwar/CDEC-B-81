# 🐧 Day 4: Linux Commands & Command Line Basics

> 🎯 **Goal:** Learn how to navigate Linux using the command line and perform basic file and directory operations.

---

# 💻 What is a Command?

A **command** is an instruction that we give to the Linux Operating System to perform a specific task.

Just like we give instructions to a person, we give instructions to Linux using commands.

### Examples

- Display the current directory
- Create a folder
- Create a file
- Restart the system
- View system information

> 💡 **Remember:** Linux is case-sensitive. For example, `ls` and `LS` are treated as different commands.

---

# 🖥️ What is the Linux Terminal?

The **Terminal** is a text-based interface used to interact with the Linux operating system.

Instead of clicking icons, we type commands to perform tasks.

Example:

```bash
pwd
ls
mkdir DevOps
```

---

# 📝 Understanding the Linux Prompt

Whenever you open the terminal, you will see something like this:

```bash
[root@localhost ~]#
```

Let's understand each part.

| Part | Meaning |
|------|---------|
| **root** | Current logged-in user |
| **localhost** | Hostname (Computer Name) |
| **~** | Current working directory (Home Directory) |
| **#** | Root (Administrator) user |

---

## 👤 Local User Prompt

```bash
labex@ubuntu:~$
```

| Symbol | Meaning |
|---------|---------|
| **$** | Normal (Local) User |
| **#** | Root (Administrator) User |

> 💡 **Tip:** Be careful while working as the **root user** because it has permission to modify or delete any file in the system.

---

# 🖥️ Command Syntax

Most Linux commands follow this format:

```text
command [options] [arguments]
```

### Example

```bash
ls -l /home
```
---

# 📚 Commands Covered Today

## 📂 Navigation Commands

| Command | Description |
|---------|-------------|
| `pwd` | Displays the **Present Working Directory** (current location). |
| `ls` | Lists files and directories. |
| `ll` | Displays files and directories in **long listing format**. |
| `cd <directory>` | Changes the current directory. |
| `cd ..` | Moves **one directory back** (parent directory). |
| `cd ~` | Moves to the **Home Directory** of the current user. |
| `clear` | Clears the terminal screen. |

---

## 📁 File & Directory Commands

| Command | Description |
|---------|-------------|
| `touch <file>` | Creates a new empty file. |
| `mkdir <directory>` | Creates a new directory (folder). |

---

## 🔐 User Commands

| Command | Description |
|---------|-------------|
| `logout` | Logs out from the current user session. |
| `exit` | Closes the current terminal session. |
| `Ctrl + D` | Shortcut to exit the current terminal session. |
| `sudo -i` | Switches to the **root (administrator)** user. |
| `sudo ls` | Runs the `ls` command with administrator privileges. |

---

## ⚙️ System Commands

| Command | Description |
|---------|-------------|
| `date` | Displays the current system date and time. |
| `cal` | Displays the calendar of the current month. |
| `hostname` | Displays the system's hostname (computer name). |
| `shutdown` | Safely shuts down the system. |
| `shutdown -h now` | Immediately shuts down and powers off the system. |
| `reboot` | Restarts the system. |
| `init 6` | Restarts the system (legacy command). |

---

## 🖥️ System Information Commands

| Command | Description |
|---------|-------------|
| `hostnamectl` | Displays detailed system and hostname information. |
| `uname -a` | Displays kernel and operating system information. |
| `free -h` | Displays memory (RAM) usage in human-readable format. |
| `lsusb` | Lists all connected USB devices. |
| `lscpu` | Displays detailed CPU information. |
| `dmidecode` | Displays hardware information such as BIOS, RAM, and motherboard details (requires root access). |

---

## ❓ Help Commands

| Command | Description |
|---------|-------------|
| `man <command>` | Displays the complete manual page for a command. |
| `info <command>` | Displays detailed documentation for a command (alternative to `man`). |
| `whatis <command>` | Displays a one-line description of a command. |
| `<command> --help` | Displays a short help message with available options. |
| `which <command>` | Shows the path of the executable command. |
| `whereis <command>` | Shows the locations of the command, source code, and manual pages. |
