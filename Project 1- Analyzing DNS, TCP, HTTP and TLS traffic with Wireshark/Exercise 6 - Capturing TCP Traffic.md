# Exercise 6 - Capturing TCP Traffic

This guide walks through capturing TCP traffic in Wireshark.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- A website you haven't visited recently, so a fresh connection actually gets made

## Steps

### 1. Pick your network

Open Wireshark and choose the network connection you're using (Wi-Fi or Ethernet).

### 2. Start capturing

Click the blue shark-fin button to start recording.

### 3. Filter for TCP only

Type this in the filter bar and hit Enter:

```
tcp
```

### 4. Make some traffic happen

While it's still recording, visit a website in your browser. Loading any page generates plenty of TCP traffic in the background.

### 5. Stop recording

Click the red square button once you've seen some TCP packets show up.

### 6. Save it

`File → Save As`, and save it into your `captures/` folder.

## What you should see

A long list of packets, all showing **TCP** in the Protocol column. Every bit of data going back and forth between your computer and a website counts as TCP traffic, so this list fills up fast compared to DNS.

## If nothing shows up

- Make sure you picked the right network interface in step 1
- Make sure the capture is actually running (the shark-fin button should look "pressed down" while active)
- Try visiting a website while the capture is running, not before
