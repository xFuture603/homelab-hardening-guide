# Restrict Privileges and Capabilities

By default, Docker containers run with a restricted set of Linux capabilities.
These capabilities control what a container can do on the host system.
Granting additional privileges makes the container more powerful—but also
significantly increases your security risk.

## To stay safe

Do not use `--privileged`. This flag gives the container almost the same level
of access as the host. If the container is compromised, an attacker could gain
near-full control of your system.

Avoid adding capabilities like `SYS_ADMIN`. This particular capability is
extremely powerful and effectively removes many isolation boundaries between the
container and the host.

Grant only the minimal privileges required for the container to work.
Don’t give more permissions “just in case.”

### Sources

[Docker Container Privileges][docker-container-privileges]

[docker-container-privileges]: https://docs.docker.com/reference/cli/docker/container/run/#privileged
