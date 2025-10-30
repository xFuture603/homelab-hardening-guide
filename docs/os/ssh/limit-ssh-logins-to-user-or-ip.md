# Limit SSH Logins to allowed Users or IP Addresses

Controlling SSH access through the server configuration provides an additional
ayer of defense by explicitly allowing only authorized accounts from trusted
sources.

## Configuration

### Add `AllowUsers` to whitelist certain users

Open your SSH configuration file:

```bash
sudo vim /etc/ssh/sshd_config
```

```bash
AllowUsers <your_username>
```

The `AllowUsers` directive functions as a whitelist. Only users listed here will
be permitted to authenticate, and all other accounts are implicitly denied.

### Restrict access to a user from a specific IP address

```bash
AllowUsers <your_username>@<your_ip_address>
```

When specifying a user with an IP, access is restricted to that **exact user-IP
combination**, overriding a more general AllowUsers rule for the same account.

To allow multiple user-IP combinations, list them separated by spaces:

```bash
AllowUsers <your_username>@<your_ip_address> <your_other_username>@<your_other_ip_address>
```

### Restart the SSH service

Apply your changes:

```bash
sudo systemctl restart ssh
```

### Verify access restrictions

Test SSH connections with both authorized and unauthorized accounts and
source IPs to confirm that the restrictions are correctly enforced.
