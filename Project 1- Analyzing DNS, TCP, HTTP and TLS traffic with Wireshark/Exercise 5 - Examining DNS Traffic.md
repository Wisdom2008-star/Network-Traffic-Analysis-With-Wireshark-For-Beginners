# Exercise 5 - Examining DNS Traffic

This guide pulls everything from Exercises 1-4 together — looking at a full DNS conversation from start to finish, not just one piece at a time.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from an earlier exercise
- A website that makes several DNS lookups at once (most sites do this in the background, loading images, ads, fonts, etc. from other domains)

## Steps

### 1. Open your capture in Wireshark

Use an earlier capture, or start a fresh one and browse to a website.

### 2. Filter for DNS

Type `dns` in the filter bar like before.

### 3. Look at the whole picture, not just one pair

Instead of clicking into just one question and answer, scroll through the full list of DNS packets. Notice:

- How many different websites got looked up just from visiting one page
- Whether any hostname was asked more than once
- Whether both A (IPv4) and AAAA (IPv6) questions were sent for the same site

### 4. Follow one hostname all the way through

Pick one hostname from the list. Find:
- Its question packet
- Its answer packet
- The actual IP address it got back

Then think about what happens next: that IP address is what your computer uses to actually connect to the website, right after this.

### 5. Check the timing

Look at the **Time** column for your DNS packets. Notice how fast the answer usually comes back after the question — this is normally a fraction of a second unless something's wrong with the network.

### 6. Spot anything unusual

While scrolling through, look out for:
- A reply code that isn't "No error"
- A question that never got an answer
- A hostname that looks suspicious or unfamiliar (this matters a lot in real security work — unexpected lookups can be a sign of malware "phoning home")

## What you should see

A full page load usually triggers a handful of DNS lookups, not just one — often for the main site plus other domains it pulls content from behind the scenes. Each one follows the same pattern from Exercises 3 and 4: a question, then a matching answer.

## If something looks wrong

- Way more lookups than expected — normal for busy websites, they load resources from lots of different places
- A hostname you don't recognize at all — worth a quick search to see what it belongs to
- No answer for a question — could mean a slow or blocked DNS server
