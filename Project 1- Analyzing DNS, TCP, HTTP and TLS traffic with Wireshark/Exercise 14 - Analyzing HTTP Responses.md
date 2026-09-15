# Exercise 14 - Analyzing HTTP Responses

This guide focuses on the response packets that come back after an HTTP request — what they contain and what to check.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 11, 12, or 13

## Steps

### 1. Open your HTTP capture in Wireshark

Use a saved capture, or start a fresh one and visit a plain HTTP site.

### 2. Filter for responses only

Type this in the filter bar and hit Enter:

```
http.response
```

### 3. Click on a response packet

In the details pane, expand **Hypertext Transfer Protocol**.

### 4. Look at the status line first

At the top, you'll see something like:

```
HTTP/1.1 200 OK
```

- **200** — the status code, telling you what happened
- **OK** — a short description of that code

Common status codes to recognize:
- **200** — success, here's the page
- **301 / 302** — redirect, go look somewhere else instead
- **404** — not found
- **500** — something broke on the server's end

### 5. Look at the headers

Below the status line, expand a few headers:

- **Content-Type** — what kind of content this is (e.g. `text/html`)
- **Content-Length** — how big the response body is, in bytes
- **Server** — info about the software running the web server

### 6. Look at the actual content

If you expand further, you may see **Line-based text data** or similar — this is the actual HTML that was sent back, which is what your browser turns into the visible page.

## What's the Difference from Exercise 13?

Exercise 13 was about **requests** — what your browser asks for. This exercise is about **responses** — what the server sends back.

| | Requests (Exercise 13) | Responses (this exercise) |
|---|---|---|
| Who sends it | Your browser | The web server |
| First line to check | Request line (method, path) | Status line (status code) |
| Main things to check | Method, Path, Host | Status code, Content-Type, Content-Length |
| What it tells you | What you're asking for | Whether it worked, and what came back |

Every request should have exactly one matching response.

## What you should see

- Status code: 200
- Status text: OK
- Content-Type: text/html
- Content-Length: (some number of bytes)

## If something looks wrong

- Status code isn't 200 — check what it is against the list above; a 404 or 500 tells you something specific went wrong
- No response at all for a request — the connection may have been interrupted or is still waiting
- Can't see the actual HTML content — some responses are compressed, which Wireshark may show as unreadable bytes instead of plain text
