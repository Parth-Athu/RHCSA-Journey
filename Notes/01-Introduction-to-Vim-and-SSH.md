# Chapter 1: Introduction to Vim, Linux Basics & SSH

> **Objective:** Learn the Linux shell, basic file management commands, and secure remote access using SSH.

---

# Table of Contents

1. Introduction
2. Bash Shell
3. Linux Basics
4. Linux Command Syntax
5. Getting Help
6. Basic Linux Commands
7. What is SSH?
8. SSH Key Authentication
9. SSH Passphrase
10. SSH Agent
11. Non-Default SSH Keys
12. Practice Tasks
13. Interview Questions
14. Common Mistakes
15. Quick Revision
16. Summary

---

# Introduction

Linux is a powerful, open-source operating system widely used for servers, cloud computing, DevOps, cybersecurity, and software development.

Unlike Windows, Linux is primarily managed through the **command line**, making command-line skills essential for every Linux administrator.

This chapter introduces the Bash shell, basic Linux commands, and SSH (Secure Shell), which is the standard method for securely accessing remote Linux systems.

---

# Bash Shell

## What is Bash?

**Bash (Bourne Again Shell)** is the default command-line shell in most Linux distributions.

A shell acts as a bridge between the user and the Linux kernel.

Instead of clicking icons, users execute commands.

Example:

```bash
pwd
ls
mkdir project
```

---

# Linux Basics

## Home Directory

The symbol

```bash
~
```

represents the current user's home directory.

Example

```bash
cd ~
```

---

## Root User

```
root
```

The root user is the system administrator.

Root has permission to perform every administrative task on the system.

⚠ Never use the root account unless required.

---

# Linux Command Syntax

Most Linux commands follow this syntax.

```bash
command [option] [argument]
```

Example

```bash
ls -l /home
```

| Part | Meaning |
|------|---------|
| command | Program to execute |
| option | Modifies command behavior |
| argument | File, directory, or target |

---

# Getting Help

Linux provides built-in documentation.

## Method 1

```bash
command --help
```

Example

```bash
ls --help
```

---

## Method 2

```bash
man command
```

Example

```bash
man ssh
```

Press

```
q
```

to exit.

---

# Basic Linux Commands

| Command | Purpose | Example |
|---------|---------|---------|
| ls | List directory contents | `ls` |
| ls -l | Long listing | `ls -l` |
| ls -a | Show hidden files | `ls -a` |
| ls -t | Sort by modification time | `ls -t` |
| touch | Create empty file | `touch notes.txt` |
| mkdir | Create directory | `mkdir Linux` |
| rm | Delete file | `rm notes.txt` |
| rmdir | Delete empty directory | `rmdir Linux` |
| rm -rf | Force delete directory | `rm -rf Linux` |
| cat | Display file | `cat file.txt` |
| head | First 10 lines | `head file.txt` |
| tail | Last 10 lines | `tail file.txt` |
| echo | Print or write text | `echo "Hello"` |

---

# What is SSH?

SSH stands for

> **Secure Shell**

SSH is a secure network protocol used to remotely connect to Linux systems.

Unlike Telnet, SSH encrypts all communication.

Syntax

```bash
ssh username@hostname
```

Example

```bash
ssh student@192.168.1.20
```

---

# SSH Key Authentication

Instead of entering the account password every time, SSH can authenticate using public and private keys.

## Step 1

Generate the key pair.

```bash
ssh-keygen
```

Files created

```
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```

| File | Description |
|------|-------------|
| id_rsa | Private Key (Never share) |
| id_rsa.pub | Public Key (Can be shared) |

---

## Step 2

Copy the public key.

```bash
ssh-copy-id student@serverb
```

---

## Step 3

Login

```bash
ssh student@serverb
```

No account password is required.

---

# SSH Passphrase

A passphrase protects the private key.

Generate a key.

```bash
ssh-keygen
```

Enter

```
Passphrase
```

Copy the key.

```bash
ssh-copy-id student@serverb
```

Now SSH asks for the passphrase.

---

# SSH Agent

SSH Agent stores decrypted keys in memory.

Start the agent.

```bash
eval $(ssh-agent)
```

Add the key.

```bash
ssh-add ~/.ssh/id_rsa
```

Now you don't need to enter the passphrase every login.

---

# Non-Default SSH Key

Generate another key.

```bash
ssh-keygen -f ~/.ssh/mykey
```

Copy it.

```bash
ssh-copy-id -i ~/.ssh/mykey.pub student@serverb
```

---

# Practice Tasks

## Task 1

Configure passwordless SSH login from Server A to Server B.

---

## Task 2

Configure SSH using a passphrase-protected key.

---

## Task 3

Login as root from Server A to Server B.

---

# Interview Questions

### What is Bash?

Bash is the default Linux shell that allows users to execute commands.

---

### What is SSH?

SSH is a secure protocol used for remote login.

---

### Difference between SSH and Telnet?

| SSH | Telnet |
|------|--------|
| Encrypted | Plain Text |
| Secure | Not Secure |
| Port 22 | Port 23 |

---

### What is the purpose of ssh-agent?

It stores decrypted private keys in memory so users don't repeatedly enter the passphrase.

---

# Common Mistakes

❌ Sharing the private key.

❌ Using `rm -rf` without checking the path.

❌ Forgetting to copy the public key.

❌ Connecting with the wrong username.

❌ Logging in as root on production servers.

---

# Quick Revision

```bash
ls
ls -l
ls -a
ls -t

touch

mkdir

rm

rmdir

rm -rf

cat

head

tail

echo

ssh

ssh-keygen

ssh-copy-id

ssh-agent

eval $(ssh-agent)

ssh-add
```

---

# Summary

In this chapter, I learned:

- Linux command syntax
- Bash Shell
- Home directory
- Root user
- Linux help commands
- Basic Linux commands
- Secure Shell (SSH)
- SSH key authentication
- SSH passphrase
- SSH Agent
- Non-default SSH keys

---

# Key Takeaways

✅ Linux is command-line driven.

✅ Bash is the default Linux shell.

✅ Use `man` and `--help` whenever you're unsure.

✅ Never share your private SSH key.

✅ SSH is the standard secure method for remote administration.

✅ Practice commands regularly—Linux is learned by doing.