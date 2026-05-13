# Networking Basics

## What is it?

Computer networking is the practice of connecting machines so they can exchange data. In the context of Kubernetes, the key networking concepts are: IP addresses, ports, protocols, DNS, and the client-server communication model.

---

## In Simple Language

Networking is how computers talk to each other.

Every device on a network gets an **IP address** (its unique address). When it wants to talk to another device, it sends data packets to that address. **Ports** specify which service on that machine should receive the data. **DNS** translates human-friendly names into IP addresses.

---

## Real World Analogy

Think of networking as the **postal system**:

- **IP address** = Street address of a building
- **Port** = Apartment number in that building
- **DNS** = The phone book that converts "google.com" to "142.250.80.46"
- **Packet** = A sealed envelope carrying a message
- **Protocol** = The postal rules (format, stamps, handling) — HTTP, TCP, UDP
- **Router** = The postal sorting facility that directs mail to the right destination

Sending a request to `http://myapp.com:8080` is like mailing a letter to:
> *142.250.x.x, Apartment 8080, New York*

---

## Why This Exists

Without networking:
- Computers would be isolated islands
- Sharing data would require physical media (USB, disk)
- Services like websites, APIs, and databases couldn't be accessed remotely

Kubernetes is a **networked system** — every pod gets an IP, services expose ports, and DNS makes discovery automatic. Understanding networking is essential to understanding how Kubernetes works.

---

## How It Works

**IP Addresses:**
- Every device on a network has a unique IP address (e.g., `192.168.1.10`)
- IPv4: four numbers 0–255 separated by dots
- IPv6: longer format for more addresses

**Ports:**
- A single machine can run many services simultaneously
- Ports (0–65535) direct traffic to the right service
- Common defaults: HTTP = 80, HTTPS = 443, SSH = 22, DNS = 53

**DNS (Domain Name System):**
1. You type `kubernetes.io` in your browser
2. Your OS asks a DNS server: "What IP is `kubernetes.io`?"
3. DNS returns: `147.75.40.148`
4. Your browser connects to that IP

**TCP vs UDP:**
- **TCP:** Reliable delivery — confirms packets arrived, resends if lost. Used by HTTP, databases.
- **UDP:** Fast, no confirmation — packets may be lost. Used by video streaming, DNS.

**HTTP Request Flow:**
```
Browser types URL
      │
      ▼
DNS lookup → gets IP
      │
      ▼
TCP connection to IP:port
      │
      ▼
HTTP request sent
      │
      ▼
Server responds with data
      │
      ▼
Browser renders page
```

---

## Visual Diagram

**Technical Diagram:**
```
[Your Machine: 192.168.1.5]
         │
         │  "I want google.com"
         ▼
[DNS Server] ──► returns 142.250.80.46
         │
         ▼
[Router: 192.168.1.1] ──► [Internet] ──► [Google Server: 142.250.80.46:443]
```

**Analogy Diagram:**
```
[You: Writing a letter]
         │
         │  "I want to reach Google"
         ▼
[Phone Book (DNS)] ──► returns "1600 Amphitheatre Pkwy, Mountain View"
         │
         ▼
[Post Office (Router)] ──► [Delivery] ──► [Google HQ, Suite 443]
```

> **Excalidraw idea:** A city map. Each building has a street address (IP). Each door has a number (port). A phone book building (DNS) in the center. Postal vans (packets) driving between buildings with labeled envelopes (protocol headers).

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **IP Address** | A numerical label assigned to each network device | The unique address of a computer on a network |
| **Port** | A number (0–65535) identifying a specific service on a host | The apartment number at the IP address |
| **DNS** | Domain Name System — resolves hostnames to IP addresses | The internet's phone book |
| **Protocol** | Rules governing data format and exchange (TCP, UDP, HTTP) | The language and rules for how data is packaged |
| **Packet** | A small chunk of data transmitted over a network | An individual envelope carrying part of a message |
| **Router** | A device that forwards packets between networks | The postal sorting facility |
| **Firewall** | A system that controls allowed network traffic | A security guard at the building entrance |
| **LoadBalancer** | Distributes traffic across multiple servers | A receptionist routing calls to available agents |
| **ClusterIP** | A virtual IP accessible only inside a Kubernetes cluster | An internal extension number |

---

## Kubernetes-Specific Networking Concepts

| K8s Concept | What It Does | Networking Parallel |
|-------------|-------------|---------------------|
| Pod IP | Each pod gets its own IP address | Each apartment has its own phone |
| Service | Stable virtual IP for a set of pods | A department's main reception number |
| ClusterDNS | K8s automatically resolves service names | Internal company phone directory |
| Ingress | Routes external HTTP traffic to services | The building's main reception desk |

---

## Common Misconceptions

- **"IP addresses are permanent"** — Pods get new IPs when recreated. This is why Services exist in Kubernetes.
- **"DNS is just for websites"** — Kubernetes uses DNS internally for service discovery between pods.
- **"HTTP and TCP are the same"** — TCP is the transport layer (handles delivery). HTTP is the application layer (the message format) that runs on top of TCP.
- **"Port 80 and 8080 are the same"** — No. They're different ports. Many dev apps run on 8080 to avoid needing root permissions (ports below 1024 require elevated permissions on Linux).

---

## Related Concepts

- [Why Orchestration?](./why-orchestration.md)
- [Kubernetes Services](../02-core-objects/services/README.md)
- [Kubernetes Networking](../03-networking/README.md)

---

## Additional Learning Resources

- [How DNS Works — Cloudflare](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [TCP/IP Illustrated (Introduction)](https://en.wikipedia.org/wiki/TCP/IP_Illustrated)
- [Networking for Beginners — freeCodeCamp](https://www.freecodecamp.org/news/computer-networking-how-applications-talk-over-the-internet/)
- [Kubernetes Networking Model](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
