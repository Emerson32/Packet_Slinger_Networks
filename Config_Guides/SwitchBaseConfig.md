# Switch Base Config Guide

## Overview
This configuration guide contains the CLI configuration commands used to deploy the Packet Slinger Distribtuion Networks baseline network switch configuration.

## Configuration

### 1. Hostname

```cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname BO-SW01
```

### 2. Local Authentication

```cisco
! Define a username and password
BO-SW01(config)# username cisco password <password>
! Enable the password encryption service
BO-SW01(config)# service password-encryption
! Create enable secret for privileged-exec mode
BO-SW01(config)# enable secret <secret>
! Tie console and remote login to local authentication
BO-SW01(config)# line console 0
BO-SW01(config-line)# login local
BO-SW01(config-line)# line vty 0 4
BO-SW01(config-line)# login local
BO-SW01(config-line)# transport input ssh
BO-SW01(config-line)# logging synchronous
BO-SW01(config-line)# line vty 5 15 
BO-SW01(config-line)# login local
BO-SW01(config-line)# transport input ssh
BO-SW01(config-line)# logging syncrhonous
BO-SW01(config-line)# exit
```

### 3. Login banner

```cisco
BO-SW01(config)# banner motd #
***********************************
WARNING: Authorized personnel only!
***********************************
#
```


### 4. Disable VTP

```cisco
BO-SW01(config)# vtp mode transparent
```


### 5. Defining standard VLANs

```cisco
BO-SW01(config)# vlan 10
BO-SW01(config-vlan)# name MANAGEMENT
BO-SW01(config-vlan)# vlan 20
BO-SW01(config-vlan)# name CORPORATE
BO-SW01(config-vlan)# vlan 30
BO-SW01(config-vlan)# name VOIP
BO-SW01(config-vlan)# vlan 40
BO-SW01(config-vlan)# name SECURITY
BO-SW01(config-vlan)# exit
```

### 6. Assign management SVI address
```cisco
BO-SW01(config)# interface vlan 10
BO-SW01(config-if)# ip address <IP ADDRESS> <NETMASK>
BO-SW01(config-if)# no shutdown
BO-SW01(config-if)# exit
BO-SW01(config)# ip default-gateway <GATEWAY>
! Assign last physical port to management VLAN
BO-SW01(config)# inter 1/1/<LAST_PORT_NUM>
BO-SW01(config-if)# switchport mode access
BO-SW01(config-if)# switchport access vlan 10
BO-SW01(config-if)# exit
```

### 7. Configure SSH
```cisco
BO-SW01(config)# ip domain-name psdn.local
BO-SW01(config)# crypto key generate rsa modulus 4096
BO-SW01(config)# ip ssh version 2
```

### 8. Port Descriptions

```cisco
BO-SW01(config)# inter 1/1/<LAST_PORT_NUM>
BO-SW01(config-if)# description MANAGEMENT_PORT
BO-SW01(config-if)# exit
```

### 9. Save Config

```cisco
BO-SW01(config)# end
BO-SW01# wr
```
