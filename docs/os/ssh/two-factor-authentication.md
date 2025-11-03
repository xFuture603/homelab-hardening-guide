# Use Two Factor Authentication to secure SSH

You can also secure your SSH with a two factor code. There are certainly other
methods and variants (even better ones) for solving this, but in this
documentation we use [libpam-google-authenticator][google-authenticator].

Google Authenticator implements time-based one-time passwords (TOTP), where each
authentication code is generated from a shared secret and is only valid for a
short window (typically 30 seconds). Even if an attacker manages to obtain a
user's password, they would still be unable to authenticate without access to
the device that generates the TOTP. Enabling Google Authenticator therefore adds
a second factor to the login process, significantly strengthening the overall
security of SSH access.

## Requirements

- Correctly configured NTP service for time synchronization

## Configuration

!!! info

    Some commands may differ depending on which package manager is used.

### Install the Google Authenticator PAM module

```bash
sudo apt-get install libpam-google-authenticator -y
```

### Generate Authentication Tokens

The token generation has to be done for each user in the system.
Run the following command for the user to generate the 2FA token:

```bash
google-authenticator
```

You will be prompted with several configuration questions. Review each carefully
to ensure the setup matches your preferences. The following responses are
recommended for most environments:

- **Use time-based tokens:** `y`
- **Update the `~/.google_authenticator` file:** `y`
- **Disallow reuse of authentication tokens:** `y`
- **Allow token reuse in a short time window:** `n`
- **Enable rate limiting to slow brute-force attempts:** `y`

During this process, a QR code and a corresponding secret key will be displayed
in the terminal. Scan the QR code using an authenticator application such as
Google Authenticator, Authy, or Aegis. Alternatively, you can manually enter the
provided secret key into your authenticator app.

### Configure PAM (Pluggable Authentication Modules)

```bash
sudo vim /etc/pam.d/sshd
```

Add the following line at the top of the file, **before** any other
authentication-related lines:

```bash
auth required pam_google_authenticator.so
```

### Configuring SSH to Require Two-Factor Authentication

!!! danger

    Enabling two-factor authentication for SSH modifies the login flow. If your
    SSH client, PAM configuration, or authenticator setup is incorrect, you
    may lose access to your system.

We now need to configure the SSH daemon to use PAM for authentication.
This ensures that the PAM configuration, which includes our Google Authenticator
integration, is enforced.

Edit the SSH configuration file:

!!! note

    Before applying these changes on a production machine, test them on a
    second user account or in a separate terminal session.
    Keep at least one alternative access method available (local console, IPMI,
    Proxmox/ESXi console, or cloud provider recovery shell) to recover in case
    your SSH login fails.

```bash
sudo vim /etc/ssh/sshd_config
```

Add or modify the following lines to:

```
ChallengeResponseAuthentication yes
PasswordAuthentication no
UsePAM yes
```

### Restart the SSH service

Apply your changes:

```bash
sudo systemctl restart ssh
```

### Sources

- [Google Authenticator Libpam][google-authenticator]

[google-authenticator]: https://github.com/google/google-authenticator-libpam
