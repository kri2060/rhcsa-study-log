# Chapter 1 - Linux Basics

## Overview

Today's focus was getting comfortable with the Linux terminal. I learned how to inspect the system, work with files and directories, navigate the Linux filesystem, create links, search for files and text, and edit files using Vim. I also learned how to get help directly from the terminal without relying on external resources.

---

## System Information Commands

### `whoami`

* Displays the username of the currently logged-in user.

* **Syntax**

```bash
whoami
```

---

### `date`

* Displays the current system date and time.

* **Syntax**

```bash
date
```

---

### `timedatectl`

* Shows detailed information about the system clock, timezone, NTP synchronization, and RTC configuration.

* **Syntax**

```bash
timedatectl
```

---

### `ps`

* Lists the currently running processes.

* **Syntax**

```bash
ps [OPTIONS]
```

* **Examples**

```bash
ps
ps -e
ps -f
ps aux
```

* **Useful Options**

| Option | Description                         |
| ------ | ----------------------------------- |
| `-e`   | Show all running processes          |
| `-f`   | Full process information            |
| `aux`  | Display all processes in BSD format |

---

### `passwd`

* Changes the password of the current user.

* **Syntax**

```bash
passwd
```

---

## Getting Help

### `command --help`

* Displays a quick summary of a command's usage and available options.

* **Examples**

```bash
grep --help
find --help
cp --help
```

* **Notes**

Use this when you only need a quick reminder of a command's syntax.

---

### `man`

* Displays the complete manual page for a command.

* **Examples**

```bash
man grep
man find
man passwd
man 5 passwd
```

* **Useful Navigation**

| Key | Action         |
| --- | -------------- |
| `/` | Search         |
| `n` | Next match     |
| `N` | Previous match |
| `g` | Go to top      |
| `G` | Go to bottom   |
| `q` | Quit           |

* **Notes**

Some commands and configuration files have the same name.

```bash
man passwd
```

Displays the command manual.

```bash
man 5 passwd
```

Displays the `/etc/passwd` file format.

---

## File Commands

### `cat`

* Displays the contents of one or more files.

* **Syntax**

```bash
cat [OPTIONS] FILE
```

* **Examples**

```bash
cat file.txt
cat file1 file2
cat > newfile.txt
```

---

### `file`

* Identifies the actual file type by inspecting its contents.

* **Syntax**

```bash
file FILE
```

* **Notes**

Linux identifies files by their contents, not by their filename extension.

---

### `wc`

* Counts lines, words, characters, or bytes.

* **Syntax**

```bash
wc [OPTIONS] FILE
```

* **Useful Options**

| Option | Description      |
| ------ | ---------------- |
| `-l`   | Count lines      |
| `-w`   | Count words      |
| `-c`   | Count bytes      |
| `-m`   | Count characters |

---

### `cp`

* Copies files or directories.

* **Syntax**

```bash
cp [OPTIONS] SOURCE DESTINATION
```

* **Useful Options**

| Option | Description                  |
| ------ | ---------------------------- |
| `-r`   | Copy directories recursively |
| `-i`   | Ask before overwriting       |
| `-v`   | Show copied files            |

---

### `mv`

* Moves or renames files and directories.

* **Syntax**

```bash
mv SOURCE DESTINATION
```

---

### `rm`

* Removes files or directories.

* **Syntax**

```bash
rm [OPTIONS] FILE
```

* **Useful Options**

| Option | Description         |
| ------ | ------------------- |
| `-r`   | Remove recursively  |
| `-f`   | Force removal       |
| `-i`   | Ask before deleting |

* **Notes**

Files deleted with `rm` are not moved to a recycle bin.

---

### `rmdir`

* Removes empty directories.

* **Syntax**

```bash
rmdir DIRECTORY
```

---

### `find`

* Searches recursively for files and directories.

* **Syntax**

```bash
find PATH OPTIONS
```

* **Examples**

```bash
find . -name "start.sh"
find . -type f
find . -type d
find . -size +10M
find . -amin -10
```

* **Useful Options**

| Option    | Description                      |
| --------- | -------------------------------- |
| `-name`   | Search by filename               |
| `-type f` | Files only                       |
| `-type d` | Directories only                 |
| `-size`   | Search by file size              |
| `-mtime`  | Search by modification time      |
| `-amin`   | Search by access time (minutes)  |
| `-exec`   | Execute a command on each result |

* **Notes**

Hide permission errors using:

```bash
find . 2>/dev/null
```

---

### `grep`

* Searches for lines matching a pattern.

* **Syntax**

```bash
grep [OPTIONS] PATTERN FILE
```

* **Examples**

```bash
grep "root" /etc/passwd
grep -i "linux" notes.txt
grep -r "main" .
grep -n "error" logfile
```

* **Useful Options**

| Option | Description                   |
| ------ | ----------------------------- |
| `-i`   | Ignore case                   |
| `-r`   | Search recursively            |
| `-n`   | Show line numbers             |
| `-v`   | Show non-matching lines       |
| `-c`   | Count matching lines          |
| `-l`   | Print matching filenames only |

* **Example with Pipe**

```bash
ps aux | grep firefox
```

---

## Redirection

### `>`

* Redirects output to a file.

* Overwrites the file if it already exists.

* **Example**

```bash
echo "Hello" > file.txt
```

---

### `>>`

* Appends output to the end of a file.

* Creates the file if it doesn't already exist.

* **Example**

```bash
echo "World" >> file.txt
```

* **Difference**

```bash
echo "One" > notes.txt
echo "Two" > notes.txt
```

Result:

```text
Two
```

```bash
echo "One" > notes.txt
echo "Two" >> notes.txt
```

Result:

```text
One
Two
```

---

## Pipes

### `|`

* Sends the output of one command as the input to another command.

* **Example**

```bash
ls -l | less
ps aux | grep ssh
```

---

## Viewing Large Files

### `more`

* Displays text one page at a time.

```bash
more file.txt
```

---

### `less`

* Displays files with forward and backward navigation.

```bash
less file.txt
```

* **Useful Keys**

| Key | Action          |
| --- | --------------- |
| `/` | Search          |
| `n` | Next match      |
| `g` | Go to beginning |
| `G` | Go to end       |
| `q` | Quit            |

---

## Vim Basics

| Command | Description           |
| ------- | --------------------- |
| `i`     | Enter Insert mode     |
| `Esc`   | Return to Normal mode |
| `:w`    | Save                  |
| `:q`    | Quit                  |
| `:wq`   | Save and quit         |
| `:q!`   | Quit without saving   |

---

## Linux Filesystem Hierarchy

Linux organizes everything under a single directory tree starting at the root directory (`/`).

| Directory | Purpose                           |
| --------- | --------------------------------- |
| `/`       | Root of the filesystem            |
| `/home`   | User home directories             |
| `/etc`    | System configuration files        |
| `/bin`    | Essential user commands           |
| `/usr`    | User applications                 |
| `/var`    | Variable data (logs, mail, cache) |
| `/tmp`    | Temporary files                   |

> **Remember:** In Linux, almost everything is treated as a file.

---

## Links

### Hard Link

* Points directly to the inode.
* Shares the same data as the original file.
* Continues working even if the original filename is deleted.
* Cannot span different filesystems.

```bash
ln file.txt hardlink.txt
```

---

### Soft Link (Symbolic Link)

* Points to another file by its pathname.
* Similar to a Windows shortcut.
* Can span different filesystems.
* Breaks if the original file is removed.

```bash
ln -s file.txt symlink.txt
```

---

## Key Takeaways

* Linux is built around many small tools that work well together.
* Use `--help` for quick references and `man` for detailed documentation.
* Learn common options instead of trying to memorize every available flag.
* Combine commands with pipes to build powerful workflows.
* `>` overwrites files, while `>>` appends to them.
* `find` and `grep` are two of the most frequently used commands in Linux.
* Understanding the Linux filesystem hierarchy is essential for system administration.

