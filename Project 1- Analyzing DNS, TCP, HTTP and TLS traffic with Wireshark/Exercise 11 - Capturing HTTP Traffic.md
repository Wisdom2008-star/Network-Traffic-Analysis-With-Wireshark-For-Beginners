# Exercise 11 - Capturing HTTP Traffic

This guide walks through capturing HTTP traffic in Wireshark.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- A plain HTTP website (not HTTPS), since most modern sites use HTTPS and won't show readable HTTP traffic

## Steps

### 1. Pick your network

Open Wireshark and choose the network connection you're using (Wi-Fi or Ethernet).

### 2. Start capturing

Click the blue shark-fin button to start recording.

### 3. Filter for HTTP only

Type this in the filter bar and hit Enter:

```
http
```

### 4. Visit a plain HTTP site

While it's still recording, visit a website that starts with `http://` instead of `https://`. Most modern sites redirect straight to HTTPS, so you may need to search for a site that still uses plain HTTP, or use a test site made for this purpose (like `http://neverssl.com`).

### 5. Stop recording

Click the red square button once you've seen some HTTP packets show up.

### 6. Save it

`File → Save As`, and save it into your `captures/` folder.

## What you should see

A short list of packets showing **HTTP** in the Protocol column, usually with Info like:

<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Capturing%20HTTP%20traffic.png">

| Info |
|---|
| GET / HTTP/1.1 |
| HTTP/1.1 200 OK (text/html) |

The first line is your browser asking for a page. The second is the server sending it back.

## If nothing shows up

- Most sites today use HTTPS by default, which shows up as **TLS**, not **HTTP** — this is expected and doesn't mean the capture failed
- Try `http://neverssl.com`, a site made specifically for testing plain HTTP connections
- Make sure you picked the right network interface in step 1
