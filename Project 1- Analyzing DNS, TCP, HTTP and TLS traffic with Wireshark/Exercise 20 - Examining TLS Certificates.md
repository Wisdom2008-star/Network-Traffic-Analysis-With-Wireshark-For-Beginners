# Exercise 20 - Examining TLS Certificates

This guide covers the certificate a server sends during the TLS handshake, which proves its identity.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 16 or 17

## Steps

### 1. Open your TLS capture in Wireshark

Use a saved capture, or start a fresh one and visit an HTTPS site.

### 2. Filter for the certificate message

Type this in the filter bar and hit Enter:

```
tls.handshake.type == 11
```

This is the **Certificate** message, sent by the server right after its Server Hello.

### 3. Click on the certificate packet

In the details pane, expand **Transport Layer Security → Handshake Protocol: Certificate → Certificates**.

### 4. Open up one certificate

Expand the first certificate listed. Look for:

- **Issuer** — who verified and issued this certificate (a Certificate Authority, like Let's Encrypt or DigiCert)
- **Subject** — who the certificate actually belongs to (should match the website's domain name)
- **Validity** — the "not before" and "not after" dates, showing when the certificate is valid
- **Public Key** — the key used as part of setting up encryption

### 5. Check for more than one certificate

Servers often send a small chain of certificates, not just one — the site's own certificate, plus one or more from the Certificate Authority backing it up. Look through the list to see if more than one is present.

## What you should see

- Subject: matches the website you visited
- Issuer: a recognizable Certificate Authority
- Validity dates: a "not before" in the past and a "not after" in the future

If the dates, subject, or issuer look wrong, that's exactly the kind of thing your browser checks automatically — and would warn you about with a security error if something didn't match up.

## If something looks wrong

- No certificate message found — some connections reuse an earlier session and skip sending the certificate again
- Subject doesn't match the website — could mean the certificate covers multiple domains (check for a "Subject Alternative Name" field) or something is misconfigured
- Can't expand the certificate details — try clicking directly on the certificate bytes in the hex pane instead of the summary line
