
# 3. Computer Networks

## 3.1 What is Computer Networking?

A computer network is a group of connected devices that communicate and exchange data.

Examples:

- Internet
- LAN
- WAN
- Client-server architecture

### Client-server model

The client sends a request, and the server processes it and sends a response.

[How the Web works, Part II: What happens when you visit a URL -](https://images.openai.com/static-rsc-4/H3RYTUYEv7ZPU_WskThwKhSqygSYeWQ5i-z-cZhwjKliz2GfTIJvd9SGHnrpxAVTHdsdfyc2WBhvOsMnSng-RcO_5mW_VPX1ZMpLaD2JvMT7amKNeeMmJUQnXheLHtXU5Hejl2q5WwB0gU623e_Q1g6P-BB9E4UVQqtu7dqzqs0?purpose=inline)

[pressidium.com](https://pressidium.com/blog/2016/how-the-web-works-what-happens-when-you-visit-a-url/?utm_source=chatgpt.com)

Backend example:

1. Browser sends a login request.
2. Backend server receives it.
3. Server validates credentials.
4. Database checks user information.
5. Server returns an HTTP response.

## 3.2 TCP vs UDP

This is one of the most important networking MCQ topics.

### TCP (Transmission Control Protocol)

TCP is connection-oriented and provides reliable, ordered byte-stream delivery.

Features:

- Connection establishment.
- Reliable delivery.
- Error detection and retransmission.
- Ordered data.
- Flow control.
- Congestion control.

### UDP (User Datagram Protocol)

UDP is connectionless and provides best-effort datagram delivery.

Features:

- No connection establishment.
- No guaranteed delivery.
- No guaranteed ordering.
- Lower protocol overhead.
- Supports broadcast and multicast use cases.

### TCP vs UDP

| Feature        | TCP                       | UDP                           |
| -------------- | ------------------------- | ----------------------------- |
| Connection     | Connection-oriented       | Connectionless                |
| Reliability    | Reliable                  | Best effort                   |
| Ordering       | Maintained                | Not guaranteed                |
| Retransmission | Yes                       | No built-in retransmission    |
| Speed/overhead | More overhead             | Less overhead                 |
| Use cases      | Web, email, file transfer | DNS, streaming, gaming, voice |

Examples:

- HTTPS commonly uses TCP.
- DNS commonly uses UDP, but can also use TCP.
- HTTP/3 uses QUIC over UDP.

### TCP Three-Way Handshake

Before establishing a TCP connection, the client and server perform a three-way handshake.

[TCP 3-Way Handshake](https://images.openai.com/static-rsc-4/6gwA6gBGeNzuFPpuXdmiAs-vlhGCbPmLWBgI_4xJCZxasydLAwYwM8FCbvaLpPhutfzcMhfoVnohyupfP_Nzx5KP3BexROJjP8T2Ai6setOQ53pzUai8U3spaoDWIONhaiEVa9wLnsHUh8d2wIsoUNo_L2cSoErWphUHRcaQFPA?purpose=inline)

[blog.jargoniseasy.com](https://blog.jargoniseasy.com/tcp-3-way-handshake?utm_source=chatgpt.com)

Steps:

1. SYN – Client requests a connection.
2. SYN-ACK – Server acknowledges and responds.
3. ACK – Client acknowledges.

Connection established.

Memory trick: SYN → SYN-ACK → ACK.

## 3.3 IP Address and Port

### IP Address

An IP address identifies a network interface for communication.

Types:

- IPv4: 32-bit address.
- IPv6: 128-bit address.

Example:

- IPv4: `192.168.1.1`
- IPv6: `2001:db8::1`

### Port Number

A port identifies a service or application endpoint on a host.

Important ports:

| Port  | Protocol/Service |
| ----- | ---------------- |
| 20/21 | FTP              |
| 22    | SSH              |
| 25    | SMTP             |
| 53    | DNS              |
| 80    | HTTP             |
| 443   | HTTPS            |
| 3306  | MySQL            |
| 5432  | PostgreSQL       |
| 27017 | MongoDB          |

Remember: Ports identify services, while IP addresses identify network interfaces.

## 3.4 HTTP (Hypertext Transfer Protocol)

HTTP is an application-layer protocol used for communication between clients and servers.

It follows a request-response model.

Example:

```
GET /users/10 HTTP/1.1
Host: example.com
```

Server response:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 10,
  "name": "Nova"
}
```

### HTTP Methods

| Method | Purpose                   | Idempotent?     |
| ------ | ------------------------- | --------------- |
| GET    | Retrieve data             | Yes             |
| POST   | Create/process resource   | Generally no    |
| PUT    | Replace resource          | Yes             |
| PATCH  | Partially update resource | Not necessarily |
| DELETE | Delete resource           | Yes             |

Important:

- Safe methods do not intend to modify server state.
- Idempotent means repeating the same request has the same intended effect as performing it once.
- PUT is generally idempotent.
- POST is generally not idempotent.
- DELETE is idempotent in terms of intended server state, even if repeated responses differ.

### HTTP Status Codes

Memorize these.

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 202  | Accepted              |
| 204  | No Content            |
| 301  | Moved Permanently     |
| 302  | Found                 |
| 304  | Not Modified          |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 405  | Method Not Allowed    |
| 409  | Conflict              |
| 422  | Unprocessable Content |
| 429  | Too Many Requests     |
| 500  | Internal Server Error |
| 502  | Bad Gateway           |
| 503  | Service Unavailable   |
| 504  | Gateway Timeout       |

Common interview traps:

- 401 = Authentication missing or invalid.
- 403 = Authenticated or otherwise identified client is not allowed to access the resource.
- 404 = Resource not found.
- 500 = Server-side error.
- 502 = Gateway received an invalid response from upstream.
- 503 = Service unavailable.

## 3.5 HTTPS

HTTPS is HTTP secured using TLS (Transport Layer Security).

It provides:

1. Confidentiality – Encryption protects data from being read by unauthorized parties.
2. Integrity – Detects unauthorized modification.
3. Authentication – Certificates help verify server identity.

### HTTP vs HTTPS

| HTTP                              | HTTPS                     |
| --------------------------------- | ------------------------- |
| No TLS protection                 | Uses TLS                  |
| Data not encrypted by HTTP itself | Data encrypted in transit |
| Default port 80                   | Default port 443          |
| No TLS certificate required       | TLS certificate used      |

### How HTTPS works

Simplified process:

1. Client connects to server.
2. TLS handshake takes place.
3. Server presents its certificate.
4. Client validates the certificate.
5. Client and server establish shared session keys.
6. HTTP communication happens securely over TLS.

Important: HTTPS does not mean a website is trustworthy in every respect. It protects the connection, not the honesty of the website.

## 3.6 DNS (Domain Name System)

DNS translates domain names into IP addresses.

Example:

```
google.com → IP address
```

Without DNS, users would need to remember IP addresses instead of domain names.

### DNS resolution process

[Understanding DNS Resolution Basics](https://images.openai.com/static-rsc-4/7kzkMW7q2TaNLaj1TqaFc6TAeK8Z77TJZAb1BmuVgt-3Nu7N43SgrlweHLjTBWCKYwJX7oRQY77jxOc1KzXFoSOeT6OsSVc5OZb5mIrpKjWSGOtlaOLGR5-0FlF2igBh6NJYmc8tSXS9HUetkuBwH75xanhpt99xUHvtkUhdlS8?purpose=inline)

[blog.dhiraj.dev](https://blog.dhiraj.dev/how-dns-resolution-works?utm_source=chatgpt.com)

Simplified steps:

1. Browser checks its DNS cache.
2. Operating system checks its cache.
3. DNS resolver is queried.
4. Resolver may contact root DNS servers.
5. Root server directs it to the TLD server.
6. TLD server directs it to the authoritative DNS server.
7. Authoritative server provides the DNS record.
8. The IP address is returned to the client.

### Important DNS records

| Record | Purpose                                                             |
| ------ | ------------------------------------------------------------------- |
| A      | Domain → IPv4 address                                               |
| AAAA   | Domain → IPv6 address                                               |
| CNAME  | Alias to another domain name                                        |
| MX     | Mail server information                                             |
| NS     | Authoritative name servers                                          |
| TXT    | Text information, commonly verification and email security policies |
| PTR    | Reverse DNS lookup                                                  |

Important: DNS typically uses port 53 over UDP or TCP.

## 3.7 OSI Model

A common networking MCQ topic.

The OSI model has seven layers.

[Please Do Not Throw Sausage Pizza Away! — OSI Model Mnemonic | by Anupriya Verma | Jan, 2026 | Medium](https://images.openai.com/static-rsc-4/-EvFEexLeoloW_uDL0wDjwdrW4XqW_lXIdnbDtHSi8nqkqWP-5up_oYGN7nAJc01khLO0BZMWbYNcoxMR1BvTRoxjxHH0WBeSnvdLkJUhZejoNpwm-x9KrqevbqkjkBW3F7_Rx0wVaY6H61fQzkT1kzTerWEugxjoKkFG4NingY?purpose=inline)

[medium.com](https://medium.com/%40anupriyaverma/please-do-not-throw-sausage-pizza-away-osi-model-mnemonic-daa8b92a7324?utm_source=chatgpt.com)

| Layer | Name         | Main responsibility                          |
| ----- | ------------ | -------------------------------------------- |
| 7     | Application  | Network services for applications            |
| 6     | Presentation | Data representation, encryption, compression |
| 5     | Session      | Session management                           |
| 4     | Transport    | End-to-end delivery                          |
| 3     | Network      | Routing and IP addressing                    |
| 2     | Data Link    | Frames and MAC addressing                    |
| 1     | Physical     | Transmission of bits                         |

Memory trick (top to bottom): All People Seem To Need Data Processing.

Important associations:

- HTTP, DNS → Application
- TCP, UDP → Transport
- IP → Network
- Ethernet, MAC → Data Link

