# 🐧 Linux Command Line Mastery Guide

<div align="center">

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Terminal](https://img.shields.io/badge/Terminal-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white)
![Security](https://img.shields.io/badge/Cyber_Security-000000?style=for-the-badge&logo=hackaday&logoColor=white)

### 🚀 The Ultimate Linux Command Reference for System Administrators, DevOps Engineers & Cybersecurity Professionals

*Master the command line • Ace technical interviews • Automate like a pro*

[Getting Started](#-quick-start) • [Commands](#-system-information) • [Interview Prep](#-interview-preparation) • [Scenarios](#-real-world-scenarios)

</div>

---

## 📋 Table of Contents

1. [System Information](#1--system-information)
2. [Hardware Information](#2--hardware-information)
3. [Performance Monitoring and Statistics](#3--performance-monitoring-and-statistics)
4. [User Information and Management](#4--user-information-and-management)
5. [File and Directory Commands](#5--file-and-directory-commands)
6. [Manipulating Data](#6--manipulating-data)
7. [Process Management](#7--process-management)
8. [File Permissions](#8--file-permissions)
9. [Networking](#9--networking)
10. [Archives (TAR Files)](#10--archives-tar-files)
11. [Installing Packages](#11--installing-packages)
12. [Search](#12--search)
13. [SSH Logins](#13--ssh-logins)
14. [File Transfers](#14--file-transfers)
15. [Disk Usage](#15--disk-usage)
16. [Directory Navigation](#16--directory-navigation)
17. [Programming](#17--programming)
18. [Interview Preparation](#-interview-preparation)
19. [Real-World Scenarios](#-real-world-scenarios)

---

## 🎯 Quick Start

This guide covers **170+ essential Linux commands** organized into 17 categories. Whether you're preparing for interviews, administering systems, or automating workflows, this is your go-to reference.

**💡 Pro Tip:** Use `Ctrl + F` to quickly find any command!

---

## 1 • 💻 SYSTEM INFORMATION

Get comprehensive information about your Linux system.

### `uname` - System Information

```bash
# Display Linux system information
$ uname -a
Linux server 5.15.0-56-generic #62-Ubuntu SMP x86_64 GNU/Linux

# Display kernel release information
$ uname -r
5.15.0-56-generic
```

**Interview Question:** *"How do you check the kernel version?"*
- **Answer:** `uname -r` displays the kernel release version, which is crucial for compatibility checks and security auditing.

---

### `lsb_release` - Distribution Information

```bash
# Show which version of Ubuntu is installed
$ lsb_release -a
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.1 LTS
Release:        22.04
Codename:       jammy
```

---

### `uptime` - System Uptime

```bash
# Show how long the system has been running + load
$ uptime
10:30:15 up 15 days, 3:25, 5 users, load average: 0.52, 0.58, 0.59
```

**Load Average Explained:**
- **First number (0.52):** 1-minute average
- **Second number (0.58):** 5-minute average
- **Third number (0.59):** 15-minute average

**Rule of thumb:** Load should be ≤ number of CPU cores

---

### `hostname` - Host Information

```bash
# Show system host name
$ hostname
webserver-01

# Display the IP addresses of the host
$ hostname -I
192.168.1.100 10.0.0.5

# Display network address of hostname
$ hostname -i
192.168.1.100
```

---

### System History & Time

```bash
# Show system reboot history
$ last reboot
reboot   system boot  5.15.0-56-generi Fri Dec 15 08:30
reboot   system boot  5.15.0-56-generi Mon Dec 11 14:22

# Show the current date and time
$ date
Fri Dec 27 10:30:45 UTC 2024

# Show this month's calendar
$ cal
   December 2024
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

---

### Current Users

```bash
# Display who is online
$ w
10:30:45 up 15 days,  3:25,  2 users,  load average: 0.52, 0.58, 0.59
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
john     pts/0    192.168.1.50     09:30    1:00   0.05s  0.01s vim file.txt

# Who you are logged in as
$ whoami
john
```

---

## 2 • 🔧 HARDWARE INFORMATION

Query hardware components and specifications.

### CPU Information

```bash
# Display CPU information
$ cat /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 142
model name      : Intel(R) Core(TM) i7-8565U CPU @ 1.80GHz
cpu MHz         : 1992.000
cache size      : 8192 KB
cpu cores       : 4

# Quick CPU summary
$ lscpu
Architecture:        x86_64
CPU(s):              8
Thread(s) per core:  2
Core(s) per socket:  4
```

---

### Memory Information

```bash
# Display memory information
$ cat /proc/meminfo
MemTotal:       16384000 kB
MemFree:         4096000 kB
MemAvailable:   12288000 kB

# Display free and used memory (human readable)
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           15Gi       3.2Gi       8.1Gi       256Mi       4.0Gi        11Gi
Swap:         2.0Gi          0B       2.0Gi

# In megabytes
$ free -m

# In gigabytes
$ free -g
```

**Interview Question:** *"What's the difference between free and available memory?"*
- **Free:** Completely unused memory
- **Available:** Memory that can be used by applications (includes reclaimable cache)

---

### Device Information

```bash
# Display PCI devices (in tree format)
$ lspci -tv
-[0000:00]-+-00.0  Intel Corporation Host Bridge
           +-02.0  Intel Corporation VGA compatible controller
           +-14.0  Intel Corporation USB controller

# Display USB devices
$ lsusb -tv
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/6p
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p
        |__ Port 3: Dev 3, If 0, Class=Human Interface Device

# Display DMI/SMBIOS (hardware info) from BIOS
$ dmidecode
BIOS Information
    Vendor: Dell Inc.
    Version: 2.5.0
    Release Date: 08/15/2023
```

---

### Disk Information

```bash
# Show info about disk sda
$ hdparm -i /dev/sda
Model=Samsung SSD 860, FwRev=RVT02B6Q

# Perform a read speed test on disk sda
$ hdparm -tT /dev/sda
Timing cached reads:   24000 MB in  2.00 seconds = 12000 MB/sec
Timing buffered disk reads: 1500 MB in  3.00 seconds = 500.00 MB/sec
```

---

## 3 • 📊 PERFORMANCE MONITORING AND STATISTICS

Monitor system performance, processes, and resource usage.

### `top` - Process Monitor

```bash
# Display and manage the top processes
$ top
top - 10:30:45 up 15 days,  3:25,  2 users,  load average: 0.52, 0.58, 0.59
Tasks: 245 total,   2 running, 243 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.2 us,  2.1 sy,  0.0 ni, 92.1 id,  0.4 wa,  0.0 hi,  0.2 si,  0.0 st
MiB Mem :  15980.0 total,   8096.0 free,   3200.0 used,   4684.0 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.  11520.0 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1234 john      20   0 2048000 512000  32000 S   5.2   3.2   10:30.00 python
 5678 nginx     20   0  256000  64000  16000 S   2.1   0.4    5:15.00 nginx
```

**Top keyboard shortcuts:**
- `M` - Sort by memory usage
- `P` - Sort by CPU usage
- `k` - Kill a process
- `q` - Quit
- `h` - Help

---

### CPU & Memory Statistics

```bash
# Display processor related statistics (1 second intervals)
$ mpstat 1
Linux 5.15.0-56-generic    12/27/24    _x86_64_    (8 CPU)

10:30:45     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
10:30:46     all    5.12    0.00    2.15    0.43    0.00    0.21    0.00    0.00    0.00   92.09

# Display virtual memory statistics
$ vmstat 1
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0      0 8096000 128000 4556000  0    0    12    45  890 1234  5  2 92  1  0

# Display I/O statistics
$ iostat 1
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           5.12    0.00    2.15    0.43    0.00   92.30

Device            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda             15.23       125.45        234.12    5123456    9876543
```

---

### Network Monitoring

```bash
# Capture and display all packets on interface eth0
$ tcpdump -i eth0
10:30:45.123456 IP 192.168.1.100.52345 > 93.184.216.34.80: Flags [S], seq 123456

# Monitor all traffic on port 80 (HTTP)
$ tcpdump -i eth0 'port 80'

# Save capture to file
$ tcpdump -i eth0 -w capture.pcap

# Read from file
$ tcpdump -r capture.pcap
```

**Interview Scenario:** *"How do you debug network connectivity issues?"*
```bash
# 1. Check if interface is up
$ ip link show eth0

# 2. Monitor live traffic
$ tcpdump -i eth0 -n

# 3. Check for packet loss
$ ping -c 100 8.8.8.8 | grep loss
```

---

### File & Process Monitoring

```bash
# List all open files on the system
$ lsof
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
systemd       1 root  cwd    DIR  259,2     4096    2 /
nginx      1234 www   10u  IPv4  12345      0t0  TCP *:80 (LISTEN)

# List files opened by specific user
$ lsof -u john
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
vim      5678 john    3u   REG  259,2     2048 123456 /home/john/file.txt

# List processes using a specific file
$ lsof /var/log/syslog

# List processes using a specific port
$ lsof -i :8080
```

---

### Watch Command

```bash
# Execute "df -h", showing periodic updates every 2 seconds
$ watch df -h
Every 2.0s: df -h                                    Fri Dec 27 10:30:45 2024

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1       100G   45G   50G  48% /
/dev/sda2       200G  120G   70G  64% /home

# Custom interval (1 second)
$ watch -n 1 free -h

# Highlight differences
$ watch -d free -h
```

---

## 4 • 👥 USER INFORMATION AND MANAGEMENT

Manage users, groups, and view user activity.

### User Information

```bash
# Display the user and group IDs of your current user
$ id
uid=1000(john) gid=1000(john) groups=1000(john),27(sudo),44(video)

# Display the last users who have logged onto the system
$ last
john     pts/0        192.168.1.50    Fri Dec 27 09:30   still logged in
sarah    pts/1        192.168.1.51    Thu Dec 26 14:22 - 18:30  (04:08)
reboot   system boot  5.15.0-56       Thu Dec 26 08:00

# Show who is logged into the system
$ who
john     pts/0        2024-12-27 09:30 (192.168.1.50)
sarah    pts/1        2024-12-27 10:15 (192.168.1.51)

# Show who is logged in and what they are doing
$ w
 10:30:45 up 15 days,  3:25,  2 users,  load average: 0.52, 0.58, 0.59
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
john     pts/0    192.168.1.50     09:30    0.00s  0.15s  0.02s w
sarah    pts/1    192.168.1.51     10:15   15:00   0.05s  0.05s vim report.txt
```

---

### Group Management

```bash
# Create a group named "test"
$ groupadd test

# Create group with specific GID
$ groupadd -g 5000 developers

# View all groups
$ cat /etc/group

# View groups for current user
$ groups
john sudo docker developers
```

---

### User Management

```bash
# Create account named john with comment and home directory
$ useradd -c "John Smith" -m john

# Create user with specific shell
$ useradd -s /bin/bash -m alice

# Create user with specific UID
$ useradd -u 2000 -m bob

# Set password for user
$ passwd john
Enter new UNIX password: ********
Retype new UNIX password: ********

# Delete the john account
$ userdel john

# Delete user and home directory
$ userdel -r john

# Add the john account to the sales group
$ usermod -aG sales john

# Change user's shell
$ usermod -s /bin/zsh john

# Lock user account
$ usermod -L john

# Unlock user account
$ usermod -U john
```

**Interview Question:** *"What's the difference between `useradd` and `adduser`?"*
- **useradd:** Low-level utility, requires manual configuration
- **adduser:** High-level, interactive script (Debian/Ubuntu), creates home directory and sets defaults automatically

---

### Sudo Operations

```bash
# View sudo privileges
$ sudo -l

# Switch to root user
$ sudo -i

# Run command as another user
$ sudo -u postgres psql

# Edit sudoers file safely
$ visudo
```

---

## 5 • 📁 FILE AND DIRECTORY COMMANDS

Essential commands for file and directory manipulation.

### Listing Files

```bash
# List all files in long listing (detailed) format
$ ls -al
total 48
drwxr-xr-x  5 john john  4096 Dec 27 10:30 .
drwxr-xr-x 15 root root  4096 Dec 26 08:00 ..
-rw-r--r--  1 john john   220 Dec 25 14:30 .bashrc
drwxr-xr-x  3 john john  4096 Dec 27 09:00 Documents

# List with human-readable sizes
$ ls -lh
-rw-r--r-- 1 john john 1.5M Dec 27 10:30 report.pdf

# Sort by modification time (newest first)
$ ls -lt

# Sort by size (largest first)
$ ls -lS

# List only directories
$ ls -d */
```

---

### Navigation

```bash
# Display the present working directory
$ pwd
/home/john/projects/linux-guide

# Change to home directory
$ cd
$ cd ~

# Change to previous directory
$ cd -

# Go up one level
$ cd ..
```

---

### Creating Directories

```bash
# Create a directory
$ mkdir directory

# Create nested directories (create parent directories as needed)
$ mkdir -p projects/linux/scripts

# Create directory with specific permissions
$ mkdir -m 755 public_html

# Create multiple directories
$ mkdir dir1 dir2 dir3
```

---

### File Operations

```bash
# Remove (delete) file
$ rm file.txt

# Remove directory and its contents recursively
$ rm -r directory/

# Force removal without prompting
$ rm -f file.txt

# Force recursive removal (DANGEROUS!)
$ rm -rf directory/

# Interactive mode (ask before each removal)
$ rm -i *.txt

# Delete empty directory
$ rmdir empty_directory/
```

**⚠️ CRITICAL WARNING:**
```bash
# NEVER RUN THESE COMMANDS:
$ rm -rf /           # Deletes entire system
$ rm -rf /*          # Deletes everything
$ rm -rf ~/*         # Deletes entire home directory
```

---

### Copying Files

```bash
# Copy file1 to file2
$ cp file1.txt file2.txt

# Copy directory recursively
$ cp -r source_directory/ destination/

# Copy with verbose output
$ cp -v file.txt backup/
'file.txt' -> 'backup/file.txt'

# Preserve attributes (permissions, timestamps, ownership)
$ cp -p file.txt backup/

# Copy only if source is newer
$ cp -u file.txt backup/

# Interactive mode (prompt before overwrite)
$ cp -i file.txt backup/

# Copy multiple files to directory
$ cp file1.txt file2.txt file3.txt /backup/
```

---

### Moving/Renaming Files

```bash
# Rename file
$ mv oldname.txt newname.txt

# Move file to directory
$ mv file.txt /home/john/documents/

# Move multiple files
$ mv file1.txt file2.txt file3.txt directory/

# Interactive mode
$ mv -i file.txt destination/

# Don't overwrite existing files
$ mv -n file.txt destination/
```

---

### Creating Links

```bash
# Create symbolic link (soft link)
$ ln -s /path/to/file linkname

# Example: Create shortcut to log file
$ ln -s /var/log/nginx/access.log ~/nginx-log

# Create hard link
$ ln file.txt hardlink.txt

# Check if file is a symbolic link
$ ls -l linkname
lrwxrwxrwx 1 john john 15 Dec 27 10:30 linkname -> /path/to/file
```

**Hard Link vs Soft Link:**

| Feature | Hard Link | Soft Link |
|---------|-----------|-----------|
| Inode | Same as original | Different inode |
| Can link directories | No | Yes |
| Works across filesystems | No | Yes |
| Survives if original deleted | Yes | No (becomes broken link) |

---

### File Operations

```bash
# Create empty file or update timestamp
$ touch file.txt

# Create multiple files
$ touch file1.txt file2.txt file3.txt

# Update access time only
$ touch -a file.txt

# Update modification time only
$ touch -m file.txt

# Set specific timestamp
$ touch -t 202412271030.00 file.txt  # YYYYMMDDhhmm.ss
```

---

### Viewing File Contents

```bash
# View the contents of file
$ cat file.txt

# Concatenate multiple files
$ cat file1.txt file2.txt > combined.txt

# Show line numbers
$ cat -n file.txt

# Browse through a text file (with scrolling)
$ less file.txt

# Navigation in less:
# Space / f    - Forward one page
# b            - Backward one page
# /pattern     - Search forward
# ?pattern     - Search backward
# n            - Next match
# q            - Quit

# Display first 10 lines
$ head file.txt

# Display first 20 lines
$ head -n 20 file.txt

# Display last 10 lines
$ tail file.txt

# Display last 20 lines
$ tail -n 20 file.txt

# Follow file (monitor for new content)
$ tail -f /var/log/syslog

# Follow file starting from line 100
$ tail -n +100 -f application.log
```

---

### Other File Commands

```bash
# Determine file type
$ file myfile
myfile: ASCII text

$ file image.jpg
image.jpg: JPEG image data, JFIF standard

$ file script.sh
script.sh: Bourne-Again shell script, ASCII text executable

# Change file group
$ chgrp developers project.txt

# Spool file for printing
$ lpr document.pdf
```

---

### Text Editors

```bash
# Vi/Vim text editor
$ vi file.txt
$ vim file.txt

# Gedit (GNOME text editor)
$ gedit file.txt

# Nano (simple text editor)
$ nano file.txt
```

---

## 6 • 🔄 MANIPULATING DATA

Powerful text processing and data manipulation tools.

### `grep` - Pattern Searching

```bash
# Basic search
$ grep "error" logfile.txt

# Case-insensitive search
$ grep -i "error" logfile.txt

# Recursive search in directories
$ grep -r "TODO" /home/john/projects/

# Show line numbers
$ grep -n "error" logfile.txt

# Count matches
$ grep -c "error" logfile.txt

# Invert match (show non-matching lines)
$ grep -v "success" logfile.txt

# Show context (3 lines before and after)
$ grep -C 3 "error" logfile.txt

# Multiple patterns (OR)
$ grep -E "error|warning|critical" logfile.txt

# Show only filenames with matches
$ grep -l "error" *.log
```

**Interview Question:** *"How do you find all ERROR lines in logs from last hour?"*
```bash
$ grep "ERROR" /var/log/app.log | awk -v date="$(date -d '1 hour ago' '+%Y-%m-%d %H')" '$0 ~ date'
```

---

### `awk` - Pattern Scanning and Processing

```bash
# Print specific column (first column)
$ awk '{print $1}' file.txt

# Print multiple columns
$ awk '{print $1, $3}' file.txt
john 25
sarah 30

# Use custom delimiter
$ awk -F: '{print $1}' /etc/passwd
root
daemon
bin

# Print lines where column 3 > 100
$ awk '$3 > 100' sales.txt

# Sum values in column
$ awk '{sum += $2} END {print sum}' numbers.txt

# Calculate average
$ awk '{sum += $1; count++} END {print sum/count}' numbers.txt

# Print lines between patterns
$ awk '/START/,/END/' file.txt

# Custom output format
$ awk '{printf "Name: %-10s Age: %d\n", $1, $2}' people.txt
```

**Real-world example:** Extract IP addresses from log
```bash
$ awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -rn
    245 192.168.1.100
    189 192.168.1.101
    156 192.168.1.102
```

---

### `sed` - Stream Editor

```bash
# Replace first occurrence in each line
$ sed 's/old/new/' file.txt

# Replace all occurrences (global)
$ sed 's/old/new/g' file.txt

# Delete lines containing pattern
$ sed '/pattern/d' file.txt

# Delete empty lines
$ sed '/^$/d' file.txt

# Print specific line (line 5)
$ sed -n '5p' file.txt

# Print range of lines (5-10)
$ sed -n '5,10p' file.txt

# Delete lines 2-4
$ sed '2,4d' file.txt

# In-place editing (modify file directly)
$ sed -i 's/old/new/g' file.txt

# In-place with backup
$ sed -i.bak 's/old/new/g' file.txt

# Multiple substitutions
$ sed -e 's/foo/bar/g' -e 's/hello/world/g' file.txt

# Add line after pattern
$ sed '/pattern/a This is a new line' file.txt

# Insert line before pattern
$ sed '/pattern/i This is a new line' file.txt
```

---

### `cut` - Extract Fields

```bash
# Cut specific field (delimiter is tab by default)
$ cut -f1 file.txt

# Custom delimiter (comma)
$ cut -d',' -f1,3 data.csv

# Extract characters 1-5
$ cut -c1-5 file.txt

# Extract username from /etc/passwd
$ cut -d: -f1 /etc/passwd
```

---

### `sort` - Sort Lines

```bash
# Sort file alphabetically
$ sort file.txt

# Sort numerically
$ sort -n numbers.txt

# Reverse sort
$ sort -r file.txt

# Sort by specific column (3rd column)
$ sort -k3 data.txt

# Sort by month
$ sort -M months.txt

# Remove duplicates while sorting
$ sort -u file.txt

# Sort human-readable numbers (1K, 2M, 3G)
$ sort -h sizes.txt
```

---

### `uniq` - Report or Remove Duplicates

```bash
# Remove adjacent duplicate lines
$ uniq file.txt

# Count occurrences
$ uniq -c file.txt
   3 apple
   2 banana
   1 orange

# Show only duplicates
$ uniq -d file.txt

# Show only unique lines
$ uniq -u file.txt

# Case-insensitive comparison
$ uniq -i file.txt

# Typical usage: sort then uniq
$ sort file.txt | uniq -c | sort -rn
```

---

### `wc` - Word Count

```bash
# Count lines, words, and characters
$ wc file.txt
  150  800 4500 file.txt
# 150 lines, 800 words, 4500 characters

# Count lines only
$ wc -l file.txt

# Count words only
$ wc -w file.txt

# Count characters only
$ wc -c file.txt

# Count bytes
$ wc -c file.txt
```

---

### `diff` - Compare Files

```bash
# Compare two files
$ diff file1.txt file2.txt
3c3
< This is the old line
---
> This is the new line

# Side-by-side comparison
$ diff -y file1.txt file2.txt

# Unified format (like git diff)
$ diff -u file1.txt file2.txt

# Ignore case
$ diff -i file1.txt file2.txt

# Ignore whitespace
$ diff -w file1.txt file2.txt
```

---

### `tr` - Translate Characters

```bash
# Convert lowercase to uppercase
$ echo "hello" | tr 'a-z' 'A-Z'
HELLO

# Delete characters
$ echo "hello123" | tr -d '0-9'
hello

# Squeeze repeated characters
$ echo "hellooo   world" | tr -s 'o '
helo world

# ROT13 encoding
$ echo "hello" | tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

---

### `join` - Join Files on Common Field

```bash
# Join files on first field
$ join file1.txt file2.txt

# Join on specific field
$ join -1 2 -2 1 file1.txt file2.txt
```

---

### `paste` - Merge Lines

```bash
# Merge files line by line (tab-separated)
$ paste file1.txt file2.txt

# Custom delimiter
$ paste -d',' file1.txt file2.txt
```

---

### `split` - Split Files

```bash
# Split file into 1000-line chunks
$ split -l 1000 largefile.txt chunk_

# Split into 100MB chunks
$ split -b 100M largefile.iso part_

# Split with numeric suffixes
$ split -d -l 1000 file.txt chunk_
```

---

### Compression Tools

```bash
# Compress file with gzip
$ gzip file.txt
# Creates: file.txt.gz

# Decompress gzip file
$ gunzip file.txt.gz
# or
$ gzip -d file.txt.gz

# View compressed file without extracting
$ zcat file.txt.gz
$ zmore file.txt.gz

# Compare compressed files
$ zcmp file1.txt.gz file2.txt.gz
$ zdiff file1.txt.gz file2.txt.gz

# Uncompress .Z files
$ uncompress file.txt.Z

# Keep original file when compressing
$ gzip -k file.txt
```

---

### Other Text Tools

```bash
# Find lines in sorted data
$ look prefix /usr/share/dict/words

# Perl one-liners
$ perl -pe 's/old/new/g' file.txt        # Replace text
$ perl -ne 'print if /pattern/' file.txt # Grep-like

# Expand tabs to spaces
$ expand -t 4 file.txt

# Convert spaces to tabs
$ unexpand -t 4 file.txt

# Compare file contents byte by byte
$ cmp file1.txt file2.txt
```

---

## 7 • ⚙️ PROCESS MANAGEMENT

Control and monitor system processes.

### Viewing Processes

```bash
# Display currently running processes
$ ps
  PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 5678 pts/0    00:00:00 ps

# Display all processes on the system
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Dec26 ?        00:00:02 /sbin/init
root       123     1  0 Dec26 ?        00:00:00 /lib/systemd/systemd-journald

# Alternative BSD-style
$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169564 11234 ?        Ss   Dec26   0:02 /sbin/init
john      5678  2.5  5.2 2048576 524288 ?      Sl   10:30   1:25 python app.py

# Display process tree
$ ps auxf
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169564 11234 ?        Ss   Dec26   0:02 /sbin/init
root       123  0.0  0.0  12345  1234 ?        S    Dec26   0:00  \_ /usr/sbin/cron

# Display processes for specific user
$ ps -u john

# Display process information for specific process name
$ ps -ef | grep nginx
root      1234     1  0 10:30 ?        00:00:00 nginx: master process
www-data  5678  1234  0 10:30 ?        00:00:05 nginx: worker process
```

**Process States:**
- `R` - Running
- `S` - Sleeping (waiting for event)
- `D` - Uninterruptible sleep (usually I/O)
- `Z` - Zombie (terminated but not reaped)
- `T` - Stopped

---

### Interactive Process Monitoring

```bash
# Display and manage top processes
$ top

# Better alternative: htop (more user-friendly)
$ htop

# Top keyboard shortcuts:
# M - Sort by memory
# P - Sort by CPU
# k - Kill process
# r - Renice process
# u - Filter by user
# h - Help
# q - Quit
```

---

### Killing Processes

```bash
# Kill process with PID (graceful termination)
$ kill 1234

# Force kill (immediate termination)
$ kill -9 1234
# or
$ kill -SIGKILL 1234

# Send specific signal
$ kill -HUP 1234    # Hang up (reload config)
$ kill -TERM 1234   # Terminate (default)
$ kill -STOP 1234   # Stop (pause)
$ kill -CONT 1234   # Continue

# Kill all processes with name
$ killall nginx

# Kill all processes by pattern
$ pkill python

# Kill all user processes
$ pkill -u john

# Interactive kill (asks for confirmation)
$ killall -i processname
```

**Interview Question:** *"What's the difference between kill -15 and kill -9?"*
- **kill -15 (SIGTERM):** Graceful shutdown, allows cleanup, can be caught/ignored
- **kill -9 (SIGKILL):** Immediate forced kill, cannot be caught, no cleanup

---

### Background & Foreground Jobs

```bash
# Start program in background
$ program &
[1] 5678

# Start normally then suspend with Ctrl+Z
$ long_running_command
^Z
[1]+  Stopped    long_running_command

# Display stopped or background jobs
$ jobs
[1]-  Stopped    vim file.txt
[2]+  Running    python script.py &

# Bring most recent background job to foreground
$ fg
python script.py

# Bring specific job to foreground
$ fg %1
vim file.txt

# Resume stopped job in background
$ bg
[1]+ python script.py &

# Resume specific job in background
$ bg %2

# Disown job (won't be killed when terminal closes)
$ disown %1
```

**Pro Tip:** Use `nohup` for processes that should survive terminal closure:
```bash
$ nohup long_running_script.sh &
```

---

### Process Priority

```bash
# Run command with lower priority
$ nice -n 10 command

# Run with higher priority (requires root)
$ nice -n -10 command

# Change priority of running process
$ renice -n 5 -p 1234

# View process priority
$ ps -eo pid,ni,cmd
```

**Nice values:** -20 (highest priority) to 19 (lowest priority)

---

## 8 • 🔐 FILE PERMISSIONS

Understanding and managing Linux file permissions.

### Permission Structure

```
-rwxr-xr-x  1 john developers 4096 Dec 27 10:30 script.sh
│││││││││
│││││││└┴─ Others: r-x (read, execute)
││││││└──── Group: r-x (read, execute)
│││└┴┴───── Owner: rwx (read, write, execute)
││└────────── Number of hard links
│└─────────── File type (- file, d directory, l link, b block, c character, p pipe, s socket)
```

### Permission Matrix

| **Permission** | **User (U)** | **Group (G)** | **World (W)** | **Octal** |
|----------------|--------------|---------------|---------------|-----------|
| `rwx rwx rwx` | read, write, execute | read, write, execute | read, write, execute | **777** |
| `rwx rwx r-x` | read, write, execute | read, write, execute | read, execute | **775** |
| `rwx r-x r-x` | read, write, execute | read, execute | read, execute | **755** |
| `rw- rw- r--` | read, write | read, write | read | **664** |
| `rw- r-- r--` | read, write | read | read | **644** |
| `rw- --- ---` | read, write | none | none | **600** |
| `rwx --- ---` | read, write, execute | none | none | **700** |

---

### Understanding Octal Permissions

Each permission is a sum:
- **Read (r)** = 4
- **Write (w)** = 2
- **Execute (x)** = 1

Examples:
- `7` = 4+2+1 = rwx
- `6` = 4+2 = rw-
- `5` = 4+1 = r-x
- `4` = 4 = r--
- `0` = 0 = ---

**755 means:**
- Owner: 7 (rwx) = read, write, execute
- Group: 5 (r-x) = read, execute
- Others: 5 (r-x) = read, execute

---

### `chmod` - Change Permissions

```bash
# Numeric (octal) method
$ chmod 755 script.sh     # rwxr-xr-x
$ chmod 644 file.txt      # rw-r--r--
$ chmod 600 secret.txt    # rw-------
$ chmod 700 private_dir/  # rwx------

# Symbolic method
# Format: [who][operation][permission]
# who: u(user), g(group), o(others), a(all)
# operation: +(add), -(remove), =(set exactly)
# permission: r(read), w(write), x(execute)

# Add execute permission for user
$ chmod u+x script.sh

# Remove write permission for group
$ chmod g-w file.txt

# Add execute for all
$ chmod a+x script.sh
$ chmod +x script.sh  # same as above

# Set exact permissions for user
$ chmod u=rwx,g=rx,o=r file.txt

# Multiple operations
$ chmod u+x,g-w,o-r file.txt

# Recursive (apply to directory and all contents)
$ chmod -R 755 /var/www/html/

# Copy permissions from one file to another
$ chmod --reference=file1.txt file2.txt
```

**Common Use Cases:**

```bash
# Make script executable
$ chmod +x script.sh

# Secure SSH private key
$ chmod 600 ~/.ssh/id_rsa

# Web directory permissions
$ chmod 755 public_html/
$ chmod 644 public_html/*.html

# Shared directory with group write
$ chmod 775 shared_project/
```

---

### `chown` - Change Ownership

```bash
# Change owner only
$ chown john file.txt

# Change owner and group
$ chown john:developers file.txt

# Change group only (alternative to chgrp)
$ chown :developers file.txt

# Recursive change
$ chown -R john:developers /var/www/

# Change ownership to match reference file
$ chown --reference=file1.txt file2.txt

# Don't follow symbolic links
$ chown -h john symlink
```

---

### `chgrp` - Change Group

```bash
# Change group ownership
$ chgrp developers project.txt

# Recursive
$ chgrp -R developers /shared/project/

# Verbose output
$ chgrp -v developers file.txt
changing group of 'file.txt' to 'developers'
```

---

### Special Permissions

```bash
# SUID (Set User ID) - Run as file owner
$ chmod u+s /usr/bin/passwd
$ chmod 4755 file  # SUID + 755

# SGID (Set Group ID) - Run as file group / inherit directory group
$ chmod g+s /shared/directory
$ chmod 2755 directory  # SGID + 755

# Sticky Bit - Only owner can delete files (useful for /tmp)
$ chmod +t /shared/directory
$ chmod 1755 directory  # Sticky + 755

# View special permissions
$ ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 59640 Mar 22  2023 /usr/bin/passwd
     ^-- SUID bit

$ ls -ld /tmp
drwxrwxrwt 15 root root 4096 Dec 27 10:30 /tmp
         ^-- Sticky bit
```

---

### Umask - Default Permissions

```bash
# View current umask
$ umask
0022

# Set umask (subtract from 666 for files, 777 for directories)
$ umask 0002
# Files will be created as 664 (666-002)
# Directories as 775 (777-002)

$ umask 0077
# Files: 600 (666-077)
# Directories: 700 (777-077)

# Symbolic umask
$ umask u=rwx,g=rx,o=
```

---

### ACL - Access Control Lists

```bash
# View ACL
$ getfacl file.txt

# Set ACL for specific user
$ setfacl -m u:john:rw file.txt

# Set ACL for specific group
$ setfacl -m g:developers:rwx directory/

# Remove ACL
$ setfacl -x u:john file.txt

# Remove all ACLs
$ setfacl -b file.txt

# Recursive ACL
$ setfacl -R -m u:john:rw directory/
```

---

### Interview Questions

**Q: "How do you make a file readable by everyone but writable only by the owner?"**
```bash
$ chmod 644 file.txt
# or
$ chmod u=rw,go=r file.txt
```

**Q: "What does permission 777 mean and why is it dangerous?"**
- **Answer:** Everyone can read, write, and execute. Dangerous because:
  - Any user can modify or delete the file
  - Security vulnerability if file contains sensitive data
  - Can execute malicious code if it's a script

**Q: "How do you find all files with 777 permissions?"**
```bash
$ find / -type f -perm 0777
```

---

## 9 • 🌐 NETWORKING

Network configuration, monitoring, and troubleshooting.

### Interface Configuration

```bash
# Display all network interfaces and IP addresses
$ ifconfig -a
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        ether 00:1a:2b:3c:4d:5e  txqueuelen 1000  (Ethernet)

# Modern alternative: ip command
$ ip addr show
$ ip a

# Display specific interface (eth0)
$ ifconfig eth0
$ ip addr show eth0

# Bring interface up/down
$ ifconfig eth0 up
$ ifconfig eth0 down
$ ip link set eth0 up
$ ip link set eth0 down

# Assign IP address
$ ifconfig eth0 192.168.1.100 netmask 255.255.255.0
$ ip addr add 192.168.1.100/24 dev eth0
```

---

### Network Device Information

```bash
# Query or control network driver and hardware settings
$ ethtool eth0
Settings for eth0:
    Speed: 1000Mb/s
    Duplex: Full
    Link detected: yes

# View statistics
$ ethtool -S eth0
```

---

### Connectivity Testing

```bash
# Send ICMP echo request to host
$ ping google.com
PING google.com (142.250.185.46) 56(84) bytes of data.
64 bytes from lga25s65-in-f14.1e100.net (142.250.185.46): icmp_seq=1 ttl=117 time=12.3 ms

# Limit to 5 packets
$ ping -c 5 google.com

# Ping with specific interval (0.2 seconds)
$ ping -i 0.2 192.168.1.1

# Ping with packet size
$ ping -s 1000 google.com

# Flood ping (requires root)
$ ping -f google.com
```

---

### DNS Queries

```bash
# Display whois information for domain
$ whois google.com
Domain Name: GOOGLE.COM
Registrar: MarkMonitor Inc.
Creation Date: 1997-09-15

# Display DNS information for domain
$ dig google.com
; <<>> DiG 9.18.1 <<>> google.com
;; ANSWER SECTION:
google.com.    300    IN    A    142.250.185.46

# Short answer
$ dig +short google.com
142.250.185.46

# Specific record type
$ dig google.com MX
$ dig google.com TXT
$ dig google.com NS

# Reverse DNS lookup
$ dig -x 142.250.185.46
$ dig -x 8.8.8.8 +short
dns.google.

# Query specific nameserver
$ dig @8.8.8.8 google.com

# Trace DNS resolution path
$ dig +trace google.com

# Display DNS IP address (simpler than dig)
$ host google.com
google.com has address 142.250.185.46
google.com mail is handled by 10 smtp.google.com.

# Reverse lookup
$ host 142.250.185.46
```

---

### Hostname Resolution

```bash
# Display network address of hostname
$ hostname -i
192.168.1.100

# Display all local IP addresses
$ hostname -I
192.168.1.100 10.0.0.5 172.17.0.1
```

---

### File Downloads

```bash
# Download file with wget
$ wget http://example.com/file.zip

# Download to specific filename
$ wget -O output.zip http://example.com/file.zip

# Continue interrupted download
$ wget -c http://example.com/largefile.iso

# Download in background
$ wget -b http://example.com/file.zip

# Mirror entire website
$ wget --mirror --convert-links --page-requisites http://example.com

# Download with curl
$ curl -O http://example.com/file.zip

# Save to specific filename
$ curl -o output.zip http://example.com/file.zip

# Follow redirects
$ curl -L http://example.com/redirect

# Download with progress bar
$ curl -# -O http://example.com/file.zip

# Send POST request
$ curl -X POST -d "param1=value1&param2=value2" http://api.example.com

# Send JSON data
$ curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' http://api.example.com
```

---

### Network Statistics

```bash
# Display listening TCP and UDP ports and programs
$ netstat -nutlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1234/nginx
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      5678/sshd

# Show all connections
$ netstat -an

# Show routing table
$ netstat -r
$ route -n
$ ip route show

# Modern alternative: ss (socket statistics)
$ ss -nutlp
Netid  State   Recv-Q  Send-Q  Local Address:Port  Peer Address:Port  Process
tcp    LISTEN  0       128     0.0.0.0:80          0.0.0.0:*          users:(("nginx",pid=1234))

# Show all sockets
$ ss -a

# Show established connections
$ ss -t state established

# Show listening sockets
$ ss -l
```

---

### Network File Transfer Programs

```bash
# FTP - File Transfer Protocol
$ ftp ftp.example.com
Connected to ftp.example.com
Name: username
Password: ********

# TFTP - Trivial File Transfer Protocol
$ tftp 192.168.1.1
tftp> get file.txt
tftp> put file.txt
tftp> quit

# SFTP - Secure File Transfer Protocol
$ sftp user@server.com
sftp> ls
sftp> get remotefile.txt
sftp> put localfile.txt
sftp> quit
```

---

### Remote Access

```bash
# Telnet (insecure - avoid in production!)
$ telnet server.com 23

# SSH - Secure Shell (covered in detail in section 13)
$ ssh user@server.com

# Remote login
$ rlogin -l username hostname

# Remote shell (deprecated - use SSH)
$ rsh hostname command

# Remote copy (deprecated - use scp)
$ rcp file.txt user@host:/path/
```

---

### Network Troubleshooting

```bash
# Trace route to destination
$ traceroute google.com
$ tracepath google.com

# Check if port is open
$ nc -zv google.com 80
Connection to google.com 80 port [tcp/http] succeeded!

# TCP port scan
$ nc -zv 192.168.1.1 20-100

# Display ARP cache
$ arp -a
? (192.168.1.1) at aa:bb:cc:dd:ee:ff [ether] on eth0

# Show network statistics
$ netstat -s

# Monitor bandwidth usage
$ iftop
$ nethogs
$ vnstat
```

---

### Firewall Commands

```bash
# UFW (Ubuntu/Debian)
$ ufw status
$ ufw allow 80/tcp
$ ufw deny 23/tcp
$ ufw enable

# iptables (advanced)
$ iptables -L
$ iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# firewalld (RHEL/CentOS)
$ firewall-cmd --list-all
$ firewall-cmd --add-port=80/tcp --permanent
$ firewall-cmd --reload
```

---

## 10 • 📦 ARCHIVES (TAR FILES)

Creating and extracting compressed archives.

### Creating Archives

```bash
# Create tar archive (uncompressed)
$ tar -cvf archive.tar directory/
directory/
directory/file1.txt
directory/file2.txt

# Create gzip compressed tar (.tar.gz or .tgz)
$ tar -czvf archive.tar.gz directory/

# Create bzip2 compressed tar (.tar.bz2)
$ tar -cjvf archive.tar.bz2 directory/

# Create xz compressed tar (.tar.xz)
$ tar -cJvf archive.tar.xz directory/
```

**Flags explained:**
- `c` - Create archive
- `x` - Extract archive
- `t` - List contents
- `v` - Verbose (show files being processed)
- `f` - File (specify archive filename)
- `z` - gzip compression
- `j` - bzip2 compression
- `J` - xz compression

---

### Extracting Archives

```bash
# Extract tar archive
$ tar -xvf archive.tar

# Extract to specific directory
$ tar -xvf archive.tar -C /path/to/destination/

# Extract gzip compressed tar
$ tar -xzvf archive.tar.gz

# Extract bzip2 compressed tar
$ tar -xjvf archive.tar.bz2

# Extract xz compressed tar
$ tar -xJvf archive.tar.xz

# Auto-detect compression
$ tar -xvf archive.tar.gz  # Works without 'z'
$ tar -xvf archive.tar.bz2 # Works without 'j'
```

---

### Listing Archive Contents

```bash
# List contents without extracting
$ tar -tvf archive.tar
drwxr-xr-x john/users    0 2024-12-27 10:30 directory/
-rw-r--r-- john/users 1024 2024-12-27 10:30 directory/file1.txt

# List compressed archive
$ tar -tzvf archive.tar.gz
```

---

### Advanced Tar Operations

```bash
# Exclude files while creating archive
$ tar -czvf archive.tar.gz --exclude='*.log' directory/

# Append files to existing archive
$ tar -rvf archive.tar newfile.txt

# Extract specific file
$ tar -xzvf archive.tar.gz directory/specific-file.txt

# Extract files matching pattern
$ tar -xzvf archive.tar.gz --wildcards '*.txt'

# Create archive with timestamp
$ tar -czvf backup-$(date +%Y%m%d).tar.gz directory/

# Split large archive into parts
$ tar -czvf - directory/ | split -b 100M - archive.tar.gz.part

# Combine and extract split archive
$ cat archive.tar.gz.part* | tar -xzvf -
```

---

### Other Archive Formats

```bash
# Create zip archive
$ zip -r archive.zip directory/

# Extract zip archive
$ unzip archive.zip

# Extract to specific directory
$ unzip archive.zip -d /path/to/destination/

# List zip contents
$ unzip -l archive.zip

# Create password-protected zip
$ zip -e -r secure.zip directory/

# Extract specific file from zip
$ unzip archive.zip file.txt

# 7z archives
$ 7z a archive.7z directory/   # Create
$ 7z x archive.7z               # Extract

# rar archives
$ rar a archive.rar directory/  # Create
$ unrar x archive.rar           # Extract
```

---

### Interview Question

**Q: "What's the difference between .tar.gz and .tar.bz2?"**

| Feature | .tar.gz (gzip) | .tar.bz2 (bzip2) |
|---------|----------------|------------------|
| Compression ratio | Good | Better (smaller size) |
| Speed | Faster | Slower |
| CPU usage | Lower | Higher |
| Common use | General purpose | When size matters |

---

## 11 • 📥 INSTALLING PACKAGES

Package management for different Linux distributions.

### YUM/DNF (RHEL, CentOS, Fedora)

```bash
# Search for package by keyword
$ yum search nginx
$ dnf search nginx

# Install package
$ yum install nginx
$ dnf install nginx

# Install specific version
$ yum install nginx-1.18.0

# Display description and summary
$ yum info nginx
Name         : nginx
Version      : 1.18.0
Summary      : High performance web server

# Install from local RPM file
$ rpm -i package.rpm
$ rpm -ivh package.rpm  # verbose with progress

# Query installed package
$ rpm -q nginx

# List files in package
$ rpm -ql nginx

# Find which package owns a file
$ rpm -qf /usr/sbin/nginx

# Remove/uninstall package
$ yum remove nginx
$ dnf remove nginx

# Update specific package
$ yum update nginx

# Update all packages
$ yum update

# List installed packages
$ yum list installed
$ rpm -qa

# Clean package cache
$ yum clean all

# Download package without installing
$ yumdownloader nginx

# List available groups
$ yum grouplist

# Install package group
$ yum groupinstall "Development Tools"
```

---

### APT (Debian, Ubuntu)

```bash
# Update package lists
$ apt update

# Install package
$ apt install nginx

# Install specific version
$ apt install nginx=1.18.0-0ubuntu1

# Install local .deb file
$ dpkg -i package.deb
$ apt install ./package.deb  # Handles dependencies

# Search for package
$ apt search nginx

# Show package information
$ apt show nginx

# Remove package (keep config files)
$ apt remove nginx

# Remove package and config files
$ apt purge nginx

# Remove unnecessary packages
$ apt autoremove

# Upgrade specific package
$ apt install --only-upgrade nginx

# Upgrade all packages
$ apt upgrade

# Distribution upgrade
$ apt dist-upgrade

# List installed packages
$ apt list --installed
$ dpkg -l

# List files in package
$ dpkg -L nginx

# Find which package owns file
$ dpkg -S /usr/sbin/nginx

# Fix broken dependencies
$ apt --fix-broken install
```

---

### Installing from Source Code

```bash
# Extract source code
$ tar -xzvf sourcecode.tar.gz
$ cd sourcecode/

# Configure build (check dependencies, set options)
$ ./configure
$ ./configure --prefix=/usr/local

# Compile source code
$ make

# Install compiled binaries
$ sudo make install

# Uninstall (if Makefile supports it)
$ sudo make uninstall

# Complete example: Installing nginx from source
$ wget http://nginx.org/download/nginx-1.24.0.tar.gz
$ tar -xzvf nginx-1.24.0.tar.gz
$ cd nginx-1.24.0/
$ ./configure --prefix=/usr/local/nginx --with-http_ssl_module
$ make
$ sudo make install
```

---

### Snap Packages (Universal)

```bash
# Install snap package
$ snap install package-name

# List installed snaps
$ snap list

# Update snap
$ snap refresh package-name

# Remove snap
$ snap remove package-name
```

---

### Flatpak (Universal)

```bash
# Install flatpak
$ flatpak install flathub com.example.app

# Run flatpak application
$ flatpak run com.example.app

# List installed flatpaks
$ flatpak list

# Update
$ flatpak update
```

---

## 12 • 🔍 SEARCH

Finding files, directories, and text patterns.

### `grep` - Search in Files

```bash
# Search for pattern in file
$ grep "error" /var/log/syslog

# Case-insensitive search
$ grep -i "ERROR" logfile.txt

# Search recursively in directory
$ grep -r "TODO" /home/john/projects/

# Show line numbers
$ grep -n "function" script.py

# Show only filenames with matches
$ grep -l "error" *.log

# Count matching lines
$ grep -c "error" logfile.txt

# Invert match (show non-matching lines)
$ grep -v "success" logfile.txt

# Show context (3 lines before and after)
$ grep -C 3 "error" logfile.txt
$ grep -B 3 "error" logfile.txt  # Before
$ grep -A 3 "error" logfile.txt  # After

# Extended regex (multiple patterns)
$ grep -E "error|warning|critical" logfile.txt

# Fixed string search (faster, no regex)
$ grep -F "literal.string" file.txt

# Search for whole word only
$ grep -w "error" logfile.txt
```

---

### `locate` - Fast File Search

```bash
# Find files and directories by name (uses database)
$ locate filename

# Case-insensitive search
$ locate -i filename

# Limit results
$ locate -n 10 filename

# Show statistics
$ locate -S
Database /var/lib/mlocate/mlocate.db:
    8,116 directories
    103,264 files

# Update database (run as root)
$ updatedb

# Search in specific path
$ locate -r '^/home.*\.pdf$'
```

**Note:** `locate` is very fast but uses a database updated daily. Use `find` for real-time searches.

---

### `find` - Real-time File Search

```bash
# Find files by name
$ find /home -name "file.txt"

# Case-insensitive name search
$ find /home -iname "FILE.TXT"

# Find files with wildcard
$ find /home/john -name "*.txt"
$ find /home/john -name 'prefix*'

# Find by type (f=file, d=directory, l=link)
$ find /var -type f -name "*.log"
$ find /home -type d -name "projects"

# Find by size
$ find / -size +100M              # Larger than 100MB
$ find / -size -1M                # Smaller than 1MB
$ find /home -size +100M -size -1G # Between 100MB and 1GB

# Find by modification time
$ find /home -mtime -7            # Modified in last 7 days
$ find /home -mtime +30           # Modified more than 30 days ago
$ find /var/log -mtime 0          # Modified today

# Find by access time
$ find /home -atime -7            # Accessed in last 7 days

# Find by change time
$ find /etc -ctime -1             # Changed in last 24 hours

# Find by permissions
$ find / -perm 777                # Exactly 777
$ find / -perm -u+s               # Files with SUID bit

# Find by owner
$ find /home -user john
$ find /var -group developers

# Find empty files and directories
$ find /tmp -empty

# Find and execute command on results
$ find . -name "*.tmp" -exec rm {} \;
$ find . -name "*.log" -exec chmod 644 {} \;

# Find and prompt before executing
$ find . -name "*.bak" -ok rm {} \;

# Find and execute with multiple files at once
$ find . -name "*.txt" -exec grep "pattern" {} +

# Combine multiple conditions (AND)
$ find /var/log -name "*.log" -size +10M -mtime -7

# OR conditions
$ find /home -name "*.txt" -o -name "*.pdf"

# Exclude directories
$ find /home -path /home/user/.cache -prune -o -name "*.txt" -print

# Find files modified in last 24 hours
$ find /var/www -type f -mtime -1

# Find largest files
$ find /home -type f -exec du -h {} + | sort -rh | head -10
```

---

### `which` and `whereis`

```bash
# Find location of command
$ which python
/usr/bin/python

# Find all instances in PATH
$ which -a python
/usr/bin/python
/usr/local/bin/python

# Find binary, source, and man pages
$ whereis nginx
nginx: /usr/sbin/nginx /etc/nginx /usr/share/man/man8/nginx.8.gz
```

---

### Interview Scenarios

**Scenario 1: "Find all PHP files modified in last 2 days larger than 1MB"**
```bash
$ find /var/www -name "*.php" -type f -mtime -2 -size +1M
```

**Scenario 2: "Find and delete old log files (older than 30 days)"**
```bash
$ find /var/log -name "*.log" -type f -mtime +30 -delete
```

**Scenario 3: "Find files with wrong permissions (777)"**
```bash
$ find / -type f -perm 0777 -ls
```

---

## 13 • 🔐 SSH LOGINS

Secure Shell connections and authentication.

### Basic SSH Connection

```bash
# Connect to host as your local username
$ ssh host
$ ssh 192.168.1.100

# Connect as specific user
$ ssh user@host
$ ssh john@192.168.1.100

# Connect using specific port
$ ssh -p 2222 user@host
$ ssh -p 22000 john@server.com

# Specify identity file (private key)
$ ssh -i ~/.ssh/id_rsa user@host
$ ssh -i /path/to/private-key user@host
```

---

### SSH Key Authentication

```bash
# Generate SSH key pair (RSA 4096-bit)
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/john/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 

# Generate ED25519 key (more secure, smaller)
$ ssh-keygen -t ed25519 -C "your_email@example.com"

# Generate key without passphrase (non-interactive)
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/mykey -N ""

# Copy public key to remote server (easy method)
$ ssh-copy-id user@host
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@host

# Manual method (if ssh-copy-id unavailable)
$ cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# View public key
$ cat ~/.ssh/id_rsa.pub

# Test SSH connection
$ ssh -T user@host
```

---

### SSH Config File

Create `~/.ssh/config` for convenient connections:

```bash
$ cat ~/.ssh/config
Host webserver
    HostName 192.168.1.100
    User john
    Port 22
    IdentityFile ~/.ssh/id_rsa

Host db-server
    HostName 10.0.0.50
    User dbadmin
    Port 2222
    IdentityFile ~/.ssh/db_key

Host github.com
    User git
    IdentityFile ~/.ssh/github_key

# Now connect simply with:
$ ssh webserver
$ ssh db-server
```

---

### SSH Advanced Options

```bash
# Enable X11 forwarding (run GUI apps remotely)
$ ssh -X user@host
$ ssh -Y user@host  # Trusted X11 forwarding

# Port forwarding (local)
$ ssh -L 8080:localhost:80 user@host
# Access remote port 80 via local port 8080

# Port forwarding (remote)
$ ssh -R 8080:localhost:80 user@host
# Remote can access your local port 80 via their 8080

# Dynamic port forwarding (SOCKS proxy)
$ ssh -D 1080 user@host

# Run command on remote host without interactive shell
$ ssh user@host "ls -la /var/log"
$ ssh user@host "df -h && free -m"

# Run local script on remote host
$ ssh user@host 'bash -s' < local_script.sh

# Disable strict host key checking (not recommended for production)
$ ssh -o StrictHostKeyChecking=no user@host

# Keep connection alive
$ ssh -o ServerAliveInterval=60 user@host

# Verbose output (debugging)
$ ssh -v user@host      # Level 1
$ ssh -vv user@host     # Level 2
$ ssh -vvv user@host    # Level 3 (maximum verbosity)

# Connect through jump host (bastion)
$ ssh -J jumphost user@finalhost
$ ssh -J user1@jump1,user2@jump2 user3@final
```

---

### SSH Agent (Key Management)

```bash
# Start SSH agent
$ eval $(ssh-agent)

# Add private key to agent
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/john/.ssh/id_rsa: 

# Add key with lifetime (1 hour)
$ ssh-add -t 3600 ~/.ssh/id_rsa

# List loaded keys
$ ssh-add -l

# Remove key from agent
$ ssh-add -d ~/.ssh/id_rsa

# Remove all keys
$ ssh-add -D

# Kill agent
$ ssh-agent -k
```

---

### SSH Security

```bash
# Set correct permissions
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/id_rsa
$ chmod 644 ~/.ssh/id_rsa.pub
$ chmod 600 ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/config

# Generate strong key
$ ssh-keygen -t ed25519 -a 100

# Change key passphrase
$ ssh-keygen -p -f ~/.ssh/id_rsa
```

---

### SSH Tunneling Examples

```bash
# Access remote MySQL through SSH tunnel
$ ssh -L 3307:localhost:3306 user@dbserver
# Connect to localhost:3307 to reach remote MySQL

# Access internal web server through bastion
$ ssh -L 8080:internal-server:80 user@bastion
# Access http://localhost:8080

# Share local web server with remote
$ ssh -R 8080:localhost:3000 user@remote
# Remote can access your localhost:3000 via their 8080
```

---

### Interview Question

**Q: "How do you troubleshoot SSH connection issues?"**

```bash
# 1. Check if SSH service is running on remote
$ ssh -v user@host  # Verbose output

# 2. Check if port is open
$ nc -zv host 22
$ telnet host 22

# 3. Check firewall
$ sudo ufw status
$ sudo iptables -L

# 4. Check SSH logs on remote
$ sudo tail -f /var/log/auth.log  # Debian/Ubuntu
$ sudo tail -f /var/log/secure    # RHEL/CentOS

# 5. Verify SSH daemon config
$ sudo sshd -t  # Test config syntax

# 6. Check file permissions
$ ls -la ~/.ssh/
```

---

## 14 • 📤 FILE TRANSFERS

Transfer files between local and remote systems.

### SCP - Secure Copy

```bash
# Copy local file to remote server
$ scp file.txt user@server:/tmp/
$ scp file.txt user@192.168.1.100:/home/user/

# Copy remote file to local system
$ scp user@server:/var/log/app.log ./
$ scp user@server:/path/to/file.txt /local/path/

# Copy directory recursively
$ scp -r directory/ user@server:/path/
$ scp -r user@server:/path/directory/ ./

# Copy multiple files
$ scp file1.txt file2.txt user@server:/tmp/
$ scp *.txt user@server:/backup/

# Specify port
$ scp -P 2222 file.txt user@server:/tmp/

# Preserve file attributes (timestamps, permissions)
$ scp -p file.txt user@server:/tmp/

# Limit bandwidth (in Kbit/s)
$ scp -l 1000 largefile.iso user@server:/tmp/

# Use specific identity file
$ scp -i ~/.ssh/mykey file.txt user@server:/tmp/

# Verbose output
$ scp -v file.txt user@server:/tmp/

# Copy between two remote hosts
$ scp user1@server1:/path/file.txt user2@server2:/path/

# Copy all HTML files from server to local /tmp
$ scp user@server:/var/www/*.html /tmp/

# Copy all files recursively from server to local /tmp
$ scp -r user@server:/var/www /tmp/
```

---

### Rsync - Advanced Synchronization

```bash
# Basic synchronization (local)
$ rsync source/ destination/

# Synchronize /home to /backups/
$ rsync -a /home /backups/
$ rsync -a /home/ /backups/home/  # Note the trailing slash

# Remote synchronization
$ rsync -avz /home user@server:/backups/

# Sync from remote to local
$ rsync -avz user@server:/var/www/ /local/backup/

# Dry run (show what would be transferred)
$ rsync -avzn /home user@server:/backups/

# Show progress
$ rsync -avz --progress /home user@server:/backups/

# Delete files in destination that don't exist in source
$ rsync -avz --delete /source/ /destination/

# Exclude files/directories
$ rsync -avz --exclude='*.log' --exclude='cache/' /source/ /dest/

# Include only specific files
$ rsync -avz --include='*.txt' --exclude='*' /source/ /dest/

# Use SSH with specific port
$ rsync -avz -e "ssh -p 2222" /local user@server:/remote/

# Use SSH with identity file
$ rsync -avz -e "ssh -i /path/to/key" /local user@server:/remote/

# Limit bandwidth (KB/s)
$ rsync -avz --bwlimit=1000 /large-files user@server:/backup/

# Resume interrupted transfer
$ rsync -avz --partial /source user@server:/dest/

# Compress during transfer
$ rsync -avz --compress-level=9 /source user@server:/dest/

# Preserve hard links
$ rsync -avzH /source user@server:/dest/

# Show differences only
$ rsync -avz --itemize-changes /source /dest/

# Synchronize with timestamps
$ rsync -avz --update /source /dest/
```

**Rsync flags explained:**
- `a` - Archive mode (preserves permissions, timestamps, symbolic links, etc.)
- `v` - Verbose
- `z` - Compress during transfer
- `h` - Human-readable numbers
- `P` - Show progress and keep partial files
- `n` - Dry run (don't actually transfer)

---

### Rsync over SSH Examples

```bash
# Backup website files
$ rsync -avz --delete /var/www/ user@backup-server:/backups/www/

# Sync only PHP files
$ rsync -avz --include='*.php' --exclude='*' /var/www/ user@server:/backup/

# Backup with exclusions
$ rsync -avz --exclude='node_modules' --exclude='.git' \
    /home/user/project/ user@server:/backups/project/

# Mirror directory (exact copy)
$ rsync -avz --delete --force /source/ user@server:/mirror/

# Backup system directories
$ rsync -aAXv --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} \
    / /backup/
```

---

### Other Transfer Methods

```bash
# SFTP - Secure FTP
$ sftp user@server
sftp> ls                          # List remote files
sftp> lls                         # List local files
sftp> pwd                         # Remote working directory
sftp> lpwd                        # Local working directory
sftp> get remotefile.txt          # Download file
sftp> put localfile.txt           # Upload file
sftp> get -r remote-directory/    # Download directory
sftp> put -r local-directory/     # Upload directory
sftp> quit

# NetCat file transfer (no encryption!)
# On receiver:
$ nc -l 9999 > received_file.txt
# On sender:
$ nc receiver_ip 9999 < file.txt

# Use tar over SSH for fast directory transfer
$ tar czf - /source/directory/ | ssh user@server "tar xzf - -C /destination/"

# Transfer with progress using pv
$ tar czf - /source/ | pv | ssh user@server "tar xzf - -C /dest/"
```

---

### Interview Scenarios

**Scenario 1: "Sync local directory to remote, excluding logs"**
```bash
$ rsync -avz --exclude='*.log' --exclude='logs/' /var/www/ user@server:/backup/www/
```

**Scenario 2: "Download only new/modified files from server"**
```bash
$ rsync -avzu user@server:/var/www/ /local/backup/
```

**Scenario 3: "Transfer with bandwidth limit (useful for production servers)"**
```bash
$ rsync -avz --bwlimit=500 /large-backup/ user@server:/offsite-backup/
```

---

## 15 • 💾 DISK USAGE

Monitor and analyze disk space usage.

### `df` - Disk Free Space

```bash
# Show free and used space on mounted filesystems
$ df
Filesystem     1K-blocks     Used Available Use% Mounted on
/dev/sda1      102400000 46080000  51456000  48% /
/dev/sda2      204800000 122880000 71680000  64% /home

# Human-readable format (KB, MB, GB)
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1       100G   45G   50G  48% /
/dev/sda2       200G  120G   70G  64% /home
tmpfs           7.8G  1.2M  7.8G   1% /run

# Show inode usage (file count limits)
$ df -i
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/sda1      6553600 245678 6307922    4% /
/dev/sda2     13107200 567890 12539310   5% /home

# Show filesystem type
$ df -T
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/sda1      ext4  100G   45G   50G  48% /
/dev/sda2      ext4  200G  120G   70G  64% /home

# Show specific filesystem
$ df -h /home
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       200G  120G   70G  64% /home

# Exclude specific filesystem types
$ df -h -x tmpfs -x devtmpfs
```

**Interview Question:** *"What does 100% inode usage mean?"*
- **Answer:** No more files can be created even if disk space is available, because the filesystem has run out of inodes (file index entries). Solution: Delete files or increase inode count.

---

### `du` - Disk Usage

```bash
# Show disk usage for all files and directories (human-readable)
$ du -ah
4.0K    ./file1.txt
2.0M    ./images/photo.jpg
50M     ./videos/
52M     .

# Show total disk usage of current directory
$ du -sh
52M     .

# Show disk usage of specific directory
$ du -sh /var/log/
2.5G    /var/log/

# Show size of all subdirectories (one level deep)
$ du -h --max-depth=1
4.0M    ./documents
2.0G    ./videos
50M     ./images
2.1G    .

# Alternative: limit depth
$ du -h -d 1 /var/
120M    /var/log
45M     /var/cache
15M     /var/tmp
180M    /var

# Show largest directories (top 10)
$ du -ah | sort -rh | head -10
2.1G    .
2.0G    ./videos
120M    ./documents/projects
50M     ./images

# Sort by size (human-readable)
$ du -sh * | sort -hr
2.0G    videos
120M    documents
50M     images
4.0M    scripts

# Exclude specific directories
$ du -sh --exclude='*.log' --exclude='cache' /var/

# Show only directories, not files
$ du -h --max-depth=1 | sort -rh

# Find directories larger than 1GB
$ du -h / 2>/dev/null | grep '^[0-9.]*G'

# Show disk usage with apparent size
$ du -h --apparent-size file.txt
```

---

### Finding Large Files

```bash
# Find largest files in current directory
$ find . -type f -exec du -h {} + | sort -rh | head -20

# Find files larger than 100MB
$ find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null

# Find largest files system-wide
$ find / -type f -printf '%s %p\n' 2>/dev/null | sort -rn | head -20

# Human-readable version
$ find / -type f -exec du -h {} + 2>/dev/null | sort -rh | head -20

# Find large log files
$ find /var/log -type f -size +50M -exec ls -lh {} \;

# Find old and large files (older than 30 days, larger than 100MB)
$ find /var -type f -mtime +30 -size +100M -exec ls -lh {} \;
```

---

### Disk Usage Analysis Tools

```bash
# NCurses Disk Usage (interactive)
$ ncdu /
$ ncdu /home

# Graphical disk usage analyzer
$ baobab  # GNOME Disk Usage Analyzer

# Show disk usage as a tree
$ tree -h --du /path/

# Detailed disk usage report
$ df -h && echo && du -sh /*
```

---

### Monitoring Disk I/O

```bash
# Show I/O statistics
$ iostat
$ iostat -x 1  # Extended stats every 1 second

# Monitor disk I/O by process
$ iotop
$ iotop -o  # Show only processes doing I/O

# Disk I/O stats (detailed)
$ iostat -dx 1
Device            r/s     w/s     rkB/s     wkB/s   await  %util
sda             12.34   45.67    234.56    789.12    5.23   45.6
```

---

### Cleanup Commands

```bash
# Find and delete old log files
$ find /var/log -name "*.log" -mtime +30 -delete

# Find and delete empty directories
$ find /tmp -type d -empty -delete

# Clear system cache (requires root)
$ sync && echo 3 > /proc/sys/vm/drop_caches

# Clean APT cache (Debian/Ubuntu)
$ apt clean
$ apt autoclean

# Clean YUM cache (RHEL/CentOS)
$ yum clean all

# Find duplicate files
$ fdupes -r /home/user/

# Compress old log files
$ find /var/log -name "*.log" -mtime +7 -exec gzip {} \;
```

---

### Interview Scenarios

**Scenario 1: "Disk is 100% full, find what's using space"**
```bash
$ df -h                          # Identify full filesystem
$ du -sh /* | sort -rh           # Find large directories
$ du -sh /var/* | sort -rh       # Drill down
$ find /var -type f -size +100M  # Find large files
$ lsof | grep deleted            # Find deleted files still held open
```

**Scenario 2: "Clean up disk space automatically"**
```bash
# Create cleanup script
$ cat > /usr/local/bin/cleanup.sh << 'EOF'
#!/bin/bash
# Delete logs older than 30 days
find /var/log -name "*.log" -mtime +30 -delete
# Delete temp files older than 7 days
find /tmp -mtime +7 -delete
# Clean package cache
apt clean
EOF

$ chmod +x /usr/local/bin/cleanup.sh

# Add to cron (run weekly)
$ crontab -e
0 2 * * 0 /usr/local/bin/cleanup.sh
```

---

## 16 • 🧭 DIRECTORY NAVIGATION

Efficient directory navigation and management.

### Basic Navigation

```bash
# Go to home directory
$ cd
$ cd ~
$ cd $HOME

# Go to specific directory
$ cd /etc
$ cd /var/log
$ cd ~/projects/linux-guide

# Go up one level
$ cd ..

# Go up two levels
$ cd ../..

# Go to previous directory
$ cd -
$ cd -  # Toggle between last two directories

# Stay in current directory (useful in scripts)
$ cd .
```

---

### Advanced Navigation Techniques

```bash
# CDPATH - Search path for cd command
$ export CDPATH=.:~:/var/log:/etc
$ cd nginx  # Will search for nginx in CDPATH

# Create directory and cd into it
$ mkdir -p ~/projects/new-project && cd $_
$ mkdir new-dir && cd $_

# Use pushd and popd for directory stack
$ pwd
/home/john

$ pushd /var/log
/var/log ~
$ pwd
/var/log

$ pushd /etc
/etc /var/log ~
$ pwd
/etc

$ popd
/var/log ~
$ pwd
/var/log

$ popd
~
$ pwd
/home/john

# View directory stack
$ dirs
/etc /var/log /home/john

# Switch to directory by stack index
$ pushd +1
```

---

### Directory Bookmarks

```bash
# Create bookmarks using symbolic links
$ ln -s /var/log ~/bookmarks/logs
$ ln -s /etc/nginx ~/bookmarks/nginx-config
$ cd ~/bookmarks/logs

# Using environment variables
$ export PROJECTS=~/projects
$ export LOGS=/var/log
$ cd $PROJECTS
$ cd $LOGS

# Add to ~/.bashrc for persistence
$ echo 'export PROJECTS=~/projects' >> ~/.bashrc
```

---

### Useful Aliases

```bash
# Create navigation aliases
$ alias ..='cd ..'
$ alias ...='cd ../..'
$ alias ....='cd ../../..'
$ alias ~='cd ~'
$ alias -- -='cd -'

# Directory listing aliases
$ alias ll='ls -lah'
$ alias la='ls -A'
$ alias l='ls -CF'

# Quick directory access
$ alias projects='cd ~/projects'
$ alias logs='cd /var/log'
$ alias nginx='cd /etc/nginx'

# Add to ~/.bashrc or ~/.bash_aliases
$ cat >> ~/.bashrc << 'EOF'
alias ..='cd ..'
alias ...='cd ../..'
alias projects='cd ~/projects'
alias logs='cd /var/log'
EOF
```

---

### Directory Information

```bash
# Show current directory
$ pwd
/home/john/projects/linux-guide

# Show physical path (resolve symlinks)
$ pwd -P

# Count files in directory
$ ls | wc -l

# Count files including hidden
$ ls -A | wc -l

# Directory size
$ du -sh .

# Number of subdirectories
$ find . -type d | wc -l

# Number of files
$ find . -type f | wc -l

# Tree view of directory
$ tree
$ tree -L 2      # Limit depth to 2
$ tree -d        # Directories only
$ tree -h        # Human-readable sizes
```

---

### Directory Operations

```bash
# Create nested directories
$ mkdir -p projects/web/frontend/src

# Create multiple directories
$ mkdir dir1 dir2 dir3

# Create directory with specific permissions
$ mkdir -m 755 public_dir

# Remove empty directory
$ rmdir empty_dir

# Remove directory and contents
$ rm -r directory/
$ rm -rf directory/  # Force, no prompts

# Copy directory preserving structure
$ cp -r source/ destination/

# Move/rename directory
$ mv old_name new_name
$ mv directory/ /new/path/
```

---

### Navigation Tips & Tricks

```bash
# Use tab completion
$ cd /var/lo[TAB]      # Completes to /var/log
$ cd ~/proj[TAB]       # Completes to ~/projects

# Use wildcards
$ cd ~/pro*/lin*       # Goes to ~/projects/linux-guide

# Find and cd to directory
$ cd $(find /home -name "project-name" -type d 2>/dev/null | head -1)

# Recent directories
$ pwd >> ~/.dir_history
$ tail -5 ~/.dir_history

# Undo cd (go back)
$ cd -
$ cd -
$ cd -  # Toggle back and forth

# Auto cd (bash 4+)
$ shopt -s autocd
$ /var/log          # Automatically does: cd /var/log
$ ..                # Automatically does: cd ..
```

---

### Advanced Tools

```bash
# fzf - Fuzzy finder for directories
$ cd $(find ~ -type d | fzf)

# autojump - Learn your habits, jump to frequent directories
$ j projects        # Jumps to most frecent directory matching "projects"
$ j -s              # Show statistics

# z - Jump to frecent directories
$ z projects
$ z -l              # List all directories
```

---

## 17 • 💻 PROGRAMMING

Development tools and compilers.

### Make - Build Automation

```bash
# Compile using Makefile
$ make

# Clean build artifacts
$ make clean

# Install compiled binaries
$ make install

# Uninstall
$ make uninstall

# View Makefile targets
$ make help

# Compile specific target
$ make target_name

# Parallel compilation (4 jobs)
$ make -j4

# Dry run (show commands without executing)
$ make -n
```

---

### GCC - GNU C Compiler

```bash
# Compile C program
$ gcc hello.c -o hello

# Compile with warnings
$ gcc -Wall hello.c -o hello

# Compile with debugging symbols
$ gcc -g hello.c -o hello

# Compile with optimization
$ gcc -O2 hello.c -o hello
$ gcc -O3 hello.c -o hello  # Maximum optimization

# Link with library
$ gcc program.c -o program -lm  # Link math library

# Compile multiple files
$ gcc main.c utils.c helper.c -o program

# Generate preprocessor output
$ gcc -E source.c

# Generate assembly code
$ gcc -S source.c

# Compile to object file (don't link)
$ gcc -c source.c

# Show all warnings
$ gcc -Wall -Wextra -Werror source.c -o program

# Compile for debugging with gdb
$ gcc -g -O0 program.c -o program
```

---

### G++ - GNU C++ Compiler

```bash
# Compile C++ program
$ g++ hello.cpp -o hello

# Specify C++ standard
$ g++ -std=c++11 program.cpp -o program
$ g++ -std=c++17 program.cpp -o program
$ g++ -std=c++20 program.cpp -o program

# Compile with all warnings
$ g++ -Wall -Wextra hello.cpp -o hello

# Compile with optimization
$ g++ -O3 program.cpp -o program

# Link with libraries
$ g++ program.cpp -o program -lpthread -lboost_system
```

---

### Debugging and Analysis Tools

```bash
# GDB - GNU Debugger
$ gdb ./program
(gdb) run
(gdb) break main
(gdb) next
(gdb) print variable
(gdb) quit

# Run program with arguments in gdb
$ gdb --args ./program arg1 arg2

# ctrace - C program debugger
$ ctrace program.c

# Valgrind - Memory leak detector
$ valgrind ./program
$ valgrind --leak-check=full ./program

# strace - System call tracer
$ strace ./program
$ strace -o output.txt ./program

# ltrace - Library call tracer
$ ltrace ./program
```

---

### Code Analysis and Formatting

```bash
# View program sizes
$ size program
   text    data     bss     dec     hex filename
   1234     567      89    1890     762 program

# Print program's name list (symbols)
$ nm program
0000000000001234 T main
0000000000005678 D global_var

# Strip symbol table (reduce size)
$ strip program

# Before stripping
$ ls -lh program
-rwxr-xr-x 1 john john 100K Dec 27 10:30 program

# After stripping
$ strip program
$ ls -lh program
-rwxr-xr-x 1 john john 45K Dec 27 10:30 program

# C++ beautifier
$ bcpp source.cpp

# Indent and format C code
$ indent -kr -i4 source.c         # Kernighan & Ritchie style
$ indent -gnu source.c             # GNU style
$ indent -linux source.c           # Linux kernel style

# Generate C program cross-reference
$ cxref program.c > reference.html
```

---

### Build Tools

```bash
# CMake - Cross-platform build system
$ mkdir build && cd build
$ cmake ..
$ make
$ make install

# Autotools (configure, make, make install)
$ ./configure
$ ./configure --prefix=/usr/local
$ make
$ sudo make install

# Ninja - Fast build system
$ ninja
$ ninja -j8  # 8 parallel jobs

# Scons - Python-based build tool
$ scons
$ scons -c  # Clean
```

---

### Python Development

```bash
# Run Python script
$ python script.py
$ python3 script.py

# Run Python module
$ python -m module_name

# Interactive Python shell
$ python
$ python3

# Install package with pip
$ pip install package_name
$ pip3 install package_name

# Requirements file
$ pip install -r requirements.txt

# Create virtual environment
$ python -m venv myenv
$ source myenv/bin/activate
$ deactivate

# Byte-compile Python files
$ python -m py_compile script.py

# Python code formatter
$ black script.py

# Python linter
$ pylint script.py
$ flake8 script.py
```

---

### Other Languages

```bash
# Java
$ javac Program.java      # Compile
$ java Program           # Run

# Node.js / JavaScript
$ node script.js

# Ruby
$ ruby script.rb

# Perl
$ perl script.pl

# Bash script
$ bash script.sh
$ ./script.sh  # If executable

# Go
$ go build program.go
$ go run program.go

# Rust
$ rustc program.rs
$ cargo build
$ cargo run
```

---

## 🎓 INTERVIEW PREPARATION

Common Linux interview questions and answers.

### System Administration Questions

#### Q1: "How do you check if a service is running?"

```bash
# Systemd (modern Linux)
$ systemctl status nginx
$ systemctl is-active nginx

# Check process
$ ps aux | grep nginx
$ pgrep nginx

# Check port
$ netstat -tulpn | grep :80
$ ss -tulpn | grep :80
```

---

#### Q2: "How do you find which process is using the most memory?"

```bash
# Method 1: top (Press M to sort by memory)
$ top

# Method 2: ps command
$ ps aux --sort=-%mem | head -10

# Method 3: Specific user
$ ps -u username --sort=-%mem

# Method 4: With human-readable memory
$ ps aux --sort=-%mem | awk '{print $11,$4,$6}' | head -10
```

---

#### Q3: "How do you check disk space and find large files?"

```bash
# Check disk space
$ df -h

# Find largest directories
$ du -sh /* | sort -rh | head -10

# Find large files (>100MB)
$ find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null

# NCurses disk usage (interactive)
$ ncdu /
```

---

#### Q4: "How do you monitor real-time log files?"

```bash
# Follow single log
$ tail -f /var/log/syslog

# Follow multiple logs
$ tail -f /var/log/nginx/access.log /var/log/nginx/error.log

# With grep filter
$ tail -f /var/log/syslog | grep -i error

# Last 100 lines and follow
$ tail -n 100 -f /var/log/application.log

# Using journalctl
$ journalctl -f
$ journalctl -u nginx -f
```

---

#### Q5: "How do you find files modified in the last 24 hours?"

```bash
$ find /var/www -type f -mtime 0
$ find /var/www -type f -mtime -1

# With details
$ find /var/www -type f -mtime -1 -ls

# Specific file type
$ find /var/www -name "*.php" -mtime -1
```

---

### Networking Questions

#### Q6: "How do you troubleshoot network connectivity?"

```bash
# Step 1: Check interface is up
$ ip link show
$ ifconfig

# Step 2: Check IP configuration
$ ip addr show
$ ifconfig -a

# Step 3: Test local connectivity
$ ping -c 4 127.0.0.1

# Step 4: Test gateway
$ ping -c 4 192.168.1.1

# Step 5: Test external connectivity
$ ping -c 4 8.8.8.8

# Step 6: Test DNS
$ nslookup google.com
$ dig google.com

# Step 7: Check routing
$ ip route show
$ traceroute google.com

# Step 8: Check firewall
$ iptables -L -n
$ ufw status
```

---

#### Q7: "How do you check open ports?"

```bash
# All listening ports
$ netstat -tulpn
$ ss -tulpn

# Specific port
$ netstat -tulpn | grep :80
$ lsof -i :80

# Check if port is open remotely
$ nc -zv server.com 80
$ telnet server.com 80
```

---

### Security Questions

#### Q8: "How do you find failed login attempts?"

```bash
# View auth log
$ grep "Failed password" /var/log/auth.log

# Count by IP
$ grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -rn

# Last 10 failed attempts
$ grep "Failed password" /var/log/auth.log | tail -10

# Failed sudo attempts
$ grep "sudo" /var/log/auth.log | grep "FAILED"
```

---

#### Q9: "How do you find files with SUID bit set?"

```bash
# System-wide search
$ find / -perm -4000 -type f 2>/dev/null

# With details
$ find / -perm -4000 -type f -exec ls -l {} \; 2>/dev/null

# SUID and SGID
$ find / -type f \( -perm -4000 -o -perm -2000 \) -exec ls -l {} \; 2>/dev/null
```

---

#### Q10: "How do you check for listening services?"

```bash
# All listening ports with processes
$ netstat -tulpn | grep LISTEN
$ ss -tulpn | grep LISTEN

# Using lsof
$ lsof -i -n -P | grep LISTEN

# Specific service
$ systemctl status nginx
$ ps aux | grep nginx
```

---

### Performance Questions

#### Q11: "System is slow, how do you troubleshoot?"

```bash
# Step 1: Check load average
$ uptime
$ w

# Step 2: Check CPU usage
$ top
$ mpstat 1 5

# Step 3: Check memory
$ free -h
$ vmstat 1 5

# Step 4: Check disk I/O
$ iostat -x 1 5
$ iotop

# Step 5: Check processes
$ ps aux --sort=-%cpu | head -10
$ ps aux --sort=-%mem | head -10

# Step 6: Check disk space
$ df -h

# Step 7: Check network
$ netstat -s
$ iftop
```

---

#### Q12: "How do you check CPU information?"

```bash
# Detailed CPU info
$ lscpu

# CPU cores
$ nproc
$ grep -c ^processor /proc/cpuinfo

# CPU model
$ grep "model name" /proc/cpuinfo | uniq

# All CPU details
$ cat /proc/cpuinfo
```

---

## 🔥 REAL-WORLD SCENARIOS

Practical scenarios you'll encounter in production.

### Scenario 1: Server is Running Out of Disk Space

```bash
# Step 1: Identify full filesystem
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1       50G   49G  1.0G  98% /

# Step 2: Find largest directories
$ du -sh /* | sort -rh | head -10
15G     /var
12G     /home
8G      /usr

# Step 3: Drill down into /var
$ du -sh /var/* | sort -rh | head -10
10G     /var/log
3G      /var/cache
2G      /var/lib

# Step 4: Find large log files
$ find /var/log -type f -size +100M -exec ls -lh {} \;

# Step 5: Compress old logs
$ find /var/log -name "*.log" -mtime +7 -exec gzip {} \;

# Step 6: Delete old logs
$ find /var/log -name "*.log.gz" -mtime +30 -delete

# Step 7: Find deleted files still held open
$ lsof | grep deleted

# Step 8: Restart services holding deleted files
$ systemctl restart nginx
```

---

### Scenario 2: High CPU Usage Investigation

```bash
# Step 1: Identify CPU-intensive processes
$ top -b -n 1 | head -20
$ ps aux --sort=-%cpu | head -10

# Step 2: Get process details
$ ps -p PID -f
$ lsof -p PID

# Step 3: Check process threads
$ ps -eLf | grep PID

# Step 4: Monitor specific process
$ top -p PID

# Step 5: Trace system calls
$ strace -p PID

# Step 6: Check process priority
$ ps -eo pid,ni,cmd | grep PID

# Step 7: Reduce priority if needed
$ renice -n 10 -p PID
```

---

### Scenario 3: Cannot SSH to Server

```bash
# Step 1: Check if port is open
$ nc -zv server.com 22
$ telnet server.com 22

# Step 2: Try verbose SSH
$ ssh -vvv user@server

# Step 3: Check from another client
$ ssh user@server  # From different machine

# Step 4: Check server firewall (if you have console access)
$ iptables -L -n | grep 22
$ ufw status

# Step 5: Check SSH service status
$ systemctl status sshd
$ systemctl status ssh

# Step 6: Check SSH logs
$ tail -f /var/log/auth.log
$ journalctl -u sshd -f

# Step 7: Verify SSH config
$ sshd -t
$ cat /etc/ssh/sshd_config | grep -v "^#"

# Step 8: Check file permissions
$ ls -la ~/.ssh/
$ ls -la /etc/ssh/
```

---

### Scenario 4: Application Won't Start

```bash
# Step 1: Check if port is already in use
$ netstat -tulpn | grep :8080
$ lsof -i :8080

# Step 2: Kill process using the port
$ kill -9 PID

# Step 3: Check application logs
$ tail -f /var/log/application/error.log

# Step 4: Check system logs
$ journalctl -xe
$ tail -f /var/log/syslog

# Step 5: Check file permissions
$ ls -la /path/to/application

# Step 6: Check disk space
$ df -h

# Step 7: Check dependencies
$ ldd /path/to/application/binary

# Step 8: Check configuration
$ /path/to/application --test-config

# Step 9: Test network connectivity
$ ping -c 4 database-server
$ nc -zv database-server 5432

# Step 10: Try starting manually
$ /path/to/application --debug
```

---

### Scenario 5: Find Source of High Network Traffic

```bash
# Step 1: Monitor network interfaces
$ ifconfig
$ ip -s link

# Step 2: Real-time bandwidth monitoring
$ iftop -i eth0
$ nethogs

# Step 3: Check connections
$ netstat -an | grep ESTABLISHED | wc -l
$ ss -s

# Step 4: Find top talkers
$ netstat -an | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -rn | head -10

# Step 5: Monitor specific port
$ tcpdump -i eth0 port 80 -c 100

# Step 6: Check process network usage
$ nethogs eth0

# Step 7: Save capture for analysis
$ tcpdump -i eth0 -w capture.pcap
$ wireshark capture.pcap  # Analyze on desktop
```

---

### Scenario 6: Recover Accidentally Deleted File

```bash
# Step 1: Check if file is still open by a process
$ lsof | grep filename

# Step 2: Copy from file descriptor
$ cp /proc/PID/fd/FD /path/to/recovered/file

# Step 3: Use extundelete (ext3/ext4)
$ extundelete /dev/sda1 --restore-file /path/to/file

# Step 4: Use testdisk/photorec
$ photorec /dev/sda1

# Step 5: Check backups
$ rsync -avz backup-server:/backups/file ./

# Prevention: Create aliases
$ alias rm='rm -i'  # Ask before delete
$ alias rm='echo "Use /bin/rm or trash-cli instead"'
```

---

### Scenario 7: Automate Daily Backups

```bash
# Create backup script
$ cat > /usr/local/bin/daily-backup.sh << 'EOF'
#!/bin/bash

# Configuration
SOURCE="/var/www"
DEST="/backups"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_NAME="backup_$DATE"
RETENTION_DAYS=30

# Create backup
tar -czf "$DEST/$BACKUP_NAME.tar.gz" "$SOURCE"

# Sync to remote server
rsync -avz "$DEST/$BACKUP_NAME.tar.gz" backup-server:/offsite-backups/

# Delete old backups
find "$DEST" -name "backup_*.tar.gz" -mtime +$RETENTION_DAYS -delete

# Send notification
echo "Backup completed: $BACKUP_NAME" | mail -s "Daily Backup" admin@example.com
EOF

# Make executable
$ chmod +x /usr/local/bin/daily-backup.sh

# Add to crontab (run daily at 2 AM)
$ crontab -e
0 2 * * * /usr/local/bin/daily-backup.sh >> /var/log/backup.log 2>&1
```

---

### Scenario 8: Monitor and Alert on High Load

```bash
# Create monitoring script
$ cat > /usr/local/bin/monitor-load.sh << 'EOF'
#!/bin/bash

# Get number of CPUs
CPU_COUNT=$(nproc)

# Get 1-minute load average
LOAD=$(uptime | awk -F'load average:' '{print $2}' | awk '{print $1}' | sed 's/,//')

# Threshold (1.5x number of CPUs)
THRESHOLD=$(echo "$CPU_COUNT * 1.5" | bc)

# Compare (convert to integer)
LOAD_INT=$(echo "$LOAD * 100" | bc | cut -d. -f1)
THRESHOLD_INT=$(echo "$THRESHOLD * 100" | bc | cut -d. -f1)

if [ $LOAD_INT -gt $THRESHOLD_INT ]; then
    # Get top processes
    TOP_PROCS=$(ps aux --sort=-%cpu | head -6 | tail -5)
    
    # Send alert
    echo -e "High load detected: $LOAD\n\nTop processes:\n$TOP_PROCS" | \
        mail -s "ALERT: High Load on $(hostname)" admin@example.com
fi
EOF

# Make executable
$ chmod +x /usr/local/bin/monitor-load.sh

# Run every 5 minutes
$ crontab -e
*/5 * * * * /usr/local/bin/monitor-load.sh
```

---

## 🎯 Quick Tips & Best Practices

### Productivity Tips

1. **Use history effectively**
```bash
$ history | grep command
$ !123              # Run command #123 from history
$ !!                # Repeat last command
$ sudo !!           # Run last command with sudo
$ !$                # Last argument of previous command
$ !*                # All arguments of previous command
```

2. **Use aliases**
```bash
$ alias update='sudo apt update && sudo apt upgrade'
$ alias ports='netstat -tulpn | grep LISTEN'
$ alias meminfo='free -h && ps aux --sort=-%mem | head -10'
```

3. **Use functions in .bashrc**
```bash
mkcd() {
    mkdir -p "$1" && cd "$1"
}

extract() {
    if [ -f "$1" ]; then
        case "$1" in
            *.tar.gz) tar xzf "$1" ;;
            *.zip) unzip "$1" ;;
            *.tar.bz2) tar xjf "$1" ;;
            *) echo "Unknown archive format" ;;
        esac
    fi
}
```

---

### Safety Best Practices

1. **Always use -i for destructive operations**
```bash
$ alias rm='rm -i'
$ alias mv='mv -i'
$ alias cp='cp -i'
```

2. **Test dangerous commands with echo first**
```bash
# Bad
$ find /important -name "*.tmp" -delete

# Good
$ find /important -name "*.tmp" -exec echo {} \;  # Review first
$ find /important -name "*.tmp" -delete           # Then delete
```

3. **Use shellcheck for scripts**
```bash
$ shellcheck script.sh
```

---

## 📚 Additional Resources

- [Linux Documentation Project](https://tldp.org/)
- [Ubuntu Official Documentation](https://help.ubuntu.com/)
- [Red Hat Enterprise Linux Documentation](https://access.redhat.com/documentation/)
- [Arch Linux Wiki](https://wiki.archlinux.org/)
- [ExplainShell](https://explainshell.com/) - Explain any shell command
- [Command Line Challenge](https://cmdchallenge.com/)

---

## 🤝 Contributing

Found an error or want to add more commands? Contributions are welcome!

1. Fork the repository
2. Add your improvements
3. Submit a pull request

---

## 📝 License

This guide is open source and available for educational purposes.

---

<div align="center">

**⭐ Star this repository if it helped you ace your Linux interview! ⭐**

**Made with ❤️ for Linux professionals, system administrators, and DevOps engineers worldwide**

</div>
