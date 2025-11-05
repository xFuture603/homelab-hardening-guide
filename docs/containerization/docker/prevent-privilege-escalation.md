# Prevent Privilege Escalation

By default, some container images include tools such as `sudo`, `doas`, or
`setuid/setgid` binaries that can grant additional privileges at runtime. This
creates a potential risk: if a process inside the container is compromised, it
may be able to escalate its privileges.

To reduce this risk, explicitly prevent containers from acquiring new privileges
by enabling the `no-new-privileges` security option.

## Configuration

You can set it in your `compose.yaml` file like this:

```yaml
security_opt:
  - no-new-privileges=true
```

Or via CLI:

```bash
docker run --security-opt=no-new-privileges=true image-name
```

!!! note

    Some applications may require `setuid/setgid` functionality to work
    correctly. Test containers after enabling `no-new-privileges` to confirm
    they behave as expected.
