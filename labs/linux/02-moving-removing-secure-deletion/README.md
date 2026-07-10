# Section 5 Lab: Moving, Removing, and Secure Deletion

## Purpose

This lab practiced Linux file viewing, copying, moving, renaming, removing, and secure deletion commands inside a safe local Ubuntu VM workspace.

The goal was to understand how file operations behave before applying these commands later on real Linux servers, EC2 instances, logs, configuration files, backups, and security-sensitive files.

## Lab Environment

Lab directory:

```bash
~/section5-mv-rm-lab
```

Confirmed working directory with:

```bash
pwd
```

The lab was completed without `sudo`.

## Starting Structure

```text
section5-mv-rm-lab/
├── archive/
│   └── a.txt
├── backup/
├── inbox/
│   ├── a.txt
│   ├── report.txt
│   └── todo.txt
├── logs/
│   ├── app.log
│   └── error.log
├── secrets/
│   └── token.txt
└── trash-test/
    ├── delete-me.txt
    └── subdir/
        └── old.txt
```

## Commands Practiced

```bash
pwd
tree
cat
cat -n
head
tail
cp
cp -i
cp -r
mv
mv -i
mv -n
mv -u
rm
rm -i
rm -r
rm -rf
shred
```

## File Viewing and Redirection Review

Reviewed file viewing commands:

```bash
cat logs/app.log
cat -n logs/app.log
head -n 2 logs/app.log
tail -n 2 logs/app.log
```

Created a combined file:

```bash
cat inbox/report.txt logs/app.log > backup/combined.txt
```

Verified the combined file:

```bash
cat backup/combined.txt
```

## Copying Review

Copied `report.txt` into the backup directory:

```bash
cp inbox/report.txt backup/
```

Copied the whole `inbox/` directory into `backup/` using recursive mode:

```bash
cp -r inbox backup/
```

Verified the backup structure:

```bash
tree backup/
```

Result:

```text
backup/
├── combined.txt
├── inbox/
│   ├── a.txt
│   ├── report.txt
│   └── todo.txt
└── report.txt
```

## Moving and Renaming

Renamed `todo.txt` to `tasks.txt`:

```bash
mv inbox/todo.txt inbox/tasks.txt
```

Moved `report.txt` from `inbox/` to `archive/`:

```bash
mv inbox/report.txt archive/
```

Moved all `.log` files from `logs/` to `archive/` using a wildcard:

```bash
mv logs/*.log archive/
```

After this step:

```text
archive/
├── app.log
├── a.txt
├── error.log
└── report.txt

inbox/
├── a.txt
└── tasks.txt

logs/
```

## Move Overwrite Protection

Tested `mv -i`:

```bash
mv -i inbox/a.txt archive/
```

When prompted to overwrite `archive/a.txt`, answered:

```text
n
```

This prevented the overwrite.

Tested `mv -n`:

```bash
mv -n inbox/a.txt archive/
```

This refused to overwrite because `archive/a.txt` already existed.

Tested `mv -u`:

```bash
mv -u inbox/a.txt archive/
```

This only moves the source if it is newer than the destination, or if the destination does not exist.

Verified destination contents with:

```bash
cat archive/a.txt
tree archive/
```

## Removing Files and Directories

Before removing anything, confirmed the current location:

```bash
pwd
```

Removed a file interactively:

```bash
rm -i trash-test/delete-me.txt
```

Answered:

```text
y
```

Tried removing a directory with normal `rm`:

```bash
rm trash-test/subdir/
```

Received the expected error:

```text
rm: cannot remove 'trash-test/subdir/': Is a directory
```

Removed the directory correctly using recursive mode:

```bash
rm -r trash-test/subdir/
```

Created and removed a disposable directory using `rm -rf`:

```bash
mkdir danger-zone
rm -rf danger-zone/
```

Verified the result with:

```bash
tree
```

## Secure Deletion with `shred`

Created fake secret content:

```bash
echo "this is a secret" > secrets/token.txt
```

Used `shred` with verbose output, removal, and a custom number of overwrite passes:

```bash
shred -v -u -n 100 secrets/token.txt
```

Verified the file was removed:

```bash
tree secrets
```

Result:

```text
secrets

0 directories, 0 files
```

## Final Structure

Final lab structure:

```text
section5-mv-rm-lab/
├── archive/
│   ├── app.log
│   ├── a.txt
│   ├── error.log
│   └── report.txt
├── backup/
│   ├── combined.txt
│   ├── inbox/
│   │   ├── a.txt
│   │   ├── report.txt
│   │   └── todo.txt
│   └── report.txt
├── inbox/
│   ├── a.txt
│   └── tasks.txt
├── logs/
├── secrets/
└── trash-test/
```

Final command used to verify:

```bash
pwd
tree
```

## Lab Questions and Answers

### 1. What is the difference between `cp` and `mv`?

`cp` copies files or directories.

`mv` moves or renames files or directories.

A copy leaves the original in place. A move removes the original from the source location.

### 2. What happens if `mv` moves a file into a directory where the same filename already exists?

It can overwrite the destination file.

### 3. What does `mv -i` do?

`mv -i` asks before overwriting an existing destination file.

### 4. What does `mv -n` do?

`mv -n` refuses to overwrite an existing destination file.

### 5. What does `mv -u` do?

`mv -u` moves only if the source file is newer than the destination file, or if the destination file does not exist.

### 6. What did the wildcard move?

The wildcard `*.log` moved all files ending in `.log`.

In this lab, it moved:

```text
logs/app.log
logs/error.log
```

into:

```text
archive/
```

### 7. Why does normal `rm` fail on a directory?

Normal `rm` removes files.

Directories can contain files and subdirectories, so recursive mode is required.

### 8. What is the difference between `rm -r` and `rm -rf`?

`rm -r` removes directories recursively.

`rm -rf` removes directories recursively and forcefully, suppressing many prompts and ignoring nonexistent files.

### 9. Why should you use TAB autocomplete before `rm -rf`?

TAB autocomplete reduces path mistakes.

This matters because extra spaces, wrong paths, leading slashes, or bad wildcards can make `rm -rf` delete the wrong target.

### 10. Why is `shred` more secure than `rm`, but still not perfect?

`rm` removes the file entry and allows the disk space to be reused later.

`shred` overwrites the file before removing it, making recovery harder.

However, `shred` is not perfect because SSDs, journaling filesystems, backups, snapshots, copy-on-write filesystems, and cloud storage can keep data elsewhere.

### 11. What mistake would be most dangerous in this lab?

The most dangerous mistake would be running `rm -rf` on the wrong path.

Examples include:

```text
using the wrong current directory
adding an accidental leading slash
using extra spaces
using a bad wildcard
running destructive commands as root
```

## Security Connection

This lab connects to cybersecurity because moving and deleting files affects system integrity, logs, evidence, secrets, and recovery.

Risks:

```text
overwriting important files
deleting logs
destroying evidence
removing backups
exposing or mishandling secrets
assuming rm securely deletes data
```

Controls:

```text
check pwd before destructive commands
use tree or ls before deletion
use TAB autocomplete
use interactive options while practicing
avoid sudo unless required
avoid rm -rf outside disposable lab directories
encrypt sensitive data before deletion
```

Recovery Connection:

Accidental deletion or overwriting can destroy important files quickly. Backups, snapshots, version control, and careful command habits are necessary for resilient systems.

## Project Connection

These skills will be reused later when working with:

```text
EC2 instances
SSH sessions
Linux logs
configuration files
service directories
backup and restore workflows
incident response
secret handling
CloudOps runbooks
```

Understanding safe file movement and removal is part of building secure and resilient Linux/server habits.