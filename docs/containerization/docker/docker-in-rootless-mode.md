# Run Docker in Rootless Mode

Rootless mode allows both the Docker daemon and containers to run under an
unprivileged user account. This significantly reduces the impact of a container
breakout, because even if an attacker escapes a container, they inherit non-root
permissions on the host. This differs from `userns-remap`, where the Docker
daemon still runs as root.

Under the hood, rootless mode operates inside a user namespace. It does not rely
on `setuid` binaries or elevated kernel capabilities, apart from `newuidmap` and
`newgidmap`, which are required so the namespace can utilize a range of
subordinate user/group IDs.

!!! warning

    Running Docker in rootless mode require some prerequisites before it will
    work. Changing your configuration to a rootless setup, may break your
    currently running configuration!

You can get a good guide to use the rootless mode on the official
[Docker documentation][docker-rootless-mode].

!!! tip

    If it is possible, you can also consider running [`Podman`][podman-docs],
    since it is designed to run rootless by default.

## Sources

- [Docker Rootless Mode][docker-rootless-mode]
- [Podman Documentation][podman-docs]

[docker-rootless-mode]: https://docs.docker.com/engine/security/rootless/
[podman-docs]: https://podman.io/docs
