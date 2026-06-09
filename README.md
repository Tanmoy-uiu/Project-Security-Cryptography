# Enterprise Network Design and Security Implementation using Cisco Packet Tracer

## Overview

This project demonstrates the design, configuration, and security implementation of a small enterprise network in Cisco Packet Tracer. The network was built by subnetting a Class C network into multiple LANs and implementing essential networking services such as DHCP, Static Routing, Access Control Lists (ACLs), and Port Address Translation (PAT).

The objective was to create a secure and functional network where internal users can communicate according to organizational policies while restricting unauthorized access.

---

## Network Topology

The network consists of:

* 1 Floor Router (Router0)
* 1 ISP Router (Router1)
* 3 LAN Segments
* DHCP-enabled client PCs
* Static-addressed secure department PCs
* WAN connection between Floor Router and ISP Router

---

## IP Addressing Scheme

Base Network:

```text
10.123.23.0/24
```

Subnetted into three /26 networks:

| Network Segment | Network Address  | Subnet Mask     |
| --------------- | ---------------- | --------------- |
| LAN 01          | 10.123.23.0/26   | 255.255.255.192 |
| LAN 02          | 10.123.23.64/26  | 255.255.255.192 |
| LAN 03          | 10.123.23.128/26 | 255.255.255.192 |
| WAN Link        | 201.115.2.0/30   | 255.255.255.252 |

### Router Interfaces

| Interface  | IP Address    |
| ---------- | ------------- |
| G0/0       | 10.123.23.1   |
| G0/1       | 10.123.23.65  |
| G0/2       | 10.123.23.129 |
| S0/0/0     | 201.115.2.1   |
| ISP S0/0/0 | 201.115.2.2   |

---

## Features Implemented

### 1. Subnetting

* Divided a /24 network into multiple /26 subnets.
* Each subnet supports up to 62 usable hosts.
* Designed separate broadcast domains for different departments.

### 2. DHCP Configuration

Router0 acts as the DHCP server.

Implemented DHCP pools for:

* LAN 01
* LAN 02

Automatically assigns:

* IP Address
* Subnet Mask
* Default Gateway

LAN 03 uses static IP addressing.

### 3. Static Routing

Configured a default route on Router0 to forward unknown traffic toward the ISP Router.

```bash
ip route 0.0.0.0 0.0.0.0 201.115.2.2
```

### 4. Access Control Lists (ACLs)

Implemented network security using Standard ACLs.

#### Internal Security

Protected LAN 03 from unauthorized access.

Blocked:

* LAN 01 → LAN 03
* LAN 02 → LAN 03

Allowed:

* LAN 01 ↔ LAN 02 communication

#### External Security

Blocked traffic initiated from the ISP Router toward internal private networks.

Allowed:

* Internal hosts to access external networks

Blocked:

* External hosts from accessing internal devices

### 5. Port Address Translation (PAT)

Configured NAT Overload to allow multiple internal hosts to share a single public IP address.

PAT was implemented using:

```bash
ip nat inside source list 1 interface Serial0/0/0 overload
```

Benefits:

* Conserves public IP addresses
* Allows internal users to communicate externally
* Hides private network addresses

---

## Verification and Testing

The following connectivity tests were performed:

| Test                      | Expected Result |
| ------------------------- | --------------- |
| PC0 → PC1                 | Success         |
| PC1 → PC0                 | Success         |
| PC0 → PC2                 | Blocked         |
| PC1 → PC2                 | Blocked         |
| PC0 → ISP Router          | Success         |
| ISP Router → Internal PCs | Blocked         |

Additional verification commands:

```bash
show ip interface brief
show ip route
show access-lists
show ip dhcp binding
show ip nat translations
```

---

## Technologies Used

* Cisco Packet Tracer
* IPv4 Addressing
* Subnetting
* DHCP
* Static Routing
* Standard ACL
* NAT
* PAT (NAT Overload)
* Cisco IOS CLI

---

## Learning Outcomes

Through this project I gained hands-on experience with:

* Network design and subnet planning
* Router interface configuration
* DHCP deployment
* Static routing
* Access Control Lists (ACLs)
* Network Address Translation (NAT/PAT)
* Network troubleshooting and verification

---

## Author

Student ID: 0112230123
MD. SIAM AFROZ TANMOY
Course Project – Computer Networks Laboratory
