# Enterprise-Grade Multi-Branch Network Design & Dynamic Routing

<p align="center">
  <img src="https://github.com/user-attachments/assets/6c932a0b-952a-4425-961c-bd9738d7c5eb" alt="Network Topology" width="1000">
</p>

---

## The Vision: Building a Scalable Corporate Core

This repository showcases a high-performance, robust, and scalable network simulation designed in **Cisco Packet Tracer**. The project models a typical enterprise scenario connecting multiple isolated branches through a secure, high-speed Wide Area Network (WAN) core.

This isn't just a basic connectivity test; it's a deep dive into **real-world network engineering concepts**, demonstrating proficiency in intricate subnetting, dynamic routing protocols, and automated client services.

---

## Key Architectural Features

| Feature | Description | The "Pro" Edge |
| :--- | :--- | :--- |
| **Backbone Dynamic Routing** | **OSPF (Open Shortest Path First) Area 0** | Deployed for Dijkstra-based, lightning-fast convergence and optimal path selection across WAN links. |
| **Efficient Subnetting** | **VLSM (Variable Length Subnet Masking)** | Utilizing efficient **`/30`** subnets for serial Point-to-Point links to guarantee **0% IP address exhaustion** on WAN connects. |
| **Automated Services** | **Dual-Method DHCP** | Demonstrates adaptability by deploying both dedicated **Server-Based** DHCP and **Cisco IOS CLI-Based** DHCP pools. |
| **End-to-End Visibility** | **Comprehensive Documentation** | Every node, interface, and end device is meticulously labeled with its logical address. |

---

## Meticulous IP Addressing Scheme

| Network Segment | Network ID | Subnet Mask | Gateway Interface | Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Branch A (LAN)** | `192.168.1.0` | `255.255.255.0` (`/24`) | `192.168.1.1` (`R0`) | Data/Server Subnet |
| **Branch B (LAN)** | `192.168.2.0` | `255.255.255.0` (`/24`) | `192.168.2.1` (`R2`) | Client Subnet |
| **WAN Link 1 (R0-R1)**| `10.1.1.0` | `255.255.255.252` (`/30`) | `10.1.1.1` | Serial Backbone |
| **WAN Link 2 (R1-R2)**| `10.2.2.0` | `255.255.255.252` (`/30`) | `10.2.2.1` | Serial Backbone |

---

## Configuration Deep Dive (The Runbook)

To showcase the underlying logic, here are the core Cisco IOS configurations deployed in this lab. 

### Dynamic IP Allocation (DHCP via Cisco IOS)
Instead of relying solely on GUI servers, **Router 2** was configured as a DHCP Server for Branch B using pure CLI. This ensures lightweight, automated IP leasing directly from the edge router.

```bash
! Entering Global Configuration Mode
Router> enable
Router# configure terminal

! Creating DHCP Address Pool for LAN Clients
Router(config)# ip dhcp pool LAN-B

! Defining Network Range and Subnet Mask for Branch B
Router(dhcp-config)# network 192.168.2.0 255.255.255.0

! Defining the Default Router (Gateway) for the Subnet
Router(dhcp-config)# default-router 192.168.2.1

! Exiting DHCP configuration
Router(dhcp-config)# exit
