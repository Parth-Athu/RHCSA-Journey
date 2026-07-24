# 📂 Chapter 4: Control Access to Files

> **Objective:** Learn how Linux controls access to files and directories using permissions, ownership, and the `chmod`, `chown`, and `chgrp` commands.

---

# 📚 Table of Contents

1. Access Control Mechanisms
2. Linux File Permissions
3. Permission Levels
4. File vs Directory Permissions
5. Viewing Permissions
6. Changing Permissions (`chmod`)
7. Symbolic Method
8. Octal (Numeric) Method
9. File Ownership
10. Changing Ownership (`chown`)
11. Changing Group Ownership (`chgrp`)
12. Practice Tasks
13. RHCSA Exam Tips
14. Interview Questions
15. Quick Revision

---

# 🔐 Access Control Mechanisms

Linux provides two methods to control access to files and directories.

## 1. DAC (Discretionary Access Control)

DAC allows the **owner of a file or directory** to decide who can access it by assigning permissions.

Example:

- User creates a file.
- That user can decide who can read, modify, or execute it.

---

## 2. MAC (Mandatory Access Control)

MAC controls how **processes** interact with system resources.

In Red Hat Enterprise Linux, this is implemented using **SELinux (Security-Enhanced Linux)**.

Unlike DAC, users cannot directly modify MAC policies.

---

# 🔑 Linux File Permissions

Every file and directory has three permission sets.

```text
rw-   r--   r--
│      │      │
│      │      └── Others (o)
│      └───────── Group (g)
└──────────────── User/Owner (u)
```

| Symbol | Represents |
|---------|------------|
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
| Read (r) | Read file contents | List files inside the directory |
| Write (w) | Modify file | Create, rename, or delete files |
| Execute (x) | Run the file | Enter/access the directory |

---

# 👀 Viewing Permissions

Use the following command:

```bash
ls -l
```

Example output:

```text
-rwxr-xr--
```

Breakdown:

```text
- rwx r-x r--
  │   │   │
  │   │   └── Others
  │   └────── Group
  └────────── User
```

First Character:

| Symbol | Meaning |
|--------|---------|
| - | Regular File |
| d | Directory |
| l | Symbolic Link |

---

# 🛠 Changing Permissions (`chmod`)

`chmod` stands for **Change Mode**.

Syntax:

```bash
chmod [permissions] file
```

Linux supports two methods:

- Symbolic Method
- Octal (Numeric) Method

---

# 🔠 Symbolic Method

Symbols used:

| Symbol | Meaning |
|--------|---------|
| u | User |
| g | Group |
| o | Others |
| + | Add permission |
| - | Remove permission |
| = | Assign exact permission |

Examples

Remove execute permission from owner

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

# 🔢 Octal (Numeric) Method

Permission values

| Permission | Value |
|------------|------:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

### Common Values

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

---

### Examples

#### chmod 674 file1

| User | Group | Others |
|------|-------|--------|
| rw- | rwx | r-- |

```bash
chmod 674 file1
```

---

#### chmod 755 file2

| User | Group | Others |
|------|-------|--------|
| rwx | r-x | r-x |

```bash
chmod 755 file2
```

---

#### chmod 643 file3

| User | Group | Others |
|------|-------|--------|
| rw- | r-- | -wx |

```bash
chmod 643 file3
```

---

#### Example

Permissions

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

Every file has two ownership types.

## User Ownership

Represents the owner of the file.

## Group Ownership

Represents the group associated with the file.

Check ownership

```bash
ls -l
```

---

# 👨‍💻 Change User Ownership

Use the `chown` command.

Syntax

```bash
chown username file
```

Example

```bash
chown student file1
```

---

# 👥 Change Group Ownership

### Method 1

```bash
chown :developers file1
```

### Method 2

```bash
chgrp developers file1
```

---

# 🔄 Change User & Group Together

Syntax

```bash
chown username:groupname file
```

Example

```bash
chown student:developers file1
```

---

# 🧪 Practice Tasks

## Task 1

Create a file.

```bash
touch file1
```

---

## Task 2

Display file permissions.

```bash
ls -l file1
```

---

## Task 3

Give permission `644`.

```bash
chmod 644 file1
```

---

## Task 4

Give permission `755`.

```bash
chmod 755 file1
```

---

## Task 5

Remove execute permission from the owner.

```bash
chmod u-x file1
```

---

## Task 6

Change the file owner.

```bash
chown student file1
```

---

## Task 7

Change the file group.

```bash
chgrp developers file1
```

---

## Task 8

Change both owner and group.

```bash
chown student:developers file1
```

---

# 💡 RHCSA Exam Tips

- `chmod` → Change file permissions.
- `chown` → Change file owner.
- `chgrp` → Change file group.
- `ls -l` → View permissions and ownership.

Remember:

| Permission | Value |
|------------|------:|
| r | 4 |
| w | 2 |
| x | 1 |

---

# 🎤 Interview Questions

### What is DAC?

Discretionary Access Control allows the file owner to manage access permissions.

---

### What is MAC?

Mandatory Access Control is enforced by SELinux and controls how processes access resources.

---

### Difference between `chmod` and `chown`?

- `chmod` changes permissions.
- `chown` changes ownership.

---

### Difference between `chown` and `chgrp`?

- `chown` changes the user owner (and optionally the group).
- `chgrp` changes only the group owner.

---

### Which permission allows entering a directory?

**Execute (`x`)**

---

# ⚡ Quick Revision

```bash
ls -l

chmod 755 file

chmod 644 file

chmod u+x file

chmod g-w file

chmod o-r file

chmod u=rwx,g=rx,o=r file

chown student file

chown :developers file

chgrp developers file

chown student:developers file
```