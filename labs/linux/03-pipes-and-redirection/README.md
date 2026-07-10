# Section 5 Lab: Pipes and Command Redirection

## Purpose

This lab practiced Linux pipes, command redirection, standard streams, `wc`, `cut`, and `tee` inside a safe local Ubuntu VM workspace.

The goal was to understand how command output moves through the shell, how normal output and errors behave differently, and how to save or inspect command results for later troubleshooting.

## Lab Environment

Lab directory:

```bash
~/section5-pipes-redirection-lab
```

Confirmed working directory with:

```bash
pwd
```

The lab was completed without `sudo`.

## Starting Structure

```text
section5-pipes-redirection-lab/
├── data/
│   └── users.txt
├── errors/
├── logs/
│   ├── access.log
│   └── app.log
└── outputs/
```

The starting structure was verified with:

```bash
tree
cat data/users.txt
```

## Commands and Operators Practiced

```bash
pwd
tree
cat
head
tail
wc
cut
tee
ls
echo
>
>>
2>
2>&1
|
```

## Standard Streams

Every Linux command has three standard streams:

```text
STDIN  = 0 = standard input
STDOUT = 1 = standard output
STDERR = 2 = standard error
```

A pipe sends the left command's `STDOUT` into the right command's `STDIN`.

By default, pipes do not carry `STDERR`.

## Part 1: Pipes and `wc`

Viewed the contents of `logs/app.log`:

```bash
cat logs/app.log
```

Counted lines:

```bash
wc -l logs/app.log
```

Counted words:

```bash
wc -w logs/app.log
```

Tested a pipe chain:

```bash
tail -n 5 logs/app.log | head -n 1
```

This command takes the last 5 lines of `logs/app.log`, then sends that output into `head`, which prints the first line from those 5 lines.

## Takeaways

`wc` shows line count, word count, and byte count by default.

Useful `wc` options:

```text
-l = lines only
-w = words only
-c = bytes only
-m = characters only
```

A pipe sends output from the left command as input for the right command.

## Part 2: `>` and `>>`

Redirected command output into a file:

```bash
ls -ltr /etc/ | tail -n 2 > outputs/appsummary.txt
```

Verified the file:

```bash
cat outputs/appsummary.txt
```

Overwrote the same file with different output:

```bash
ls -ltr /etc/ | tail -n 5 > outputs/appsummary.txt
```

Appended new content:

```bash
echo "bleh" >> outputs/appsummary.txt
```

Verified the result:

```bash
cat outputs/appsummary.txt
```

## Takeaways

`>` redirects `STDOUT` into a file and overwrites the file if it already has content.

`>>` redirects `STDOUT` into a file and appends to the end instead of overwriting.

## Part 3: `STDOUT` vs `STDERR`

Redirected normal output:

```bash
ls /home/lavin/Desktop/ > outputs/stdout-only2.txt
```

Generated an error:

```bash
ls asikdfo/asdgjksrdfkgljs
```

Tried redirecting an error with `>`:

```bash
ls asikdfo/asdgjksrdfkgljs > tearswar.txt
```

This did not capture the error because `>` redirects only `STDOUT` by default.

Redirected the error correctly with `2>`:

```bash
ls asikdfo/asdgjksrdfkgljs 2> tearswar.txt
```

Moved the captured error file into the errors directory:

```bash
mv tearswar.txt errors/error-only.txt
```

Verified the captured error:

```bash
cat errors/error-only.txt
```

## Takeaways

`>` redirects file descriptor 1, which is `STDOUT`.

Errors use file descriptor 2, which is `STDERR`.

To redirect errors, use:

```bash
2>
```

## Part 4: Redirecting `STDOUT` and `STDERR` Together

Used one valid path and one invalid path, then redirected both normal output and errors into one file:

```bash
cat slkdjfgklsdfg/WTF /var/log/auth.log 2>&1 | tail -n 5 > outputs/combined-streams.txt
```

Verified the result:

```bash
cat outputs/combined-streams.txt
```

## Takeaways

`2>&1` means redirect `STDERR` to the same destination as `STDOUT`.

In plain English:

```text
Send error output to wherever normal output is currently going.
```

## Part 5: `cut`

Used `cut` with colon-separated data in `data/users.txt`.

Showed field 1:

```bash
cut -d ":" -f1 data/users.txt
```

Showed fields 1 through 3:

```bash
cut -d ":" -f1-3 data/users.txt
```

Showed fields 1 and 3:

```bash
cut -d ":" -f1,3 data/users.txt
```

## Takeaways

`cut` extracts sections from each line.

`-d` specifies the delimiter.

`-f` specifies which fields to display.

Example:

```bash
cut -d ":" -f1-3 data/users.txt
```

This uses `:` as the delimiter and prints fields 1 through 3 from each line.

## Part 6: `tee`

Used `tee` to print output to the terminal and save it to a file:

```bash
ls -ltr outputs | tee outputs/tee-output.txt
```

Used `tee` to write output into two files:

```bash
cat outputs/tee-output.txt | tee tee-one.txt tee-two.txt
```

Verified output files:

```bash
tree outputs/
cat outputs/tee-output.txt
```

## Takeaways

`>` saves output to a file but does not print it to the terminal.

`tee` prints output to the terminal and saves it to a file.

`tee` can also write the same output to multiple files.

## Part 7: `tee` with Errors

Ran a command with one valid path and one invalid path:

```bash
ls -ltr outputs/ fake/directory | tee tee-with-errors.txt
```

The error printed to the terminal, but it was not saved by `tee` because the pipe only carried `STDOUT`.

Verified the file:

```bash
cat tee-with-errors.txt
```

Then ran the corrected version:

```bash
ls -ltr outputs/ fake/directory 2>&1 | tee tee-with-errors.txt
```

Verified the file:

```bash
cat tee-with-errors.txt
```

## Takeaways

This command does not capture the first command's errors into `tee`:

```bash
command1 | tee file.txt 2>&1
```

That is because `2>&1` applies to `tee`, not to `command1`.

Correct placement:

```bash
command1 2>&1 | tee file.txt
```

This sends both `STDOUT` and `STDERR` from `command1` into `tee`.

## Final Structure

Final lab structure:

```text
section5-pipes-redirection-lab/
├── data/
│   └── users.txt
├── errors/
│   └── error-only.txt
├── logs/
│   ├── access.log
│   └── app.log
├── outputs/
│   ├── appsummary.txt
│   ├── combined-streams.txt
│   ├── stdout-only.txt
│   ├── stdout-only2.txt
│   └── tee-output.txt
├── tee-one.txt
├── tee-two.txt
└── tee-with-errors.txt
```

## Lab Questions and Answers

### 1. What does a pipe send from the left command to the right command?

It sends output from the left command as input for the right command.

More specifically, it sends the left command's `STDOUT` into the right command's `STDIN`.

### 2. Does a pipe carry `STDERR` by default?

No.

To include `STDERR`, redirect it into `STDOUT` first with `2>&1`.

### 3. What does `wc` show by default?

`wc` shows:

```text
line count
word count
byte count
```

### 4. What is the difference between `wc -l`, `wc -w`, `wc -c`, and `wc -m`?

```text
wc -l = lines only
wc -w = words only
wc -c = bytes only
wc -m = characters only
```

### 5. What does `>` do?

`>` redirects `STDOUT` into a file.

If the file already has content, it overwrites the file.

### 6. What does `>>` do?

`>>` redirects `STDOUT` into a file and appends to the end instead of overwriting.

### 7. Why does `>` not capture errors by default?

Because `>` redirects `STDOUT`, which is file descriptor 1.

Errors use `STDERR`, which is file descriptor 2.

### 8. What does `2>` do?

`2>` redirects `STDERR` into a file.

### 9. What does `2>&1` mean in plain English?

It means redirect error output to the same destination as regular output.

### 10. Why does `command1 | tee file.txt 2>&1` not capture `command1`'s errors?

Because `2>&1` applies to `tee`, not to `command1`.

The pipe only carries `command1`'s `STDOUT` by default.

### 11. What is the correct placement if you want `tee` to receive both `STDOUT` and `STDERR` from `command1`?

Use:

```bash
command1 2>&1 | tee file.txt
```

The `2>&1` must come before the pipe so `STDERR` from `command1` gets redirected into the pipe.

### 12. What does `cut -d ":" -f1-3` do?

It uses `:` as the delimiter and prints fields 1 through 3 from each line.

### 13. What does `tee` do that `>` does not?

`>` stores output in a file only.

`tee` prints output to the terminal and stores it in a file.

## Security and Cloud Connection

This lab connects to Linux server, CloudOps, and incident response work because real troubleshooting often requires capturing both normal output and error output.

Examples:

```text
saving command output during troubleshooting
capturing errors from failed commands
building shell scripts that log failures
saving evidence during incident response
viewing logs while also storing a copy
extracting useful fields from structured files
```

If only `STDOUT` is saved, the actual failure may be missed because errors often go through `STDERR`.

## Project Connection

These skills will be reused later when working with:

```text
EC2 troubleshooting
SSH sessions
Linux log review
CloudWatch and CloudTrail workflows
shell scripting
cron job output
incident notes
runbooks
automation checks
```

Understanding pipes, streams, and redirection is part of building reliable troubleshooting habits for cloud security and resilience work.