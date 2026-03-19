# Lab 03: Multi-Network DHCP & Routing (Final Practice Challenge)

## Overview
This is a comprehensive configuration lab where I designed, configured, and verified a multi-network topology. The goal was to provide automatic IP addressing using DHCP from the router to devices across different subnets and ensure full connectivity.

## Topology
Below is a screenshot of the completed and fully connected network topology:

![Network Topology](https://github.com/user-attachments/assets/33e682f0-4abd-4abf-9f68-b028f3efab57)

## Requirements Met
- [x] **Two Different Networks:** Configured two separate networks (192.168.30.0/24 and 192.168.40.0/24) on different router interfaces.
- [x] **Configure DHCP:** The central Router is configured as a DHCP server for both networks, providing IP addresses, subnet masks, and default gateways to all PCs.
- [x] **Full Connectivity:** Verified communication by successfully pinging between PCs across the networks (e.g., PC0 pinging PC3).

## Router CLI Configuration

### 1. Interface Configuration (Gateways)
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
