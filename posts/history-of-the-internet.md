---
title: "History of the Internet
slug: "history-of-the-internet"
date: "2025-04-30"
tags: ["internet", "history"]
cover: 
author: "Yehuda Freedman"
---

# A Developer’s Grand Tour Through the History & Architecture of the Internet
*From Cold‑War packet dreams to QUIC‑powered streams — now with deeper dives into every layer.*

> “The Internet is a 60‑year bug‑fix.” — someone on IRC, probably  
> “And we’re still `tcpdump`‑ing why.” — you, tomorrow morning

---

## 0. Reading Roadmap
- **🕰️ Part I (Sections 1‑6)** – *Chronology*: year‑by‑year breakthroughs.  
- **📚 Part II (Sections 7‑13)** – *Layer‑by‑Layer*: Physical → Application in modern detail.  
- **🛠️ Part III (Sections 14‑15)** – *Toolbox*: key RFCs, labs, emulators, books.

Scroll, skim, Ctrl‑F, or dive line‑by‑line — it’s all Markdown, so steal what you need.

---

## Part I — Chronology of Breakthroughs

### 1. Thought Experiments & First Packets (1960‑1969)

Before the Net there was telephony: synchronous, circuit‑switched, expensive. Two overlapping research threads flipped that paradigm:

| Year | Who/Where | What Happened | Proto‑DevOps Takeaway |
|------|-----------|---------------|-----------------------|
| **1961** | Leonard Kleinrock (MIT) | Queuing theory papers solve “burst traffic” maths. | Statistical multiplexing beats over‑provision. |
| **1964** | Paul Baran (RAND) | 11‑volume plan for a bomb‑proof, distributed mesh. | *Resilience by design*, not firewall‑afterthought. |
| **1965–67** | Donald Davies (NPL, UK) | Coins **packet**; builds a store‑and‑forward switch. | Independent confirmation = idea has legs. |
| **1969** | ARPANET–IMP #1 shipped by BBN | UCLA ⇋ SRI ⇋ UCSB ⇋ Utah at 50 kbps. | First backbone, first remote `login` (“LO…”) |

<small>*- Lesson #1: Packets trump circuits; software can heal blown links faster than humans rerouting copper.*</small>

---

### 2. Making It Work (1970‑1979)

> “If we can connect four sites, why not all of them?” — Vint Cerf, paraphrased

Key protocol plumbing solidifies:

* **1971 – Email**: Ray Tomlinson hacks `SNDMSG` + `CPYNET`; `user@host` syntax sticks.
* **1973 – Ethernet**: Bob Metcalfe’s memo proposes CSMA/CD; collisions are not bugs, they’re features.
* **1974 – TCP v1**: Cerf & Kahn publish the inter‑networking spec (single monolithic header).
* **1978 – TCP v3** splits into **TCP + IP**; the “hourglass waist” is born.
* **1978‑79 – Van Jacobson** patches congestion collapse (window backoff, AIMD).

---

### 3. From Research Net to *Internet* (1980‑1989)

| Date | Milestone | Why It’s Huge |
|------|-----------|---------------|
| **1983‑01‑01** | **Flag Day**: NCP off, **TCP/IP** on. | Every host must speak packets. |
| 1983 | **DNS** replaces `HOSTS.TXT`. | Names scale; `/etc/hosts` retires. |
| 1986 | **NSFNET**: gov’t backbone, 56 kbps → 1.5 Mbps. | Universities get on. |
| 1989 | **BGP (RFC 1105)** | Autonomous routing; commercial ISPs possible. |
| 1989 | **WWW proposal** by Tim Berners‑Lee. | Hypertext over TCP; next decade decided. |

---

### 4. Commercial Explosion (1990‑1999)

GUI browsers land; modem screeches become household sounds.

| Year | Event | Layer Impact |
|------|-------|--------------|
| 1991 | **HTTP/0.9 + HTML** open‑sourced. | Application |
| 1993 | **Mosaic 1.0** ships. | UX matters. |
| 1994 | **SSL 2.0** (Netscape) draft. | Transport security |
| 1994 | **NAT** (RFC 1631). | “Private 10/8 forever” |
| 1996 | **HTTP/1.0** formal (RFC 1945). | Caching, headers, status codes. |
| 1997 | **Wi‑Fi 802.11‑1997** (2 Mbps DSSS) | Link |
| 1998 | **Akamai CDN** launch. | Edge, Performance |
| 1998 | **IPv6** (RFC 2460). | Network |
| 1999 | **TLS 1.0** (RFC 2246). | Deprecates SSL |

---

### 5. Scale, Speed & Security (2000‑2009)

* **2000 – Dot‑com bust** clears hype, leaves fiber.  
* **2004 – AJAX** (Gmail) demonstrates async JS.  
* **2005 – YouTube** → birth of massive HTTP progressive download, then adaptive streaming.  
* **2008 – Chrome + V8** crank JS from KB/s to MB/s JIT compile speeds.  
* **2009 – SPDY** shows multiplexing fixes HoL blocking.

---

### 6. Modern Era (2010 → 2025)

| Year | Milestone | Why You Should Care |
|------|-----------|---------------------|
| 2012 | **QUIC** rolls out @ Google. | UDP, 0‑RTT, head‑of‑line freedom. |
| 2015 | **HTTP/2** (RFC 7540). | Binary frames; HPACK header compression. |
| 2015 | **Let’s Encrypt** begins. | Free DV certs → HTTPS everywhere. |
| 2018 | **TLS 1.3** (RFC 8446). | 1‑RTT handshake, AEAD ciphers. |
| 2022 | **HTTP/3** (RFC 9114). | QUIC becomes de‑facto web transport. |
| 2024 | **BBRv3** drafts. | Fairer, faster congestion flow. |

---

## Part II — Layer‑by‑Layer Deep Dive

The Internet stack is often depicted as OSI‑7 or TCP/IP‑4. Reality: an *hourglass* where the narrow waist (IP) allows innovation above and below.

### 7. Physical Layer – *Photons & Volts*

* **Copper**: early 56 kbps DDS, T‑1 (1.544 Mbps, 24 × 64 kbps DS0) lines.  
* **Coax (DOCSIS)**: shared RF channels; now DOCSIS 4 hitting 10 Gbps down.  
* **Fiber**: DWDM packs 64+ lambdas × 100 Gbps per strand; coherent optics overcome dispersion.  
* **Wireless**:  
  * **Wi‑Fi 6E (802.11ax)** – OFDMA + 6 GHz band.  
  * **5G NR** – sub‑6 GHz & mmWave, flexible numerology, standalone core.  
* **New hotness**: LEO satellite constellations (Starlink, OneWeb) using phased‑array beam‑forming.

### 8. Link/Access Layer – *Local Framing & MACs*

| Tech | Medium | MAC Features |
|------|--------|--------------|
| **Ethernet** | Twisted‑pair/Fiber | CSMA/CD (legacy) → full‑duplex switching; 10 Mbps → 400 GbE (802.3bs). |
| **Wi‑Fi** | 2.4/5/6 GHz | CSMA/CA + RTS/CTS; roaming with 802.11r/k/v. |
| **MPLS** | Fiber trunks | Label‑switched paths (Layer 2.5) for QoS. |
| **DOCSIS** | Hybrid Fiber‑Coax | Time‑division upstream scheduling. |

### 9. Network Layer – *IP & Friends*

* **IPv4** (RFC 791, 1981): 32‑bit, fragmentation at routers (discouraged today), best‑effort.  
* **IPv6** (RFC 8200, updated): 128‑bit, fixed 40‑byte header, extension headers, no NAT.  
* **ICMP**: diagnostics (`ping`, `traceroute` TTL‑poke).  
* **BGP‑4**: path‑vector; attributes (AS‑PATH, LOCAL_PREF, MED), route reflectors, communities.  
* **MPLS/BGP‑VPN**: isolates tenant VRFs over provider backbones.  
* **Anycast**: same /32 (/128) announced from many POPs; DNS roots, CDNs.

### 10. Transport Layer – *Bytes & Congestion*

| Protocol | Use‑case | Notable RFCs | Congestion Algorithms |
|----------|----------|--------------|-----------------------|
| **TCP** | Reliable stream | 793, 1122, 6298 | Tahoe, Reno, NewReno, CUBIC, BBR. |
| **UDP** | Unreliable datagram | 768 | None (apps roll their own). |
| **QUIC** | Reliable streams over UDP + TLS 1.3 | 9000, 9001 | CUBIC/BBR inside. |

TCP flow control = **rwnd**; congestion control = **cwnd**. Modern Linux defaults: CUBIC (2006, scalable) or BBR (2016, bottleneck bandwidth + RTT model).

### 11. Session / Presentation – *State & Security*

* **TLS Evolution**  
  * SSL 2 (’94) → SSL 3 (’96) → TLS 1.0 (’99) → TLS 1.2 (’08) → **TLS 1.3 (’18)**.  
  * Key exchange: RSA → DH → ECDHE.  
  * Record ciphers: 3DES → AES‑GCM → ChaCha20‑Poly1305.  
  * Certificate chain → OCSP → **Certificate Transparency** logs.  
* **gRPC / HTTP framing**: Protobuf messages over HTTP/2 streams, binary headers.

### 12. Application Layer – *Human & Machine Protocols*

* **WWW**: HTML (structure) + CSS (style) + JS (logic).  
* **HTTP** versions:  
  * 0.9 (single line), 1.0 (headers), 1.1 (persistent + chunked), 2 (binary frames), 3 (QUIC).  
* **DNS**: UDP 53, TCP fallback, EDNS0 extensions, DNSSEC, DoH/DoT encryption.  
* **Email**: SMTP (push) + POP3/IMAP (pull) + SPF/DKIM/DMARC anti‑spoof.  
* **Realtime**: RTP/SRTP for media, WebRTC (ICE + DTLS‑SRTP).  
* **overlay networks**: Tor onion routing, IPFS content‑addressable transport.

### 13. Cross‑Cutting Concerns

* **CDNs**: hierarchical caching, anycast DNS, smart load balancing → sub‑100 ms global RTT.  
* **Edge Compute**: Cloudflare Workers, AWS Lambda@Edge run JS/WebAssembly at PoPs.  
* **Observability**: packet capture (`tcpdump`), flow logs (NetFlow/IPFIX), active probes.  
* **Security**: HSTS preload lists, CSP, SameSite cookies, Zero Trust overlay (WireGuard, Tailscale).

---

## Part III — Toolbox for Future Packet Whisperers

### 14. Must‑Read RFCs & Drafts

| RFC | Topic | Quick Value |
|-----|-------|-------------|
| 791 | IP | Header layout: version, IHL, flags. |
| 793 | TCP | State machine diagrams. |
| 1034‑5 | DNS | Zones, SOA, glue. |
| 1918 | Private IPv4 | 10/8, 172.16/12, 192.168/16 ranges. |
| 2460 • 8200 | IPv6 original & updated. |
| 7540 | HTTP/2 | Frame types, HPACK table. |
| 8446 | TLS 1.3 | 1‑RTT handshake. |
| 9000‑9001 | QUIC transport + recovery. |
| 9114 | HTTP/3 | Mapping to QUIC streams. |

### 15. Hands‑On Labs

* **Mininet** – emulate SDN topologies on a laptop.  
* **netem/tc** – simulate latency & loss.  
* **Wireshark** – protocol dissector (filters like `quic && tls.handshake`).  
* **Container labs** – run FRRouting + BGP peering in Docker (`docker compose up bgp-lab`).  
* **Book shelf**:  
  * “TCP/IP Illustrated” Vol 1‑3 (Stevens).  
  * “BGP for Cisco Networks” (Stewart).  
  * “HTTP: The Definitive Guide” (Gourley).

---

## Final ASCII Map (Cheat Sheet)

```text
  Users ─►  Browser ─►  HTTP/3  ─► QUIC  ─►  IPv6  ─►   Wi‑Fi 6E   ─►  Fiber   ─►  CDN Edge
        ╰──────────── telemetry ◄───────── gRPC ◄────────────── TLS 1.3 ◄──────╯

