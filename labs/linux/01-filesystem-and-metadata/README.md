## Lab: File Viewing and File Management

### Goal

Practice viewing files, creating files/directories, copying files, observing overwrite behavior, and monitoring changing files.

### Commands Practiced

- `mkdir`
- `mkdir -p`
- `touch`
- `tree`
- `cat`
- `cat -n`
- `less`
- `head`
- `tail`
- `tail -f`
- `watch`
- `cp`
- `cp -i`
- `cp -r`
- `>`
- `>>`

### What I Did

Created a lab workspace called `section5-file-practice` with directories for docs, logs, backups, and project configuration.

Created files including:

- `docs/notes.txt`
- `logs/app.log`
- `logs/auth.log`
- `projects/app/config/settings.conf`

Added content to files, viewed contents with `cat`, combined files into `combined.txt`, tested `head` and `tail`, monitored a growing log with `tail -f`, monitored a directory with `watch`, and practiced copying files/directories with `cp`.

### Key Takeaways

- `cat` displays the full file contents.
- `cat -n` displays file contents with line numbers.
- `less` is better than `cat` for larger files because it lets you scroll/search page by page.
- `head` shows the beginning of a file.
- `tail` shows the end of a file.
- `tail -f` follows a file as it grows, which is useful for watching logs.
- `watch` repeatedly runs a command and refreshes the output.
- `cp` overwrites files by default.
- `cp -i` asks before overwriting.
- `cp -r` is needed to recursively copy directories.
- `>` overwrites or creates a file.
- `>>` appends to the end of a file.

### Mistakes / Things to Remember

- Using `>` multiple times overwrites the file each time.
- Use `>>` when adding new lines without deleting existing content.
- `cat notes.txt` failed because `notes.txt` was inside `docs/`, so the correct path was `docs/notes.txt`.
- Normal `cp` failed on a directory because recursive mode was not specified.

### Project Connection

These commands matter for future Linux server and cloud work because cloud engineers often need to inspect logs, monitor changing files, copy configuration files, safely back up files, and understand paths while working on EC2 or other Linux-based systems.

