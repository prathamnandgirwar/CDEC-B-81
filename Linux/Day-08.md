# Day 8: The Editor's Lair  
## Mastering Text Editing with VIM

---

## Entering Execute Mode

Execute Mode allows you to run commands for file operations, searching, and other advanced functionalities.

To enter Execute Mode, press:

:

---

## Practical

### Open Vim
vim example.txt

### Enter Execute Mode and save the file
:w

### Quit Vim
:q

### Combine commands to save and quit
:wq

---

## Executing Basic Commands: File Operations, Searching, Line Numbering

### File Operations

Save the file:
:w

Save as a new file:
:w newfile.txt

Quit Vim:
:q

Force quit without saving:
:q!

---

### Line Numbering

Show line numbers:
:set number

Hide line numbers:
:set nonumber

---

## Practical

Search for the term "example" in a file:
(example search command)
/example

Enable line numbering and locate specific lines using line numbers.

---

## Entering Visual Mode

Visual Mode allows for text selection and manipulation.

### Visual Mode Types

Character-wise selection:
v

Line-wise selection:
V

Block selection:
Ctrl + v

---

## Practical

1. Open a file in Vim
2. Use `v` to select a word or character sequence
3. Use `V` to select a full line
4. Use `Ctrl + v` to select a rectangular block of text

---

## Manipulating Text in Visual Mode

Once text is selected in Visual Mode, you can manipulate it using the following commands:

Copy text:
y

Delete text:
d

Paste text:
p

Replace selected text:
1. Select the text
2. Press `c` to cut and enter Insert Mode
3. Type the replacement text
4. Press `Esc`

---

## Summary

- `:` → Execute Mode  
- `v / V / Ctrl + v` → Visual Mode  
- `y, d, p, c` → Text manipulation  
- `:w`, `:q`, `:wq` → File operations  

---

Mastering Vim improves speed, efficiency, and control while working on Linux systems.
