# 📘 Day 10: Advanced User & Group Management in Linux

## 🎯 Learning Objectives

By the end of this session, you will be able to:

- Understand the importance of password security.
- Manage user passwords using the `passwd` command.
- Lock and unlock user accounts.
- Force users to change passwords.
- Understand the `/etc/shadow` file.
- Manage password aging using `chage`.
- Learn Primary and Secondary Groups.
- Create, modify, and delete groups.
- Manage group memberships.
- Verify user and group information.

---

# 🔒 Why is Password Security Important?

Passwords are the **first line of defense** for any Linux system.

Imagine a company server where multiple employees log in every day.

If a password is weak:

- Someone can guess it.
- Hackers may gain unauthorized access.
- Important company data can be stolen.
- Entire servers may be compromised.

A strong password greatly improves system security.

---

# ✅ Best Practices for Strong Passwords

✔ Use at least **8–12 characters**

✔ Include:

- Uppercase letters (A-Z)
- Lowercase letters (a-z)
- Numbers (0-9)
- Special characters (@ # $ % & *)

✔ Avoid using:

- Your name
- Mobile number
- Birth date
- "password123"

✔ Change passwords periodically.

✔ Never share your password.

---

# 🔑 The `passwd` Command

The **`passwd`** command is used to:

- Set a password
- Change a password
- Lock a user account
- Unlock a user account
- Force password reset

---

## Syntax

```bash
passwd [OPTIONS] username
```

If no username is provided, it changes the password of the currently logged-in user.

---

# Change Your Own Password

```bash
passwd
```

Example

```
Changing password for user ubuntu.

Current password:
New password:
Retype new password:

passwd: password updated successfully
```

---

# Change Another User's Password

Only the **root user** or a user with **sudo** privileges can do this.

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

# 🔒 Lock a User Account

Sometimes a user should not be allowed to log in temporarily.

Instead of deleting the account, simply lock it.

```bash
sudo passwd -l john
```

Example Output

```
Locking password for user john.
passwd: Success
```

---

# 🔓 Unlock a User Account

Enable login again.

```bash
sudo passwd -u john
```

Example Output

```
Unlocking password for user john.
passwd: Success
```

---

# 🔄 Force Password Change at Next Login

Useful when:

- Creating new employee accounts
- Resetting forgotten passwords
- Improving security

```bash
sudo passwd -e john
```

When John logs in:

```
You are required to change your password immediately.
```

---

# 🔍 Verify if an Account is Locked

Check the user's entry in the **`/etc/shadow`** file.

```bash
sudo grep john /etc/shadow
```

Example Output

```
john:!$6$YH3...
```

If the encrypted password starts with **`!`**, the account is locked.

---

# 📄 Understanding `/etc/shadow`

The **`/etc/shadow`** file stores:

- Encrypted passwords
- Password expiry information
- Password aging policies

Only the **root user** can read this file.

View it using:

```bash
sudo cat /etc/shadow
```

---

# Format of `/etc/shadow`

Example

```
john:$6$abc123...:20230:0:90:7:30:20300
```

| Field | Description |
|--------|-------------|
| Username | Login name |
| Password | Encrypted password |
| Last Change | Days since password was changed |
| Min Days | Minimum days before password can be changed |
| Max Days | Maximum password validity |
| Warning | Days before password expiry warning |
| Inactive | Days after expiry before account is disabled |
| Expire | Account expiration date |

---

# Meaning of Special Password Symbols

| Symbol | Meaning |
|----------|---------|
| `!` | Account is locked |
| `*` | Login disabled |
| `$6$` | SHA-512 encrypted password |

---

# 🔒 Account Lock vs Password Expiry

## Account Lock

The user **cannot log in** until the account is unlocked.

Example

```bash
sudo passwd -l john
```

---

## Password Expiry

The user **must create a new password** before continuing.

Example

```bash
sudo passwd -e john
```

---

# 📅 The `chage` Command

The **`chage`** command manages:

- Password aging
- Password expiry
- Account expiry

---

## Syntax

```bash
chage [OPTIONS] username
```

---

# View Password Aging Information

```bash
sudo chage -l john
```

Example Output

```
Last password change
Password expires
Password inactive
Account expires
Minimum days
Maximum days
Warning days
```

---

# Set Maximum Password Age

Require the user to change the password every **90 days**.

```bash
sudo chage -M 90 john
```

---

# Set Minimum Password Age

Prevent password changes for **7 days**.

```bash
sudo chage -m 7 john
```

---

# Set Warning Days

Warn the user **7 days before** password expiry.

```bash
sudo chage -W 7 john
```

---

# Force Password Change on Next Login

```bash
sudo chage -d 0 john
```

---

# Set Account Expiration Date

Disable the account after a specific date.

```bash
sudo chage -E 2026-12-31 john
```

---

# 👥 Linux Groups

A **Group** is a collection of users.

Instead of assigning permissions to every user individually, Linux allows permissions to be assigned to groups.

Example

```
Developers
Admins
QA
HR
Finance
```

---

# Types of Groups

## 1️⃣ Primary Group

Every user has **one Primary Group**.

- Created automatically when the user is created.
- Files created by the user belong to this group by default.

Example

```
User : john
Primary Group : john
```

---

## 2️⃣ Secondary Group

A user can belong to **multiple Secondary Groups**.

Used to provide additional permissions.

Example

```
User : john

Primary Group

john

Secondary Groups

developers
docker
sudo
```

---

# 📄 Understanding `/etc/group`

This file stores group information.

View it:

```bash
cat /etc/group
```

Example Entry

```
developers:x:1002:john,alice,bob
```

| Field | Description |
|--------|-------------|
| Group Name | developers |
| Password Placeholder | x |
| Group ID (GID) | 1002 |
| Members | john, alice, bob |

---

# 📄 Understanding `/etc/gshadow`

Stores secure group information.

View it:

```bash
sudo cat /etc/gshadow
```

Example Entry

```
developers:!::john,alice,bob
```

| Field | Description |
|--------|-------------|
| Group Name | developers |
| Group Password | Encrypted (rarely used) |
| Group Admins | Group administrators |
| Members | Regular members |

---

# ➕ Create a Group

```bash
sudo groupadd developers
```

---

# 🗑 Delete a Group

```bash
sudo groupdel developers
```

---

# ✏ Rename a Group

```bash
sudo groupmod -n dev_team developers
```

---

# 🔢 Change Group ID (GID)

```bash
sudo groupmod -g 2001 dev_team
```

---

# ➕ Add a User to a Group

```bash
sudo usermod -aG developers john
```

> **Note:** Always use `-aG`. Without `-a`, the user may be removed from existing supplementary groups.

---

# ➖ Remove a User from a Group

```bash
sudo gpasswd -d john developers
```

---

# 👀 View User Group Membership

```bash
groups john
```

Example Output

```
john : john developers docker
```

---

# 📋 View All Groups

```bash
cat /etc/group
```

---

# 🧪 Hands-on Lab

## Step 1: Create a User

```bash
sudo useradd -m -s /bin/bash john
sudo passwd john
```

---

## Step 2: Lock the Account

```bash
sudo passwd -l john
```

Verify:

```bash
sudo grep john /etc/shadow
```

---

## Step 3: Unlock the Account

```bash
sudo passwd -u john
```

---

## Step 4: View Password Aging

```bash
sudo chage -l john
```

---

## Step 5: Force Password Change

```bash
sudo chage -d 0 john
```

---

## Step 6: Create a Group

```bash
sudo groupadd developers
```

---

## Step 7: Add User to Group

```bash
sudo usermod -aG developers john
```

---

## Step 8: Verify Membership

```bash
groups john
```

---

## Step 9: Rename the Group

```bash
sudo groupmod -n dev_team developers
```

---

## Step 10: Remove User from Group

```bash
sudo gpasswd -d john dev_team
```

---

## Step 11: Delete the Group

```bash
sudo groupdel dev_team
```

---

# 📊 Difference Between `passwd` and `chage`

| Feature | `passwd` | `chage` |
|----------|----------|----------|
| Change password | ✅ | ❌ |
| Lock account | ✅ | ❌ |
| Unlock account | ✅ | ❌ |
| Force password reset | ✅ | ✅ (`-d 0`) |
| Password aging | ❌ | ✅ |
| Password expiry | ❌ | ✅ |
| Account expiry | ❌ | ✅ |

---

# 📌 Summary

| Command | Purpose |
|----------|---------|
| `passwd` | Change user password |
| `passwd -l` | Lock a user account |
| `passwd -u` | Unlock a user account |
| `passwd -e` | Expire password immediately |
| `chage -l` | View password aging information |
| `chage -M` | Set maximum password age |
| `chage -m` | Set minimum password age |
| `chage -W` | Set password expiry warning days |
| `chage -d 0` | Force password change at next login |
| `chage -E` | Set account expiry date |
| `groupadd` | Create a group |
| `groupdel` | Delete a group |
| `groupmod` | Modify group name or GID |
| `usermod -aG` | Add user to a supplementary group |
| `gpasswd -d` | Remove user from a group |
| `groups` | Display a user's group memberships |
| `cat /etc/group` | View all groups |
| `cat /etc/gshadow` | View secure group information (root only) |

---
