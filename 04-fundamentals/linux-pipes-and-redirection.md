# Linux Pipes and Command Redirection

## Purpose

This document summarizes Linux pipes, command redirection, standard streams, `wc`, `cut`, and `tee`.

These concepts matter because Linux server work often involves chaining commands, filtering output, saving command results, separating normal output from errors, and building troubleshooting commands.

## Commands and Operators Covered

```bash
|
wc
>
>>
2>
2>&1
&>
cut
tee
```

## Pipes

A pipe sends the standard output of one command into the standard input of another command.

Basic structure:

```bash
command1 | command2 | command3
```

The output of the command on the left becomes the input of the command on the right.

Example:

```bash
ls -ltr /etc/ | head -n 20 | tail -n 7
```

This command:

```text
1. lists /etc in long format, sorted by modification time in reverse order
2. sends that output into head
3. head keeps the first 20 lines
4. tail keeps the last 7 lines of those first 20 lines
```

The final result lists the last 7 entries from the first 20 entries of the original `ls -ltr /etc/` output.

## Important Pipe Rule

By default, pipes only carry `STDOUT`.

They do not carry `STDERR` unless `STDERR` is redirected into `STDOUT`.

This matters when a command produces errors.

## `wc`

`wc` means word count.

By default, it prints:

```text
line count
word count
byte count
```

Common options:

```bash
wc -l
wc -w
wc -c
wc -m
```

Meanings:

```text
-l = line count
-w = word count
-c = byte count
-m = character count
```

Example:

```bash
cat file.txt | wc -l
```

This counts the number of lines in `file.txt`.

## Command Redirection

Redirection sends command output somewhere other than the terminal.

## `>`

The `>` operator redirects `STDOUT` to a file.

```bash
ls -l /var/log/auth.log > newAuthLogFile.txt
```

This creates `newAuthLogFile.txt` if it does not exist and stores the output inside it.

If the file already exists, `>` overwrites it.

## `>>`

The `>>` operator appends `STDOUT` to a file.

```bash
echo "new line" >> output.txt
```

This adds to the end of `output.txt` instead of overwriting it.

## Standard Streams

Every Linux command has three standard streams:

```text
STDIN  = 0 = standard input
STDOUT = 1 = standard output
STDERR = 2 = standard error
```

Mental model:

```text
STDIN  → command → STDOUT
                 → STDERR
```

Examples:

```text
STDIN  = input the command receives
STDOUT = normal output
STDERR = error output
```

## Redirecting Errors with `2>`

Since `>` redirects `STDOUT` by default, it does not capture errors by itself.

To redirect errors, use `2>`.

Example:

```bash
tail -n 3 /etc/randomFile.txt 2> error.txt
```

This sends the error output into `error.txt`.

## Redirecting `STDOUT` and `STDERR` Together

Use:

```bash
> output.txt 2>&1
```

Example:

```bash
tail -n 2 /etc/passwd /false/directory > output.txt 2>&1
```

This means:

```text
> output.txt redirects STDOUT to output.txt
2>&1 redirects STDERR to the same destination as STDOUT
```

So both normal output and error output go into `output.txt`.

## Valid Command With No Error

Example:

```bash
tail -n 2 /etc/passwd ~/Desktop > output.txt 2>&1
```

If both paths are valid, normal output goes into `output.txt`.

Since there is no error, nothing meaningful is sent through `STDERR`.

## Valid Command With an Error

Example:

```bash
tail -n 2 /etc/passwd /false/directory > output.txt 2>&1
```

In this case:

```text
/etc/passwd is valid
/false/directory is invalid
STDOUT goes into output.txt
STDERR is redirected into the same place as STDOUT
```

So both the normal output and the error message are saved.

## `cut`

`cut` extracts sections from each line of text.

It commonly works with delimiters and fields.

Useful options:

```bash
-d
-f
```

Meanings:

```text
-d = delimiter
-f = fields to display
```

Examples:

```bash
cut -d ":" -f1 /etc/passwd
cut -d ":" -f1-3 /etc/passwd
cut -d ":" -f1,3 /etc/passwd
```

Meanings:

```text
-f1   = display field 1
-f1-3 = display fields 1 through 3
-f1,3 = display fields 1 and 3
```

Example:

```bash
cut -d ":" -f1-3 /etc/passwd
```

In `/etc/passwd`, fields are separated by `:`.

This command displays the first 3 fields from each line.

## `tee`

`tee` reads from `STDIN`, prints to the terminal, and writes to a file.

Without `tee`:

```bash
ls -ltr /etc/
```

prints to the terminal.

With `>`:

```bash
ls -ltr /etc/ > output.txt
```

stores output in a file but does not print it.

With `tee`:

```bash
ls -ltr /etc/ | tee output.txt
```

prints to the terminal and stores the output in `output.txt`.

`tee` can also write to multiple files:

```bash
ls -ltr /etc/ | tee output1.txt output2.txt
```

## `tee` and Errors

This command does not capture the first command’s errors into `tee`:

```bash
ls -ltr /etc/passwd /fake/invalid | tee output.txt 2>&1
```

Why?

Because `2>&1` is applied to `tee`, not to the `ls` command.

The pipe only carries the left command’s `STDOUT` by default.

Correct version:

```bash
ls -ltr /etc/passwd /fake/invalid 2>&1 | tee output.txt
```

This sends both `STDOUT` and `STDERR` from `ls` through the pipe into `tee`.

## Why This Matters for Cloud Architecture

Pipes and redirection are important for cloud, Linux, and security work because they allow command output to be filtered, saved, shared, and inspected.

These skills matter later for:

```text
reading logs
saving troubleshooting output
separating normal output from errors
capturing failed command output
writing shell scripts
building CloudOps runbooks
inspecting system files
analyzing security logs
automating checks
```

## Security Connection

Pipes and redirection matter in cybersecurity because logs and errors often contain evidence.

Useful examples:

```text
save command output for incident notes
capture errors separately from normal output
filter logs for suspicious fields
extract usernames or IDs with cut
save output while still viewing it with tee
```

Risks:

```text
overwriting evidence with >
missing errors because STDERR was not redirected
thinking a pipe captures STDERR when it only captures STDOUT
saving sensitive output into insecure files
```

Controls:

```text
use >> when appending instead of overwriting
use 2> when capturing errors
use 2>&1 when STDOUT and STDERR should be captured together
use tee when output should be viewed and saved
verify output files after redirection
```

## Key Takeaways

`|` sends `STDOUT` from one command into `STDIN` of another command.

`wc` counts lines, words, bytes, or characters.

`>` redirects `STDOUT` and overwrites the destination file.

`>>` redirects `STDOUT` and appends to the destination file.

`2>` redirects `STDERR`.

`2>&1` redirects `STDERR` to the same destination as `STDOUT`.

`cut` extracts fields from lines using delimiters.

`tee` prints output to the terminal and writes it to a file.

Pipes do not carry `STDERR` by default.

To pipe errors into another command, redirect `STDERR` before the pipe.