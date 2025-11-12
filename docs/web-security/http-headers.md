# HTTP Headers

HTTP response headers provide another way to improve web security.  
They help prevent common issues such as XSS, clickjacking, and information
disclosure, and enforce secure behavior in browsers.

In a homelab or self-hosted environment, setting proper headers at
your reverse proxy (e.g., Nginx, Traefik, or Caddy) ensures consistent
protection across all hosted and published applications.

## Recommended Headers

For most environments, the following headers
([from the OWASP Cheat Sheet][owasp-http-headers]) offer a strong baseline
configuration:

```md
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload

X-Content-Type-Options: nosniff

Referrer-Policy: strict-origin-when-cross-origin

Permissions-Policy: geolocation=(), camera=(), microphone=()

X-Frame-Options: DENY

Content-Security-Policy: default-src 'self';
```

!!! warning

    Be cautious when applying `Content Security Policy` (CSP).
    Test configurations carefully, as restrictive CSP rules can break
    functionality on some web interfaces.

We won’t cover how to implement HTTP headers in your web server in this guide,
as the configuration steps vary depending on the web server software. Please
refer to the official docs from your used web server application.

### Sources

- [OWASP HTTP Headers Cheat Sheet][owasp-http-headers]
- [Mozilla HTTP Headers][mozilla-http-headers]
- [Mozilla HTTP Observatory (Test your Headers)][mozilla-http-observatory]

[owasp-http-headers]: https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html#security-headers
[mozilla-http-headers]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers
[mozilla-http-observatory]: https://developer.mozilla.org/en-US/observatory
