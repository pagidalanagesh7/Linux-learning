# 🔄 Updating & Upgrading Packages

Keeping packages updated is one of the most important tasks for every Linux Administrator, DevOps Engineer, and SRE. Regular updates improve security, fix bugs, and introduce new features.

---

# 📌 Update vs Upgrade

Many beginners confuse **Update** and **Upgrade**. They serve different purposes.

| Update | Upgrade |
|----------|----------|
| Refreshes package metadata | Installs newer versions of installed packages |
| Downloads latest package information | Downloads and installs package updates |
| Does not install software | Updates existing software |
| Safe to run anytime | May require service restart or reboot |

---

## 📦 What does `apt update` do?

The `apt update` command downloads the latest package information from configured repositories.

```bash
sudo apt update
```

Example Output

```
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease

Reading package lists... Done
```

### What happens internally?

```
Repository
      │
      ▼
Download Latest Package Metadata
      │
      ▼
Update Local Package Database
```

> **Important:** `apt update` **does not** install or upgrade any software.

---

## 📦 What does `apt upgrade` do?

After refreshing package metadata, run:

```bash
sudo apt upgrade
```

Example Output

```
Calculating upgrade...

The following packages will be upgraded:

openssl

curl

git
```

This installs the latest available versions of already installed packages.

---

## 📦 What is `apt full-upgrade`?

```bash
sudo apt full-upgrade
```

This command:

- Installs package updates
- Removes obsolete packages if required
- Handles complex dependency changes

Useful after major OS upgrades.

---

# 📦 Updating Packages in Red Hat

### Check Available Updates

```bash
sudo dnf check-update
```

or

```bash
sudo yum check-update
```

---

### Upgrade Packages

```bash
sudo dnf upgrade
```

or

```bash
sudo yum update
```

Example Output

```
Dependencies resolved.

Upgrading:

kernel

openssl

curl
```

---

# 🔄 Package Update Workflow

```
Repositories
       │
       ▼
Download Latest Metadata
       │
       ▼
Compare Installed Versions
       │
       ▼
Download Updated Packages
       │
       ▼
Install Updates
```

---

# 💼 Production Example

Updating an Ubuntu Server

```bash
sudo apt update

sudo apt upgrade
```

Updating a Rocky Linux Server

```bash
sudo dnf check-update

sudo dnf upgrade
```

---

# 🛡️ Why Regular Updates Are Important

Regular package updates provide:

- Security patches
- Bug fixes
- Performance improvements
- New features
- Compatibility updates

Example

```
OpenSSL Vulnerability

↓

Security Patch Released

↓

apt upgrade

↓

System Secured
```

---

# ⚠️ Best Practices

- Always run `apt update` before installing software.
- Review packages before upgrading.
- Take backups before major upgrades.
- Test updates in staging environments before production.

---

# ⚙️ Installing Software from Source (Compilation)

Sometimes software is not available in repositories or you need the latest version. In such cases, you can compile the software from source code.

---

# 📌 What is Source Code?

Source code is human-readable code written by developers.

Examples:

- C
- C++
- Java
- Go
- Python

Source code cannot run directly. It must be compiled into machine code.

---

# 🧠 Why Compile from Source?

Reasons include:

- Access the latest version
- Enable or disable specific features
- Performance optimization
- Software unavailable in repositories
- Learning and development purposes

---

# 📦 Common Source Package Formats

```
software.tar.gz

software.tar.xz

software.zip
```

---

# 🔄 Compilation Workflow

```
Download Source Code
        │
        ▼
Extract Archive
        │
        ▼
Configure Build
        │
        ▼
Compile Source Code
        │
        ▼
Install Software
```

---

# 📥 Step 1: Download Source Code

Example

```bash
wget https://example.com/software.tar.gz
```

---

# 📂 Step 2: Extract the Archive

```bash
tar -xvf software.tar.gz
```

Options:

| Option | Meaning |
|----------|----------|
| `-x` | Extract |
| `-v` | Verbose |
| `-f` | File |

Example

```bash
tar -xvf nginx.tar.gz
```

---

# 📁 Step 3: Change Directory

```bash
cd software
```

Example

```bash
cd nginx-1.28.0
```

---

# ⚙️ Step 4: Configure

```bash
./configure
```

The configure script:

- Checks required libraries
- Verifies compiler availability
- Detects operating system
- Creates Makefile

Example Output

```
Checking compiler...

Checking libraries...

Creating Makefile...
```

---

# 🔨 Step 5: Compile

```bash
make
```

The `make` command reads the **Makefile** and compiles the source code into executable binaries.

Example Output

```
Compiling source files...

Linking objects...

Build complete.
```

---

# 📦 Step 6: Install

```bash
sudo make install
```

This copies the compiled binaries, libraries, and configuration files to the appropriate system directories.

---

# 🛠️ Common Build Tools

| Tool | Purpose |
|------|---------|
| `gcc` | GNU C Compiler |
| `g++` | GNU C++ Compiler |
| `make` | Build automation tool |
| `cmake` | Cross-platform build system |
| `autoconf` | Generates configure scripts |
| `automake` | Generates Makefile templates |

---

# 🧩 Compilation Architecture

```
Source Code (.c/.cpp)
        │
        ▼
Compiler (gcc/g++)
        │
        ▼
Object Files (.o)
        │
        ▼
Linker
        │
        ▼
Executable Binary
```

---

# 💼 Production Example

Compile the latest version of Nginx:

```bash
wget https://nginx.org/download/nginx-1.28.0.tar.gz

tar -xvf nginx-1.28.0.tar.gz

cd nginx-1.28.0

./configure

make

sudo make install
```

---

# ⚠️ Common Compilation Errors

### Missing Compiler

```
gcc: command not found
```

**Solution**

```bash
sudo apt install build-essential
```

or

```bash
sudo dnf groupinstall "Development Tools"
```

---

### Missing Libraries

```
configure: error:
OpenSSL library not found
```

Install the required development package before running `./configure` again.

---

# 🎯 Interview Tips

- `apt update` refreshes package metadata.
- `apt upgrade` installs newer versions of installed packages.
- `apt full-upgrade` can remove obsolete packages to satisfy dependencies.
- Source compilation is useful when repositories do not contain the required version.
- The typical compilation flow is:
  - `./configure`
  - `make`
  - `sudo make install`

---

## 📝 Quick Revision

| Command | Description |
|----------|-------------|
| `apt update` | Refresh package metadata |
| `apt upgrade` | Upgrade installed packages |
| `apt full-upgrade` | Perform full system upgrade |
| `dnf check-update` | Check available updates |
| `dnf upgrade` | Upgrade packages |
| `tar -xvf file.tar.gz` | Extract archive |
| `./configure` | Prepare build environment |
| `make` | Compile source code |
| `sudo make install` | Install compiled software |

---
