# Day4-Training-ARC-13523023

# **Konfigurasi Jaringan Cisco Packet Tracer**

---

## **Topologi Jaringan**
### **Devices:**
- **Router:** Floor14
- **Switch:** Room-146, Floor14-Switch
- **PC:** Manager-A, Reception-A, Manager-B, Reception-B

### **Alamat IP**
#### **IPv4 Addressing:**
- **Manager-A:** 10.10.10.101/24 (Gateway: 10.10.10.1)
- **Reception-A:** 10.10.10.102/24 (Gateway: 10.10.10.1)
- **Manager-B:** 10.10.11.101/24 (Gateway: 10.10.11.1)
- **Reception-B:** 10.10.11.102/24 (Gateway: 10.10.11.1)

#### **IPv6 Addressing:**
- **Manager-A:** 2001:DB8:ACAD:100::50/64 (Gateway: FE80::2)
- **Reception-A:** 2001:DB8:ACAD:100::60/64 (Gateway: FE80::3)
- **Manager-B:** 2001:DB8:ACAD:200::50/64 (Gateway: FE80::2)
- **Reception-B:** 2001:DB8:ACAD:200::60/64 (Gateway: FE80::3)

---

## **Konfigurasi Router (Floor14)**
```cisco
! Konfigurasi Interface
interface GigabitEthernet0/0
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:100::1/64
 no shutdown
!
interface GigabitEthernet0/1
 ip address 10.10.11.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:200::1/64
 no shutdown
!
ip route 0.0.0.0 0.0.0.0 10.10.10.1
ipv6 route ::/0 2001:DB8:ACAD:100::1
```

---

## **Konfigurasi VLAN pada Switch (Room-146 & Floor14-Switch)**
```cisco
! VLAN Setup
vlan 10
 name MANAGEMENT
vlan 20
 name RECEPTION
!
! Konfigurasi Trunking
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown
```

---

## **Password Security**
```cisco
! Password untuk akses
enable secret cisco
line console 0
 password cisco
 login
!
line vty 0 4
 password cisco
 login
!
service password-encryption
```

---
