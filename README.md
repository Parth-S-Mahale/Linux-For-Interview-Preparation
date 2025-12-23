# 🐧 Linux Fundamentals - Interview Preparation Guide

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Security](https://img.shields.io/badge/Cyber_Security-000000?style=for-the-badge&logo=hackaday&logoColor=white)

> **A comprehensive guide to mastering Linux fundamentals for cybersecurity professionals and system administrators. Perfect for technical interviews and real-world scenarios.**

---

## 📋 Table of Contents

- [Overview](#overview)
- [Part 1: Basic Commands](#part-1-basic-commands)
- [Part 2: SSH & File Systems](#part-2-ssh--file-systems)
- [Part 3: Common Utilities](#part-3-common-utilities)
- [Interview Preparation](#interview-preparation)
- [Quick Reference](#quick-reference)
- [Contributing](#contributing)

---

## 🎯 Overview

Many servers and security tools use Linux. This guide covers essential Linux operating system skills critical in cybersecurity, including:

- **Navigation & File Management** - Master the filesystem hierarchy
- **Remote Access** - SSH and secure connections
- **Text Processing** - Grep, sed, awk for log analysis
- **System Administration** - User management, permissions, processes
- **Security Fundamentals** - File permissions, secure file transfer

---

## 🚀 Part 1: Basic Commands

*Embark on the journey of learning Linux fundamentals. Run essential commands on an interactive terminal.*

### Navigation Commands

#### `pwd` - Print Working Directory
Shows your current location in the filesystem.

```bash
$ pwd
/home/user/documents
```

**Interview Tip:** Always verify your current directory before running commands, especially `rm` or `mv`.

---

#### `ls` - List Directory Contents

```bash
# Basic listing
$ ls

# Long format with details
$ ls -l

# Show hidden files
$ ls -a

# Human-readable sizes, sorted by modification time
$ ls -lhrt

# List only directories
$ ls -d */
```

**Common Interview Question:** *"What does `ls -la` show?"*
- **Answer:** All files including hidden ones (`-a`) in long format (`-l`) showing permissions, owner, size, and timestamp.

---

#### `cd` - Change Directory

```bash
# Go to home directory
$ cd ~
$ cd

# Go to previous directory
$ cd -

# Go up one level
$ cd ..

# Go up two levels
$ cd ../..

# Absolute path
$ cd /var/log
```

---

### File Operations

#### `cat` - Concatenate and Display Files

```bash
# Display file content
$ cat file.txt

# Display multiple files
$ cat file1.txt file2.txt

# Show line numbers
$ cat -n file.txt

# Create a new file (Ctrl+D to save)
$ cat > newfile.txt
```

---

#### `touch` - Create Empty Files

```bash
# Create a single file
$ touch file.txt

# Create multiple files
$ touch file1.txt file2.txt file3.txt

# Update timestamp of existing file
$ touch existing_file.txt
```

---

#### `mkdir` - Make Directory

```bash
# Create single directory
$ mkdir projects

# Create nested directories
$ mkdir -p projects/linux/scripts

# Create multiple directories
$ mkdir dir1 dir2 dir3
```

---

#### `cp` - Copy Files/Directories

```bash
# Copy file
$ cp source.txt destination.txt

# Copy directory recursively
$ cp -r source_dir/ dest_dir/

# Copy with verbose output
$ cp -v file.txt backup/

# Preserve attributes (permissions, timestamps)
$ cp -p file.txt backup/
```

---

#### `mv` - Move/Rename Files

```bash
# Rename file
$ mv oldname.txt newname.txt

# Move file to directory
$ mv file.txt /home/user/documents/

# Move multiple files
$ mv file1.txt file2.txt directory/
```

---

#### `rm` - Remove Files/Directories

```bash
# Remove file
$ rm file.txt

# Remove directory and contents
$ rm -r directory/

# Force remove without prompt
$ rm -f file.txt

# Interactive mode (ask before deletion)
$ rm -i file.txt

# Remove empty directory
$ rmdir empty_directory/
```

**⚠️ Warning:** `rm -rf /` can delete your entire system. Always double-check paths!

---

### Viewing File Contents

#### `less` and `more` - Page Through Files

```bash
# View large files
$ less /var/log/syslog

# Navigation in less:
# Space - Next page
# b - Previous page
# / - Search forward
# ? - Search backward
# q - Quit
```

---

#### `head` and `tail` - View File Beginning/End

```bash
# First 10 lines (default)
$ head file.txt

# First 20 lines
$ head -n 20 file.txt

# Last 10 lines
$ tail file.txt

# Follow file updates (log monitoring)
$ tail -f /var/log/syslog

# Last 50 lines and follow
$ tail -n 50 -f application.log
```

**Interview Scenario:** *"How do you monitor a live log file?"*
- **Answer:** `tail -f /var/log/application.log`

---

## 🔐 Part 2: SSH & File Systems

*Continue your Linux journey with SSH, advanced commands, and file system interaction.*

### SSH - Secure Shell

#### Basic Connection

```bash
# Connect to remote server
$ ssh username@192.168.1.100

# Specify port
$ ssh -p 2222 username@server.com

# Use identity file (private key)
$ ssh -i ~/.ssh/id_rsa username@server.com
```

---

#### SSH Key Generation

```bash
# Generate SSH key pair
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Generate ED25519 key (more secure)
$ ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy public key to server
$ ssh-copy-id username@server.com
```

**Interview Question:** *"What's the difference between SSH and Telnet?"*
- **Answer:** SSH encrypts all traffic (including passwords), while Telnet sends data in plain text. SSH uses port 22 by default, Telnet uses port 23.

---

### SCP - Secure Copy

```bash
# Copy file to remote server
$ scp file.txt username@server.com:/home/username/

# Copy file from remote server
$ scp username@server.com:/home/username/file.txt ./

# Copy directory recursively
$ scp -r directory/ username@server.com:/path/

# Specify port
$ scp -P 2222 file.txt username@server.com:/path/
```

---

### File Permissions

#### Understanding Permissions

```
-rwxr-xr-x  1 user group 4096 Dec 23 10:00 file.txt
│││││││││
│││││││└┴─ Others: r-x (read, execute)
││││││└──── Group: r-x (read, execute)
│││└┴┴───── Owner: rwx (read, write, execute)
││└────────── Number of links
│└─────────── File type (- = file, d = directory, l = link)
```

---

#### `chmod` - Change Permissions

```bash
# Numeric method
$ chmod 755 script.sh    # rwxr-xr-x
$ chmod 644 file.txt     # rw-r--r--
$ chmod 600 private.key  # rw-------

# Symbolic method
$ chmod u+x script.sh    # Add execute for user
$ chmod g-w file.txt     # Remove write for group
$ chmod o-r secret.txt   # Remove read for others
$ chmod a+x script.sh    # Add execute for all

# Recursive
$ chmod -R 755 directory/
```

**Common Permission Values:**
- `777` (rwxrwxrwx) - Full access for everyone (⚠️ Security risk!)
- `755` (rwxr-xr-x) - Standard for directories and executables
- `644` (rw-r--r--) - Standard for files
- `600` (rw-------) - Private files (like SSH keys)
- `700` (rwx------) - Private directories

---

#### `chown` - Change Ownership

```bash
# Change owner
$ chown user file.txt

# Change owner and group
$ chown user:group file.txt

# Recursive change
$ chown -R user:group directory/
```

---

### Finding Files

#### `find` - Search for Files

```bash
# Find by name
$ find /home -name "*.txt"

# Find by type (f=file, d=directory)
$ find /var -type f -name "*.log"

# Find by size
$ find / -size +100M

# Find by modification time (last 7 days)
$ find /home -mtime -7

# Find and execute command
$ find . -name "*.tmp" -exec rm {} \;

# Find files with specific permissions
$ find / -perm 777
```

**Interview Question:** *"How do you find all files larger than 1GB modified in the last 24 hours?"*
```bash
$ find /path -type f -size +1G -mtime -1
```

---

#### `locate` - Fast File Search

```bash
# Quick search (uses database)
$ locate filename

# Update database
$ sudo updatedb

# Case-insensitive search
$ locate -i filename
```

---

### Disk Usage

#### `df` - Disk Free Space

```bash
# Show disk usage
$ df -h

# Show inode usage
$ df -i
```

---

#### `du` - Directory Usage

```bash
# Show directory size
$ du -sh directory/

# Show size of all subdirectories
$ du -h --max-depth=1 /var/

# Sort by size
$ du -sh * | sort -hr
```

---

## 🛠️ Part 3: Common Utilities

*Power-up your Linux skills with utilities for day-to-day tasks.*

### Text Processing

#### `grep` - Search Text Patterns

```bash
# Basic search
$ grep "error" /var/log/syslog

# Case-insensitive search
$ grep -i "warning" log.txt

# Recursive search in directories
$ grep -r "TODO" /home/user/projects/

# Show line numbers
$ grep -n "error" file.txt

# Invert match (show lines NOT matching)
$ grep -v "success" log.txt

# Count matches
$ grep -c "error" log.txt

# Show context (3 lines before and after)
$ grep -C 3 "error" log.txt

# Multiple patterns
$ grep -E "error|warning|critical" log.txt
```

**Interview Scenario:** *"Find all failed login attempts in auth.log"*
```bash
$ grep "Failed password" /var/log/auth.log
```

---

#### `awk` - Pattern Scanning and Processing

```bash
# Print specific columns
$ awk '{print $1}' file.txt

# Print first and third columns
$ awk '{print $1, $3}' file.txt

# Use custom delimiter
$ awk -F: '{print $1}' /etc/passwd

# Print lines where column 3 > 100
$ awk '$3 > 100' file.txt

# Sum values in column 2
$ awk '{sum += $2} END {print sum}' numbers.txt
```

**Example:** Extract usernames from /etc/passwd
```bash
$ awk -F: '{print $1}' /etc/passwd
```

---

#### `sed` - Stream Editor

```bash
# Replace first occurrence in each line
$ sed 's/old/new/' file.txt

# Replace all occurrences
$ sed 's/old/new/g' file.txt

# Delete lines containing pattern
$ sed '/pattern/d' file.txt

# Print specific line (line 5)
$ sed -n '5p' file.txt

# Delete lines 2-4
$ sed '2,4d' file.txt

# In-place editing
$ sed -i 's/old/new/g' file.txt
```

---

### Process Management

#### `ps` - Process Status

```bash
# Show all processes
$ ps aux

# Show process tree
$ ps auxf

# Filter by user
$ ps -u username

# Find specific process
$ ps aux | grep nginx
```

---

#### `top` / `htop` - Interactive Process Viewer

```bash
# Real-time process monitoring
$ top

# Better alternative (if installed)
$ htop

# Sort by memory usage in top: Press M
# Sort by CPU usage in top: Press P
# Kill process in top: Press k, then enter PID
```

---

#### `kill` - Terminate Processes

```bash
# Graceful termination
$ kill 1234

# Force kill
$ kill -9 1234

# Kill by name
$ pkill processname

# Kill all processes by name
$ killall processname
```

**Interview Question:** *"What's the difference between `kill` and `kill -9`?"*
- **Answer:** `kill` (SIGTERM) allows graceful shutdown; the process can catch the signal and clean up. `kill -9` (SIGKILL) forcefully terminates immediately without cleanup.

---

### System Information

#### `uname` - System Information

```bash
# Kernel name
$ uname

# All information
$ uname -a

# Kernel version
$ uname -r
```

---

#### `uptime` - System Uptime

```bash
$ uptime
# Output: 10:30:15 up 5 days, 3:25, 2 users, load average: 0.52, 0.58, 0.59
```

---

#### `whoami` / `who` - User Information

```bash
# Current user
$ whoami

# Logged in users
$ who

# Detailed user info
$ w
```

---

### Networking

#### `ping` - Test Connectivity

```bash
# Basic ping
$ ping google.com

# Ping with count
$ ping -c 4 google.com
```

---

#### `curl` / `wget` - Download Files

```bash
# Download with curl
$ curl -O https://example.com/file.zip

# Download with wget
$ wget https://example.com/file.zip

# Follow redirects with curl
$ curl -L https://example.com/redirect
```

---

#### `netstat` / `ss` - Network Statistics

```bash
# Show all connections
$ netstat -tuln

# Modern alternative
$ ss -tuln

# Show which process is using port 80
$ sudo netstat -tulpn | grep :80
```

---

### Archiving & Compression

#### `tar` - Archive Files

```bash
# Create archive
$ tar -cvf archive.tar directory/

# Create compressed archive (gzip)
$ tar -czvf archive.tar.gz directory/

# Extract archive
$ tar -xvf archive.tar

# Extract compressed archive
$ tar -xzvf archive.tar.gz

# List archive contents
$ tar -tvf archive.tar
```

**Flags explained:**
- `c` - Create
- `x` - Extract
- `v` - Verbose
- `f` - File
- `z` - Gzip compression
- `j` - Bzip2 compression

---

#### `zip` / `unzip`

```bash
# Create zip archive
$ zip -r archive.zip directory/

# Extract zip
$ unzip archive.zip

# List zip contents
$ unzip -l archive.zip
```

---

### User Management

#### `useradd` / `adduser` - Create User

```bash
# Add user (basic)
$ sudo useradd newuser

# Add user with home directory
$ sudo useradd -m newuser

# Add user with specific shell
$ sudo useradd -s /bin/bash newuser
```

---

#### `passwd` - Change Password

```bash
# Change your password
$ passwd

# Change another user's password (as root)
$ sudo passwd username
```

---

#### `sudo` - Execute as Superuser

```bash
# Run command as root
$ sudo command

# Switch to root shell
$ sudo -i

# Run command as another user
$ sudo -u username command
```

---

## 💼 Interview Preparation

### Common Linux Interview Questions

#### 1. **What is the Linux kernel?**
The kernel is the core component of Linux that manages system resources, hardware, and provides essential services to applications.

---

#### 2. **Explain the Linux directory structure**

```
/           → Root directory
/home       → User home directories
/root       → Root user's home
/etc        → Configuration files
/var        → Variable data (logs, databases)
/tmp        → Temporary files
/usr        → User programs and data
/bin        → Essential user binaries
/sbin       → System binaries
/lib        → Shared libraries
/dev        → Device files
/proc       → Process information (virtual filesystem)
```

---

#### 3. **What's the difference between hard link and soft link?**

```bash
# Hard link (points to inode directly)
$ ln file.txt hardlink.txt

# Soft link / Symbolic link (points to filename)
$ ln -s file.txt softlink.txt
```

- **Hard Link:** Same inode, cannot cross filesystems, cannot link directories
- **Soft Link:** Different inode, can cross filesystems, can link directories

---

#### 4. **How do you check system logs?**

```bash
# System logs
$ sudo tail -f /var/log/syslog       # Debian/Ubuntu
$ sudo tail -f /var/log/messages     # RHEL/CentOS

# Authentication logs
$ sudo tail -f /var/log/auth.log

# Using journalctl (systemd)
$ sudo journalctl -f
$ sudo journalctl -u nginx.service
```

---

#### 5. **How do you find which process is using a port?**

```bash
# Method 1: netstat
$ sudo netstat -tulpn | grep :80

# Method 2: ss
$ sudo ss -tulpn | grep :80

# Method 3: lsof
$ sudo lsof -i :80
```

---

### Practical Scenarios

#### Scenario 1: Server is Running Slow
```bash
# 1. Check CPU and memory usage
$ top

# 2. Check disk usage
$ df -h

# 3. Check disk I/O
$ iostat

# 4. Check running processes
$ ps aux --sort=-%mem | head -10

# 5. Check system load
$ uptime
```

---

#### Scenario 2: Application Won't Start
```bash
# 1. Check if port is already in use
$ sudo netstat -tulpn | grep :8080

# 2. Check application logs
$ tail -f /var/log/application.log

# 3. Check system resources
$ df -h && free -m

# 4. Check file permissions
$ ls -la /path/to/application

# 5. Test network connectivity
$ ping -c 4 database-server.com
```

---

#### Scenario 3: Find and Remove Old Log Files
```bash
# Find files older than 30 days
$ find /var/log -name "*.log" -mtime +30

# Delete files older than 30 days
$ find /var/log -name "*.log" -mtime +30 -delete

# Compress old logs instead
$ find /var/log -name "*.log" -mtime +30 -exec gzip {} \;
```

---

## 📚 Quick Reference

### Essential Command Cheat Sheet

| Command | Description | Example |
|---------|-------------|---------|
| `ls -lah` | List all files with details | `ls -lah /home` |
| `cd -` | Go to previous directory | `cd -` |
| `cp -r` | Copy directory recursively | `cp -r src/ backup/` |
| `rm -rf` | Force remove directory | `rm -rf temp/` |
| `chmod 755` | Set permissions | `chmod 755 script.sh` |
| `grep -r` | Recursive search | `grep -r "error" logs/` |
| `find -name` | Find files by name | `find / -name "*.conf"` |
| `ps aux` | List all processes | `ps aux \| grep nginx` |
| `tail -f` | Follow log file | `tail -f /var/log/syslog` |
| `tar -xzvf` | Extract tar.gz | `tar -xzvf file.tar.gz` |

---

### Keyboard Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl + C` | Terminate current process |
| `Ctrl + Z` | Suspend current process |
| `Ctrl + D` | Exit current shell / EOF |
| `Ctrl + L` | Clear screen |
| `Ctrl + A` | Move to beginning of line |
| `Ctrl + E` | Move to end of line |
| `Ctrl + R` | Search command history |
| `Ctrl + U` | Delete from cursor to start |
| `Ctrl + K` | Delete from cursor to end |
| `Tab` | Auto-complete |

---

### Pipes and Redirection

```bash
# Pipe output to another command
$ command1 | command2

# Redirect output to file (overwrite)
$ command > file.txt

# Redirect output to file (append)
$ command >> file.txt

# Redirect stderr to stdout
$ command 2>&1

# Redirect both stdout and stderr
$ command &> file.txt

# Redirect input from file
$ command < input.txt
```

---

## 🤝 Contributing

Feel free to contribute by:
- Adding more command examples
- Suggesting interview questions
- Improving explanations
- Fixing errors

---

## 📝 License

This guide is open source and available for educational purposes.

---

## 🔗 Resources

- [Linux Command Line Basics](https://ubuntu.com/tutorials/command-line-for-beginners)
- [Bash Scripting Guide](https://www.gnu.org/software/bash/manual/)
- [Linux System Administrator's Guide](https://tldp.org/LDP/sag/html/)
- [The Linux Documentation Project](https://tldp.org/)

---

**⭐ Star this repository if you find it helpful!**

**Made with ❤️ for Linux learners and cybersecurity enthusiasts**
