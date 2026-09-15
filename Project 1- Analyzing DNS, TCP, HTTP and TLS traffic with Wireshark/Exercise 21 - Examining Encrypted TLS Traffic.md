# Exercise 21 - Examining Encrypted TLS Traffic

This guide looks at what encrypted TLS traffic actually looks like once the handshake is done — and why that's expected, not a problem.

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

### 2. Filter for the encrypted data

Type this in the filter bar and hit Enter:

```
tls.record.content_type == 23
```

This shows just the **Application Data** packets — the actual encrypted content, sent after the handshake finishes.

### 3. Click on one of these packets

In the details pane, expand **Transport Layer Security**. You'll see it's labeled as **Application Data**, with no readable fields inside like you saw with Client Hello or Certificate messages.

### 4. Look at the raw bytes

Check the hex pane at the bottom. The bytes should look completely random — no patterns, no readable text. That's what properly encrypted data looks like.

### 5. Try "Follow TLS Stream" (optional)

Right-click one of these packets and choose **Follow → TLS Stream**. Unless Wireshark has been given the session keys separately, this will also show scrambled, unreadable content rather than the actual page.

### 6. Compare against an unencrypted example

If you still have an HTTP capture from Exercise 11, open it side by side. Following an HTTP stream shows plain readable text, while following a TLS stream shows unreadable data — a clear side-by-side example of what encryption actually does.

## What you should see

- Protocol: TLSv1.2 or TLSv1.3
- Info: Application Data
- Hex bytes: random-looking, no visible words or patterns

This is exactly what it should look like. Not being able to read the content is the entire point of TLS — it's protecting whatever's being sent from anyone else watching the traffic.

## If something looks wrong

- You can actually read some content — double check the site is really using HTTPS, or that you're not looking at a Client Hello (SNI is still readable there)
- No Application Data packets at all — the handshake may not have completed, or the connection was very short
- Bytes look like they repeat a pattern — capture a bit more traffic, small captures can look deceptively patterned by chance
