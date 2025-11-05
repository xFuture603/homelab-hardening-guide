# Overview

This section covers practical approaches to running Docker more securely — from
restricting container capabilities, to managing secrets, to reducing the impact
of a compromised container. We will also cover a variety of tips for hardened
container images.

!!! warning

    Docker security is not something you can “set and forget.”
    Container environments are dynamic, and new vulnerabilities or image updates
    can change behavior over time. Always validate changes in a test environment
    before applying them to critical services.

## Understanding Potential Attack Vectors

- **Insecure Exposure:** Exposing the web interfaces of containerized
  applications without proper authentication or network restrictions can make
  them easy targets for attackers.

- **Untrusted or Malicious Images:** Running container images from unverified
  sources, such as third-party repositories with limited transparency about
  authorship or source code, introduces potential security risks.

- **Supply Chain Attacks:** Even trusted images may contain dependencies with
  vulnerabilities or malicious code, creating a vector for compromise within the
  container.

- **Lateral Movement:** If a container or host is compromised, attackers can
  leverage it to move laterally within the network, potentially gaining access
  to other hosts or services.

- **Application Vulnerabilities:** All containerized applications may contain
  bugs or security flaws. Unpatched vulnerabilities can be exploited to escalate
  privileges or disrupt services.

And certainly a few more.

Since we are mostly talking about our homelab, we will focus more on docker
itself and not so much on hardening container images, since you presumably
consume more images from external sources then you create on your own.

## General Useful Resources

- [Docker Security Cheat Sheet][owasp-docker-cheat-sheet]
- [Docker Bench for Security][docker-bench-security]

[owasp-docker-cheat-sheet]: https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html
[docker-bench-security]: https://github.com/docker/docker-bench-security
