# Exercise 2 - Filtering DNS Traffic

This guide walks through narrowing a Wireshark capture down to just DNS traffic, and picking out the useful details.

## Lab Setup and Tools

Here's what you need before starting:

**Machine**
- A computer connected to a network (Wi-Fi or Ethernet — either works)

**Software**
- [Wireshark](https://www.wireshark.org/download.html) installed
- A terminal or command prompt (already built into Windows, macOS, and Linux — nothing extra to install)

**Permissions**
- Ability to run Wireshark as admin/root, or capture permissions on your network interface

**Optional but helpful**
- A capture already saved from Exercise 1, or a fresh one you can start recording now
- A hostname or website you haven't visited recently, so the DNS lookup actually happens instead of pulling from a local cache

## Steps

### 1. Open or start a capture

Either open the `.pcapng` file you saved in Exercise 1 (`File → Open`), or start a fresh capture on your network interface like before.

### 2. Apply the basic DNS filter

Type this in the filter bar and hit Enter:

```
dns
```

This hides everything that isn't DNS, so the packet list only shows lookups.

### 3. Narrow it down further (optional filters)

Sometimes `dns` on its own still shows more than you need. A few useful narrower filters:

- Only DNS queries you sent out (not responses coming back):
  ```
  dns.flags.response == 0
  ```
- Only DNS responses coming back:
  ```
  dns.flags.response == 1
  ```
- Only lookups for a specific website:
  ```
  dns.qry.name == "example.com"
  ```
- Catch DNS traffic even before Wireshark labels it as DNS (rare, but useful):
  ```
  udp.port == 53
  ```

### 4. Click into a packet

Click on any single DNS packet in the list. In the panel below, expand the section labeled **Domain Name System**. This is where the actual useful info lives — the hostname being looked up, and (for responses) the IP address that was found.

### 5. Save your filtered view (optional)

If you want to keep just the filtered packets as their own file: `File → Export Specified Packets`, choose "Displayed" under Packet Range, and save it.

## What you should see

With the `dns` filter applied, your packet list should look something like this:

| Source | Destination | Info |
|---|---|---|
| Your computer | DNS server | Standard query — asking for example.com |
| DNS server | Your computer | Standard query response — example.com is at 93.184.216.34 |

<img src="https://github.com/Wisdom2008-star/Networking-Wireshack-Assignment-3-/blob/b48683dadd3caef8c29634ce04ffcd95f38dd620/Capturing%20DNS%20traffic.png">

Everything else — web page loading, background app traffic, etc. — should be hidden from view. Only the question-and-answer pairs for DNS lookups show up.

If you open the response packet's details and expand **Domain Name System → Answers**, you'll see the actual IP address it resolved to, along with how long that answer is valid for before it needs to be looked up again.

## If nothing shows up

- Make sure DNS lookups actually happened during your capture (revisit Exercise 1's tip about using a fresh hostname)
- Double check the filter bar turned green, not red — red means Wireshark doesn't recognize the filter as typed
- If you're using `dns.qry.name`, make sure the hostname is spelled exactly as it appears in the browser
