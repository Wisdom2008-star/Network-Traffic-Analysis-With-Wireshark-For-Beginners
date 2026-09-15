# Exercise 12 - Filtering HTTP Traffic

This guide covers narrowing down HTTP traffic in Wireshark so it's easier to make sense of.

## Lab Setup and Tools

**Machine**
- A computer connected to the internet

**Software**
- Wireshark installed

**Permissions**
- Ability to run Wireshark as admin (it'll ask if needed)

**Optional but helpful**
- Your saved capture from Exercise 11, or a fresh one

## Steps

### 1. Open or start a capture

Open the file from Exercise 11, or start a new capture and visit a plain HTTP site (like `http://neverssl.com`).

### 2. Apply the basic HTTP filter

Type this in the filter bar and hit Enter:

```
http
```

### 3. Narrow it down further

A few useful ways to narrow things down:

- Only the requests your browser sent out:
  ```
  http.request
  ```

- Only the responses coming back:
  ```
  http.response
  ```

- Only a specific type of request, like GET:
  ```
  http.request.method == "GET"
  ```

- Only responses with a specific status code, like errors:
  ```
  http.response.code == 404
  ```

- Traffic to or from one specific website:
  ```
  http.host == "neverssl.com"
  ```

### 4. Try "Follow HTTP Stream"

Right-click any HTTP packet and choose **Follow → HTTP Stream**. This shows the request and response together, laid out cleanly.

### 5. Save your filtered view (optional)

`File → Export Specified Packets`, choose "Displayed" under Packet Range, and save it.

## What you should see

With just `http`, you'll see both requests and responses mixed together. Using `http.request` or `http.response` on its own splits them apart. Using "Follow HTTP Stream" shows one full exchange — the request and its matching response — in a single readable view.

## If nothing shows up

- Double check the site you visited was actually plain HTTP, not HTTPS (HTTPS traffic shows up as TLS, not HTTP)
- Make sure the filter bar turned green, not red — red means Wireshark doesn't recognize what you typed
- If using `http.host`, make sure the hostname is typed exactly as it appears in the address bar
