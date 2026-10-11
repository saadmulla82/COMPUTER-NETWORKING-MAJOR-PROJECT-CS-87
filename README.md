# Fairoak Escape Room and Entertainment Venues

## Campus LAN Segmentation, Trunking and Spanning Tree

**Case Study No.: 87**

## Project Overview

This project focuses on designing a secure and segmented campus network for Fairoak Escape Room and Entertainment Venues. The network connects three locations: Downtown, Harbor District, and Old Mill.

The project uses VLAN segmentation, 802.1Q trunking, Spanning Tree Protocol, EtherChannel, inter-VLAN routing, Access Control Lists, and port security to improve network organization, reliability, and security.

The main objective is to separate different types of network traffic and prevent guest devices from accessing internal systems, especially the Puzzle-Control network.

## Objectives

- Divide the network into separate VLANs.
- Configure secure trunk connections between switches.
- Use VLAN 999 as the unused native VLAN.
- Configure SW-OldMill as the Spanning Tree root bridge.
- Configure EtherChannel between SW-OldMill and SW-Downtown.
- Enable inter-VLAN routing.
- Restrict Guest VLAN access to internal networks.
- Apply port security to guest access ports.
- Verify connectivity and network redundancy.

## Network Topology

The network consists of three interconnected switches arranged in a triangle.

- **SW-OldMill:** Layer 3 routing switch and STP root bridge.
- **SW-Downtown:** Supports Puzzle-Control, Staff-Booking, and IT management.
- **SW-Harbor:** Supports Puzzle-Control, Staff-Booking, Guest, and IT management.

The redundant links provide an alternative path when a network connection fails. Spanning Tree Protocol prevents Layer 2 switching loops.

## VLAN Configuration

| VLAN ID | VLAN Name | Subnet |
|---|---|---|
| 18 | Puzzle-Control | 10.10.18.0/24 |
| 28 | Staff-Booking | 10.10.28.0/24 |
| 38 | Admin | 10.10.38.0/24 |
| 48 | IT-Mgmt | 10.10.48.0/24 |
| 950 | Guest | 10.10.50.0/24 |
| 999 | Native VLAN | No user subnet |

VLAN 18 is used for Puzzle-Control, VLAN 28 for Staff-Booking, VLAN 38 for Admin, VLAN 48 for IT management, and VLAN 950 for public guest access. VLAN 999 is reserved as an unused native VLAN on trunk links.

## Technologies and Concepts Used

### VLANs

Virtual Local Area Networks separate devices into logical broadcast domains and help reduce unnecessary broadcast traffic.

### 802.1Q Trunking

Trunk links carry traffic for multiple VLANs between switches. VLAN 999 is configured as the unused native VLAN.

### Spanning Tree Protocol

STP prevents switching loops in the triangular topology. SW-OldMill is configured as the root bridge, while SW-Downtown is the backup root candidate.

### EtherChannel

EtherChannel combines two physical Gigabit Ethernet links between SW-OldMill and SW-Downtown into one logical connection using LACP.

### Inter-VLAN Routing

SW-OldMill performs Layer 3 routing between the required VLANs using Switch Virtual Interfaces and IP routing.

### Access Control Lists

The extended ACL named `GUEST-RESTRICT` blocks Guest VLAN traffic from reaching the Puzzle-Control, Staff-Booking, Admin, and IT management subnets.

### Port Security

Port security is configured on the Harbor District guest access port. It allows a maximum of two learned MAC addresses and uses the restrict violation mode with sticky MAC learning.

### VTP

VTP Transparent mode is recommended so that VLAN configuration remains locally controlled on each switch.

## IP Addressing

| VLAN | Default Gateway |
|---|---|
| Puzzle-Control | 10.10.18.1 |
| Staff-Booking | 10.10.28.1 |
| Admin | 10.10.38.1 |
| IT-Mgmt | 10.10.48.1 |
| Guest | 10.10.50.1 |

The default gateways are configured on the corresponding VLAN interfaces of SW-OldMill.

## Verification Commands

The following Cisco IOS commands are used to verify the network configuration:

```text
show vlan brief
show interfaces trunk
show spanning-tree vlan 18
show spanning-tree vlan 28
show etherchannel summary
show ip interface brief
show ip route
show mac address-table
show ip access-lists GUEST-RESTRICT
show port-security interface fa0/6
show vtp status
```

These commands help verify VLAN assignments, trunk connections, STP operation, EtherChannel status, routing, MAC address learning, ACL rules, port security, and VTP configuration.

## Testing and Expected Results

- VLANs separate network traffic according to their purpose.
- Trunk links carry the required VLAN traffic between switches.
- SW-OldMill operates as the STP root bridge.
- EtherChannel provides a logical connection using two physical links.
- Guest devices are prevented from accessing the specified internal subnets.
- Port security restricts the number of learned MAC addresses on the guest access port.
- STP restores connectivity through an alternative path when the tested link fails, after convergence.

## Security Considerations

The network uses multiple security measures to reduce unauthorized access. VLAN segmentation separates public guest traffic from internal systems, while the Guest ACL blocks access to internal subnets. Port security adds another layer of protection at the switch access port.

## Conclusion

This project demonstrates the design and configuration of a segmented campus LAN using Cisco networking concepts. VLANs organize network traffic, trunking connects the switches, STP prevents switching loops, and EtherChannel provides link redundancy. Inter-VLAN routing and ACLs control communication between networks, while port security helps protect guest access ports.

The proposed design improves network organization, reliability, and security across all three Fairoak locations.

## Project Details

- **Student Name:** Mohammed Saad Mulla
- **Roll Number:** 150096725112
- **Program:** B.Tech CSE
- **Cohort:** 2025-2029
- **Cohort Name:** Sam Altman
- **Subject:** Computer Networking and Cyber Security
- **Case Study Number:** 87
