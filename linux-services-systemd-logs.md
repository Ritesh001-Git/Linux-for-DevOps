# Services, Daemons, systemd & Linux Logs

## Services and Daemons

A **daemon** is a background process that performs system tasks.

Linux uses **systemd** to manage startup and services.

systemd manages:

- Startup
- Services
- Daemons
- Dependencies
- Resource activation

---

## systemd Units

Important systemd unit types:

```text
.service
.socket
.path
```

### `.service`

Represents a service or process managed by systemd.

Example:

```text
sshd.service
```

### `.socket`

Represents an IPC or network socket that systemd can monitor.

A socket can activate a corresponding service when a connection or request arrives.

### `.path`

Monitors a file or directory for filesystem changes.

A `.path` unit can activate a corresponding service when a specified filesystem event occurs.

### List Units

List service units:

```bash
systemctl list-units --type=service
```

List socket units:

```bash
systemctl list-units --type=socket
```

List path units:

```bash
systemctl list-units --type=path
```

---

## systemctl Important Commands

`systemctl` is used to manage systemd services and units.

### Check Status

```bash
systemctl status ssh
```

Checks whether the service is running and shows recent service information.

### Start a Service

```bash
sudo systemctl start ssh
```

Starts the service immediately.

### Stop a Service

```bash
sudo systemctl stop ssh
```

Stops the service immediately.

### Restart a Service

```bash
sudo systemctl restart ssh
```

Restarts the service.

### Reload a Service

```bash
sudo systemctl reload ssh
```

Reloads the service configuration without fully restarting the service, when supported.

### Enable a Service at Boot

```bash
sudo systemctl enable ssh
```

Configures the service to start automatically during boot.

### Disable a Service at Boot

```bash
sudo systemctl disable ssh
```

Disables automatic startup during boot.

### Check Failed Services

```bash
systemctl --failed --type=service
```

Shows services that have failed.

### Important Difference

```text
start   → Start the service now
stop    → Stop the service now
restart → Restart the service now
reload  → Reload configuration
enable  → Start automatically at boot
disable → Do not start automatically at boot
```

---

## Linux Logs

Logs are important for:

- Troubleshooting
- Security
- Auditing
- Monitoring
- Debugging system problems

Traditional Linux log files are commonly stored under:

```text
/var/log
```

Linux systems using systemd also use:

```text
systemd-journald
```

to collect system and service event messages.

`rsyslog` may also be used to process syslog messages and store logs.

---

## systemd Journal

**systemd-journald** is the logging service associated with systemd.

It collects messages from sources such as:

- System services
- The kernel
- Applications
- Other system components

The main command used to view the systemd journal is:

```bash
journalctl
```

---

## journalctl Important Commands

### View All Journal Logs

```bash
journalctl
```

Displays available journal entries.

### Show Newest Entries

```bash
journalctl -e
```

Jumps to the end of the journal.

### Show Last 20 Entries

```bash
journalctl -n 20
```

Displays the last 20 journal entries.

### Follow Logs Live

```bash
journalctl -f
```

Continuously displays new log entries as they are created.

### View Logs for a Service

```bash
journalctl -u ssh
```

Shows journal entries for the SSH service.

If the system uses `sshd` as the service name:

```bash
journalctl -u sshd
```

### Show Last 20 Service Logs

```bash
journalctl -u ssh -n 20
```

### View Logs from the Current Boot

```bash
journalctl -b
```

Shows logs from the current system boot.

### View Kernel Logs

```bash
journalctl -k
```

Shows kernel-related journal messages.

### Show Error Messages

```bash
journalctl -p err
```

Filters journal messages by error priority.

### Show Warning Messages

```bash
journalctl -p warning
```

Shows warning-level and more severe messages.

### View Logs Since a Specific Time

```bash
journalctl --since "10:00"
```

### View Logs Between Two Times

```bash
journalctl --since "10:00" --until "11:00"
```

### View Logs for a Specific User ID

```bash
journalctl _UID=1000
```

---

## Persistent Journal

Journal data may be stored temporarily under:

```text
/run/log/journal
```

Logs stored there may not survive a reboot.

Persistent journal storage can be configured in:

```text
/etc/systemd/journald.conf
```

The `Storage` setting controls journal storage behavior.

Persistent logs are useful for investigating events that happened before a reboot or system failure.
