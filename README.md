# Cisco ASA Firewall Enterprise Lab (Packet Tracer)

## Overview

This project demonstrates a small enterprise-style network designed and configured in Cisco Packet Tracer using a Cisco ASA Firewall.

The lab includes:

- Cisco ASA Firewall configuration
- NAT/PAT configuration
- Routing setup
- Switch-based LAN architecture
- Wireless access point integration
- Server connectivity
- VLAN concepts
- ICMP inspection
- Enterprise-style topology design
- Troubleshooting and verification

---

# Network Topology

```text
                    +----------------+
                    |   Server0      |
                    +----------------+
                             |
                         +--------+
                         |Switch1 |
                         +--------+
                              |
                              |

+---------+          +----------------+          +--------+
| Router  |----------| Cisco ASA 5505 |----------|Switch0 |
+---------+          +----------------+          +--------+
                                                         |
                               +-------------------------+-------------------+
                               |                         |                   |
                           +-------+                 +-------+        +----------------+
                           | PC0   |                 | PC1   |        | Wireless Router|
                           +-------+                 +-------+        +----------------+
                                                                                 |
                                                                              WiFi
                                                                                 |
                                                                            +----------+
                                                                            | Laptop   |
                                                                            +----------+
```

---

# Technologies Used

- Cisco Packet Tracer
- Cisco ASA 5505 Firewall
- Cisco Router
- Cisco Switches
- Wireless Router (Access Point mode)
- NAT/PAT
- VLANs
- ICMP Inspection
- Static Routing

---

# IP Addressing Scheme

| Device | Interface | IP Address |
|---|---|---|
| Router | Fa0/0 | 192.168.0.1 |
| ASA Outside | VLAN2 | 192.168.0.3 |
| ASA Inside | VLAN10 | 10.0.0.1 |
| PC0 | FastEthernet0 | 10.0.0.5 |
| PC1 | FastEthernet0 | 10.0.0.6 |
| Server0 | FastEthernet0 | 10.0.0.12 |
| Laptop | Wireless0 | 10.0.0.8 |
| Wireless Router | LAN IP | 10.0.0.2 |

Subnet Mask:

```text
255.255.255.0
```

Default Gateway:

```text
10.0.0.1
```

---

# ASA Firewall Configuration

## Outside Interface

```bash
interface vlan 2
nameif outside
security-level 0
ip address 192.168.0.3 255.255.255.0
no shutdown
```

## Inside Interface

```bash
interface vlan 1
nameif inside
security-level 100
ip address 10.0.0.1 255.255.255.0
no shutdown
```

## NAT Configuration

```bash
object network INSIDE-NET
 subnet 10.0.0.0 255.255.255.0
 nat (inside,outside) dynamic interface
```

## Default Route

```bash
route outside 0.0.0.0 0.0.0.0 192.168.0.1
```

## ICMP Inspection

```bash
class-map inspection_default
 match default-inspection-traffic

policy-map global_policy
 class inspection_default
  inspect icmp

service-policy global_policy global
```

---

# Router Configuration

```bash
enable
configure terminal

interface fastethernet0/0
ip address 192.168.0.1 255.255.255.0
no shutdown

end
```

---

# Wireless Router Configuration

The wireless router was configured in Access Point mode.

## Important Configuration

- Connected using LAN/Ethernet port
- Internet/WAN port NOT used
- DHCP disabled
- Static IP assigned

### Wireless Router IP

```text
10.0.0.20
```

### Gateway

```text
10.0.0.1
```

---

# Connectivity Tests

## PC to ASA

```bash
ping 10.0.0.1
```

Result:

```text
SUCCESS
```

## ASA to Router

```bash
ping 192.168.0.1
```

Result:

```text
SUCCESS
```

## PC to Server

```bash
ping 10.0.0.12
```

Result:

```text
SUCCESS
```

## Laptop to ASA

```bash
ping 10.0.0.1
```

Result:

```text
SUCCESS
```

---

# Skills Demonstrated

- Firewall Administration
- Network Troubleshooting
- Cisco CLI Configuration
- Enterprise Network Design
- VLAN Management
- NAT Configuration
- Wireless Network Integration
- Basic Security Architecture

---

# Future Improvements

Possible future enhancements:

- VLAN20 Server Network
- Inter-VLAN Routing
- ACL Policies
- DMZ Network
- Site-to-Site VPN
- Port Forwarding
- Dual ISP Failover
- DHCP Server Integration
- DNS Server Setup
- Internet Simulation

---

# Author

Created by Naveen Patil

Cisco Packet Tracer Enterprise Firewall Lab Project
