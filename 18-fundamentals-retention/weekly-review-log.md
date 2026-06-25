# Weekly Review Log

## Purpose

This file tracks weekly retention for the Secure Mission Data Platform project.

The goal is to make sure earlier fundamentals stay active as the project becomes more advanced. Linux, networking, databases, AWS, security, cost modeling, Terraform, and documentation should not be treated as separate isolated topics.

Each week should show what I learned, what I reused, what I documented, and what still needs work.

## Weekly Review Template

### Week of: YYYY-MM-DD

## New Concepts Learned

*

## Older Skills Reused

### Linux

*

### Networking

*

### AWS

*

### Security

*

### Database / Recovery

*

### Cost Modeling

*

### Documentation

*

## Project Artifacts Updated

*

## Commands Practiced

```bash
```

## What I Tested or Validated

*

## What I Can Explain Without Notes

*

## What Still Feels Weak

*

## Next Week Focus

*

---

## Week of: 2026-06-22

## New Concepts Learned

* Difference between `sudo apt update` and `sudo apt full-upgrade`
* Purpose of VirtualBox snapshots
* Difference between VirtualBox Extension Pack and Guest Additions
* Difference between terminal, shell, and console
* Basic Linux command structure
* How to use man pages, `--help`, `help`, `man -k`, and `apropos`
* Difference between shell built-ins and executable commands using `type`

## Older Skills Reused

### Linux

* Practiced basic command-line navigation and help tools

### Networking

* Reviewed early commands related to network interfaces such as `ifconfig` and `ip addr`

### AWS

* No AWS build work yet. Current focus is local Linux foundation.

### Security

* Connected snapshots and rollback habits to safer system changes

### Database / Recovery

* No database work yet. Recovery mindset introduced through VM snapshots.

### Cost Modeling

* No cost modeling work yet.

### Documentation

* Created initial project documentation structure
* Wrote early Linux foundation notes in a professional format

## Project Artifacts Updated

* `README.md`
* `04-fundamentals/linux-command-basics.md`
* `04-fundamentals/linux-help-system.md`
* `04-fundamentals/virtualbox-snapshots.md`
* `04-fundamentals/terminal-shell-console.md`
* `00-documentation-standards/technical-writing-notes.md`
* `18-fundamentals-retention/weekly-review-log.md`

## Commands Practiced

```bash
git status
git init
man ls
ls --help
help cd
type cd
type ls
df -h
ip addr
```

## What I Tested or Validated

* Confirmed Git is installed and working on Windows
* Created the local Git repository
* Created the first project folders and Markdown documentation files
* Ran basic Linux identity, shell, disk usage, and network interface commands inside the VM.
* Verified the VM has a working shell environment and active network interface.

## What I Can Explain Without Notes

* Why `apt update` does not install upgrades by itself
* Why snapshots are useful before risky changes
* Basic difference between terminal, shell, and console
* How `/` and `?` search inside man pages
* Why `help cd` works differently from `ls --help`

## What Still Feels Weak

* GitHub workflow is still new
* Markdown documentation workflow is still new
* Linux commands need more hands-on repetition inside the VM

## Next Week Focus

* Continue Linux foundation
* Practice commands inside the Linux VM
* Create a clean VM snapshot
* Start documenting actual lab outputs, not just concepts


### Date

2026-06-24

### New Topic Learned

Linux terminal productivity:

* TAB completion
* Keyboard shortcuts
* Bash history
* History privacy settings
* Adding date/time to command history

### Old Skills Reused

```text
pwd
whoami
echo $SHELL
type
man
apropos
df -h
ip addr
```

### Commands Practiced

```bash
history
history | tail
echo $HISTSIZE
echo $HISTFILESIZE
cat ~/.bash_history
history -d
history -c
```

### What I Understand Now

TAB completion helps me move faster and avoid typing mistakes.

Keyboard shortcuts make terminal work faster.

Bash history helps me reuse and audit commands, but it can also be risky if sensitive commands are saved.

`HISTSIZE` controls session history, while `HISTFILESIZE` controls how much history is saved to the history file.

`HISTTIMEFORMAT` can add timestamps to command history.

### Weak Spots

Need to remember exact variable names:

* `HISTSIZE`
* `HISTFILESIZE`
* `HISTCONTROL`
* `HISTTIMEFORMAT`

Need more practice with:

* `Ctrl + R`
* `history -d`
* history expansion like `!!`, `!17`, and `!ls`

### Next Review

Redo the Bash history commands and terminal shortcuts without notes.


## Date

2026-06-25

### New Topic Learned

Linux root access and privilege basics:

* Root vs non-privileged users
* `sudo`
* `su`
* `sudo su`
* `sudo su -`
* `passwd`
* `sudo -v`
* `sudo -k`
* Root directory `/` vs root user home directory `/root`

### Old Skills Reused

```text
TAB completion
man pages
Bash history
history deletion
running commands without saving to history
Ctrl + D
apt update
package installation
```

### Commands Practiced

```bash
whoami
id
sudo whoami
sudo su
sudo su -
su
exit
passwd
sudo passwd root
sudo -v
sudo -k
tail /etc/shadow
apt update
apt install nmap
lshw
man nmap
route -n
nmap -sV -p 80 www.example.com
nmap -sV -p 80,443 default_gateway_ip
history
history -d 4
history -c
```

### Challenges Completed

Section 4 Linux Terminal challenges completed successfully.

Challenge topics:

* Ran `tail /etc/shadow` as a normal user and as root
* Used TAB completion
* Became root temporarily
* Installed `nmap`
* Exited root with `Ctrl + D`
* Set the root password
* Used `su`
* Ran `lshw` as root
* Used `man nmap` and searched for `-sV`
* Ran a basic `nmap -sV` scan
* Found the default gateway using `route -n`
* Practiced history display, line deletion, no-trace command usage, and history clearing

### What I Understand Now

Root is the most privileged account on a Linux system.

Normal users should be used for normal work, and root/admin privileges should only be used when needed.

`sudo [command]` is safer than staying logged in as root because it runs one admin command at a time.

`su` switches users and can be used to become root if the root password is known.

`sudo su` and `sudo su -` both give root shells, but `sudo su -` loads the root login environment.

`passwd` changes passwords, and root can change other users’ passwords.

The root directory `/` is the top-level filesystem directory, while `/root` is the root user’s home directory.

### Security Connection

This topic connects directly to least privilege.

In cloud/security work, users and services should only receive the permissions they need. Admin access should be controlled, temporary, and auditable.

This will matter later for:

* SSH access
* sudoers
* Linux hardening
* IAM roles
* cloud admin permissions
* incident response
* audit logging

### Weak Spots

Need more review on:

* exact difference between `sudo su` and `sudo su -`
* when to use `sudo [command]` instead of a root shell
* `route -n` output and identifying the default gateway
* safe and ethical use of `nmap`

### Next Review

Redo the root access commands and explain the difference between normal user, root, `sudo`, and `su` without notes.


