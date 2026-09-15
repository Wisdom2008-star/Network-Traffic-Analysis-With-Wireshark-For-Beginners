# Exercise 17 - Filtering TLS Traffic

This guide covers narrowing down TLS traffic in Wireshark so it's easier to make sense of.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 16, or a fresh one

## Steps

### 1. Open or start a capture

Open the file from Exercise 16, or start a new capture and visit an HTTPS site.

### 2. Apply the basic TLS filter

Type this in the filter bar and hit Enter:

```
tls
```

### 3. Narrow it down further

A few useful ways to narrow things down:

- Only the very first message a client sends to start the connection:
  ```
  tls.handshake.type == 1
  ```
  (this is the Client Hello)

- Only the server's reply to that:
  ```
  tls.handshake.type == 2
  ```
  (this is the Server Hello)

- Only the handshake messages, skipping the encrypted data that comes after:
  ```
  tls.handshake
  ```

- Traffic to or from one specific server:
  ```
  ip.addr == 172.217.22.46 && tls
  ```

### 4. Try each filter and compare

Notice how `tls` on its own shows everything, including the encrypted Application Data packets, while `tls.handshake` only shows the setup messages before encryption starts.

### 5. Save your filtered view (optional)

`File → Export Specified Packets`, choose "Displayed" under Packet Range, and save it.

## What you should see

With `tls.handshake.type == 1`, you should see one or more **Client Hello** packets. With type `== 2`, the matching **Server Hello** packets. These are the only parts of a TLS connection that aren't encrypted — everything else after them shows up as unreadable Application Data.

## If nothing shows up

- Double check you're on a site that actually uses HTTPS (look for the padlock icon in the browser)
- Make sure the filter bar turned green, not red — red means Wireshark doesn't recognize what you typed
- If using an IP filter, confirm that address actually appeared in your capture
