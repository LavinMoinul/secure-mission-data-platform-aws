# Linux File Viewing and File Management

## Purpose

This document summarizes Linux file viewing and basic file management commands from Section 5 of the Linux course.

These commands will be reused later when working with Linux servers, EC2 instances, SSH sessions, logs, configuration files, backups, troubleshooting, and CloudOps-style runbooks.

## Commands Covered

```bash
cat
less
head
tail
watch
mkdir
touch
cp
```

Options and related operators practiced:

```bash
cat -n
tail -n
tail -f
head -n
watch -n
mkdir -p
mkdir -v
cp -i
cp -r
>
>>
```

## Viewing Files

### `cat`

`cat` displays the contents of a file.

```bash
cat file.txt
```

It prints the entire file directly into the terminal, so it is best for smaller files.

Example:

```bash
cat docs/notes.txt
```

### `cat -n`

`cat -n` displays the file contents with line numbers.

```bash
cat -n logs/app.log
```

This is useful when I need to reference specific lines in a file.

### Combining Files with `cat`

`cat` can display multiple files together.

```bash
cat file1.txt file2.txt
```

It can also combine multiple files and redirect the combined output into another file.

```bash
cat docs/notes.txt logs/app.log > combined.txt
```

In this example:

* `cat` combines the contents of `docs/notes.txt` and `logs/app.log`
* `>` sends that combined output into `combined.txt`

## Basic Redirection Used During Practice

### `>`

The `>` operator writes output into a file.

If the file already exists, it overwrites the existing contents.

```bash
echo "Line 1" > logs/app.log
```

During practice, I accidentally used `>` multiple times when adding lines to `logs/app.log`, which overwrote the previous contents each time.

### `>>`

The `>>` operator appends output to the end of a file.

It does not delete the existing contents.

```bash
echo "Line 2" >> logs/app.log
```

Key difference:

```text
>  overwrites
>> appends
```

## `less`

`less` opens a file in a scrollable viewer.

```bash
less logs/app.log
```

It is better than `cat` for larger files because it lets me move through the file one page at a time instead of dumping the entire file into the terminal.

Useful keys:

```text
q       quit
/text   search forward
n       next search result
N       previous search result
g       beginning of file
G       end of file
```

## `head`

`head` shows the beginning of a file.

```bash
head logs/app.log
```

By default, it shows the first 10 lines.

To show a specific number of lines:

```bash
head -n 2 logs/app.log
```

## `tail`

`tail` shows the end of a file.

```bash
tail logs/app.log
```

By default, it shows the last 10 lines.

To show a specific number of lines:

```bash
tail -n 2 logs/app.log
```

## `tail -f`

`tail -f` follows a file as it grows.

```bash
tail -f logs/app.log
```

This is useful for watching log files update live.

Example use cases:

* checking new login activity
* watching application logs
* seeing new errors appear
* monitoring service behavior

Stop it with:

```text
Ctrl + C
```

## `watch`

`watch` repeatedly runs a command at a set interval.

```bash
watch -n 2 ls logs
```

This runs `ls logs` every 2 seconds.

It is useful when I want to repeatedly monitor command output without manually running the command over and over.

Stop it with:

```text
Ctrl + C
```

## Creating Directories

### `mkdir`

`mkdir` creates a directory.

```bash
mkdir docs
```

### `mkdir -v`

`mkdir -v` creates a directory and prints a confirmation message.

```bash
mkdir -v section5-file-practice
```

### `mkdir -p`

`mkdir -p` creates parent directories if they do not already exist.

```bash
mkdir -p projects/app/config
```

Without `-p`, creating nested directories can fail if the parent directories do not already exist.

Example:

```bash
mkdir first/second/third
```

This can fail if `first` and `second` do not already exist.

Using `-p` fixes that:

```bash
mkdir -p first/second/third
```

## Creating Files

### `touch`

`touch` creates an empty file if the file does not already exist.

```bash
touch docs/notes.txt
```

If the file already exists, `touch` updates its timestamps.

During practice, I used `touch` to create files such as:

```text
docs/notes.txt
logs/app.log
logs/auth.log
projects/app/config/settings.conf
```

## Copying Files

### `cp`

`cp` copies files.

```bash
cp docs/notes.txt backup
```

By default, `cp` can overwrite an existing file without asking.

During practice, I confirmed that copying one file over another replaced the destination file’s contents.

### `cp -i`

`cp -i` asks before overwriting.

```bash
cp -i docs/notes.txt logs/app.log
```

This is safer when copying over important files.

If I answer `n`, the overwrite does not happen.

If I answer `y`, the overwrite happens.

### `cp -r`

`cp -r` copies directories recursively.

```bash
cp -r projects backup
```

A normal `cp` fails on directories because a directory contains other files and directories.

The `-r` option tells Linux to copy the directory and everything inside it.

## Practice Lab Summary

I created a practice workspace called:

```bash
section5-file-practice
```

Inside it, I created this structure:

```text
section5-file-practice/
├── backup/
├── docs/
├── logs/
└── projects/
    └── app/
        └── config/
```

Then I created files:

```text
docs/notes.txt
logs/app.log
logs/auth.log
projects/app/config/settings.conf
```

I added text to files using `echo`, `>`, and `>>`.

I viewed file contents using:

```bash
cat
cat -n
less
head
tail
```

I monitored a changing log using:

```bash
tail -f logs/app.log
```

I monitored a directory using:

```bash
watch -n 2 ls logs
```

I copied files and directories using:

```bash
cp
cp -i
cp -r
```

## Mistakes / Things to Remember

Using `>` multiple times overwrites previous file contents.

Using `>>` appends new content to the end of the file.

I tried:

```bash
cat notes.txt
```

but that failed because `notes.txt` was inside the `docs` directory.

The correct path was:

```bash
cat docs/notes.txt
```

Normal `cp` failed when copying a directory:

```text
cp: -r not specified; omitting directory 'projects'
```

The correct command was:

```bash
cp -r projects backup
```

## What I Understand Now

`cat` is useful for quickly viewing small files.

`cat -n` adds line numbers.

`less` is better for larger files because it lets me scroll and search.

`head` shows the beginning of a file.

`tail` shows the end of a file.

`tail -f` follows a file as it grows.

`watch` repeatedly runs a command and refreshes the output.

`mkdir` creates directories.

`mkdir -p` creates missing parent directories.

`touch` creates empty files.

`cp` copies files and overwrites by default.

`cp -i` asks before overwriting.

`cp -r` copies directories recursively.

`>` overwrites a file.

`>>` appends to a file.

## Why This Matters for Cloud Architecture

Cloud and infrastructure work requires reading files, inspecting logs, copying backups, checking configuration files, and monitoring running systems.

These commands will matter later when working with:

* EC2 instances
* SSH sessions
* Linux logs
* service configuration files
* backup and recovery workflows
* troubleshooting runbooks
* CloudOps tasks
* incident response basics

Understanding these commands now builds the Linux foundation needed for cloud security and resilience work.