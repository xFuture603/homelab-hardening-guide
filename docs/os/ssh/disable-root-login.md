# Disable SSH Root Login

Disabling the root login will add an extra layer of security by requiring users
to log in with a regular user with the need to escalate privileges afterwards.

This will also reduces the risk of brute-force attacks on the root account.

!!! warning

    Before disabling root login, ensure that you have created a regular user
    account and granted it sudo privileges. This allows you to perform
    administrative tasks when needed while avoiding direct root access,
    which is considered a security best practice.

## Configuration

### Create a user account

```bash
adduser <your_username>
```

Add the user to the sudo group by modifying the `/etc/group` file:

```bash
sudo vim /etc/group
```

An example entry can look like this:

```bash
sudo:x:27:<your_username>
```

### Edit the `/etc/ssh/sshd_config` file to disable root login

```bash
vim /etc/ssh/sshd_config
```

Search for the option `PermitRootLogin` and set it to:

```md
PermitRootLogin no
```

### Restart the SSH server

```bash
sudo systemctl restart ssh
```
