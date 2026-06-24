# 🚀 Linux Day 9 (Part 2)

# User Management, File Viewing & Background Process Execution

---

# 👤 userdel Command

## What is userdel?

`userdel` is used to delete an existing user account from a Linux system.

It removes the user entry from:

* `/etc/passwd`
* `/etc/shadow`
* `/etc/group` (if applicable)

---

## Syntax

```bash
userdel [options] username
```

---

## Examples

Delete a user:

```bash
userdel devuser
```

Delete a user along with home directory:

```bash
userdel -r devuser
```

Force delete a user:

```bash
userdel -f devuser
```

---

## Common Options

| Option | Description           |
| ------ | --------------------- |
| -r     | Remove home directory |
| -f     | Force deletion        |
| -h     | Help                  |

---

## Best Practice

Before deleting a user:

```bash
ps -u devuser
```

Verify no critical processes are running.

---

# 👥 groupdel Command

## What is groupdel?

`groupdel` removes an existing group from Linux.

Used when a group is no longer required.

---

## Syntax

```bash
groupdel groupname
```

---

## Examples

```bash
groupdel developers
```

```bash
groupdel testing
```

---

## Best Practice

Verify no users depend on the group.

Check group membership:

```bash
getent group developers
```

---

# ⚖️ userdel vs groupdel

| Feature                | userdel         | groupdel         |
| ---------------------- | --------------- | ---------------- |
| Removes User           | ✅               | ❌                |
| Removes Group          | ❌               | ✅                |
| Deletes Home Directory | Optional        | ❌                |
| Used For               | User Management | Group Management |

---

# 📖 more Command

## What is more?

`more` displays file content page by page.

Useful for reading large files without opening an editor.

---

## Syntax

```bash
more logfile.log
```

---

## Example

```bash
more /var/log/messages
```

---

## Navigation Keys

| Key   | Action    |
| ----- | --------- |
| Space | Next Page |
| Enter | Next Line |
| q     | Quit      |

---

# 📚 less Command

## What is less?

`less` is an advanced file viewer.

Unlike `more`, it allows:

* Forward navigation
* Backward navigation
* Searching content

---

## Syntax

```bash
less logfile.log
```

---

## Example

```bash
less /var/log/messages
```

---

## Search Examples

Search for error:

```bash
/error
```

Search for warning:

```bash
/warning
```

Next result:

```bash
n
```

---

## Why Admins Prefer less?

Because it handles very large log files efficiently.

---

# 📊 more vs less

| Feature             | more    | less      |
| ------------------- | ------- | --------- |
| Forward Navigation  | ✅       | ✅         |
| Backward Navigation | ❌       | ✅         |
| Search Capability   | Limited | Advanced  |
| Large File Handling | Good    | Excellent |
| Admin Preference    | Medium  | High      |

---

# ⚙️ nohup Command

## What is nohup?

`nohup` stands for:

```text
No Hang Up
```

It keeps a process running even after the user logs out.

---

## Syntax

```bash
nohup command &
```

---

## Example

```bash
nohup sh backup.sh &
```

---

## Output

By default:

```bash
nohup.out
```

stores the command output.

---

# 🚀 nohup sh demo.sh & Explained

## Command

```bash
nohup sh demo.sh &
```

---

## Breakdown

### nohup

Ignores terminal hangup signal.

---

### sh

Runs the shell interpreter.

---

### demo.sh

Shell script to execute.

---

### &

Runs process in background.

---

## Verification

Check process:

```bash
ps -ef | grep demo.sh
```

---

Check jobs:

```bash
jobs -l
```

---

# 🔄 Background Job Monitoring

## View Jobs

```bash
jobs
```

Detailed view:

```bash
jobs -l
```

---

## View Processes

```bash
ps -ef
```

---

## Real-Time Monitoring

```bash
top
```

---

# 📂 Log Monitoring

Monitor logs continuously:

```bash
tail -f app.log
```

View logs page-wise:

```bash
less app.log
```

```bash
more app.log
```

---

# 💡 Pro Tips

### Redirect Output Properly

```bash
nohup sh demo.sh > app.log 2>&1 &
```

---

### Monitor Logs

```bash
tail -f app.log
```

---

### Search Logs Quickly

Inside less:

```bash
/ERROR
```

---

### Verify Running Jobs

```bash
jobs -l
```

---

# 🎯 Key Takeaway

Linux administrators frequently manage users, inspect large log files, and execute long-running tasks.

Mastering:

* userdel
* groupdel
* more
* less
* nohup

helps ensure safe administration, efficient troubleshooting, and reliable production operations.

---

# 🎤 Real-Time Project Scenario Questions & Answers

## 1. A user left the company. How would you safely remove the account?

### Answer

Check running processes:

```bash
ps -u username
```

Remove account:

```bash
userdel -r username
```

Verify deletion.

---

## 2. You accidentally deleted a user without -r. What happens?

### Answer

The user account is removed but the home directory remains on the server.

---

## 3. Developers report application logs are huge (10GB+). Which command would you use?

### Answer

```bash
less application.log
```

Because it supports searching and backward navigation.

---

## 4. Why would you choose less over more?

### Answer

Because less supports:

* Search
* Backward movement
* Better handling of large files

---

## 5. A backup script must continue running after logout. What command would you use?

### Answer

```bash
nohup sh backup.sh &
```

---

## 6. How do you verify whether a background script is still running?

### Answer

```bash
ps -ef | grep backup.sh
```

or

```bash
jobs -l
```

---

## 7. Where does nohup store output by default?

### Answer

```bash
nohup.out
```

---

## 8. Application deployment takes 2 hours. How would you run it safely?

### Answer

```bash
nohup sh deploy.sh > deploy.log 2>&1 &
```

---

## 9. How do you monitor deployment progress?

### Answer

```bash
tail -f deploy.log
```

---

## 10. A group is no longer required. How do you remove it?

### Answer

```bash
groupdel developers
```

After verifying no users depend on it.

---

## 11. How do you find users belonging to a group?

### Answer

```bash
getent group developers
```

---

## 12. Your script stopped after SSH disconnect. Why?

### Answer

It was not executed using:

```bash
nohup
```

or a session manager like screen/tmux.

---

## 13. How do you search for "ERROR" inside a log file?

### Answer

```bash
less app.log
```

Then:

```bash
/ERROR
```

---

## 14. How do you continuously monitor production logs?

### Answer

```bash
tail -f application.log
```

---

## 15. During troubleshooting, what commands do you commonly use together?

### Answer

```bash
ps -ef
```

```bash
jobs -l
```

```bash
tail -f app.log
```

```bash
less app.log
```

These commands help verify process status, monitor logs, and troubleshoot production issues efficiently.
