# 🏢 Big Office Company — Enterprise Network Lab

A simulated enterprise network built from scratch using
**Cisco Packet Tracer**, to practice Cisco networking and
Blue-Team security fundamentals.

## 📌 Overview
- 12+ Cisco devices: ISP router, edge router, Layer-3 core
  switch, and 5 access switches (HRD, Finance, IT, Guest, Server)
- 5 VLANs for department segmentation
- Inter-VLAN routing, DHCP, NAT, and static routing
- Guest isolation enforced with extended ACL + logging
- Centralized syslog server and NTP time synchronization

## 🗺️ Topology
<img width="1902" height="713" alt="Screenshot 2026-08-17 012105" src="https://github.com/user-attachments/assets/819a39a5-4fa7-4c52-bc68-e059afc4f45e" />


## 🧱 VLAN & IP Plan
| VLAN | Name   | Network       | Gateway     |
|------|--------|---------------|-------------|
| 20   | HRD    | 10.10.20.0/24 | 10.10.20.1  |
| 30   | FIN    | 10.10.30.0/24 | 10.10.30.1  |
| 40   | IT     | 10.10.40.0/24 | 10.10.40.1  |
| 50   | SERVER | 10.10.50.0/24 | 10.10.50.1  |
| 99   | GUEST  | 172.16.99.0/24| 172.16.99.1 |

## 🔐 Security Highlights
- Guest VLAN: internet allowed, all internal networks denied
  (extended ACL with `log` keyword)
- Centralized syslog server (Server1) for audit & investigation
- NTP synchronization for consistent log timestamps

## ✅ Validation
| Test | Expected | Result |
|---|---|---|
| PC receives IP from DHCP | IP 10.10.x.x | ✔ |
| Inter-VLAN ping (PC0 → PC4) | reply | ✔ |
| Internet ping (PC0 → 8.8.8.8) | reply | ✔ |
| Guest → internal server | **blocked + logged** | ✔ |

## 🐞 Troubleshooting Journal
### 1. CDP Native-VLAN Mismatch
- **Symptom:** `%CDP-4-NATIVE_VLAN_MISMATCH` on trunk link
- **Cause:** two trunk ends had different native VLANs
- **Fix:** aligned trunk configuration on both sides
- **Lesson:** always verify both ends of a trunk; mismatch
  can break segmentation and enable VLAN-hopping attacks

### 2. Router Link Down (red arrow)
- **Cause:** interface not enabled
- **Fix:** `no shutdown` on both ends
- **Lesson:** check Layer-1 before blaming Layer-3

## 🚀 How to Run
1. Install Cisco Packet Tracer 8.x
2. Open `big-office.pkt`
3. See `configs/` for full device configurations

## 👤 Author

Ibra Febriano 
[LinkedIn](https://www.linkedin.com/in/ibrafebriano)
