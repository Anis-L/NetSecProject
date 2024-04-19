**Configuration Settings**

* **Enable Password :**
  - `enable secret cisco`  (Active le mot de passe pour les privilèges d'administration)
* **Username and Password:**
  - `username admin secret cisco` (Définit le nom d'utilisateur et le mot de passe pour l'authentification)


**Interfaces configuration**

* **GigabitEthernet 0/0**

    - `interface GigabitEthernet 0/0`
    - `description Link to ASA-DMZ-I`
    - `ip address 195.1.1.129 255.255.255.252`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/1**

    - `interface GigabitEthernet0/1`
    - `description Link to ISP1`
    - `ip address 198.10.10.2 255.255.255.252`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/2**

    - `interface GigabitEthernet0/2`
    - `description Link to ASAv-I`
    - `ip address 172.16.0.2 255.255.255.252`
    - `no shutdown`
    - `exit`

* **GigabitEthernet 0/3**
    - `interface GigabitEthernet0/3`
    - `description Link to ISP2`
    - `ip address 197.10.10.2 255.255.255.252`
    - `no shutdown`
    - `exit`

* **LoopBack 0**
    - `interface loopback 0`
    - `description Management`
    - `ip address 10.1.1.5 255.255.255.255`
    - `no shutdown`
    - `exit`


**NAT Configuration**
* **Cette configuration détermine comment les adresses IP internes sont traduites en adresses IP externes. Les listes d'accès définissent les réseaux internes à traduire, le pool NAT spécifie les adresses externes à utiliser, et la configuration ip nat inside source list 1 pool 1 overload active le NAT pour ces réseaux.**

* **Standard access-list 1**
    - `access-list 1 permit 192.168.10.0 0.0.0.255`
    - `access-list 1 permit 192.168.20.0 0.0.0.255`
    - `access-list 1 permit 192.168.30.0 0.0.0.255`
    - `access-list 1 permit 192.168.40.0 0.0.0.255`
    - `access-list 1 permit 10.0.0.0 0.0.0.255`
    - `access-list 1 permit 10.1.1.0 0.0.0.255`
    - `access-list 1 permit 172.16.0.0 0.0.0.255`
    - `access-list 1 permit 172.16.50.0 0.0.0.255`
    - `access-list 1 deny any`
* **NAT pool of inside global addresses**
    - `ip nat pool 1 195.1.1.1 195.1.1.127 netmask 255.255.255.128`
* **NAT Overload**
    - `ip nat inside source list 1 pool 1 overload`
* **Inside and outside interfaces**
    
    * **GigabitEthernet 0/0**

        - `interface GigabitEthernet 0/0`
        - `ip nat outside`


    * **GigabitEthernet 0/1**

        - `interface GigabitEthernet0/1`
        - `ip nat outside`
   
    * **GigabitEthernet 0/2**

        - `interface GigabitEthernet0/2`
        - `ip nat outside`
        - `ip nat inside`


**Static Routes Configuration**
* **Ces commandes définissent les routes statiques pour diriger le trafic vers les réseaux spécifiés via les passerelles spécifiées.**
    - `ip route 172.16.0.0 255.255.0.0 172.16.0.1`
    - `ip route 192.168.0.0 255.255.192.0 172.16.0.1`
    - `ip route 10.0.0.0 255.0.0.0 172.16.0.1`
    - `ip route 195.1.1.128 255.255.255.128 195.1.1.130`
    - `ip route 195.1.1.0 255.255.255.0 null0`

**eBGP Configuration**
* **Cette configuration active le protocole de routage eBGP et définit les voisins BGP, avec des numéros AS (système autonome) différents. Les filtres et les politiques sont également configurés pour contrôler le trafic BGP.**
    - `router bgp 64500`
    - `neighbor 198.10.10.1 remote-as 64501`
    - `neighbor 198.10.10.1 password isp1md5pass`
    - `neighbor 197.10.10.1 remote-as 64502`
    - `neighbor 197.10.10.1 password isp2md5pass`
    - `network 195.1.1.0 mask 255.255.255.0`
    - `neighbor isp-group peer-group`
    - `neighbor isp-group ttl-security hops 1`
    - `neighbor isp-group filter-list 10 out`
    - `neighbor 198.10.10.1 peer-group isp-group`
    - ` neighbor 198.10.10.1 route-map setlocalin in`
    - `neighbor 197.10.10.1 peer-group isp-group `
    
    

**NTP Configuration**
* **Cette configuration définit un serveur NTP pour la synchronisation horaire du routeur et configure le fuseau horaire.**
    - `ntp server 172.16.50.1`
    - `clock timezone UTC+2 +2`
    - `ntp source loopback 0`

**Logging Configuration**
* **Ces commandes définissent le niveau de sévérité des messages à enregistrer, l'hôte de destination pour les messages de journalisation, et l'interface source pour les messages de journalisation.**
    - `logging trap notifications`
    - `logging host 172.16.50.1`
    - `logging source-interface loopback 0`

**Dns Client Configuration**
* **Cette configuration définit le serveur DNS à utiliser pour les requêtes DNS et active la résolution DNS.**
    - `ip name-server 195.1.1.161`
    - `ip domain-lookup`


**Security**

* **Using SSH version 2**

    - `ip ssh version 2` 
    - `ip domain-name companyXYZ.sk`(Configuration du nom de domaine pour la résolution DNS)

    - `crypto key generate rsa modulus 4096`
* **Restrecting remote access only to SSH**

    - `line vty 0 924`
    - `login local `
    - `transport input ssh`
    - `access-class ssh-access in `
* **standard access-list ssh-access that permits login to VTY from the management subnet 192.168.40.0/24 only.**

    - `ip access-list standard ssh-access`
    - `permit 192.168.40.0 0.0.0.255`
    - `deny any`

    
