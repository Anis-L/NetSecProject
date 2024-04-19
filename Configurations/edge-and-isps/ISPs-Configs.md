**Configuration Settings**
* **Configuration of the router ISP2 is similar to the configuration of the ISP1. For this reason we only share the configuration of ISP1**
 


**Interfaces configuration**

* **GigabitEthernet 0/0**

    - `interface GigabitEthernet 0/0`
    - `description Link to Simulated Internet`
    - `ip address dhcp`
    - `ip nat outside`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 1/0**

    - `interface GigabitEthernet0/1`
    - `description Link to Company Inc`
    - `ip address 198.10.10.1 255.255.255.252`
    - `ip nat inside`
    - `no shutdown`
    - `exit`


**eBGP Configuration**

* **Prefix-list**
    - `ip prefix-list static_default permit 0.0.0.0/0`
* **dynamic routing**
    - `router bgp 64501`
    - `neighbor 198.10.10.2 remote-as 64500`
    - `neighbor 198.10.10.2 ttl-security hops 1`
    - `neighbor 198.10.10.2 password isp1md5pass`
    - `neighbor 198.10.10.2 route-map static_default out`
    - `network 0.0.0.0 mask 0.0.0.0`


**NAT Configuration**
* **Standard access-list 1**
    - `ip access-list standard 1`
    - `permit 195.1.1.0 0.0.0.255`
    - `permit 198.10.10.0 0.0.0.3`
    - `deny any`
    
* **NAT Overload on the interface Gig 0/0**
    - `ip nat inside source list 1 interface GigabitEthernet 0/0 overload`


**Dns Configuration**
    - `ip domain-lookup`
    - ` ip name-server 8.8.8.8 8.8.4.4`



