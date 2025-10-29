# Use SSH Keys for Remote Access

!!! quote

    SSH (Secure Shell) key-based authentication is a security method that uses a
    pair of cryptographic keys to authenticate a user’s identity on a remote
    server. This approach involves generating and storing a public-private key
    pair on your computer and configuring the SSH server to recognize and accept
    these keys. It significantly improves security by reducing the risks
    associated with traditional Password-based Authentication.

### Key Components

SSH keys are created as a pair and saved as plain-text files.
A key pair consists of two parts:

**Public Key**: This part is stored on the SSH server.
It can be safely shared, allowing the server to
recognize your identity when you connect.

**Private Key**: This part is stored on your computer and should be kept secure
at all times. It’s used to authenticate with the server and should never be
shared. The private key should be set with permissions so that no other users
on your computer can read the file.

### Configuration

Some information on how you can generate and use SSH Keys can be found
[here](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server).

!!! danger

    Never share your private SSH key with anyone! If a application or site
    requests your SSH Key (for example various CI/CD solutions), they are
    referring to your public key.

Some of the advantages using SSH keys:

- **Improved Usability:** Eliminates the need to remember or manage
  complex passwords, minimizing human error and the likelihood of
  password-related breaches.
- **Enhanced Security:** Since keys are unique and therefore harder to guess,
  key based authentication is more resistant to brute-force attacks.
- **Reduced Credential Exposure:** If a server is compromised, SSH key
  authentication prevents credential leakage since no reusable passwords are
  stored or transmitted.
- **Enables Secure Automation:** Passwordless authentication allows automated
  systems, scripts, and tools (such as Ansible) to access SSH servers safely
  without manual password entry.

### Sources

- [Configure SSH Key Authentication (DigitalOcean)][ssh-key-based-auth]

[ssh-key-based-auth]: https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
