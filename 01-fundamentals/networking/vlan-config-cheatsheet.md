# VLAN & Port Configuration Cheat Sheet

## Basic Configuration Access

Switch> enable

Switch# configure terminal

## Create and Name VLANs

Switch(config)# vlan VLAN-ID

Switch(config-vlan)# name NAME

Switch(config-vlan)# exit

**Example:**
Switch(config)# vlan 10

Switch(config-vlan)# name SALES

Switch(config-vlan)# vlan 20

Switch(config-vlan)# name HR

Switch(config-vlan)# vlan 30

Switch(config-vlan)# name IT

## Configure Access Port (One VLAN per Port)

Switch(config)# interface INTERFACE-ID

Switch(config-if)# switchport mode access

Switch(config-if)# switchport access vlan VLAN-ID

Switch(config-if)# spanning-tree portfast

Switch(config-if)# exit

**Example:**
Switch(config)# interface fastEthernet0/5

Switch(config-if)# switchport mode access

Switch(config-if)# switchport access vlan 10

Switch(config-if)# spanning-tree portfast

Switch(config-if)# exit

## Configure Trunk Port (Multiple VLANs Between Switches)

Switch(config)# interface INTERFACE-ID

Switch(config-if)# switchport trunk encapsulation dot1q

Switch(config-if)# switchport mode trunk

Switch(config-if)# switchport trunk allowed vlan VLAN-LIST

Switch(config-if)# exit

**Note:** `switchport trunk encapsulation dot1q` not needed on all models

**Example:**
Switch(config)# interface gigabitEthernet0/1

Switch(config-if)# switchport mode trunk

Switch(config-if)# switchport trunk allowed vlan 10,20,30

Switch(config-if)# exit

**Add VLANs without overwriting:**
Switch(config-if)# switchport trunk allowed vlan add VLAN-ID

**Remove VLANs:**
Switch(config-if)# switchport trunk allowed vlan remove VLAN-ID

## Verify Configuration

**Check VLAN list:**
Switch# show vlan brief

**Check trunk status:**
Switch# show interfaces trunk

**Check interface settings:**
Switch# show running-config interface INTERFACE-ID

## Additional Useful Commands

**Set port description:**
Switch(config)# interface INTERFACE-ID

Switch(config-if)# description <>

**Disable port:**
Switch(config)# interface INTERFACE-ID

Switch(config-if)# shutdown

**Enable port:**
Switch(config-if)# no shutdown

**Save configuration:**
Switch# write memory

or

Switch# copy running-config startup-config

## Complete Example Configuration

Switch# configure terminal

Switch(config)# vlan 10

Switch(config-vlan)# name SALES

Switch(config-vlan)# vlan 20

Switch(config-vlan)# name HR

Switch(config-vlan)# exit
___

Switch(config)# interface fa0/3

Switch(config-if)# description PC van HR

Switch(config-if)# switchport mode access

Switch(config-if)# switchport access vlan 20

Switch(config-if)# spanning-tree portfast

Switch(config-if)# exit
___

Switch(config)# interface gi0/1

Switch(config-if)# description Trunk naar Switch 2

Switch(config-if)# switchport mode trunk

Switch(config-if)# switchport trunk allowed vlan 10,20

Switch(config-if)# exit

Switch(config)# exit

Switch# write memory

## Quick Reference

| Task | Command |
|------|---------|
| Create VLAN | `vlan <ID>` + `name <NAME>` |
| Access Port | `switchport mode access` + `switchport access vlan <ID>` |
| Trunk Port | `switchport mode trunk` + `switchport trunk allowed vlan <ID>` |
| Show VLANs | `show vlan brief` |
| Show Trunks | `show interfaces trunk` |
| Save Config | `write memory`|
