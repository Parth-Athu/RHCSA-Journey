# 📦 Chapter 8: Install and Update Software Packages

> **Objective:** Learn how Linux manages software packages, use RPM, YUM, and DNF, and configure software repositories.

---

# 📚 Table of Contents

1. Introduction
2. Package Basics
3. Package Managers
4. Repository
5. Package Management Commands
6. Package Groups
7. Repository Configuration
8. Practice Tasks
9. RHCSA Exam Tips
10. Interview Questions
11. Quick Revision

---

# 📌 Introduction

Software in Linux is distributed as **packages**.

A package contains everything required to install and run an application.

---

# 📦 Package Components

A package mainly consists of:

## 1. Binary Files

These are the executable files of the application.

Example

```text
/bin
/usr/bin
/usr/sbin
```

---

## 2. Library Files

Libraries are required for an application to run correctly.

Without the required libraries, the application cannot execute.

---

## 3. Dependency Files

Dependencies are additional packages required before installing an application.

Example

```
Program
     │
     ├── Binary
     ├── Library
     └── Dependencies
```

---

# 📦 Package Managers

Linux provides different package management tools.

---

## 1. RPM (Red Hat Package Manager)

RPM is the basic package manager in Red Hat Linux.

Features

- Installs RPM packages
- Removes packages
- Queries package information

### Limitation

Dependencies must be installed manually.

---

## 2. YUM (Yellowdog Updater Modified)

YUM is an advanced package manager.

Features

- Installs packages
- Automatically resolves dependencies
- Updates packages
- Removes packages

Because YUM automatically installs required dependencies, it is also called a **Package Resolver**.

---

## 3. DNF (Dandified YUM)

DNF is the newer version of YUM.

Features

- Faster
- Better dependency resolution
- Modern replacement for YUM

Both **YUM** and **DNF** share the same binary files and work similarly.

Check

```bash
ls -l /usr/bin | grep yum
```

---

# 📂 Repository

A **Repository** is a centralized location where software packages are stored.

Linux downloads packages from repositories.

Two common repositories in RHEL are:

## BaseOS

Contains packages required for the operating system.

---

## AppStream

Contains additional applications and software packages.

---

# 📥 Package Management Commands

## Install Package

```bash
yum install package_name
```

or

```bash
dnf install package_name
```

Example

```bash
dnf install httpd
```

---

## Search Package

Search package by keyword

```bash
yum search keyword
```

Search package name and description

```bash
yum search all keyword
```

Example

```bash
yum search all apache
```

---

## Package Information

```bash
yum info package_name
```

Example

```bash
yum info httpd
```

Displays

- Package version
- Repository
- Description
- Installed or not

---

## Find Which Package Provides a File

```bash
yum whatprovides filename
```

Example

```bash
yum whatprovides ifconfig
```

---

## List Package

```bash
yum list package_name
```

Example

```bash
yum list httpd
```

---

## List All Available Packages

```bash
yum list
```

---

## List Installed Packages

```bash
yum list installed
```

---

## Update Package

```bash
yum update package_name
```

Example

```bash
yum update httpd
```

---

## Upgrade Packages

```bash
yum upgrade
```

Upgrade installs newer versions and removes old package versions.

---

# 📦 Package Groups

Linux also provides package groups.

There are two types.

---

## Package Group

A collection of related packages.

Example

```
Development Tools
```

---

## Environment Group

A collection of multiple package groups.

---

## List Groups

```bash
yum group list
```

---

## Install Group

```bash
yum group install "Group Name"
```

Example

```bash
yum group install "Development Tools"
```

---

# 🌐 Repository Configuration

A repository stores information about the server from which packages are downloaded.

Default repository location

```text
/etc/yum.repos.d/
```

View configured repositories

```bash
yum repolist all
```

---

# Methods to Configure Repository

There are two methods.

---

## Method 1: Using Command

Tool

```text
dnf config-manager
```

Example

```bash
dnf config-manager --add-repo http://example.com/repo
```

---

## Method 2: Manual Configuration

Create a repository file.

Location

```text
/etc/yum.repos.d/
```

Example

```text
myrepo.repo
```

---

# Repository File Format

```ini
[repoid]
name=Repository Name
baseurl=http://server/path
enabled=1
gpgcheck=0
```

### Explanation

| Option | Description |
|---------|-------------|
| repoid | Unique repository ID |
| name | Repository name |
| baseurl | Server URL (provided in exam) |
| enabled | 1 = Enabled, 0 = Disabled |
| gpgcheck | 0 = Disable GPG check |

---

# Verify Repository

Display enabled repositories

```bash
yum repolist enabled
```

---

Display available packages

```bash
yum list
```

If the repository is configured correctly, Linux contacts the repository server and displays the available packages.

---

# 🧪 Practice Tasks

## Task 1

Install the HTTP server.

```bash
dnf install httpd
```

---

## Task 2

Search for the Apache package.

```bash
yum search apache
```

---

## Task 3

Display package information.

```bash
yum info httpd
```

---

## Task 4

List installed packages.

```bash
yum list installed
```

---

## Task 5

Update a package.

```bash
yum update httpd
```

---

## Task 6

Display package groups.

```bash
yum group list
```

---

## Task 7

Configure a repository using `dnf config-manager`.

---

## Task 8

Create a repository manually in

```text
/etc/yum.repos.d/
```

---

# 💡 RHCSA Exam Tips

- RPM installs packages but **does not resolve dependencies**.
- YUM and DNF automatically install dependencies.
- DNF is the newer version of YUM.
- BaseOS contains core operating system packages.
- AppStream contains additional software.
- Repository files are stored in `/etc/yum.repos.d/`.
- Always verify a repository using `yum repolist`.
- Check package information before installing.

---

# 🎤 Interview Questions

### What is a package?

A package is a collection of binaries, libraries, and dependency files used to install software.

---

### What is the difference between RPM and YUM?

| RPM | YUM |
|-----|-----|
| Manual dependency installation | Automatic dependency resolution |
| Basic package manager | Advanced package manager |

---

### What is DNF?

DNF (Dandified YUM) is the newer version of YUM.

---

### What is a Repository?

A centralized location from which Linux downloads software packages.

---

### Where are repository files stored?

```text
/etc/yum.repos.d/
```

---

### What is BaseOS?

Repository containing essential operating system packages.

---

### What is AppStream?

Repository containing additional applications and software packages.

---

### Which command shows enabled repositories?

```bash
yum repolist enabled
```

---

### Which command searches for a package?

```bash
yum search keyword
```

---

### Which command displays package information?

```bash
yum info package_name
```

---

# ⚡ Quick Revision

```bash
rpm

yum install

dnf install

yum search

yum search all

yum info

yum list

yum list installed

yum update

yum upgrade

yum whatprovides

yum group list

yum group install

yum repolist all

yum repolist enabled

dnf config-manager --add-repo

/etc/yum.repos.d/
```

---

# 📝 Summary

In this chapter, you learned:

- Package components
- RPM package manager
- YUM package manager
- DNF package manager
- Package installation and updates
- Package groups
- Repository concepts
- Repository configuration
- Repository verification