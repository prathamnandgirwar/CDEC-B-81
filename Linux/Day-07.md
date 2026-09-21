# 📝 Day 7: Mastering Text Editing with VIM

![Linux](https://img.shields.io/badge/Linux-Text%20Editor-yellow?logo=linux)
![Vim](https://img.shields.io/badge/Vim-Editor-green?logo=vim)
![CLI](https://img.shields.io/badge/CLI-Terminal-black?logo=gnubash)
![Level](https://img.shields.io/badge/Level-Beginner-blue)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

# 📘 Overview of Vim and Its History

Vim (Vi IMproved) is a powerful and versatile text editor widely used in the Linux ecosystem.

It originated from the **Vi editor** and provides enhanced features like:

- Syntax highlighting
- Plugin support
- Advanced navigation commands
- High customization

---

# ❓ Why Use Vim?

- Lightweight and fast  
- Works in terminal environments (ideal for remote servers)  
- Highly extensible and customizable  

---

# 🛠️ Practical: Check & Install Vim

## 🔍 Check if Vim is installed

```bash
vim --version
```

## 📦 Install Vim (if not installed)

### Debian / Ubuntu
```bash
sudo apt install vim
```

### RHEL / CentOS
```bash
sudo yum install vim
```

---

# 🧠 Basic Concepts: Modes in Vim

Vim operates in multiple modes:

| Mode | Purpose |
|-------|----------|
| Command Mode | Default mode for navigation & commands |
| Insert Mode | For writing/editing text |
| Visual Mode | For selecting text |
| Execute Mode | For running commands using `:` |

---

# 🚀 Practical: Switching Between Modes

Open a file:

```bash
vim example.txt
```

- Starts in **Command Mode**
- Press `i` → Enter **Insert Mode**
- Press `Esc` → Return to **Command Mode**

---

# 🧭 Basic Navigation in Command Mode

Move cursor:

| Key | Direction |
|------|------------|
| h | Left |
| l | Right |
| j | Down |
| k | Up |

---

# 📌 Command Mode (Default Mode)

### 📋 Copy Commands

```
yy      → Copy single line
nyy     → Copy multiple lines
yw      → Copy single word
p       → Paste
```

---

### 🗑️ Delete Commands

```
dd      → Delete single line
ndd     → Delete multiple lines
dw      → Delete single word
```

---

### ✂️ Cut Commands

```
cc      → Cut single line
ncc     → Cut multiple lines
cw      → Cut single word
P       → Paste before cursor
```

---

### ↩️ Undo & Redo

```
u        → Undo
Ctrl + r → Redo
```

---

### 🔝 File Navigation

```
gg   → Top of file
H    → Top of page

G    → Bottom of file
L    → Bottom of page

M    → Middle of page
A    → End of current line
```

---

### 🔎 Search & Jump

```
<n>gg       → Move to nth line
:/<word>    → Search word
```

---

### ✏️ Replace Commands

```
s → Remove current character & enter Insert Mode
S → Remove current line & enter Insert Mode
```

---

# ✍️ Insert Mode (Writable Mode)

(Press `Esc` and then `i` to enter)

| Command | Action |
|----------|---------|
| i | Insert at cursor |
| I | Insert at start of line |
| a | Insert after cursor |
| A | Insert at end of line |
| o | Insert new line below |
| O | Insert new line above |
| r | Replace single character |
| R | Replace multiple characters |

---

# 🎯 Conclusion

Mastering Vim requires:

- Understanding its modes
- Practicing navigation commands
- Memorizing frequently used shortcuts

Experiment with the commands above to build confidence.

---

⭐ The more you practice Vim, the faster and more efficient you become in Linux.
