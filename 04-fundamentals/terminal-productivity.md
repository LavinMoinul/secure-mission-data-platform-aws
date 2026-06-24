# Linux Terminal Productivity

## Source

Linux course Section 3:

* Video 14: Mastering the TAB Key
* Video 15: Keyboard Shortcuts
* Video 17: Bash History
* Video 19: Recording Date and Time in History

## TAB Completion

TAB completion helps autocomplete commands, file names, and directory names.

Examples:

```bash
cd /e<TAB>
ls /u<TAB>
man l<TAB>
```

If there are multiple matches, pressing TAB again can show or cycle through possible options.

## Keyboard Shortcuts

Useful terminal shortcuts:

```text
Ctrl + A = move cursor to beginning of line
Ctrl + E = move cursor to end of line
Ctrl + U = cut text before the cursor
Ctrl + K = cut text after the cursor
Ctrl + C = stop the current running command
Ctrl + Z = suspend the current foreground command
Ctrl + L = clear the terminal screen
Ctrl + D = send EOF; at an empty shell prompt, this exits the shell
Ctrl + R = search command history
Up/Down arrows = cycle through command history
```

## Bash History

Bash stores commands that were previously run.

Useful commands:

```bash
history
history | tail
echo $HISTSIZE
echo $HISTFILESIZE
cat ~/.bash_history
```

Important variables:

```text
HISTSIZE = how many commands Bash keeps in memory for the current session
HISTFILESIZE = how many commands are saved to the history file
```

Useful history shortcuts:

```bash
!!
!17
!-7
!ls
```

Meanings:

```text
!! = run the previous command
!17 = run command number 17 from history
!-7 = run the 7th previous command
!ls = run the most recent command that started with "ls"
```

To preview history expansion before running it:

```bash
:p
```

Example:

```bash
!ls:p
```

## Removing or Clearing History

Delete a specific line from history:

```bash
history -d 17
```

Clear the current session history:

```bash
history -c
```

## Running Commands Without Saving to History

If `HISTCONTROL=ignorespace` or `HISTCONTROL=ignoreboth` is enabled, commands that start with a space are not saved to history.

Example:

```bash
 export TEST_SECRET="example"
```

This matters because terminal history can accidentally store sensitive information.

## Adding Date and Time to History

By default, `history` usually shows command numbers and commands, but not timestamps.

To add timestamps:

```bash
HISTTIMEFORMAT="%d/%m/%y %T "
```

To save it permanently:

```bash
echo 'HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bashrc
source ~/.bashrc
```

## Why This Matters Later

Terminal productivity matters because later AWS CLI, SSH, Terraform, Docker, Git, and Linux troubleshooting all depend on fast and accurate command-line usage.

Bash history is useful for repeating commands and auditing past work, but it can also become a security risk if sensitive commands, passwords, tokens, or secrets are saved.

## Commands Practiced

```bash
pwd
whoami
echo $SHELL
type cd
type ls
man man
apropos copy
df -h
ip addr
history
history | tail
echo $HISTSIZE
echo $HISTFILESIZE
```
