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

### 9. `absolute path` vs `relative path` — Make Directory

- An `absolute path` starts from / and works from anywhere: /etc/nginx/nginx.conf.
- A `relative path` starts from the folder you're in now: if you're in /etc, then nginx/nginx.conf points to the same file.