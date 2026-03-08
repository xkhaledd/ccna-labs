# 🖧 Lab 2: Routing Basics & End-to-End Connectivity

## 🎯 Objective
Build and connect two different subnets using a Router, ensuring successful internal and external ICMP traffic (Ping). This lab was part of "Session 2 - Network Basics".

## 🛠️ Network Topology & Addressing
- **Network 1:** `192.168.10.0/24` (Gateway: `192.168.10.1`)
- **Network 2:** `192.168.20.0/24` (Gateway: `192.168.20.1`)
- **Hardware:** 1x Cisco 1941 Router, 2x Cisco 2960 Switches, 4x PCs.

## ⚙️ Key Configurations & Troubleshooting
1. **IP Addressing:** Assigned static IPs, Subnet Masks, and Default Gateways to all end devices.
2. **Router Setup:** Configured and enabled (`no shutdown`) GigabitEthernet interfaces `G0/0` and `G0/1` with their respective Gateway IPs.
3. **Traffic Control (Cleanup):** Disabled unnecessary background traffic (STP BPDUs, CDP, and DTP) using interface-level filters (`spanning-tree bpdufilter`, `switchport nonegotiate`) and global commands (`no cdp run`) to optimize the simulation environment.

## ✅ Verification
- Successful Ping between PCs in the **same subnet** (Switching).
- Successful Ping between PCs in **different subnets** (Routing).

### 📸 Screenshots
![photo_3_2026-03-08_03-05-50](https://github.com/user-attachments/assets/512b820c-c60e-4625-94f3-3f0fe4c86eda)
![photo_2_2026-03-08_03-05-50](https://github.com/user-attachments/assets/dc2a288e-a47b-4ca2-8367-d9232fbd7385)

