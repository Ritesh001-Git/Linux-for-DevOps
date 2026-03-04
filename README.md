# Linux Notes

## What is Linux
Linux is an **open-source operating system** based on the Linux kernel.  
It is widely used in servers, cloud infrastructure, embedded systems, and development environments.

Unlike many commercial operating systems, Linux allows users to **view, modify, and distribute its source code** freely.

A key fact often mentioned in tech:

- Around **90% of personal computers use Windows**
- But **around 90% of servers and applications run on Linux**

This is because Linux is **stable, secure, customizable, and efficient for servers and development**.

---
## Linux Architecture Diagram
<img src="linux-arch.png" width="700">

## Types of Applications

Applications can mainly be divided into two types:

### Standalone Applications
Standalone applications run **directly on a computer without needing a web browser or internet connection**.

Examples:
- MS Word
- VLC Media Player
- Calculator apps

### Web Applications
Web applications run on **servers and are accessed through web browsers over the internet**.

Examples:
- Gmail
- Facebook
- Online banking systems

## Web Server vs App Server

### Web Server
A **web server** handles **static content** and delivers it to users through HTTP & HTTPS.

Static content includes:
- HTML files
- CSS files
- Images
- JavaScript files

Example Web Servers:
- Nginx
- Apache

### Application Server
An **application server** handles **dynamic content**.  
It runs backend logic and processes user requests.

Examples:
- Django (Python)
- Node.js (JavaScript)
- Spring Boot (Java)

Dynamic content examples:
- Login systems
- Database queries
- Personalized dashboards

---

## Windows vs Linux

### Windows
- Commercial and **licensed operating system**
- Mostly used for **general personal computing**
- Graphical interface focused
- Less terminal-based work

### Linux
- Distributed under **General Public License (GPL)**
- Strong focus on **development and server environments**
- Heavy use of **terminal, scripting, and automation**
- Highly customizable

---

## What is a Kernel

The **kernel is the core (heart) of an operating system**.

It acts as a bridge between:
- Hardware (CPU, memory, devices)
- Software (applications and programs)

The kernel controls how the system uses hardware resources.

---

## Linux Kernel

The **Linux kernel** manages communication between hardware and software.

Main responsibilities include:
- Process management
- Memory management
- Device management
- File system management
- System security

It ensures programs can safely access system resources.

---

## Shell Scripting

A **shell** is a command-line interface that allows users to interact with the operating system.

Shell scripting is a way to **write scripts that communicate with the Linux kernel and automate tasks**.

Common shells:
- Bash
- Zsh
- Sh

Example uses:
- Automating system tasks
- Running multiple commands automatically
- Managing servers

---

## Bootloader

A **bootloader** is a program that runs when a computer starts.

Its job is to:
- Load the operating system into memory
- Start the kernel
- Initialize the system

Without a bootloader, the operating system cannot start.

---

## Types of Bootloaders

### GRUB (Grand Unified Bootloader)

GRUB is the **most commonly used bootloader in Linux systems**.

Responsibilities:
- Loads the Linux kernel
- Manages the boot process
- Allows selecting between multiple operating systems

Example:
A system with both **Linux and Windows** can use GRUB to choose which OS to start.

## System Level Commands

| Command | Description | Example |
|-------|-------------|--------|
| `uname` | Displays system information such as OS name, kernel version, and architecture. | `uname -a` |
| `uptime` | Shows how long the system has been running along with current load average. | `uptime` |
| `date` | Displays the current system date and time. | `date` |
| `who` | Shows the list of users currently logged into the system. | `who` |
| `whoami` | Displays the username of the current logged-in user. | `whoami` |
| `which` | Shows the full path of a command or executable. | `which python` |
| `id` | Displays user ID (UID), group ID (GID), and groups the user belongs to. | `id` |
| `sudo` | Stands for **SuperUser DO**. Allows a permitted user to run commands with administrative privileges. | `sudo shutdown`, `sudo reboot` |
| `apt` | Package manager used in Debian-based Linux systems to install, update, and remove software packages. | `sudo apt-get install docker.io` |


## Linux Basic Commands

| Command | Description | Example |
|-------|-------------|--------|
| `ls` | Lists files and directories in the current directory. | `ls` |
| `ls -l` | Lists files with detailed information like permissions, owner, size, and date. | `ls -l` |
| `clear` | Clears the terminal screen. | `clear` |
| `mkdir` | Creates a new directory. | `mkdir project` |
| `pwd` | Shows the current working directory path. | `pwd` |
| `touch` | Creates a new empty file. | `touch file.txt` |
| `cd` | Changes the current directory. | `cd project` |
| `cd ..` | Moves one directory back (to the parent directory). | `cd ..` |
| `rm` | Removes a file. | `rm file.txt` |
| `rm -r` | Recursively removes a directory and its contents. | `rm -r cloud` |
| `cat` | Displays the contents of a file. | `cat file.txt` |
| `echo` | Prints text to the terminal or writes text to a file. | `echo "Hello Linux" > file.txt` |
| `head` | Displays the first 10 lines of a file by default. | `head file.txt` |
| `tail` | Displays the last 10 lines of a file by default. | `tail file.txt` |
| `less` | Views file content page by page (scrollable). | `less file.txt` |
| `more` | Displays file content page by page but with limited navigation. | `more file.txt` |
| `cp` | Copies files or directories. | `cp file.txt backup.txt` |
| `mv` | Moves or renames files and directories. | `mv file.txt newfile.txt` |
| `Soft Link (Symbolic Link)` | Creates a shortcut pointing to another file. | `ln -s /path/to/file softlink` |
| `Hard Link` | Creates another reference to the same file data on disk. | `ln /path/to/file hardlink` |
| `cut` | Extracts specific columns or fields from a file. | `cut -c 1-5 file.txt > output.txt` |
| `tee` | Writes output to both the terminal and a file. | `ls \| tee output.txt` |
| `sort` | Sorts lines of text files alphabetically or numerically. | `sort file.txt` |
| `diff` | Shows differences between two files. | `diff file1.txt file2.txt` |
| `wc` | Counts lines, words, and characters in a file. | `wc file.txt` |
| `vi` | Opens the `vi` text editor to create or edit files. | `vi file.txt` |
| `df` | Shows disk space usage of file systems. | `df -h` |
| `top` | Displays real-time system processes and resource usage. | `top` |
| `fuser` | Shows which process is using a file or port. | `fuser file.txt` |
| `kill` | Terminates a process using its process ID (PID). | `kill 1234` |
| `nohup` | Runs a command that continues running even after logout, output saved to `nohup.out`. | `nohup python app.py &` |
| `vmstat` | Displays system performance information such as memory, processes, and CPU usage. | `vmstat` |
| `vmstat -a` | Shows active and inactive memory information. | `vmstat -a` |
