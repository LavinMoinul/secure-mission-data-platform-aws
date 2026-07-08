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


## Date

2026-06-26

### New Topic Learned

Linux filesystem basics:

* What a filesystem does
* Linux treating almost everything as a file
* Filesystem Hierarchy Standard
* Common Linux directories
* Root directory `/`
* Root user home directory `/root`
* Normal user home directories under `/home`
* Current user home shortcut `~`
* Absolute paths
* Relative paths
* `.` and `..`
* Hidden dotfiles
* `pwd`, `cd`, `ls`, and `tree`

### Old Skills Reused

```text
TAB completion
root directory vs /root
/home and user home directories
ls
cat
reading protected/sensitive filesystem paths
Bash history
terminal navigation
```

### Commands Practiced

```bash
pwd
cd
cd ~
cd ..
cd ../..
ls
ls /
ls ~
ls ..
ls ../..
ls -la
cat /etc/hosts
cat hosts
cat /etc/cron.daily/logrotate
cat cron.daily/logrotate
cat ../../etc/cron.daily/logrotate
tree
tree -d
tree -f
lsblk
df -h
```

### What I Understand Now

A filesystem controls how data is stored, retrieved, named, and organized.

Linux has one top-level root directory: `/`.

The root directory `/` is not the same thing as `/root`.

`/root` is the home directory of the root user.

Normal users usually have home directories under `/home`.

`~` means the home directory of the current user, such as `/home/lavin`.

An absolute path starts from `/` and works from anywhere.

A relative path starts from the current working directory and does not start with `/`.

`.` means the current directory.

`..` means the parent directory.

Files that start with `.` are hidden files.

`tree` helps visualize directory structure recursively.

### Security and Cloud Connection

Filesystem knowledge matters because important Linux server files live in predictable places.

This connects later to:

* SSH configuration
* SSH keys
* system logs
* user account files
* protected password files
* service configuration
* backups
* web server directories
* cloud server troubleshooting

Important examples:

* `/etc/ssh/sshd_config`
* `/var/log`
* `/home/user/.ssh`
* `/etc/passwd`
* `/etc/shadow`
* `/tmp`
* `/var/www`

### Weak Spots

Need more review on:

* moving through relative paths with `..`
* common FHS directory purposes
* `tree -f` behavior

### Next Review

Redo path practice without notes:

* start from `/home/lavin`
* explain how to reach `/etc`
* explain why `../../etc/cron.daily/logrotate` works
* compare `/`, `/root`, `/home`, and `~`


---

## Date

2026-07-08

### New Topic Learned

Linux file viewing and basic file management:

* `cat`
* `cat -n`
* `less`
* `head`
* `tail`
* `tail -f`
* `watch`
* `mkdir`
* `mkdir -p`
* `mkdir -v`
* `touch`
* `cp`
* `cp -i`
* `cp -r`
* basic redirection using `>` and `>>`

### Old Skills Reused

```text
pwd
cd
ls
tree
relative paths
file and directory structure
Ctrl + C
man pages / command exploration
```

### Commands Practiced

```bash
mkdir
mkdir -v
mkdir -p
cd
pwd
ls
tree
touch
cat
cat -n
less
head
head -n 2
tail
tail -n 2
tail -f
watch -n 2
cp
cp -i
cp -r
echo "text" > file
echo "text" >> file
```

### What I Tested or Validated

* Created a Linux practice workspace named `section5-file-practice`
* Created nested directories using `mkdir -p`
* Created files using `touch`
* Added file contents using `echo`
* Confirmed that `>` overwrites file contents
* Confirmed that `>>` appends to file contents
* Used `cat` to view full file contents
* Used `cat -n` to view file contents with line numbers
* Used `less` to open a file in a scrollable viewer
* Used `head` and `tail` to view the beginning and end of files
* Used `tail -f` to watch a log file update live
* Used `watch` to monitor a directory as files changed
* Copied files with `cp`
* Confirmed that `cp` overwrites by default
* Used `cp -i` to ask before overwriting
* Confirmed that normal `cp` fails on directories without recursive mode
* Used `cp -r` to copy a directory and its contents

### What I Understand Now

`cat` is useful for quickly viewing smaller files.

`cat -n` shows line numbers.

`less` is better for larger files because it lets me scroll and search instead of printing everything at once.

`head` shows the beginning of a file.

`tail` shows the end of a file.

`tail -f` follows a file as it grows, which is useful for live log monitoring.

`watch` repeatedly runs a command and refreshes the output.

`mkdir` creates directories.

`mkdir -v` creates a directory and prints confirmation.

`mkdir -p` creates missing parent directories.

`touch` creates empty files if they do not exist.

`cp` copies files and overwrites by default.

`cp -i` asks before overwriting.

`cp -r` copies directories recursively.

`>` overwrites a file.

`>>` appends to a file.

### Mistakes / Things to Remember

I initially used `>` multiple times when adding lines to `logs/app.log`, which overwrote the previous contents each time.

I corrected this by using `>>` to append lines.

I also tried to run:

```bash
cat notes.txt
```

from the wrong location. The file was inside `docs`, so the correct path was:

```bash
cat docs/notes.txt
```

Normal `cp` failed on a directory because recursive mode was not specified.

The correct command was:

```bash
cp -r projects backup
```

### Security and Cloud Connection

These commands matter for Linux server and cloud work because I will need to inspect files, read logs, follow live logs, copy configuration files, back up directories, and avoid unsafe overwrites.

This connects later to:

* EC2 troubleshooting
* SSH sessions
* Linux log inspection
* backup and restore workflows
* service configuration review
* CloudOps runbooks
* incident response basics

### Weak Spots

Need more practice with:

* choosing `>` vs `>>`
* remembering correct relative paths
* using `less` navigation without notes
* using `tail -f` and `watch` smoothly with two terminals
* knowing when a command is safe vs destructive

### Next Review

Practice the next Section 5 file management commands:

* `mv`
* `rm`
* `shred`

Then review:

* moving vs copying files
* renaming files
* safe deletion habits
* destructive command caution
* when to use interactive options