# Lab 03: Multi-Network DHCP & Routing (Final Practice Challenge)

## Overview
This is a comprehensive configuration lab where I designed, configured, and verified a multi-network topology. The goal was to provide automatic IP addressing using DHCP from the router to devices across different subnets and ensure full connectivity.

## 1. Network Topology
Below is a screenshot of the completed and fully connected network topology:

![photo_6_2026-03-19_02-09-09](https://github.com/user-attachments/assets/7e081079-b44d-469c-a51b-f1933419db8f)

## Requirements Met
- [x] **Two Different Networks:** Configured two separate networks (192.168.30.0/24 and 192.168.40.0/24) on different router interfaces.
- [x] **Configure DHCP:** The central Router is configured as a DHCP server for both networks, providing IP addresses, subnet masks, and default gateways to all PCs.
- [x] **Full Connectivity:** Verified communication by successfully pinging between PCs across the networks (e.g., PC0 pinging PC3).

## 2. DHCP Verification
The screenshot below verifies that the PCs successfully received their IP configuration automatically from the Router acting as a DHCP server:

![photo_1_2026-03-19_02-09-09](https://github.com/user-attachments/assets/f2b2c632-6df4-483d-98c8-010f4687f3ff)

## 3. Connectivity Test (Ping)
The following ping test confirms full end-to-end routing and connectivity between the two different networks:

![photo_5_2026-03-19_02-09-09](https://github.com/user-attachments/assets/65141cfd-25a3-48bf-bbfe-76b9b4383f30)

## Router CLI Configuration

### Interface Configuration (Gateways)
```ios
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.30.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.40.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
