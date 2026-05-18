# Multi-LAN RIP Network with DHCP & VLAN Configuration

**A comprehensive Cisco Packet Tracer simulation demonstrating advanced networking concepts including VLAN segmentation, inter-VLAN routing, RIP dynamic routing, and centralized DHCP services.**

![Network Topology](https://raw.githubusercontent.com/sarowarhosen01/Multi-LAN-RIP-Network-with-DHCP-VLAN-Configuration/refs/heads/main/Screenshots/Multi-LAN%20RIP%20Network%20with%20DHCP%20%26%20VLAN%20Configuration.jpg)  
*(Replace with screenshot/export of your .pkt topology or add image here)*

## Project Overview

This project implements a **multi-LAN enterprise-style network** using Cisco Packet Tracer. It features multiple departments (VLANs) connected across routers with **RIP v2** for dynamic routing, **DHCP** for automatic IP address assignment, and proper **VLAN trunking** for segmentation.

**Key Learning Outcomes & Skills Demonstrated:**
- VLAN creation and port assignment for network segmentation
- Inter-VLAN routing (Router-on-a-Stick or Layer 3 switching)
- RIP (Routing Information Protocol) v2 configuration for multi-router dynamic routing
- DHCP server configuration with multiple pools for different VLANs/subnets
- Trunk links and inter-switch connectivity
- IP addressing scheme design and subnetting
- Basic security (passwords, VTY access, etc.)
- End-to-end connectivity testing (ping, web access, etc.)

**Ideal for CCNA-level portfolio, networking students, and junior network engineers.**

## Network Topology

### Devices Used:
- **Routers**: 2–3 (e.g., 2911 or 4331 series)
- **Switches**: 2–4 Layer 2/3 switches (2960 or 3560)
- **DHCP Server**: 1 (Server-PT or router acting as DHCP)
- **End Devices**: Multiple PCs, laptops, printers per VLAN/department
- **Connections**: Ethernet, Serial (if WAN simulation), Trunk links

### High-Level Topology Description:
- **Core Routers** connected via RIP-enabled links.
- **Distribution/Access Switches** with VLANs configured.
- Multiple LANs (e.g., VLAN 10 - Admin, VLAN 20 - Sales, VLAN 30 - Engineering, VLAN 99 - Management/Native).
- Centralized or distributed DHCP serving multiple subnets.
- Full connectivity between all VLANs via routing.


## Network Topology Table

| Device Type     | Device Name       | Interface(s)              | Connected To          | VLAN / Purpose          |
|-----------------|-------------------|---------------------------|-----------------------|-------------------------|
| Router         | R1 (HQ)          | G0/0, G0/1, S0/0         | SW1, R2              | Router-on-a-Stick      |
| Router         | R2 (Branch)      | G0/0, S0/0               | R1, SW2              | RIP Neighbor           |
| Switch         | SW1 (Core)       | Multiple + Trunk ports   | R1, SW2              | VLAN Trunking          |
| Switch         | SW2 (Access)     | Access + Trunk ports     | End Devices          | Department VLANs       |
| Server         | DHCP-Server      | Ethernet                 | SW1                  | DHCP + DNS + HTTP      |
| PC Groups      | PC-VLAN10, etc.  | Ethernet                 | SW2                  | Department Clients     |

## IP Addressing Table

| VLAN / Subnet     | Network Address     | Subnet Mask     | Gateway          | DHCP Pool Range          | Purpose              |
|-------------------|---------------------|-----------------|------------------|--------------------------|----------------------|
| VLAN 10          | 192.168.10.0/24    | 255.255.255.0  | 192.168.10.1    | 192.168.10.10 - .100    | Administration      |
| VLAN 20          | 192.168.20.0/24    | 255.255.255.0  | 192.168.20.1    | 192.168.20.10 - .100    | Sales / Marketing   |
| VLAN 30          | 192.168.30.0/24    | 255.255.255.0  | 192.168.30.1    | 192.168.30.10 - .100    | Engineering / IT    |
| VLAN 99 (Native) | 192.168.99.0/24    | 255.255.255.0  | 192.168.99.1    | 192.168.99.10 - .50     | Management / Servers|
| Router-Router Link | 10.0.0.0/30       | 255.255.255.252| 10.0.0.1 / .2   | N/A                     | RIP Backbone        |


Switch(config)# interface range fa0/1 - 10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
