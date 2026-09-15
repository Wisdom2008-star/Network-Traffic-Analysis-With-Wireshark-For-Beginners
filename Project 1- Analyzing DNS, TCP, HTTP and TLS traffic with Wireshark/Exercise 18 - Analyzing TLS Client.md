# Exercise 18 - Analyzing TLS Client

This guide covers the Client Hello — the very first message sent when a device starts setting up an encrypted connection.

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

### 2. Filter for the Client Hello

Type this in the filter bar and hit Enter:

```
tls.handshake.type == 1
```

### 3. Click on a Client Hello packet

In the details pane, expand **Transport Layer Security → Handshake Protocol: Client Hello**.

### 4. Look at the key fields

- **Version** — the TLS version being proposed (e.g. TLS 1.2 or 1.3)
- **Cipher Suites** — a list of encryption methods the client is willing to use; the server will pick one
- **Server Name Indication (SNI)** — the actual hostname the client is trying to reach, sent here in plain, readable text

### 5. Notice what's still readable

Even though TLS is about encryption, the Client Hello itself isn't encrypted yet — that's why the SNI hostname can be seen in plain text here. Encryption only kicks in after this handshake finishes.

## What you should see

- Version: TLS 1.2 or TLS 1.3
- A long list of Cipher Suites
- Server Name: (the website's hostname, in plain readable text)

The SNI field is worth remembering — it means even encrypted HTTPS connections reveal which website you're visiting to anyone watching the network, just not what you actually do on that site.

## If something looks wrong

- No Server Name field — some older or unusual connections skip SNI, though this is rare on modern websites
- Can't find "Client Hello" anywhere — make sure your filter is exactly `tls.handshake.type == 1` and that the site actually uses HTTPS
