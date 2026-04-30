# CCNA Lab 2 – Finalized Enterprise Branch Network

## 📌 Overview
This project implements a full CCNA-level enterprise branch network with:
- VLAN segmentation
- Inter-VLAN routing (Router-on-a-Stick)
- NAT (PAT)
- OSPF routing
- DHCP services
- Wireless per VLAN (multi-SSID via AP)
- Extended ACL (Least Privilege enforcement)
- Port Security + SSH

## 🧱 VLAN Design (/26)
| VLAN | Department | Network |
|------|------------|--------|
| 10 | ADMIN | 192.168.1.0/26 |
| 20 | HR/FIN | 192.168.1.64/26 |
| 30 | ACCOUNTS | 192.168.1.128/26 |
| 40 | DELIVERY | 192.168.1.192/26 |
| 50 | CUSTOMER | 192.168.2.0/26 |

## 🌐 WAN
203.13.1.0/30 → Gateway ↔ Cloud

## ☁️ Server Network
8.8.8.0/24
- DNS: 8.8.8.2
- WEB: 8.8.8.3
- EMAIL: 8.8.8.4
- FTP/TFTP: 8.8.8.5
- NTP: 8.8.8.6

## 🔐 Security Policy
| Dept | Access |
|------|--------|
| ADMIN | FULL |
| HR | WEB + EMAIL |
| CUSTOMER | WEB ONLY |
| ACCOUNTS | EMAIL ONLY |
| DELIVERY | BLOCKED |

## 📡 Wireless
One AP → multiple SSIDs mapped to VLANs

## 🚀 Usage
1. Import configs
2. Assign cables
3. Test connectivity (ping, traceroute)

Generated: 2026-04-30 14:01:13.986887
