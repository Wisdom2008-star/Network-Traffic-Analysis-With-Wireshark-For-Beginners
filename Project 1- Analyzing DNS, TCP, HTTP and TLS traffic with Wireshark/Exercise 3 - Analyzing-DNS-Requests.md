# Exercise 3 - Analyzing DNS Requests

This guide is about opening up a DNS packet and understanding what's inside it.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed
- A terminal or command prompt

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 2
- A couple different websites looked up, so you have more than one to look at

## Steps

### 1. Open your DNS capture

Use the file from Exercise 2, or start a new capture and filter with `dns` like before.

### 2. Click on a question packet

Find a packet going FROM your computer TO a DNS server. Click it, then open the section that says **Domain Name System (query)**.

You'll see:
- **Name** — the website it's asking about
- **Type** — usually just "A", which means it wants an IP address

<img width="964" height="478" alt="Screenshot 2026-09-06 233035" src="https://github.com/user-attachments/assets/304fc916-c7fb-4283-9398-10700c289fbd" />


### 3. Find the matching answer packet

Right after the question, there should be an answer packet coming back. Click it, then open **Domain Name System (response)**.

<img src="https://github.com/Wisdom2008-star/Networking-Wireshack-Assignment-3-/blob/f90d3b5fc4bc735b694e6b757d1d9027c4491482/Screenshot%202026-09-06%20230157.png">

You'll see:
- **Answer** — the actual IP address it found
- **Time to live** — how many seconds it can remember this answer before asking again
- **Reply code** — should say "No error" if it worked

### 4. Look at a few more

If you have more than one lookup in your capture, check a few. You'll notice:
- Some sites give back more than one IP address
- Some answers come back faster than others
- The "time to live" number is different for every site

### 5. Try a lookup that fails (optional)

Type `nslookup somefakewebsitethatdoesnotexist.com` and capture it. Check the reply code on the answer — it'll say something like "Name Error" instead of "No error." That's what it looks like when a website doesn't exist.

## What you should see

**The question:**
- Name: example.com
- Type: A

**The answer:**
- Reply code: No error
- Answer: 93.184.216.34
- Time to live: 300

Basically — the question asks for a website's IP address, and the answer gives it back (or says it failed).

## If something looks wrong

- No answer showing up? The lookup might have failed or timed out
- A short or long "time to live"? Totally normal, every site sets its own
- More than one IP address for one site? Also normal, big sites use several servers
