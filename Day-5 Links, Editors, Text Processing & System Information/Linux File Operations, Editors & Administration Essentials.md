# Linux Command Guide

---

## `ln` Command (Link Creation)
The `ln` command in Linux is used to create **links** between files. There are two types of links:
- **Hard Links**
- **Symbolic (Soft) Links**

### Syntax
```bash
ln originalfile linkfile         # Hard Link
ln -s originalfile linkfile     # Soft Link (Symbolic)
```

### Example
```bash
sudo ln devops.txt hardlink.txt
ln -s devops.txt softlink.txt   # It will start with 'l' in ls -l output
```

### Hard Link vs Soft Link
| Feature                          | Hard Link                                   | Soft Link (Symbolic)                      |
|----------------------------------|---------------------------------------------|-------------------------------------------|
| Inode Number                     | Same as original                            | Different from original                   |
| File Deletion Impact            | Still accessible                            | Link breaks if original is deleted       |
| Works With                      | Files only                                  | Files and directories                    |
| Data Synchronization            | Yes                                         | Yes                                      |
| Cross-filesystem Linking        | No                                          | Yes                                      |
| Identified With `ls -l`         | Regular file                                | Starts with 'l'                          |

### Use Cases
- Create multiple names for one file without duplicating data.
- Maintain backup references.
- Organize directory access using symbolic links.
- Shortcuts to config files or frequently accessed paths.

---

## `tr` Command (Translate Characters)
The `tr` command is used to translate or delete characters from input provided via stdin.

### Syntax
```bash
cat demo.txt | sort | tr [a-z] [A-Z]  # Converts lowercase to uppercase
```

### Use Case
- Format output (like logs or reports) to a specific case.
- Clean or normalize input data.

---

## Linux Editors

### `vi` Editor
A powerful, standard editor available on all Unix/Linux systems.

```bash
vi demo.txt     # Open file
:wq             # Save and exit
:q!             # Quit without saving
:q              # Quit if no changes
```

#### Navigation
```bash
:se nu        # Show line numbers
:se nonu      # Hide line numbers
:90           # Go to line 90
/data         # Search for 'data'
dd            # Delete a line
u             # Undo
```

### Use Case
- System administrators use `vi` to quickly edit config files.
- Lightweight and efficient on low-resource servers.

---

### `nano` Editor
A beginner-friendly text editor in Linux.

```bash
nano demo.txt
sudo yum install nano -y     # Install nano if not available
```

#### Commands
- Ctrl+O  → Save
- Ctrl+X  → Exit

### Use Case
- Quick and intuitive editing of small files or scripts.

---

## `find` Command (Search Files & Directories)
Used to search for files and directories based on different filters.

### Syntax & Examples
```bash
find . -type f -empty                 # Find empty files in current directory
find ~ -type f -empty                # Find empty files in home directory
find /tmp -type f -empty            # Find empty files in /tmp
find . -type d -name <dirName>      # Search directory by name

find . -name deployment.yaml         # Case-sensitive search
find . -iname deployment.yaml        # Case-insensitive search
find . -type f -perm 0777            # Files with 777 permissions

find . -mtime 1                      # Modified exactly 1 day ago
find . -mtime -1                     # Modified less than 1 day ago
find . -mtime +1                     # Modified more than 1 day ago

find ./ -type f -name "*.txt"        # Find all .txt files

```

### Use Case
- Locate old log files for cleanup.
- Search configuration files across directory structures.
- Security scans for permission issues.

---

## `sed` Command (Stream Editor)
Used for parsing and transforming text in files without opening them.

### Syntax & Examples
```bash
sed 's/unix/linux/' abc.txt          # Replace first occurrence
sed 's/unix/linux/2' abc.txt         # Replace 2nd occurrence
sed 's/unix/linux/g' abc.txt         # Replace all occurrences

sed '3 s/unix/linux/' abc.txt        # Replace on line 3
sed '3 s/am/was/p' sed.txt           # Duplicate replaced line
sed -n 's/am/was/p' sed.txt          # Print only replaced lines

sed '1,3 s/unix/linux/' abc.txt      # Replace in line range
sed '5d' filename.txt                # Delete line 5
sed '3,6d' filename.txt              # Delete lines 3 to 6
sed -n '60,80p' filename             # To display lines 60 to 80 of a file using sed

```

### Use Case
- Modify large files programmatically.
- Replace strings in configuration or data files.
- Scripted cleanup of logs or report files.

---

## `who` Command (User Sessions)
Displays users currently logged into the system.

```bash
who -H    # Display with headers
```

## `w` Command
Shows who is logged in and what they are doing.

```bash
w
```

### Use Case
- Monitor logged-in users.
- Check terminal activity.
- System performance monitoring.

---

## `/proc/cpuinfo` (CPU Info)
```bash
cat /proc/cpuinfo     # Displays processor details
```

### Load Average
Found in output of `top` or `uptime`:
```
load average: 0.08, 0.15, 0.16
```
- 1st value → last 1 minute
- 2nd value → last 5 minutes
- 3rd value → last 15 minutes

### Use Case
- Identify CPU usage over time.
- Detect overloaded systems.
- Useful for performance tuning and diagnostics.

---

---

# Linux Interview Questions & Answers (Real-Time Scenarios)

## 1. What is the purpose of the `ln` command?

### Answer

The `ln` command is used to create links between files.

```bash
ln source.txt hardlink.txt
ln -s source.txt softlink.txt
```

**Real-Time Use Case:**
Create shortcuts to configuration files or share the same file using multiple names without duplicating data.

---

## 2. What is the difference between Hard Link and Soft Link?

### Answer

| Hard Link                       | Soft Link                          |
| ------------------------------- | ---------------------------------- |
| Same inode                      | Different inode                    |
| Works only for files            | Works for files and directories    |
| Survives original file deletion | Breaks if original file is deleted |
| Cannot cross filesystems        | Can cross filesystems              |

**Interview Tip:**
Hard Link points to inode, Soft Link points to file path.

---

## 3. How can you identify a symbolic link?

### Answer

```bash
ls -l
```

Output starts with:

```bash
lrwxrwxrwx
```

The letter `l` indicates a symbolic link.

---

## 4. What happens if the original file is deleted?

### Answer

* Hard Link → Still accessible
* Soft Link → Becomes a broken link

---

## 5. Why can't hard links be created across filesystems?

### Answer

Hard links depend on inode numbers, which are unique only within the same filesystem.

---

## 6. What is the `tr` command used for?

### Answer

The `tr` command translates or deletes characters from standard input.

```bash
echo "linux" | tr a-z A-Z
```

Output:

```bash
LINUX
```

---

## 7. How would you convert a file's contents to uppercase?

### Answer

```bash
cat file.txt | tr a-z A-Z
```

---

## 8. Which editor is commonly preferred in production environments?

### Answer

Most Linux administrators prefer **vi/vim** because:

* Installed by default
* Lightweight
* Works in recovery mode
* Efficient for remote servers

---

## 9. How do you save and quit in vi editor?

### Answer

```bash
:wq
```

---

## 10. How do you quit vi without saving changes?

### Answer

```bash
:q!
```

---

## 11. How do you search for a word inside vi?

### Answer

```bash
/error
```

This searches for the word "error".

---

## 12. What is the purpose of the `find` command?

### Answer

The `find` command searches files and directories based on:

* Name
* Type
* Permissions
* Size
* Modification time

Example:

```bash
find / -name "*.log"
```

---

## 13. How do you find files modified in the last 24 hours?

### Answer

```bash
find /var/log -type f -mtime -1
```

---

## 14. How do you find files with 777 permissions?

### Answer

```bash
find / -type f -perm 777
```

**Real-Time Use Case:** Security audits and compliance checks.

---

## 15. What is `sed`?

### Answer

`sed` (Stream Editor) is used to:

* Search text
* Replace text
* Delete lines
* Modify files without opening them

---

## 16. Replace all occurrences of "dev" with "prod" in a file.

### Answer

```bash
sed 's/dev/prod/g' file.txt
```

---

## 17. How do you print lines 50–100 from a file using sed?

### Answer

```bash
sed -n '50,100p' file.txt
```

---

## 18. What is the difference between `who` and `w`?

### Answer

### who

Displays logged-in users.

```bash
who
```

### w

Displays:

* Logged-in users
* Login time
* Running processes
* System load

```bash
w
```

---

## 19. How do you check CPU information in Linux?

### Answer

```bash
cat /proc/cpuinfo
```

Shows:

* CPU Model
* Number of Cores
* Threads
* Cache Information
* Processor Details

---

## 20. What is Load Average and how do you interpret it?

### Answer

```bash
uptime
```

Example:

```text
load average: 1.20, 0.90, 0.75
```

Represents:

* Last 1 minute
* Last 5 minutes
* Last 15 minutes

### Real-Time Scenario

For a server with 4 CPU cores:

* Load < 4 → Healthy
* Load = 4 → Fully utilized
* Load > 4 → CPU bottleneck

**Interview Answer:**
Load Average indicates the number of processes waiting for CPU resources. If the load consistently exceeds the number of CPU cores, the server may be overloaded.

---

# Scenario-Based Interview Questions

## 21. A symbolic link is not working. How will you troubleshoot?

### Answer

```bash
ls -l linkfile
```

Verify whether the target file exists.

```bash
file linkfile
```

If broken:

```bash
rm linkfile
ln -s targetfile linkfile
```

---

## 22. A directory contains thousands of log files. How will you delete logs older than 30 days?

### Answer

```bash
find /logs -type f -mtime +30 -delete
```

---

## 23. How do you replace an IP address across multiple configuration files?

### Answer

```bash
sed -i 's/10.0.0.1/10.0.0.2/g' *.conf
```

---

## 24. Users report slowness on a Linux server. What will you check first?

### Answer

```bash
uptime
w
top
cat /proc/cpuinfo
```

Check:

* Load Average
* CPU Utilization
* Logged-in Users
* Running Processes
* CPU Capacity

---

## 25. How do you find all empty files on a server?

### Answer

```bash
find / -type f -empty
```

---

## 26. How do you find all empty directories?

### Answer

```bash
find / -type d -empty
```

---

## 27. How do you search for a file regardless of case sensitivity?

### Answer

```bash
find . -iname deployment.yaml
```

---

## 28. How do you delete lines 10–20 from a file using sed?

### Answer

```bash
sed '10,20d' file.txt
```

---

## 29. How do you display only lines 60–80 of a file?

### Answer

```bash
sed -n '60,80p' filename
```

---

## 30. During a production issue, which Linux commands do you use first?

### Answer

```bash
w
who
uptime
top
cat /proc/cpuinfo
```

These commands help quickly identify:

* Active users
* Running sessions
* Server load
* CPU availability
* Resource bottlenecks

---
