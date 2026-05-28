# Task 04 — Silent Transmission

## Briefing

> *"The ghost was communicating. Someone was listening. Find what was sent."*

A network capture was taken from a host suspected of beaconing to an unknown endpoint.
The traffic appears normal at first glance — standard HTTP requests, common user agents,
familiar destinations.

Look closer. Something is being sent out. Something quiet.

**File:** `ghost_traffic.pcap`

---

## Objectives

Analyse the packet capture and extract the hidden flag.

**Flag format:** `GHOSTTASK4{...}`

---

## Hints

> *Not all traffic goes where it should.*

> *The message is not in the body — it is in the header.*

> *Order matters. So does direction.*

---

## Solve Path

This task has **three layers**. Work through them in order.

**Layer 1 — Find the anomaly**  
Most traffic is normal. Something stands out — a different destination, a different port,
a regular interval. Isolate it.

**Layer 2 — Extract the hidden data**  
The suspicious packets contain something unusual in their HTTP headers.
Collect it. Order matters.

**Layer 3 — Decode**  
What you extracted is encoded. Decode it. Then apply one more transformation.

---

## Tools Suggested

| Tool | Purpose |
|---|---|
| Wireshark | Primary analysis — filter, follow streams, inspect headers |
| `tshark` | Command-line extraction of specific fields |
| Python `dpkt` / `scapy` | Scripted packet parsing |
| CyberChef | Decoding the extracted data |

**Useful Wireshark filters:**
```
http                          — show only HTTP traffic
ip.dst == <suspicious IP>     — isolate destination
http.request.line             — show all request headers
```

---

## Scoring

| Criteria | Points |
|---|---|
| Flag submitted correctly | 100 pts |
| Identified C2 IP and port | +10 pts bonus |
| Documented full decode chain | +25 pts bonus |

**Max total: 135 pts**

---

*GHOST Exercise — Blue Team Challenge Series*
