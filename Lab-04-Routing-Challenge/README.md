# Lab 04: Advanced Routing Protocols Challenge (Static, RIPv2, OSPF)

## Overview

This is a comprehensive configuration lab where I designed, configured, and verified a multi-router chain topology on Cisco Packet Tracer. The core objective was to establish full end-to-end connectivity between isolated LANs by progressively deploying, troubleshooting, and testing three different routing methods: **Static Routing**, **RIP Version 2**, and **OSPF Area 0**.

---

## 1. Network Topology & Design

Below is a screenshot of the completed, fully connected, and symmetrically designed network topology:

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/dae4f06d-0f32-4098-a7f7-39ce8a4984ed" width="100%">
</div>
<br>

### Requirements Met:
- [x] **Chain Topology:** Built a 3-router infrastructure (R0-R1-R2) ensuring correct physical layer connectivity using appropriate crossover and straight-through cabling.
- [x] **IP Addressing & VLSM:** Configured completely isolated local networks (`192.168.1.0/24` and `192.168.2.0/24`) and optimized Point-to-Point WAN links using `/30` subnet masks to conserve IP space.
- [x] **Routing Evolution:** Successfully transitioned the network's core from manual **Static Routing**, to distance-vector **RIPv2** (with `no auto-summary`), and finally to a highly scalable link-state **OSPF Area 0** architecture.

---

## 2. Routing Verification & Analysis

The following side-by-side analysis demonstrates the successful implementation of OSPF and the resulting flawless End-to-End connectivity.

<br>

<table align="center">
  <tr>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/872aa69e-4325-4b92-81e9-0b03e5718378" width="100%">
      <br>
      <i>Image 1: OSPF Adjacency (FULL State) & Routing Table Verification</i>
    </td>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/3880f462-bbd8-4c30-be72-001df3033a45" width="100%">
      <br>
      <i>Image 2: ICMP Ping Connectivity Test (0% Packet Loss)</i>
    </td>
  </tr>
</table>

<br>

---

## 3. Complete CLI Configuration Guide

Below is the step-by-step CLI configuration I applied to achieve the final topology, covering everything from basic interface setup to advanced dynamic routing.

### Phase 0: Base IP & Interface Configuration
Activating ports and assigning IPs using VLSM (/24 for LANs, /30 for WAN links).

**Router 0 (R0):**
```text
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface gigabitEthernet 0/1
ip address 10.0.12.1 255.255.255.252
no shutdown
exit
```

**Router 1 (R1 - Transit):**
```text
enable
configure terminal
interface gigabitEthernet 0/0
ip address 10.0.12.2 255.255.255.252
no shutdown
exit
interface gigabitEthernet 0/1
ip address 10.0.23.1 255.255.255.252
no shutdown
exit
```

**Router 2 (R2):**
```text
enable
configure terminal
interface gigabitEthernet 0/0
ip address 10.0.23.2 255.255.255.252
no shutdown
exit
interface gigabitEthernet 0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

---

### Phase 1: Static Routing Implementation
Manually defining next-hop IP addresses to route traffic to remote networks.

**R0:**
```text
ip route 10.0.23.0 255.255.255.252 10.0.12.2
ip route 192.168.2.0 255.255.255.0 10.0.12.2
```
**R1:**
```text
ip route 192.168.1.0 255.255.255.0 10.0.12.1
ip route 192.168.2.0 255.255.255.0 10.0.23.2
```
**R2:**
```text
ip route 10.0.12.0 255.255.255.252 10.0.23.1
ip route 192.168.1.0 255.255.255.0 10.0.23.1
```

---

### Phase 2: RIPv2 Implementation (Dynamic Distance-Vector)
Removing static routes and implementing RIP version 2, disabling auto-summary to support our VLSM scheme.

**Clearing Static Routes (All Routers):**
```text
no ip route [Network] [Mask] [Next-Hop]
```

**R0:**
```text
router rip
version 2
no auto-summary
network 192.168.1.0
network 10.0.0.0
```
**R1:**
```text
router rip
version 2
no auto-summary
network 10.0.0.0
```
**R2:**
```text
router rip
version 2
no auto-summary
network 192.168.2.0
network 10.0.0.0
```

---

### Phase 3: OSPF Area 0 Implementation (Dynamic Link-State)
Removing RIP and establishing OSPF adjacencies using precise Wildcard Masks.

**Clearing RIP (All Routers):**
```text
no router rip
```

**R0:**
```text
router ospf 1
router-id 1.1.1.1
network 192.168.1.0 0.0.0.255 area 0
network 10.0.12.0 0.0.0.3 area 0
```
**R1:**
```text
router ospf 1
router-id 2.2.2.2
network 10.0.12.0 0.0.0.3 area 0
network 10.0.23.0 0.0.0.3 area 0
```
**R2:**
```text
router ospf 1
router-id 3.3.3.3
network 10.0.23.0 0.0.0.3 area 0
network 192.168.2.0 0.0.0.255 area 0
```
