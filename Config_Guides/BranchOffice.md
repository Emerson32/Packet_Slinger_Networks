# Branch Office Configuration Guide

## Overview
This configuration guide contains the CLI configuration commands used to build the Branch Office Network depicted in the
[Branch Office Diagram](../Diagrams/Branch_Office_Design/Branch_Office_Diagram.png).

## Network Devices
Branch offices at Packet Slinger Networks consist of the following:
- 1 x Router
- 2 x Network Switches
- 2 x Wireless Access Points (WAP)
- 10 x Workstations

## Configuration
### 1. Base Configuration

### 2. VLANs
Branch offices at Packet Slinger Networks have the following VLAN design:
- VLAN 10 (Management Network) - 10.0.20.0/27
- VLAN 20 (Corporate Network) -  10.0.20.32/27

1. Create VLANs on both switches

    **BO-SW01**
    ```cisco
    BO-SW01> enable
    BO-SW01# configure terminal
    BO-SW01(config)# vlan 10
    BO-SW01(config)# description MANAGEMENT
    BO-SW01(config)# vlan 20
    BO-SW01(config)# description CORPORATE
    ```
    
    **BO-SW02**
    ```cisco
    BO-SW02> enable
    BO-SW02# configure terminal
    BO-SW02(config)# vlan 10
    BO-SW02(config)# description MANAGEMENT
    BO-SW02(config)# vlan 20
    BO-SW02(config)# description CORPORATE
    ```

2. Create SVI management interface on VLAN 10

    **BO-SW01**
    ```cisco
    BO-SW01# configure terminal
    BO-SW01(config)# interface vlan 10
    BO-SW01(config-if)# ip address 10.0.20.2 255.255.255.224
    BO-SW01(config-if)# no shut
    BO-SW01(config-if)# exit
    BO-SW01(config)# ip default-gateway 10.0.20.1
    ```
    
    **BO-SW02**
    ```cisco
    BO-SW02# configure teminal
    BO-SW02(config)# interface vlan 10
    BO-SW02(config-if)# ip address 10.0.20.3 255.255.255.224
    BO-SW02(config-if)# no shut
    BO-SW02(config-if)# exit
    BO-SW02(config)# ip default-gateway 10.0.20.1
    ```

3. Add VLANs to switch trunks

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface gi0/2
    BO-SW01(config-if)# switchport trunk encapsulation dot1q
    BO-SW01(config-if)# switchport mode trunk
    BO-SW01(config-if)# switchport trunk allowed vlan 10,20
    BO-SW01(config-if)# switchport trunk native vlan 10
    BO-SW01(config-if)# exit
    ```
    
    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface gi0/2
    BO-SW02(config-if)# switchport trunk encapsulation dot1q
    BO-SW02(config-if)# switchport mode trunk
    BO-SW02(config-if)# switchport trunk allowed vlan 10,20
    BO-SW02(config-if)# switchport trunk native vlan 10
    BO-SW02(config-if)# exit
    ```

4. Assign ports 5-9 to VLAN 20 on both switches

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface range gi0/5-9
    BO-SW01(config-if-range)# switchport mode access
    BO-SW01(config-if-range)# switchport access vlan 20
    ```

    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface range gi0/5-9
    BO-SW02(config-if-range)# switchport mode access
    BO-SW02(config-if-range)# switchport access vlan 20
    ```

5. Configure VLAN Trunks for WAPs

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface gi0/4
    BO-SW01(config-if)# switchport trunk encapsulation dot1q
    BO-SW01(config-if)# switchport trunk allowed vlans 10,20
    BO-SW01(config-if)# switchport trunk native vlan 10
    ```
    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface gi0/4
    BO-SW02(config-if)# switchport trunk encapsulation dot1q
    BO-SW02(config-if)# switchport trunk allowed vlans 10,20
    BO-SW02(config-if)# switchport trunk native vlan 10
    ```

### 3. Router On a Stick

### 4. Switchport Hardening

### 5. Configure NAT Overload for Internet Access
