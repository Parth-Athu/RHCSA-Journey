# ⚙️ Chapter 6: Manage Processes and System Performance

> **Objective:** Learn how Linux manages processes, monitor system performance, control process priority, and optimize the system using Tuned profiles.

---

# 📚 Table of Contents

1. Introduction to Processes
2. Types of Processes
3. Process Management
4. Process States
5. Process Control using Signals
6. Monitoring Processes
7. CPU Load Average
8. Using `top`
9. Tuned Profiles
10. Process Priority (Nice & Renice)
11. Practice Tasks
12. RHCSA Exam Tips
13. Interview Questions
14. Quick Revision

---

# 📌 What is a Process?

A **process** is a running instance of a program.

Examples:

- Command
- Application
- Background Job
- Task

Whenever a program is executed, Linux creates a unique process.

---

# 🔄 Types of Processes

## 1. Foreground Process

A foreground process runs directly on the terminal.

Example

```bash
firefox
```

Characteristics

- Uses the current terminal
- User must wait until the process finishes
- Accepts keyboard input

---

## 2. Background Process

A background process runs behind the terminal.

Example

```bash
firefox &
```

Output

```text
[1] 2458
```

Where

- **1** → Job ID
- **2458** → Process ID (PID)

---

# Managing Background Processes

## Stop a Process

Press

```text
Ctrl + Z
```

The process is stopped and moved to the background.

---

## Resume in Background

```bash
bg %1
```

---

## Bring to Foreground

```bash
fg %1
```

---

## Show Background Jobs

```bash
jobs
```

---

## Terminate Process

Press

```text
Ctrl + C
```

---

## Logout

Press

```text
Ctrl + D
```

---

# 🔍 Viewing Processes

## Display Current Terminal Processes

```bash
ps
```

---

## Long Format

```bash
ps -l
```

Displays

- UID
- PID
- PPID
- Priority
- Process State

---

## Display All User Processes

```bash
ps aux
```

---

## Customize Output

```bash
ps -o uid,ppid,pid,cmd
```

---

## View Parent and Child Processes

```bash
pstree
```

Specific process

```bash
pstree PID
```

---

## Sleep Command

Pause a process for a specific time.

```bash
sleep 30
```

---

# 🔄 Process States

| State | Description |
|--------|-------------|
| Running | Process is executing |
| Sleeping | Waiting for an event or user input |
| Stopped | Temporarily paused |
| Continued | Resumed after being stopped |
| Terminated | Process ended normally |
| Zombie | Child process waiting for parent to collect exit status |
| New | Newly created process |
| Killed | Forcefully terminated |

View process state

```bash
ps -l
```

---

# 🎯 Process Control

Linux controls processes using **signals**.

Signals are sent using the `kill` command.

## Syntax

```bash
kill SIGNAL PID
```

Example

```bash
kill -9 3499
```

or

```bash
kill -SIGKILL 3499
```

---

## List Available Signals

```bash
kill -l
```

---

## Common Signals

| Signal | Number | Purpose |
|---------|--------|---------|
| SIGKILL | 9 | Forcefully terminate |
| SIGSTOP | 19 | Stop process |
| SIGCONT | 18 | Continue stopped process |

---

## Kill by Process Name

Instead of PID

```bash
pkill processname
```

Example

```bash
pkill firefox
```

---

# 📊 Monitor Process Activity

## Check System Load

```bash
uptime
```

Output

```text
load average: 0.20, 0.35, 0.42
```

The three values represent CPU load over

- 1 minute
- 5 minutes
- 15 minutes

---

## Check CPU Count

```bash
lscpu
```

---

## Calculate CPU Load

Formula

```text
CPU Load = Load Average / Number of CPUs
```

Example

Load Average

```text
5.2
```

CPUs

```text
4
```

Calculation

```text
5.2 ÷ 4 = 1.3
```

If the result is **greater than 1**, the CPU is considered overloaded.

---

# 📈 Live Monitoring (`top`)

Launch

```bash
top
```

Useful shortcuts

| Key | Function |
|-----|----------|
| h | Help |
| k | Kill Process |
| s | Change Refresh Time |
| Shift + F | Customize Fields |
| Shift + B | Highlight Running Process |
| Shift + M | Sort by Memory Usage |
| z | Change Color |

---

# ⚡ Tuned Profiles

**Tuned** optimizes Linux performance using predefined profiles.

Package

```text
tuned
```

Service

```text
tuned.service
```

Administration Command

```bash
tuned-adm
```

---

## View Recommended Profile

```bash
tuned-adm recommend
```

---

## Apply a Profile

```bash
tuned-adm profile PROFILE_NAME
```

Example

```bash
tuned-adm profile virtual-guest
```

---

## Configuration Files

Main configuration

```text
/etc/tuned/tuned-main.conf
```

Available profiles

```text
/usr/lib/tuned/
```

---

# 🚀 Process Priority

Linux schedules processes using a **Nice Value**.

Range

```text
-20 -------------- 19
```

| Nice Value | Priority |
|------------|-----------|
| -20 | Highest |
| 0 | Normal |
| 19 | Lowest |

---

## Start a Process with Nice

```bash
nice command
```

---

## Change Priority of Running Process

```bash
renice -n VALUE PID
```

Example

```bash
renice -n -10 2458
```

---

# 🧪 Practice Tasks

### Task 1

Run a process in the background.

```bash
sleep 100 &
```

---

### Task 2

Display running jobs.

```bash
jobs
```

---

### Task 3

Bring a job to the foreground.

```bash
fg %1
```

---

### Task 4

Send it back to the background.

```bash
bg %1
```

---

### Task 5

View all running processes.

```bash
ps aux
```

---

### Task 6

Display parent-child process tree.

```bash
pstree
```

---

### Task 7

Kill a process.

```bash
kill -9 PID
```

---

### Task 8

Monitor the system.

```bash
top
```

---

### Task 9

Check CPU load.

```bash
uptime
```

---

### Task 10

Check CPU information.

```bash
lscpu
```

---

### Task 11

Display the recommended Tuned profile.

```bash
tuned-adm recommend
```

---

### Task 12

Change the priority of a running process.

```bash
renice -n -5 PID
```

---

# 💡 RHCSA Exam Tips

- `ps` → Current processes
- `ps aux` → All running processes
- `jobs` → Background jobs
- `bg` → Resume in background
- `fg` → Bring to foreground
- `kill -9` → Forcefully terminate
- `pkill` → Kill by process name
- `top` → Live process monitoring
- `uptime` → Check load average
- `lscpu` → CPU information
- `tuned-adm` → Manage performance profiles
- `renice` → Change process priority

---

# 🎤 Interview Questions

### What is a process?

A running instance of a program.

---

### Difference between foreground and background processes?

Foreground processes use the terminal directly, while background processes run behind the terminal.

---

### What is a Zombie process?

A completed child process whose exit status has not yet been collected by its parent.

---

### Which command displays all running processes?

```bash
ps aux
```

---

### Difference between PID and Job ID?

- **PID** → Unique Process ID assigned by the kernel.
- **Job ID** → Identifier assigned by the shell for background jobs.

---

### What does `kill -9` do?

Forcefully terminates a process using the **SIGKILL** signal.

---

### What is the Nice value range?

```text
-20 to 19
```

---

### Which Nice value has the highest priority?

```text
-20
```

---

### What is Tuned?

A Linux service that applies predefined performance optimization profiles.

---

# ⚡ Quick Revision

```bash
ps

ps -l

ps aux

ps -o uid,ppid,pid,cmd

pstree

jobs

bg %1

fg %1

kill -9 PID

kill -l

pkill process

top

uptime

lscpu

tuned-adm recommend

tuned-adm profile PROFILE_NAME

renice -n VALUE PID
```