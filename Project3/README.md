# CSP451 Project 3
## :white_check_mark: INSPECTION PASSED
##### :blue_book: **COURSE INFORMATION:** Computer Systems Projects: On Premises Networking and Server Administration
##### :page_with_curl: **FULL COURSE CODE:** CSP450NDD.07194.2244 
##### :book: **INSTRUCTOR’S NAME:** Sebastian Maurice
### Team Members:
<details>
  <summary>View Team Members here</summary>
- ##### :raising_hand: **STUDENT NAME:** Micaira Mateo
  - ##### :name_badge: Student ID# 103732228
  - ##### :pushpin: **SUBNET NUMBER:** 120
- ##### :raising_hand: **STUDENT NAME:** Robert Akkerman
  - ##### :name_badge: Student ID# 106234206
  - ##### :pushpin: **SUBNET NUMBER:** 100
- ##### :raising_hand: **STUDENT NAME:** Prabin Acharya
  - ##### :name_badge: Student ID# 100706225
  - ##### :pushpin: **SUBNET NUMBER:** 112
- ##### :raising_hand: **STUDENT NAME:** Ched Duloy 
  - ##### :name_badge: Student ID# 185662210
  - ##### :pushpin: **SUBNET NUMBER:** 113
- ##### :raising_hand: **STUDENT NAME:** Eliza May Silvestre 
  - ##### :name_badge: Student ID# 186630216 
  - ##### :pushpin: **SUBNET NUMBER:** 114
</details>

## :star: Network Configuration Documentation
## Network Diagram
![Network Diagram](insert link here)

## Aruba 6300 Switch Configuration
<details>
<summary>Click here to see Switch 1 and 2 and PC IP-Range configurations</summary>

  ##### Switch 1(on top of rack)
```
10.10.10.33/28
```
  ##### Switch 2(below Switch 1)
```
10.10.10.34/28
```

##### PC IP-Range
```
10.10.10.35-38/28 - 255.255.255.240
```

  ##### Configuration Commands Used for SWITCH-AA
[SWITCH-AA-Configuration](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/switch-aa-config-setup.txt)
  ##### Configuration Commands Used for SWITCH-BB
[SWITCH-CC-Configuration](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/switch-cc-config-setup.txt)
</details>

## Aruba 2530/2540 Series Switch Configuration
<details>
<summary>Click here to see Switch 3 and 4 configurations</summary>

  ##### Switch 3 (below Switch 2)
```
COM4
```
  ##### Switch 4 (below Switch 3)
```
COM3
```

  ##### Configuration Commands Used for SWITCH-BB
[SWITCH-BB-Configuration](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/switch-bb-config-setup.txt)
  ##### Configuration Commands Used for SWITCH-DD
[SWITCH-DD-Configuration](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/switch-dd-config-setup.txt)
</details>

## Wireshark
[Click here for Wireshark Files](https://github.com/103732228-myseneca/CSP450-Project/tree/main/Project3/wireshark_files/pcapng_files)

#### Screenshots:
- An SSH request from your Ubuntu VM to the Switch and the subsequent reply (2 packets)
![wireshark-sc-1]()

- On OSPF Packet, Any source/destination
![wireshark-sc-2]()

- An SSH request from your Ubuntu VM to your partner's Ubuntu VM and the subsequent reply (2 Packets)
![wireshark-sc-3]()

- An HTTP request to your partner's Apache server and the subsequent response (2 Packets)
![wireshark-sc-4]()

- A MariaDB request to your partner's MariaDB server and the subsequent response (2 Packets) 
![wireshark-sc-5]()

## Ubuntu VM execute commands output
- ip a 
![ubuntu-vm-sc-1]()

- ip route 
![ubuntu-vm-sc-2]()

- The SSH result from your Ubuntu VM to your parnter's VM 
![ubuntu-vm-sc-3]()

- Connect to your partner's Apache server and display the web page 
![ubuntu-vm-sc-4]()

- Connect to your parnter's MariaDB server as a Read-Only user and try to modify the database contents 
![ubuntu-vm-sc-5]()

## sshd_config file
[Click here to view](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/sshd_config)

## NFTABLES script
[Click here to view](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project3/config_files/nftables.conf)

## Switch execute commands output
- sh ip int br 
![switch-sc-1]()

- sh vlan 
![switch-sc-1]()

- sh spanning-tree 
![switch-sc-1]()

- sh ip route
![switch-sc-1]()
