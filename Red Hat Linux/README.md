# Red Hat Enterprise Linux (RHEL)

---

## What is Red Hat Enterprise Linux?

**Red Hat Enterprise Linux (RHEL)** is an enterprise-grade Linux operating system developed by Red Hat. It is designed for servers, cloud workloads, virtualization, containers, application platforms, and enterprise infrastructure.

### Common RHEL use cases

| Use case | Description |
|---|---|
| Servers | Web, application, database, file, DNS, and other server workloads |
| Cloud | Running workloads on AWS, Azure, Google Cloud, and other platforms |
| Virtualization | Hosting and managing virtual machines |
| Containers | Containerized applications and Kubernetes/OpenShift environments |
| Networking | Configuring interfaces, IP addresses, routes, DNS, VLANs, bridges, bonds, and more |
| Security | SELinux, firewalld, identity management, auditing, and enterprise security controls |
| Automation | Administration with shell scripts, Ansible, systemd, and configuration management |
| Enterprise applications | Long-lived, supportable platforms for business applications |

## 1. NetworkManager & nmcli

RHEL uses NetworkManager as its primary network management service.

| Command | Purpose |
|---|---|
| `systemctl status NetworkManager` | Check NetworkManager |
| `sudo systemctl restart NetworkManager` | Restart NetworkManager |
| `sudo systemctl enable --now NetworkManager` | Enable and start it |
| `nmcli general status` | NetworkManager status |
| `nmcli device status` | Show network devices |
| `nmcli device show` | Detailed device information |
| `nmcli device show enp0s1` | Details for one interface |
| `nmcli connection show` | List connection profiles |
| `nmcli connection show --active` | Show active profiles |
| `nmcli connection show dummy02` | Show one profile |
| `sudo nmcli connection up dummy02` | Activate profile |
| `sudo nmcli connection down dummy02` | Deactivate profile |
| `sudo nmcli connection delete dummy02` | Delete profile |

### Create a static Ethernet connection

```bash
sudo nmcli connection add type ethernet con-name dummy02 ifname enp0s1
sudo nmcli connection modify dummy02 ipv4.method manual ipv4.addresses 192.168.64.15/24 ipv4.gateway 192.168.64.2 ipv4.dns "8.8.8.8 1.1.1.1"
sudo nmcli connection up dummy02
```

### DHCP

```bash
sudo nmcli connection modify dummy02 ipv4.method auto
sudo nmcli connection up dummy02
```

---

## 2. RHEL Networking

| Command | Purpose |
|---|---|
| `ip addr` | Show IP addresses |
| `ip -4 addr` | Show IPv4 addresses |
| `ip addr show enp0s1` | Show interface address |
| `ip link` | Show interfaces |
| `ip route` | Show routing table |
| `ip route get 8.8.8.8` | Show route selected for destination |
| `ip neigh` | Show ARP/neighbor table |
| `ping -c 4 <gateway>` | Test gateway |
| `ping -c 4 8.8.8.8` | Test IP connectivity |
| `getent hosts google.com` | Test DNS resolution |
| `dig google.com` | Detailed DNS query |
| `ss -tulpen` | Show listening network sockets |

---

## 3. Network Troubleshooting

```bash
nmcli dev status
ip addr
ip route
ip neigh
ping -c 4 <gateway>
ping -c 4 8.8.8.8
getent hosts google.com
ss -tulpen
journalctl -u NetworkManager
```

NetworkManager logs:

```bash
journalctl -u NetworkManager
journalctl -u NetworkManager -f
journalctl -u NetworkManager -p err..alert
```

---

## 4. systemd Services

| Command | Purpose |
|---|---|
| `systemctl status <service>` | Check service |
| `sudo systemctl start <service>` | Start service |
| `sudo systemctl stop <service>` | Stop service |
| `sudo systemctl restart <service>` | Restart service |
| `sudo systemctl reload <service>` | Reload configuration |
| `sudo systemctl enable <service>` | Enable at boot |
| `sudo systemctl disable <service>` | Disable at boot |
| `sudo systemctl enable --now <service>` | Enable and start |
| `systemctl is-active <service>` | Check active state |
| `systemctl is-enabled <service>` | Check boot state |
| `systemctl --failed` | List failed units |
| `systemctl list-units --type=service` | List services |

---

## 5. journalctl

| Command | Purpose |
|---|---|
| `journalctl` | System journal |
| `journalctl -b` | Current boot logs |
| `journalctl -b -1` | Previous boot |
| `journalctl -f` | Follow logs |
| `journalctl -u sshd` | SSH logs |
| `journalctl -u NetworkManager` | NetworkManager logs |
| `journalctl -p err` | Error messages |
| `journalctl --since today` | Today's logs |
| `journalctl --since "1 hour ago"` | Recent logs |

---

## 6. DNF Package Management

RHEL uses DNF for package management.

| Command | Purpose |
|---|---|
| `dnf search <package>` | Search packages |
| `dnf info <package>` | Package information |
| `sudo dnf install <package>` | Install |
| `sudo dnf remove <package>` | Remove |
| `sudo dnf update` | Update packages |
| `dnf list installed` | Installed packages |
| `dnf list available` | Available packages |
| `dnf history` | Transaction history |
| `dnf history info <ID>` | Transaction details |
| `dnf provides <command-or-file>` | Find providing package |

Example:

```bash
dnf provides /usr/bin/semanage
```

---

## 7. RHEL Repositories

```bash
dnf repolist
dnf repolist all
dnf repoinfo
dnf repolist -v
```

Enable/disable a repository when supported by the installed DNF tooling:

```bash
sudo dnf config-manager --set-enabled <repo-id>
sudo dnf config-manager --set-disabled <repo-id>
```

---

## 8. Red Hat Subscription Management

Used for RHEL registration and subscription/repository management.

| Command | Purpose |
|---|---|
| `sudo subscription-manager status` | Subscription status |
| `sudo subscription-manager identity` | Registered identity |
| `sudo subscription-manager list` | Subscription information |
| `sudo subscription-manager list --consumed` | Consumed subscriptions |
| `sudo subscription-manager register` | Register system |
| `sudo subscription-manager unregister` | Unregister system |
| `sudo subscription-manager refresh` | Refresh subscription data |
| `sudo subscription-manager repos --list` | List repositories |
| `sudo subscription-manager repos --enable=<repo-id>` | Enable repository |
| `sudo subscription-manager repos --disable=<repo-id>` | Disable repository |

---

## 9. SELinux

SELinux is a major RHEL security feature providing mandatory access control.

| Command | Purpose |
|---|---|
| `getenforce` | Show SELinux mode |
| `sestatus` | Detailed SELinux status |
| `ls -Z` | Show file security contexts |
| `ps -eZ` | Show process contexts |
| `id -Z` | Show current security context |
| `getsebool -a` | List SELinux booleans |
| `semanage fcontext -l` | List file-context rules |
| `restorecon -Rv /path` | Restore expected contexts |
| `setsebool -P <boolean> on` | Persistently enable boolean |
| `ausearch -m AVC -ts recent` | Find SELinux AVC denials |

Typical troubleshooting:

```bash
sudo ausearch -m AVC -ts recent
sudo ausearch -m AVC -ts recent | audit2why
```

Custom file context workflow:

```bash
sudo semanage fcontext -a -t <type> "/path(/.*)?"
sudo restorecon -Rv /path
```

> Prefer fixing SELinux policy/context issues rather than disabling SELinux.

---

## 10. firewalld

RHEL commonly uses firewalld for host firewall management.

| Command | Purpose |
|---|---|
| `firewall-cmd --state` | Firewall state |
| `firewall-cmd --get-zones` | List zones |
| `firewall-cmd --get-active-zones` | Active zones |
| `firewall-cmd --get-default-zone` | Default zone |
| `firewall-cmd --list-all` | Current zone configuration |
| `firewall-cmd --list-services` | Allowed services |
| `firewall-cmd --list-ports` | Allowed ports |

Allow a service permanently:

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

Allow a port permanently:

```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
```

Remove:

```bash
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --permanent --remove-port=8080/tcp
sudo firewall-cmd --reload
```

---

## 11. Storage & Filesystems

| Command | Purpose |
|---|---|
| `lsblk` | List block devices |
| `lsblk -f` | Devices + filesystem information |
| `df -h` | Filesystem usage |
| `df -i` | Inode usage |
| `findmnt` | Mounted filesystems |
| `blkid` | UUID/filesystem information |
| `fdisk -l` | Disk/partition information |

---

## 12. LVM

LVM is widely used in RHEL storage administration.

| Command | Purpose |
|---|---|
| `pvs` | Physical volumes |
| `pvdisplay` | Detailed PV information |
| `vgs` | Volume groups |
| `vgdisplay` | Detailed VG information |
| `lvs` | Logical volumes |
| `lvdisplay` | Detailed LV information |

---

## 13. XFS

XFS is a common RHEL filesystem.

```bash
lsblk -f
findmnt
xfs_info /mountpoint
sudo xfs_repair -n /dev/device
```

> Filesystem repair should be performed carefully and normally requires the filesystem to be unmounted.

---

## 14. Persistent Mounts

View filesystem mount configuration:

```bash
cat /etc/fstab
```

Test configured mounts:

```bash
sudo mount -a
```

Verify:

```bash
findmnt
findmnt /mountpoint
```

---

## 15. SSH / OpenSSH Server

```bash
sudo systemctl status sshd
sudo systemctl enable --now sshd
sudo sshd -t
journalctl -u sshd
ss -lntp | grep ssh
```

`sshd -t` is especially useful for validating SSH configuration before restarting the service.

---

## 16. Time Synchronization — chrony

RHEL commonly uses chronyd for time synchronization.

| Command | Purpose |
|---|---|
| `systemctl status chronyd` | Service status |
| `sudo systemctl enable --now chronyd` | Enable/start chronyd |
| `chronyc tracking` | Synchronization status |
| `chronyc sources` | Time sources |
| `chronyc sources -v` | Detailed sources |
| `timedatectl` | Time configuration |

---

## 17. Kernel & Hardware Administration

| Command | Purpose |
|---|---|
| `uname -r` | Kernel version |
| `dmesg` | Kernel messages |
| `lscpu` | CPU information |
| `free -h` | Memory |
| `lspci` | PCI devices |
| `lsusb` | USB devices |
| `lsmod` | Loaded kernel modules |
| `modinfo <module>` | Module information |
| `sudo modprobe <module>` | Load module |
| `sudo modprobe -r <module>` | Remove module |

---

## 18. Boot Troubleshooting

```bash
systemctl --failed
journalctl -b
journalctl -b -1
dmesg
systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain
```

---

## 19. Performance Monitoring

```bash
top
free -h
uptime
vmstat
iostat
```

`iostat` may require the appropriate package to be installed.

---

## 20. Scheduled Tasks

Traditional cron:

```bash
crontab -l
crontab -e
ls /etc/cron.*
```

systemd timers:

```bash
systemctl list-timers
systemctl list-timers --all
```

---

## 21. RPM

Use DNF for normal package management, but RPM is useful for package inspection and verification.

```bash
rpm -qa
rpm -q <package>
rpm -qi <package>
rpm -ql <package>
rpm -V <package>
```

---

## 22. Podman Containers

Podman is the RHEL container engine.

| Command | Purpose |
|---|---|
| `podman --version` | Version |
| `podman ps` | Running containers |
| `podman ps -a` | All containers |
| `podman images` | Images |
| `podman pull <image>` | Pull image |
| `podman run -d --name web <image>` | Run container |
| `podman stop web` | Stop container |
| `podman rm web` | Remove container |
| `podman logs web` | Container logs |
| `podman inspect web` | Container details |
| `podman network ls` | Container networks |
| `podman network inspect <network>` | Network details |
| `podman port <container>` | Published ports |

---

## 23. Cockpit

Cockpit provides web-based RHEL administration.

```bash
rpm -q cockpit
systemctl status cockpit.socket
sudo systemctl enable --now cockpit.socket
ss -lntp | grep 9090
```

Cockpit commonly listens on TCP port `9090`.

---

## 24. Ansible / RHEL Automation

Where Ansible is installed:

```bash
ansible --version
ansible all -m ping
ansible all -m command -a "uptime"
```

Ansible is useful for repeatable RHEL configuration and enterprise automation.

---
