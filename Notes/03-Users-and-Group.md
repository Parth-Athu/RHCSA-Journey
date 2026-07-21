# Chapter 3: Users, Groups & Password Management

> **Objective:** Learn Linux user management, groups, password policies, user account administration, and password aging using practical commands.

---

# Table of Contents

1. Introduction
2. Types of Linux Users
3. User Identification Number (UID)
4. Group Identification Number (GID)
5. User Information (`/etc/passwd`)
6. Group Information (`/etc/group`)
7. Password Information (`/etc/shadow`)
8. Creating Users
9. Setting Passwords
10. Modifying Users
11. Groups
12. Password Aging Policy
13. Managing Password Policy (`chage`)
14. Default Password Policy (`/etc/login.defs`)
15. Practice Tasks
16. RHCSA Exam Tips
17. Interview Questions
18. Common Mistakes
19. Quick Revision
20. Summary
21. Key Takeaways

---

# Introduction

Linux is a **multi-user operating system**, allowing multiple users to access and work on the same system simultaneously.

Each user has a unique identity, permissions, and home directory.

Managing users and groups is one of the most important responsibilities of a Linux System Administrator.

---

# Types of Linux Users

Linux supports three types of users.

## 1. Super User (Root)

The **root** user is the administrator of the Linux system.

Features

- Full administrative privileges
- Can create and delete users
- Can install software
- Can modify system configurations
- Can access all files and directories

Username

```text
root
```

UID

```text
0
```

---

## 2. Regular User (Local User)

Regular users are created for everyday work.

Examples

```text
parth

student

john
```

Features

- Limited permissions
- Personal home directory
- Cannot modify critical system files

Default UID Range

```text
1000 - 60000
```

---

## 3. System User

System users are automatically created for services.

Examples

```text
apache

mysql

sshd

nobody
```

These accounts generally cannot log in.

UID Range

```text
1 - 999
```

---

# User Identification Number (UID)

Each Linux user has a unique User ID (UID).

Linux internally identifies users by UID rather than username.

| UID | User Type |
|------|-----------|
| 0 | Root |
| 1–999 | System Users |
| 1000–60000 | Regular Users |

---

# Group Identification Number (GID)

Every group has a unique Group ID (GID).

Groups simplify permission management by allowing multiple users to share the same permissions.

---

# User Information

Linux stores user account information in

```text
/etc/passwd
```

View users

```bash
cat /etc/passwd
```

Example

```text
root:x:0:0:root:/root:/bin/bash
```

Meaning

| Field | Description |
|---------|-------------|
| root | Username |
| x | Password placeholder |
| 0 | UID |
| 0 | GID |
| root | User description |
| /root | Home Directory |
| /bin/bash | Default Login Shell |

---

# Group Information

Group details are stored in

```text
/etc/group
```

View groups

```bash
cat /etc/group
```

---

# Password Information

Encrypted passwords are stored in

```text
/etc/shadow
```

Only the **root user** can read this file.

View

```bash
cat /etc/shadow
```

Example

```text
root:$6$.....:19130:0:99999:7:::
```

---

# Understanding /etc/shadow

| Field | Description |
|---------|-------------|
| Username | Login name |
| Encrypted Password | SHA-512 encrypted password |
| Last Password Change | Days since 1 Jan 1970 |
| Minimum Password Age | Minimum days before changing password |
| Maximum Password Age | Password validity |
| Warning Days | Password expiry warning |
| Inactive Days | Grace period after expiry |
| Expiry Date | Account expiration date |

---

# Creating Users

Syntax

```bash
useradd username
```

Example

```bash
useradd test1
```

Specify UID

```bash
useradd -u 3000 test1
```

Verify

```bash
id test1
```

---

# Setting Passwords

Syntax

```bash
passwd username
```

Example

```bash
passwd test1
```

---

# Modifying Users

The **usermod** command modifies an existing user.

Syntax

```bash
usermod [options] username
```

Examples

Change shell

```bash
usermod -s /bin/bash test1
```

Change home directory

```bash
usermod -d /home/test1 test1
```

Lock account

```bash
usermod -L test1
```

Unlock account

```bash
usermod -U test1
```

---

# Groups

Linux supports two types of groups.

## Primary Group

Every user has one primary group.

Example

```
test1
```

---

## Secondary Group

A user may belong to multiple secondary groups.

Examples

```
developers

docker

wheel
```

---

# Password Aging Policy

Password aging improves account security.

### Last Password Change (-d)

Days since **1 January 1970**.

---

### Minimum Password Age (-m)

Minimum days before changing password.

Example

```
0
```

Meaning

User can change password anytime.

---

### Maximum Password Age (-M)

Maximum number of days the password remains valid.

Example

```
30
```

---

### Warning Days (-W)

Number of days before expiry when Linux warns the user.

Example

```
7
```

---

### Inactive Days (-I)

Grace period after password expiration.

Example

```
5
```

---

### Account Expiry (-E)

Account expiration date.

Format

```text
YYYY-MM-DD
```

Example

```
2026-12-31
```

---

# Managing Password Policy

Linux uses the **chage** command.

Display password information

```bash
chage -l test1
```

Force password change at next login

```bash
chage -d 0 test1
```

Set minimum password age

```bash
chage -m 2 test1
```

Set maximum password age

```bash
chage -M 30 test1
```

Set warning period

```bash
chage -W 7 test1
```

Set inactive period

```bash
chage -I 5 test1
```

Set account expiry

```bash
chage -E 2026-12-31 test1
```

---

# Default Password Policy

Linux applies default password settings from

```text
/etc/login.defs
```

View

```bash
cat /etc/login.defs
```

This file controls

- Default UID range
- Password expiration
- Password aging
- Warning period
- Home directory creation

---

# Practice Tasks

### Task 1

Create user

```bash
useradd -u 3000 test1
```

---

### Task 2

Assign password

```bash
passwd test1
```

---

### Task 3

Check user information

```bash
id test1
```

---

### Task 4

Display all users

```bash
cat /etc/passwd
```

---

### Task 5

Display groups

```bash
cat /etc/group
```

---

### Task 6

Display password policy

```bash
chage -l test1
```

---

### Task 7

Force password change

```bash
chage -d 0 test1
```

---

### Task 8

Set password aging

```bash
chage -m 2 test1

chage -M 30 test1

chage -W 7 test1

chage -I 5 test1
```

---

# RHCSA Exam Tips

📌 Root UID = **0**

📌 `/etc/passwd` → User Information

📌 `/etc/group` → Group Information

📌 `/etc/shadow` → Password Information

📌 `/etc/login.defs` → Default Password Policy

📌 `id` → Display User Information

📌 `passwd` → Set Password

📌 `chage` → Manage Password Aging

---

# Interview Questions

### What is UID?

User Identification Number.

---

### What is GID?

Group Identification Number.

---

### Which file stores encrypted passwords?

```
/etc/shadow
```

---

### Which command creates a user?

```bash
useradd
```

---

### Which command changes a password?

```bash
passwd
```

---

### Which command displays password aging?

```bash
chage -l
```

---

### Which file controls default password policy?

```
/etc/login.defs
```

---

# Common Mistakes

❌ Creating users without passwords.

❌ Confusing UID with GID.

❌ Editing `/etc/passwd` manually.

❌ Sharing the `/etc/shadow` file.

❌ Forgetting to verify users with `id`.

---

# Quick Revision

```bash
cat /etc/passwd

cat /etc/group

cat /etc/shadow

id test1

useradd test1

useradd -u 3000 test1

passwd test1

usermod -L test1

usermod -U test1

chage -l test1

chage -d 0 test1

cat /etc/login.defs
```

---

# Summary

In this chapter, I learned

- Linux User Types
- UID and GID
- `/etc/passwd`
- `/etc/group`
- `/etc/shadow`
- User Management
- Group Management
- Password Management
- Password Aging
- `chage`
- `/etc/login.defs`

---

# Key Takeaways

✅ Linux is a multi-user operating system.

✅ Every user has a unique UID.

✅ Root always has UID 0.

✅ `/etc/passwd` stores user information.

✅ `/etc/group` stores group information.

✅ `/etc/shadow` stores encrypted passwords.

✅ `useradd` creates users.

✅ `passwd` assigns passwords.

✅ `usermod` modifies existing users.

✅ `chage` manages password aging policies.

✅ `/etc/login.defs` defines default password settings.