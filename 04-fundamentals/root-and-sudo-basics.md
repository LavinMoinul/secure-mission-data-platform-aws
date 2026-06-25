# Linux Root Access and Privilege Basics

## Source

Section 3:

* Video 21: root vs. Non-privileged Users. Getting root Access
* Video 22: Commands - Getting root access
* Section 4: Challenges - The Linux Terminal

## Root vs Non-Privileged Users

Linux has two main user categories:

```text
Non-privileged users = normal users with no special system-wide rights
Root user = the superuser / administrator account with full control of the system
```

The root account is the most privileged account on a Linux system. Root can modify system files, manage users, change passwords, install packages, stop services, and control the system.

It is not recommended to use root for ordinary daily tasks because a small mistake as root can cause major damage.

A safer approach is:

```text
Use a normal user for regular work.
Use sudo only when admin permissions are needed.
Exit root/admin sessions when finished.
```

## Why Root Access Is Dangerous

Root has absolute power on the system.

A mistake as a normal user may only affect that user’s files.

A mistake as root can affect:

```text
system files
user accounts
passwords
installed software
services
logs
network configuration
security settings
```

This is why root access should be temporary and intentional.

## `sudo`

`sudo` is commonly understood as “superuser do.”

It allows a permitted user to run a command with elevated privileges.

Example:

```bash
sudo whoami
```

If successful, this returns:

```text
root
```

This means the command was run with root privileges.

## `sudo [command]`

This runs one command as root without fully logging in as root.

Example:

```bash
sudo apt update
```

This is safer than staying logged in as root because it reduces the chance of forgetting that the shell has full admin power.

## `sudo su`

`sudo su` starts a root shell.

Example:

```bash
sudo su
```

This gives temporary access as root until the user exits the root shell.

Exit root with:

```bash
exit
```

or:

```text
Ctrl + D
```

## `sudo su -`

`sudo su -` switches to a full root login environment.

Example:

```bash
sudo su -
```

Difference:

```text
sudo su    = becomes root but usually keeps the current environment/directory
sudo su -  = becomes root with root's login environment and usually moves to /root
```

## `su`

`su` means substitute user or switch user.

Example:

```bash
su
```

By default, `su` tries to switch to root and requires the root password.

This is different from `sudo`, which usually asks for the current user’s password if the user is allowed to use sudo.

## `id`

The `id` command shows the current user ID, group ID, and group memberships.

Example:

```bash
id
```

This is useful for checking what user and groups are active.

## `passwd`

The `passwd` command changes a user password.

Change the current user’s password:

```bash
passwd
```

Change the root password using sudo:

```bash
sudo passwd root
```

As root, change another user’s password:

```bash
passwd username
```

## `sudo -v`

`sudo -v` refreshes sudo authentication without running a command.

Example:

```bash
sudo -v
```

This is useful before doing multiple admin commands because it refreshes the sudo timer.

## `sudo -k`

`sudo -k` invalidates the current sudo session.

Example:

```bash
sudo -k
```

This forces sudo to ask for the password again next time.

This is useful when you want to remove cached sudo authentication for security.

## Root Directory vs Root User Home Directory

The root directory is:

```text
/
```

This is the top-level directory of the Linux filesystem.

Example:

```bash
ls /
```

The root user’s home directory is:

```text
/root
```

Normal users usually have home directories under:

```text
/home/username
```

Example:

```text
/root        = root user's home directory
/home/lavin  = normal user's home directory example
/            = top-level filesystem root
```

## Section 4 Challenge Results

### Challenge 1: `/etc/shadow` as Normal User vs Root

Task:

```bash
tail /etc/shadow
```

Result as normal user:

```text
Permission denied / access blocked
```

Reason:

```text
/etc/shadow stores sensitive password-hash information and is protected from normal users.
```

Result as root:

```text
The command can read the file.
```

Security note:

```text
Do not paste /etc/shadow contents into GitHub or public notes.
```

### Challenge 2: Temporary Root Access and Installing `nmap`

Task:

```bash
sudo su
apt update && apt install nmap
```

Then exit root with:

```text
Ctrl + D
```

or:

```bash
exit
```

What this proved:

```text
I can temporarily become root, run admin package-management commands, install software, and exit root when finished.
```

### Challenge 3: Root Password, `su`, and `lshw`

Task:

```bash
sudo passwd root
su
lshw
```

What this proved:

```text
I can set the root password, switch to root with su, and run a hardware-information command as root.
```

### Challenge 4: `nmap`, Man Pages, and Default Gateway Scan

Tasks:

```bash
man nmap
```

Search inside the man page for:

```text
-sV
```

Run:

```bash
sudo nmap -sV -p 80 www.example.com
```

Find default gateway:

```bash
route -n
```

Then scan ports 80 and 443 on the default gateway:

```bash
sudo nmap -sV -p 80,443 default_gateway_ip
```

What this proved:

```text
I can use man pages to research command options, use nmap for basic service/version scanning, identify the default gateway, and run a targeted scan against specific ports.
```

Security note:

```text
Only scan systems I own, systems in my lab, or approved public examples. Do not randomly scan networks without permission.
```

### Challenge 5: Bash History Management

Tasks:

```bash
history
history -d 4
```

Run a command without saving it to history by starting it with a space if HISTCONTROL allows it:

```bash
 whoami
```

Then verify with:

```bash
history
```

Clear current session history:

```bash
history -c
```

What this proved:

```text
I can display command history, remove a specific history line, run a command without recording it when configured, and clear shell history.
```

## Why This Matters for Cloud and Security

Root access connects directly to security and cloud administration.

In cloud and infrastructure work, systems should follow least privilege:

```text
Users should only have the permissions they need.
Admin access should be temporary and intentional.
Sensitive files should be protected.
Privileged sessions should be exited when finished.
Commands should be auditable when appropriate.
```

This connects later to:

```text
SSH administration
Linux hardening
IAM least privilege
admin roles
sudoers
cloud server access
incident response
audit logs
secure operations
```

## Commands Practiced

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
passwd username
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
