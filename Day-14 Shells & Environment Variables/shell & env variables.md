# 🚀 Linux Series – Day 14

# Shells & Environment Variables

> **Shell Types | Environment Variables | Shell Configuration Files**

---

# 📚 What You'll Learn

* Shell Types (`sh`, `bash`, `zsh`)
* Environment Variables
* `printenv` Command
* `export` Command
* `.bashrc`
* `.profile`
* Real-Time DevOps Use Cases
* Production Troubleshooting
* Interview Questions

---

# 1. What is a Shell?

A **Shell** is a command-line interpreter that acts as an interface between the **User** and the **Linux Kernel**.

It accepts commands from the user, interprets them, and passes them to the kernel for execution.

## Architecture

```text
      User
        │
        ▼
+----------------+
| Shell (bash)   |
+----------------+
        │
        ▼
+----------------+
| Linux Kernel   |
+----------------+
        │
        ▼
 Hardware Resources
```

### Responsibilities

* Execute Linux commands
* Run shell scripts
* Manage environment variables
* Launch applications
* Automate repetitive tasks

> **Interview Tip:** The shell is the bridge between the user and the Linux kernel.

---

# 2. Types of Linux Shells

## A. sh (Bourne Shell)

The Bourne Shell (`sh`) is the original UNIX shell.

### Features

* Lightweight
* POSIX compliant
* Basic scripting
* Available on almost every UNIX system

### Example

```bash
sh script.sh
```

---

## B. bash (Bourne Again Shell)

`bash` is the most popular Linux shell and the default shell in most Linux distributions.

### Features

* Command History
* Auto Completion
* Aliases
* Variables
* Advanced Shell Scripting

### Check Bash Version

```bash
echo $BASH_VERSION
```

Example Output

```text
5.2.x
```

Run a Script

```bash
bash script.sh
```

---

## C. zsh (Z Shell)

Z Shell is an advanced interactive shell widely used by developers.

### Features

* Powerful Auto Completion
* Themes
* Plugins
* Better Command Suggestions
* High Customization

### Commands

```bash
zsh
```

```bash
echo $ZSH_VERSION
```

Example Output

```text
5.9
```

---

## Shell Comparison

| Feature         | sh | bash    | zsh        |
| --------------- | -- | ------- | ---------- |
| Basic Shell     | ✅  | ✅       | ✅          |
| Shell Scripting | ✅  | ✅       | ✅          |
| Command History | ❌  | ✅       | ✅          |
| Auto Completion | ❌  | ✅       | ✅ Advanced |
| Themes          | ❌  | ❌       | ✅          |
| Plugins         | ❌  | Limited | ✅          |
| Most Popular    | ❌  | ✅       | Growing    |

> **Interview Tip:** Bash is the default shell on most Linux distributions.

---

# 3. Environment Variables

Environment Variables are **name-value pairs** used by the operating system and applications.

They provide configuration information to programs.

Example

```text
HOME=/home/devops
USER=nagesh
PATH=/usr/bin:/bin
SHELL=/bin/bash
```

---

## Common Environment Variables

| Variable | Purpose                   |
| -------- | ------------------------- |
| HOME     | User Home Directory       |
| PATH     | Executable Search Path    |
| USER     | Current Username          |
| SHELL    | Current Shell             |
| PWD      | Present Working Directory |
| HOSTNAME | System Hostname           |
| LANG     | Language Settings         |

---

## Environment Variable Flow

```text
User Login
      │
      ▼
Shell Starts
      │
Loads Environment Variables
      │
Applications Read Variables
```

> Environment variables help applications locate executables, configuration files, and user settings.

---

# 4. printenv Command

Displays environment variables.

## Display All Variables

```bash
printenv
```

---

## Display Specific Variable

```bash
printenv PATH
```

```bash
printenv HOME
```

Example Output

```text
HOME=/home/devops
PATH=/usr/local/bin:/usr/bin:/bin
```

### Production Use Cases

* Verify PATH
* Debug applications
* Check runtime configuration

---

# 5. export Command

`export` creates environment variables that are inherited by child processes.

Syntax

```bash
export VARIABLE=value
```

Example

```bash
export NAME=Nagesh
```

Verify

```bash
echo $NAME
```

Output

```text
Nagesh
```

---

## Add Directory to PATH

```bash
export PATH=$PATH:/opt/scripts
```

---

## Remove Variable

```bash
unset NAME
```

> **Interview Tip:** Variables created using `export` are available to child processes.

---

# 6. Shell Configuration Files

## ~/.bashrc

`.bashrc` is executed whenever an **interactive Bash shell** starts.

Common Uses

* Aliases
* Functions
* Prompt Customization
* Environment Variables

Example

```bash
export JAVA_HOME=/usr/lib/jvm/java-17
```

```bash
alias ll='ls -la'
```

Reload File

```bash
source ~/.bashrc
```

---

## ~/.profile

`.profile` executes during **user login**.

Common Uses

* PATH Configuration
* Login Environment Variables
* Startup Commands

Example

```bash
export PATH=$PATH:$HOME/bin
```

---

## Difference Between `.bashrc` and `.profile`

| .bashrc                          | .profile               |
| -------------------------------- | ---------------------- |
| Runs for Interactive Bash Shells | Runs During Login      |
| Stores Aliases                   | Stores Login Variables |
| Prompt Customization             | PATH Configuration     |
| Frequently Loaded                | Loaded Once Per Login  |

---

# Shell Startup Sequence

```text
User Login
     │
     ▼
.profile
     │
     ▼
bash Starts
     │
     ▼
.bashrc
     │
     ▼
Ready to Use
```

---

# Best Practices

* Store aliases inside `.bashrc`
* Store login configuration inside `.profile`
* Reload changes using:

```bash
source ~/.bashrc
```

---

# Real-Time DevOps Use Cases

* Configure JAVA_HOME
* Configure MAVEN_HOME
* Configure Terraform PATH
* Configure AWS CLI
* Configure Kubernetes CLI
* Configure Docker Environment
* Configure Jenkins Build Agents
* Configure CI/CD Pipelines
* Configure Application Runtime Variables
* Customize Administrator Shell

---

# Production Troubleshooting

## Scenario 1

Command Not Found

```text
echo $PATH
      ↓
printenv PATH
      ↓
export PATH=...
      ↓
source ~/.bashrc
```

---

## Scenario 2

Environment Variable Missing

```text
printenv
      ↓
export VARIABLE=value
      ↓
source ~/.bashrc
```

---

## Scenario 3

Alias Not Working

```text
cat ~/.bashrc
      ↓
Verify Alias
      ↓
source ~/.bashrc
```

---

# Interview Questions & Answers

## 1. What is a Shell?

A shell is a command-line interpreter that allows users to interact with the Linux kernel.

---

## 2. Difference between sh, bash and zsh?

| sh                  | bash                     | zsh                                  |
| ------------------- | ------------------------ | ------------------------------------ |
| Original UNIX shell | Most popular Linux shell | Advanced interactive shell           |
| Basic features      | Scripting + History      | Plugins + Themes + Better Completion |

---

## 3. Which shell is used by default in Linux?

**bash** is the default shell in most Linux distributions.

---

## 4. What are Environment Variables?

Environment variables store configuration values that applications and the operating system use during execution.

---

## 5. What is PATH?

PATH contains directories where Linux searches for executable commands.

---

## 6. What does printenv do?

Displays all or specific environment variables.

Example

```bash
printenv
```

---

## 7. What does export do?

Creates environment variables that child processes inherit.

Example

```bash
export JAVA_HOME=/usr/lib/jvm/java-17
```

---

## 8. Difference between `.bashrc` and `.profile`?

* `.profile` executes during login.
* `.bashrc` executes for interactive Bash sessions.

---

## 9. How do you reload `.bashrc`?

```bash
source ~/.bashrc
```

---

## 10. How do you check your current shell?

```bash
echo $SHELL
```

---

# Must Remember

* Shell connects the user and Linux kernel.
* `bash` is the default shell on most Linux systems.
* `zsh` provides advanced customization and plugins.
* `printenv` displays environment variables.
* `export` creates environment variables.
* `PATH` defines executable search locations.
* `.profile` executes during login.
* `.bashrc` executes for interactive Bash sessions.
* Use `source ~/.bashrc` after modifying `.bashrc`.

---

# Key Takeaways

Understanding Linux shells and environment variables is essential for Linux Administrators, DevOps Engineers, Cloud Engineers, and SREs. Mastering **sh, bash, zsh, printenv, export, `.bashrc`, and `.profile`** helps configure development environments, automate administration, troubleshoot runtime issues, and build reliable CI/CD pipelines.
