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


## User and Group Management Commands

| Command | Description | Example |
|-------|-------------|--------|
| `sudo adduser -m username` | Creates a new user. The `-m` flag is important because it creates a **home directory** for the user. Without `-m`, the user is created without a personal folder. | `sudo adduser -m ritesh` |
| `sudo passwd username` | Sets or changes the password of a user. | `sudo passwd ritesh` |
| `su username` | Switches from the current user to another user. | `su ritesh` |
| `cat /etc/passwd` | Displays all users in the system along with their user IDs (UID), group IDs (GID), home directory, and shell information. | `cat /etc/passwd` |
| `sudo userdel username` | Deletes a user from the system. | `sudo userdel ritesh` |
| `sudo groupadd groupname` | Creates a new group in the system. | `sudo groupadd devops` |
| `sudo gpasswd -a username groupname` | Adds a user to a specific group. | `sudo gpasswd -a ritesh devops` |
| `sudo gpasswd -M user1,user2,user3 groupname` | Adds multiple users to a group at once. | `sudo gpasswd -M ritesh,rahul,aman devops` |
| `cat /etc/group` | Displays all groups in the system and the users belonging to each group. | `cat /etc/group` |
| `sudo groupdel groupname` | Deletes a group from the system. | `sudo groupdel devops` |

## SSH (Secure Shell)

### What is SSH
SSH (Secure Shell) is a **secure network protocol used to connect to remote servers** over the internet.  
It allows users to **access and manage servers through the command line securely**.

SSH encrypts the communication between the **client (your computer)** and the **server**, which prevents attackers from reading sensitive information like passwords or commands.

---

### SSH Key Authentication

SSH commonly uses **key-based authentication** instead of passwords.

- **Private Key** → Stored securely on the **user's local machine**
- **Public Key** → Stored on the **server**

When a user tries to connect:
1. The server checks the public key.
2. The user proves ownership of the matching private key.
3. If they match, the connection is allowed.

Example key file:

This `.pem` file is the **private key** used to access the server.

---

### Connecting to an AWS EC2 Instance using SSH

Follow these steps to connect to an EC2 instance:

#### 1. Launch an EC2 Instance
- Go to AWS Console
- Open **EC2 Dashboard**
- Click **Launch Instance**
- Download the **.pem key pair file**

Example:

---

#### 2. Go to the Connect Tab
After the instance starts:

1. Select your EC2 instance
2. Click **Connect**
3. Choose **SSH Client**
4. AWS will provide a command like:


---

#### 3. Find the Directory of the `.pem` File

Check where your `.pem` file is downloaded.

Example (Downloads folder): `cd /Downloads`

---

#### 4. Go to the Correct Directory

Use the `cd` command to move to the folder where the `.pem` file exists.
Example: `ssh -i "my-key.pem" ubuntu@ec2-xx-xxx-xxx-xxx.compute.amazonaws.com`


---

#### 6. Successful Connection

After running the command, your terminal will connect to the EC2 server and you will see something like: `ubuntu@ip-172-31-xx-xx:~$`
Now you can **run Linux commands directly on your EC2 server from your terminal**.

## File Permissions in Linux

### Viewing File Permissions

You can check file and directory permissions using:

| Command | Description | Example |
|--------|-------------|--------|
| `ls -l` | Displays detailed file information including permissions, owner, group, size, and timestamp. | `ls -l` |

Example output: `-rwxr-xr-- 1 user group 1200 Mar 4 demo.sh`

Explanation:

- **First character**
  - `d` → directory  
  - `-` → regular file  

- **Next 9 characters represent permissions**
`rwx r-x r--` User Group Other

Meaning:

| Symbol | Meaning |
|------|------|
| r | Read permission |
| w | Write permission |
| x | Execute permission |
| - | Permission not granted |

Order of permissions: User → Group → Others


---

# Permission Numeric System (Binary Representation)

Linux permissions can also be represented using numbers **0–7**.

| Number | Binary | Read (r) | Write (w) | Execute (x) | Meaning |
|------|------|------|------|------|------|
| 0 | 000 | - | - | - | No permission |
| 1 | 001 | - | - | x | Execute only |
| 2 | 010 | - | w | - | Write only |
| 3 | 011 | - | w | x | Write + Execute |
| 4 | 100 | r | - | - | Read only |
| 5 | 101 | r | - | x | Read + Execute |
| 6 | 110 | r | w | - | Read + Write |
| 7 | 111 | r | w | x | Full permission |

Example permission: `chmod 777 cloud`

| Permission | Meaning |
|------|------|
| 7 | User → rwx |
| 7 | Group → rwx |
| 7 | Others → rwx |

So **777 = Full permission for everyone**.

Example:

| Command | Description |
|------|------|
| `chmod 777 cloud` | Full permissions for user, group, and others |
| `chmod 755 cloud` | User → full access, Group → read & execute, Others → read & execute |
| `chmod 715 cloud` | User → full access, Group → execute only, Others → read & execute |

---

### Umask (Default File Permissions)

`umask` defines the **default permissions assigned when new files or directories are created**.

| Command | Description | Example |
|------|------|------|
| `umask` | Displays the default permission mask for new files | `umask` |

Example output: 0022


Meaning:

- User → full permissions
- Group → read and execute
- Others → read and execute

*(You mentioned you will add the umask table image manually.)*

---

### Ownership Commands

| Command | Description | Example |
|------|------|------|
| `chown` | Changes file or directory owner | `chown devops demo.txt` |
| `chgrp` | Changes group ownership of a file | `chgrp dev demo.txt` |

---

### Zip Commands

First install zip utility:

| Command | Description |
|------|------|
| `sudo apt install zip -y` | Installs zip package |

Note:

`-y` means **automatically answer "yes" during installation**.

#### Zip Operations

| Command | Description | Example |
|------|------|------|
| `zip name.zip file.txt` | Compress a single file | `zip data.zip file.txt` |
| `zip -r name.zip folder` | Compress a directory recursively | `zip -r project.zip devops` |
| `unzip name.zip` | Extract zip archive | `unzip project.zip` |

---

### Tar Command

`tar` is commonly used in Linux to **archive and compress files or directories**.

### Difference Between ZIP and TAR

| Feature | ZIP | TAR |
|------|------|------|
| Compression | Compresses files individually | Mainly archives files |
| Linux usage | Less common in Linux systems | Very common in Linux |
| Extensions | `.zip` | `.tar`, `.tar.gz`, `.tar.bz2` |

---

#### Tar Flags

| Flag | Meaning |
|------|------|
| `c` | Create archive |
| `x` | Extract archive |
| `v` | Verbose (show progress) |
| `f` | File name |
| `z` | gzip compression |
| `j` | bzip2 compression |
| `C` | Change directory before operation |

---

#### Tar Examples

| Command | Description |
|------|------|
| `tar -cvzf name.tar.gz dev` | Create compressed archive |
| `tar -xvzf name.tar.gz` | Extract compressed archive |

## File Transfer Commands (Local ↔ Server)

### 1. SCP (Secure Copy)

`scp` is used to **securely copy files between a local machine and a remote server using SSH**.  
It encrypts the data transfer and is commonly used with **AWS EC2 instances**.

---

### Local → Server File Transfer

General command structure: `scp -i key.pem file.txt ubuntu@server-ip:/home/ubuntu`

Explanation of each part:

| Part | Meaning |
|-----|------|
| `scp` | Secure copy command used to transfer files over SSH |
| `-i` | Specifies the **private key file** used for authentication |
| `key.pem` | The **AWS private key (.pem)** used to connect to the server |
| `file.txt` | File from your **local system** that you want to transfer |
| `ubuntu@server-ip` | Username and server address |
| `:/home/ubuntu` | Destination directory on the server |

Example: `scp -i my-key.pem file.txt ubuntu@ec2-12-34-56-78.compute.amazonaws.com:/home/ubuntu`

This command will **copy `file.txt` from your local machine to the `/home/ubuntu` directory on the server**.

---

### Server → Local File Transfer

General command structure: `scp -i key.pem -r ubuntu@server-ip:/home/ubuntu/cloud`

Explanation:

| Part | Meaning |
|-----|------|
| `scp` | Secure copy command |
| `-i key.pem` | Private key for server authentication |
| `-r` | Recursively copy directories |
| `ubuntu@server-ip` | Remote server address |
| `/home/ubuntu/cloud` | File or folder on the server |
| `.` | Current directory on local machine |

Example: `scp -i my-key.pem -r ubuntu@ec2-12-34-56-78.compute.amazonaws.com:/home/ubuntu/cloud`

This command will **copy the `cloud` directory from the server to your local machine**.

---

### 2. RSYNC (Remote Sync)

`rsync` is used to **synchronize files and directories between systems efficiently**.  
It transfers **only changed data**, making it faster than `scp` for large transfers.

---

### Remote Sync Command

General command structure: `rsync -avjz -e "ssh -i linux-dev.pem" /local/path ubuntu@server-ip:/home/ubuntu`

Explanation of flags:

| Flag | Meaning |
|----|----|
| `-a` | Archive mode (preserves permissions, timestamps, etc.) |
| `-v` | Verbose output |
| `-j` | Compression during transfer |
| `-z` | Enables compression for faster transfer |
| `-e` | Specifies remote shell to use (SSH) |

Example: `rsync -avjz -e "ssh -i Downloads/linux-dev.pem" ./project ubuntu@ec2-12-34-56-78.compute.amazonaws.com:/home/ubuntu`

This command will **synchronize the local `project` folder to the server's `/home/ubuntu` directory**.

## Networking Commands

| Command | Description | Example |
|-------|-------------|--------|
| `sudo apt install net-tools -y` | Installs **net-tools package** which provides networking utilities like `ifconfig`, `netstat`, etc. (`-y` automatically confirms installation). | `sudo apt install net-tools -y` |
| `ping` | Checks connectivity between your system and another host by sending ICMP packets. | `ping google.com` |
| `netstat` | Displays network connections, routing tables, interface statistics, and listening ports. | `netstat -tuln` |
| `ifconfig` | Displays or configures network interfaces and IP addresses. | `ifconfig` |
| `ifconfig \| grep inet` | Shows only the **IP address lines** from the interface output. | `ifconfig \| grep inet` |
| `traceroute` | Shows the path packets take to reach a destination server. | `traceroute youtube.com` |
| `tracepath` | Similar to traceroute but does not require root privileges. | `tracepath youtube.com` |
| `mtr` | Combines `ping` and `traceroute` to provide real-time network diagnostics. | `mtr youtube.com` |
| `nslookup` | Queries DNS servers to obtain domain name or IP address mapping. | `nslookup youtube.com` |
| `telnet` | Tests connectivity to a specific port on a server. | `telnet youtube.com 80` |
| `hostname` | Displays the current system hostname. | `hostname` |
| Change hostname | Hostname can be configured in `/etc/hosts` by mapping an IP with a hostname. | `sudo vi /etc/hosts` |
| `iwconfig` | Displays wireless network interface configuration. | `iwconfig` |
| `ss` | Modern replacement for `netstat` to display socket statistics and network connections. | `ss -tuln` |
| `dig` | DNS lookup utility used to query DNS records. | `dig youtube.com` |
| `whois` | Displays domain ownership, registration, and administrative information. | `whois youtube.com` |
| `dig +short` | Displays only the IP address of the domain. | `dig youtube.com +short` |
| `dig +mx` | Displays mail exchange records of a domain. | `dig youtube.com +mx` |
| `dig +trace` | Shows full DNS resolution path from root servers. | `dig youtube.com +trace` |
| `arp` | Displays or modifies the ARP table (maps IP addresses to MAC addresses). | `arp -a` |
| `ip link` | Shows network interface status and MAC addresses. | `ip link` |
| `curl` | Sends HTTP requests to APIs or websites from the command line. | `curl -X GET https://api.example.com` |
| `curl \| jq` | Pipes curl output to `jq` for **formatted JSON output**. | `curl -X GET https://api.example.com \| jq` |
| `wget` | Downloads files from the internet via HTTP/HTTPS/FTP. | `wget https://example.com/file.zip` |
| `sudo iptables -L` | Lists firewall rules configured in iptables. | `sudo iptables -L` |
| `watch` | Runs a command repeatedly at intervals and shows updated output. | `watch -n 5 top` |
| `watch mtr` | Continuously monitors network path statistics. | `watch mtr youtube.com` |
| `nmap` | Network scanner used to discover open ports, services, and operating systems. | `nmap 192.168.1.1` |
| `nmap -sV` | Detects service versions running on open ports. | `nmap -sV 192.168.1.1` |
| `nmap -sn` | Performs a **ping scan** to detect active hosts on the network. | `nmap -sn 192.168.1.0/24` |

## Process Management Commands

| Command | Description | Example |
|--------|-------------|--------|
| `ps` | Displays currently running processes in the system. | `ps aux` |
| `top` | Shows real-time system processes along with CPU and memory usage. | `top` |
| `jobs` | Lists background jobs running in the current shell session. | `jobs` |
| `bg` | Resumes a stopped job and runs it in the background. | `bg %1` |
| `fg` | Brings a background job to the foreground. | `fg %1` |
| `kill` | Terminates a process using its process ID (PID). | `kill 1234` |
| `kill -9` | Forcefully terminates a process. | `kill -9 1234` |
| `nohup` | Runs a process that continues even after the user logs out. Output is saved to `nohup.out`. | `nohup python app.py &` |
| `htop` | Interactive process viewer (better version of `top`). | `htop` |
| `nice` | Starts a process with a specific priority level. | `nice -n 10 python app.py` |
| `renice` | Changes the priority of a running process. | `renice 10 -p 1234` |

## Pro Linux Commands (AWK, SED, GREP)

In Linux, many small text-processing tasks can be done using powerful command-line tools like **AWK, SED, and GREP**.  
Instead of writing a full **shell script**, these tools allow you to quickly **search, filter, transform, and process text files directly from the terminal**.

These commands are heavily used in **DevOps, log analysis, and automation tasks**.

---

# 1. AWK

`awk` is a powerful **text processing tool** used to extract and manipulate data from files, especially column-based data.

| Command | Description |
|-------|-------------|
| `awk '{print}' file.txt` | Prints the entire file |
| `awk '{print $1}' file.txt` | Prints the first column |
| `awk '{print $1,$2}' file.txt` | Prints first and second columns |
| `awk '/INFO/ {print $1,$2}' logs.txt` | Prints columns where line contains "INFO" |
| `awk '{print NF}' file.txt` | Prints number of fields in each line |
| `awk '{print NR,$0}' file.txt` | Prints line number with each line |
| `awk -F ":" '{print $1}' /etc/passwd` | Uses `:` as separator and prints first column |

Example: `awk '{print $1,$3}' data.txt`
Prints column 1 and column 3 from `data.txt`.

---

# 2. SED

`sed` (Stream Editor) is used to **modify text, replace words, delete lines, or edit files automatically**.

| Command | Description |
|-------|-------------|
| `sed 's/linux/unix/' file.txt` | Replace first occurrence of "linux" with "unix" |
| `sed 's/linux/unix/g' file.txt` | Replace all occurrences in a line |
| `sed -n '1,5p' file.txt` | Print lines 1 to 5 |
| `sed '3d' file.txt` | Delete line number 3 |
| `sed '/ERROR/d' logs.txt` | Delete lines containing "ERROR" |
| `sed 's/^/> /' file.txt` | Add `>` at the start of every line |

Example: sed `'s/error/warning/g' logs.txt`
Replaces all `error` words with `warning`.

---

# 3. GREP

`grep` is used to **search for patterns or text inside files**.

| Command | Description |
|-------|-------------|
| `grep "error" logs.txt` | Finds lines containing "error" |
| `grep -i "error" logs.txt` | Case-insensitive search |
| `grep -n "error" logs.txt` | Shows line numbers with results |
| `grep -r "config" /etc` | Recursively search inside directories |
| `grep -v "info" logs.txt` | Shows lines NOT containing "info" |
| `grep -c "error" logs.txt` | Counts occurrences of "error" |

Example: `grep -i "failed" system.log`
Finds all lines containing **failed** ignoring case.

---

These commands are extremely useful in **DevOps tasks**, such as:

- Searching logs
- Filtering configuration files
- Extracting metrics from logs
- Processing structured data quickly

## Volume & Storage Commands

| Command | Description | Example |
|-------|-------------|--------|
| `lsblk` | Lists all **block devices** (disks and partitions) attached to the system. Useful for checking newly attached volumes. | `lsblk` |
| `df -h` | Shows **disk space usage** of all mounted file systems in human-readable format (GB/MB). | `df -h` |
| `df -h /` | Displays the **storage usage of the root filesystem**. | `df -h /` |

### Understanding Block Devices

When you run: `lsblk`

Example output may include device names like:
`xvda` `xvdb` `xvdc` `nvme0n1`

Meaning:

- `/dev/xvda` → Usually the **root volume**
- `/dev/xvdb`, `/dev/xvdc` → Additional attached disks
- `/dev/nvme0n1` → NVMe storage devices (common in modern EC2 instances)

These represent **physical or virtual disks attached to the system**.

---

# Difference Between Attach and Mount

| Concept | Meaning |
|------|------|
| **Attach** | A **cloud-level / hardware-level operation** where a storage device (like an AWS EBS volume) is connected to a server or instance. |
| **Mount** | An **OS-level operation** that makes the attached storage accessible inside the filesystem. |

### Attach

Attaching means **connecting a storage device to a server**.

Example:

- Attaching an **EBS volume to an EC2 instance**
- After attachment, the disk appears as something like: `/dev/xvdc`
- 
But it **cannot be used yet** until it is mounted.

---

### Mount

Mounting means **binding the disk to a directory in the filesystem** so the OS can use it.

Example: Disk → mounted to /data directory

Now the storage is accessible through `/data`.

---

# Simple Summary

| Attach | Mount |
|------|------|
| Hardware / cloud-level action | OS-level action |
| Connect storage to server | Make storage usable in filesystem |
| Example: EBS attached to EC2 | Example: disk mounted to `/data` |

In simple terms:

- **Attach → connect storage to the machine**
- **Mount → make that storage usable in the operating system**
