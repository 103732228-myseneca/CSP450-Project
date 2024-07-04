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
![Network Diagram](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/screenshot_extras/Network%20Configuration%20Diagram.png)

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

##### VLAN 2 Configuration
- network 172.20.112.0/25
- default gateway 172.20.112.1
- dhcp pool: 172.16.112.1 - 172.16.112.126
##### VLAN 3 Configuration
- network 172.20.120.0/25
- default gateway 172.20.120.1
- dhcp pool: 172.20.120.1 - 172.20.120.126


# VM Setup (Ubuntu Oracle Box VM)
1. **Network Adapters**
- For both PCs
- Configure two network adapters:
- Adapter 1: Bridged Adapter (connects to lab network)
- Adapter 2: NAT Adapter (provides internet access)

2. **Set Up Network Configuration**
- For PC1
```bash
sudo ip route add 172.20.112.17 via 172.20.120.1
```
- For PC2
```bash
sudo ip route add 172.20.120.45 172.20.112.1
```

# Apache Web Server Setup on VM for PC1
1. **Install Apache**
```bash
sudo apt update
sudo apt install apache2
```

2. **Create Custom Webpage**
```bash
sudo tee /var/www/html/index.html <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>Project 2 for CSP450.</title>
</head>
<body>
    <h1>Hello! This is Project 2 for CSP450.</h1>
    <p>Members of this project are following their student ID number:</p>
    <ul>
        <li>Micaira Mateo - ID#103732228</li>
        <li>Prabin Acharya - ID#100706225</li>
        <li>Robert Akkerman - ID#106234206</li>
    </ul>
</body>
</html>
EOF

```

3. **Start Apache Service**
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

## Wireshark
[Click here for Wireshark Files](https://github.com/103732228-myseneca/CSP450-Project/tree/main/Project2/wireshark)
#### Screenshots:
- An SSH request from your Ubuntu VM to the Switch and the subsequent reply (2 packets) 
![SSH request from your Ubuntu VM to the Switch](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/screenshot_extras/wireshark%20screenshot%20ssh%20request%20ubuntu%20vm%20to%20switch.png)
- An SSH request from your Ubuntu VM to your partner's Ubuntu VM and the subsequent reply (2 Packets)
![SSH request from your Ubuntu VM to your partner's Ubuntu VM](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/screenshot_extras/wireshark%20screenshot%20ssh%20request%20ubuntu%20vm%20to%20partner%20vm.png)
- An HTTP request to your partner's Apache server and the subsequent response (2 Packets) 
![HTTP request to your partner's Apache server](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/screenshot_extras/wireshark%20screenshot%20http%20request%20to%20your%20partner%20apache%20server.png)
 

## VM execute commands output
- `ip a`
![ip a](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/ip%20a%20from%20pc%201.png)
- `ip route`
![ip route](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/ip%20route.png)
- The SSH result from your Ubuntu VM to your partner's VM
![SSH result](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/ssh%20result%20from%20pc%201%20to%20pc%202.png)
- `sshd_config` file :
[sshd_config file](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/configs/sshd_config)

## Switch execute commands output
- `sh ip int br`
![sh ip int br](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/sh%20ip%20int%20br.png)
- `sh vlan`
![sh vlan](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/sh%20vlan.png)
- `sh spanning-tree`
![sh spanning-tree](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/sh%20spanning-tree.png)
- `sh dhcp-server leases`
![sh dhcp-server leases](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project2/images/commands_entered/sh%20dhcp-server%20leases.png)




