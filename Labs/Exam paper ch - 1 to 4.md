# 📝 RHCSA Practice Exam 01

> **Duration:** 2.5 Hours  
> **Difficulty:** Intermediate  
> **Topics Covered:** SSH, User Management, Password Policy, Permissions, Links, Umask, Sudo

---

# Instructions

- Complete all tasks as the **root** user unless otherwise specified.
- Do not skip verification commands.
- Restart services if configuration changes require it.
- Test every configuration before moving to the next task.

---

# Task 1: SSH Configuration (10 Marks)

## Objective

Verify and configure the SSH service.

### Requirements

- Enable SSH login for the **root** user.
- Restart the SSH service if required.
- Verify that the root user can log in through SSH.

> **Note:** After configuration, use SSH from **servera** to **serverb** as the **trainee** user and switch to the **root** user using `sudo`.

---

# Task 2: SSH Key Authentication (10 Marks)

Configure passwordless SSH authentication.

### Requirements

- From **serverb**, configure passwordless SSH login from the **trainee** user to the **engineer** user on **servera**.
- Generate SSH keys.
- Configure the key with the passphrase:

```text
welcome123
```

- Verify that the SSH connection works correctly.
- Return to the root user on **servera** after testing.

---

# Task 3: User Management (15 Marks)

Create and configure users.

### Requirements

1. Create a group:

```
analytics
```

with

```
GID = 7000
```

2. Create the following users:

```
analytics1
analytics2
analytics3
```

3. Configure the following:

- analytics1 should be a member of the **analytics** group.
- analytics2 should have the home directory:

```
/analytics2
```

- analytics3 should **not** be allowed to log in.

4. Set the password of all users to:

```
Jessica
```

---

# Task 4: Password Policy (15 Marks)

Create and configure the user **Monica**.

### Requirements

- Create user:

```
Monica
```

- Password:

```
Jessica
```

- Display Monica's password aging information.
- Configure password expiry after:

```
20 Days
```

- Configure account expiry after:

```
120 Days
```

- Force Monica to change the password during the first login.

---

# Task 5: Collaborative Directory (20 Marks)

Create a shared directory.

### Requirements

Create

```
/mysql
```

Configure:

- Group owner should be:

```
analytics
```

- Members of the analytics group should have full access.
- Other users must not have write permission.
- Newly created files should automatically inherit the **analytics** group.
- Users must not be able to delete each other's files.
- Verify the configuration.

---

# Task 6: Working with Files, Permissions & Links (15 Marks)

Complete the following tasks.

### Hard Link

Create

```
/root/restore.txt
```

having the same inode number as

```
/root/linuxadmin.txt
```

---

### Edit File

Modify **restore.txt**

Content

```
This is restore.txt to the rescue
```

---

### Copy File

Copy

```
linuxadmin.txt
```

to

```
/home/trainee/practice/
```

---

### Verify Directory Permissions

Switch to the **trainee** user.

Ensure the directory

```
practice
```

is accessible.

If required, modify permissions.

---

### Soft Link

Create a symbolic link

```
/tmp/sending-practice
```

pointing to

```
/home/trainee/practice
```

---

# Task 7: Temporary Umask (5 Marks)

Configure a temporary umask.

### Requirements

New Files

```
640
```

New Directories

```
750
```

Verify by creating

```
tempfile.txt
tempdir
```

Confirm that the configuration disappears after logging out.

---

# Task 8: Permanent Umask (5 Marks)

Configure a permanent umask for

```
analytics1
```

Requirements

New Files

```
600
```

New Directories

```
700
```

Verify after logging out and logging back in.

Create

```
securefile.txt
securedir
```

---

# Task 9: Full Sudo Access (5 Marks)

Create

```
adminuser
```

Requirements

- Full sudo access.
- Verify sudo configuration.
- Test administrative commands.

---

# Task 10: Limited Sudo Access (10 Marks)

Create

```
user
```

Configure sudo so the user can execute **only user and group management commands** learned in Chapter 3.

Examples include

- useradd
- usermod
- userdel
- passwd
- groupadd
- groupdel
- groupmod
- gpasswd
- id

Verify the configuration and test the permissions.

---

# Evaluation Checklist

| Task | Marks | Status |
|-------|------:|--------|
| SSH Configuration | 10 | ☐ |
| SSH Keys | 10 | ☐ |
| User Management | 15 | ☐ |
| Password Policy | 15 | ☐ |
| Collaborative Directory | 20 | ☐ |
| Links & Permissions | 15 | ☐ |
| Temporary Umask | 5 | ☐ |
| Permanent Umask | 5 | ☐ |
| Full Sudo | 5 | ☐ |
| Limited Sudo | 10 | ☐ |

---

# Total Marks

**100 Marks**

---

# Skills Covered

- SSH
- SSH Keys
- User Management
- Groups
- Password Aging
- Password Policies
- Hard Links
- Soft Links
- Permissions
- SGID
- Sticky Bit
- Umask
- Sudo
- File Ownership
- Linux Administration