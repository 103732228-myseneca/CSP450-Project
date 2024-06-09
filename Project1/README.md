# CSP451 Project 1
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


## :star: Network Configuration Documentation
## Network Diagram
![Network Diagram](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/Network%20Configuration.png)

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

no dhcp-server vrf default

dhcp-server vrf default
pool 1
range 172.16.112.1 172.16.112.62 prefix-len 26
default-router 172.16.112.1
exit

dhcp-server vrf default
pool 2
range 172.16.120.1 172.16.120.62 prefix-len 26
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

## VM SETUP PC1

1. Create Ubuntu VM
2. Configure network adaptors:
   - Bridge and NAT network adaptors to ensure connectivity. The bridged adaptor connects to the lab network (through the Aruba switch), and the NAT adaptor provides internet access through the host machine.
3. Run command in terminal to add a route:
    ```bash
    sudo ip route add 172.16.120.4 via 172.16.112.1
    ```
4. Generate SSH key pair:
    ```bash
    ssh-keygen
    ```
5. Transfer the public key to PC2:
    ```bash
    scp ~/.ssh/id_rsa.pub user@172.16.120.4:~/id_rsa.pub
    ```
6. Create a new user and set a password on the server.
7. Copy your public key to the server:
    ```bash
    ssh-copy-id user@172.16.120.4
    ```
    Alternatively, you can manually copy the contents of `~/.ssh/id_rsa.pub` to the `~/.ssh/authorized_keys` file on the server.
8. Configure the `sshd_config` file to allow the new user and disable root SSH access. Edit the file:
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
    Add or modify the following directives:
    ```plaintext
    AllowUsers user
    PermitRootLogin no
    ```

## VM SETUP PC2

1. Create Ubuntu VM
2. Configure network adaptors:
   - Bridge and NAT network adaptors to ensure connectivity. The bridged adaptor connects to the lab network (through the Aruba switch), and the NAT adaptor provides internet access through the host machine.
3. Run command in terminal to add a route:
    ```bash
    sudo ip route add 172.16.112.36 via 172.16.120.1
    ```
4. Create a new user and set a password:
    ```bash
    sudo adduser newuser
    ```
    Follow the prompts to set the user password and other information.
5. Create `.ssh` directory and set permissions:
    ```bash
    mkdir -p ~/.ssh
    chmod 700 ~/.ssh
    ```
6. Configure `authorized_keys` file to allow SSH access:
    ```bash
    cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    ```
7. Configure the `sshd_config` file to allow the new user and disable root SSH access. Edit the file:
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
    Add or modify the following directives:
    ```plaintext
    AllowUsers newuser
    PermitRootLogin no
    ```
8. Restart the SSH service:
    ```bash
    sudo systemctl restart ssh
    ```

## Wireshark
[Click here for Wireshark Files](https://github.com/103732228-myseneca/CSP450-Project/tree/main/Project1/wireshark)
#### Screenshots:
- wireshark ssh from pc 1 to switch
![wireshark ssh from pc 1 to switch](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/wireshark%20ssh%20from%20pc%201%20to%20switch.png)
- wireshark ssh from pc 1 to pc 2
![wireshark ssh from pc 1 to pc 2](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/wireshark%20ssh%20from%20pc%201%20to%20pc%202.png)

## VM execute commands output
- `ip a`
![ip a](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/ip%20a.png)
- `ip route`
![ip route](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/ip%20route.png)
- The SSH result from your Ubuntu VM to your partner's VM
![SSH result](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/ssh%20result.png)
- `sshd_config` file :
[Project Configuration Files](https://github.com/103732228-myseneca/CSP450-Project/tree/main/Project1/configs)

## Switch execute commands output
- `sh ip int br`
![sh ip int br](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/sh%20ip%20int%20br.png)
- `sh vlan`
![sh vlan](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/sh%20vlan.png)
- `sh spanning-tree`
![sh spanning-tree](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/sh%20spanning-tree.png)
- `sh dhcp-server leases`
![sh dhcp-server leases](https://github.com/103732228-myseneca/CSP450-Project/blob/main/Project1/images/sh%20dhcp-server%20leases.png)
