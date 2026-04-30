# CCNA Lab 2 – Small Enterprise -Multi-Department Branch Network

A fully configured Cisco Packet Tracer lab implementing enterprise-level networking concepts including VLAN segmentation, inter-VLAN routing, NAT, DHCP, ACL security, and wireless integration.

All devices are configured, tested, and aligned with CCNA-level design and troubleshooting scenarios.

---

## 📋 Table of Contents

* Network Topology
* Lab Overview
* Device List
* IP Addressing Summary
* VLAN Summary
* Technologies Implemented
* Device Configurations
* How to Use This Repository
* Skills Demonstrated

---

## 🗺️ Network Topology

> Add your exported Packet Tracer image here:

```
/images/topology.png
```

---

## 📚 Lab Overview

| Section | Description                             | Status     |
| ------- | --------------------------------------- | ---------- |
| Part 1  | Basic Setup (hostname, interfaces)      | ✅ Complete |
| Part 2  | VLANs & Trunking                        | ✅ Complete |
| Part 3  | Inter-VLAN Routing (Router-on-a-Stick)  | ✅ Complete |
| Part 4  | DHCP Configuration                      | ✅ Complete |
| Part 5  | NAT (PAT Overload)                      | ✅ Complete |
| Part 6  | OSPF Routing                            | ✅ Complete |
| Part 7  | ACL Security (Least Privilege)          | ✅ Complete |
| Part 8  | Wireless Networking (AP + VLAN mapping) | ✅ Complete |
| Part 9  | Port Security & Hardening               | ✅ Complete |

---

## 🖥️ Device List

### Routers

| Device         | Role                          |
| -------------- | ----------------------------- |
| Gateway Router | Inter-VLAN Routing, NAT, DHCP |
| Cloud Router   | Simulated Internet            |

### Switches

| Device | Role                           |
| ------ | ------------------------------ |
| SW1    | VLANs, Trunking, Port Security |

### Other Devices

| Device       | Role                                  |
| ------------ | ------------------------------------- |
| Access Point | Multi-SSID Wireless (mapped to VLANs) |
| Servers      | DNS, Web, Email, FTP, TFTP, NTP       |
| PCs          | End-user devices per department       |

---

## 🌐 IP Addressing Summary

### Internal VLAN Networks (/26)

| VLAN | Department | Network          | Gateway       |
| ---- | ---------- | ---------------- | ------------- |
| 10   | ADMIN      | 192.168.1.0/26   | 192.168.1.1   |
| 20   | HR/FIN     | 192.168.1.64/26  | 192.168.1.65  |
| 30   | ACCOUNTS   | 192.168.1.128/26 | 192.168.1.129 |
| 40   | DELIVERY   | 192.168.1.192/26 | 192.168.1.193 |
| 50   | CUSTOMER   | 192.168.2.0/26   | 192.168.2.1   |

---

### WAN Link

| Link            | Network       |
| --------------- | ------------- |
| Gateway ↔ Cloud | 203.13.1.0/30 |

---

### Server Network

| Service  | IP      |
| -------- | ------- |
| Gateway  | 8.8.8.1 |
| DNS      | 8.8.8.2 |
| Web      | 8.8.8.3 |
| Email    | 8.8.8.4 |
| FTP/TFTP | 8.8.8.5 |
| NTP      | 8.8.8.6 |

---

## 🏷️ VLAN Summary

| VLAN | Name     | Purpose             |
| ---- | -------- | ------------------- |
| 10   | ADMIN    | Full network access |
| 20   | HR/FIN   | Email + Web only    |
| 30   | ACCOUNTS | Email only          |
| 40   | DELIVERY | No server access    |
| 50   | CUSTOMER | Web only            |

---

## ⚙️ Technologies Implemented

| Technology         | Details                         |
| ------------------ | ------------------------------- |
| VLANs              | Department segmentation         |
| Trunking           | 802.1Q                          |
| Inter-VLAN Routing | Router-on-a-Stick               |
| DHCP               | Router-based pools              |
| NAT                | PAT (overload on WAN interface) |
| OSPF               | Internal routing                |
| ACLs               | Least privilege enforcement     |
| Port Security      | Sticky MAC, max 2               |
| SSH                | Secure remote access            |
| Wireless           | Multi-SSID mapped to VLANs      |

---

## 🔐 Security Policy (ACL Enforcement)

| Department | Allowed Access |
| ---------- | -------------- |
| ADMIN      | Full access    |
| HR/FIN     | Web + Email    |
| CUSTOMER   | Web only       |
| ACCOUNTS   | Email only     |
| DELIVERY   | Blocked        |

---

## 📁 Device Configurations

All configurations are stored under:

```
configs/
├── router_gateway.txt
├── router_cloud.txt
├── switch.txt
```

---

## 🚀 How to Use This Repository

### Option 1 – Packet Tracer

1. Open Cisco Packet Tracer
2. Build topology using diagram
3. Copy configs into devices

### Option 2 – Study Mode

* Review configs line-by-line
* Understand design decisions

### Option 3 – Practice Mode

* Delete configs
* Rebuild from scratch

---

## 🧪 Verification

Use these commands:

```
show ip route
show ip nat translations
show access-lists
ping 8.8.8.3
```

Expected:

* VLAN communication works
* NAT translations appear
* ACL restrictions enforced

---

## 🎓 Skills Demonstrated

* ✅ VLAN segmentation & trunking
* ✅ Inter-VLAN routing
* ✅ DHCP configuration
* ✅ NAT/PAT implementation
* ✅ OSPF routing
* ✅ ACL-based security
* ✅ Port security hardening
* ✅ Wireless VLAN integration
* ✅ Network troubleshooting

---

## 📖 Credits

Lab designed and implemented by **Moses Chazama**
Inspired by enterprise CCNA-level lab structures.

---

## 📅 Last Updated

2026


Generated: 2026-04-30 14:01:13.986887
