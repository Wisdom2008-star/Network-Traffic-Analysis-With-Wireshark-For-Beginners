# Exercise 16 - Capturing TLS Traffic

This guide walks through capturing TLS traffic in Wireshark — the encryption layer that sits underneath HTTPS.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Any regular HTTPS website — almost every modern site works for this

## Steps

### 1. Pick your network

Open Wireshark and choose the network connection you're using (Wi-Fi or Ethernet).

### 2. Start capturing

Click the blue shark-fin button to start recording.

### 3. Filter for TLS only

Type this in the filter bar and hit Enter:

```
tls
```

### 4. Visit a website

While it's still recording, visit any regular website starting with `https://`. Since almost everything today uses HTTPS, this should generate TLS traffic right away.

### 5. Stop recording

Click the red square button once you've seen some TLS packets show up.

### 6. Save it

`File → Save As`, and save it into your `captures/` folder.

## What you should see

A list of packets showing **TLSv1.2** or **TLSv1.3** in the Protocol column, with Info like:

| Info |
|---|
| Client Hello |
| Server Hello |
| Application Data |

The Hello messages happen right at the start of the connection. Everything after that shows up as "Application Data" — this is the actual encrypted content, which Wireshark can't read without the encryption keys.

## If nothing shows up

- Make sure you picked the right network interface in step 1
- Make sure the capture is actually running (the shark-fin button should look "pressed down" while active)
- Visit a site while the capture is running, not before
