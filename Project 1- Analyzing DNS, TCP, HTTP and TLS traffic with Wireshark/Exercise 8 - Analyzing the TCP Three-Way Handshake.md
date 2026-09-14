# Exercise 8 - Analyzing the TCP Three-Way Handshake

This guide walks through finding and understanding the three-way handshake — how a TCP connection actually gets started.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 6 or 7

## Steps

### 1. Open your TCP capture in Wireshark

Use a saved capture, or start a fresh one and browse to a website.

### 2. Filter for TCP traffic

Type this in the filter bar and hit Enter:

```
tcp
```

Using the plain `tcp` filter (instead of a SYN-only filter) means all three handshake packets will actually show up in the list — nothing gets hidden.

### 3. Find a set of three packets

Look for three packets close together, going back and forth between your computer and one server, all using the same port number:

1. Your computer → server, with **[SYN]** in the Info column
2. Server → your computer, with **[SYN, ACK]** in the Info column
3. Your computer → server, with just **[ACK]** in the Info column

Tip: if you filter using `tcp.flags.syn == 1` instead, you'll only see packets 1 and 2 — the final ACK doesn't have the SYN flag set, so it gets hidden. Stick with the plain `tcp` filter for this exercise so you can see the full handshake.

### 4. Click into each packet

Open the **Transmission Control Protocol** section in the details pane for each of the three, and look at:

- **Flags** — confirms which stage this is (SYN, SYN-ACK, or ACK)
- **Sequence number** — a number each side uses to keep track of the data
- **Acknowledgment number** — confirms what's been received so far

### 5. See how the numbers connect

Notice how each packet's acknowledgment number is one more than the sequence number it's replying to. That's how the two sides confirm they're both on the same page before sending any real data.

## What you should see

A clean set of three packets like this:

| Step | Direction | Flags |
|---|---|---|
| 1 | Your computer → Server | SYN |
| 2 | Server → Your computer | SYN, ACK |
| 3 | Your computer → Server | ACK |

Once all three have happened, the connection is open and ready — that's when you'll start seeing regular data packets (like TLS or HTTP traffic) between the same two addresses.

## If something looks off

- Only seeing SYN and SYN-ACK, no final ACK — check that you're using the plain `tcp` filter, not `tcp.flags.syn == 1`, since that filter hides the final ACK
- Handshake never seems to finish — could mean the connection failed, or you started capturing after it already happened
- Multiple handshakes happening close together — normal, since a single page load often opens several connections at once
