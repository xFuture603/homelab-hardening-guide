# Ensure GPG Keys are configured

Ensuring that the software installed on your system comes from verified sources
is a common security practice. Most package managers implement GPG key signing,
which allows verification of package integrity during installation. Proper
management of these keys prevents attackers from injecting malicious packages
into your system.

!!! note

    The exact steps for managing GPG keys vary between package managers.
    This section focuses on Ubuntu/Debian-based systems using apt. Other systems
    such as Fedora (`dnf`) or openSUSE (`zypper`) use different commands and
    paths for GPG key management.

## Why GPG Keys Matter

GPG keys are cryptographic tokens used to verify the authenticity of software
packages. When a package is signed, your package manager can check the signature
against the repository’s public key, ensuring that the package has not been
tampered with.

Failing to properly manage GPG keys can lead to:

- Spoofed or malicious packages being installed
- Compromised system integrity
- Security breaches through untrusted software

## Managing GPG Keys on Ubuntu/Debian

### Adding a Repository GPG Key

```bash
sudo mkdir -p /etc/apt/keyrings
wget -O- <url_to_gpg_key> | gpg --dearmor | sudo tee /etc/apt/keyrings/<keyring_name>.gpg
```

### Adding a Repository with the Key

After importing the GPG key, create a new `.list` file under
`/etc/apt/sources.list.d/`:

```bash
echo "deb [signed-by=/etc/apt/keyrings/<keyring_name>.gpg] \
<repository_url> <distribution> <components>" | sudo tee \
/etc/apt/sources.list.d/<file_name>.list
```

This ensures that packages from this repository are only trusted if they match
the specified GPG key.

### Updating and Installing Packages

```bash
sudo apt update
sudo apt install <package_name>
```

Now this guide has several placeholder values. Below I try to explain them:

- `url_to_gpg_key`: The URL where the repository’s GPG key can be downloaded.

- `keyring_name`: A descriptive name for the key file, e.g., `docker.gpg`.

- `repository_url`: The repository’s base URL, e.g.,
  https://download.docker.com/linux/ubuntu.

- `distribution`: The codename of your OS release, e.g., `trixie` for Debian 13.

- `components`: Repository components, e.g., `stable` or `main`.

- `file_name`: The filename for the .list file in `/etc/apt/sources.list.d/`,
  e.g., `docker.list`.

- `package_name`: The actual package you want to install, e.g., `docker-ce`.

## Sources

[APT manpages][apt-manpages]

[apt-manpages]: https://manpages.debian.org/buster/apt/apt.8.en.html
