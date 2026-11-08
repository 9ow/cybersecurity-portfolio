# Client–Server Fundamentals — TryHackMe

**Platform:** TryHackMe  
**Room:** Client–Server  
**Status:** Completed — 8 November 2026

## Overview

Studied how networked computers exchange information using the client–server model. A client initiates a request for a service or resource; the server processes that request and returns a response. A server can offer several services, with protocols and ports governing how clients access them.

## Core concepts

| Concept | Technical explanation |
| --- | --- |
| Client | A device or application that initiates requests, such as a web browser |
| Server | A system or application that handles requests and provides services |
| Network | Connected systems that exchange data and share services |
| Protocol | Rules for message syntax, structure, commands, and responses |
| Port | A transport-layer identifier for a network endpoint/service |
| DNS | Domain Name System; resolves domain names to DNS records, including IP addresses |
| IP address | A network-layer address used to identify an interface and route traffic |

### Request and response

For ordinary web browsing, the client sends a request and the web server responds with a status code, headers, and usually a response body. A request for an unavailable resource may produce `404 Not Found`; a successful request commonly returns `200 OK`.

### URLs and service access

Example: `https://www.iamlearning.thm/contact`

- **Scheme:** `https`
- **Host:** `www.iamlearning.thm`
- **Path:** `/contact`
- **Port:** HTTPS typically uses TCP port `443` when no different port is specified.

The host identifies the destination by name; DNS can resolve a host name to an IP address. A port selects the network service endpoint. Common ports include `22/TCP` (SSH), `80/TCP` (HTTP), `443/TCP` (HTTPS), and `53/UDP` or `53/TCP` (DNS).

## HTTP and HTTPS

HTTP is an application-layer request–response protocol. HTTP itself is **stateless**: each request is self-contained rather than automatically remembering prior requests. Web applications maintain user sessions through mechanisms such as cookies, server-side session identifiers, and tokens.

HTTPS carries HTTP over TLS to protect data in transit.

### HTTP methods

| Method | Primary use |
| --- | --- |
| `GET` | Retrieve a resource |
| `POST` | Submit data for processing |
| `PUT` | Create or replace a resource at a target URI |
| `PATCH` | Apply a partial modification |
| `DELETE` | Request removal of a resource |
| `HEAD` | Request response headers without a body |
| `OPTIONS` | Discover communication options |
| `CONNECT` | Establish a tunnel, often through a proxy |
| `TRACE` | Request a diagnostic loopback |

## HTTP GET exercise

Opened the room's browser-based **HTTP GET Request Demo** at `http://httpdemo.local:8080`. The page listed the resources `/` (the index page), `style.css`, and `script.js`; the browser displayed a JavaScript alert reading **“JavaScript loaded via GET!”**.

The exercise introduced Firefox Developer Tools (`F12` → **Network**) as a method for observing individual HTTP requests, including the scheme, host, requested filename/path, destination address, status code, and response body.

Example request:

```http
GET / HTTP/1.1
Host: httpdemo.local:8080
```

A successful response may include a `200 OK` status, `Content-Type: text/html`, and an HTML document body. In the exercise explanation, `127.0.0.1` represents the loopback address for a web service hosted on the same machine.

## Security relevance

Understanding the difference between a request and a response is foundational for web traffic analysis. Analysts can examine URLs, methods, response codes, and HTTP metadata when reviewing application access logs, proxy data, or packet captures. A successful HTTP response alone does not establish that an attack occurred.

## Key takeaways

- The client initiates the service request; the server processes it and sends a response.
- DNS, IP addresses, and ports solve different parts of service discovery and connectivity.
- HTTP methods specify the action requested; response codes report the outcome.
- Cookies and sessions provide application-level state on top of stateless HTTP.
- Browser Developer Tools expose the requests a web page makes for HTML, CSS, and JavaScript resources.
