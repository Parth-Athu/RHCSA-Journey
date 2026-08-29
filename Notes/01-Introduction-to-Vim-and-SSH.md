# CH-1: Introduction to Vim & SSH

> **RHCSA Journey — Chapter 1**
> This chapter covers basic Linux command usage, Vim, Bash shell, and SSH remote access.

---

## 1. Bash Shell

### What is Bash?

**Bash** stands for:

> **Bourne Again Shell**

Bash is a command-line shell commonly used in Linux to interact with the operating system.

Example:

```bash
ls
pwd
cd /etc
```

---

## 2. Important Linux Terms

### `~` — Home Directory

The tilde (`~`) represents the **current user's home directory**.

Example:

```bash
cd ~
```

If the user is `rhcsa`, it generally points to:

```text
/home/rhcsa
```

For the `root` user:

```text
/root
```

Check your current home directory:

```bash
echo $HOME
```

---

### Root User

The Linux administrator account is called **root**.

Root has almost unrestricted permissions on the system.

Check the current user:

```bash
whoami
```

Example output:

```text
root
```

or:

```text
rhcsa
```

---

# 3. Linux Command Syntax

A common Linux command structure is:

```text
command [options] [arguments]
```

The target can often be a file or directory path.

### Types of Commands

```bash
command
```

Example:

```bash
ls
```

---

```bash
command option
```

Example:

```bash
ls -l
```

---

```bash
command argument
```

Example:

```bash
cat file.txt
```

---

```bash
command option argument
```

Example:

```bash
ls -l /etc
```

> **Remember:** Not every command requires an option or argument.

---

# 4. Getting Help in Linux

Linux provides documentation and help for commands.

## Method 1 — `--help`

Use:

```bash
command --help
```

Example:

```bash
ls --help
```

This provides a quick overview of the command and its available options.

---

## Method 2 — `man`

Use:

```bash
man command
```

Example:

```bash
man ls
```

`man` displays the detailed **manual page** for a command.

### Useful `man` keys

Inside a man page:

| Key       | Function           |
| --------- | ------------------ |
| `↑` / `↓` | Move up/down       |
| `Space`   | Next page          |
| `b`       | Previous page      |
| `/word`   | Search for a word  |
| `n`       | Next search result |
| `q`       | Quit               |

Example:

```bash
man ssh
```

---

# 5. Basic Linux Commands

## 5.1 `ls`

Lists files and directories in the current working directory.

```bash
ls
```

Example:

```text
file1.txt
file2.txt
Documents
Downloads
```

---

## 5.2 `ls -l`

Displays files in **long listing format**.

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 root root 120 Aug 29 10:20 file.txt
```

It provides information such as:

* File type
* Permissions
* Owner
* Group
* File size
* Modification time
* File name

---

## 5.3 `ls -a`

Displays all files, including hidden files.

```bash
ls -a
```

Hidden files generally start with `.`.

Example:

```text
.
..
.bashrc
.profile
file.txt
```

---

## 5.4 `ls -t`

Sorts files according to modification time.

```bash
ls -t
```

Recently modified files appear first.

### Useful combination

```bash
ls -lt
```

Long listing + time sorting.

---

## 5.5 `touch`

Creates an empty file if the file does not already exist.

Syntax:

```bash
touch [filename]
```

Example:

```bash
touch file.txt
```

Create a file using a path:

```bash
touch /tmp/test.txt
```

---

## 5.6 `mkdir`

Creates a directory.

Syntax:

```bash
mkdir [directory_name]
```

Example:

```bash
mkdir test
```

Create a directory at a specific path:

```bash
mkdir /tmp/mydir
```

### Create parent directories

```bash
mkdir -p /tmp/linux/rhcsa/test
```

---

## 5.7 `rm`

Removes files.

Syntax:

```bash
rm [filename]
```

Example:

```bash
rm file.txt
```

---

## 5.8 `rmdir`

Removes an **empty directory**.

Syntax:

```bash
rmdir [directory_name]
```

Example:

```bash
rmdir test
```

If the directory contains files, `rmdir` will not remove it.

---

## 5.9 `rm -rf`

Removes directories and their contents recursively.

```bash
rm -rf directory
```

Meaning:

* `-r` → recursive
* `-f` → force

Example:

```bash
rm -rf test
```

> ⚠️ **CAUTION:** `rm -rf` is dangerous. Always verify the path before executing it, especially when working as `root`.

---

## 5.10 `cat`

Displays the contents of a file.

```bash
cat file.txt
```

Example:

```bash
cat /etc/hostname
```

---

## 5.11 `head`

Displays the first **10 lines** of a file by default.

```bash
head file.txt
```

To display a specific number of lines:

```bash
head -5 file.txt
```

---

## 5.12 `tail`

Displays the last **10 lines** of a file by default.

```bash
tail file.txt
```

Specific number of lines:

```bash
tail -5 file.txt
```

Useful for watching log files:

```bash
tail -f /var/log/messages
```

---

## 5.13 `echo`

Displays text on the terminal.

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

### Write text to a file

```bash
echo "Hello Linux" > file.txt
```

### Append text to a file

```bash
echo "Welcome to RHCSA" >> file.txt
```

> `>` overwrites the file.
> `>>` appends to the file.

---

# 6. Vim

**Vim** is a powerful text editor commonly used to edit configuration files in Linux.

Example:

```bash
vim file.txt
```

For RHCSA, Vim is especially useful for editing configuration files.

Example:

```bash
vim /etc/ssh/sshd_config
```

---

## Vim Modes

The most important Vim modes are:

### 1. Normal Mode

Used for navigation and commands.

Press:

```text
Esc
```

to return to Normal Mode.

---

### 2. Insert Mode

Used to type/edit text.

Press:

```text
i
```

to enter Insert Mode.

Other useful commands:

```text
a
o
```

---

### 3. Command Mode

From Normal Mode, press:

```text
:
```

Common commands:

```text
:w
```

Save file.

```text
:q
```

Quit Vim.

```text
:wq
```

Save and quit.

```text
:q!
```

Quit without saving.

---

## Basic Vim Workflow

```bash
vim file.txt
```

Then:

```text
i
```

→ type your content

```text
Esc
```

→ return to Normal Mode

```text
:wq
```

→ save and exit

---

# 7. SSH

## What is SSH?

**SSH** stands for:

> **Secure Shell**

SSH is used to securely connect to and manage a remote Linux system.

Example:

```bash
ssh user@192.168.10.2
```

SSH commonly uses **TCP port 22**.

---

# 8. SSH Syntax

General syntax:

```bash
ssh [username]@[hostname/IP]
```

Example using hostname:

```bash
ssh rhcsa@serverb
```

Example using IP address:

```bash
ssh rhcsa@192.168.10.20
```

---

# 9. SSH Authentication Methods

For RHCSA practice, you should know:

1. Password-based SSH
2. SSH key-based authentication
3. SSH key with passphrase
4. SSH agent
5. Root SSH access

---

# 10. Normal SSH — Password Authentication

Suppose:

```text
Server A → 192.168.10.10
Server B → 192.168.10.20
```

From Server A:

```bash
ssh rhcsa@192.168.10.20
```

You will be prompted for the user's password.

Example:

```text
rhcsa@192.168.10.20's password:
```

---

# 11. SSH Key-Based Authentication

SSH keys allow authentication without entering the remote user's password every time.

SSH normally uses a **key pair**:

```text
Private Key
+
Public Key
```

### Important

The:

* **Private key** stays on your machine.
* **Public key** is copied to the remote user's account.

Never share your private key.

---

# 12. Generate SSH Keys

Run:

```bash
ssh-keygen
```

You will see prompts similar to:

```text
Generating public/private rsa key pair.
Enter file in which to save the key:
Enter passphrase:
Enter same passphrase again:
```

If you do not want a passphrase, press:

```text
Enter
```

twice.

The default key location is usually:

```text
~/.ssh/
```

Check:

```bash
ls -la ~/.ssh/
```

You may see:

```text
id_rsa
id_rsa.pub
```

or another key type depending on the system/default configuration.

### Important

```text
Private key → id_rsa
Public key  → id_rsa.pub
```

Do **NOT** share the private key.

---

# 13. Copy Public Key to Remote Server

Use:

```bash
ssh-copy-id username@remote-host
```

Example:

```bash
ssh-copy-id rhcsa@serverb
```

or:

```bash
ssh-copy-id rhcsa@192.168.10.20
```

You will normally enter the remote user's password once.

The public key is added to:

```text
~/.ssh/authorized_keys
```

on the remote account.

---

# 14. Test SSH Without Password

After copying the key:

```bash
ssh rhcsa@serverb
```

If the key is configured correctly and has no passphrase, you should be able to log in without entering the remote account password.

---

# 15. SSH with Passphrase

A **passphrase** protects your private SSH key.

It adds an additional layer of security.

Generate a key:

```bash
ssh-keygen
```

When prompted:

```text
Enter passphrase:
```

Enter something such as:

```text
demo123
```

Then confirm it.

Copy the public key:

```bash
ssh-copy-id rhcsa@serverb
```

Now connect:

```bash
ssh rhcsa@serverb
```

You may be asked for:

```text
Enter passphrase for key:
```

### Important Difference

Without passphrase:

```text
SSH → private key → login
```

With passphrase:

```text
SSH → private key → passphrase → login
```

The passphrase protects the **private key**, not the remote Linux account password.

---

# 16. SSH Agent

Typing the SSH key passphrase every time can become annoying.

For this purpose, Linux provides **ssh-agent**.

`ssh-agent` is a background process that can hold private keys in memory and use them for SSH authentication.

---

## Start ssh-agent

Run:

```bash
eval "$(ssh-agent)"
```

You may see:

```text
Agent pid 1234
```

The PID identifies the running SSH agent process.

---

## Add Private Key to Agent

Use:

```bash
ssh-add ~/.ssh/id_rsa
```

You will be asked for the key's passphrase.

Example:

```text
Enter passphrase for /home/rhcsa/.ssh/id_rsa:
```

Enter the passphrase.

---

## Check Loaded Keys

```bash
ssh-add -l
```

This lists keys currently loaded into the SSH agent.

---

## Connect to Remote Server

Now:

```bash
ssh rhcsa@serverb
```

The SSH agent can provide the key authentication, so you normally do **not** need to type the passphrase again for each connection during that agent session.

---

# 17. SSH Root Login

By default, direct root SSH login may be disabled depending on the system configuration.

To configure root SSH login on the server:

Edit:

```bash
vim /etc/ssh/sshd_config
```

Find or add:

```text
PermitRootLogin yes
```

Then save:

```text
:wq
```

Restart the SSH service:

```bash
systemctl restart sshd
```

Check the service:

```bash
systemctl status sshd
```

Then from another machine:

```bash
ssh root@serverb
```

### Important RHCSA Note

For exam practice, understand the configuration:

```text
PermitRootLogin yes
```

But in real production environments, direct root SSH login is generally discouraged. Prefer logging in as a normal administrative user and using `sudo`.

---

# 18. Important SSH Files

| File                     | Purpose                                |
| ------------------------ | -------------------------------------- |
| `/etc/ssh/sshd_config`   | SSH server configuration               |
| `~/.ssh/`                | User's SSH configuration/key directory |
| `~/.ssh/authorized_keys` | Public keys allowed to log in          |
| `~/.ssh/id_rsa`          | Private key                            |
| `~/.ssh/id_rsa.pub`      | Public key                             |

> Key names can vary. For example, modern systems may use `id_ed25519` and `id_ed25519.pub`.

---

# 19. SSH Practical — Server A → Server B

### Scenario

```text
Server A
Hostname: servera

Server B
Hostname: serverb

User:
rhcsa
```

### Goal

Create an SSH key on Server A and use it to log in to `rhcsa` on Server B without entering the remote account password.

---

## Step 1 — Login to Server A

```bash
ssh rhcsa@servera
```

---

## Step 2 — Generate SSH Key

```bash
ssh-keygen
```

Press `Enter` for the default location.

For no passphrase:

```text
Enter passphrase:
[Press Enter]

Enter same passphrase again:
[Press Enter]
```

---

## Step 3 — Verify Key

```bash
ls -la ~/.ssh/
```

Look for:

```text
id_rsa
id_rsa.pub
```

---

## Step 4 — Copy Public Key

```bash
ssh-copy-id rhcsa@serverb
```

Enter the password of the remote `rhcsa` user when prompted.

---

## Step 5 — Test

```bash
ssh rhcsa@serverb
```

You should now be able to log in without entering the remote user's password.

---

# 20. RHCSA Practical — SSH with Passphrase

### Question

> Create an SSH key for user `rhcsa` on Server B with passphrase `demo123` and configure SSH key authentication to another server.

### Step 1 — Generate key

```bash
ssh-keygen
```

When prompted:

```text
Enter passphrase:
demo123
```

Confirm:

```text
demo123
```

---

### Step 2 — Copy Public Key

```bash
ssh-copy-id rhcsa@servera
```

---

### Step 3 — Test

```bash
ssh rhcsa@servera
```

You should be prompted for the key passphrase.

---

# 21. RHCSA Practical — SSH Agent

### Goal

Use a passphrase-protected SSH key without entering the passphrase for every SSH connection.

### Step 1 — Start agent

```bash
eval "$(ssh-agent)"
```

---

### Step 2 — Add private key

```bash
ssh-add ~/.ssh/id_rsa
```

Enter:

```text
demo123
```

---

### Step 3 — Verify

```bash
ssh-add -l
```

---

### Step 4 — SSH

```bash
ssh rhcsa@servera
```

The SSH agent handles the key authentication.

---

# 22. RHCSA Practical — Root SSH Access

### On the server you want to access as root:

Edit:

```bash
vim /etc/ssh/sshd_config
```

Set:

```text
PermitRootLogin yes
```

Save and exit:

```text
:wq
```

Restart SSH:

```bash
systemctl restart sshd
```

Test:

```bash
ssh root@serverb
```

---

# 23. Common SSH Troubleshooting Commands

### Check SSH service

```bash
systemctl status sshd
```

### Restart SSH service

```bash
systemctl restart sshd
```

### Check SSH configuration

```bash
sshd -t
```

This is useful **before restarting `sshd`** to check for configuration syntax errors.

### Check listening port

```bash
ss -tlnp | grep :22
```

### Check hostname

```bash
hostname
```

### Test network connectivity

```bash
ping serverb
```

### Check SSH connection with verbose output

```bash
ssh -v rhcsa@serverb
```

For more debugging information:

```bash
ssh -vvv rhcsa@serverb
```

---

# 24. Important SSH Concepts — Quick Table

| Concept           | Command / File           |
| ----------------- | ------------------------ |
| SSH connection    | `ssh user@host`          |
| Generate key      | `ssh-keygen`             |
| Copy public key   | `ssh-copy-id user@host`  |
| SSH agent         | `ssh-agent`              |
| Start agent       | `eval "$(ssh-agent)"`    |
| Add key           | `ssh-add ~/.ssh/id_rsa`  |
| List agent keys   | `ssh-add -l`             |
| SSH server config | `/etc/ssh/sshd_config`   |
| Authorized keys   | `~/.ssh/authorized_keys` |
| SSH service       | `sshd`                   |
| Check SSH config  | `sshd -t`                |
| SSH port          | `22/TCP`                 |

---

# 25. Exam-Focused SSH Questions

## Question 1

> Create an SSH key from `servera` and send the key to `serverb`.

### Commands

```bash
ssh-keygen
ssh-copy-id user@serverb
ssh user@serverb
```

---

## Question 2

> Configure SSH key-based authentication so that `rhcsa` on Server A can access `rhcsa` on Server B without entering a password.

### Commands

```bash
ssh-keygen
ssh-copy-id rhcsa@serverb
ssh rhcsa@serverb
```

---

## Question 3

> Create an SSH key with passphrase `demo123`.

### Command

```bash
ssh-keygen
```

When prompted for the passphrase:

```text
demo123
```

---

## Question 4

> Use SSH agent so that you don't have to enter the key passphrase every time.

### Commands

```bash
eval "$(ssh-agent)"
ssh-add ~/.ssh/id_rsa
ssh-add -l
ssh user@serverb
```

---

## Question 5

> Enable root login through SSH.

### On the SSH server:

```bash
vim /etc/ssh/sshd_config
```

Set:

```text
PermitRootLogin yes
```

Then:

```bash
sshd -t
systemctl restart sshd
```

Test:

```bash
ssh root@serverb
```

---

# 26. SSH Key Flow — Remember This

```text
              SERVER A
                 |
                 | ssh-keygen
                 ↓
        ┌──────────────────┐
        │   Private Key    │
        │   Public Key     │
        └──────────────────┘
                 |
                 | ssh-copy-id
                 ↓
              SERVER B
                 |
                 ↓
       ~/.ssh/authorized_keys
                 |
                 ↓
            SSH Login
```

### Golden Rule

```text
PRIVATE KEY → NEVER SHARE
PUBLIC KEY  → COPY TO REMOTE SERVER
```

---

# 27. Important Commands to Memorize

### Linux Basics

```bash
ls
ls -l
ls -a
ls -t
touch file
mkdir directory
rm file
rmdir directory
rm -rf directory
cat file
head file
tail file
echo "text"
```

### Help

```bash
command --help
man command
```

### Vim

```bash
vim file
```

Inside Vim:

```text
i       → Insert
Esc     → Normal mode
:w      → Save
:q      → Quit
:wq     → Save + Quit
:q!     → Quit without saving
```

### SSH

```bash
ssh user@host
ssh-keygen
ssh-copy-id user@host
ssh-add ~/.ssh/id_rsa
ssh-add -l
eval "$(ssh-agent)"
```

### SSH Server

```bash
vim /etc/ssh/sshd_config
sshd -t
systemctl restart sshd
systemctl status sshd
```

---

# 28. One-Minute Revision

```text
Bash
↓
Bourne Again Shell

~
↓
Current user's home directory

root
↓
Linux superuser/administrator

ls
↓
List files

ls -l
↓
Long listing

ls -a
↓
Show hidden files

touch
↓
Create file

mkdir
↓
Create directory

rm
↓
Remove file

rmdir
↓
Remove empty directory

cat
↓
Display file

head
↓
First 10 lines

tail
↓
Last 10 lines

echo
↓
Display/write text

vim
↓
Text editor

SSH
↓
Secure Shell / Remote login

ssh user@host
↓
Connect to remote system

ssh-keygen
↓
Generate SSH key pair

ssh-copy-id
↓
Copy public key to remote user

ssh-agent
↓
Stores SSH keys/passphrases in memory for authentication

ssh-add
↓
Add private key to agent

sshd_config
↓
SSH server configuration

Port 22
↓
Default SSH port
```

---

# 29. Practice Lab

Before moving to the next RHCSA chapter, practice these commands yourself.

### Basic Linux

```bash
mkdir ~/rhcsa-ch1
cd ~/rhcsa-ch1

touch file1.txt
touch file2.txt

echo "RHCSA Journey" > file1.txt
cat file1.txt

ls
ls -la

head file1.txt
tail file1.txt
```

### Vim

```bash
vim notes.txt
```

Practice:

```text
i
Esc
:w
:q
```

Then:

```bash
cat notes.txt
```

### SSH

On Server A:

```bash
ssh-keygen
ls -la ~/.ssh/
ssh-copy-id user@serverb
ssh user@serverb
```

### SSH with passphrase

```bash
ssh-keygen
ssh-copy-id user@serverb
ssh user@serverb
```

### SSH Agent

```bash
eval "$(ssh-agent)"
ssh-add ~/.ssh/id_rsa
ssh-add -l
ssh user@serverb
```

---

# 30. RHCSA Exam Mindset

When you see an SSH question in the exam, remember this sequence:

```text
1. Generate key
       ↓
2. Copy PUBLIC key
       ↓
3. Test SSH
       ↓
4. If passphrase → use ssh-agent
       ↓
5. If root access → check sshd_config
       ↓
6. Validate configuration
       ↓
7. Restart sshd if configuration changed
       ↓
8. Test again
```

### Most Important Commands

```bash
ssh-keygen
ssh-copy-id
ssh
ssh-agent
ssh-add
vim /etc/ssh/sshd_config
sshd -t
systemctl restart sshd
```

> **RHCSA Tip:** Don't just memorize the commands. Build two VMs (`servera` and `serverb`) and perform every SSH task yourself from the CLI. The goal is to be able to solve the task without looking at the notes.
