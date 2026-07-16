# Chapter 2: Manage Files from the Command Line

> **Objective:** Understand the Linux file system hierarchy, navigate directories, create links, search text using `grep`, and use shell expansions and wildcards efficiently.

---

# Table of Contents

1. Linux File System Hierarchy
2. Navigation Basics
3. Soft Links (Symbolic Links)
4. Hard Links
5. Inode Number
6. Searching Text with `grep`
7. Wildcards
8. Brace Expansion
9. Practice Tasks
10. Interview Questions
11. Common Mistakes
12. Quick Revision
13. Summary

---

# Introduction

Everything in Linux is organized in a hierarchical directory structure called the **File System Hierarchy**.

Unlike Windows (C:, D:, E: drives), Linux starts from a single top-level directory called the **Root Directory (`/`)**.

```
        /
       ├── boot
       ├── dev
       ├── etc
       ├── home
       ├── root
       ├── usr
       ├── var
       ├── tmp
       └── ...
```

Understanding this hierarchy is essential for every Linux administrator.

---

# 1. Linux File System Hierarchy

## `/boot`

Stores boot-related files.

Contents include:

- Linux Kernel (`vmlinuz`)
- Bootloader files
- Initial RAM Disk (initramfs)

Example

```bash
ls /boot
```

---

## `/dev`

Contains device files.

Examples

- Hard Disk
- Keyboard
- Mouse
- CPU
- Printer
- USB Devices

Example

```bash
ls /dev
```

---

## `/home`

Stores home directories for regular users.

Example

```
/home/parth
```

---

## `/root`

Home directory of the **root** user.

```
/root
```

---

## `/etc`

Stores system configuration files.

Examples

```
passwd

hosts

fstab

ssh
```

Example

```bash
ls /etc
```

---

## `/tmp`

Temporary storage.

- Any user can create files here.
- Temporary files are automatically deleted after reboot.

Example

```bash
cd /tmp
```

---

## `/usr/bin`

Stores executable programs for regular users.

Example

```bash
ls /usr/bin
```

---

## `/usr/sbin`

Stores administrative commands.

Usually used by the root user.

---

## `/usr/lib` and `/usr/lib64`

Contain shared libraries used by applications.

---

## `/media`

Automatically mounts removable storage devices.

Examples

- USB Drives
- CD/DVD

---

## `/mnt`

Used for manually mounting storage devices.

---

## `/run`

Stores runtime information.

Contains temporary process information and runtime logs.

---

## `/var`

Stores variable data.

Examples

- System Logs
- Mail
- Cache
- Print Queue

Most log files are stored in

```
/var/log
```

---

# 2. Navigation Basics

## Current Directory

```
.
```

Represents the current working directory.

---

## Parent Directory

```
..
```

Represents the previous directory.

Example

```bash
cd ..
```

---

## Home Directory

```bash
cd
```

or

```bash
cd ~
```

Moves directly to the current user's home directory.

---

# 3. Soft Link (Symbolic Link)

A **Soft Link** acts like a Windows shortcut.

It points to another file or directory.

## Syntax

```bash
ln -s source destination
```

Example

```bash
ln -s /home/parth/file.txt shortcut.txt
```

---

## Advantages

- Can link files
- Can link directories
- Easy access

---

## Dangling Soft Link

If the original file is moved or deleted,

the symbolic link becomes invalid.

Example

```
shortcut.txt -> Broken Link
```

Linux usually displays broken links in **red**.

---

# 4. Hard Link

A Hard Link creates another reference to the same file.

## Syntax

```bash
ln source destination
```

Example

```bash
ln file.txt backup.txt
```

---

## Advantages

Even if the original file is deleted,

the hard link still contains the data.

---

## Limitations

❌ Cannot create a hard link for directories.

❌ Cannot create hard links across different file systems.

---

# Soft Link vs Hard Link

| Soft Link | Hard Link |
|------------|-----------|
| Shortcut | Copy of inode |
| Can link directories | Cannot link directories |
| Breaks if source is deleted | Still works |
| Different inode | Same inode |

---

# 5. Inode Number

Every file in Linux has a unique **inode number**.

The inode stores information like

- Owner
- Permissions
- Size
- Creation Time
- File Location

---

## Check Inode Number

```bash
ls -i
```

Example

```bash
ls -i file.txt
```

Files having the same inode number are hard links.

---

# 6. Searching Text using grep

`grep` is used to search text inside files.

## Syntax

```bash
grep [options] "pattern" filename
```

Example

```bash
grep "linux" notes.txt
```

---

## grep Options

### Ignore Case

```bash
grep -i linux file.txt
```

Matches

```
Linux
LINUX
linux
```

---

### Exclude Pattern

```bash
grep -v linux file.txt
```

Displays everything except lines containing

```
linux
```

---

### Show Line Numbers

```bash
grep -n linux file.txt
```

---

### Count Matches

```bash
grep -c linux file.txt
```

---

### Match Whole Word

```bash
grep -w dog file.txt
```

Matches

```
dog
```

Does not match

```
doggy
```

---

# 7. Wildcards

Wildcards are special symbols used to search or match file names.

| Symbol | Meaning |
|---------|---------|
| `*` | Zero or more characters |
| `?` | Exactly one character |
| `^` | Beginning of line (grep regex) |
| `$` | End of line (grep regex) |
| `!` | Negation / Exclude (depends on context) |

Examples

Starts with

```bash
grep "^comp" file.txt
```

Ends with

```bash
grep "ing$" file.txt
```

---

# 8. Brace Expansion

Brace expansion creates multiple files or directories.

Example

```bash
touch file{1..20}.txt
```

Creates

```
file1.txt

file2.txt

file3.txt

...

file20.txt
```

Create folders

```bash
mkdir project{1..10}
```

---

# Practice Tasks

## Task 1

Create

```
/root/grep-practice
```

Inside it create

```
Document1.doc

...

Document30.doc
```

Command

```bash
mkdir /root/grep-practice

cd /root/grep-practice

touch Document{1..30}.doc
```

---

## Task 2

Search words starting with

```
comp
```

```bash
grep "^comp" /usr/share/dict/words
```

---

## Task 3

Search the exact word

```
dog
```

```bash
grep -w dog /usr/share/dict/words
```

---

## Task 4

Practice

```
grep

grep -i

grep -v

grep -n

grep -c

grep -w
```

---

# Interview Questions

### What is the Linux File System Hierarchy?

It is the directory structure used by Linux to organize files and system resources.

---

### What is the difference between Soft Link and Hard Link?

Soft Link is a shortcut.

Hard Link shares the same inode with the original file.

---

### What is an inode?

An inode is a unique identifier containing metadata about a file.

---

### What is grep?

`grep` is a command-line utility used to search text inside files.

---

### What is Brace Expansion?

Brace expansion automatically creates multiple files or directories.

Example

```bash
touch file{1..5}.txt
```

---

# Common Mistakes

❌ Deleting the original file and expecting the symbolic link to work.

❌ Creating hard links for directories.

❌ Forgetting `-s` while creating symbolic links.

❌ Confusing `grep -w` and `grep -i`.

❌ Running `grep` on binary files.

---

# Quick Revision

```bash
cd
cd ..

ls

ls -i

ln -s source destination

ln source destination

grep keyword file

grep -i keyword file

grep -v keyword file

grep -n keyword file

grep -c keyword file

grep -w keyword file

touch file{1..20}.txt
```

---

# Summary

In this chapter, I learned

- Linux File System Hierarchy
- Home and Root directories
- Soft Links
- Hard Links
- Inode Numbers
- grep command
- Wildcards
- Brace Expansion

---

# Key Takeaways

✅ Linux follows a hierarchical file system.

✅ Every file has a unique inode.

✅ Soft links behave like shortcuts.

✅ Hard links remain valid even if the original filename is deleted.

✅ `grep` is one of the most powerful commands for searching text.

✅ Brace expansion saves time when creating multiple files.

✅ Mastering file management is a core RHCSA skill.