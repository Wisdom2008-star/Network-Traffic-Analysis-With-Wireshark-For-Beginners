# Exercise 19 - Analyzing TLS Server

This guide covers the Server Hello — the server's reply to a Client Hello, agreeing on how the encrypted connection will work.

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

### 2. Filter for the Server Hello

Type this in the filter bar and hit Enter:

```
tls.handshake.type == 2
```

### 3. Click on a Server Hello packet

In the details pane, expand **Transport Layer Security → Handshake Protocol: Server Hello**.

### 4. Look at the key fields

- **Version** — the TLS version the server has agreed to use
- **Cipher Suite** — just one, chosen from the list the client offered in its Client Hello
- **Session ID** — used to help reconnect faster next time, without redoing the whole handshake

## What's the Difference from Exercise 18?

Exercise 18 was about the **Client Hello** — the client proposing options. This exercise is about the **Server Hello** — the server picking from those options.

| | Client Hello (Exercise 18) | Server Hello (this exercise) |
|---|---|---|
| Who sends it | Your computer | The web server |
| Cipher Suites | A whole list of options | Just one, chosen |
| Includes SNI | Yes, the hostname being requested | No |
| What it tells you | What the client can support | What was actually agreed on |

Together, these two messages settle everything needed before the actual encryption starts.

## What you should see

- Version: matches whatever the client proposed (or a version the server prefers)
- Cipher Suite: one single choice, not a list this time
- Session ID: a string of numbers/letters

## If something looks wrong

- No Server Hello found — the connection may have failed right after the Client Hello; check for FIN or RST packets nearby
- Version doesn't match what the client sent — normal, the server can choose an older supported version if needed
