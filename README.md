# 🐧 Linux Mastery Series

A practical Linux learning series designed for DevOps Engineers, Cloud Engineers, SREs, and System Administrators.

This repository contains structured Linux notes, commands, interview questions, real-world examples, and hands-on practice content.

---

# 📚 Learning Roadmap

## ✅ Day 1 — Linux Fundamentals

### Topics Covered

* What is Linux?
* History of Linux
* Open Source Concept
* Linux Features
* Linux Distributions

  * RHEL
  * Ubuntu
  * CentOS
  * Debian
  * SUSE
* Linux File System Structure
* Important Directories

  * /
  * /bin
  * /sbin
  * /etc
  * /home
  * /root
  * /dev
  * /proc
  * /tmp
  * /opt

### Interview Questions

* Difference between `/bin` and `/sbin`
* Purpose of `/opt`
* What is Linux Distribution?
* Difference between Root Directory and Root User

### Skills Gained

✔ Linux Architecture Understanding

✔ File System Navigation Basics

✔ Linux Distribution Knowledge

---

## ✅ Day 2 — Essential Linux Commands

### Topics Covered

#### Basic Navigation Commands

```bash
pwd
cd
mkdir
rmdir
rm
touch
```

#### User & System Commands

```bash
whoami
who
uname
sudo su -
```

#### Utility Commands

```bash
clear
history
man
```

### Interview Questions

* Difference between `sudo su` and `sudo su -`
* How to clear command history?
* Difference between command and program?

### Skills Gained

✔ Terminal Navigation

✔ User Management Basics

✔ Command History Management

✔ Linux Documentation Usage

---

## ✅ Day 3 — File Management & Linux Permissions

### File Operations

```bash
ls
cat
tac
cp
mv
head
tail
sort
grep
wc
```

### User & Group Commands

```bash
id
groups
```

### Linux Permissions

#### UMASK

```bash
umask
umask 022
```

#### CHMOD

```bash
chmod 777 file
chmod 644 file
chmod u+x file
```

#### CHOWN

```bash
chown user file
chown -R user directory
```

#### CHGRP

```bash
chgrp group file
```

### Utility Commands

```bash
file
diff
echo
```

### Interview Questions

* How UMASK works?
* Difference between 777 and ugo+rwx?
* Difference between chmod 400 and chmod ugo+r?
* Why user cannot open file even with write permission?
* Difference between `/root` and `/`?

### Skills Gained

✔ File Management

✔ Permission Management

✔ Ownership Management

✔ User & Group Administration

✔ Linux Security Fundamentals

---

## 🚧 ## ✅ Day 4 — Process Management & Monitoring

### Topics Covered

#### Process Management

```bash
ps
top
htop
jobs
bg
fg
kill
killall
pkill
nohup
nice
renice
```

#### System Monitoring

```bash
uptime
free
vmstat
iostat
sar
```

### Concepts Learned

* Process vs Program
* PID & PPID
* Foreground & Background Processes
* Process Priorities
* Zombie Process
* Orphan Process
* System Resource Monitoring

### Interview Questions

* Difference between Process and Program?
* What is PID and PPID?
* Difference between kill, killall and pkill?
* What is Zombie Process?
* What is Orphan Process?
* How to identify high CPU or memory consuming processes?

### Skills Gained

✔ Process Management

✔ Process Troubleshooting

✔ Resource Monitoring

✔ Linux Performance Analysis

✔ Production Server Monitoring

# 🛠️ Prerequisites

* Basic Computer Knowledge
* Linux VM / EC2 Instance / WSL
* Curiosity to Learn Linux

---

# ⭐ Repository Goals

* Learn Linux from Basics to Advanced
* Understand Real-Time Production Concepts
* Prepare for DevOps Interviews
* Build Strong Linux Administration Skills

---

### Happy Learning Linux 🐧🚀
