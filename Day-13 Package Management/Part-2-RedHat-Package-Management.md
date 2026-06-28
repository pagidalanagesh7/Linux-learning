# 🐧 Red Hat Package Management

Red Hat-based Linux distributions use **RPM packages** and package managers such as **YUM** and **DNF** to install, update, remove, and manage software.

Popular Red Hat-based distributions include:

- Red Hat Enterprise Linux (RHEL)
- CentOS
- Rocky Linux
- AlmaLinux
- Fedora
- Oracle Linux

---

# 📦 RPM (Red Hat Package Manager)

RPM is the **low-level package manager** used in Red Hat-based systems.

It works directly with `.rpm` package files.

Example:

```
nginx-1.28.0.rpm
docker-ce.rpm
```

### Features

- Install local RPM packages
- Remove packages
- Verify installed packages
- Query package information
- List installed packages

> ⚠️ RPM **does NOT automatically resolve dependencies**.

---

## Install an RPM Package

```bash
sudo rpm -ivh package.rpm
```

### Options

| Option | Meaning |
|---------|----------|
| `-i` | Install |
| `-v` | Verbose Output |
| `-h` | Show Progress Bar |

Example

```bash
sudo rpm -ivh nginx.rpm
```

Sample Output

```
Preparing...

#################################

Installing...

Complete!
```

---

## Upgrade an RPM Package

```bash
sudo rpm -Uvh package.rpm
```

Example

```bash
sudo rpm -Uvh nginx.rpm
```

This upgrades the existing package.

---

## Remove a Package

```bash
sudo rpm -e nginx
```

Example Output

```
Removing package...
Complete!
```

---

## List Installed Packages

```bash
rpm -qa
```

Example Output

```
bash

curl

git

docker

nginx
```

---

## Package Information

```bash
rpm -qi nginx
```

Displays:

- Version
- Release
- Vendor
- Install Date
- Description

---

## List Files Installed by a Package

```bash
rpm -ql nginx
```

Example

```
/etc/nginx/

/usr/sbin/nginx

/usr/share/doc
```

---

## Find Which Package Owns a File

```bash
rpm -qf /usr/bin/bash
```

Output

```
bash-5.2.x86_64
```

---

# 🍴 YUM (Yellowdog Updater Modified)

YUM is a **high-level package manager** built on top of RPM.

It downloads packages from repositories and **automatically resolves dependencies**.

Used in:

- CentOS 7
- RHEL 7
- Older Enterprise Linux systems

---

## Features

- Repository management
- Automatic dependency resolution
- Install packages
- Remove packages
- Upgrade packages
- Search packages

---

## Install Package

```bash
sudo yum install httpd
```

Sample Output

```
Dependencies resolved.

Installing:

httpd
```

---

## Remove Package

```bash
sudo yum remove httpd
```

---

## Update Packages

```bash
sudo yum update
```

Updates all installed packages to the latest available version.

---

## Search Package

```bash
yum search nginx
```

---

## Package Information

```bash
yum info nginx
```

---

## List Installed Packages

```bash
yum list installed
```

---

# 🍴 DNF (Dandified YUM)

DNF is the **modern replacement for YUM**.

Introduced in:

- Fedora 22
- RHEL 8+
- Rocky Linux
- AlmaLinux

---

## Why DNF Replaced YUM?

DNF provides:

- Faster performance
- Better dependency resolution
- Lower memory usage
- Improved package conflict handling
- More reliable transactions

---

# DNF Features

- Automatic dependency resolution
- Better performance
- Faster metadata handling
- Rollback support
- Improved package management

---

## Install Package

```bash
sudo dnf install nginx
```

---

## Remove Package

```bash
sudo dnf remove nginx
```

---

## Upgrade Packages

```bash
sudo dnf upgrade
```

---

## Search Package

```bash
dnf search docker
```

---

## Package Information

```bash
dnf info docker
```

---

## List Installed Packages

```bash
dnf list installed
```

---

## Check Available Updates

```bash
dnf check-update
```

---

# 🆚 YUM vs DNF

| Feature | YUM | DNF |
|----------|-----|-----|
| High-Level Package Manager | ✅ | ✅ |
| Repository Support | ✅ | ✅ |
| Dependency Resolution | ✅ | ✅ |
| Faster Performance | ❌ | ✅ |
| Lower Memory Usage | ❌ | ✅ |
| Default in RHEL 8+ | ❌ | ✅ |
| Active Development | ❌ | ✅ |

---

# 📊 RPM vs YUM vs DNF

| Feature | RPM | YUM | DNF |
|----------|-----|-----|-----|
| Install Local RPM | ✅ | ✅ | ✅ |
| Repository Support | ❌ | ✅ | ✅ |
| Dependency Resolution | ❌ | ✅ | ✅ |
| Search Packages | ❌ | ✅ | ✅ |
| Update Packages | ❌ | ✅ | ✅ |
| High-Level Package Manager | ❌ | ✅ | ✅ |

---

# 🔄 Package Management Architecture

```
                 User
                   │
        ┌──────────┴──────────┐
        │                     │
      Debian              Red Hat
        │                     │
    ┌───┴────┐          ┌──────┴──────┐
    │        │          │             │
   APT      DPKG       DNF           RPM
    │                    │
    └────────────┬───────┘
                 │
          Package Repository
                 │
          Download Packages
                 │
      Resolve Dependencies
                 │
          Install Software
```

---

# 💼 Production Example 1

Install Nginx on Ubuntu

```bash
sudo apt update

sudo apt install nginx
```

---

# 💼 Production Example 2

Install Apache on Rocky Linux

```bash
sudo dnf install httpd
```

---

# 💼 Production Example 3

Install Local RPM

```bash
sudo rpm -ivh monitoring-agent.rpm
```

---

# 💼 Production Example 4

List Installed Packages

```bash
rpm -qa

dnf list installed
```

---

# 💡 Best Practices

✅ Always install packages from official repositories.

✅ Keep packages updated regularly.

✅ Verify package information before installation.

✅ Remove unused packages.

✅ Avoid downloading random RPM/DEB packages from unknown websites.

---

# ⚠️ Common Mistakes

❌ Using `rpm -ivh` for packages with dependencies (may fail).

❌ Forgetting to run `apt update` before installing new software.

❌ Installing software from untrusted repositories.

❌ Removing system packages without understanding their dependencies.

---

# 🎯 Interview Tips

- RPM is a **low-level package manager**.
- YUM and DNF are **high-level package managers**.
- DNF is the modern replacement for YUM.
- RPM **does not resolve dependencies** automatically.
- DNF provides faster dependency resolution and better performance than YUM.

---

## 📝 Quick Revision

| Command | Description |
|----------|-------------|
| `rpm -ivh package.rpm` | Install local RPM package |
| `rpm -Uvh package.rpm` | Upgrade RPM package |
| `rpm -e package` | Remove package |
| `rpm -qa` | List installed packages |
| `rpm -qi package` | Package information |
| `rpm -ql package` | List package files |
| `rpm -qf file` | Find package owning a file |
| `yum install package` | Install package |
| `yum update` | Update installed packages |
| `dnf install package` | Install package |
| `dnf upgrade` | Upgrade packages |
| `dnf check-update` | Check available updates |

---
