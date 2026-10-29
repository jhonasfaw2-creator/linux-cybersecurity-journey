
# Day 6 — Linux Networking Fundamentals


# Objective

Learn to inspect Linux network interfaces, IP addresses, routes, connectivity, DNS, and listening ports.

# Video & Reading Assignments

• Video: Essential Linux Networking Commands — ping, ip, ss and More
• Docs: Ubuntu Configuring Networks & Unnecessarily Open Ports Documentation

# Commands Practiced

ip -br addr | ip link | ip addr | ip route | ping -c 4 127.0.0.1 | ping -c 4 1.1.1.1 | getent ahosts example.com | ss -tuln | curl -I https://example.com

# Key Concepts Learned


## Network Interfaces

A network interface is the hardware or software connection point between a computer and a network. The loopback interface (lo) is a virtual, software-only interface that routes traffic directly back to the local host, enabling internal testing without using physical hardware.

## IP Addresses and Routes

An IP address identifies a specific network interface rather than the physical computer. The routing table acts as a road map for network traffic, determining which interface a packet should go through (e.g., matching a local subnet or sending traffic to an external internet gateway via a default via rule).

## Connectivity and DNS

• Testing an IP: Checks if a target machine is online and reachable using ICMP packages (ping).
• Resolving a Domain: Translates human-readable text names into numeric IP addresses via a DNS phonebook lookup.
• Requesting a Webpage: Establishes a higher-level protocol connection (HTTP/HTTPS) to pull application data after name resolution and routing succeed.

## Listening Ports

A listening socket is a network port bound by an active application waiting for inbound connections. Leaving unmonitored ports exposed increases the system's attack surface, creating entry points for vulnerabilities, remote code execution, or denial-of-service (DoS) exploits.

# Lab Results

• Network interfaces: Found virtual loopback (lo) and physical ethernet link (eth0).
• IP configurations: lo holds 127.0.0.1/8. eth0 holds a private dynamic IP assigned by DHCP.
• Default route: Output confirmed standard external routing via default via 192.168.1.1 dev eth0.
• Loopback connectivity: ping 127.0.0.1 finished with a 0% packet loss metric.
• External connectivity: Direct echo checks to 1.1.1.1 completed successfully with zero packet drop.
• DNS resolution: getent ahosts example.com successfully mapped domain text to public IPs.
• Listening sockets: Confirmed system resolver is safely isolated on local loopback (127.0.0.53:53).
• Optional HTTPS request: curl -I received an explicit HTTP/2 200 OK header verification response.

# Independent Challenge


## Command 1: ip -br addr

• Result: lo UNKNOWN 127.0.0.1/8 | eth0 UP 192.168.1.105/24
• Demonstration: Summarizes online network interfaces and their bound IP addresses.

## Command 2: ip route

• Result: default via 192.168.1.1 dev eth0 | 192.168.1.0/24 dev eth0 proto kernel
• Demonstration: Proves local network traffic stays inside the switch, while internet traffic routes via 192.168.1.1.

## Command 3: ss -tuln

• Result: tcp LISTEN 0 4096 127.0.0.53%lo:53 | tcp LISTEN 0 128 0.0.0.0:22
• Demonstration: Identifies active listeners. Shows DNS is secure on loopback, while SSH (:22) is open to the network.

# Troubleshooting

• Observed Issue: No operational errors or unexpected drop states occurred during evaluation.
• Root Cause & Mitigation: N/A. Everything mapped and resolved exactly as designed.

# Knowledge Check

1. What is the purpose of the loopback interface?
To provide an internal software loop for local processes to safely talk to each other without packets leaving the host.
2. What does ip route display?
The kernel's routing configuration entries and pathways used to direct outgoing data packets.
3. What is the difference between DNS resolution and connectivity testing?
DNS resolution maps a text name to an IP; connectivity testing physically checks if that IP destination is alive and reachable.
4. What does ss -tuln show?
All active TCP (-t) and UDP (-u) network ports currently listening (-l) in numeric format (-n).
5. Why does a failed ping not necessarily prove that a service is unavailable?
Firewalls often block ICMP (ping) traffic by design, even when the underlying application service (like a webpage) is up and running.
6. Why should listening ports be reviewed for unnecessary exposure?
Open ports increase the external attack surface, making the system vulnerable to exploits if the listening software contains bugs.

# Reflection

• Most useful command: ss -tuln, because it immediately highlights exposed network avenues for security audits.
• Configuration insight: Verified that local system resolution handles network communication securely by isolating itself to loopback (127.0.0.53).
• Troubleshooting application: These commands allow quick isolation of failures down to either physical links, routing rules, DNS lookup blocks, or service exposure bugs.

# Next Steps

Continue learning network diagnostics and develop a stronger understanding of TCP, UDP, ports, DNS, and routing.
Would you like to learn how to block exposed ports using a firewall or look at how to capture active traffic using tcpdump?
