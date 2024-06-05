# CSP451 Project 1

##### :blue_book: **COURSE INFORMATION:** Computer Systems Projects: On Premises Networking and Server Administration
##### :page_with_curl: **FULL COURSE CODE:** CSP450NDD.07194.2244 
##### :book: **INSTRUCTOR’S NAME:** Sebastian Maurice
- ##### :raising_hand: **STUDENT NAME:** Prabin Acharya
  - ##### :name_badge: Student ID# 
  - ##### :pushpin: **SUBNET NUMBER:** 112
- ##### :raising_hand: **STUDENT NAME:** Micaira Mateo
  - ##### :name_badge: Student ID# 103732228
  - ##### :pushpin: **SUBNET NUMBER:** 120


## :star: Network Configuration Documentation
## Network Diagram
Submit a Network Diagram with all pertinent information about the project.
Someone should be able to look at your diagram and understand your project well enough to build it.

![Network Diagram](insert-screenshot-here)

## Aruba 6300 Switch Configuration
##### Switch 1(on top of rack)
```
10.10.10.17/28
```
##### PC IP-Range
```
10.10.10.21-25/28 - 255.255.255.240
```
##### Vlan Configuration Commands Used
```
conf t
vlan 2
int 1/1/1
no shutdown
no routing
vlan access 2
interface vlan 2
ip address 172.16.112.1/26

conf t
vlan 3 
int 1/1/2
no shutdown
no routing
vlan access 3
interface vlan 3
ip address 172.16.120.1/26

dhcp-server vrf default
pool 1
range 172.16.112.1 172.16.112.62 prefix-len 26
default-router 172.16.112.1
exit

dhcp-server vrf default
pool 2
range 172.120.116.1 172.16.120.62 prefix-len 26
default-router 172.16.120.1
exit

dhcp-server vrf default
auto-confirm
enable
```
##### VLAN 2 Configuration
- network 172.16.112.0/26
- default gateway 172.16.112.1
- dhcp pool: 172.16.112.1 - 172.16.112.62
##### VLAN 3 Configuration
- network 172.16.120.0/26
- default gateway 172.16.120.1
- dhcp pool: 172.16.120.1 - 172.16.120.62


