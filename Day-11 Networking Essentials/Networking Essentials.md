# 🚀 Linux Day 11 – Networking Essentials

> **Linux Networking Fundamentals & Troubleshooting** for Linux Administrators, DevOps Engineers, Cloud Engineers, and SREs.

---

# 📌 Topics Covered

## 1. Network Configuration

* `ifconfig`
* `ip`
* `nmcli`

## 2. Hostname & DNS Resolution

* `hostname`
* `/etc/hosts`
* `nslookup`
* `dig`
* `host`

## 3. Network Utilities

* `ping`
* `traceroute`
* `curl`
* `wget`
* `netstat`
* `ss`

---

# 📖 Introduction

Linux networking is one of the most important skills in production environments.

Whenever an application cannot connect to another server, Kubernetes Pods fail, APIs become unreachable, websites stop responding, or databases cannot be accessed, Linux networking tools become the first line of troubleshooting.

A DevOps Engineer should know how to:

* Configure network interfaces
* Verify IP addresses
* Troubleshoot DNS
* Test connectivity
* Verify listening ports
* Download files
* Debug HTTP APIs

---

# 1️⃣ ifconfig

## Purpose

Displays or configures network interfaces.

> **Note:** `ifconfig` is a legacy networking utility and has been replaced by `ip` on most modern Linux distributions.

### Command

```bash
ifconfig
```

### Sample Output

```text
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>
inet 192.168.1.25
netmask 255.255.255.0
```

### Real-Time Use

* Check server IP after VM creation
* Verify network interface status

---

# 2️⃣ ip

Modern replacement for `ifconfig`.

### Command

```bash
ip addr
```

### Sample Output

```text
2: eth0:
inet 192.168.1.25/24
```

### Useful Commands

```bash
ip addr
ip link
ip route
ip neigh
```

### Real-Time Use

* Verify Pod/Node IP
* Check routing table
* Troubleshoot gateways
* View network interfaces

---

# 3️⃣ nmcli

NetworkManager command-line utility.

### Command

```bash
nmcli device status
```

### Sample Output

```text
DEVICE  TYPE      STATE      CONNECTION
eth0    ethernet  connected  Wired
```

### Restart Network

```bash
nmcli connection down eth0
nmcli connection up eth0
```

### Real-Time Use

* Configure static IP
* Restart network
* Manage network interfaces

---

# 4️⃣ hostname

Displays the system hostname.

### Command

```bash
hostname
```

### Sample Output

```text
prod-web-01
```

### Change Hostname

```bash
hostnamectl set-hostname prod-web-01
```

### Real-Time Use

* Rename production servers
* Verify server identity

---

# 5️⃣ /etc/hosts

Local hostname resolution file.

### Example

```text
192.168.1.20 db-server
192.168.1.30 app-server
```

### Real-Time Use

* Temporary DNS override
* Internal testing
* Local hostname mapping

---

# 6️⃣ nslookup

Queries a DNS server.

### Command

```bash
nslookup google.com
```

### Sample Output

```text
Name: google.com
Address: 142.250.193.14
```

### Real-Time Use

* Verify DNS resolution
* Troubleshoot DNS issues

---

# 7️⃣ dig

Detailed DNS lookup utility.

### Command

```bash
dig google.com
```

### Short Output

```bash
dig google.com +short
```

### Sample Output

```text
142.250.193.14
```

### Real-Time Use

* DNS troubleshooting
* Verify DNS records
* Check authoritative DNS servers

---

# 8️⃣ host

Simple DNS lookup command.

### Command

```bash
host google.com
```

### Sample Output

```text
google.com has address 142.250.193.14
```

### Real-Time Use

* Quick hostname resolution
* Verify DNS mappings

---

# 9️⃣ ping

Tests network connectivity.

### Command

```bash
ping google.com
```

### Sample Output

```text
64 bytes from google.com
icmp_seq=1 ttl=115 time=22 ms
```

### Real-Time Use

* Verify server reachability
* Measure network latency

---

# 🔟 traceroute

Shows the path packets take to reach the destination.

### Command

```bash
traceroute google.com
```

### Sample Output

```text
1  Router
2  ISP
3  Google
```

### Real-Time Use

* Troubleshoot network latency
* Identify routing issues

---

# 1️⃣1️⃣ curl

Transfers HTTP requests.

### Basic Request

```bash
curl https://example.com
```

### View HTTP Headers

```bash
curl -I https://example.com
```

### POST Request

```bash
curl -X POST https://example.com/api
```

### Real-Time Use

* API testing
* Health checks
* Download API responses

---

# 1️⃣2️⃣ wget

Downloads files from the internet.

### Command

```bash
wget https://example.com/file.zip
```

### Sample Output

```text
Saving to: file.zip
```

### Real-Time Use

* Download installers
* Fetch Helm charts
* Retrieve scripts and packages

---

# 1️⃣3️⃣ netstat

Displays network connections and listening ports.

### Command

```bash
netstat -tulnp
```

### Sample Output

```text
tcp        0      0 0.0.0.0:80    LISTEN    nginx
```

### Real-Time Use

* Find listening services
* Verify open ports

---

# 1️⃣4️⃣ ss

Modern replacement for `netstat`.

### Command

```bash
ss -tulnp
```

### Sample Output

```text
LISTEN 0 128 *:22 users:(("sshd"))
```

### Real-Time Use

* Verify application ports
* Inspect active socket connections

---

# 🔥 Real-Time Production Scenarios

## Scenario 1 – Application Cannot Reach Database

```text
ping db-server
      ↓
nslookup db-server
      ↓
ip route
      ↓
ss -tulnp
      ↓
curl http://db-server:8080/health
      ↓
Identify the root cause
```

---

## Scenario 2 – Website Down

```text
ping
      ↓
traceroute
      ↓
curl
      ↓
ss
      ↓
systemctl status nginx
```

---

## Scenario 3 – Jenkins Agent Not Connecting

```text
hostname
      ↓
cat /etc/hosts
      ↓
ping jenkins-server
      ↓
curl http://jenkins-server:8080
      ↓
ss -tulnp
```

---

# ⭐ Top 20 Interview Questions & Answers

### 1. Difference between `ifconfig` and `ip`?

**Answer:** `ifconfig` is a legacy tool, while `ip` is the modern replacement from the iproute2 package and provides advanced networking features.

---

### 2. Which command replaces `ifconfig`?

**Answer:** `ip`

---

### 3. How do you check your server IP?

```bash
ip addr
```

---

### 4. How do you display the routing table?

```bash
ip route
```

---

### 5. What is `nmcli` used for?

**Answer:** It manages NetworkManager connections, interfaces, and network configuration from the command line.

---

### 6. What is the purpose of `/etc/hosts`?

**Answer:** It maps hostnames to IP addresses locally before querying a DNS server.

---

### 7. What is DNS?

**Answer:** DNS (Domain Name System) translates domain names into IP addresses.

---

### 8. Difference between `nslookup`, `dig`, and `host`?

**Answer:**

* **nslookup** – Basic DNS queries
* **dig** – Detailed DNS troubleshooting
* **host** – Quick hostname lookup

---

### 9. What does `ping` test?

**Answer:** Network reachability and round-trip latency using ICMP.

---

### 10. Can `ping` fail while the server is still running?

**Answer:** Yes. Firewalls or security groups may block ICMP traffic.

---

### 11. What is `traceroute` used for?

**Answer:** It identifies the network path and detects where packets are delayed or dropped.

---

### 12. Difference between `curl` and `wget`?

**Answer:**

* **curl** – HTTP/API requests
* **wget** – File downloads with resume support

---

### 13. How do you check only HTTP response headers?

```bash
curl -I https://example.com
```

---

### 14. Which command is commonly used for REST API testing?

**Answer:** `curl`

---

### 15. What is `netstat` used for?

**Answer:** Displays network connections, listening ports, routing tables, and interface statistics.

---

### 16. Why is `ss` preferred over `netstat`?

**Answer:** It is faster, uses less memory, and is the modern replacement.

---

### 17. How do you check listening ports?

```bash
ss -tulnp
```

---

### 18. A website is not opening. What steps would you take?

1. `ping`
2. `nslookup` or `dig`
3. `traceroute`
4. `curl`
5. `ss -tulnp`
6. Check firewall, web server, and application logs

---

### 19. How do you verify whether a service is listening on port 8080?

```bash
ss -tulnp | grep 8080
```

---

### 20. In a production issue, DNS is suspected. Which commands would you use?

**Answer:** `nslookup`, `dig`, `host`, inspect `/etc/hosts`, and compare the resolved IP with the expected server IP.

---

# 💡 Key Takeaway

Linux networking commands are essential for diagnosing connectivity issues, validating DNS resolution, inspecting routes, verifying open ports, and testing web services.

Mastering **`ip`**, **`nmcli`**, **`ping`**, **`curl`**, **`ss`**, and DNS utilities enables Linux Administrators, DevOps Engineers, Cloud Engineers, and SREs to troubleshoot production networking incidents quickly and efficiently.
