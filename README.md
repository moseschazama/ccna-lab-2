# CCNALab2 – Small Enterprise Multi-Department Branch Network

![Version](https://img.shields.io/badge/version-2.0-blue)
![CCNA](https://img.shields.io/badge/CCNA-Practical%20Lab-green)
![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-orange)

A fully configured Cisco Packet Tracer lab implementing enterprise-level networking concepts including VLAN segmentation, inter-VLAN routing, NAT, DHCP, ACL security, and wireless integration.

**All devices are configured, tested, and aligned with CCNA-level design and troubleshooting scenarios.**

---

## 📋 Table of Contents

- [Network Topology](#-network-topology)
- [Lab Overview](#-lab-overview)
- [Device List](#-device-list)
- [IP Addressing Summary](#-ip-addressing-summary)
- [VLAN Summary](#-vlan-summary)
- [Technologies Implemented](#-technologies-implemented)
- [Security Policy & ACL Deep Dive](#-security-policy--acl-deep-dive)
- [Device Configurations](#-device-configurations)
- [How to Use This Repository](#-how-to-use-this-repository)
- [Verification Commands](#-verification-commands)
- [Skills Demonstrated](#-skills-demonstrated)
- [Credits](#-credits)

---

## 🗺️ Network Topology

INTERNET (8.8.8.0/24)
┌─────────────────────┐
│ DNS: 8.8.8.2 │
│ WEB: 8.8.8.3 │
│ Email: 8.8.8.4 │
│ FTP/TFTP: 8.8.8.5 │
│ NTP: 8.8.8.6 │
└──────────┬──────────┘
│
┌──────────┴──────────┐
│ Cloud Router │
│ (Simulated ISP) │
└──────────┬──────────┘
│
┌──────────┴──────────┐
│ Gateway Router │
│ (NAT, DHCP, OSPF) │
└──────────┬──────────┘
│ Trunk (802.1Q)
┌──────────┴──────────┐
│ SW1 │
│ (VLANs, Trunking, │
│ Port Security) │
└──────────┬──────────┘
│
┌──────────┬──────────┬──────────┬─────┴─────┬──────────┐
│ │ │ │ │ │
VLAN 10 VLAN 20 VLAN 30 VLAN 40 VLAN 50 WLC
ADMIN HR/FIN ACCOUNTS DELIVERY CUSTOMER + APs
192.168. 192.168. 192.168. 192.168. 192.168.
1.0/26 1.64/26 1.128/26 1.192/26 2.0/26
text


> **Note:** Add your exported Packet Tracer topology image as `/images/topology.png`

---

## 📚 Lab Overview

| Section | Description | Status |
|---------|-------------|--------|
| Part 1 | Basic Setup (hostname, interfaces, banners) | ✅ Complete |
| Part 2 | VLANs & Trunking (802.1Q) | ✅ Complete |
| Part 3 | Inter-VLAN Routing (Router-on-a-Stick) | ✅ Complete |
| Part 4 | DHCP Configuration (Per-VLAN pools) | ✅ Complete |
| Part 5 | NAT (PAT Overload to Internet) | ✅ Complete |
| Part 6 | OSPF Routing (Single Area 0) | ✅ Complete |
| Part 7 | ACL Security (Least Privilege Enforcement) | ✅ Complete |
| Part 8 | Wireless Networking (AP + VLAN mapping) | ✅ Complete |
| Part 9 | Port Security & Hardening (Sticky MAC, SSH) | ✅ Complete |

---

## 🖥️ Device List

### Routers

| Device | Role | Interfaces |
|--------|------|------------|
| Gateway Router | Inter-VLAN Routing, NAT, DHCP, OSPF | G0/0/0 (WAN), G0/0/1 (Trunk to SW1) |
| Cloud Router | Simulated Internet / ISP | G0/0/0 (to Gateway), G0/0/1 (to Servers) |

### Switches

| Device | Role | Features |
|--------|------|----------|
| SW1 | Access/Distribution | VLANs, Trunking, Port Security, SSH |

### Other Devices

| Device | Role |
|--------|------|
| Access Point | Multi-SSID Wireless (mapped to VLANs 10,20,30,40,50) |
| Wireless LAN Controller | Centralized AP management |
| Servers (x6) | DNS, Web, Email, FTP, TFTP, NTP |
| PCs (x10+) | End-user devices per department (wired + wireless) |

---

## 🌐 IP Addressing Summary

### Internal VLAN Networks (/26 subnet mask)

| VLAN | Department | Network Address | Gateway | Usable Range |
|------|------------|-----------------|---------|--------------|
| 10 | ADMIN / IT | 192.168.1.0/26 | 192.168.1.1 | 192.168.1.1 - 192.168.1.62 |
| 20 | HR / FINANCE | 192.168.1.64/26 | 192.168.1.65 | 192.168.1.65 - 192.168.1.126 |
| 30 | ACCOUNTS | 192.168.1.128/26 | 192.168.1.129 | 192.168.1.129 - 192.168.1.190 |
| 40 | DELIVERY | 192.168.1.192/26 | 192.168.1.193 | 192.168.1.193 - 192.168.1.254 |
| 50 | CUSTOMER SERVICE | 192.168.2.0/26 | 192.168.2.1 | 192.168.2.1 - 192.168.2.62 |

### WAN Link

| Link | Network | Gateway IP |
|------|---------|------------|
| Gateway Router ↔ Cloud Router | 203.13.1.0/30 | 203.13.1.1 (Gateway), 203.13.1.2 (Cloud) |

### Server Network (8.8.8.0/24)

| Service | IP Address | Port |
|---------|------------|------|
| Default Gateway | 8.8.8.1 | - |
| DNS Server | 8.8.8.2 | UDP 53 |
| Web Server (HTTP/HTTPS) | 8.8.8.3 | TCP 80, 443 |
| Email Server (SMTP/POP3) | 8.8.8.4 | TCP 25, 110, 143 |
| FTP / TFTP Server | 8.8.8.5 | TCP 20,21 / UDP 69 |
| NTP Server | 8.8.8.6 | UDP 123 |

### Management Network

| VLAN | Network | Purpose |
|------|---------|---------|
| VLAN 99 | 192.168.99.0/24 | Switch, WLC, AP management |

### Unused Ports

| VLAN | Name | Purpose |
|------|------|---------|
| VLAN 999 | PARKING_LOT | Dumping ground for unused switch ports |

---

## 🏷️ VLAN Summary

| VLAN ID | Name | Purpose | Security Level |
|---------|------|---------|----------------|
| 10 | ADMIN | Full network access for IT staff | 🔓 Unrestricted |
| 20 | HR_FINANCE | HR and Finance department | 🔒 Restricted (Web + Email only) |
| 30 | ACCOUNTS | Accounts / Billing team | 🔒 Restricted (Email only) |
| 40 | DELIVERY | Warehouse / Logistics | 🔒 Restricted (No server access) |
| 50 | CUSTOMER | Customer service representatives | 🔒 Restricted (Web only) |
| 99 | MANAGEMENT | Network device management | 🔒 Admin-only access |
| 999 | PARKING_LOT | Unused ports (disabled) | 🔒 Shutdown |

---

## ⚙️ Technologies Implemented

| Category | Technology | Details |
|----------|------------|---------|
| **Switching** | VLANs | Department segmentation (10,20,30,40,50,99,999) |
| | Trunking | 802.1Q encapsulation |
| | EtherChannel | LACP between switches (if multiple switches) |
| | Port Security | Sticky MAC, max 2 devices, violation restrict |
| **Routing** | Inter-VLAN Routing | Router-on-a-Stick with subinterfaces |
| | OSPF | Single Area 0, passive interfaces |
| | Default Route | 0.0.0.0/0 to Cloud Router |
| **IP Services** | DHCP | Router-based pools per VLAN |
| | NAT | PAT Overload on WAN interface |
| | DNS | Forwarding to 8.8.8.2 |
| **Security** | Extended ACLs | Least privilege enforcement |
| | SSHv2 | Secure remote access (no Telnet) |
| | VTY Access-class | Restrict SSH to Admin VLAN only |
| | Disabled Unused Ports | shutdown + parking lot VLAN |
| **Wireless** | Access Point | Multi-SSID |
| | VLAN Mapping | Each SSID mapped to specific VLAN |
| | DHCP over Wireless | Wireless clients get IP from router DHCP |

---

## 🔐 Security Policy & ACL Deep Dive

### The Core Principle: Least Privilege

> **"Only necessary access allowed"** – Each department gets ONLY the services required for their job function.

### Important Clarification: Public Website Access

**The company website (8.8.8.3) is PUBLIC** – anyone on the internet can access it. Therefore, **all departments can access the company website**.

**So why have ACLs?** Because ACLs restrict **OTHER services** (email, inter-VLAN communication, management access, other websites), not the public website.

---

### Department Access Matrix

| Department | VLAN | Company Website | Other Websites | Email | HR VLAN | Management |
|------------|------|----------------|----------------|-------|---------|------------|
| **ADMIN / IT** | 10 | ✅ | ✅ | ✅ | ✅ | ✅ |
| **HR / FINANCE** | 20 | ✅ | ✅ | ✅ | N/A | ❌ |
| **ACCOUNTS** | 30 | ✅ | ❌ | ✅ | ❌ | ❌ |
| **CUSTOMER SERVICE** | 40 | ✅ | ❌ | ❌ | ❌ | ❌ |
| **DELIVERY** | 50 | ✅ | ✅ | ❌ | ❌ | ❌ |

---

### Business Justification for Each ACL

#### 🔓 ADMIN (VLAN 10) – No ACL
> *"IT staff need full access to configure, troubleshoot, and manage all network devices and servers."*

#### 🔒 HR / FINANCE (VLAN 20) – Web + Email Only
> *"HR processes salaries and hiring. Finance handles company money. They need email for contracts and web for banking portals. They should NOT manage network devices."*

#### 🔒 ACCOUNTS (VLAN 30) – Email Only (No other web browsing)
> *"Accounts team has access to bank accounts and payment systems. If they browse Facebook and get malware, attackers could steal banking credentials. They ONLY need company website and email."*

#### 🔒 CUSTOMER SERVICE (VLAN 40) – Web Only + Block HR VLAN
> *"Customer service reps handle angry customers daily. High stress = high turnover = security risk. If a disgruntled ex-employee still has email access, they could impersonate the company. They also must NEVER see HR salary data."*

#### 🔒 DELIVERY (VLAN 50) – No Email (Maps + Web only)
> *"Delivery drivers leave tablets in trucks overnight. Trucks get broken into. If a thief finds an unlocked tablet with email, they can send phishing emails FROM your company domain. Drivers need maps, not email."*

---

### ACL Configuration Summary

```cisco
! ACL 1: HR/FINANCE (VLAN 20) - Web + Email only
ip access-list extended FINANCE_HR_ACL
 permit udp 192.168.1.64 0.0.0.63 any eq 53      ! DNS
 permit tcp 192.168.1.64 0.0.0.63 any eq 80      ! HTTP
 permit tcp 192.168.1.64 0.0.0.63 any eq 443     ! HTTPS
 permit tcp 192.168.1.64 0.0.0.63 any eq 25      ! SMTP
 permit tcp 192.168.1.64 0.0.0.63 any eq 110     ! POP3
 deny ip 192.168.1.64 0.0.0.63 192.168.99.0 0.0.0.255  ! Block Management
 permit ip any any

! ACL 2: ACCOUNTS (VLAN 30) - Email ONLY (block other web)
ip access-list extended ACCOUNTS_ACL
 permit udp 192.168.1.128 0.0.0.63 any eq 53
 permit tcp 192.168.1.128 0.0.0.63 host 8.8.8.3 eq 80   ! Company website only
 permit tcp 192.168.1.128 0.0.0.63 any eq 25
 permit tcp 192.168.1.128 0.0.0.63 any eq 110
 deny tcp 192.168.1.128 0.0.0.63 any eq 80              ! Block other web
 deny tcp 192.168.1.128 0.0.0.63 any eq 443             ! Block other HTTPS
 deny ip any any log

! ACL 3: CUSTOMER (VLAN 40) - Web only + BLOCK HR
ip access-list extended CUSTOMER_ACL
 deny ip 192.168.1.192 0.0.0.63 192.168.1.64 0.0.0.63   ! CRITICAL: Block HR
 permit udp 192.168.1.192 0.0.0.63 any eq 53
 permit tcp 192.168.1.192 0.0.0.63 any eq 80
 permit tcp 192.168.1.192 0.0.0.63 any eq 443
 deny tcp 192.168.1.192 0.0.0.63 any eq 25              ! Block email
 deny ip any any log

! ACL 4: DELIVERY (VLAN 50) - No email (maps + web only)
ip access-list extended DELIVERY_ACL
 permit udp 192.168.2.0 0.0.0.63 any eq 53
 permit tcp 192.168.2.0 0.0.0.63 any eq 80
 permit tcp 192.168.2.0 0.0.0.63 any eq 443
 deny tcp 192.168.2.0 0.0.0.63 any eq 25               ! Block SMTP
 deny tcp 192.168.2.0 0.0.0.63 any eq 110              ! Block POP3
 deny ip 192.168.2.0 0.0.0.63 192.168.1.0 0.0.0.255    ! Block other VLANs
 permit ip any any

Where ACLs Are Applied (Inbound on Subinterfaces)
ACL	Applied On	Direction
FINANCE_HR_ACL	G0/0.20	in
ACCOUNTS_ACL	G0/0.30	in
CUSTOMER_ACL	G0/0.40	in
DELIVERY_ACL	G0/0.50	in
Infrastructure Protection (VTY / SSH)
cisco

ip access-list standard SSH_ADMIN_ONLY
 permit 192.168.1.0 0.0.0.63    ! Only Admin VLAN can SSH
 deny any

line vty 0 4
 access-class SSH_ADMIN_ONLY in
 transport input ssh
 login local

Port Security (Per Access Port)
cisco

interface range f0/1-24
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation restrict

Unused Ports (Industry Best Practice)
cisco

vlan 999
 name PARKING_LOT

interface range f0/10-24
 shutdown
 switchport mode access
 switchport access vlan 999

📁 Device Configurations

All full device configurations are stored under:
text

configs/
├── router_gateway.txt      # Full Gateway Router config (NAT, DHCP, OSPF, ACLs)
├── router_cloud.txt        # Simulated ISP router
├── switch.txt              # SW1 config (VLANs, trunking, port security, SSH)
├── access_point.txt        # AP config (Multi-SSID, VLAN mapping)
└── wlc.txt                 # Wireless LAN Controller config (if used)

Key Configuration Highlights
Device	Key Configs
Gateway Router	Subinterfaces (10,20,30,40,50), DHCP pools, NAT overload, OSPF, ACLs, SSH
SW1	VLANs 10,20,30,40,50,99,999, trunk to router, port security, SSH
Access Point	SSIDs: Admin-WIFI, HR-WIFI, Accounts-WIFI, Customer-WIFI, Delivery-WIFI
Cloud Router	Static default route, simulated internet
🚀 How to Use This Repository
Option 1 – Packet Tracer (Build & Test)

    Open Cisco Packet Tracer (version 8.0 or higher recommended)

    Build the topology using the diagram above

    Copy configurations from /configs/ into each device's CLI

    Save the file as CCNA_Lab2.pkt

Option 2 – Study Mode (Review & Understand)

    Read the configurations line-by-line

    Understand design decisions – why each VLAN, ACL, and security feature

    Follow the ACL logic – trace how traffic flows through subinterfaces

Option 3 – Practice Mode (Rebuild from Scratch)

    Delete all configurations from devices (except hostname)

    Try to configure from memory using only the IP tables above

    Check your work against the provided configs

🧪 Verification Commands
On Gateway Router
bash

show ip interface brief          # Check all subinterfaces are up/up
show ip route                    # Verify OSPF routes and default route
show ip dhcp binding             # Verify DHCP leases per VLAN
show ip nat translations         # Verify PAT is working
show access-lists                # Check ACL hits (matches)
show running-config | section ip access-list
show logging | include deny      # View ACL block logs

On SW1
bash

show vlan brief                  # Verify VLANs and port assignments
show interfaces trunk            # Verify trunk encapsulation and allowed VLANs
show port-security               # Check sticky MAC addresses
show mac address-table           # View learned MAC addresses
show running-config | section port-security

Testing Connectivity
Test	Source	Destination	Expected Result
Ping HR gateway	Customer PC (VLAN 40)	192.168.1.65	✅ Success
Ping HR PC	Customer PC (VLAN 40)	192.168.1.66	❌ FAIL (ACL blocks Customer→HR)
Ping Web Server	Customer PC	8.8.8.3	✅ Success
Ping Email Server	Customer PC	8.8.8.4	❌ FAIL (Customer no email)
Ping Web Server	Accounts PC	8.8.8.3	✅ Success (company website allowed)
Ping Facebook	Accounts PC	any 80/443	❌ FAIL (Accounts no other web)
Ping Google Maps	Delivery tablet	any 443	✅ Success
Ping Email Server	Delivery tablet	8.8.8.4	❌ FAIL (Delivery no email)
SSH to Router	Admin PC (VLAN 10)	192.168.1.1	✅ Success
SSH to Router	HR PC (VLAN 20)	192.168.1.1	❌ FAIL (VTY access-class)
Troubleshooting Checklist

    All VLANs appear in show vlan brief

    Trunk ports show trunking and correct native VLAN

    Router subinterfaces have correct IPs and no shutdown

    DHCP pools have network and default-router configured

    ACLs applied inbound on correct subinterface

    Port security shows SecurePort MaxSecureAddr count

    Wireless clients receive IP from correct subnet

🎓 Skills Demonstrated
Core CCNA Skills
Skill	Demonstrated By
✅ VLAN segmentation	7 VLANs (10,20,30,40,50,99,999)
✅ 802.1Q trunking	SW1 trunk to router
✅ Inter-VLAN routing	Router-on-a-Stick subinterfaces
✅ DHCP configuration	Per-VLAN DHCP pools on router
✅ Static routing	Default route to ISP
✅ OSPF (single area)	Internal routing between VLANs
✅ NAT / PAT	Overload on WAN interface
✅ Extended ACLs	Least privilege enforcement
✅ Port Security	Sticky MAC, max 2 devices
✅ SSH configuration	Secure remote access
✅ Wireless integration	Multi-SSID with VLAN mapping
Advanced / Professional Skills
Skill	Demonstrated By
🔐 Management VLAN	VLAN 99 for network devices
🔒 Parking lot VLAN	VLAN 999 for unused ports
📋 ACL logging	deny any any log for troubleshooting
🛡️ VTY access-class	Restrict SSH to Admin VLAN only
🧪 Production-ready ACLs	Allow public website, block other services
📊 Business-driven security	Each ACL justified by real risk
📖 Credits

    Lab Design & Implementation: Moses Chazama

    Inspired by: Enterprise CCNA-level lab structures, Jeremy's IT Lab, and real-world branch deployments

    Cisco Packet Tracer Version: 8.2+ (recommended)

📅 Last Updated

2026-06-05
📜 License

This lab is free for educational use. Feel free to fork, modify, and share with attribution.
⭐ Found this useful?

Give the repository a ⭐ and share it with fellow CCNA students!

Generated: 2026-06-05 16:30:00 UTC

Questions or suggestions? Open an issue or submit a pull request!
text


---

## 📁 File Structure for GitHub

CCNA-Lab2/
│
├── README.md # The complete file above
├── images/
│ └── topology.png # Your exported Packet Tracer diagram
├── configs/
│ ├── router_gateway.txt # Full gateway router config
│ ├── router_cloud.txt # ISP cloud router config
│ ├── switch.txt # SW1 config
│ ├── access_point.txt # AP config
│ └── wlc.txt # WLC config (if used)
├── CCNA_Lab2.pkt # The actual Packet Tracer file
└── CHANGELOG.md # Optional: track changes
