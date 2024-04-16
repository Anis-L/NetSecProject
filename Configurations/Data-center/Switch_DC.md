**Configuration Settings**

**VLAN Creation**

* **Create VLAN:**
  - `vlan 50` 
* **VLAN Name :**
  - `name Servers_DC`

**Interfaces configuration**

* **GigabitEthernet 0/2 and 0/3 (Server1 Connection):**

    - `interface GigabitEthernet0/2`
    - `description Link to Serv1`
    - `switchport access vlan 50`
    - `no shutdown`
    - `exit`
    
    - `interface GigabitEthernet0/2`
    - `description Link to Serv1`
    - `switchport access vlan 50`
    - `no shutdown`
    - `exit`



**SSH configuration**

* **Using SSH version 2**
    - `ip ssh version 2`
    - `ip domain-name companyXYZ.sk`
    - `crypto key generate rsa modulus 4096`
* **Restrecting remote access only to SSH**
    - `line vty 0 1500`
    - `transport input ssh`
    - `login local `