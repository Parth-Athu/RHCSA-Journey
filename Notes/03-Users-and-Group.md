# Chapter 3: Users and Groups

> **Objective:** Learn about Linux user types, User IDs (UIDs), Group IDs (GIDs), user management, and group management.

---

# Table of Contents

1. Introduction
2. Types of Users
3. User Identification Number (UID)
4. User Information (`/etc/passwd`)
5. Creating Users
6. Setting User Passwords
7. Modifying Users
8. Groups
9. Viewing User Information
10. Practice Tasks
11. Interview Questions
12. Common Mistakes
13. Quick Revision
14. Summary
15. Key Takeaways

---

# Introduction

Linux is a multi-user operating system, meaning multiple users can work on the same system simultaneously.

Each user has a unique identity and specific permissions that determine what they can access or modify.

User and group management is one of the core responsibilities of a Linux System Administrator.

---

# 1. Types of Users

Linux has three main types of users.

## 1. Super User (Root)

The **root** user is the administrator of the Linux system.

Features:

- Full access to the entire system
- Can install software
- Can create or delete users
- Can modify system configurations
- Can access every file and directory

Username:

```text
root
```

UID:

```text
0
```

---

## 2. Regular User (Local User)

A regular user is created for daily work.

Examples:

- parth
- student
- john

Features

- Limited permissions
- Cannot modify system files
- Can access only permitted resources

UID Range

```text
1000 - 60000
```

---

## 3. System User

System users are created automatically by Linux for running services and applications.

Examples

- apache
- mysql
- sshd
- nobody

These users are generally not used for logging in.

UID Range

```text
1 - 999
```

---

# 2. User Identification Number (UID)

Every user has a unique **User Identification Number (UID)**.

Linux uses the UID internally instead of the username.

| UID Range | User Type |
|-----------|-----------|
| 0 | Root User |
| 1 - 999 | System Users |
| 1000 - 60000 | Regular Users |

---

# 3. User Information

Linux stores user information in

```text
/etc/passwd
```

Display its contents

```bash
cat /etc/passwd
```

Example

```text
root:x:0:0:root:/root:/bin/bash
```

Explanation

| Field | Meaning |
|--------|----------|
| root | Username |
| x | Password placeholder |
| 0 | UID |
| 0 | GID |
| root | User description (GECOS) |
| /root | Home Directory |
| /bin/bash | Default Login Shell |

---

# 4. Creating a User

The `useradd` command creates a new user.

## Syntax

```bash
useradd username
```

Example

```bash
useradd test1
```

Verify

```bash
cat /etc/passwd
```

or

```bash
id test1
```

---

# 5. Setting a Password

After creating a user, assign a password.

## Syntax

```bash
passwd username
```

Example

```bash
passwd test1
```

Linux prompts for

```
New Password

Retype Password
```

---

# 6. Usermod Command

`usermod` modifies an existing user account.

## Syntax

```bash
usermod [options] username
```

View available options

```bash
usermod --help
```

Common examples

Change login shell

```bash
usermod -s /bin/bash test1
```

Change home directory

```bash
usermod -d /home/newhome test1
```

Lock a user

```bash
usermod -L test1
```

Unlock a user

```bash
usermod -U test1
```

---

# 7. Groups

A group is a collection of users.

Groups simplify permission management.

Linux stores group information in

```text
/etc/group
```

View groups

```bash
cat /etc/group
```

---

## Primary Group

Every user has exactly one primary group.

It is automatically created when the user is created (unless specified otherwise).

Example

```
test1
```

Primary Group

```
test1
```

---

## Secondary Group

A user can belong to multiple secondary groups.

Example

```
developers

docker

wheel
```

---

# Group ID (GID)

Every group has a unique Group ID.

Example

```bash
cat /etc/group
```

Output

```text
developers:x:1001:
```

---

# 8. Viewing User Information

The `id` command displays information about a user.

## Syntax

```bash
id username
```

Example

```bash
id test1
```

Example Output

```text
uid=3000(test1)
gid=3000(test1)
groups=3000(test1)
```

---

# Practice Tasks

## Task 1

Create a user named

```text
test1
```

Assign UID

```
3000
```

```bash
useradd -u 3000 test1
```

Set password

```bash
passwd test1
```

---

## Task 2

Display information about

```
test1
```

```bash
id test1
```

---

## Task 3

Display all users

```bash
cat /etc/passwd
```

---

## Task 4

Display all groups

```bash
cat /etc/group
```

---

## Task 5

View useradd options

```bash
useradd --help
```

---

# Interview Questions

### What are the three types of users in Linux?

- Root User
- Regular User
- System User

---

### What is UID?

UID (User Identification Number) uniquely identifies every user.

---

### What is the UID of the root user?

```
0
```

---

### Which file stores user information?

```
/etc/passwd
```

---

### Which file stores group information?

```
/etc/group
```

---

### What is the difference between a Primary Group and a Secondary Group?

| Primary Group | Secondary Group |
|---------------|-----------------|
| One per user | Multiple allowed |
| Created automatically | Added manually |

---

### Which command displays user information?

```bash
id
```

---

# Common Mistakes

❌ Creating a user without assigning a password.

❌ Editing `/etc/passwd` manually without understanding its format.

❌ Confusing UID with GID.

❌ Logging in as root for normal tasks.

❌ Forgetting to verify the user using `id`.

---

# Quick Revision

```bash
cat /etc/passwd

cat /etc/group

useradd test1

useradd -u 3000 test1

passwd test1

usermod --help

id

id test1
```

---

# Summary

In this chapter, I learned

- Types of Linux users
- User IDs (UID)
- Group IDs (GID)
- `/etc/passwd`
- `/etc/group`
- Creating users
- Setting passwords
- Modifying users
- Primary and Secondary groups
- Viewing user information

---

# Key Takeaways

✅ Linux supports multiple users.

✅ Every user has a unique UID.

✅ Root always has UID 0.

✅ User information is stored in `/etc/passwd`.

✅ Group information is stored in `/etc/group`.

✅ Use `useradd` to create users.

✅ Use `passwd` to assign passwords.

✅ Use `usermod` to modify existing users.

✅ Use `id` to verify user and group information.