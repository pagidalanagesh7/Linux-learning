
# 🚀 Linux Series – Day 12: SSH & Firewall Basics

> **Secure Remote Access & Linux Firewall Management**

## 📌 Topics Covered

### 🔐 SSH (Secure Shell)

- ssh
- ssh-keygen
- ssh-copy-id
- ~/.ssh/config

---

### 📂 Secure File Transfer

- scp
- sftp

---

### 🔥 Firewall Basics

- UFW (Uncomplicated Firewall)
- iptables

---

# 📖 Introduction

In production environments, Linux servers are typically managed remotely using **SSH (Secure Shell)** instead of a graphical interface. SSH provides encrypted communication, enabling administrators to securely deploy applications, troubleshoot systems, and automate infrastructure tasks.

Equally important is securing those servers using **Linux firewalls**, which control inbound and outbound network traffic to prevent unauthorized access.

By the end of this guide, you'll know how to:

- Securely access remote Linux servers
- Configure passwordless SSH authentication
- Transfer files securely between systems
- Manage firewall rules
- Open and close application ports
- Troubleshoot SSH and firewall-related issues

---

# 1️⃣ ssh

## Purpose

Securely connects to a remote Linux server.

### Syntax

```bash
ssh username@server-ip

### Example

```bash
ssh ubuntu@192.168.1.100
```

### Common Options

```bash
ssh -p 2222 user@host
ssh -i ~/.ssh/id_rsa user@host
ssh -v user@host
```

### Real-Time Use Cases

* Login to AWS EC2 instances
* Manage Kubernetes worker nodes
* Access production Linux servers
* Remote troubleshooting

---

# 2️⃣ ssh-keygen

## Purpose

Generates SSH public and private key pairs for secure passwordless authentication.

### Command

```bash
ssh-keygen
```

### Output

```text
Generating public/private rsa key pair...
id_rsa
id_rsa.pub
```

### Real-Time Use Cases

* Passwordless SSH login
* GitHub authentication
* GitLab authentication
* CI/CD automation

---

# 3️⃣ ssh-copy-id

## Purpose

Copies your SSH public key to a remote Linux server.

### Command

```bash
ssh-copy-id user@server
```

### Real-Time Use Cases

* Passwordless authentication
* Jenkins deployments
* Automation scripts
* Secure server access

---

# 4️⃣ ~/.ssh/config

## Purpose

Simplifies SSH connections using host aliases.

### Example

```text
Host prod-server
    HostName 192.168.1.100
    User ubuntu
    IdentityFile ~/.ssh/id_rsa
```

### Connect Using

```bash
ssh prod-server
```

### Real-Time Use Cases

* Manage multiple servers easily
* Avoid typing long SSH commands
* Improve productivity

---

# 5️⃣ scp

## Purpose

Securely copies files between systems using SSH.

### Copy Local File

```bash
scp app.tar.gz user@server:/tmp/
```

### Copy From Remote

```bash
scp user@server:/var/log/app.log .
```

### Copy Directory

```bash
scp -r project user@server:/opt/
```

### Real-Time Use Cases

* Deploy applications
* Transfer configuration files
* Backup logs
* Copy deployment artifacts

---

# 6️⃣ sftp

## Purpose

Interactive secure file transfer over SSH.

### Connect

```bash
sftp user@server
```

### Useful Commands

```bash
ls
pwd
put file.txt
get backup.tar
exit
```

### Real-Time Use Cases

* Upload configuration files
* Download logs
* Exchange deployment packages
* Secure file management

---

# 7️⃣ UFW (Uncomplicated Firewall)

## Purpose

Simple firewall management tool available on Ubuntu.

### Check Status

```bash
sudo ufw status
```

### Enable Firewall

```bash
sudo ufw enable
```

### Allow SSH

```bash
sudo ufw allow ssh
```

### Allow Port 8080

```bash
sudo ufw allow 8080
```

### Delete Rule

```bash
sudo ufw delete allow 8080
```

### Real-Time Use Cases

* Secure production servers
* Restrict unauthorized access
* Allow application ports
* Protect cloud instances

---

# 8️⃣ iptables

## Purpose

Linux kernel firewall framework used for advanced packet filtering and network traffic management.

### View Rules

```bash
sudo iptables -L
```

### Allow SSH

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### Allow HTTP

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

### Drop All Incoming Traffic

```bash
sudo iptables -A INPUT -j DROP
```

### Real-Time Use Cases

* Kubernetes worker node security
* Production firewall policies
* Packet filtering
* Server hardening

---

# 🔥 Real-Time Production Scenarios

## Scenario 1: Unable to SSH into an EC2 Instance

```text
ping server-ip
        │
        ▼
ssh -v user@server
        │
        ▼
sudo ufw status
        │
        ▼
sudo iptables -L
        │
        ▼
ss -tulnp | grep 22
        │
        ▼
Identify and Fix the Issue
```

---

## Scenario 2: Application Running on Port 8080 is Not Accessible

```text
ss -tulnp
      │
      ▼
sudo ufw status
      │
      ▼
sudo ufw allow 8080
      │
      ▼
curl http://server:8080
      │
      ▼
Application Becomes Reachable
```

---

## Scenario 3: Configure Passwordless SSH Login

```text
ssh-keygen
      │
      ▼
ssh-copy-id user@server
      │
      ▼
ssh server
      │
      ▼
Automation Ready
```

---

# ⭐ Top 20 Interview Questions & Answers

## 1. What is SSH?

**Answer:** SSH (Secure Shell) is a secure protocol used to remotely access Linux systems over an encrypted connection.

---

## 2. Which port does SSH use by default?

**Answer:** Port **22**.

---

## 3. What command is used to connect to a remote server?

```bash
ssh user@server-ip
```

---

## 4. What is ssh-keygen used for?

**Answer:** It generates SSH public and private key pairs for secure authentication.

---

## 5. What is ssh-copy-id?

**Answer:** It copies your public key to a remote server, enabling passwordless login.

---

## 6. Why use SSH keys instead of passwords?

**Answer:** SSH keys are more secure and support automated authentication.

---

## 7. What is SCP?

**Answer:** Secure Copy Protocol used to transfer files over SSH.

---

## 8. How do you copy a directory using SCP?

```bash
scp -r folder user@server:/path
```

---

## 9. What is SFTP?

**Answer:** Secure File Transfer Protocol for interactive file transfers.

---

## 10. Difference between SCP and SFTP?

**Answer:** SCP performs direct file transfers, whereas SFTP provides an interactive file management session.

---

## 11. What is UFW?

**Answer:** UFW is a user-friendly firewall management tool commonly used on Ubuntu.

---

## 12. How do you enable UFW?

```bash
sudo ufw enable
```

---

## 13. How do you allow SSH through UFW?

```bash
sudo ufw allow ssh
```

---

## 14. What is iptables?

**Answer:** A Linux firewall framework used to manage and filter network traffic.

---

## 15. How do you list firewall rules in iptables?

```bash
sudo iptables -L
```

---

## 16. How do you allow HTTP traffic using iptables?

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

---

## 17. Why is SSH considered secure?

**Answer:** It encrypts all communication between the client and server.

---

## 18. SSH connection is failing. What should you check?

* Server is reachable
* SSH service is running
* Port 22 is open
* Firewall rules
* SSH logs

---

## 19. Which command helps debug SSH issues?

```bash
ssh -v user@server
```

---

## 20. Why are firewall rules important?

**Answer:** Firewall rules restrict unauthorized access, protect services, and improve overall server security.

---

# 💡 Key Takeaway

SSH and Linux firewalls are fundamental to secure Linux administration. Mastering **ssh**, **ssh-keygen**, **ssh-copy-id**, **scp**, **sftp**, **UFW**, and **iptables** enables DevOps Engineers, Linux Administrators, Cloud Engineers, and SREs to:

* Securely access remote servers
* Configure passwordless authentication
* Transfer files safely
* Protect production systems
* Manage firewall rules
* Troubleshoot connectivity issues

---

## 🎯 What's Next?

**➡️ Linux Series – Day 13:** Shell Scripting Basics (Variables, Loops, Conditions, Functions & Automation)

---

⭐ If you found this guide helpful, consider giving the repository a **Star** and sharing it with others in the DevOps community!

```
```
