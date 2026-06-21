# 🚀 Linux Administration Cheat Sheet – Day 6

## Topics Covered

* whereis
* users
* date
* timedatectl
* df
* du
* hostname
* whatis
* systemctl
* service
* last
* ps
* kill

---

# 1️⃣ System Information Commands

## hostname

Display or configure system hostname.

```bash
hostname
hostnamectl set-hostname server01
```

Sample Output:

```text
server01
```

---

## date

Display current system date and time.

```bash
date
date "+%d-%m-%Y %H:%M:%S"
```

Sample Output:

```text
Sun Jun 21 15:30:45 IST 2026
21-06-2026 15:30:45
```

---

## timedatectl

Manage timezone and NTP synchronization.

```bash
timedatectl
timedatectl set-timezone Asia/Kolkata
```

Sample Output:

```text
Local time: Sun 2026-06-21 15:31:10 IST
Universal time: Sun 2026-06-21 10:01:10 UTC
RTC time: Sun 2026-06-21 10:01:10
Time zone: Asia/Kolkata (IST, +0530)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

---

# 2️⃣ User Monitoring Commands

## users

Display currently logged-in users.

```bash
users
```

Sample Output:

```text
root devops admin
```

---

## last

Display login and reboot history.

```bash
last
last reboot
```

Sample Output:

```text
devops pts/0 192.168.1.10 Sun Jun 21 09:00 still logged in
reboot system boot Sun Jun 21 08:55
```

---

# 3️⃣ Storage Monitoring Commands

## df

Check filesystem disk space usage.

```bash
df -h
df -Th
```

Sample Output:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   22G   26G  46% /
tmpfs           3.8G     0  3.8G   0% /dev/shm
```

---

## du

Check directory and file disk usage.

```bash
du -sh *
du -sh /var/log
```

Sample Output:

```text
4.0K  file1.txt
120M  logs
1.2G  /var/log
```

---

# 4️⃣ Documentation Lookup Commands

## whereis

Locate binary, source, and man pages.

```bash
whereis kubectl
whereis nginx
```

Sample Output:

```text
kubectl: /usr/bin/kubectl /usr/share/man/man1/kubectl.1.gz
nginx: /usr/sbin/nginx /usr/share/nginx
```

---

## whatis

Display short command descriptions.

```bash
whatis ls
whatis kubectl
```

Sample Output:

```text
ls (1) - list directory contents
kubectl (1) - Kubernetes command-line tool
```

---

# 5️⃣ Service Management Commands

## systemctl

Manage systemd services.

```bash
systemctl status nginx
systemctl restart nginx
systemctl start nginx
systemctl stop nginx
systemctl enable nginx
systemctl disable nginx
```

Sample Output:

```text
● nginx.service - NGINX Web Server
   Loaded: loaded
   Active: active (running)
```

---

## service

Legacy service management utility.

```bash
service nginx status
service nginx restart
```

Sample Output:

```text
nginx is running
```

---

# 6️⃣ Process Management Commands

## ps

Display running processes.

```bash
ps -ef
ps aux
```

Sample Output:

```text
UID   PID  PPID CMD
root    1     0 /sbin/init
root  876     1 nginx: master process
nginx 877   876 nginx: worker process
```

---

## kill

Terminate processes.

```bash
kill 876
kill -9 876
```

Sample Output:

```text
Process terminated successfully
Killed
```

---

# 7️⃣ Real-World DevOps Use Cases

| Command     | Use Case                      |
| ----------- | ----------------------------- |
| hostname    | Server Identification         |
| timedatectl | Timezone Standardization      |
| df          | Disk Capacity Monitoring      |
| du          | Log Directory Analysis        |
| users       | User Activity Auditing        |
| last        | Security Investigation        |
| systemctl   | Production Service Management |
| ps          | Application Troubleshooting   |
| kill        | Hung Process Recovery         |
| whereis     | Binary Location Verification  |
| whatis      | Quick Command Reference       |

---

# 8️⃣ Comparison Tables

## df vs du

| Feature | df                  | du                  |
| ------- | ------------------- | ------------------- |
| Shows   | Filesystem Usage    | Directory Usage     |
| Scope   | Entire Filesystem   | Files & Directories |
| Purpose | Capacity Monitoring | Space Analysis      |

---

## systemctl vs service

| Feature           | systemctl | service  |
| ----------------- | --------- | -------- |
| Init System       | systemd   | SysVinit |
| Modern Linux      | Yes       | Legacy   |
| Advanced Features | Yes       | Limited  |

---

## ps vs kill

| Feature             | ps  | kill |
| ------------------- | --- | ---- |
| Monitor Processes   | Yes | No   |
| Terminate Processes | No  | Yes  |
| Troubleshooting     | Yes | Yes  |

---

# 9️⃣ Troubleshooting Scenarios

## Disk Full

```bash
df -h
du -sh /*
```

## Service Not Starting

```bash
systemctl status nginx
journalctl -xe
```

## High CPU Usage

```bash
ps aux --sort=-%cpu
```

---

# 🔟 Security Best Practices

* Monitor login activity using `last`
* Verify active users using `users`
* Avoid unnecessary use of `kill -9`
* Audit service status periodically
* Maintain NTP synchronization
* Monitor disk usage regularly

---

# 1️⃣1️⃣ Quick Revision Notes

📌 hostname → System Identity

📌 date → Current Date & Time

📌 timedatectl → Time Management

📌 df → Filesystem Usage

📌 du → Directory Usage

📌 whereis → Command Location

📌 whatis → Command Description

📌 users → Active Users

📌 last → Login History

📌 ps → Running Processes

📌 kill → Process Control

📌 systemctl → Service Management

---

# 1️⃣2️⃣ Interview Questions & Answers

### Q1. Difference between df and du?

df shows filesystem usage while du shows directory/file usage.

### Q2. Difference between systemctl and service?

systemctl manages systemd services while service is a legacy SysVinit utility.

### Q3. How do you check active users?

```bash
users
```

### Q4. How do you view login history?

```bash
last
```

### Q5. How do you find process PID?

```bash
ps -ef
```

### Q6. Difference between kill and kill -9?

* kill → SIGTERM (Graceful)
* kill -9 → SIGKILL (Forceful)

### Q7. How do you restart a service?

```bash
systemctl restart nginx
```

### Q8. How do you check disk space?

```bash
df -h
```

### Q9. How do you check directory size?

```bash
du -sh directory_name
```

### Q10. What does timedatectl do?

Manages system time, timezone, RTC, and NTP synchronization.

---

# 🎯 Key Takeaways

✅ System Information Management

✅ Date & Time Administration

✅ Storage Monitoring & Analysis

✅ User Activity Monitoring

✅ Linux Documentation Lookup

✅ Service Administration

✅ Process Monitoring

✅ Process Troubleshooting

✅ Production Server Operations

✅ Essential Linux Administration Skills

---

### Target Audience

* Linux Administrators
* DevOps Engineers
* SREs
* Cloud Engineers
* Platform Engineers
* System Administrators
