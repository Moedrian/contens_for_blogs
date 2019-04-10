# Basic Security Configuration

## Create User

Log in as root user, create a new user then set a password:

```cmd
# adduser username
# passwd username
```

Use the `usermod` command to add the user to the wheel group:

```cmd
# usermod -aG wheel username
```

The command _appends_ `username` to _Group_ wheel in which users have sudo privileges.

## Secure Shell

### Disable root ssh login

1. Use a non-root user to log into ssh, then type the command `sudo vim /etc/ssh/sshd_config` to edit that file.

2. Locate the cursor to `#PermitRootLogin`, uncomment it and set its value to `no`, save and quit.

3. Use `sudo /etc/init.d/sshd restart` to reload it.