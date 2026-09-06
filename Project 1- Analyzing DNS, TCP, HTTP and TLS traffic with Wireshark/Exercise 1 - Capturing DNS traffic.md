# Exercise 1 - Capturing DNS Traffic

This is a simple guide to watching a DNS lookup happen in Wireshark.

## What you need

- Wireshark installed on your computer
- Permission to capture traffic (just run it as admin if it asks)

## Steps

### 1. Pick your network

Open Wireshark. You'll see a list of network connections. Pick the one you're actually using (Wi-Fi or Ethernet) — it's usually the one with a moving graph next to it.

### 2. Start capturing

Click on that network, or hit the blue shark-fin button. Wireshark is now recording everything going in and out of your computer.

### 3. Filter for DNS only

Type this in the search bar at the top and hit Enter:

```
dns
```

This hides everything except DNS traffic, so it's easier to read.

### 4. Make a DNS lookup happen

While it's still recording, do one of these:

- Visit a website you haven't opened recently
- Or open a terminal/command prompt and type: `nslookup example.com`

Use a site you haven't visited recently — if your computer already knows the IP address, it won't need to ask again.

### 5. Stop recording

Click the red square button.

### 6. Save it

Go to `File → Save As`, and save it in your `captures/` folder.

## What you should see

Two lines showing up together, like this:

| Source | Destination | What it means |
|---|---|---|
| Your computer | DNS server | "What's the IP address for example.com?" |
| DNS server | Your computer | "It's 93.184.216.34" |

That's it — one packet asking the question, one packet answering it.

If you click on the answer packet, you can open it up and see the actual IP address it found, plus how long your computer is allowed to remember that answer before asking again.

## If you don't see anything

- Try a website or hostname you haven't visited in a while
- Make sure you picked the right network in step 1
- Some apps send DNS requests in a hidden, encrypted way instead of the normal plain way — if that's happening, try using `nslookup` from a terminal instead, that almost always shows up normally
