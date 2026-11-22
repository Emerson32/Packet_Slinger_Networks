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
### 1. VLANs
Branch offices at Packet Slinger Networks have the following VLAN design:
- VLAN 10 (Management Network) - 10.0.20.0/27
- VLAN 20 (Corporate Network) -  10.0.20.32/27

1. Add VLANs to switch trunks

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface gi0/2
    BO-SW01(config-if)# switchport mode trunk
    BO-SW01(config-if)# switchport trunk allowed vlan 10,20,30,40
    BO-SW01(config-if)# switchport trunk native vlan 10
    BO-SW01(config-if)# description TRUNK_BO-SW02
    BO-SW01(config-if)# exit
    ```
    
    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface gi0/2
    BO-SW02(config-if)# switchport mode trunk
    BO-SW02(config-if)# switchport trunk allowed vlan 10,20,30,40
    BO-SW02(config-if)# switchport trunk native vlan 10
    BO-SW02(config-if)# description TRUNK_BO-SW01
    BO-SW02(config-if)# exit
    ```

2. Assign ports 5-9 to VLAN 20 on both switches

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface range gi0/5-9
    BO-SW01(config-if-range)# description CORPORATE_ACCESS
    BO-SW01(config-if-range)# switchport mode access
    BO-SW01(config-if-range)# switchport access vlan 20
    ```

    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface range gi0/5-9
    BO-SW02(config-if-range)# description CORPORATE_ACCESS
    BO-SW02(config-if-range)# switchport mode access
    BO-SW02(config-if-range)# switchport access vlan 20
    ```

3. Configure VLAN Trunks for WAPs

    **BO-SW01**
    ```cisco
    BO-SW01(config)# interface gi0/4
    BO-SW01(config)# description AP
    BO-SW01(config)# switchport mode trunk
    BO-SW01(config-if)# switchport trunk allowed vlan 20,40
    BO-SW01(config-if)# switchport trunk native vlan 20
    ```
    **BO-SW02**
    ```cisco
    BO-SW02(config)# interface gi0/4
    BO-SW02(config)# description AP
    BO-SW02(config)# switchport mode trunk
    BO-SW02(config-if)# switchport trunk allowed vlan 20,40
    BO-SW02(config-if)# switchport trunk native vlan 20
    ```

4. Assign ports 10-14 to VLAN 30 on both switches

5. Assign ports 15-16 to VLAN 40 on both switches


### 3. Router On a Stick

1. Configure router subinterfaces for each VLAN

    **BO-RTR01**
    ```cisco
    BO-RTR01> enable
    BO-RTR01# configure terminal
    BO-RTR01(config)# interface gi0/0/1.10
    BO-RTR01(config-if)# encapsulation dot1q 10
    BO-RTR01(config-if)# ip address 10.0.20.1 255.255.255.224
    BO-RTR01(config-if)# exit
    BO-RTR01(config)# interface gi0/0/1.20
    BO-RTR01(config-if)# encapsulation dot1q 20
    BO-RTR01(config-if)# ip address 10.0.20.33 255.255.255.224
    BO-RTR01(config-if)# exit
    BO-RTR01(config)# interface gi0/0/1.30
    BO-RTR01(config-if)# encapsulation dot1q 30
    BO-RTR01(config-if)# ip address 10.0.20.64 255.255.255.224
    BO-RTR01(config-if)# exit
    BO-RTR01(config)# interface gi0/0/1.40
    BO-RTR01(config-if)# encapsulation dot1q 40
    BO-RTR01(config-if)# ip address 10.0.20.96 255.255.255.224
    BO-RTR01(config-if)# exit
      ```

2. Configure DHCP scopes and then enable the router interface

    **BO-RTR01**
    ```cisco
    ! Define DCHP Pool for the Managment network
    BO-RTR01(config)# ip dhcp pool MANAGEMENT-10
    BO-RTR01(dhcp-config)# network 10.0.20.0 255.255.255.224
    BO-RTR01(dhcp-config)# default-router 10.0.20.1
    BO-RTR01(dhcp-config)# domain-name packetslinger.local
    BO-RTR01(dhcp-config)# dns-server 8.8.8.8
    BO-RTR01(dhcp-config)# exit

    ! Define DHCP pool for the Corporate network
    BO-RTR01(config)# ip dhcp pool CORPORATE-20
    BO-RTR01(dhcp-config)# network 10.0.20.32 255.255.255.224
    BO-RTR01(dhcp-config)# default-router 10.0.20.33
    BO-RTR01(dhcp-config)# domain-name packetslinger.local
    BO-RTR01(dhcp-config)# dns-server 8.8.8.8
    BO-RTR01(dhcp-config)# exit

    !Define DHCP exclusions
    BO-RTO1(config)# ip dhcp excluded-addresses 10.0.20.1 10.0.20.5
    BO-RTO1(config)# ip dhcp excluded-addresses 10.0.20.33

    !Best Practice: Now enable the router interface to avoid DHCP Binding issues
    BO-RTR01(config)# inter gi0/1
    BO-RTR01(config-if)# no shut
    BO-RTR01(config-if)# end
    BO-RTR01# wr
    ```

### 4. Configure NAT Overload for Internet Access
