# Chapter 1: Introduction to Vim & SSH

## Bash Shell

- **Bash** stands for **Bourne Again Shell**.
- It is the default command-line shell in most Linux distributions.

### Useful Terms

| Term | Description |
|------|-------------|
| `~` | Represents the current user's **Home Directory** |
| `root` | Administrator account with full system privileges |

---

# Linux Command Syntax

```bash
command [option] [argument]
```

### Examples

```bash
ls
ls -l
mkdir test
rm file.txt
```

---

# Getting Help in Linux

There are two common ways to get help for any command.

### 1. Using `--help`

Displays available options for a command.

```bash
command --help
```

Example:

```bash
ls --help
```

### 2. Using `man`

Displays the complete manual page of a command.

```bash
man command
```

Example:

```bash
man ls
```

---

# Basic Linux Commands

| Command | Description |
|---------|-------------|
| `ls` | List files and directories |
| `ls -l` | Long listing format |
| `ls -a` | Show hidden files and directories |
| `ls -t` | Sort files by modification time |
| `touch file.txt` | Create a new empty file |
| `mkdir folder` | Create a new directory |
| `rm file.txt` | Delete a file |
| `rmdir folder` | Delete an empty directory |
| `rm -rf folder` | Force delete a file or directory |
| `cat file.txt` | Display file contents |
| `head file.txt` | Show the first 10 lines |
| `tail file.txt` | Show the last 10 lines |
| `echo "text"` | Display or write text |

---

# SSH (Secure Shell)

SSH (**Secure Shell**) is a protocol used to securely connect to a remote Linux system.

### SSH Syntax

```bash
ssh username@hostname
```

or

```bash
ssh username@IP_Address
```

Example:

```bash
ssh parth@192.168.1.10
```

---

# Passwordless SSH Login

## Step 1: Generate SSH Keys

```bash
ssh-keygen
```

The keys are stored in:

```text
~/.ssh/
```

Files created:

- `id_rsa` → Private Key
- `id_rsa.pub` → Public Key

---

## Step 2: Copy the Public Key

```bash
ssh-copy-id username@hostname
```

Example:

```bash
ssh-copy-id parth@192.168.1.10
```

---

## Step 3: Login

```bash
ssh username@hostname
```

Now you can log in without entering the remote account password.

---

# SSH with Passphrase

A **passphrase** adds an extra layer of security to your private key.

## Generate a Passphrase-Protected Key

```bash
ssh-keygen
```

During key generation:

```text
Enter passphrase:
Confirm passphrase:
```

Copy the key:

```bash
ssh-copy-id username@hostname
```

Now, every time you connect, SSH will ask for the passphrase.

---

# Using SSH Agent

Instead of typing the passphrase every time, use **ssh-agent**.

## Start the Agent

```bash
eval $(ssh-agent)
```

## Add Your Private Key

```bash
ssh-add ~/.ssh/id_rsa
```

After adding the key, SSH uses the stored credentials automatically.

---

# Creating a Non-Default SSH Key

Generate a custom key.

```bash
ssh-keygen -f ~/.ssh/mykey
```

This creates:

```text
mykey
mykey.pub
```

---

## Copy the Custom Public Key

```bash
ssh-copy-id -i ~/.ssh/mykey.pub username@hostname
```

The `-i` option specifies which public key to copy.

---

# Important SSH Commands

```bash
ssh username@hostname
ssh-keygen
ssh-copy-id username@hostname
ssh-agent
eval $(ssh-agent)
ssh-add ~/.ssh/id_rsa
ssh-keygen -f ~/.ssh/mykey
ssh-copy-id -i ~/.ssh/mykey.pub username@hostname
```

---

# Key Points

- Bash is the default Linux shell.
- `~` represents the home directory.
- `root` is the administrator account.
- Use `--help` or `man` to learn about commands.
- SSH provides secure remote access.
- `ssh-keygen` creates SSH key pairs.
- `ssh-copy-id` copies the public key to a remote server.
- A passphrase secures your private key.
- `ssh-agent` stores your key in memory to avoid entering the passphrase repeatedly.
- Custom SSH keys can be created using the `-f` option.