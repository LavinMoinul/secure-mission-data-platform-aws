# Linux Moving, Renaming, and Removing Files

## Purpose

This document summarizes Linux commands for moving, renaming, removing, and securely removing files.

These commands are important because Linux server work often involves moving configuration files, renaming files, cleaning up directories, deleting temporary files, and understanding the risk of destructive commands.

## Commands Covered

```bash
mv
rm
shred
```

Options practiced:

```bash
mv -i
mv -n
mv -u
rm -i
rm -r
rm -rf
shred -v
shred -u
shred -n
```

Related concepts practiced:

```bash
wildcards
TAB autocomplete
relative paths
directory structure
overwrite behavior
recursive deletion
secure deletion limits
```

---

## Moving and Renaming with `mv`

The `mv` command moves files or directories.

```bash
mv source destination
```

It can also rename files.

```bash
mv old-name.txt new-name.txt
```

Example:

```bash
mv inbox/todo.txt inbox/tasks.txt
```

This renames `todo.txt` to `tasks.txt` inside the same directory.

## Moving a File Into Another Directory

```bash
mv inbox/report.txt archive/
```

This moves `report.txt` from `inbox/` into `archive/`.

After the move:

```text
inbox/report.txt       no longer exists
archive/report.txt     exists
```

## Moving Multiple Files

The `mv` command can move multiple files if the final argument is a destination directory.

```bash
mv file1.txt file2.txt file3.txt destination/
```

The last argument must be the directory where the files are being moved.

## Moving Files with Wildcards

Wildcards can be used with `mv`.

```bash
mv logs/*.log archive/
```

This moves all files ending in `.log` from `logs/` into `archive/`.

In the lab, this moved:

```text
logs/app.log
logs/error.log
```

into:

```text
archive/
```

## Overwrite Behavior with `mv`

If a file is moved into a directory where a file with the same name already exists, `mv` can overwrite the destination file.

Example:

```bash
mv inbox/a.txt archive/
```

If `archive/a.txt` already exists, the source file can replace it.

This is why overwrite-safe options matter.

## `mv -i`

`mv -i` asks before overwriting.

```bash
mv -i inbox/a.txt archive/
```

If the destination file already exists, Linux prompts before replacing it.

If I answer `n`, the move does not happen.

If I answer `y`, the move happens and the destination is overwritten.

## `mv -n`

`mv -n` means no-clobber.

```bash
mv -n inbox/a.txt archive/
```

It refuses to overwrite an existing destination file.

If the destination already exists, the command does not overwrite it.

## `mv -u`

`mv -u` updates the destination only if the source is newer than the destination, or if the destination does not exist.

```bash
mv -u inbox/a.txt archive/
```

This can be useful when syncing newer files without replacing newer destination files with older source files.

---

## Removing Files with `rm`

The `rm` command removes files.

```bash
rm file.txt
```

It does not move the file to a trash bin.

By default, `rm` does not ask before removing a file.

## `rm -i`

`rm -i` asks before removing a file.

```bash
rm -i trash-test/delete-me.txt
```

This is safer when practicing or when deleting important files.

## Removing Directories

Normal `rm` fails on directories.

```bash
rm trash-test/subdir/
```

Example error:

```text
rm: cannot remove 'trash-test/subdir/': Is a directory
```

A directory can contain other files and directories, so recursive mode is required.

## `rm -r`

`rm -r` removes a directory and its contents recursively.

```bash
rm -r trash-test/subdir/
```

The `-r` option means recursive.

## `rm -rf`

`rm -rf` removes recursively and forcefully.

```bash
rm -rf danger-zone/
```

Breakdown:

```text
-r = recursive
-f = force
```

The `-f` option suppresses many prompts and ignores nonexistent files.

It does not magically bypass all Linux permissions, but it removes safety prompts and can be very destructive if used on the wrong path.

## Safety Habits Before `rm -rf`

Before running destructive commands:

```bash
pwd
tree
ls
```

Use TAB autocomplete to reduce typing mistakes.

Dangerous mistakes include:

```text
wrong current directory
leading slash mistakes
extra spaces
bad wildcard use
wrong autocomplete target
```

Example dangerous pattern:

```bash
rm -rf / home/lavin/Desktop/random_folder
```

This would treat `/` and `home/lavin/Desktop/random_folder` as separate arguments.

That is extremely dangerous.

---

## Secure Removal with `shred`

The `shred` command overwrites a file before removing it.

```bash
shred -v -u file.txt
```

Breakdown:

```text
-v = verbose output
-u = remove file after overwriting
```

The number of overwrite passes can be specified with `-n`.

```bash
shred -v -u -n 100 secrets/token.txt
```

This overwrites the file 100 times before removing it.

## `rm` vs `shred`

`rm` removes the file entry and allows the space to be reused later.

The file data may still exist on disk until overwritten.

`shred` attempts to overwrite the file contents before removing the file, making recovery harder.

## Limits of `shred`

`shred` is not perfect.

It may not fully protect data on:

```text
SSDs
journaling filesystems
copy-on-write filesystems
cloud storage
snapshots
backups
RAID/storage layers
```

For truly confidential data, encryption before deletion is safer.

---

## Lab Summary

I completed a lab inside:

```bash
~/section5-mv-rm-lab
```

The lab included directories such as:

```text
inbox/
archive/
backup/
logs/
trash-test/
secrets/
```

I practiced:

```bash
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

I moved and renamed files, moved `.log` files with a wildcard, tested overwrite protection with `mv -i` and `mv -n`, tested update behavior with `mv -u`, removed files and directories, safely practiced `rm -rf` inside a disposable lab folder, and used `shred` to overwrite and remove a fake secret token file.

## Mistakes / Things to Remember

`mv` can overwrite files if the destination already has a file with the same name.

`mv -i` asks before overwriting.

`mv -n` refuses to overwrite.

`mv -u` only moves when the source is newer than the destination or when the destination is missing.

Normal `rm` fails on directories.

`rm -r` is needed to remove directories recursively.

`rm -rf` is dangerous because it removes recursively and forcefully with fewer safety checks.

`shred` is more secure than `rm`, but it is not perfect on SSDs, snapshots, backups, cloud storage, or journaling filesystems.

## Security Connection

Moving and removing files are basic Linux tasks, but they have direct security impact.

Risks:

```text
overwriting important files
deleting logs or evidence
removing the wrong directory
destroying configuration files
assuming rm securely erases data
```

Controls:

```text
use pwd before destructive commands
use tree or ls before deleting
use TAB autocomplete
use rm -i while practicing
avoid sudo unless required
avoid rm -rf outside disposable lab folders
encrypt sensitive data before removal
```

Detection / Evidence:

```text
logs can show system activity
file trees can prove current structure
command history can help audit actions
```

Recovery Connection:

Backups matter because accidental deletion, overwrite mistakes, or destructive commands can remove important files quickly.

Cloud and infrastructure work requires careful file handling because configuration files, logs, SSH keys, credentials, and backup data may all live on Linux systems.

## Why This Matters for Cloud Architecture

Cloud engineers and security engineers often work inside Linux servers, EC2 instances, containers, and automation environments.

These commands matter later for:

```text
moving configuration files
renaming deployment files
cleaning temporary files
removing old logs
protecting secrets
avoiding destructive mistakes
writing runbooks
supporting incident response
handling backup and recovery workflows
```

Understanding `mv`, `rm`, and `shred` builds safer Linux habits for cloud security and resilience work.