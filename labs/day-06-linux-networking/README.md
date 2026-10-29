Lab 06 — Linux Network Inspection
Objective

Inspect local network interfaces, IP configuration, routing information, network connectivity, DNS resolution, and listening sockets.

Environment
Item	Value
Operating System	Ubuntu
Shell	Zsh
Lab Type	Local read-only inspection
Risk Level	Beginner
Exercise 1 — Inspect Network Interfaces
bash
# View network interfaces in brief format
ip -br addr

# View lower-level link characteristics
ip link show dev eth0

Observations: Identified the loopback interface (lo) in an UNKNOWN/UP state alongside the primary connection (eth0) running in UP status.

Exercise 2 — Inspect IP Addresses and Routes
bash
# Interrogate the kernel routing table
ip route

IP Configuration: The loopback maps to 127.0.0.1/8. The primary interface operates on a private subnet assigned via DHCP.

Routing Table: Outbound traffic targets the default router gateway (via 192.168.1.1 dev eth0).

Exercise 3 — Test Connectivity
bash
# Test internal loopback stack
ping -c 4 127.0.0.1

# Test external target reachability
ping -c 4 1.1.1.1

Results: ICMP echo tests returned 0% packet loss for both local loopback and external endpoints.

Limitations: ICMP verifies network-layer reachability but does not confirm application-layer process health.

Exercise 4 — Test DNS Resolution
bash
# Query the system name resolution engine
getent ahosts example.com

Findings: Successfully resolved human-readable hostnames to valid IP mappings via the local stub resolver.

Exercise 5 — Inspect Listening Sockets
bash
# Audit open TCP and UDP listening ports
ss -tuln

Count & Types: Identified active TCP (-t) and UDP (-u) numerical (-n) listening (-l) sockets.

Security Impact: Open sockets define the system's external attack surface; unpatched listening services pose exploitation risks.

Exercise 6 — Optional HTTPS Test
bash
# Fetch HTTP response headers from target URL
curl -I --max-time 10 https://example.com

Outcome: Received an explicit HTTP/2 200 OK header response.

Key Takeaways
Interface checks (ip -br addr) confirm link status and IP bindings.
Path queries (ip route) map traffic egress through default gateways.
Socket audits (ss -tuln) monitor listening services to reduce exposure to unauthorized access.
