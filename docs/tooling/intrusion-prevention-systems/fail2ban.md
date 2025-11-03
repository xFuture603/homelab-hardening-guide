# Fail2Ban

Persistent brute-force login attempts are one of the most common attacks against
publicly exposed SSH services. **Fail2ban** helps defend your server by
monitoring authentication logs and automatically banning IP addresses that
exhibit suspicious or repetitive failed login behavior. This reduces the attack
surface significantly and slows down automated intrusion attempts.

!!! warning

    Fail2ban relies on system logs. If your system’s logging is disabled,
    heavily customized, or rotated aggressively, Fail2ban may fail to detect
    malicious activity.
    Always verify that your logfiles are being written correctly.

## Configuration

Install Fail2ban:

```bash
sudo apt install fail2ban -y
```

Fail2ban organizes its configuration like this:

- `/etc/fail2ban/` – Main configuration directory
- `/etc/fail2ban/fail2ban.conf` – Core Fail2ban settings
- `/etc/fail2ban/jail.conf` – Default jail definitions
  (should **not** be edited directly)
- `/etc/fail2ban/jail.local` – Global overrides for jail settings
- `/etc/fail2ban/jail.d/` – Directory for modular, service-specific `.local`
  files (e.g., `sshd.local`, `nginx.local`)
- `/etc/fail2ban/filter.d/` – Filter definitions used to detect malicious
  activity
- `/etc/fail2ban/action.d/` – Action definitions that execute bans,
  notifications, etc.

!!! info

    Never modify the `.conf` files directly. Instead, create `.local`
    files that override the default settings. `fail2ban.local` overrides
    `fail2ban.conf` and `jail.local` overrides `jail.conf`.

After installing `fail2ban` you can create a jail for your desired service
such as `sshd`, `dovecot` or `proftpd` for example.

You can create separate `.local` files under `/etc/fail2ban/`:

```bash
/etc/fail2ban/jail.d/
├── sshd.local
├── dovecot.local
├── proftpd.local
```

You can find some good configuration examples in the official fail2ban jail.conf
on their [GitHub][jail-conf].

Below is an example for the ssh daemon (sshd):

```ini
[sshd]
enabled = true
port = ssh,22
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
```

### Starting and enabling Fail2ban

```bash
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
sudo systemctl status fail2ban
sudo fail2ban-client status
```

You can also view specific information for a given jail, for example:

```bash
sudo fail2ban-client status sshd
```

### Reloading Fail2Ban

```bash
sudo systemctl reload fail2ban
sudo systemctl status fail2ban
```

More commands for the `fail2ban-client` or the `fail2ban-server` can be found on
the `man` pages.

### Sources

- [Fail2Ban Jail Configuration][jail-conf]

[jail-conf]: https://github.com/fail2ban/fail2ban/blob/master/config/jail.conf
