# Overview

This section covers practical approaches to running Docker more securely — from
restricting container capabilities, to managing secrets, to reducing the impact
of a compromised container.

!!! warning

    Docker security is not something you can “set and forget.”
    Container environments are dynamic, and new vulnerabilities or image updates
    can change behavior over time. Always validate changes in a test environment
    before applying them to critical services.

## General Useful Resources

- [Docker Security Cheat Sheet][owasp-docker-cheat-sheet]
- [Docker Bench for Security][docker-bench-security]

[owasp-docker-cheat-sheet]: https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html
[docker-bench-security]: https://github.com/docker/docker-bench-security
