# 📦 Linux Archiving & Resource Monitoring Cheat Sheet

## Topics Covered

* top
* zip
* unzip
* tar

---

# 1. top Command

## What is top?

`top` is a real-time Linux system monitoring tool used to view:

* CPU utilization
* Memory usage
* Running processes
* Load average
* Process IDs (PID)
* User information

It is one of the first commands Linux Administrators and DevOps Engineers use during troubleshooting.

---

## Basic Syntax

```bash
top
```

### Sample Output

```text
top - 11:45:21 up 12 days, 4:23, 2 users

Tasks: 231 total, 1 running, 230 sleeping

%Cpu(s): 18.5 us, 4.2 sy, 0.0 ni, 75.8 id

MiB Mem : 7980 total, 3520 free, 2180 used

PID   USER   %CPU  %MEM  COMMAND
2456  nginx  45.0   2.1  nginx
1289  mysql  22.5  18.4  mysqld
```

---

## Useful Keys Inside top

| Key | Description       |
| --- | ----------------- |
| P   | Sort by CPU       |
| M   | Sort by Memory    |
| k   | Kill Process      |
| r   | Renice Process    |
| c   | Show Full Command |
| q   | Quit              |

---

## Real-Time Project Scenario

### Production Application Slow

Users complain:

```text
Website loading very slowly.
```

Investigation:

```bash
top
```

Output shows:

```text
java process consuming 95% CPU
```

Action:

```bash
kill -9 <PID>
```

or restart service:

```bash
systemctl restart app-service
```

Problem resolved.

---

# 2. zip Command

## What is zip?

Used to compress files and directories.

### Benefits

* Reduce storage usage
* Faster file transfer
* Create backups

---

## Create Zip File

```bash
zip backup.zip file1.txt
```

### Output

```text
adding: file1.txt (deflated 65%)
```

---

## Zip Multiple Files

```bash
zip logs.zip app.log access.log error.log
```

---

## Zip Entire Directory

```bash
zip -r website.zip website/
```

### Output

```text
adding: website/index.html
adding: website/css/style.css
adding: website/js/app.js
```

---

## Real-Time Project Scenario

### Share Logs With Vendor

Application team requests logs.

Compress logs:

```bash
zip -r prod_logs.zip /var/log/application/
```

Transfer:

```bash
scp prod_logs.zip support@vendor.com:/tmp/
```

This is much faster than transferring thousands of files individually.

---

# 3. unzip Command

## What is unzip?

Used to extract ZIP archives.

---

## Extract Zip File

```bash
unzip backup.zip
```

### Output

```text
inflating: file1.txt
```

---

## Extract to Specific Directory

```bash
unzip backup.zip -d /tmp/restore
```

---

## List Contents Without Extracting

```bash
unzip -l backup.zip
```

### Output

```text
Length   Name
------   ----
1024     file1.txt
2048     file2.txt
```

---

## Real-Time Project Scenario

Developer sends:

```text
release-v2.zip
```

Deploy:

```bash
unzip release-v2.zip -d /opt/app/
```

Verify files before deployment.

---

# 4. tar Command

## What is tar?

`tar` stands for:

```text
Tape Archive
```

Used to:

* Archive files
* Create backups
* Package directories

Widely used in Linux environments.

---

## Create Tar Archive

```bash
tar -cvf backup.tar project/
```

### Options

```text
c = create
v = verbose
f = file
```

### Output

```text
project/
project/app.py
project/config.yaml
```

---

## Extract Tar Archive

```bash
tar -xvf backup.tar
```

### Options

```text
x = extract
v = verbose
f = file
```

---

## Create Compressed tar.gz

```bash
tar -czvf backup.tar.gz project/
```

### Options

```text
z = gzip compression
```

### Output

```text
project/
project/app.py
project/config.yaml
```

---

## Extract tar.gz

```bash
tar -xzvf backup.tar.gz
```

---

## View Contents of Tar File

```bash
tar -tvf backup.tar
```

### Output

```text
-rw-r--r-- app.py
-rw-r--r-- config.yaml
```

---

## Real-Time Project Scenario

### Kubernetes Backup Before Upgrade

Create backup:

```bash
tar -czvf k8s-manifests.tar.gz manifests/
```

Upload to storage:

```bash
aws s3 cp k8s-manifests.tar.gz s3://backup-bucket/
```

Restore if required:

```bash
tar -xzvf k8s-manifests.tar.gz
```

---

# 🔥 Difference Between zip and tar

| Feature              | zip       | tar                         |
| -------------------- | --------- | --------------------------- |
| Compression          | Yes       | No (unless gzip/bzip2 used) |
| Windows Support      | Excellent | Limited                     |
| Linux Usage          | Common    | Very Common                 |
| Preserve Permissions | Partial   | Yes                         |
| Production Backups   | Less Used | Preferred                   |

---

# 🎯 Interview Questions & Answers

## 1. What does top command do?

Displays real-time system resource usage and running processes.

---

## 2. Which key sorts processes by CPU in top?

```text
P
```

---

## 3. Which key sorts processes by Memory?

```text
M
```

---

## 4. How do you kill a process from top?

Press:

```text
k
```

Then enter the PID.

---

## 5. How do you create a zip archive?

```bash
zip files.zip file1 file2
```

---

## 6. How do you zip a directory?

```bash
zip -r backup.zip directory/
```

---

## 7. How do you extract a zip file?

```bash
unzip backup.zip
```

---

## 8. How do you list zip contents without extracting?

```bash
unzip -l backup.zip
```

---

## 9. What does tar stand for?

```text
Tape Archive
```

---

## 10. How do you create a tar archive?

```bash
tar -cvf backup.tar directory/
```

---

## 11. How do you extract a tar archive?

```bash
tar -xvf backup.tar
```

---

## 12. How do you create a compressed tar.gz archive?

```bash
tar -czvf backup.tar.gz directory/
```

---

## 13. How do you extract a tar.gz archive?

```bash
tar -xzvf backup.tar.gz
```

---

## 14. How do you view the contents of a tar file?

```bash
tar -tvf backup.tar
```

---

## 15. Which format is preferred for Linux server backups?

```text
tar.gz
```

Because it preserves permissions, ownership, and directory structure efficiently.

---

# 💡 Key Takeaway

✅ Use `top` to troubleshoot CPU, Memory, and Process issues.

✅ Use `zip` and `unzip` when sharing files across teams and platforms.

✅ Use `tar` and `tar.gz` for Linux backups, deployments, and production server maintenance.

✅ Every DevOps Engineer, Linux Administrator, SRE, and Cloud Engineer uses these commands regularly in real-world environments.
