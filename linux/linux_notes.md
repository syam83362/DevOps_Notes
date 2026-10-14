# Linux Basics

## 1. Linux Filesystem Structure

Linux starts from the **root directory `/`**.

```
/
├── home    → Users' files
├── etc     → Configuration files
├── var     → Logs and application data
├── tmp     → Temporary files
├── usr     → Programs and utilities
├── bin     → Essential commands
├── opt     → Optional/third-party applications
└── root    → Root user's home directory
```

### Important directories

| Directory | Purpose |
| --- | --- |
| `/home` | Normal users' personal files |
| `/etc` | System and application configuration |
| `/var` | Logs, databases, application data, etc. |
| `/tmp` | Temporary files |
| `/usr` | Installed programs and utilities |
| `/bin` | Essential system commands |
| `/opt` | Optional/third-party applications |
| `/root` | Home directory of the root user |
| `/var/log` | System and application logs |

---

# 2. File Permissions — chmod

Linux permissions are based on three permissions:

| Permission | Symbol | Number |
| --- | --- | --- |
| Read | `r` | `4` |
| Write | `w` | `2` |
| Execute | `x` | `1` |

### Permission calculation

```
rwx = 4 + 2 + 1 = 7
rw- = 4 + 2     = 6
r-x = 4 + 1     = 5
r-- = 4         = 4
```

Permissions are assigned to:

```
Owner   Group   Others
```

### chmod 755

```bash
chmod 755 file
```

Means:

```
Owner  → rwx → 7
Group  → r-x → 5
Others → r-x → 5
```

So:

```
755 = rwxr-xr-x
```

### chmod 644

```bash
chmod 644 file
```

Means:

```
Owner  → rw- → 6
Group  → r-- → 4
Others → r-- → 4
```

So:

```
644 = rw-r--r--
```

### Common examples

```bash
chmod 755 script.sh
chmod 644 config.txt
```

**Remember:**

```
4 = Read
2 = Write
1 = Execute
```

---

# 3. sudo vs root

### Normal user

Example:

```
Syam
```

A normal user does not have unrestricted access to the system.

### sudo

`sudo` allows a normal user to execute **one command with elevated privileges**.

Example:

```bash
sudo systemctl restart nginx
```

Only that command runs with elevated privileges.

### sudo -i

```bash
sudo -i
```

Opens a **root shell**.

After this, commands are executed as root until you exit.

```bash
exit
```

### Root

`root` is the Linux **superuser** with the highest level of privileges.

```
Normal User
     ↓
   sudo
     ↓
Elevated privilege
     ↓
    root
```

---

# 4. Processes

A **process** is a running instance of a program.

### ps

```bash
ps
```

Shows a snapshot of processes associated with the current shell/session.

### ps aux

```bash
ps aux
```

Shows a detailed snapshot of **running processes across the system**.

### top

```bash
top
```

Shows processes in a **live, continuously updating view**.

Useful for checking:

- CPU usage
- Memory usage
- Running processes
- Process IDs (PID)

---

# 5. Killing Processes

Every running process has a **PID (Process ID)**.

Example:

```
PID = 1234
```

### SIGTERM

```bash
kill 1234
```

Sends `SIGTERM`.

Meaning:

> "Please stop gracefully."
> 

The process gets a chance to clean up before exiting.

### SIGKILL

```bash
kill -9 1234
```

Sends `SIGKILL`.

Meaning:

> "Terminate immediately."
> 

The process cannot catch or ignore `SIGKILL`.

### Remember

```
kill PID
    ↓
SIGTERM
    ↓
Graceful stop

kill -9 PID
    ↓
SIGKILL
    ↓
Immediate termination
```

Use `kill -9` only when a normal `kill` does not work.

---

# 6. systemd — Managing Services

**systemd** is the service manager commonly used by modern Linux distributions.

It manages background services such as:

- Nginx
- MySQL
- Redis
- SSH
- Docker

Example:

```bash
systemctl status nginx
```

---

## Service Commands

### Check status

```bash
sudo systemctl status nginx
```

### Start

```bash
sudo systemctl start nginx
```

Starts the service.

### Stop

```bash
sudo systemctl stop nginx
```

Stops the service.

### Restart

```bash
sudo systemctl restart nginx
```

Stops and starts the service again.

Useful after configuration changes.

---

# 7. Enable vs Disable

These are related to what happens when the server **boots/restarts**.

### Enable

```bash
sudo systemctl enable nginx
```

Configures the service to **start automatically during boot**.

### Disable

```bash
sudo systemctl disable nginx
```

Prevents the service from **starting automatically during boot**.

### Important

`start` and `enable` are different.

```
start
→ Start the service NOW

enable
→ Start the service automatically on future boots
```

Similarly:

```
stop
→ Stop the service NOW

disable
→ Prevent automatic start on future boots
```

---

# 8. Linux Logs

Logs help us understand what happened when a service or application has a problem.

### /var/log

```
/var/log
```

Contains many Linux and application log files.

---

# 9. journalctl

`journalctl` is used to view logs collected by **systemd's journal**.

### View service logs

```bash
sudo journalctl -u nginx
```

Shows logs for the `nginx` service.

### Last 20 log entries

```bash
sudo journalctl -u nginx -n 20
```

Shows the latest 20 entries.

### Follow live logs

```bash
sudo journalctl -u nginx -f
```

Shows logs continuously as they arrive.

- `f` = **follow**

---

# 10. grep — Search Logs

`grep` searches for specific text.

### Search for error

```bash
sudo journalctl -u nginx | grep error
```

### Case-insensitive search

```bash
sudo journalctl -u nginx | grep -i error
```

- `i` = ignore case.

So it can find:

```
error
Error
ERROR
```

### Search for failed

```bash
journalctl -u myapp | grep -i failed
```

---

# 11. tail — Show Last Lines

`tail` shows the last lines of output.

### Last 10 lines

```bash
sudo journalctl -u nginx | tail
```

### Last 20 lines

```bash
sudo journalctl -u nginx | tail -20
```

### Useful commands

```bash
tail file.log
tail -20 file.log
tail -f file.log
```

`tail -f` is useful for watching a log file live.

---

# 12. less — Read Large Output

`less` allows you to scroll through large amounts of output.

Example:

```bash
journalctl -u nginx | less
```

Useful when the output is too large to read directly in the terminal.

---

# 13. Useful Linux Log Tools

```
journalctl
    ↓
View systemd/service logs

grep
    ↓
Search for specific text

tail
    ↓
View the last lines

less
    ↓
Scroll through large output
```

### Example — Debugging a service

```bash
sudo journalctl -u nginx | grep -i error
```

Or:

```bash
sudo journalctl -u nginx -n 20
```

Or live:

```bash
sudo journalctl -u nginx -f
```

---

# 14. APT — Linux Package Manager

`apt` is a package manager used by **Debian/Ubuntu-based Linux systems**.

It is used to:

- Install software
- Remove software
- Update package information
- Upgrade installed packages
- View package information

---

## apt update

```bash
sudo apt update
```

Refreshes the local package information from configured repositories.

**Important:** It does not upgrade your installed packages.

---

## apt upgrade

```bash
sudo apt upgrade
```

Upgrades installed packages to newer available versions.

---

## apt install

```bash
sudo apt install nginx
```

Installs a package.

General syntax:

```bash
sudo apt install <package>
```

---

## apt remove

```bash
sudo apt remove nginx
```

Removes a package.

General syntax:

```bash
sudo apt remove <package>
```

---

## apt show

```bash
apt show nginx
```

Shows information about a package.

For example:

- Version
- Description
- Dependencies
- Package size

---

## Check Installed Packages

```bash
apt list --installed
```

Shows installed packages.

To show only the first few results:

```bash
apt list --installed | head
```

---

## Check Upgradable Packages

```bash
apt list --upgradable
```

Shows installed packages for which newer versions are available.

---

# 15. APT Workflow

A common workflow is:

```bash
sudo apt update
```

↓

Refresh package information

```bash
apt list --upgradable
```

↓

Check what can be upgraded

```bash
sudo apt upgrade
```

↓

Upgrade installed packages

---

# Quick Revision

## Filesystem

```
/home → User files
/etc  → Configuration
/var  → Logs & application data
/tmp  → Temporary files
/usr  → Programs & utilities
/bin  → Essential commands
/opt  → Optional applications
/root → Root user's home
```

## Permissions

```
r = 4
w = 2
x = 1

755 = rwxr-xr-x
644 = rw-r--r--
```

## Privileges

```
sudo     → One command with elevated privileges
sudo -i  → Open root shell
root     → Highest-privilege user
```

## Processes

```
ps       → Process snapshot
ps aux   → All running processes
top      → Live process monitoring
kill PID → Graceful termination (SIGTERM)
kill -9  → Immediate termination (SIGKILL)
```

## Services

```
systemctl status
systemctl start
systemctl stop
systemctl restart
systemctl enable
systemctl disable
```

## Logs

```
/var/log        → Log files
journalctl      → systemd logs
grep            → Search text
tail            → Last lines
less            → Scroll large output
```

## Packages

```
apt update              → Refresh package information
apt install <package>   → Install
apt remove <package>    → Remove
apt show <package>      → Package information
apt list --installed    → Installed packages
apt list --upgradable   → Packages with updates
apt upgrade             → Upgrade packages
```
