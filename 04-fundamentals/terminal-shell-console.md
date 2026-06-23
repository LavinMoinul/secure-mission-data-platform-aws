# Terminal, Shell, and Console

## Purpose

This document explains the difference between the terminal, shell, and console during the Linux foundation phase of the Secure Mission Data Platform project.

Understanding these terms helps clarify how I interact with Linux systems locally and later through cloud servers.

## What I Learned

The terminal, shell, and console are related, but they are not the same thing.

## Terminal

A terminal is the text-based interface where I type commands and view output.

On a Linux desktop, the terminal is usually opened as an application.

Example shortcut:

```text
Ctrl + Alt + T
```

The terminal gives me access to the command line while still using the graphical desktop environment.

## Shell

The shell is the program that receives my commands, interprets them, and passes them to the operating system.

A common Linux shell is Bash.

Example:

```bash
echo $SHELL
```

The shell is what understands commands such as:

```bash
cd
ls
pwd
echo
```

## Console

A console is a lower-level text-only interface that can be used without the graphical desktop environment.

Modern Linux systems often provide multiple virtual consoles. These can usually be accessed with:

```text
Ctrl + Alt + F1 through F8
```

One of the consoles may be used by the graphical interface, while the others can provide text-only login sessions.

## Why Consoles Matter

Virtual consoles are useful if the graphical desktop or terminal application stops working.

Even if the GUI breaks, Linux may still be usable through a console. This matters for troubleshooting and recovery.

## Why This Matters for Cloud Architecture

Cloud servers usually do not have a desktop GUI. They are commonly managed through SSH and command-line tools.

Understanding terminal, shell, and console basics prepares me for working with:

* Linux servers
* EC2 instances
* SSH sessions
* system logs
* service troubleshooting
* AWS CLI
* Terraform workflows

## Project Connection

The Secure Mission Data Platform begins in a local Linux virtual machine, but later maps into AWS EC2.

In the local lab, I may use a graphical terminal or virtual console. In AWS, I will usually connect to servers through SSH. In both cases, I need to understand how commands are being entered, interpreted, and executed.

## Lab Proof

Commands and actions to practice:

```bash
echo $SHELL
pwd
whoami
```

Virtual console test:

```text
Try switching to another console with Ctrl + Alt + F3, then return to the GUI console.
```

Note: In VirtualBox, the host key may affect how key combinations are captured by the VM.
