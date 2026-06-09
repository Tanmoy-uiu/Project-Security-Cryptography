# 🌐 Enterprise Network Design and Security Implementation using Cisco Packet Tracer

## 📖 Project Overview

This project demonstrates the design, configuration, and security implementation of a small enterprise network using **Cisco Packet Tracer**. The network was developed by subnetting a Class C address space into multiple LAN segments and implementing essential networking services including **DHCP**, **Static Routing**, **Access Control Lists (ACLs)**, and **Port Address Translation (PAT)**.

The primary goal of this project was to build a secure, scalable, and efficient enterprise network that enables controlled communication between departments while preventing unauthorized access.

---

## 🏗️ Network Topology

The network infrastructure consists of:

* **1 Floor Router (Router0)**
* **1 ISP Router (Router1)**
* **3 LAN Segments**
* **DHCP-enabled Client PCs**
* **Static IP Department PCs**
* **WAN Connection between Router0 and Router1**

### Topology Highlights

* Separate subnet for each department
* Dynamic IP allocation through DHCP
* Secure department protected by ACLs
* Internet connectivity through NAT/PAT
* Restricted inbound access from external networks

---

## 🌍 IP Addressing Scheme

### Base Network

```text
10.123.23.0/24
```

### Subnet Allocation

| Network Segment | Network Address | CIDR | Subnet Mask     |
| --------------- | --------------- | ---- | --------------- |
| LAN 01          | 10.123.23.0     | /26  | 255.255.255.192 |
| LAN 02          | 10.123.23.64    | /26  | 255.255.255.192 |
| LAN 03          | 10.123.23.128   | /26  | 255.255.255.192 |
| WAN Link        | 201.115.2.0     | /30  | 255.255.255.252 |

### Router Interface Configuration

| Device        | Interface | IP Address    |
| ------------- | --------- | ------------- |
| Router0       | G0/0      | 10.123.23.1   |
| Router0       | G0/1      | 10.123.23.65  |
| Router0       | G0/2      | 10.123.23.129 |
| Router0       | S0/0/0    | 201.115.2.1   |
| Router1 (ISP) | S0/0/0    | 201.115.2.2   |

---

# ⚙️ Features Implemented

## 1️⃣ Network Subnetting

The original `/24` network was divided into three `/26` subnets to create separate broadcast domains for different departments.

### Benefits

* Improved network organization
* Reduced broadcast traffic
* Enhanced security and management
* Up to **62 usable hosts** per subnet

---

## 2️⃣ DHCP Configuration

**Router0** functions as the DHCP server for dynamic host configuration.

### DHCP Pools Configured

* LAN 01
* LAN 02

### Automatically Assigned Parameters

* IP Address
* Subnet Mask
* Default Gateway

### Static Addressing

LAN 03 devices use manually configured static IP addresses for enhanced control and security.

---

## 3️⃣ Static Routing

A default route was configured on Router0 to forward all unknown traffic toward the ISP router.

### Configuration

```bash
ip route 0.0.0.0 0.0.0.0 201.115.2.2
```

### Purpose

* Enables external connectivity
* Simplifies routing configuration
* Directs internet-bound traffic to the ISP

---

## 4️⃣ Access Control Lists (ACLs)

Standard ACLs were implemented to enforce internal and external security policies.

### 🔒 Internal Security Policy

Protected the secure department (LAN 03) from unauthorized access.

#### Blocked Traffic

* LAN 01 ➜ LAN 03
* LAN 02 ➜ LAN 03

#### Allowed Traffic

* LAN 01 ↔ LAN 02

### 🌐 External Security Policy

Prevented external devices from initiating communication with internal hosts.

#### Allowed

* Internal hosts accessing external networks

#### Blocked

* ISP Router accessing private LAN resources

---

## 5️⃣ Port Address Translation (PAT)

PAT (NAT Overload) was configured to allow multiple internal hosts to share a single public IP address.

### Configuration

```bash
ip nat inside source list 1 interface Serial0/0/0 overload
```

### Advantages

* Conserves public IPv4 addresses
* Enables internet access for all internal hosts
* Hides private IP addresses from external networks
* Enhances network security

---

# 🧪 Verification & Testing

The following connectivity tests were conducted to validate network functionality and security policies.

| Test Scenario             | Expected Result |
| ------------------------- | --------------- |
| PC0 → PC1                 | ✅ Success       |
| PC1 → PC0                 | ✅ Success       |
| PC0 → PC2                 | ❌ Blocked       |
| PC1 → PC2                 | ❌ Blocked       |
| PC0 → ISP Router          | ✅ Success       |
| ISP Router → Internal PCs | ❌ Blocked       |

---

## 🔍 Verification Commands

```bash
show ip interface brief
show ip route
show access-lists
show ip dhcp binding
show ip nat translations
```

These commands were used to verify:

* Interface status
* Routing table entries
* ACL functionality
* DHCP address assignments
* NAT/PAT translations

---

# 🛠️ Technologies Used

| Technology          | Purpose               |
| ------------------- | --------------------- |
| Cisco Packet Tracer | Network Simulation    |
| IPv4 Addressing     | Network Communication |
| Subnetting          | Network Segmentation  |
| DHCP                | Dynamic IP Allocation |
| Static Routing      | Traffic Forwarding    |
| Standard ACLs       | Access Control        |
| NAT                 | Address Translation   |
| PAT (NAT Overload)  | Internet Connectivity |
| Cisco IOS CLI       | Device Configuration  |

---

# 🎯 Learning Outcomes

This project provided practical experience in:

* Enterprise network design
* IP subnet planning and implementation
* Router and interface configuration
* DHCP deployment and management
* Static routing configuration
* Access Control List (ACL) implementation
* NAT and PAT configuration
* Network troubleshooting and verification
* Network security policy enforcement

---

# 🚀 Project Objectives Achieved

✅ Network segmentation through subnetting

✅ Dynamic IP assignment using DHCP

✅ Secure communication policies using ACLs

✅ Internet connectivity through NAT/PAT

✅ Protection against unauthorized external access

✅ Successful verification of all network services

---

# 👨‍💻 Author

**MD. Siam Afroz Tanmoy**

**Student ID:** 0112230123

**Course:** Computer Networks Laboratory

**Project:** Enterprise Network Design and Security Implementation using Cisco Packet Tracer

---

> This project demonstrates the practical implementation of core networking concepts including subnetting, routing, DHCP, ACLs, and NAT/PAT in a simulated enterprise environment using Cisco Packet Tracer.
