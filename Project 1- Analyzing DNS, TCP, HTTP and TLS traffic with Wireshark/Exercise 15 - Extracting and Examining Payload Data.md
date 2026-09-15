# Exercise 15 - Extracting and Examining Payload Data

This guide covers pulling the actual data (the payload) out of a packet, separate from all the header info around it.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 11, 12, 13, or 14

## Steps

### 1. Open your HTTP capture in Wireshark

Use a saved capture, or start a fresh one and visit a plain HTTP site.

### 2. Click on a packet with actual data

Filter for `http.response` and click one that returned a page (status 200 works well).

### 3. Find the payload in the details pane

Below the HTTP section, look for something like **Line-based text data** or **Media Type**. Expanding this shows the actual content that was sent — the HTML, image data, or whatever the response body was.

### 4. View it in the hex pane

Click on that payload section in the details pane. Notice how it highlights a chunk of bytes in the hex view at the bottom of the window — that's the same data, just shown as raw bytes instead of decoded text.

### 5. Export the payload to a file (optional)

Right-click the payload section and look for an option like **Export Packet Bytes**. This lets you save just that chunk of data as its own file, separate from the rest of the packet.

### 6. Try it on a TCP stream instead

Right-click any packet and choose **Follow → TCP Stream**. Everything shown there is also payload data — just the combined payload across an entire conversation instead of one single packet.

## What you should see

Clicking into the payload of an HTTP response should show you readable HTML, something like:

```
<!DOCTYPE html>
<html>
<head>...
```

If you instead see scrambled, unreadable bytes, the traffic is likely encrypted (TLS) or compressed, and can't be read directly this way.

## If something looks wrong

- Payload looks like random symbols — likely encrypted or compressed; this is expected for HTTPS traffic
- No payload section at all — the packet you clicked may not actually contain data (some packets are just acknowledgments)
- Exported file won't open properly — check what type of data it actually is; not every payload is plain text
