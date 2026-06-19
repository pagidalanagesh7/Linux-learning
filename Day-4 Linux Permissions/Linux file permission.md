# Linux Permissions, UMASK, CHMOD, CHOWN & CHGRP Guide 🐧

## Table of Contents

1. UMASK
2. File Permissions Basics
3. CHMOD
4. Directory Permissions
5. CHOWN
6. CHGRP
7. FILE Command
8. DIFF Command
9. ECHO Command

---

# 1. UMASK (User Mask)

UMASK determines the default permissions for newly created files and directories.

```bash
umask
```

Display current umask value.

### Default UMASK

| User Type   | UMASK | Default File | Default Directory |
| ----------- | ----- | ------------ | ----------------- |
| Root User   | 0022  | 644          | 755               |
| Normal User | 0022  | 644          | 755               |

> RHEL 9.x default umask = 0022

---

## How UMASK Works

### Base Permissions

Files are created with:

```text
0666
```

Directories are created with:

```text
0777
```

Then Linux subtracts the UMASK value.

### File Example

```text
Base Permission : 0666
UMASK           : 0022
----------------------
Result          : 0644
```

Permission:

```text
-rw-r--r--
```

---

### Directory Example

```text
Base Permission : 0777
UMASK           : 0022
----------------------
Result          : 0755
```

Permission:

```text
drwxr-xr-x
```

---

## Create File and Directory Example

```bash
mkdir DevOps
touch demo.txt

ls -ld DevOps
ls -l demo.txt
```

Output:

```text
drwxr-xr-x DevOps
-rw-r--r-- demo.txt
```

### Permission Breakdown

```text
Directory (755)

Owner   = rwx = 7
Group   = r-x = 5
Others  = r-x = 5
```

```text
File (644)

Owner   = rw- = 6
Group   = r-- = 4
Others  = r-- = 4
```

---

## Changing UMASK

Display current value:

```bash
umask
```

Set new value:

```bash
umask 222
```

⚠️ Note:

Changing umask affects only newly created files/directories.

Existing files/directories will NOT change.

---

# 2. Understanding File Permissions

Linux permissions consist of:

```text
Read     (r)
Write    (w)
Execute  (x)
```

---

## Permission Values

```text
r = 4
w = 2
x = 1
```

### Examples

```text
rwx = 4+2+1 = 7
rw- = 4+2+0 = 6
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
```

---

## Permission Structure

```text
-rwxr-xr--

 | |  |  |
 | |  |  +---- Others
 | |  +------- Group
 | +---------- User
 +------------ File Type
```

### Tree View

```text
Permissions
│
├── User (u)
│   ├── Read
│   ├── Write
│   └── Execute
│
├── Group (g)
│   ├── Read
│   ├── Write
│   └── Execute
│
└── Others (o)
    ├── Read
    ├── Write
    └── Execute
```

---

# 3. CHMOD

Change file or directory permissions.

```bash
chmod [permissions] file
```

---

## Remove All Permissions

```bash
chmod 000 devops.txt
```

Check:

```bash
cat devops.txt
```

Access denied.

---

## Read Only

```bash
chmod 444 devops.txt
```

or

```bash
chmod +r devops.txt
```

---

## Permission 766

```bash
chmod 766 devops.txt
```

Equivalent:

```bash
chmod u+rwx,go+rw devops.txt
```

Result:

```text
rwxrw-rw-
```

---

## Permission 777

```bash
chmod 777 devops.txt
```

or

```bash
chmod ugo+rwx devops.txt
```

Result:

```text
rwxrwxrwx
```

---

## Add Permissions

```bash
chmod u+x file.txt
```

Add execute for owner.

```bash
chmod g+w file.txt
```

Add write for group.

---

## Remove Permissions

```bash
chmod o-r file.txt
```

Remove read from others.

```bash
chmod u-w file.txt
```

Remove write from owner.

---

## Set Exact Permissions

```bash
chmod u=rwx,g=rx,o=r file.txt
```

Result:

```text
754
```

---

## Verbose Mode

```bash
chmod -v 644 file.txt
```

Shows changes performed.

---

## Interview Question

### 1. User has Write permission but cannot open file?

Because:

```text
Write ≠ Read
```

User must also have read permission.

Example:

```text
-w-------
```

Can modify but cannot read.

---

## 2. Difference Between

### chmod 400 file.txt

Sets exact permission:

```text
r--------
```

Everything else removed.

---

### chmod ugo+r file.txt

Adds read permission only.

Existing permissions remain.

Example:

```text
Before : rwxr-x---
After  : rwxr-xr--
```

---

# Directories

### 1. Change Parent Directory Only

```bash
chmod 444 DevOps/
```

Only DevOps directory changes.

Subdirectories remain unchanged.

---

### 2. Add Execute

```bash
chmod ugo+x DevOps/
```

---

### 3. Recursive Change

```bash
chmod -R 444 DevOps/
```

Changes:

* Parent directory
* Subdirectories
* Files

---

## Interview Question

### 1. Difference

```bash
chmod 777 file
```

vs

```bash
chmod ugo+rwx file
```

### 777

Overrides existing permissions completely.

### ugo+rwx

Adds permissions without removing existing ones.

---

# 5. CHOWN

(Change Owner)

Only root user can change ownership.

```bash
chown owner file
```

---

## Examples

```bash
sudo chown root devops.txt
```

```bash
sudo chown -R root DevOps
```

```bash
chown root *.java
```

---

## Root Login

### Switch to Root

```bash
sudo su -
```

Moves to:

```text
/root
```

---

### Without Hyphen

```bash
sudo su
```

Stays in current user's working directory.

---

## Root Home Directory

```text
/        -> Root filesystem
/root    -> Root user's home directory
/home    -> Normal users home directory
```

---

# 6. CHGRP

(Change Group)

Usually performed by root/admin users.

```bash
chgrp wheel devops.txt
```

---

## Available Groups

```bash
cat /etc/group
```

---

## Recursive

```bash
chgrp -R wheel DevOps
```

---

## Change Owner and Group Together

```bash
chown ec2-user:ec2-user devops.txt
```

```bash
chown ec2-user:ec2-user DevOps
```

---

# 7. FILE Command

Used to identify file type.

```bash
file demo.txt
```

```bash
file test.txt
```

Examples:

```text
ASCII text
Bourne shell script
ELF executable
directory
```

---

# 8. DIFF Command

Compare two files line by line.

```bash
diff file1.txt file2.txt
```

Example:

```bash
diff old.txt new.txt
```

Shows differences.

---

# 9. ECHO Command

Print text to terminal.

```bash
echo hello java
```

Output:

```text
hello java
```

---

```bash
echo hello        java
```

Output:

```text
hello java
```

Multiple spaces collapse into one.

---

```bash
echo "hello       java"
```

Output:

```text
hello       java
```

Spaces preserved inside quotes.

---

# Quick Revision Diagram

```text
Linux Permissions
│
├── UMASK
│   ├── Display -> umask
│   └── Change  -> umask 022
│
├── CHMOD
│   ├── Add Permissions
│   ├── Remove Permissions
│   └── Set Exact Permissions
│
├── CHOWN
│   ├── Change Owner
│   └── Recursive Change
│
├── CHGRP
│   ├── Change Group
│   └── Recursive Change
│
├── FILE
│   └── Detect File Type
│
└── DIFF
    └── Compare Files
```

---

## Common Commands Cheat Sheet

```bash
umask
umask 022

chmod 777 file.txt
chmod 644 file.txt
chmod u+x file.txt
chmod -R 755 Dir/

chown root file.txt
chown -R root Dir/

chgrp wheel file.txt

file test.txt

diff file1 file2

echo "Hello Linux"
```

# 12. Most Asked Interview Questions

# 🎯 Most Asked Linux Permission Interview Questions

### Q1. What is UMASK?

UMASK controls the default permissions for newly created files and directories.

Example:

```text
Files       : 666 - 022 = 644
Directories : 777 - 022 = 755
```

---

### Q2. Why are files created with 644 permissions by default?

Because:

```text
Base Permission = 666
UMASK           = 022
Result          = 644
```

---

### Q3. Why are directories created with 755 permissions by default?

Because:

```text
Base Permission = 777
UMASK           = 022
Result          = 755
```

---

### Q4. Difference between chmod and chown?

```text
chmod -> Changes permissions

chown -> Changes ownership
```

Example:

```bash
chmod 755 file.txt

chown ec2-user file.txt
```

---

### Q5. Difference between 777 and 755?

```text
777 -> Everyone has Read, Write and Execute permissions

755 -> Owner has full access,
       Group and Others have Read + Execute only
```

---

### Q6. Difference between chmod 777 and chmod ugo+rwx?

```text
chmod 777
→ Sets exact permissions

chmod ugo+rwx
→ Adds permissions without removing existing ones
```

---

### Q7. Why can't a user read a file even with write permission?

Because:

```text
Write ≠ Read
```

A user needs Read permission to view file contents.

Example:

```text
-w-------
```

User can write but cannot read.

---

### Q8. What is SUID?

SUID (Set User ID) allows a program to run with the file owner's privileges.

Example:

```bash
passwd
```

Permission:

```text
-rwsr-xr-x
```

---

### Q9. What is SGID?

SGID (Set Group ID) allows a program to run with the file group's privileges.

For directories, newly created files inherit the parent directory's group.

Example:

```bash
chmod 2755 project
```

---

### Q10. What is Sticky Bit?

Sticky Bit allows only the file owner to delete or rename files inside a shared directory.

Example:

```bash
ls -ld /tmp
```

Output:

```text
drwxrwxrwt
```

`t` indicates Sticky Bit.

---

### Q11. What is ACL?

ACL (Access Control List) provides fine-grained permissions beyond traditional User, Group, and Others permissions.

Example:

```bash
setfacl -m u:john:rwx file.txt
```

View ACL:

```bash
getfacl file.txt
```

---

### Q12. Why is chmod 777 considered dangerous?

Because every user can:

```text
Read
Write
Execute
```

This creates security risks and should be avoided in production environments.

---

### Q13. Difference between File Permissions and Ownership?

```text
Permissions -> Define what actions are allowed

Ownership  -> Defines who owns the file
```

Example:

```text
-rwxr-xr--

Owner : ec2-user
Group : developers
```

---

### Q14. Difference between chown and chgrp?

```text
chown -> Changes file owner

chgrp -> Changes file group
```

Examples:

```bash
chown ec2-user file.txt

chgrp developers file.txt
```

---

### Q15. Difference between sudo su and sudo su - ?

```text
sudo su
```

Switches to root user but keeps the current user's environment.

```text
sudo su -
```

Switches to root user and loads root user's environment.

Root Home Directory:

```text
/root
```

---

### Q16. How do you recursively change permissions?

```bash
chmod -R 755 DevOps
```

Changes permissions for:

* Parent Directory
* Subdirectories
* Files

---

### Q17. How do you recursively change ownership?

```bash
chown -R ec2-user:ec2-user DevOps
```

Changes ownership for:

* Parent Directory
* Subdirectories
* Files

```
```

---


Happy Learning Linux 🐧🚀
