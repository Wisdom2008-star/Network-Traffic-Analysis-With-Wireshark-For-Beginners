# Exercise 10 - Following a TCP Stream

This guide focuses specifically on the "Follow TCP Stream" window in Wireshark — what it shows and how to read it.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from an earlier exercise

## Steps

### 1. Open your capture in Wireshark

Use a saved capture, or start a fresh one and browse to a website.

### 2. Pick a TCP packet to follow

Click on any packet that's part of a TCP connection you want to look at.
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream.png">

### 3. Open Follow TCP Stream

Right-click the packet and choose **Follow → TCP Stream**. A new window opens showing that whole conversation by itself.
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(3).png">

### 4. Read the colors

Inside the stream window, the two sides of the conversation are shown in different colors:

- One color is everything your computer sent
- The other color is everything the server sent back
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(4).png">

This makes it easy to tell who said what without digging through individual packets.

### 5. Switch the view format

Near the bottom of the window, there's a dropdown (usually says something like "ASCII"). Try switching between:

- **ASCII** — readable text, if the traffic isn't encrypted
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(4).png">

- **Hex Dump** — the raw bytes, useful when the data isn't plain text
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(5).png">

- **C Arrays** — rarely needed, mostly used for programming purposes
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(6).png">

If the connection was encrypted (like TLS), you'll mostly see scrambled, unreadable characters instead of plain text — that's expected and actually a good sign the encryption is working.

### 6. Notice the filter it created

Close the stream window. Back in the main packet list, Wireshark will have applied a filter automatically, something like:

```
tcp.stream eq 3
```
<img src="https://github.com/Wisdom2008-star/Network-Traffic-Analysis-With-Wireshark-For-Beginners/blob/main/Screenshots/Following%20a%20TCP%20stream%20(7).png">

This is the same conversation, just shown in the normal packet list instead of the popup window.

### 7. Save the stream (optional)

Inside the Follow Stream window, there's usually a **Save as** option, letting you export just that conversation's data to a file.

## What you should see

A two-colored block of text (or scrambled data, if encrypted) showing the full back-and-forth of one conversation, from the first packet to the last — much easier to read top-to-bottom than scrolling through the regular packet list.

## If something looks off

- Everything looks like random symbols — normal for encrypted traffic like TLS; try picking an older, plain HTTP connection instead if you want to see readable text
- The stream window is empty — you may have clicked a packet that isn't actually part of a TCP conversation with any data in it
- Can't find "Follow TCP Stream" in the right-click menu — make sure the packet you clicked is a TCP packet, not a different protocol
