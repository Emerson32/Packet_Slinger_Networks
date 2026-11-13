# Switch Base Config Guide

## Overview
This configuration guide contains the CLI configuration commands used to deploy the Packet Slinger Distribtuion Networks baseline network switch configuration.

## Configuration

### 1. Hostname

```cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname BO1-SW01
```

### 2. Local Authentication

```cisco
! Define a username and password
BO1-SW01(config)# username cisco password <password>
! Enable the password encryption service
BO1-SW01(config)# service password-encryption
! Create enable secret for privileged-exec mode
BO1-SW01(config)# enable secret <secret>
! Tie console and remote login to local authentication
BO1-SW01(config)# line console 0
BO1-SW01(config-line)# login local
BO1-SW01(config-line)# line vty 0 4
BO1-SW01(config-line)# login local
BO1-SW01(config-line)# transport input ssh
BO1-SW01(config-line)# logging synchronous
BO1-SW01(config-line)# line vty 0 15 
BO1-SW01(config-line)# login local
BO1-SW01(config-line)# transport input ssh
BO1-SW01(config-line)# logging syncrhonous
BO1-SW01(config-line)# exit
```

### 3. Login banner

```cisco
BO1-SW01(config)# banner motd #
***********************************
WARNING: Authorized personnel only!
***********************************
#
```


### 4. Disable VTP

```cisco
BO1-SW01(config)# vtp mode transparent
```


### 5. Defining standard VLANs

```cisco
BO1-SW01(config)# vlan 10
BO1-SW01(config-vlan)# name MANAGEMENT
BO1-SW01(config-vlan)# vlan 20
BO1-SW01(config-vlan)# name CORPORATE
BO1-SW01(config-vlan)# vlan 30
BO1-SW01(config-vlan)# name VOIP
BO1-SW01(config-vlan)# vlan 40
BO1-SW01(config-vlan)# name SECURITY
BO1-SW01(config-vlan)# exit
```

### 6. Assign management SVI address
```cisco
BO1-SW01(config)# interface vlan 10
BO1-SW01(config-if)# ip address <IP ADDRESS> <NETMASK>
BO1-SW01(config-if)# no shutdown
BO1-SW01(config-if)# exit
BO1-SW01(config)# ip default-gateway <GATEWAY>
! Assign last physical port to management VLAN
BO1-SW01(config)# inter 1/1/<LAST_PORT_NUM>
BO1-SW01(config-if)# switchport mode access
BO1-SW01(config-if)# switchport access vlan 10
BO1-SW01(config-if)# exit
```

### 7. Port Descriptions

```cisco
BO1-SW01(config)# inter 1/1/<LAST_PORT_NUM>
BO1-SW01(config-if)# description MANAGEMENT_PORT
BO1-SW01(config-if)# exit
```

### 8. Save Config

```cisco
BO1-SW01(config)# end
BO1-SW01# wr
```
