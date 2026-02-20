# IP Architecture Across Modern Networks
**How One Protocol Connects Cloud Infrastructure, IoT Devices and 5G/6G Mobile Networks**

> Academic research presentation — University of Western Macedonia, Computer Science  
> Author: Dimitrios Dalaklidis | Course: Network Design

---

## The Business Problem

Every technology investment a modern organisation makes — migrating workloads to the cloud, deploying IoT sensors on a factory floor, rolling out 5G connectivity for a mobile workforce — depends on a single, invisible foundation: the Internet Protocol.

Most decision-makers treat IP as a given. It just works. But the reality is that IP behaves very differently depending on the environment it operates in, and those differences have direct consequences for infrastructure cost, system reliability, scalability, and vendor selection.

**This project answers three questions that any technology-dependent organisation should be asking:**

> *Is our cloud architecture using IP correctly — or are we paying for isolation we're not actually getting?*

> *Can our IoT deployment scale to tens of thousands of devices — or will IP addressing become a bottleneck?*

> *What does an all-IP 5G network actually mean for our latency-sensitive applications — and what trade-offs are we accepting?*

---

## What This Project Covers

The analysis examines IP not as a static standard but as a living design decision — one that gets adapted, compressed, extended and reimagined depending on the demands of the environment it serves. Three domains are examined in depth, then synthesised into a cross-domain comparison.

### 1. IP in Cloud Infrastructure

Modern cloud environments are built on virtualisation — millions of VMs and containers that need to communicate as if they share a single flat network, while remaining completely isolated from each other. IP is what makes this illusion possible.

The key mechanisms examined:

**Virtual networking** — Each VM or container receives its own virtual IP interface, allowing cloud platforms to treat every workload as an independent network node regardless of its physical location in a datacenter.

**VXLAN overlay networks** — By encapsulating Ethernet frames inside IP/UDP packets, VXLAN allows up to 16 million logically isolated tenant networks to coexist on the same physical Layer 3 fabric. Each tenant is identified by a unique VXLAN Network Identifier (VNI) — invisible to the workload, managed entirely by the hypervisor.

**Hardware offloading** — At cloud scale, processing IP headers in software becomes a CPU bottleneck. Modern NICs offload checksum calculation and encapsulation directly to hardware. Multiqueue NICs allow parallel processing of multiple IP flows simultaneously — sustaining performance in high-density VM environments without scaling CPU spend linearly.

**Key business insight:** When a cloud provider promises tenant isolation, VXLAN and overlay networking is the mechanism delivering that promise. Understanding this helps organisations ask better questions during vendor evaluation — and spot gaps in architecture proposals.

### 2. IP in IoT — The Constrained Device Challenge

Extending IP to IoT is not straightforward. The same protocol that runs on a cloud server with terabytes of RAM needs to operate on a microcontroller with 10 kilobytes. This required not optimisation but fundamental redesign.

The RFC 7228 classification of constrained IoT nodes sets the context:

| Class | RAM | IP Capability |
|---|---|---|
| Class 0 | < 10 KiB | Cannot run IP stack — requires gateway proxy |
| Class 1 | ~10 KiB | Needs 6LoWPAN + lightweight stack (uIP/lwIP) |
| Class 2 | ~50 KiB | Can run full protocols — with energy management |

The three adaptations that make IP viable at this scale:

**IPv6** — IPv4's 4 billion addresses are exhausted. IPv6 provides 340 undecillion addresses, stateless autoconfiguration, and simpler header processing — non-negotiable for deploying billions of devices without manual address management.

**6LoWPAN header compression** — IPv6 headers are 40 bytes. An IEEE 802.15.4 wireless frame is 127 bytes total. 6LoWPAN compresses those headers to 2–3 bytes, making IP transmission physically possible on constrained wireless links.

**Lightweight OS stacks** — Contiki and RIOT implement event-driven TCP/IP designed for minimal memory and energy footprint, enabling real-time IP communication on hardware that has less processing power than a 1980s home computer.

**Key business insight:** Any IoT deployment at scale is an IPv6 deployment. Organisations still running IPv4-only infrastructure — whether on-premise or in their cloud provider configuration — are building an architecture that cannot accommodate IoT growth without costly rework.

### 3. IP in 5G/6G — The All-IP Mobile Network

5G represents a complete architectural shift: every signal — voice, data, control, signalling — travels over IP. There are no legacy circuit-switched paths. This simplification brings significant capability, but also new design challenges.

The four areas examined:

**All-IP convergence** — Eliminating circuit-switched infrastructure removes entire layers of network complexity, enabling fixed and mobile networks to share management tooling and scale together on common IP infrastructure.

**Mobility and handover** — Proxy Mobile IPv6 (PMIPv6) keeps a user's IP address stable as they move between base stations. Session and Service Continuity (SSC) modes ensure handovers complete without dropping active sessions — critical for applications where a single dropped packet has consequences (financial transactions, surgical robotics, autonomous vehicles).

**Network slicing with SRv6** — Segment Routing over IPv6 allows a single physical network to be partitioned into isolated virtual networks, each with independent QoS parameters. One infrastructure simultaneously serves an autonomous vehicle requiring sub-millisecond latency, a video streaming platform requiring high throughput, and a smart meter network requiring low power — all over the same IP fabric.

**MEC and edge computing** — Multi-access Edge Computing pushes processing physically closer to users, using IP-aware routing and SmartNICs to serve latency-sensitive applications without the round-trip to a central datacenter. URLLC (Ultra-Reliable Low Latency Communications) applications target sub-1ms response times — achievable only when IP processing overhead is offloaded to hardware at the edge.

**Key business insight:** 5G is not just faster 4G. It is a fundamentally different network architecture where IP configuration choices — which slicing strategy, which mobility protocol, where to place edge compute — determine whether latency-sensitive applications are viable or not. These are infrastructure decisions with direct product and service implications.

---

## Cross-Domain Synthesis

|  | Cloud | IoT | 5G / 6G |
|---|---|---|---|
| **Scale** | Millions of VMs & containers | Billions of constrained nodes | Billions of mobile users |
| **Key technologies** | VXLAN, overlay networks | 6LoWPAN, IPv6 compression | SRv6, PMIPv6, MEC |
| **Primary challenge** | Isolation & scalability | Energy & memory | Latency & mobility |
| **IP's role** | Routes between virtual entities | Universal address for tiny devices | All-IP convergence & slicing |

The pattern across all three domains is consistent: IP succeeds not by staying fixed, but by being adapted — through encapsulation in cloud, through compression in IoT, through extension in 5G. The organisations that extract the most value from these technologies are the ones whose architects understand which adaptation is required for which environment.

---

## Skills Demonstrated

This project was structured to demonstrate the ability to take deeply technical material and reframe it around business decisions and organisational consequences — the core competency of a technology consultant.

**Technical foundations applied:**
- IP protocol analysis across three distinct architectural contexts
- Network virtualisation (VXLAN, overlay networks, SDN concepts)
- Constrained network design (6LoWPAN, RFC 7228, embedded OS stacks)
- Mobile network architecture (5G core, PMIPv6, SRv6, MEC)
- Academic research synthesis across 4 IETF RFCs and peer-reviewed papers

**Consulting-relevant capabilities demonstrated:**
- Translating protocol-level decisions into infrastructure and vendor evaluation questions
- Structuring a multi-domain technical analysis with a consistent evaluative framework
- Identifying the business consequence of each technical trade-off — not just describing the trade-off itself
- Communicating to multiple audiences: the cross-domain table serves a CTO; the domain sections serve an architect; the key insights serve a procurement lead

---

## References

1. M. Mahalingam et al., *Virtual eXtensible Local Area Network (VXLAN)*, RFC 7348, IETF, 2014
2. C. Bormann et al., *Terminology for Constrained-Node Networks*, RFC 7228, IETF, 2014
3. G. Mulligan, *The 6LoWPAN Architecture*, ACM EmNets, 2007
4. I. Shayea et al., *Key Challenges, Drivers and Solutions for Mobility Management in 5G Networks*, IEEE Access, 2020

---

## About

**Dimitrios Dalaklidis** is a Computer Science student at the University of Western Macedonia (expected graduation July 2026) with hands-on experience in backend systems, TCP/IP networking, Linux internals, and containerisation. This presentation was produced as part of a Network Design course and represents an applied exercise in evaluating infrastructure architecture across multiple technology domains.

📧 dalaklidesdemetres@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/dimitris-dalaklidis)  
💻 [GitHub](https://github.com/DimitriosDalaklidhs)
