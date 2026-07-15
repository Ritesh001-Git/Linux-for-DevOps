# Ping vs Curl vs Nmap

These three commands are commonly used for network troubleshooting, but they serve **different purposes**.

| Command | Purpose | Checks | Protocol | Common Use Case |
|----------|----------|---------|----------|-----------------|
| **ping** | Check if a host is reachable | Network connectivity | ICMP | Verify whether a server is online |
| **curl** | Send requests to a URL or API | Web/Application layer | HTTP, HTTPS, FTP, etc. | Test a website or REST API |
| **nmap** | Discover hosts and scan open ports | Network services | TCP, UDP | Find open ports and running services |

---

# 1. ping

## What is it?

`ping` checks whether a destination machine is reachable over the network.

It sends **ICMP Echo Request** packets and waits for **ICMP Echo Reply** packets.

---

## Syntax

```bash
ping google.com
```

---

## Sample Output

```text
PING google.com (142.250.xxx.xxx)

64 bytes from 142.250.xxx.xxx:
Reply time = 18 ms
```

---

## What It Tells You

- Is the server reachable?
- Network latency (response time)
- Packet loss

---

## Real-Life Example

**Scenario:**

Your application cannot connect to a server.

First, check if the server is reachable:

```bash
ping 192.168.1.20
```

If the ping fails, the problem is likely related to the network or the server being offline.

---

# 2. curl

## What is it?

`curl` sends requests to a URL and retrieves the response.

It is mainly used to test:

- Websites
- REST APIs
- Web services
- File downloads

---

## Syntax

```bash
curl https://example.com
```

---

## Sample Output

```html
<html>
    <body>Hello World</body>
</html>
```

---

## What It Tells You

- Is the website/API responding?
- HTTP status code
- Response headers
- Response body

---

## Real-Life Example

**Scenario:**

You deployed a Spring Boot API and want to verify it's working.

```bash
curl http://localhost:8080/api/users
```

If you receive JSON data, the API is working correctly.

---

# 3. nmap

## What is it?

`nmap` (Network Mapper) scans a machine to discover:

- Open ports
- Running services
- Operating system (optional)
- Connected hosts

---

## Syntax

```bash
nmap 192.168.1.20
```

---

## Sample Output

```text
PORT     STATE SERVICE

22/tcp   open  ssh

80/tcp   open  http

3306/tcp open  mysql
```

---

## What It Tells You

- Which ports are open
- Which services are running
- Potential attack surface

---

## Real-Life Example

**Scenario:**

Your web application is not accessible.

Scan the server:

```bash
nmap 192.168.1.20
```

If port **80** or **443** is closed, the web server is not listening or a firewall is blocking access.

---

# Quick Comparison

| Feature | ping | curl | nmap |
|---------|------|------|-------|
| Checks server reachability | ✅ | ❌ | ✅ |
| Tests APIs/Websites | ❌ | ✅ | ❌ |
| Shows response content | ❌ | ✅ | ❌ |
| Finds open ports | ❌ | ❌ | ✅ |
| Measures latency | ✅ | ❌ | ❌ |
| Identifies running services | ❌ | ❌ | ✅ |

---

# Which One Should You Use?

| Situation | Command |
|-----------|---------|
| Check if a server is online | `ping` |
| Test a REST API or website | `curl` |
| Check which ports are open | `nmap` |
| Verify network connectivity | `ping` |
| Verify API response | `curl` |
| Audit running network services | `nmap` |

---

# Simple Analogy

Imagine a building:

- **`ping`** → "Is anyone inside the building?"
- **`curl`** → "Go to the reception desk and ask for specific information."
- **`nmap`** → "Check which doors (ports) of the building are open."

---

# Summary

| Command | Best Used For |
|----------|---------------|
| **ping** | Checking basic network connectivity and latency |
| **curl** | Testing websites, APIs, and web services |
| **nmap** | Discovering open ports and running network services |
