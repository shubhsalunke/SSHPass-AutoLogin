# SSH Auto Login Setup Using sshpass

## Overview

This guide helps you configure passwordless-style SSH login using `sshpass` and SSH aliases.

After setup, you can connect to multiple Linux VMs directly using simple commands like:

```bash
vm1
vm2
vm3
```

without manually entering passwords every time.

---

# Prerequisites

* Ubuntu/Linux system
* SSH access to remote VMs
* Username and password for each VM
* Internet connection

---

# Step 1: Install sshpass

## Run on Main VM / Local Machine

Example:

```bash
lab-user@Shubh:~$
```

Update package list:

```bash
sudo apt update
```

Install sshpass:

```bash
sudo apt install sshpass -y
```

Verify installation:

```bash
sshpass -V
```

---

# Step 2: Configure SSH Hosts

## Run on Main VM / Local Machine

Open SSH config file:

```bash
nano ~/.ssh/config
```

Add VM details:

```text
Host 1
    HostName lab-as-1
    User lab-1

Host 2
    HostName lab-as-2
    User lab-2

Host 3
    HostName lab-as-3
    User lab-2
```

## Explanation

| Parameter | Description           |
| --------- | --------------------- |
| Host      | Shortcut name         |
| HostName  | Remote server address |
| User      | SSH username          |

Save file:

```text
CTRL + X
Y
ENTER
```

---

# Step 3: Create SSH Auto Login Aliases

## Run on Main VM / Local Machine

Open bash configuration file:

```bash
nano ~/.bashrc
```

Add aliases at bottom:

```bash
alias vm1="sshpass -p 'password1' ssh 1"
alias vm2="sshpass -p 'password2' ssh 2"
alias vm3="sshpass -p 'password3' ssh 3"
```

## Example

```bash
alias vm1="sshpass -p 'shubh' ssh 1"
alias vm2="sshpass -p 'admin123' ssh 2"
alias vm3="sshpass -p 'ubuntu123' ssh 3"
```

Save file:

```text
CTRL + X
Y
ENTER
```

---

# Step 4: Reload Bash Configuration

## Run on Main VM / Local Machine

Apply changes:

```bash
source ~/.bashrc
```

---

# Step 5: Connect to Servers

## Run on Main VM / Local Machine

Connect to VM 1:

```bash
vm1
```

Connect to VM 2:

```bash
vm2
```

Connect to VM 3:

```bash
vm3
```

---

# Example Workflow

## Connect to First VM

```bash
vm1
```

## Connect to Second VM

```bash
vm2
```

## Connect to Third VM

```bash
vm3
```

---

# Verify SSH Config

## Run on Main VM / Local Machine

Check configured hosts:

```bash
cat ~/.ssh/config
```

Expected output:

```text
Host 1
    HostName lab-as-1
    User lab-user-1
```

---

# Verify Aliases

## Run on Main VM / Local Machine

Check configured aliases:

```bash
alias
```

Expected output:

```bash
alias vm1='sshpass -p '\''shubh'\'' ssh 1'
```

---

# Troubleshooting

## sshpass Command Not Found

Run:

```bash
sudo apt install sshpass -y
```

---

## Alias Not Working

Reload bashrc:

```bash
source ~/.bashrc
```

---

## Permission Denied

Verify:

* Username
* Password
* SSH server accessibility

Test manually:

```bash
ssh 1
```

---

# Security Note

Using passwords inside `.bashrc` is not secure because passwords are stored in plain text.

Recommended production approach:

* SSH Key Authentication
* `ssh-keygen`
* `ssh-copy-id`

---

# Recommended Alternative (Secure Method)

## Run on Main VM / Local Machine

Generate SSH Key:

```bash
ssh-keygen -t ed25519
```

Copy Key to Server:

```bash
ssh-copy-id 1
```

Connect Securely:

```bash
ssh 1
```

This removes password prompts securely.

---

# Technologies Used

* Ubuntu Linux
* OpenSSH
* sshpass
* Bash aliases
