# Use a Non-Default SSH Port

Changing the SSH service from its default port 22 to a higher, non-standard port
can reduce exposure to automated scans and brute-force attempts, which
constitute the majority of attacks. This measure is not a replacement for strong
authentication or firewall policies, but it adds a minor layer of obscurity. On
top of that you can use the default ssh port for honeypots like `Cowrie` or
something like `endlessh`.

!!! info

    Avoid commonly reused alternatives such as 2222, which are often targeted by
    automated attacks. Choose a high, random port (e.g., 62022) to reduce the
    likelihood of discovery during routine scans.
    No port choice provides complete security. Determined attackers can still
    locate SSH services through comprehensive scanning of the full 65,535 TCP
    port range.

## Configuration

Open the SSH configuration file `/etc/ssh/sshd_config`:

```bash
sudo vim /etc/ssh/sshd_config
```

Edit the `Port` line:

```bash
Port <your_port>
```

### Restart the SSH service

!!! warning

    If you have configured a firewall, make sure to adjust your firewall to
    allow traffic on the new SSH port.

Apply your changes:

```bash
sudo systemctl restart ssh
```

### Verify that SSH daemon is listening on the new port

```bash
ss -an | grep <your_port>
```

### Using the New SSH Port

You can specify the port by invoking the `ssh` command followed by the `-p
<your_port>` option:

```bash
ssh -p <your_port> <your_user>@<your_host>
```

or by creating a `~/.ssh/config` file if you are regulary connecting to your
system.

### Sources

- [Configure your SSH client via config file][ssh-client-config]
- [Cowrie SSH Honeypot][cowrie]
- [Endlessh SSH tarpit][endlessh]

[ssh-client-config]: https://man.openbsd.org/ssh_config
[cowrie]: https://github.com/cowrie/cowrie
[endlessh]: https://github.com/skeeto/endlessh
