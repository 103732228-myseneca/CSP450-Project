# CSP451 Project 2
## :white_check_mark: INSPECTION PASSED
##### :blue_book: **COURSE INFORMATION:** Computer Systems Projects: On Premises Networking and Server Administration
##### :page_with_curl: **FULL COURSE CODE:** CSP450NDD.07194.2244 
##### :book: **INSTRUCTOR’S NAME:** Sebastian Maurice
- ##### :raising_hand: **STUDENT NAME:** Prabin Acharya
  - ##### :name_badge: Student ID# 100706225
  - ##### :pushpin: **SUBNET NUMBER:** 112
- ##### :raising_hand: **STUDENT NAME:** Micaira Mateo
  - ##### :name_badge: Student ID# 103732228
  - ##### :pushpin: **SUBNET NUMBER:** 120
- ##### :raising_hand: **STUDENT NAME:** Robert Akkerman
  - ##### :name_badge: Student ID# 106234206
  - ##### :pushpin: **SUBNET NUMBER:** 100

## :star: Network Configuration Documentation
## Network Diagram
![Network Diagram](insert link here)

## Aruba 6300 Switch Configuration
##### Switch 1(on top of rack)
```
10.10.10.129/28
```
##### PC IP-Range
```
10.10.10.131-134/28 - 255.255.255.240
```
##### Vlan Configuration Commands Used
```
Switch1# config t
Switch1(config)# vlan 120
Switch1(config-vlan-120)# name vlan120
Switch1(config-vlan-120)# exit
Switch1(config)# vlan 112
Switch1(config-vlan-112)# name vlan112
Switch1(config-vlan-112)# exit
Switch1(config)# interface 1/1/5
Switch1(config-if)# no shutdown
Switch1(config-if)# no routing
Switch1(config-if)# vlan trunk allowed 120,112
Switch1(config-if)# exit
Switch1(config)# interface 1/1/6
Switch1(config-if)# no shutdown
Switch1(config-if)# no routing
Switch1(config-if)# vlan trunk allowed 120,112
Switch1(config-if)# exit
Switch1(config)# interface 1/1/1
Switch1(config-if)# no shutdown
Switch1(config-if)# no routing
Switch1(config-if)# vlan access 120
Switch1(config-if)# exit
Switch1(config)# int vlan 120
Switch1(config-if-vlan)# ip address 172.20.120.1 255.255.255.128
Switch1(config-if-vlan)# exit
Switch1(config)# int vlan 112
Switch1(config-if-vlan)# ip address 172.20.112.1 255.255.255.128
Switch1(config-if-vlan)# exit
Switch1(config)# int lag 1
Switch1(config-lag-if)# no shut
Switch1(config-lag-if)# no rout
Switch1(config-lag-if)# vlan trunk allowed all
Switch1(config-lag-if)# lacp mode active
Switch1(config-lag-if)# dhcp-server vrf default
Switch1(config-dhcp-server)# pool pacharya
Switch1(config-dhcp-server-pool)# exit
Switch1(config)# dhcp-server vrf default
Switch1(config-dhcp-server)# pool mica
Switch1(config-dhcp-server-pool)# range 172.20.120.1 172.20.120.126
Switch1(config-dhcp-server-pool)# default-router 172.20.120.1
Switch1(config-dhcp-server-pool)# exit
Switch1(config-dhcp-server)# pool pacharya
Switch1(config-dhcp-server-pool)# range 172.20.112.1 172.20.112.126
Switch1(config-dhcp-server-pool)# default-router 172.20.112.1
Switch1(config-dhcp-server-pool)# exit
Switch1(config-dhcp-server)# authoritative
Switch1(config-dhcp-server)# enable
```

## Aruba 2530 Series Switch Configuration
##### Switch 3
```
10.10.10.135/28
```
##### PC IP-Range
```
10.10.10.131-134/28 - 255.255.255.240
```
##### Vlan Configuration Commands Used
```
HP-2530-24-PoEP#
HP-2530-24-PoEP# config t
HP-2530-24-PoEP(config)# trunk 5-6 trk1 lacp
HP-2530-24-PoEP(config)# vlan 112
HP-2530-24-PoEP(vlan-112)# tagged trk1
HP-2530-24-PoEP(vlan-112)# untagged 1
HP-2530-24-PoEP(vlan-112)# exit
HP-2530-24-PoEP(config)# vlan 120
HP-2530-24-PoEP(vlan-120)# tagged trk1
HP-2530-24-PoEP(vlan-120)# exit
```

# VM Setup (Ubuntu Oracle Box VM)
1. **Network Adapters**
- Configure two network adapters:
- Adapter 1: Bridged Adapter (connects to lab network)
- Adapter 2: NAT Adapter (provides internet access)

2. **Set Up Network Configuration**
- For Student P's VM {PC1} (VLAN 10):
```bash
sudo ip route add 172.20.112.17 via 172.20.120.1
```
- For Student M's VM {PC2} (VLAN 20):
```bash
sudo ip route add 172.20.120.45 172.20.112.1
```

# Apache Web Server Setup on VMs
1. **Install Apache**
```bash
sudo apt update
sudo apt install apache2
```

2. **Create Custom Webpage** :pushpin: UPDATE THIS :pushpin:
```bash
echo "UPDATE THIS" | sudo tee /var/www/html/index.html
```

3. **Start Apache Service**
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

# Verification and Testing
1. **SSH from Ubuntu VM to Switch XX (Student P)**
```bash
ssh admin@172.20.112.1
```
2. **Console into Switch YY (Student M) with Putty**
3. **SSH into Partner's Ubuntu VM (Student P to Student M)**
```bash
ssh pacharya9@172.20.120.45
```
4. **Disable Root SSH Access**
```bash
sudo nano /etc/ssh/sshd_config
# Add or modify:
PermitRootLogin no
AllowUsers newuser
sudo systemctl restart ssh
```
5. **Verify Webpage on Apache Server**
```bash
curl http://172.20.120.2
```
6. **Check Internet Access**
```bash
ping google.com
```
