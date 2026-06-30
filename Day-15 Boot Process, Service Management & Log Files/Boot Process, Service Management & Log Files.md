# 🚀 Linux Day 15 – Boot Process, Service Management & Log Files

## 📖 Overview

Understanding how Linux boots, how services are managed, and where logs are stored is essential for every Linux Administrator, DevOps Engineer, Cloud Engineer, and SRE.

These concepts help troubleshoot server failures, manage applications, monitor system health, and maintain production environments efficiently.

---

# 1️⃣ Linux Boot Process

## Boot Sequence

```text
Power ON
    │
    ▼
BIOS / UEFI
    │
    ▼
Boot Loader (GRUB)
    │
    ▼
Linux Kernel
    │
    ▼
initramfs
    │
    ▼
systemd (PID 1)
    │
    ▼
System Services
    │
    ▼
Login Prompt / GUI
```

## Boot Process Explanation

### 1. BIOS / UEFI

- Performs hardware initialization (POST)
- Detects CPU, RAM, Storage
- Loads Boot Loader

---

### 2. Boot Loader (GRUB)

Loads Linux Kernel into memory.

Example:

```bash
grub2-install
grub2-mkconfig
```

GRUB Configuration:

```text
/etc/default/grub
```

---

### 3. Linux Kernel

Responsible for:

- Memory Management
- Process Management
- Device Drivers
- Filesystem Mounting
- Networking

Verify Kernel Version

```bash
uname -r
```

---

### 4. initramfs

Temporary root filesystem.

Used to:

- Load required drivers
- Detect disks
- Mount actual root filesystem

---

### 5. systemd (PID 1)

First userspace process.

Check PID 1

```bash
ps -p 1
```

Output

```text
systemd
```

Responsible for:

- Starting Services
- Mounting Filesystems
- Managing Targets
- System Initialization

---

### 6. Login Prompt

System becomes available for users.

---

## Check Boot Time

```bash
systemd-analyze
```

Detailed Boot

```bash
systemd-analyze blame
```

---

# 2️⃣ Service Management (systemctl)

systemd manages background services (daemons).

## Check Service Status

```bash
systemctl status nginx
```

---

## Start Service

```bash
sudo systemctl start nginx
```

---

## Stop Service

```bash
sudo systemctl stop nginx
```

---

## Restart Service

```bash
sudo systemctl restart nginx
```

---

## Reload Configuration

```bash
sudo systemctl reload nginx
```

---

## Enable Service at Boot

```bash
sudo systemctl enable nginx
```

---

## Disable Service

```bash
sudo systemctl disable nginx
```

---

## Check Running Services

```bash
systemctl list-units --type=service
```

---

## Check Failed Services

```bash
systemctl --failed
```

---

## Important systemctl Commands

| Command | Description |
|----------|-------------|
| systemctl start | Start service |
| systemctl stop | Stop service |
| systemctl restart | Restart service |
| systemctl reload | Reload configuration |
| systemctl status | View service status |
| systemctl enable | Auto-start at boot |
| systemctl disable | Disable auto-start |
| systemctl is-active | Check running state |
| systemctl is-enabled | Check boot status |

---

# 3️⃣ Linux Log Files

Linux stores logs inside:

```text
/var/log/
```

These logs are extremely useful for troubleshooting.

---

## Important Log Files

### System Log

```text
/var/log/messages
```

(RHEL/CentOS)

Contains:

- Kernel messages
- System events
- Services

---

### Syslog

```text
/var/log/syslog
```

(Ubuntu/Debian)

Contains:

- General system logs
- Service logs

---

### Authentication Log

Ubuntu

```text
/var/log/auth.log
```

RHEL

```text
/var/log/secure
```

Contains:

- SSH login
- sudo activity
- Authentication failures

---

### Boot Log

```text
/var/log/boot.log
```

Shows boot process messages.

---

### Kernel Log

```text
dmesg
```

or

```bash
dmesg | less
```

Useful for:

- Hardware detection
- Driver issues
- Boot errors

---

## View Live Logs

```bash
tail -f /var/log/messages
```

Ubuntu

```bash
tail -f /var/log/syslog
```

---

## Journal Logs (systemd)

View all logs

```bash
journalctl
```

Current boot

```bash
journalctl -b
```

Specific Service

```bash
journalctl -u nginx
```

Recent logs

```bash
journalctl -n 50
```

Live logs

```bash
journalctl -f
```

---

# Common Troubleshooting Workflow

Check service

```bash
systemctl status nginx
```

↓

Read logs

```bash
journalctl -u nginx
```

↓

Restart service

```bash
sudo systemctl restart nginx
```

↓

Verify status

```bash
systemctl status nginx
```

---

# Interview Questions

### Q1. What is the Linux boot process?

**Answer:** BIOS/UEFI → GRUB → Kernel → initramfs → systemd → Services → Login.

---

### Q2. What is systemd?

**Answer:** The init system responsible for booting Linux and managing services. It runs as PID 1.

---

### Q3. How do you restart a service?

```bash
sudo systemctl restart <service-name>
```

---

### Q4. How do you check service status?

```bash
systemctl status <service-name>
```

---

### Q5. Where are Linux log files stored?

```text
/var/log/
```

---

### Q6. Which command displays systemd logs?

```bash
journalctl
```

---

### Q7. Which command shows boot performance?

```bash
systemd-analyze
```

---

### Q8. How do you enable a service during boot?

```bash
sudo systemctl enable <service-name>
```

---

# Quick Revision

✅ Linux Boot Process

- BIOS / UEFI
- GRUB
- Kernel
- initramfs
- systemd
- Services
- Login

✅ Service Management

- start
- stop
- restart
- reload
- enable
- disable
- status

✅ Log Files

- /var/log/messages
- /var/log/syslog
- /var/log/auth.log
- /var/log/secure
- /var/log/boot.log
- journalctl
- dmesg

---

# DevOps Takeaway

A DevOps Engineer should be able to:

- Understand the Linux boot sequence.
- Manage services using `systemctl`.
- Diagnose issues using `/var/log`, `journalctl`, and `dmesg`.
- Restart failed services and analyze logs efficiently.
- Troubleshoot production server startup and service failures.