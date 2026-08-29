# CH-2 — Linux File System, Links & Searching

> **RHCSA Journey**
> Focus: Filesystem Hierarchy • Links • Inodes • `grep` • Wildcards • Brace Expansion

---

## 1. Linux File System Hierarchy

Linux has a **tree-like filesystem** starting from:

```text
/
└── Root directory
```

View the main directories:

```bash
ls /
```

### 📌 Important Directories

| Directory   | Purpose                         | Remember          |
| ----------- | ------------------------------- | ----------------- |
| `/`         | Root of filesystem              | 🌳 Starting point |
| `/boot`     | Kernel & boot files             | 🚀 Boot           |
| `/dev`      | Device files                    | 🔌 Devices        |
| `/etc`      | Configuration files             | ⚙️ Config         |
| `/home`     | Regular users' home directories | 👤 Users          |
| `/root`     | Root user's home directory      | 👑 Root home      |
| `/tmp`      | Temporary files                 | 🗑️ Temporary     |
| `/usr/bin`  | Common executable programs      | 🧰 Commands       |
| `/usr/sbin` | System administration programs  | 🛠️ Admin         |
| `/usr/lib`  | Libraries                       | 📚 Libraries      |
| `/media`    | Removable media mount points    | 💿 USB/CD         |
| `/mnt`      | Temporary/manual mount point    | 📦 Mount          |
| `/run`      | Runtime data                    | ⚡ Runtime         |
| `/var`      | Variable/changing data          | 📊 Logs/data      |

### 🧠 Quick Memory

```text
boot → boot
dev  → devices
etc  → configuration
home → users
root → root's home
tmp  → temporary
usr  → programs/libraries
run  → runtime
var  → variable data
```

> ⚠️ **Don't confuse:**
> `/` = filesystem root
> `/root` = root user's home directory

---

# 2. Path Shortcuts

| Symbol | Meaning             | Example |
| ------ | ------------------- | ------- |
| `.`    | Current directory   | `ls .`  |
| `..`   | Parent directory    | `cd ..` |
| `~`    | Current user's home | `cd ~`  |
| `/`    | Filesystem root     | `cd /`  |

### Useful commands

```bash
cd
```

Go to home directory.

```bash
cd ..
```

Go to parent directory.

```bash
cd ~
```

Go to home directory.

```bash
pwd
```

Show current directory.

---

# 3. Absolute vs Relative Path

### Absolute Path

Starts from `/`.

```bash
cd /etc/ssh
```

### Relative Path

Starts from your current location.

```bash
cd Documents
cd ../Documents
```

### 🧠 Remember

```text
Absolute → starts with /
Relative → starts from current directory
```

---

# 4. Links in Linux

Linux has two important types of links:

```text
1. Soft Link
2. Hard Link
```

Command:

```bash
ln
```

---

# 5. Soft Link 🔗

Also called a **Symbolic Link**.

Think of it like a **shortcut**.

### Create

```bash
ln -s SOURCE LINK
```

Example:

```bash
touch file.txt

ln -s file.txt softlink.txt
```

Check:

```bash
ls -l
```

Output:

```text
softlink.txt -> file.txt
```

### Soft Link Can

* Point to a file
* Point to a directory
* Cross filesystems
* Become broken if the original disappears

---

## Dangling Soft Link

If the original file is deleted or moved:

```bash
rm file.txt
```

The link remains, but its target doesn't exist.

This is called a:

> **Dangling / Broken Symbolic Link**

---

# 6. Hard Link 🔗

A hard link is another directory entry pointing to the **same inode/data** as the original file.

### Create

```bash
ln SOURCE LINK
```

Example:

```bash
touch file.txt

ln file.txt hardlink.txt
```

Check:

```bash
ls -li
```

Example:

```text
123456 -rw-r--r-- 2 user user ... file.txt
123456 -rw-r--r-- 2 user user ... hardlink.txt
```

Notice:

```text
Same inode number
        ↓
     123456
```

---

# 7. Inode

An **inode** is a data structure that stores information about a filesystem object, such as:

* Permissions
* Owner
* Group
* File size
* Timestamps
* File data location information

Every file has an inode.

### Check inode number

```bash
ls -i
```

or:

```bash
ls -li
```

---

## 🔥 Hard Link Trick

If two files have:

```text
Same inode number
        ↓
They are hard links to the same file data
```

Example:

```text
1234 file.txt
1234 hardlink.txt
```

Same inode → hard links.

---

# 8. Hard Link vs Soft Link

| Feature            | Soft Link | Hard Link                                  |
| ------------------ | --------- | ------------------------------------------ |
| Command            | `ln -s`   | `ln`                                       |
| Points to          | Path/name | Same inode                                 |
| Directory link     | ✅ Yes     | ❌ Generally not allowed                    |
| Cross filesystem   | ✅ Yes     | ❌ No                                       |
| Own inode          | ✅ Yes     | ❌ Same inode                               |
| Target deleted     | ❌ Broken  | ✅ Data remains if another hard link exists |
| `ls -l` shows `->` | ✅ Yes     | ❌ No                                       |

### 🧠 Exam Shortcut

```text
ln -s → Soft Link
ln    → Hard Link
```

---

# 9. `grep` — Search Text 🔎

`grep` is used to **search for a pattern/string inside text**.

### Syntax

```bash
grep [OPTIONS] "PATTERN" FILE
```

Example:

```bash
grep "linux" file.txt
```

---

# 10. Important `grep` Options

### `grep -i`

Ignore case.

```bash
grep -i "linux" file.txt
```

Matches:

```text
Linux
linux
LINUX
LiNuX
```

---

### `grep -v`

Invert the match.

It displays lines that **do NOT contain** the pattern.

```bash
grep -v "linux" file.txt
```

---

### `grep -n`

Show line numbers.

```bash
grep -n "linux" file.txt
```

Example:

```text
5:Linux is powerful
12:Linux is open source
```

---

### `grep -c`

Count matching **lines**.

```bash
grep -c "linux" file.txt
```

> ⚠️ Remember: `grep -c` counts matching **lines**, not necessarily the total number of times the word appears.

---

### `grep -w`

Match a complete word.

```bash
grep -w "dog" file.txt
```

This matches:

```text
dog
```

but not:

```text
dogs
hotdog
doghouse
```

---

# 11. `grep` Quick Table

| Command            | Meaning                |
| ------------------ | ---------------------- |
| `grep "x" file`    | Search `x`             |
| `grep -i "x" file` | Ignore case            |
| `grep -v "x" file` | Exclude matching lines |
| `grep -n "x" file` | Show line number       |
| `grep -c "x" file` | Count matching lines   |
| `grep -w "x" file` | Match whole word       |

---

# 12. Searching with Regular Expressions

Some characters have special meanings when used with `grep`.

### `^` — Starts With

```bash
grep '^comp' file
```

Finds lines beginning with:

```text
comp
```

---

### `$` — Ends With

```bash
grep 'ich$' file
```

Finds lines ending with:

```text
ich
```

### RHCSA Example ⭐

> Find strings ending in `ich` from `/usr/share/dict/words` and save them to `/root/lines`.

```bash
grep 'ich$' /usr/share/dict/words > /root/lines
```

---

### `.` — Any Single Character

In a regular expression:

```bash
grep 'c.t' file
```

Can match:

```text
cat
cut
cot
```

---

### `*` — Zero or More of the Previous Character/Expression

Example:

```bash
grep 'ab*' file
```

Can match:

```text
a
ab
abb
abbb
```

> ⚠️ `*` does **not simply mean "including keyword"** in regular expressions. It modifies the item immediately before it.

---

# 13. Wildcards vs Regular Expressions ⚠️

Don't mix these up.

### Shell Wildcards

Used mainly for **matching filenames**.

```text
*   → Any number of characters
?   → Exactly one character
[]  → Character range/set
```

Example:

```bash
ls *.txt
```

---

### Regular Expressions

Used by commands such as `grep` to match **text patterns**.

Examples:

```text
^   → Start of line
$   → End of line
.   → Any single character
*   → Zero or more of previous item
```

### 🧠 Exam Tip

```text
Filename matching → Shell wildcards
Text matching     → grep / Regular Expressions
```

---

# 14. Shell Wildcards

## `*`

Matches zero or more characters.

```bash
ls *.txt
```

Matches:

```text
a.txt
file.txt
hello.txt
```

---

## `?`

Matches exactly **one character**.

```bash
ls file?.txt
```

Matches:

```text
file1.txt
fileA.txt
```

But not:

```text
file10.txt
```

---

## `[ ]`

Matches one character from a specified set/range.

Example:

```bash
ls file[1-3].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
```

---

# 15. Brace Expansion `{}`

Brace expansion is useful for generating multiple strings.

Example:

```bash
touch file{1..20}.txt
```

Creates:

```text
file1.txt
file2.txt
file3.txt
...
file20.txt
```

### Another Example

```bash
mkdir dir{1..5}
```

Creates:

```text
dir1
dir2
dir3
dir4
dir5
```

### Multiple values

```bash
touch {apple,banana,mango}.txt
```

Creates:

```text
apple.txt
banana.txt
mango.txt
```

> 🧠 **Brace expansion generates names; it doesn't search existing files.**

---

# 16. RHCSA Practical Tasks

## Task 1 — Create 30 Documents

Create:

```text
/root/grep-practice
```

Then create:

```text
Document1.doc
Document2.doc
...
Document30.doc
```

### Solution

```bash
mkdir -p /root/grep-practice
cd /root/grep-practice
touch Document{1..30}.doc
```

Verify:

```bash
ls
```

Or:

```bash
ls Document*.doc
```

Count them:

```bash
ls Document*.doc | wc -l
```

Expected:

```text
30
```

---

# 17. Task 2 — Search Strings Starting With `comp`

Search `/usr/share/dict/words` for strings beginning with `comp`.

```bash
grep '^comp' /usr/share/dict/words
```

### Why?

```text
^comp
│
└── line/string starts with "comp"
```

---

# 18. Task 3 — Search Exact Word `dog`

Use:

```bash
grep -w 'dog' /usr/share/dict/words
```

### Why `-w`?

It searches for the complete word rather than matching it as part of another word.

---

# 19. Task 4 — Search Ending With `ich`

```bash
grep 'ich$' /usr/share/dict/words
```

Save the result:

```bash
grep 'ich$' /usr/share/dict/words > /root/lines
```

Check:

```bash
cat /root/lines
```

---

# 20. Redirection

The `>` operator sends command output into a file.

```bash
command > file
```

Example:

```bash
grep 'ich$' /usr/share/dict/words > /root/lines
```

### Important

`>` **overwrites** the file.

`>>` **appends** to the file.

```bash
echo "Hello" > file.txt
echo "World" >> file.txt
```

---

# 21. Exam Questions ⭐

### Q1. Find strings ending in `ich` and save them to `/root/lines`.

```bash
grep 'ich$' /usr/share/dict/words > /root/lines
```

---

### Q2. Create 30 files:

```text
Document1.doc
...
Document30.doc
```

Solution:

```bash
mkdir -p /root/grep-practice
cd /root/grep-practice
touch Document{1..30}.doc
```

---

### Q3. Find strings beginning with `comp`.

```bash
grep '^comp' /usr/share/dict/words
```

---

### Q4. Find the exact word `dog`.

```bash
grep -w 'dog' /usr/share/dict/words
```

---

### Q5. Create a soft link.

```bash
ln -s source link
```

---

### Q6. Create a hard link.

```bash
ln source hardlink
```

Verify:

```bash
ls -li
```

---

# 22. 🧪 Practice Lab

Do this yourself without looking at the answers.

### Part A — Files

```text
1. Create /root/grep-practice
2. Create Document1.doc → Document30.doc
3. Display all files
4. Count the files
```

Useful commands:

```bash
mkdir -p /root/grep-practice
cd /root/grep-practice
touch Document{1..30}.doc
ls
ls Document*.doc | wc -l
```

---

### Part B — Soft Link

```text
1. Create original.txt
2. Create a soft link
3. Check the link
4. Delete original.txt
5. Check what happens to the link
```

Commands:

```bash
touch original.txt
ln -s original.txt softlink.txt
ls -l

rm original.txt
ls -l
```

Observe the broken/dangling link.

---

### Part C — Hard Link

```text
1. Create original.txt
2. Create a hard link
3. Check inode numbers
4. Delete original.txt
5. Check the hard link
```

Commands:

```bash
touch original.txt
ln original.txt hardlink.txt

ls -li

rm original.txt

cat hardlink.txt
```

### Observe

The hard link still contains the file's data because it points to the same inode.

---

### Part D — `grep`

Practice:

```bash
grep 'ich$' /usr/share/dict/words

grep '^comp' /usr/share/dict/words

grep -w 'dog' /usr/share/dict/words

grep -i 'linux' file.txt

grep -n 'linux' file.txt

grep -v 'linux' file.txt

grep -c 'linux' file.txt
```

---

# 23. 🧠 Final Revision Sheet

```text
FILESYSTEM
────────────────────────────
/       → Filesystem root
/boot   → Boot/kernel
/dev    → Devices
/etc    → Configuration
/home   → User homes
/root   → Root user's home
/tmp    → Temporary files
/usr    → Programs/libraries
/run    → Runtime data
/var    → Variable data/logs


PATHS
────────────────────────────
.       → Current directory
..      → Parent directory
~       → Home directory
/       → Filesystem root


LINKS
────────────────────────────
ln -s   → Soft link
ln      → Hard link

Soft link:
→ Path-based
→ Can link directories
→ Can cross filesystems
→ Breaks if target disappears

Hard link:
→ Same inode
→ Cannot normally link directories
→ Same filesystem
→ Data remains if another hard link exists


INODE
────────────────────────────
ls -i
ls -li

Same inode → Hard links


GREP
────────────────────────────
grep "x" file       → Search
grep -i "x" file    → Ignore case
grep -v "x" file    → Exclude matching lines
grep -n "x" file    → Line number
grep -c "x" file    → Count matching lines
grep -w "x" file    → Whole word


REGEX
────────────────────────────
^   → Starts with
$   → Ends with
.   → Any single character
*   → Zero or more of previous item


WILDCARDS
────────────────────────────
*       → Any number of characters
?       → One character
[1-3]   → Character range


BRACE EXPANSION
────────────────────────────
touch file{1..20}.txt
→ Creates file1.txt ... file20.txt
```

---

# ⭐ RHCSA Must-Know Commands

```bash
ls /
pwd
cd
cd ..
cd ~
ls -li

ln source hardlink
ln -s source softlink

grep "pattern" file
grep -i "pattern" file
grep -v "pattern" file
grep -n "pattern" file
grep -c "pattern" file
grep -w "pattern" file

grep '^comp' /usr/share/dict/words
grep 'ich$' /usr/share/dict/words

touch Document{1..30}.doc
```

> **Chapter 2 Goal:** Be able to perform every command above directly in the terminal without opening your notes.
