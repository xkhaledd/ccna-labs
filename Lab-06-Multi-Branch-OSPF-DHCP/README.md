# Enterprise-Grade Multi-Branch Network Design & Dynamic Routing

<!-- Master Topology Image -->
<img width="1220" height="668" alt="photo_1_2026-05-04_20-18-32" src="https://github.com/user-attachments/assets/8e8914a6-3193-4c76-b699-0bd5f5bbdf58" />


---

## 🌐 The Vision: Building a Scalable Corporate Core
This project models a high-performance, robust, and scalable enterprise network simulation designed in **Cisco Packet Tracer**. The topology reflects a typical corporate scenario, interconnecting four isolated branches through a secure, redundant, high-speed Wide Area Network (WAN) core.

This isn't just a connectivity test; it's a deep dive into real-world network engineering concepts, demonstrating proficiency in hierarchical design, dynamic routing protocols, and automated infrastructure services.

---

## 🚀 Key Architectural Features

| Feature | Description | The "Pro" Edge |
| :--- | :--- | :--- |
| **Backbone Dynamic Routing** | OSPF (Open Shortest Path First) Area 0 | Deployed for Dijkstra-based, lightning-fast convergence and optimal path selection across WAN links. |
| **Network Redundancy** | Full Ring Topology | Implemented redundant serial links to ensure 0% packet loss even if a backbone link fails. |
| **Automated Client Services** | Centralized DHCP & Relay Agents | Deployed a central DHCP server in Branch 1 with `ip helper-address` on remote routers for automated IP allocation. |
| **Logical Addressing** | 192.168.x.x VLSM Scheme | Efficiently partitioned the address space into 8 distinct subnets for LANs and WAN links. |

---

## 🛠 Configuration Methodology

### 1. Layer 3 Routing (OSPF Adjacency)
Configured OSPF Process 1 in Area 0 across all four routers to establish full neighbor adjacencies. This ensures a converged routing table where every branch can "see" the entire network.

<!-- OSPF Neighbor Proof Image -->
<img width="702" height="715" alt="photo_3_2026-05-04_20-18-32" src="https://github.com/user-attachments/assets/f5b73352-bf05-4b64-a0a1-b76b4d5f3c7b" />


### 2. Centralized DHCP & Relay Services
To simplify network management, a centralized DHCP server was implemented. Since DHCP broadcasts do not cross routers, **DHCP Relay Agents** (IP Helper-Address) were configured on all remote gateways.

<!-- DHCP Success Proof Image -->
<img width="702" height="715" alt="photo_4_2026-05-04_20-18-32" src="https://github.com/user-attachments/assets/1c024743-f966-4bb0-82ea-eb4578fb9e4b" />


---

## 🔍 Troubleshooting Log (The Engineering Mindset)
During the implementation, several critical "real-world" networking bugs were identified and resolved:

*   **IP Overlap Conflict:** Identified and resolved administrative overlaps on serial interfaces that were preventing Layer 3 initialization.
*   **OSPF Convergence Debugging:** Optimized interface-specific parameters to achieve the **"FULL"** state across all neighbors in the Ring topology.
*   **Broadcast Isolation Resolution:** Fixed remote branch IP failures by correctly routing DHCP Discover messages to the central server via Relay Agents.

---

## 🧪 Verification & Results
The network's integrity was verified through rigorous testing:

*   **End-to-End Connectivity:** Confirmed via ICMP Ping tests from remote branches to the HQ Server.
*   **Path Efficiency:** Verified routing logic using `traceroute` to observe packet forwarding through OSPF-learned paths.
*   **Performance:** Achieved flawless connectivity with **0% packet loss** across the entire infrastructure.

<!-- Connectivity & Tracert Proof Image -->
<img width="702" height="715" alt="photo_2_2026-05-04_20-18-32" src="https://github.com/user-attachments/assets/267969d5-b847-4a07-9de5-b6c1e4e6b0a6" />
