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
