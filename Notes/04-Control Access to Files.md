# 📂 Chapter 4: Control Access to Files

> **Objective:** Learn Linux file permissions, ownership, special permissions (SUID, SGID, Sticky Bit), and default permissions using `umask`.

---

# 📚 Table of Contents

1. Access Control Mechanisms
2. Linux Permissions
3. Basic Permissions
4. File vs Directory Permissions
5. Changing Permissions (`chmod`)
6. Permission Methods
7. File Ownership
8. Changing Ownership (`chown` & `chgrp`)
9. Special Permissions
10. Default Permissions (`umask`)
11. Practice Tasks
12. RHCSA Exam Tips
13. Interview Questions
14. Quick Revision

---

# 🔐 Access Control Mechanisms

Linux provides two mechanisms to control access to resources.

## 1. DAC (Discretionary Access Control)

DAC allows the **owner** of a file or directory to decide who can access it.

The owner controls permissions using Linux file permissions.

Example:

- Read
- Write
- Execute

---

## 2. MAC (Mandatory Access Control)

MAC controls how processes access system resources.

In Red Hat Enterprise Linux, this is implemented using **SELinux (Security-Enhanced Linux)**.

Unlike DAC, MAC policies are enforced by the operating system.

---

# 🔑 Linux Permissions

Every file and directory has three permission levels.

```text
rw-   r--   r--
│      │      │
│      │      └── Others (o)
│      └───────── Group (g)
└──────────────── User / Owner (u)
```

| Symbol | Meaning |
|---------|---------|
| u | User (Owner) |
| g | Group |
| o | Others |

---

# 📖 Basic Permissions

| Permission | Symbol | Value | File | Directory |
|------------|--------|------:|------|-----------|
| Read | r | 4 | View file contents | List directory contents |
| Write | w | 2 | Modify file | Create/Delete files inside the directory |
| Execute | x | 1 | Execute a program/script | Enter (access) the directory |

---

# 📂 File vs Directory Permissions

| Permission | File | Directory |
|------------|------|-----------|
| Read | View file contents | List files |
| Write | Modify file | Create/Delete files |
| Execute | Run program | Enter the directory |

---

# 🔧 Changing Permissions

Linux uses the **chmod** command.

**chmod** = Change Mode

## Syntax

```bash
chmod [permissions] file
```

---

# Method 1: Symbolic Method

Uses symbols such as:

| Symbol | Meaning |
|---------|---------|
| u | User |
| g | Group |
| o | Others |
| + | Add permission |
| - | Remove permission |
| = | Assign exact permission |

Examples

Remove execute permission from user

```bash
chmod u-x file1
```

Remove write permission from group

```bash
chmod g-w file1
```

Remove read permission from others

```bash
chmod o-r file1
```

Assign exact permissions

```bash
chmod u=r--,g=rw-,o=r-- file1
```

---

# Method 2: Octal (Numeric) Method

Permission values

| Permission | Value |
|------------|------:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Common combinations

| Number | Permission |
|--------:|------------|
| 0 | --- |
| 1 | --x |
| 2 | -w- |
| 3 | -wx |
| 4 | r-- |
| 5 | r-x |
| 6 | rw- |
| 7 | rwx |

Examples

```bash
chmod 674 file1
```

Permission

```text
User    → rw-
Group   → rwx
Others  → r--
```

---

```bash
chmod 755 file2
```

Permission

```text
User    → rwx
Group   → r-x
Others  → r-x
```

---

```bash
chmod 643 file3
```

Permission

```text
User    → rw-
Group   → r--
Others  → -wx
```

---

Example

```text
r-x   -wx   r--
```

Numeric

```text
5     3     4
```

Command

```bash
chmod 534 file4
```

---

# 👤 File Ownership

Every file has two ownerships.

## 1. User Ownership

Represents the owner of the file.

---

## 2. Group Ownership

Represents the group assigned to the file.

View ownership

```bash
ls -l
```

---

# 🔄 Changing Ownership

## Change User Ownership

```bash
chown username file
```

Example

```bash
chown student file1
```

---

## Change Group Ownership

Method 1

```bash
chown :developers file1
```

Method 2

```bash
chgrp developers file1
```

---

## Change User and Group Together

```bash
chown student:developers file1
```

---

# ⭐ Special Permissions

Linux provides three special permissions.

| Permission | Numeric | Applied On | Purpose |
|------------|---------|------------|---------|
| SUID | 4 | Executable Files | Run with owner's privileges |
| SGID | 2 | Directories | New files inherit the directory's group |
| Sticky Bit | 1 | Directories | Users cannot delete each other's files |

---

# 1️⃣ SUID (Set User ID)

Applied to executable files.

When another user executes the file, it runs with the **owner's privileges**.

## Symbolic

```bash
chmod u+s filename
```

## Numeric

```bash
chmod 4xxx filename
```

Example

```bash
chmod 4755 program
```

Check

```bash
ls -l program
```

Output

```text
-rwsr-xr-x
```

### Example

The `passwd` command uses SUID.

```bash
ls -l /usr/bin/passwd
```

Because it needs temporary root privileges to update `/etc/shadow`.

---

# 2️⃣ SGID (Set Group ID)

Applied mainly to **directories**.

Any file created inside inherits the **directory's group owner**, even if the creator's primary group is different.

## Symbolic

```bash
chmod g+s directory
```

## Numeric

```bash
chmod 2xxx directory
```

Example

```bash
chmod 2775 project
```

Check

```bash
ls -ld project
```

Output

```text
drwxrwsr-x
```

---

# 3️⃣ Sticky Bit

Applied to **shared directories**.

All users can create files, but users cannot delete or rename files owned by other users.

Only these users can delete a file:

- File Owner
- Directory Owner
- Root

## Symbolic

```bash
chmod o+t directory
```

## Numeric

```bash
chmod 1xxx directory
```

Example

```bash
chmod 1777 shared
```

Output

```text
drwxrwxrwt
```

Example:

```bash
ls -ld /tmp
```

Output

```text
drwxrwxrwt
```

---

# 🔒 Default Permissions

Whenever a file or directory is created, Linux automatically assigns default permissions.

These permissions are controlled by **umask**.

---

# 📌 Maximum Permissions

| Object | Maximum Permission |
|---------|-------------------:|
| File | 666 |
| Directory | 777 |

---

# 📌 What is umask?

`umask` removes permissions from the maximum permission.

Formula

```text
Default Permission = Maximum Permission - umask
```

---

### Example

Current umask

```text
022
```

Directory

```text
777 - 022 = 755
```

File

```text
666 - 022 = 644
```

---

Example

If a directory should have permission:

```text
664
```

Then

```text
777 - 664 = 113
```

So

```text
umask = 113
```

---

# 👀 View Current umask

```bash
umask
```

---

# Runtime umask

Temporary until logout.

```bash
umask 027
```

---

# Persistent umask

## Regular User

Edit

```text
~/.bashrc
```

Add

```bash
umask 027
```

Reload

```bash
source ~/.bashrc
```

---

## Root User

Edit

```text
/etc/profile
```

Add

```bash
umask 027
```

Reload

```bash
source /etc/profile
```

---

# 🧪 Practice Tasks

```bash
touch file1

ls -l

chmod 755 file1

chmod 644 file1

chmod u+x file1

chmod g+s project

chmod u+s program

chmod o+t shared

chown student file1

chgrp developers file1

chown student:developers file1

umask

umask 027
```

---

# 💡 RHCSA Exam Tips

- `chmod` → Change permissions
- `chown` → Change owner
- `chgrp` → Change group
- `ls -l` → View permissions
- `SUID` → Executable files
- `SGID` → Shared directories
- `Sticky Bit` → Shared directories like `/tmp`
- `umask` → Controls default permissions

---

# 🎤 Interview Questions

### What is DAC?

Discretionary Access Control allows the owner to control file permissions.

---

### What is MAC?

Mandatory Access Control is implemented using SELinux.

---

### Difference between SUID and SGID?

- SUID runs a program with the owner's privileges.
- SGID makes new files inherit the directory's group.

---

### What is Sticky Bit?

It prevents users from deleting each other's files in a shared directory.

---

### Why does `/usr/bin/passwd` have SUID?

Because it requires temporary root privileges to modify `/etc/shadow`.

---

### What is umask?

A value that determines the default permissions for newly created files and directories.

---

# ⚡ Quick Revision

```bash
chmod 755 file

chmod 644 file

chmod u+s file

chmod g+s directory

chmod o+t directory

chmod 4755 file

chmod 2775 directory

chmod 1777 directory

chown user file

chgrp group file

chown user:group file

umask

umask 027

source ~/.bashrc
```