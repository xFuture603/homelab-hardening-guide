# Docker Socket Proxy

The Docker socket (`/var/run/docker.sock`) is a Unix domain socket used to
communicate directly with the Docker daemon. The Docker daemon is responsible
for managing containers, images, networks, and volumes. Any process that can
access this socket can issue Docker API commands — effectively granting it
full administrative control over the host’s container environment.

Because of this, mounting the Docker socket inside a container grants that
container the same level of control as the root user on the host.
This is commonly done for convenience (f.e Portainer),
but it introduces significant security risk.

If the Docker socket is mounted inside a container, and that container is
compromised, an attacker can:

- Start, stop, modify, or delete any container
- Deploy malicious containers with elevated privileges
- Escape the container and gain direct access to the host system

Instead of exposing the Docker socket directly, we can place a
Docker Socket Proxy between the container and the Docker daemon.
The proxy intercepts API requests and allows administrators to
grant only the minimal set of permissions required for each container.

## Advantages of Using a Docker Socket Proxy

- **Reduced Attack Surface:** Applications only receive the permissions they
  require, not full administrative control.
- **Controlled Access:** Only approved containers interact with the Docker API.
- **Safer Automation:** Enables functionality such as container updates or
  monitoring without exposing the full daemon.

## Configuration

Below is a `compose.yaml` that deploys a `docker-socket-proxy` with the popular
service `Portainer`:

???+ example "compose.yaml"

    ```yaml
    ---

    services:
      socket-proxy:
        image: lscr.io/linuxserver/socket-proxy:<latest_image_version>
        container_name: socket-proxy
        restart: unless-stopped
        environment:
          - CONTAINERS=1    # Allow listing and managing containers
          - SERVICES=1      # Allow listing and managing services
          - NETWORKS=1      # Allow listing networks
          - VOLUMES=1       # Allow listing volumes
          - EXEC=0          # /exec & /containers/{id}/exec
          - SYSTEM=0        # Block the system-level API access
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock:ro
        read_only: true
        tmpfs:
          - /run
        networks:
          - proxy-network

      portainer:
        image: portainer/portainer-ce:<latest_image_version>
        container_name: portainer
        command: -H tcp://socket-proxy:2375 --tlsskipverify
        restart: unless-stopped
        ports:
          - "9000:9000"  # The Portainer Web UI
          - "9443:9443"  # Secure Portainer Web UI
        volumes:
          - portainer_data:/data
        networks:
          - proxy-network
        depends_on:
          - socket-proxy

    networks:
      proxy-network: # This network needs to already exist
        external: true

    volumes:
      portainer_data:
    ```

!!! info

    Check the [`LinuxServer`][linuxserver-socket-proxy] repository for all
    available parameters.

Before starting the project, we need to create the external network:

```bash
docker network create proxy-network
```

To start the containers, go in the directory where the `compose.yaml` is stored
and execute:

```bash
docker compose -f compose.yaml up -d
```

After that you can access Portainer from your Browser. If you've tested this
locally, it would be:

```md
http://localhost:9000 (for HTTP)
https://localhost:9443 (for HTTPS)
```

### Sources

[Linuxserver docker-socket-proxy][linuxserver-socket-proxy]

[linuxserver-socket-proxy]: https://github.com/linuxserver/docker-socket-proxy?tab=readme-ov-file&ref=paulsblog.dev#parameters
