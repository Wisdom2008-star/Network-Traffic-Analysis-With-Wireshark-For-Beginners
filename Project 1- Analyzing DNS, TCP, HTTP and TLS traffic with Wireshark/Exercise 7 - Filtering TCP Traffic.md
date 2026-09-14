# Exercise 7 - Filtering TCP Traffic

This guide covers narrowing down TCP traffic in Wireshark so it's easier to make sense of.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 6, or a fresh one

## Steps

### 1. Open or start a capture

Open the file from Exercise 6, or start a new capture and browse to a website.

### 2. Apply the basic TCP filter

Type this in the filter bar and hit Enter:

```
tcp
```
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Filtering%20TCP%20traffic.png">

### 3. Narrow it down further

`tcp` on its own still shows a lot. A few useful ways to narrow it:

- Traffic to or from one specific website's server:
  ```
  ip.addr == 172.217.22.46
  ```
  (replace with whatever IP you're looking at)

- Traffic on a specific port, like normal web traffic:
  ```
  tcp.port == 443
  ```

- Combine both, to see just one conversation:
  ```
  ip.addr == 172.217.22.46 && tcp.port == 443
  ```

### 4. Try "Follow TCP Stream"

Right-click any TCP packet and choose **Follow → TCP Stream**. This opens a new window showing just that one conversation from start to finish, which is often easier to read than scrolling the packet list.
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Filtering%20TCP%20traffic%20(3).png">
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Filtering%20TCP%20traffic%20(2).png">

### 5. Save your filtered view (optional)

`File → Export Specified Packets`, choose "Displayed" under Packet Range, and save it.

## What you should see

With just `tcp`, you'll see a long list of packets going back and forth. Once you narrow it down with an IP address or port, the list should shrink down to just the packets involving that one server or that one type of traffic.

Using "Follow TCP Stream" should open a clean, isolated view of a single conversation between your computer and one server.

## If nothing shows up

- Double check the IP address is typed correctly and actually appeared in your capture
- Make sure the filter bar turned green, not red — red means Wireshark doesn't recognize what you typed
- If using a port filter and nothing shows, that server might be using a different port than expected
