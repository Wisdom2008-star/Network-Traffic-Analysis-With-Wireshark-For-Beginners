# Exercise 4 - Analyzing DNS Responses

This guide focuses just on the answer packets that come back from a DNS server — what they contain and what to check.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 2 or 3
- A couple different response packets to compare

## What's the Difference from Exercise 3?

Exercise 3 was about **requests** — the question packet your computer sends out, asking for a website's IP address. You mainly looked at the Name and Type in that one.

This exercise is about **responses** — the answer packet coming back from the DNS server. You're checking a different set of things:

| | Requests (Exercise 3) | Responses (this exercise) |
|---|---|---|
| Who sends it | Your computer | The DNS server |
| Section to expand | Domain Name System (query) | Domain Name System (response) |
| Main things to check | Name, Type | Reply code, Answers (Address, Time to live) |
| What it tells you | What you're asking for | Whether it worked, and the actual IP address |

Basically: the request is the question, the response is the answer. Every request should have exactly one matching response with the same ID.

## Steps

### 1. Open your DNS capture in Wireshark

Use a capture from an earlier exercise, or start a new one and filter with `dns`.

### 2. Filter for responses only (optional)

If you want to see only the answer packets and hide the questions, type this in the filter bar:

```
dns.flags.response == 1
```

### 3. Click on a response packet

Pick one where the DNS server is the source (sending back to your computer). In the details pane, expand **Domain Name System (response)**.

### 4. Check the reply code first

Open the **Flags** section inside it. Look at **Reply code** — this tells you right away if the lookup worked:

- "No error" means it succeeded
- "Name Error" means the website doesn't exist
- Anything else means something else went wrong

### 5. Open the Answers section

This is the actual result. You'll see:

- **Name** — the website that was asked about
- **Type** — A (IPv4 address) or AAAA (IPv6 address)
- **Address** — the actual IP address
- **Time to live** — how long this answer is good for, in seconds, before it needs to be looked up again

### 6. Compare a few responses

Look at a couple more response packets and notice:

- Some responses list more than one address under Answers
- Time to live numbers are different for almost every site
- A and AAAA responses for the same website usually show up as two separate packets

## What you should see

For a normal, working response:

- Reply code: No error
- Name: (the website asked about)
- Address: (an IP address)
- Time to live: (some number of seconds)

That's really all a DNS response is — a yes/no on whether it worked, and if yes, the IP address plus how long to remember it.

## If something looks wrong

- Reply code says "Name Error" — the hostname doesn't exist or was typed wrong
- No Answers section at all — the lookup may have failed completely
- Response doesn't match the question's ID — you're probably looking at the wrong pair, find the response with the matching ID instead
