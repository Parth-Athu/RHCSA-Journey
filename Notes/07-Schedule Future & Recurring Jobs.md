# ⏰ Chapter 7: Schedule Future & Recurring Jobs

> **Objective:** Learn how to schedule one-time and recurring tasks in Linux using **at**, **crontab**, and **Anacron**.

---

# 📚 Table of Contents

1. Future Job Scheduling
2. at Command
3. Cron Jobs (crontab)
4. Cron Time Fields
5. Special Characters in Cron
6. Practice Examples
7. System Recurring Jobs
8. Anacron
9. Restricting Cron Access
10. Managing Other Users' Crontab
11. Practice Tasks
12. RHCSA Exam Tips
13. Interview Questions
14. Quick Revision

---

# 📅 Future Job Scheduling

Linux provides two methods for scheduling future tasks.

| Method | Purpose |
|---------|----------|
| **at** | Execute a task only once |
| **crontab** | Execute a task repeatedly |

---

# 1️⃣ at Command (One-Time Scheduling)

The **at** command is used to schedule a job that runs **only once** at a specified date and time.

## Service

```text
atd
```

## Syntax

```bash
at TIME
```

or

```bash
at TIME MONTH DATE YEAR
```

### Example

```bash
at 5:00 PM
```

Linux displays

```text
at>
```

Now enter the command.

Example

```bash
echo "Hello RHCSA" >> /tmp/output.txt
```

Press

```text
Ctrl + D
```

to save the job.

---

## View Scheduled Jobs

```bash
atq
```

Example

```text
1   Tue Aug 4 13:00:00 2026
```

---

## Remove Scheduled Job

```bash
atrm JOB_ID
```

Example

```bash
atrm 1
```

---

# 2️⃣ Cron Jobs (Recurring Tasks)

Cron is used to execute tasks repeatedly at scheduled intervals.

## Package

```text
cronie
```

## Service

```text
crond.service
```

## Edit User Cron

```bash
crontab -e
```

---

## View User Cron

```bash
crontab -l
```

---

## Remove User Cron

```bash
crontab -r
```

---

# Cron Job Format

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of Week
│ │ │ └──── Month
│ │ └────── Day of Month
│ └──────── Hour
└────────── Minute
```

---

# Cron Fields

| Field | Range |
|--------|-------|
| Minute | 0 – 59 |
| Hour | 0 – 23 |
| Day of Month | 1 – 31 |
| Month | Jan – Dec (or 1–12) |
| Day of Week | Sun – Sat (or 0–7) |

---

# Special Characters

## `*` (Asterisk)

Means **every value**.

Example

```text
* * * * *
```

Runs every minute.

---

## `-` (Range)

Used to specify a range.

Example

```text
17-19
```

Means

```text
5 PM to 7 PM
```

---

## `/` (Interval)

Used to specify an interval.

Example

```text
*/2
```

Means

```text
Every 2 minutes
```

---

## `,` (Multiple Values)

Used to specify multiple values.

Example

```text
Mon,Thu,Sat
```

---

# Examples

## Every 2 Minutes

```text
*/2 * * * * echo "Hello"
```

---

## Every Monday at 1 PM

```text
0 13 * * Mon command
```

---

## Every Minute Between 2 PM and 4 PM

```text
* 14-16 * * * command
```

---

## Every Minute Between 2 PM and 4 PM (Monday–Wednesday)

```text
* 14-16 * * Mon-Wed command
```

---

## Every Minute Between 1 PM and 3 PM (Monday & Thursday–Saturday)

```text
* 13-15 * * Mon,Thu-Sat command
```

---

## Every 5 Minutes Between 3 PM and 5 PM

```text
*/5 15-17 * * * command
```

---

# System Recurring Jobs

When recurring jobs are configured in the **system crontab file**, they are called **System Recurring Jobs**.

## Main Configuration File

```text
/etc/crontab
```

Example

```bash
echo "hello world" >> /helloworld.txt
```

This task can be scheduled from the system crontab. :contentReference[oaicite:2]{index=2}

---

# Anacron

## What is Anacron?

Anacron is a **backup scheduling service**.

It ensures scheduled jobs are executed even if the system was powered off when the scheduled time arrived.

Example

If a daily backup is scheduled at **2:00 AM**, but the system is off at that time, Anacron runs the backup after the system starts.

---

## Configuration File

```text
/etc/anacrontab
```

---

## Supported Schedules

- Daily
- Weekly
- Monthly

---

# Cron vs Anacron

| Cron | Anacron |
|------|----------|
| Executes at the exact scheduled time | Executes missed jobs after system startup |
| Suitable for servers | Suitable for desktops/laptops |
| Misses jobs if the system is off | Executes missed jobs automatically |
| Supports minute-level scheduling | Supports daily, weekly, and monthly jobs |

---

# Restrict Users from Using Cron

To prevent a user from creating cron jobs, add the username to

```text
/etc/cron.deny
```

Example

```text
student
```

Now the **student** user cannot create a crontab. :contentReference[oaicite:3]{index=3}

---

# Manage Another User's Crontab

Root can edit another user's crontab.

Syntax

```bash
crontab -eu username
```

Example

```bash
crontab -eu student
```

---

# Practice Tasks

## Task 1

Schedule a task at **1 PM every Monday**.

---

## Task 2

Run a task **every minute between 2 PM and 4 PM**.

---

## Task 3

Run a task **every minute between 2 PM and 4 PM (Monday–Wednesday)**.

---

## Task 4

Run a task **every minute between 1 PM and 3 PM (Monday & Thursday–Saturday)**.

---

## Task 5

Run a task **every 5 minutes between 3 PM and 5 PM**.

---

# 💡 RHCSA Exam Tips

✅ `at` → One-time scheduling

✅ `crontab` → Recurring scheduling

✅ `atq` → View at jobs

✅ `atrm` → Remove at jobs

✅ `crontab -e` → Edit cron jobs

✅ `crontab -l` → List cron jobs

✅ `crontab -r` → Remove cron jobs

✅ `/etc/crontab` → System cron configuration

✅ `/etc/anacrontab` → Anacron configuration

✅ `/etc/cron.deny` → Restrict cron access

---

# 🎤 Interview Questions

### Difference between `at` and `crontab`?

- **at** executes a task only once.
- **crontab** executes tasks repeatedly.

---

### What is the service used by `at`?

```text
atd
```

---

### What is the service used by cron?

```text
crond.service
```

---

### Which package provides cron?

```text
cronie
```

---

### What is Anacron?

A scheduling service that executes missed daily, weekly, and monthly jobs after the system starts.

---

### Which file stores system cron jobs?

```text
/etc/crontab
```

---

### Which file restricts users from using cron?

```text
/etc/cron.deny
```

---

### How do you edit another user's crontab?

```bash
crontab -eu username
```

---

# ⚡ Quick Revision

```bash
at

atq

atrm

crontab -e

crontab -l

crontab -r

crontab -eu username

systemctl status atd

systemctl status crond

cat /etc/crontab

cat /etc/anacrontab
```

---

# 📝 Summary

In this chapter, you learned:

- Future scheduling using **at**
- Recurring scheduling using **crontab**
- Cron syntax and special characters
- System recurring jobs
- Anacron
- Cron access control
- Managing another user's crontab
