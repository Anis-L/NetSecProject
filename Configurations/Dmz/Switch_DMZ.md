**Configuration Settings**

* **Enable Password :**
  - `enable secret cisco` 
* **Username and Password:**
  - `username admin secret cisco` 
* **Timezone:**
  - `clock timezone UTC+2 2 0` 
* **Domain Name :**
  - `ip domain-name companyXYZ.sk` (Configure a domain name for name resolution within the network, if applicable)
* **Name Server :**
  - `ip name-server 195.1.1.161` (IP address of the DNS server for network resource resolution)

**Spanning Tree and VLAN Allocation**

* **VLAN Mode :**
  - `spanning-tree mode rapid-pvst` (Enables Rapid PVST+ for spanning-tree protocol, if not already configured)
* **VLAN Allocation Policy :**
  - `vlan internal allocation policy ascending` (Sets VLAN ID allocation to ascending order, if not the default behavior)

**VLAN Creation**

* **Create VLAN:**
  - `vlan 10` 
* **VLAN Name :**
  - `name Servers_DMZ` 

**Interface Configuration**

* **GigabitEthernet 0/1 (Server DMZ Connection):**
  - `interface GigabitEthernet0/1`
  - `description Link to Serv-DMZ-I` 
  - `switchport access vlan 10` 
  - `switchport mode access` (Enables switchport mode for the interface)
* **GigabitEthernet 0/0 (ASA Firewall Connection):**
  - `interface GigabitEthernet0/0`
  - `description Link to ASAv-DMZ-I` 
  - `no switchport` (Disables switchport mode for routing purposes)
  - `ip address 195.1.1.134 255.255.255.252` 
* **VLAN Interface (Inter-VLAN Communication):**
  - `interface Vlan 10`
  - `ip address 195.1.1.166 255.255.255.248` 

**Routing**
* **Static Default Routing :**
  - `ip route 0.0.0.0 0.0.0.0 195.1.1.133` 

**Security**

* **SSH Access Control List (Optional):**
  - Create a standard access control list (ACL) to restrict SSH access to authorized devices.
  - `ip access-list standard ssh-access`
  - `permit 195.1.1.0 0.0.0.127` (Permit SSH access from specific IP addresses or ranges)
  - `deny any` (Deny SSH access from all other sources)
* **SSH Version:**
  - `ip ssh version 2` (Enforce SSH version 2 for more secure connections)

**Logging**

* Enable logging for network events:
  - `logging trap notifications` (Captures trap messages for network events)
  - `logging host 195.1.1.161` (Directs logs to a designated IP address for centralized monitoring)

**Console Access**

* Configure login settings for console