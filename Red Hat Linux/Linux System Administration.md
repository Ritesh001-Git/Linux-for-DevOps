# Linux System Administration

> Important Linux concepts and commands for interviews and practical revision (RHEL)

## Table of Contents

- [1. Hostname and Name Resolution](#1-hostname-and-name-resolution)
- [2. Archiving and File Transfer](#2-archiving-and-file-transfer)
- [3. Package Management](#3-package-management)
- [4. Scheduling Jobs](#4-scheduling-jobs)
- [5. System Performance Tuning](#5-system-performance-tuning)
- [6. Access Control Lists (ACLs)](#6-access-control-lists-acls)

---

## 1. Hostname and Name Resolution

### Hostname

A hostname is the name assigned to a computer or server in a network. It makes systems easier to identify than using IP addresses.

### Important Commands

| Command | Description |
|---|---|
| `hostname` | Displays the current hostname |
| `hostnamectl` | Displays hostname and system information |
| `hostnamectl set-hostname server1` | Changes the system hostname |
| `cat /etc/hostname` | Displays the hostname stored in the configuration file |
| `hostname -I` | Displays system IP addresses |

### Name Resolution

Name resolution converts a hostname into an IP address.

Linux commonly uses:

- `/etc/hosts` – Local hostname-to-IP mappings.
- DNS – Resolves names using DNS servers.
- `/etc/resolv.conf` – Contains DNS resolver configuration.

### Example: Local Name Resolution

```bash
sudo vi /etc/hosts
```

Add:

```text
192.168.64.100 server1
192.168.64.101 server2
```

Now the system can resolve these names locally.

Verify:

```bash
getent hosts server1
```

---

## 2. Archiving and File Transfer

### What is Archiving?

Archiving combines multiple files and directories into a single archive file.

### What is Compression?

Compression reduces the size of data to save storage space and transfer bandwidth.

### TAR Commands

| Command | Description |
|---|---|
| `tar -cvf archive.tar file1 file2` | Creates an uncompressed archive |
| `tar -xvf archive.tar` | Extracts an archive |
| `tar -tvf archive.tar` | Displays archive contents |
| `tar -czvf archive.tar.gz directory/` | Creates a gzip-compressed archive |
| `tar -xzvf archive.tar.gz` | Extracts a gzip-compressed archive |
| `tar -cJvf archive.tar.xz directory/` | Creates an xz-compressed archive |
| `tar -xJvf archive.tar.xz` | Extracts an xz-compressed archive |

### Important TAR Options

| Option | Meaning |
|---|---|
| `c` | Create archive |
| `x` | Extract archive |
| `v` | Verbose output |
| `f` | Specify archive filename |
| `z` | gzip compression |
| `J` | xz compression |
| `t` | List archive contents |

### ZIP Commands

ZIP archives are commonly used for compressed file packaging and sharing.

| Command | Description |
|---|---|
| `zip archive.zip file1.txt file2.txt` | Creates a ZIP archive |
| `zip -r archive.zip directory/` | Compresses a directory recursively |
| `unzip archive.zip` | Extracts ZIP archive |
| `unzip -l archive.zip` | Lists ZIP contents |

Install ZIP utilities if required:

```bash
sudo dnf install zip unzip -y
```

### Secure Copy – SCP

SCP securely copies files between systems over SSH.

```bash
scp file.txt user@192.168.64.101:/home/user/
```

Copies a local file to a remote system.

```bash
scp user@192.168.64.101:/home/user/file.txt .
```

Copies a remote file to the current directory.

```bash
scp -r directory/ user@192.168.64.101:/home/user/
```

Copies a directory recursively.

### Secure Synchronization – RSYNC

RSYNC synchronizes files and directories between systems. It transfers only the required differences when possible, making repeated transfers efficient.

```bash
rsync -av directory/ user@192.168.64.101:/home/user/directory/
```

Important options:

- `a` – Archive mode; preserves important file attributes and copies recursively.
- `v` – Verbose output.
- `z` – Compress data during transfer.

---

## 3. Package Management

### RPM

RPM stands for **Red Hat Package Manager**.

It manages individual software package files in RHEL. RPM can install, remove, query, and verify packages.

### Important RPM Commands

| Command | Description |
|---|---|
| `rpm -ivh package.rpm` | Installs an RPM package |
| `rpm -Uvh package.rpm` | Installs or upgrades a package |
| `rpm -e package_name` | Removes a package |
| `rpm -qa` | Lists installed packages |
| `rpm -qi package_name` | Displays package information |
| `rpm -ql package_name` | Lists files installed by a package |
| `rpm -qf /path/file` | Identifies the package owning a file |
| `rpm -q package_name` | Checks whether a package is installed |

### YUM / DNF

YUM and DNF are package managers that install, update, and remove software while resolving package dependencies automatically.

RHEL 9 primarily uses DNF; the `yum` command is available as a compatible interface.

### Important YUM/DNF Commands

| Command | Description |
|---|---|
| `yum install package_name` | Installs a package |
| `yum remove package_name` | Removes a package |
| `yum update` | Updates installed packages |
| `yum search keyword` | Searches packages |
| `yum info package_name` | Displays package information |
| `yum list installed` | Lists installed packages |
| `yum repolist` | Displays enabled repositories |
| `yum history` | Displays package-management history |
| `yum clean all` | Cleans cached package data |

### YUM Repository

A repository is a location containing software packages and package metadata.

Repository configuration files are generally stored in:

```text
/etc/yum.repos.d/
```

### RPM vs YUM

| RPM | YUM/DNF |
|---|---|
| Manages individual RPM packages | Manages packages through repositories |
| Dependency resolution is not automatic in the same way | Automatically resolves dependencies |
| Can install local RPM files | Can install packages from repositories |
| Lower-level package management | Higher-level package management |

---

## 4. Scheduling Jobs

Linux supports scheduling jobs to execute commands automatically at a specified time.

There are two important scheduling mechanisms:

- **at** – Schedules a one-time job.
- **cron** – Schedules recurring jobs.

### A. AT Jobs – One-Time Scheduling

The `at` command schedules a task to execute once at a future time.

The `atd` daemon executes scheduled AT jobs.

### Important Commands

| Command | Description |
|---|---|
| `at now + 5 minutes` | Schedules a job after five minutes |
| `at 11:00` | Schedules a job at the next 11:00 |
| `atq` | Displays pending AT jobs |
| `atrm JOB_ID` | Removes a scheduled job |
| `at -c JOB_ID` | Displays the commands saved in a job |
| `systemctl status atd` | Checks AT daemon status |
| `sudo systemctl enable --now atd` | Enables and starts AT daemon |

### Example

```bash
at now + 2 minutes
```

Enter the command:

```text
echo "Job executed" > /tmp/job.txt
```

Press `Ctrl+D` on an empty line to submit the job.

Verify:

```bash
atq
```

### B. Cron Jobs – Recurring Scheduling

Cron is used to schedule commands or scripts that execute repeatedly at fixed intervals.

The `crond` service runs scheduled cron jobs.

### Important Commands

| Command | Description |
|---|---|
| `crontab -e` | Edits the current user's cron jobs |
| `crontab -l` | Lists current user's cron jobs |
| `crontab -r` | Removes current user's cron jobs |
| `sudo crontab -e` | Edits root's cron jobs |
| `systemctl status crond` | Checks cron service status |
| `sudo systemctl enable --now crond` | Enables and starts cron service |

### Cron Syntax

```text
MINUTE HOUR DAY_OF_MONTH MONTH DAY_OF_WEEK COMMAND
```

| Field | Range |
|---|---|
| Minute | 0–59 |
| Hour | 0–23 |
| Day of month | 1–31 |
| Month | 1–12 |
| Day of week | 0–7 (Sunday is 0 or 7) |

### Example Cron Jobs

```cron
0 2 * * * /home/user/backup.sh
```

Runs every day at 2 AM.

```cron
*/5 * * * * /home/user/check.sh
```

Runs every five minutes.

```cron
0 9 * * 1 /home/user/report.sh
```

Runs every Monday at 9 AM.

### Special Cron Expressions

| Expression | Meaning |
|---|---|
| `@reboot` | Runs at system startup |
| `@daily` | Runs once every day |
| `@weekly` | Runs once every week |
| `@monthly` | Runs once every month |
| `@hourly` | Runs once every hour |

### Cron Configuration Locations

- `/etc/crontab` – System-wide cron configuration.
- `/etc/cron.d/` – Additional system cron job files.
- `/etc/cron.hourly/` – Hourly scripts.
- `/etc/cron.daily/` – Daily scripts.
- `/etc/cron.weekly/` – Weekly scripts.
- `/etc/cron.monthly/` – Monthly scripts.

### AT vs CRON

| AT | CRON |
|---|---|
| One-time execution | Repeated execution |
| Runs at a specified future time | Runs at recurring intervals |
| Uses `atd` daemon | Uses `crond` service |
| Jobs disappear from queue after execution | Cron schedule remains configured |

---

## 5. System Performance Tuning

### What is Performance Tuning?

Performance tuning is the process of optimizing system resources and configuration settings to improve system efficiency, response time, and throughput according to workload requirements.

### Tuned Service

Tuned is a performance tuning service in RHEL that applies predefined performance profiles.

A profile is a collection of configuration settings designed for a specific workload.

### Important Tuned Commands

| Command | Description |
|---|---|
| `tuned-adm list` | Lists available profiles |
| `tuned-adm active` | Displays active profile |
| `tuned-adm recommend` | Recommends a profile |
| `tuned-adm profile balanced` | Activates balanced profile |
| `tuned-adm profile throughput-performance` | Activates throughput profile |
| `tuned-adm profile latency-performance` | Activates latency profile |
| `tuned-adm profile powersave` | Activates power-saving profile |
| `tuned-adm profile virtual-guest` | Activates virtual machine profile |
| `tuned-adm profile virtual-host` | Activates virtualization host profile |
| `tuned-adm off` | Disables Tuned profile management |

### Important Performance Profiles

| Profile | Purpose |
|---|---|
| `balanced` | Balance between performance and power consumption |
| `powersave` | Reduce power consumption |
| `throughput-performance` | Optimize throughput |
| `latency-performance` | Optimize latency |
| `virtual-guest` | Optimize virtual machines |
| `virtual-host` | Optimize hosts running virtual machines |

### Practical Performance Tuning Workflow

**Step 1: Check the Tuned service**

```bash
systemctl status tuned
```

**Step 2: Start and enable Tuned**

```bash
sudo systemctl enable --now tuned
```

**Step 3: List available profiles**

```bash
tuned-adm list
```

**Step 4: Check recommended profile**

```bash
tuned-adm recommend
```

**Step 5: Check active profile**

```bash
tuned-adm active
```

**Step 6: Apply a suitable profile**

For a general-purpose system:

```bash
sudo tuned-adm profile balanced
```

For a high-throughput workload:

```bash
sudo tuned-adm profile throughput-performance
```

**Step 7: Verify the active profile**

```bash
tuned-adm active
```

### Process Scheduling – Nice Values

Nice values influence the CPU scheduling preference of processes.

- Range: `-20` to `+19`.
- `-20` = Highest scheduling preference.
- `+19` = Lowest scheduling preference.
- Lower nice value means higher scheduling preference.
- Higher nice value means lower scheduling preference.

### Important Nice Commands

| Command | Description |
|---|---|
| `nice -n 10 command` | Runs a command with nice value 10 |
| `sudo nice -n -10 command` | Runs a command with nice value -10 |
| `renice -n 15 -p PID` | Changes the nice value of an existing process |
| `ps -o pid,ni,pri,comm` | Displays PID, nice value, priority, and command |
| `ps -o pid,ni,pri,comm -p PID` | Displays details for a specific process |

### Practical Nice Example

**Step 1: Run a process with nice value 10**

```bash
nice -n 10 sleep 300 &
```

**Step 2: Find its PID and nice value**

```bash
ps -o pid,ni,pri,comm
```

**Step 3: Change its nice value**

```bash
sudo renice -n 15 -p PID
```

Replace `PID` with the actual process ID.

**Step 4: Verify**

```bash
ps -o pid,ni,pri,comm -p PID
```

**Step 5: Stop the process**

```bash
kill PID
```

> Note: Nice values influence scheduling preference but do not guarantee a fixed amount of CPU time.

---

## 6. Access Control Lists (ACLs)

### What is ACL?

ACL stands for **Access Control List**.

ACL is an advanced file permission mechanism in Linux that allows administrators to assign permissions to specific users and groups beyond the traditional owner, group, and others permission categories.

### Why ACL is Required?

Traditional Linux permissions provide three categories:

- Owner
- Group
- Others

ACL allows additional permissions for named users and groups without changing file ownership.

### ACL vs Traditional Permissions

| Traditional Permissions | ACL |
|---|---|
| Owner, group, others | Owner, group, others plus named users and groups |
| Basic permission control | Flexible permission control |
| Cannot separately assign permissions to multiple named users | Can assign permissions to multiple named users |
| No default ACL inheritance | Supports default ACLs |

### ACL Package

ACL commands are provided by the `acl` package.

Install:

```bash
sudo dnf install acl -y
```

### Important ACL Commands

| Command | Description |
|---|---|
| `getfacl file` | Displays ACL permissions |
| `setfacl -m u:username:rwx file` | Gives user permissions |
| `setfacl -m g:groupname:rw file` | Gives group permissions |
| `setfacl -x u:username file` | Removes a user's ACL entry |
| `setfacl -x g:groupname file` | Removes a group's ACL entry |
| `setfacl -b file` | Removes extended ACL entries |
| `setfacl -m d:u:username:rwx directory` | Sets default ACL for a directory |

### Practical ACL Example

**Scenario:** Create a user and group, then give a specific user read and write permissions on a file.

**Step 1: Create a user**

```bash
sudo useradd rahul
```

**Step 2: Create a group**

```bash
sudo groupadd developers
```

**Step 3: Create a file**

```bash
touch project.txt
```

**Step 4: Give Rahul read and write permissions**

```bash
sudo setfacl -m u:rahul:rw project.txt
```

**Step 5: Check ACL**

```bash
getfacl project.txt
```

Expected important entries:

```text
user::rw-
user:rahul:rw-
group::r--
mask::rw-
other::r--
```

**Step 6: Give the developers group read and write permissions**

```bash
sudo setfacl -m g:developers:rw project.txt
```

**Step 7: Verify again**

```bash
getfacl project.txt
```

**Step 8: Remove Rahul's ACL**

```bash
sudo setfacl -x u:rahul project.txt
```

### ACL Mask

The ACL mask defines the maximum effective permissions for:

- Named users
- Named groups
- Owning group

The effective permissions may be lower than the permissions specified in an ACL entry because of the mask.

### Default ACL

A default ACL is associated with a directory and is inherited by newly created files and subdirectories.

Example:

```bash
sudo setfacl -m d:u:rahul:rwx /shared
```

This sets a default ACL for Rahul on the `/shared` directory.

### Important ACL Viva Questions

**Q1. What is ACL?**

ACL is an Access Control List that provides flexible permissions for specific users and groups.

**Q2. How is ACL different from chmod?**

ACL supports additional named users and groups, whereas traditional permissions use owner, group, and others.

**Q3. What is the ACL mask?**

The ACL mask limits effective permissions for named users, named groups, and the owning group.

**Q4. What is a default ACL?**

A default ACL is inherited by newly created files and directories inside a directory.

**Q5. Does ACL replace traditional permissions?**

No. ACL extends the traditional permission system.

---

## Quick Revision – Most Important Commands

| Topic | Command |
|---|---|
| Hostname | `hostnamectl` |
| Change hostname | `hostnamectl set-hostname server1` |
| Name resolution | `getent hosts server1` |
| TAR archive | `tar -cvf archive.tar directory/` |
| Compressed TAR | `tar -czvf archive.tar.gz directory/` |
| Extract TAR | `tar -xvf archive.tar` |
| Extract compressed TAR | `tar -xzvf archive.tar.gz` |
| ZIP | `zip -r archive.zip directory/` |
| Unzip | `unzip archive.zip` |
| SCP | `scp file user@host:/path/` |
| RSYNC | `rsync -av directory/ user@host:/path/` |
| Install package | `yum install package` |
| Remove package | `yum remove package` |
| RPM query | `rpm -qa` |
| AT job | `at now + 5 minutes` |
| AT queue | `atq` |
| Cancel AT job | `atrm JOB_ID` |
| Cron edit | `crontab -e` |
| Cron list | `crontab -l` |
| Tuned profiles | `tuned-adm list` |
| Active profile | `tuned-adm active` |
| Apply profile | `tuned-adm profile balanced` |
| Nice process | `nice -n 10 command` |
| Change nice | `renice -n 15 -p PID` |
| Check nice | `ps -o pid,ni,pri,comm` |
| View ACL | `getfacl file` |
| Set ACL | `setfacl -m u:user:rw file` |
| Remove ACL | `setfacl -x u:user file` |
| Remove extended ACL | `setfacl -b file` |

---

## Interview Preparation Priorities

Focus especially on:

1. Difference between RPM and YUM/DNF.
2. Difference between TAR and ZIP.
3. Difference between SCP and RSYNC.
4. Difference between AT and CRON.
5. Cron syntax and scheduling examples.
6. Tuned profiles and their purposes.
7. Nice values and process scheduling.
8. Difference between ACL and chmod.
9. ACL mask and default ACL.
10. Hostname and name resolution.

