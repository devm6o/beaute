+++
title = 'Inspecting TLS Certificates with openssl'
date = 2026-02-08T09:00:00Z
description = 'A few openssl one-liners for checking who issued a certificate and when it expires.'
tags = ['linux', 'security', 'tls']
+++

When a site's certificate looks wrong, `openssl` can tell you exactly what the
server is sending.

## See the certificate a server presents

```bash
openssl s_client -connect example.com:443 -servername example.com </dev/null 2>/dev/null \
  | openssl x509 -noout -subject -issuer -dates
```

`-servername` sends SNI, so you get the certificate for that host name rather
than the server's default one.

## Check the names it covers

```bash
openssl s_client -connect example.com:443 -servername example.com </dev/null 2>/dev/null \
  | openssl x509 -noout -ext subjectAltName
```

## Will it expire soon?

`-checkend` takes a number of seconds. This checks the next 30 days:

```bash
openssl x509 -in cert.pem -noout -checkend 2592000 \
  && echo "OK" || echo "Expires within 30 days"
```

## Show the whole chain

```bash
openssl s_client -connect example.com:443 -servername example.com -showcerts </dev/null
```

> NOTE: A missing intermediate certificate is one of the most common TLS
> problems. Browsers often hide it, but command-line clients will fail.
