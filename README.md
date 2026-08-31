# SOHO Network Design & Implementation — XYZ Company Branch (Bonalbo)

**Enterprise Network Project #2** — Cisco Packet Tracer
*Based on the project brief by Gurutech Networking Training (Benard Otom Owino)*

---

## 1. Case Study

XYZ company is a fast-growing company in Eastern Australia with more than 2 million customers globally. The company deals with selling and buying of food items, which are basically operated from the headquarters. The company is intending to open a branch near the local village Bonalbo. Thus, the company requires young IT graduates  to design the  network for the branch. The network is intended to operate separately from the HQ network.

## 2. Requirements

- One Cisco router and one Cisco switch
- Three departments: **Admin/IT**, **Finance/HR**, **Customer Service/Reception**
- Each department on a separate VLAN
- Each department has its own wireless network
- Hosts obtain IPv4 addresses automatically (DHCP)
- All departments can communicate with each other
- ISP-assigned base network: `192.168.1.0`

## 3. Technologies Implemented

1. Simple network topology (1 router, 1 switch)
2. Correct cabling (straight-through / crossover / trunk as needed)
3. VLAN creation and port assignment
4. Subnetting and IP addressing
5. Inter-VLAN routing (router-on-a-stick)
6. DHCP server configuration (router as DHCP server)
7. WLAN / access point configuration
8. Host device configuration
9. Testing and verification

---

## 4. Network Topology

*[Insert your topology screenshot here — the one you already have]*

| Device | Role |
|---|---|
| Router0 | Router-on-a-stick, DHCP server |
| Switch (multilayer/L2) | VLAN trunking, access ports |
| Access Point 0/1/2 | Wireless per department |
| PC0, PC1, PC2 | Wired department hosts |
| Printer0/1/2 | Department printers |
| Laptop0/1/2, Smartphone0/1/2, Tablet PC0 | Wireless department clients |

---

## 5. IP Addressing Plan

Base network: `192.168.1.0/24`, subnetted into three `/26` blocks (2 borrowed bits → 4 subnets of 64 hosts each, 3 used).

| Department | VLAN | Subnet | Usable Range | Gateway (Router subinterface) | Broadcast |
|---|---|---|---|---|---|
| Admin/IT | 10 | 192.168.1.0/26 | .1 – .62 | 192.168.1.1 | 192.168.1.63 |
| Finance/HR | 20 | 192.168.1.64/26 | .65 – .126 | 192.168.1.65 | 192.168.1.127 |
| CS/Reception | 30 | 192.168.1.128/26 | .129 – .190 | 192.168.1.129 | 192.168.1.191 |

*(Fill in the actual DHCP pool ranges and exclusions you configured.)*

---

## 6. Configuration Summary

### 6.1 VLAN Creation (Switch)
```
[paste your switch config commands here, e.g.]
Switch(config)#vlan 10
Switch(config-vlan)#name ADMIN-IT
...
```
📸 *Screenshot: `show vlan brief` output*

### 6.2 Trunk and Access Ports
```
[paste trunk config for the link to the router, and access port configs per VLAN]
```
📸 *Screenshot: `show interfaces trunk`*

### 6.3 Router-on-a-Stick (Inter-VLAN Routing)
```
[paste subinterface configs — e.g. GigabitEthernet0/0.10, .20, .30]
```
📸 *Screenshot: `show ip interface brief`*

### 6.4 DHCP Server Configuration
```
[paste DHCP pool configs per VLAN]
```
📸 *Screenshot: DHCP pool config + a host's `ipconfig` showing a leased address*

### 6.5 Wireless (Access Points)
```
[SSID, security mode, and VLAN mapping per department AP]
```
📸 *Screenshot: AP config GUI/CLI for each department*

### 6.6 Host Device Configuration
📸 *Screenshot: `ipconfig` on one wired and one wireless device per department*

---

## 7. Testing & Verification

| Test | From | To | Expected Result | Actual Result | Screenshot |
|---|---|---|---|---|---|
| Same-VLAN ping | PC0 (Admin) | Printer0 (Admin) | Success | | |
| Cross-VLAN ping | PC0 (Admin) | PC1 (Finance) | Success (inter-VLAN routing) | | |
| Cross-VLAN ping | PC2 (CS) | PC1 (Finance) | Success | | |
| DHCP lease | Laptop0 (wireless, Admin) | — | Gets 192.168.1.x address | | |
| Wireless connectivity | Smartphone1 (Finance) | Wired PC in same VLAN | Success | | |

Add `tracert` output for at least one cross-VLAN path to show the packet actually routes through the router subinterfaces.

---

## 8. Troubleshooting Log

| Issue | Cause | Fix |
|---|---|---|
| *e.g. AP not broadcasting SSID* | *e.g. access port on wrong VLAN* | *e.g. reassigned Fa0/2 to VLAN 10* |

---

## 9. Key Learnings

- [What subnetting/VLSM insight you gained]
- [What router-on-a-stick taught you about trunking]
- [Any DHCP scoping gotchas]
- [Anything about wireless security you'd change for production, e.g. WPA2 vs open]

---

## 10. Files in This Repo

- `soho-network-project2.pkt` — completed Packet Tracer file
- `screenshots/` — all configuration and verification screenshots
- `README.md` — this document

---

**Skills demonstrated:** VLAN segmentation, subnetting/VLSM, router-on-a-stick inter-VLAN routing, DHCP server configuration, wireless network setup, Cisco IOS CLI configuration, network testing and verification.
