# Exercise 9 - Analyzing TCP Connections

This guide is about looking at a full TCP connection from start to finish — not just the handshake, but everything that happens after it too.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from an earlier exercise, with a handshake already found

## Steps

### 1. Open your capture in Wireshark

Use a saved capture, or start a fresh one and browse to a website.

### 2. Find one connection to follow

Pick one of the handshakes you found in Exercise 8 — note the IP address and port number involved (e.g. port 34076 talking to 172.217.22.46).

<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/analysing%20TCP%20connection.png">

### 3. Follow just that one connection

Right-click any packet from that handshake and choose **Follow → TCP Stream**. This opens a clean window showing only that one conversation, in order.

Close that window when done, and you'll notice Wireshark has automatically applied a filter for you in the main window — something like `tcp.stream eq 5`. That's another easy way to isolate one connection.

### 4. Watch the connection grow

Scroll through the filtered packets and notice:

- **Seq** and **Ack** numbers going up as data is sent — this is how both sides keep track of how much has been sent and received
- **Win** (window size) — how much data can be sent before waiting for an acknowledgment
- Packets with **[PSH, ACK]** — these usually carry actual data, not just a handshake or acknowledgment

### 5. Find how the connection ends

Keep scrolling to the end of that same conversation. Look for:

- **[FIN, ACK]** — one side saying "I'm done sending"
- A matching **[ACK]** back
- Sometimes a second **[FIN, ACK]** the other direction, since either side can end its part separately

If a connection instead ends with a **[RST]** packet, that means it was cut off abruptly rather than closed politely — often due to an error or a server refusing something.

### 6. Compare a couple of connections

Look at a different `tcp.stream` number and compare. Notice how connection length, amount of data, and closing behavior can be different every time.

## What you should see

A full connection generally follows this shape:

1. SYN, SYN-ACK, ACK (the handshake from Exercise 8)
2. A series of PSH/ACK packets carrying the actual data
3. FIN/ACK packets closing the connection down (or a RST if it ended abruptly)

## If something looks off

- No FIN or RST anywhere — the connection might still be open, or your capture stopped before it closed
- Seeing a RST — not necessarily a problem, some servers close idle connections this way instead of a clean FIN
- Can't find "Follow TCP Stream" — make sure you right-clicked directly on a TCP packet, not a different protocol
