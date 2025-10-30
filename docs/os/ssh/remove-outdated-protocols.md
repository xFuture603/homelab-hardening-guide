# Remove Outdated and Insecure SSH Protocols

Outdated SSH protocols and weak algorithms can expose your server to
downgrade attacks and other vulnerabilities. Disabling them ensures that all
connections use modern, secure cryptography.

!!! warning

    These settings may prevent older clients from connecting.
    On personal homelabs, this is usually acceptable.
    For shared or production environments, verify that any automated scripts or
    legacy clients support the new algorithms.

## Configuration

### Edit the SSH server configuration

```bash
sudo vim /etc/ssh/sshd_config
```

Specify modern key exchange algorithms, ciphers, and MACs by adding or editing
the following lines:

```bash
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp521,ecdh-sha2-nistp384,ecdh-sha2-nistp256,diffie-hellman-group-exchange-sha256

Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,umac-128@openssh.com
```

- **KexAlgorithms:** Modern key exchange algorithms, including Curve25519 and
  strong ECDH variants, ensure secure session key negotiation.

- **Ciphers:** Strong encryption for data-in-transit. Includes ChaCha20 and
  AES-GCM for authenticated encryption, and AES-CTR as a fallback.

- **MACs:** Message Authentication Codes or
  (Hash-based Message Authentication Code) verify message integrity and prevent
  tampering.

!!! info

    Recommended Ciphers, KexAlgorithms and MACs may differ depending on the
    OpenSSH version used.
    Check the [linked source][mozilla-openssh-settings] for more information.

### Restart the SSH service

Apply your changes:

```bash
sudo systemctl restart ssh
```

### Sources

- [Mozilla's recommended settings for
  OpenSSH configuration][mozilla-openssh-settings]

[mozilla-openssh-settings]: https://infosec.mozilla.org/guidelines/openssh
