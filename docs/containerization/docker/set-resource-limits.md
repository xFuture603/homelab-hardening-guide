# Set Resource Limits

Without proper limits, containers can consume excessive CPU, memory, or process
resources, potentially degrading system performance or even causing outages.  
To avoid this, define resource constraints directly in your `compose.yaml`
configuration.

## Configuration

Below is a simplified example using a shared configuration block
(using YAML anchors) to apply limits consistently across multiple containers:

```yaml
x-limits: &limits
  mem_limit: 1000m
  pids_limit: 200
  cpus: "2"
  logging:
    options:
      max-size: "10m"
      max-file: "3"

services:
  web:
    <<: *limits
  database:
    <<: *limits
```

!!! tip

    You can use YAML anchors and aliases to create re-usable code blocks.

By enforcing these limits, you ensure that individual containers cannot
monopolize system resources, which helps maintain stability and makes resource
usage more predictable.

### Sources

- [Fragments in Docker Compose][docker-compose-fragments]
- [Docker ulimits][docker-ulimits]

[docker-compose-fragments]: https://docs.docker.com/reference/compose-file/fragments/
[docker-ulimits]: https://docs.docker.com/reference/cli/docker/container/run/#set-ulimits-in-container---ulimit
