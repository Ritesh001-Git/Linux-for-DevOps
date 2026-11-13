# Essential Linux Commands (5-Minute Interview Sheet)

> A compact list of commonly used Linux commands, grouped by topic. Examples use RHEL/Rocky Linux-style commands. Replace sample names, paths, and PIDs with your own values.

## 1. Basic System Information

```bash
whoami                         # Show current user
hostname                       # Show system hostname
hostnamectl                    # Show hostname and OS details
uname -a                        # Show kernel/system information
uptime                         # Show uptime and load average
date                            # Show current date and time
```

## 2. File and Directory Management

```bash
pwd                             # Show current directory
ls -lah                         # List files, including hidden files, with details
cd /var/log                     # Change directory
mkdir -p /opt/project           # Create directory (including parent directories)
touch /opt/project/app.log      # Create an empty file
cp app.txt backup.txt           # Copy a file
mv old.txt new.txt              # Move or rename a file
rm -i unwanted.txt              # Remove a file after confirmation
find /etc -name "hosts"         # Find a file by name
```

## 3. File Permission and Ownership

```bash
chmod 755 script.sh             # Owner: rwx; group/others: r-x
chmod 644 file.txt              # Owner: rw; group/others: r
sudo chown user1 file.txt       # Change file owner
sudo chown user1:developers file.txt  # Change owner and group
sudo chgrp developers file.txt  # Change group ownership
```

## 4. Text Processing

```bash
cat file.txt                    # Display file contents
less file.txt                   # Read a file page by page
head -n 5 file.txt              # Show first 5 lines
tail -n 5 file.txt              # Show last 5 lines
tail -f /var/log/messages       # Follow a log file live (RHEL)
grep -n "error" app.log         # Search for 'error' with line numbers
wc -l file.txt                 # Count lines
```

## 5. User and Group Management

```bash
sudo useradd -m rahul           # Create user and home directory
sudo passwd rahul                # Set/change user's password
sudo usermod -aG developers rahul  # Add user to supplementary group
sudo groupadd developers        # Create group
id rahul                         # Show user ID and group memberships
getent group developers         # Check group details
```

## 6. Process Management

```bash
ps aux                           # List running processes
top                              # Live process/resource view
pgrep -a nginx                  # Find nginx process and show command
kill 1234                        # Ask process PID 1234 to stop
kill -9 1234                     # Force-stop PID 1234 (use only if normal stop fails)
nice -n 10 sleep 300             # Start command with lower CPU scheduling priority
sudo renice -n 5 -p 1234         # Adjust priority of PID 1234
```

## 7. Networking

```bash
ip addr show                     # Show IP addresses/interfaces
ip route                         # Show routing table/default gateway
ping -c 4 8.8.8.8                # Test network connectivity
ss -tuln                         # Show listening TCP/UDP ports
hostname -I                      # Show assigned IP addresses
nmcli device status             # Show NetworkManager device status
```

## 8. Disk and File System

```bash
lsblk                            # List disks and partitions
df -h                             # Show filesystem space usage
du -sh /var/log                  # Show total size of a directory
blkid                             # Show filesystem UUID/type
```

## 9. Service and System Administration

```bash
sudo systemctl status sshd       # Check SSH service status (RHEL)
sudo systemctl start sshd        # Start SSH service
sudo systemctl stop sshd         # Stop SSH service
sudo systemctl restart sshd      # Restart SSH service
sudo systemctl enable sshd       # Start SSH automatically at boot
sudo systemctl disable sshd      # Disable automatic start at boot
sudo journalctl -u sshd -n 20   # Show last 20 SSH service log lines
```

---

## Quick Interview Tip

If asked to write Linux commands, write **2–4 commands per category** and briefly state what each does. Use `sudo` for administrative actions and replace example values (`rahul`, `developers`, `1234`, file paths) with the actual ones.
