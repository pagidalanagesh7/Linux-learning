# 👤 User and Group Management in RHEL (Red Hat Enterprise Linux)

---

## 💾 Creating Users with `useradd`

🔐 **Only the `root` user or users with `sudo` privileges can create new users.**

### 🔹 Basic Commands:

```bash
ls -l /home                     # List user home directories
sudo useradd nagesdevops            # Create a new user named 'nagesdevops'
cat /etc/passwd                 # View all user account information
cat /etc/group                  # View all group information
cat /etc/shadow                 # View encrypted passwords (only root can view)
```

### 🧠 Notes:
- `/etc/passwd`: Stores basic user info like username, UID, GID, shell, home dir.
- `/etc/group`: Stores group info.
- `/etc/shadow`: Stores hashed passwords and password aging info (readable only by root).

---

## 👤 Default UID Values:

| RHEL Version | First UID Assigned |
|--------------|--------------------|
| RHEL 6.x and older | `500` |
| RHEL 7.x and newer | `1000` |

---

## 🔑 SSH Login with `.pem` Key (Public Key Auth)

### 🔹 Steps to Enable Key-based Login for a New User (e.g., `devuser`)

```bash
sudo mkdir /home/devuser/.ssh
sudo cp /home/ec2-user/.ssh/authorized_keys /home/devuser/.ssh/
sudo chown -R devuser:devuser /home/devuser/.ssh
sudo chmod 700 /home/devuser/.ssh
sudo chmod 600 /home/devuser/.ssh/authorized_keys
```

### 🔹 SSH from Local:
```bash
ssh -i "your-key.pem" devuser@your-ec2-public-ip
```

---

## 🔒 Set or Change Passwords with `passwd`

### 🔹 As Root:
```bash
sudo passwd nagesdevops
```

### 🔹 As the User:
```bash
passwd
```

Prompts:
```
Current password:
New password:
Retype new password:
```

---

## ⏳ Password Expiry with `chage`

### 🔹 Set password expiration for a user:
```bash
sudo chage nagesdevops
```

You’ll be prompted to enter:
- Minimum password age
- Maximum password age
- Password expiration warning, etc.

### 🔹 View updated values:
```bash
cat /etc/shadow
```

---

## 🥱 Remove a Package

### 🔹 Using YUM or DNF:
```bash
sudo yum remove tree -y       # RHEL 7 or earlier
sudo dnf remove tree -y       # RHEL 8 and newer
```

---

## 👥 Group Management

### 🔹 Create a Group:
```bash
sudo groupadd devops
```

- Groups info is stored in: `/etc/group`
- Each user also has a default group created with their name.

---

## ➕ Add a User to a Group with `usermod`

```bash
sudo usermod -aG devops nagesdevops
```

### 🔹 Verify Group Members:
```bash
sudo lid -g devops
```
> If `lid` is not installed, install it:
```bash
sudo yum install libuser -y
```

---

## 💼 Check User's Group Membership

```bash
id nagesdevops          # Shows UID, GID, and group membership
groups nagesdevops      # Lists all groups the user belongs to
```

---

## 📌 Summary Table

| Task                         | Command                                      |
|------------------------------|----------------------------------------------|
| Create User                  | `sudo useradd nagesdevops`                       |
| Set Password (root)          | `sudo passwd nagesdevops`                        |
| Change Password (self)       | `passwd`                                     |
| View User Info               | `cat /etc/passwd`                            |
| View Group Info              | `cat /etc/group`                             |
| View Password Info           | `cat /etc/shadow`                            |
| Create Group                 | `sudo groupadd devops`                       |
| Add User to Group            | `sudo usermod -aG devops nagesdevops`           |
| Check User's Groups          | `id nagesdevops` / `groups nagesdevops`             |
| Check Group Members          | `sudo lid -g devops`                         |
| Set Password Expiry          | `sudo chage nagesdevops`                         |
| Remove a Package             | `sudo yum/dnf remove tree -y`               |
| Enable SSH via .pem          | Set `.ssh/authorized_keys` for user         |


