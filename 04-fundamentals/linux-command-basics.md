# Linux Command Basics

## Purpose

This document summarizes the Linux command structure and basic command-line habits I am learning during the local lab phase of the Secure Mission Data Platform project.

These fundamentals will be reused later when working with Linux servers, EC2 instances, SSH, logs, networking tools, AWS CLI, and Terraform.

## Command Structure

Linux commands generally follow this structure:

```bash
command option argument
```

Example:

```bash
ping -c 7 127.0.0.1
```

Breakdown:

* `ping` is the command
* `-c` is the option
* `7` is the value for the option
* `127.0.0.1` is the argument being tested

Commands, options, and arguments are separated by spaces.

## Options

Options modify how a command behaves.

Example:

```bash
ls -l
```

In this command:

* `ls` lists files and directories
* `-l` shows the output in long format

Multiple options can sometimes be combined.

Example:

```bash
ls -l -a -h
```

Can also be written as:

```bash
ls -lah
```

## Useful Commands Learned So Far

### `ls`

Lists files and directories.

```bash
ls
ls -l
ls -lah
```

### `df`

Shows filesystem disk usage.

```bash
df -h
```

The `-h` option makes the output human-readable.

### `ifconfig` and `ip addr`

Both can show network interface information.

Modern Linux systems commonly use:

```bash
ip addr
```

Older courses and systems may still show:

```bash
ifconfig
```

## Why This Matters for Cloud Architecture

Cloud infrastructure still depends heavily on command-line work. Even when the final architecture is hosted on AWS, I will still need to understand Linux commands to troubleshoot servers, inspect logs, check network interfaces, verify disk usage, and test connectivity.

This same command structure also applies later to tools such as:

* AWS CLI
* Terraform
* Bash scripts
* networking tools
* database commands

## Project Connection

The first version of this project starts inside a local Linux virtual machine. These command basics will be reused when I configure secure access, test networking, troubleshoot services, validate backup behavior, and later compare the local Linux environment to AWS EC2.
