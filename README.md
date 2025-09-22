

# Routing, Switching, and ACL Labs in Cisco Packet Tracer

## 🖥️ VLAN and Switching

### Topology

![Lab 4 Topology]("E:\CNMANG\LAB5\topology 1.png")

### Objective
Based on the topology and requirements:
- Create VLANs to segment a network into multiple broadcast domains.
- Assign switch ports to the correct VLANs and subnets.  

Zone 1 has 4 VLANs:
§ VLAN 10: 192.168.0.0/24 PC11, PC13, PC15
§ VLAN 11: 192.168.1.0/24 PC12
§ VLAN 12: 192.168.2.0/24 PC14
§ VLAN 13: 192.168.3.0/24 PC15

Zone 2 has 3 VLANs:
§ VLAN 20: 172.20.0/16 PC21, PC22, PC23, PC25
§ VLAN 21: 192.21.0.0/16 PC24
§ VLAN 22: 192.22.0.0/16 PC26

Zone 3 (network: 192.168.8.0/24) has 5 VLANs:
§ VLAN 31: PC31, PC33, PC35
§ VLAN 32: PC32
§ VLAN 33:
§ VLAN 34:
§ VLAN 35: PC36

- Configure trunk links for inter-switch communication.  


### General Commands
```bash
# On the switch
vlan <VLAN_ID>
 name <VLAN_NAME>

interface <interface_id>
 switchport mode access
 switchport access vlan <VLAN_ID>

# Trunk port
interface <interface_id>
 switchport mode trunk
 switchport trunk allowed vlan <VLAN_LIST>
````

### Verification

```bash
show vlan brief
show interfaces trunk
```

---

## 🔀 Inter-VLAN Routing

### Objective

Enable communication between VLANs using one of three methods:

1. **Legacy routing** — each VLAN connected to a physical router interface.
2. **Router-on-a-stick** — single router interface with subinterfaces for each VLAN.
3. **Layer 3 switch routing** — switch acts as the router using switched virtual interfaces (SVIs).

### General Commands

#### Router-on-a-Stick

```bash
interface g0/0.<subinterface>
 encapsulation dot1q <VLAN_ID>
 ip address <IP> <MASK>
```

#### Layer 3 Switch

```bash
interface vlan <VLAN_ID>
 ip address <IP> <MASK>
 no shutdown

ip routing   # enables L3 routing
```

### Verification

```bash
ping <IP_of_other_VLAN>
show ip route
```

---

## 🔐 Access Control Lists (ACLs)

### Objective

Control traffic between VLANs or networks according to policy. Implement ACLs and apply them in the correct direction/interface to satisfied these requirements:

1. Configure an ACL on router R1 to deny all traffic from PC21 (Zone2) to PC11(Zone1), but allow all other traffic.
2. Create an ACL on router R2 that blocks HTTP traffic (port 80) from any
device in Zone2 to any device in Zone3, while allowing all other protocols.
3. Design and implement ACLs on routers R1 and R2 with these requirements:
- Zone1 devices can only access Zone3 devices using SSH (port 22).
- Zone2 devices cannot access Zone1 at all.
- Zone3 devices can freely communicate with Zone1 but only HTTP/HTTPS with Zone2
4. PC26 (Zone 2) cannot ping PC16 (Zone 1), but PC16 can ping PC26.

---

## ✅ Final Verification Checklist

* `show vlan brief` → VLANs created and ports assigned.
* `show interfaces trunk` → trunk links operational.
* `ping` between VLAN hosts → connectivity as designed.
* `show ip route` → router or L3 switch has routes for all VLANs.
* ACL test cases: verify blocked and allowed traffic using ping, HTTP, SSH, or other services.
* `show access-lists` → confirm ACL entries and counters.

---

## 📂 Repository Contents

* **LAB.pkt** — Cisco Packet tracer file.
* **README.md** — This combined summary with steps and verification.

---


