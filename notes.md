# DevOps Journal — Linux Week 1

## Day 1: Basic Linux Commands

### 1. `pwd` — Print Working Directory

**What it does:** Shows the absolute path of the directory I'm currently in.

```bash
pwd
```

**Example output:**
```text
/home/ubuntu
```

**When to use it:** To check my current location in the filesystem.

### 2. `ls` — List Directory Contents

**What it does:** Lists files and directories in the current directory.

```bash
ls
ls -l
ls -la
ls -lah
```

- `ls`: Lists visible files and directories.
- `ls -l`: Shows detailed information, including permissions and ownership.
- `ls -la`: Also shows hidden files.
- `ls -lah`: three options combined (-l long format, -a show hidden files, -h human-readable sizes) 

**When to use it:** To inspect files and directories on a server.

### 3. `cd` — Change Directory

**What it does:** Moves me into another directory.

```bash
cd /etc
cd ..
cd ~
```

- `cd /etc`: Moves into `/etc`.
- `cd ..`: Moves one directory up.
- `cd ~`: Returns to my home directory.

**When to use it:** To navigate the Linux filesystem.

### 4. `mkdir` — Make Directory

**What it does:** Creates a new directory.

```bash
mkdir projects
mkdir -p projects/website/logs
```

- `mkdir projects`: Creates a directory named `projects`.
- `mkdir -p projects/website/logs`: Creates nested directories if they don't already exist.

**When to use it:** To create directories for applications, configuration files, or logs.

### 5. `touch` — Create an Empty File

**What it does:** Creates an empty file if it doesn't exist. If it already exists, it updates its modification timestamp.

```bash
touch notes.txt
```

**When to use it:** To create a file before editing it.

### 6. `cat` — Display File Contents

**What it does:** Prints the contents of a file to the terminal.

```bash
cat notes.txt
```

**When to use it:** To quickly read configuration files, scripts, or notes.

### 7. `grep` — Search Text

**What it does:** Searches text for a specified pattern.

```bash
grep "error" application.log
grep -i "error" application.log
```

- `grep "error"`: Searches for the exact lowercase text `error`.
- `grep -i "error"`: Ignores letter case.

**When to use it:** To find errors in application logs or search configuration files.

### 8. `sudo` — Run a Command with Elevated Privileges

**What it does:** Runs a command with elevated privileges, usually as the root user.

```bash
sudo apt update
```

**When to use it:** When an administrative task requires permissions that my normal user doesn't have.

**Important:** I should understand the command before running it with `sudo`.

### 9. `absolute path` vs `relative path`

- An `absolute path` starts from / and works from anywhere: /etc/nginx/nginx.conf.
- A `relative path` starts from the folder you're in now: if you're in /etc, then nginx/nginx.conf points to the same file.

## Day 2: Filesystem and text processing

### 1. `awk` — Text Processing

**What it does:** Searches, filters, and processes text, especially column-based data.

**Syntax:**
```bash
awk 'pattern { action }' filename
```

**Examples:**
```bash
awk '{print $1}' file.txt
```
Prints the first column of each line.

```bash
awk '{print $1, $3}' file.txt
```
Prints the first and third columns.

```bash
awk -F: '{print $1}' /etc/passwd
```
Uses `:` as the field separator and prints the first field (usernames).

```bash
awk '/error/ {print}' app.log
```
Prints lines containing `error`.

**Key concepts:**
- `$0` — the entire line.
- `$1`, `$2` — the first and second fields.
- `-F` — specifies the field separator.

**When to use it:** Extracting columns, filtering logs, and processing command output in Linux and DevOps.


### 2. `cp -r` — Copy Directories Recursively

**What it does:** Copies a directory and all its contents, including subdirectories and files.

**Syntax:**
```bash
cp -r source_directory destination
```

**Examples:**

```bash
cp -r website/ backup/
```
Copies the `website` directory and its contents into `backup/`.

```bash
cp -r website/ /opt/apps/
```
Copies the `website` directory into `/opt/apps/`.

```bash
cp -r website/ website_backup/
```
Creates a copy named `website_backup`.

**Key concept:**
- `cp` — copies files and directories.
- `-r` — recursively copies directories and their contents.

**When to use it:** Backing up application directories, copying project files, or moving configuration directories between locations.

**Note:** `cp` copies files; to move them, use `mv`.

### 3. `mv` — Move or Rename Files

**What it does:** Moves files and directories to another location or renames them.

**Syntax:**
```bash
mv source destination
```

**Examples:**

```bash
mv file.txt /home/ubuntu/
```
Moves `file.txt` into `/home/ubuntu/`.

```bash
mv old_name.txt new_name.txt
```
Renames `old_name.txt` to `new_name.txt`.

```bash
mv website/ /opt/apps/
```
Moves the `website` directory into `/opt/apps/`, including its contents.

**Key concept:**
- `mv` — moves or renames files and directories.
- Unlike `cp`, it does not create a separate copy.

**When to use it:** Organizing files, renaming configuration files, or moving application directories on a Linux server.

**Note:** Be careful: `mv` can overwrite an existing destination file. Use `mv -i` to ask for confirmation before overwriting.

### 4. `rm -r` — Remove Directories Recursively

**What it does:** Deletes a directory and all its contents, including files and subdirectories.

**Syntax:**
```bash
rm -r directory
```

**Examples:**

```bash
rm -r old_project/
```
Deletes `old_project/` and everything inside it.

```bash
rm -ri old_project/
```
Prompts for confirmation as it removes files and directories.

```bash
rm file.txt
```
Deletes a file without the `-r` option.

**Key concepts:**
- `rm` — removes files.
- `-r` — recursively removes directories and their contents.
- `-i` — asks for confirmation before each removal.

**When to use it:** Removing obsolete project directories, temporary files, or unwanted application files on a Linux server.

**Warning:** Deleted files usually cannot be recovered easily. Always double-check the path before running `rm -r`. Avoid `rm -rf` unless you fully understand the consequences.

### 5. `ln -s` — Create a Symbolic Link

**What it does:** Creates a link that points to another file or directory.

**Syntax:**
```bash
ln -s target link_name
```

**Example:**
```bash
ln -s ~/lab/app ~/app-link
```
Creates `app-link` as a symbolic link pointing to `~/lab/app`.

**Symbolic link vs. hard link**

| Symbolic link (symlink) | Hard link |
|---|---|
| Points to a file path | Points to the same inode (file data) |
| Can link to directories | Usually cannot link to directories |
| Can cross filesystems | Must be on the same filesystem |
| Breaks if the target path is removed or becomes inaccessible | Still works if the original filename is deleted, as long as another hard link remains |

**Examples:**
```bash
ln -s file.txt shortcut
ln file.txt hardlink
```

**When to use it:** Symlinks are useful for shortcuts, shared application paths, and pointing to the current version of a deployment.

**Useful command:**
```bash
ls -l
```
Shows symbolic links and the paths they point to.

### 6. `uniq -c`

- `uniq` removes consecutive duplicate lines.
- `-c` displays the number of occurrences of each consecutive group of identical lines.
- **Important:** `uniq` only detects adjacent duplicates. Use `sort` first to group identical lines together.

**Example:**
```bash
sort file.txt | uniq -c
```

**Input:**
```text
apple
banana
apple
apple
```

**Output:**
```text
      3 apple
      1 banana
```

**Common use:** Count repeated values, such as IP addresses in web server logs.

```bash
awk '{print $1}' access.log | sort | uniq -c
```

This extracts the first field from each log line, sorts the values, and counts how many times each value appears.