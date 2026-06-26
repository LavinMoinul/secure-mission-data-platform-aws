# Linux Filesystem Basics

## Source

Section 5:

* Video 24: Intro to The Linux File System
* Video 25: The Filesystem Hierarchy Standard
* Video 26: Absolute vs. Relative Paths. Walking through the File System: `pwd`, `cd`, `tree`

## What Is a Filesystem?

A filesystem controls how data is stored and retrieved.

A file is a named piece or group of data.

The filesystem provides the structure and rules used to manage files, directories, and file names.

In Linux, almost everything is treated like a file, including regular files, directories, devices, and special system information.

## Accessing External Storage

External storage, like a USB drive, can usually be accessed through the file manager under devices.

From the command line, you can inspect device paths and mounted filesystems.

Useful commands:

```bash
lsblk
df -h
ls -lh /path/to/mounted/device
```

## Filesystem Hierarchy Standard

Linux organizes files under one top-level root directory:

```text
/
```

This is the top of the Linux filesystem.

Common Linux directories:

```text
/bin     = essential user command binaries used by all users
/sbin    = system/admin binaries, often used by the superuser
/boot    = files required to boot/start the system
/home    = home directories for normal users
/dev     = device files
/etc     = system-wide configuration files
/lib     = shared library files used by programs
/media   = mount point for automatically mounted external storage
/mnt     = temporary mount point, used less often
/tmp     = temporary files, may be deleted without notice
/proc    = process/kernel/system information shown as files
/run     = runtime data stored in RAM; clears after reboot
/var     = variable data such as logs and files that change often
/sys     = information about devices, drivers, and kernel features
/srv     = data for services/servers
/usr     = user-space programs, libraries, and shared resources
```

Some newer distributions may use:

```text
/usr/bin
/usr/sbin
```

instead of using separate physical directories for:

```text
/bin
/sbin
```

## Important Directory Examples

### `/`

`/` is the root directory.

It is the top-level directory of the Linux filesystem.

Example:

```bash
ls /
```

### `/root`

`/root` is the home directory of the root user.

This is different from `/`.

```text
/      = top of the filesystem
/root  = root user's home directory
```

### `/home`

`/home` contains normal users' home directories.

Example:

```text
/home/lavin
/home/bob
/home/tom
```

### `~`

`~` refers to the home directory of the current user.

Example:

```bash
ls ~
```

For the user `lavin`, this means:

```text
~ = /home/lavin
```

Important note:

```text
~ means the current user's home directory.
~ does not mean the parent /home directory.
```

## Basic Navigation Commands

### `pwd`

`pwd` means print working directory.

It shows the directory you are currently in.

```bash
pwd
```

### `cd`

`cd` means change directory.

It moves you into a different directory.

```bash
cd /etc
cd ~
cd ..
```

### `ls`

`ls` lists directory contents.

```bash
ls
ls /
ls ~
ls ..
ls ../..
```

Examples:

```bash
ls ..
```

This lists the parent directory relative to where you are right now.

```bash
ls ../..
```

This lists the parent of the parent directory.

## What Is a Path?

A path is the location of a file or directory.

There are two main types:

```text
absolute path
relative path
```

## Absolute Path

An absolute path starts from the root directory `/`.

It always begins with:

```text
/
```

Example:

```bash
cat /etc/hosts
```

Another example:

```bash
cat /etc/cron.daily/logrotate
```

Absolute paths work no matter where you are in the filesystem.

## Relative Path

A relative path starts from the current working directory.

It does not start with `/`.

Example if you are already inside `/etc`:

```bash
cat hosts
```

This works because `hosts` is inside the current directory.

Example if you are already inside `/etc` and want the logrotate file:

```bash
cat cron.daily/logrotate
```

This is relative because it starts from the current directory, not from `/`.

## Dot and Double Dot

### `.`

A single dot means the current directory.

```text
. = the directory I am currently in
```

Example:

```bash
ls .
```

### `..`

Double dot means the parent directory.

```text
.. = one directory above the current directory
```

Example:

```bash
ls ..
```

### Hidden Files

Files that start with a dot are hidden by default.

Example:

```text
.bashrc
.profile
.ssh
```

To show hidden files:

```bash
ls -la
```

## Relative Path Example

Absolute path:

```text
/etc/cron.daily/logrotate
```

If you are in:

```text
/home/lavin
```

then you need to move up to `/` first, because `/etc` is directly under the root directory.

From `/home/lavin`:

```bash
cat ../../etc/cron.daily/logrotate
```

Breakdown:

```text
..        = /home
../..     = /
../../etc = /etc
```

So:

```text
../../etc/cron.daily/logrotate
```

means:

```text
go up from /home/lavin to /home
go up again to /
then enter /etc/cron.daily/logrotate
```

## `tree`

`tree` shows a recursive directory listing.

It helps visualize parent and child directories.

Basic usage:

```bash
tree
```

Show only directories:

```bash
tree -d
```

Show paths for each file and directory:

```bash
tree -f
```

Note:

`tree -f` prints paths based on the path you give it. If you run it on an absolute path, the output will show absolute paths.

Example:

```bash
tree -f /etc
```

## Why This Matters for Cloud and Security

Filesystem knowledge matters because important Linux server files live in predictable places.

Examples:

```text
/etc/ssh/sshd_config = SSH server configuration
/var/log             = system and application logs
/home/user/.ssh      = SSH keys for a user
/etc/passwd          = user account information
/etc/shadow          = protected password hash information
/tmp                 = temporary files
/var/www             = common web server content location
```

In cloud and security work, understanding the filesystem helps with:

```text
finding configuration files
reading logs
troubleshooting services
securing SSH
understanding user home directories
locating scripts
managing backups
understanding where applications store data
```

## Commands Practiced

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
