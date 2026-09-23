# 📘 Day 9: Managing Users and Permissions in Linux

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Understand what a user is in Linux.
- Learn different types of users.
- Create, modify, and delete users.
- Manage groups.
- Set user passwords.
- Understand important user-related files.
- Switch between users.
- Verify user and group information.

---

# 🤔 Why Do We Need Users?

Imagine a company where 100 employees use the same Linux server.

Without user accounts:
- Everyone can access everyone else's files.
- Anyone can delete important data.
- No accountability.

With user accounts:
- Every user gets their own workspace.
- Files remain secure.
- Permissions can be controlled.
- Activities can be tracked.

This is why Linux is considered one of the most secure operating systems.

---

# 👤 What is a User?

A **User** is a person (or service) that uses the Linux operating system.

Every user has:

- Username
- Password
- User ID (UID)
- Group ID (GID)
- Home Directory
- Login Shell

Example:

```
Username : john
UID      : 1001
Home     : /home/john
Shell    : /bin/bash
```

---

# 👥 Types of Users in Linux

## 1️⃣ Root User (Super User)

The most powerful user in Linux.

### Features

- Full access to the system
- Can create/delete users
- Can install software
- Can modify any file
- Can shut down the server

Default Details

```
Username : root
UID       : 0
Shell     : /bin/bash
```

---

## 2️⃣ System User

Created automatically while installing Linux or applications.

Used by services like:

- Apache
- MySQL
- Nginx
- Docker
- Jenkins

Characteristics

- Cannot login normally
- Used only by system services
- Limited permissions

Typical Details

```
UID   : 1 - 999
Shell : /sbin/nologin
```

Example

```
mysql
www-data
daemon
```

---

## 3️⃣ Standard User (Normal User)

Created by the administrator.

Used for daily work.

Characteristics

- Limited permissions
- Own home directory
- Can access only permitted files

Typical Details

```
UID   : 1000+
Shell : /bin/bash
```

Example

```
john
rahul
pratham
```

---

# 🧑‍💻 Identify the Current User

Display the currently logged-in user.

```bash
whoami
```

Example Output

```
ubuntu
```

---

# 👀 View All Users

Display all users available in Linux.

```bash
cat /etc/passwd
```

Example Output

```
root:x:0:0:root:/root:/bin/bash
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
```

---

# 📂 Important User & Group Files

| File | Purpose |
|------|----------|
| `/etc/passwd` | Stores user information |
| `/etc/shadow` | Stores encrypted passwords |
| `/etc/group` | Stores group information |
| `/etc/gshadow` | Stores secure group information |

---

# 📄 Files Updated When a User Is Created

Whenever a new user is created, Linux automatically updates these files:

## 1. `/etc/passwd`

Stores:

- Username
- UID
- GID
- Home directory
- Shell

---

## 2. `/etc/shadow`

Stores:

- Encrypted password
- Password expiry
- Password aging policies

---

## 3. `/etc/group`

Stores:

- Group names
- Group IDs
- Group members

---

## 4. `/etc/gshadow`

Stores:

- Group password
- Secure group membership

---

## 5. Home Directory

Created inside:

```
/home/username
```

Example

```
/home/john
```

---

## 6. Mailbox

Created inside

```
/var/spool/mail/
```

---

## 7. Skeleton Files

Default files are copied from:

```
/etc/skel
```

---

# 🗂 Skeleton Files

Skeleton files are default configuration files copied into every new user's home directory.

Check skeleton files:

```bash
ls -la /etc/skel
```

Typical Output

```
.bash_logout
.bash_profile
.bashrc
```

---

## `.bash_logout`

Runs when the user logs out.

Example use:

- Cleanup
- Remove temporary files

---

## `.bash_profile`

Runs only once after login.

Usually used for:

- Environment variables
- PATH
- Startup scripts

---

## `.bashrc`

Runs every time a new terminal opens.

Usually contains:

- Aliases
- Prompt customization
- Functions

---

## `.bash_history`

Stores command history.

Example:

```bash
history
```

Location

```
~/.bash_history
```

> **Note:** This file is created automatically after the user starts using the shell. It is **not** copied from `/etc/skel`.

---

# ➕ Create a New User

Syntax

```bash
sudo useradd [options] username
```

Common Options

| Option | Description |
|---------|-------------|
| `-m` | Create home directory |
| `-s` | Specify login shell |
| `-G` | Add to supplementary groups |

Example

```bash
sudo useradd -m -s /bin/bash john
```

---

# ✅ Verify User

```bash
id john
```

Example Output

```
uid=1001(john)
gid=1001(john)
groups=1001(john)
```

---

# 🔑 Set User Password

```bash
sudo passwd john
```

Example

```
New password:
Retype new password:
passwd: password updated successfully
```

---

# 🔄 Switch User

Login as another user.

```bash
su - john
```

Check current user:

```bash
whoami
```

Exit:

```bash
exit
```

---

# 📄 Understanding `/etc/passwd`

Example Entry

```
john:x:1001:1001:John:/home/john:/bin/bash
```

| Field | Meaning |
|--------|----------|
| john | Username |
| x | Password stored in `/etc/shadow` |
| 1001 | User ID (UID) |
| 1001 | Group ID (GID) |
| John | Comment (GECOS) |
| /home/john | Home Directory |
| /bin/bash | Login Shell |

---

# 👥 Group Management

A **Group** is a collection of users.

Instead of giving permissions to each user individually, permissions can be assigned to the group.

Example:

```
Developers
Admins
QA
HR
```

---

# ➕ Create a Group

```bash
sudo groupadd developers
```

---

# ➕ Add User to a Group

```bash
sudo usermod -aG developers john
```

> **Note:** Always use `-aG`. Without `-a`, the user may be removed from existing supplementary groups.

---

# 👀 Check User Groups

```bash
groups john
```

Example Output

```
john developers
```

---

# Verify Group

```bash
cat /etc/group | grep developers
```

---

# 🗑 Remove User

Delete only the user account:

```bash
sudo userdel john
```

---

Delete user along with the home directory:

```bash
sudo userdel -r john
```

---

# 📂 Check User Home Directories

List all home directories:

```bash
ls /home
```

View a specific user's home directory:

```bash
sudo ls /home/john
```

---

# 🔄 Switching Between Users

Login without loading the user's environment:

```bash
su john
```

Login with the user's environment:

```bash
su - john
```

Exit the current session:

```bash
exit
```

---

# 📌 Summary

| Command | Purpose |
|----------|---------|
| `whoami` | Show current user |
| `cat /etc/passwd` | List all users |
| `useradd` | Create a user |
| `passwd` | Set/change password |
| `id` | Display user information |
| `su - username` | Switch user |
| `groupadd` | Create a group |
| `usermod -aG` | Add user to a group |
| `groups` | Show group membership |
| `userdel` | Delete a user |
| `userdel -r` | Delete user and home directory |
| `sudo -i` | Switch to root |
| `sudo -l` | View sudo permissions |

---

# 🧪 Hands-on Lab

### Step 1: Create a User

```bash
sudo useradd -m -s /bin/bash john
```

---

### Step 2: Set Password

```bash
sudo passwd john
```

---

### Step 3: Verify User

```bash
id john
```

---

### Step 4: Switch User

```bash
su - john
whoami
exit
```

---

### Step 5: Create a Group

```bash
sudo groupadd developers
```

---

### Step 6: Add User to Group

```bash
sudo usermod -aG developers john
```

---

### Step 7: Verify Group Membership

```bash
groups john
```

---

### Step 8: Verify Group Entry

```bash
cat /etc/group | grep developers
```

---

### Step 9: View Home Directory

```bash
ls /home
sudo ls /home/john
```

---

### Step 10: Remove User

```bash
sudo userdel -r john
```

---

# 🎯 Key Takeaways

- Linux is a multi-user operating system.
- Every user has a unique UID.
- Root user has unrestricted access.
- System users run background services.
- Standard users perform daily tasks.
- Groups simplify permission management.
- User details are stored in `/etc/passwd`.
- Passwords are stored securely in `/etc/shadow`.
- Default user configuration comes from `/etc/skel`.
- Use `sudo` carefully, as it grants administrative privileges.
