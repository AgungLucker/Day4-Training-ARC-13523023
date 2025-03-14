# Day4-Training-ARC-13523023

Nama : Muhammad Aufa Farabi
NIM : 13523023

# Basic Network Configuration - Packet Tracer

## Addressing Table
| Device       | Interface | IPv4 Address       | IPv6 Address                  | Default Gateway |
|-------------|----------|--------------------|-------------------------------|----------------|
| Floor14     | G0/0     | 10.10.10.1/24      | 2001:DB8:ACAD:100::1/64       | N/A            |
|             | G0/1     | 10.10.11.1/24      | 2001:DB8:ACAD:200::1/64       | N/A            |
| Room-145    | VLAN 1   | 10.10.10.100/24    | -                             | 10.10.10.1     |
| Room-146    | VLAN 1   | 10.10.11.100/24    | -                             | 10.10.11.1     |
| Manager-A   | NIC      | 10.10.10.101/24    | 2001:DB8:ACAD:100::50/64      | FE80::2        |
| Reception-A | NIC      | 10.10.10.102/24    | 2001:DB8:ACAD:100::60/64      | FE80::2        |
| Manager-B   | NIC      | 10.10.11.101/24    | 2001:DB8:ACAD:200::50/64      | FE80::3        |
| Reception-B | NIC      | 10.10.11.102/24    | 2001:DB8:ACAD:200::W60/64      | FE80::3        |

## Configuration Details

### Router Configuration (Floor14)
```
enable
configure terminal
hostname Floor14

interface GigabitEthernet0/0
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:100::1/64
 no shutdown
 description Connection to Room-145 Switch

interface GigabitEthernet0/1
 ip address 10.10.11.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:200::1/64
 no shutdown
 description Connection to Room-146 Switch

exit
```

### Switch Configuration (Room-146)
```
enable
configure terminal
hostname Room-146

interface VLAN 1
 ip address 10.10.11.100 255.255.255.0
 no shutdown
 description VLAN Interface for Room-146

ip default-gateway 10.10.11.1
exit
```

### Security Configuration
```
enable secret class
line console 0
 password cisco
 login
 exit

line vty 0 4
 password cisco
 login
 exit

service password-encryption
```

### Banner Configuration
```
banner motd # Unauthorized access is prohibited! #
```
