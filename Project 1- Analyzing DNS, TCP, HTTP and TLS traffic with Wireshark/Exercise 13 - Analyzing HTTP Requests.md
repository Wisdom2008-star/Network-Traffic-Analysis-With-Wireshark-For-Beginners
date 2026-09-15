# Exercise 13 - Analyzing HTTP Requests

This guide is about opening up an HTTP request packet and understanding what's inside it.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 11 or 12

## Steps

### 1. Open your HTTP capture in Wireshark

Use a saved capture, or start a fresh one and visit a plain HTTP site (like `http://neverssl.com`).

### 2. Filter for requests only

Type this in the filter bar and hit Enter:

```
http.request
```

### 3. Click on a request packet

In the details pane, expand **Hypertext Transfer Protocol**.

### 4. Look at the request line

At the top, you'll see something like:

```
GET / HTTP/1.1
```

- **GET** — the method, meaning "just give me this page" (other methods exist too, like POST for submitting data)
- **/** — the path, which page or resource is being asked for
- **HTTP/1.1** — the version of HTTP being used

### 5. Look at the headers

Below the request line, expand a few of the headers:

- **Host** — which website this request is going to
- **User-Agent** — info about the browser making the request
- **Accept** — what kind of content the browser is willing to receive back

### 6. Compare a few requests

If your capture has more than one request, look at a couple more. Notice:

- Not every request uses GET — some pages submit forms with POST
- The Host header stays the same for every request to the same site, even across different pages

## What you should see

A request packet broken down like this:

- Method: GET
- Path: /
- Version: HTTP/1.1
- Host: neverssl.com
- User-Agent: (your browser's name and version)

Basically — the request line says what's being asked for, and the headers give extra details about who's asking and what they're willing to accept back.

## If something looks wrong

- No requests showing up — you may have captured only HTTPS traffic, which won't appear under `http.request`
- Method isn't GET — that's normal, forms and some page actions use POST or other methods instead
- Can't find "Hypertext Transfer Protocol" in the details pane — make sure you clicked a packet that's actually an HTTP request, not just any packet
