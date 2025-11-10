# HTTP Strict Transport Security

The `HTTP Strict-Transport-Security response header` (HSTS)
informs browsers that the host should only be accessed using `HTTPS`, and that
any future attempts to access it using `HTTP` should automatically be upgraded
to `HTTPS`. Additionally, on future connections to the host, the browser will
not allow the user to bypass secure connection errors, such as an invalid
certificate. `HSTS` identifies a host by its domain name only.

## What Problem does HSTS Solve?

HSTS helps protect against several common attack scenarios:

- **Users manually entering `http://` URLs:** The browser will automatically
  redirect to `HTTPS`.

- **Web applications containing accidental HTTP links:** Requests are rewritten
  to `HTTPS` before leaving the browser.

- **Certificate warning bypass (MITM attacks):** Browsers will not allow users
  to click through certificate warnings when `HSTS` is active.

In short: It will reduces the risk of **man-in-the-middle attacks** and protects
against accidental unencrypted requests.

## Configuration

More information and how to configure `HSTS` can be found in the
[Mozilla Resources for Developers][mozilla-hsts].

### Sources

[Mozilla Strict-Transport-Security header][mozilla-hsts]

[mozilla-hsts]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Strict-Transport-Security
