**Configuration Settings**

* **Enable Password :**
  - `enable secret cisco` 
* **Username and Password:**
  - `username admin secret cisco` 
* **Timezone:**
  - `clock timezone UTC+2 2 0` 
* **Domain Name :**
  - `ip domain-name companyXYZ_2.sk` (Configure a domain name for name resolution within the network, if applicable)
* **Name Server :**
  - `ip name-server 172.16.50.0` (IP address of the DNS server for network resource resolution)

**Spanning Tree and VLAN Allocation**

* **VLAN Mode :**
  - `spanning-tree mode rapid-pvst` (Enables Rapid PVST+ for spanning-tree protocol, if not already configured)
* **VLAN Allocation Policy :**
  - `vlan internal allocation policy ascending` (Sets VLAN ID allocation to ascending order, if not the default behavior)


**VLAN Creation**

* **Create VLAN:**
  - `vlan 50` 
* **VLAN Name :**
  - `name Servers_DC`

**Interfaces configuration**

* **GigabitEthernet 0/0**

    - `interface GigabitEthernet0/2`
    - `description Link to ASAv-I`
    - `ip address 172.16.0.6 255.255.255.252`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/1**

    - `interface GigabitEthernet0/2`
    - `description Link to ASAv-I`
    - `ip address 172.16.0.6 255.255.255.252`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/2**

    - `interface GigabitEthernet0/2`
    - `description Link to Serv1`
    - `switchport access vlan 50`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/3**
    - `interface GigabitEthernet0/2`
    - `description Link to Serv1`
    - `switchport access vlan 50`
    - `no shutdown`
    - `exit`

* **EtherChannel**
    - `interface range gigabitethernet 0/2-3`
    - `channel-group 1 mode on`

* **VLAN Interface (Inter-VLAN Communication):**
    - `interface Vlan 50`
    - `ip address 172.16.50.254 255.255.255.0` 


**Security**

* **Using SSH version 2**
    - `ip ssh version 2` (Enforce SSH version 2 for more secure connections)
    - `ip domain-name companyXYZ_2.sk`
    - `crypto key generate rsa modulus 4096`
* **Restrecting remote access only to SSH**
    - `line vty 0 1500`
    - `transport input ssh`
    - `login local `
* **Message digest (MD5) authentication password**
    - `area 0 authentication message-digest`
    - `key 36 md5 key_for_md5`
    - `area 0 authentication message-digest-key 36`

**NTP Synchronization**

* Configure NTP
    - `ntp server 172.16.50.1`
    - `clock timezone UTC+2 +2`

**Loggins**

* Enable logging for network events:
    - `logging host 172.16.50.1`
    - `logging trap notifications`


