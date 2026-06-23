# VirtualBox Snapshots

## Purpose

This document explains how I am using VirtualBox snapshots during the local lab phase of the Secure Mission Data Platform project.

Snapshots give me a safe rollback point before making changes that could break the virtual machine.

## What I Learned

A VirtualBox snapshot saves the current state of a virtual machine at a specific point in time.

A snapshot can include:

* The current system state
* Installed packages
* Configuration files
* VM settings
* The current disk state

If something breaks later, I can restore the VM back to the snapshot instead of rebuilding the entire system.

## When to Take a Snapshot

Snapshots are useful before risky changes, such as:

* Running major updates
* Installing Guest Additions
* Changing network settings
* Changing SSH settings
* Changing firewall rules
* Installing unfamiliar packages
* Testing commands that could affect the system
* Starting a new lab section

## Example Snapshot Names

Clear snapshot names make rollback easier.

Examples:

```text
clean-linux-baseline
before-guest-additions
before-networking-changes
before-ssh-hardening
before-firewall-rules
before-package-upgrades
```

## Why This Matters

Snapshots are my first local version of rollback planning.

In real infrastructure work, changes should be tested safely before production. If something fails, there should be a way to recover or roll back.

VirtualBox snapshots help practice that mindset early.

## Cloud Architecture Connection

Later AWS equivalents include:

* AMIs for EC2 instance backups
* EBS snapshots for volume backups
* RDS snapshots for database recovery
* Terraform state and version control
* Staging environments
* Rollback plans
* Backup and restore runbooks

The concept is the same: before making risky changes, create a recovery path.

## Project Connection

The Secure Mission Data Platform starts in a local Linux VM before moving into AWS.

Before major changes to the local VM, I will take a snapshot and record what the snapshot protects. This helps build safe lab habits that later map to AWS backup, recovery, and rollback planning.

## Lab Proof

Initial snapshot to create:

```text
clean-linux-baseline
```

Purpose:

```text
Baseline snapshot after the Linux VM is installed and working, before making major configuration changes.
```

Future snapshots should be documented with:

* Snapshot name
* Date created
* Reason for snapshot
* Change being tested
* Restore result if rollback is needed
