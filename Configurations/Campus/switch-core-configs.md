Building configuration...

Current configuration : 3156 bytes
!
! Last configuration change at 17:07:27 UTC+2 Wed Sep 13 2017 by raadmin
! NVRAM config last updated at 17:07:12 UTC+2 Wed Sep 13 2017 by raadmin
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
service compress-config
!
hostname vIOS-Core-I
!
boot-start-marker
boot-end-marker
!
!
enable secret 5 $1$78b3$xtQa1A6wFCybA2fbZZWeU.
!
username admin privilege 15 secret 5 $1$SUUR$R.rWrThT1MWlk/GocKXzc0
aaa new-model
!
!         
aaa authentication login default group radius local
aaa authentication enable default group radius enable
aaa authorization console
aaa authorization exec default group radius local 
!
!
!
!
!
!
aaa session-id common
clock timezone UTC+2 2 0
!
!
!
!
!
!
!
!
ip domain-name companyXYZ.sk
ip name-server 172.16.50.1
ip cef    
no ipv6 cef
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
vlan internal allocation policy ascending
!
ip ssh version 2
! 
!
!
!
!
!
!
!
!
!
!
!
interface Loopback0
 ip address 10.1.1.1 255.255.255.255
 ip ospf message-digest-key 1 md5 7 14543F123C05393865786061
!
interface GigabitEthernet0/2
 description Link to vEOS-Dis-I
 no switchport
 ip address 10.0.0.10 255.255.255.252
 ip ospf message-digest-key 1 md5 7 03477612360E325F0F594A51
 ip ospf network point-to-point
 negotiation auto
!
interface GigabitEthernet0/1
 description Link to vEOS-Dis-II
 no switchport
 ip address 10.0.0.18 255.255.255.252
 ip ospf message-digest-key 1 md5 7 01502B1D6B0A151C601C1D5D
 ip ospf network point-to-point
 negotiation auto
!
interface GigabitEthernet0/0
 description Link to vIOS-Core-II     
 no switchport
 ip address 10.0.0.5 255.255.255.252
 ip ospf message-digest-key 1 md5 7 15512615342B383769636676
 ip ospf network point-to-point
 negotiation auto
!
interface GigabitEthernet0/3
 description Link to ASAv-I
 no switchport
 ip address 172.16.0.10 255.255.255.252
 ip ospf message-digest-key 1 md5 7 05482B16114D5D1A58554446
 negotiation auto
!
interface GigabitEthernet1/0
 description Unused
 shutdown
 media-type rj45
 negotiation auto
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/1
 description Unused
 shutdown
 media-type rj45
 negotiation auto
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/2
 description Unused
 shutdown
 media-type rj45
 negotiation auto
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/3
 description Unused
 shutdown
 media-type rj45
 negotiation auto
 no lldp transmit
 no lldp receive
!
router ospf 1
 router-id 10.1.1.1
 area 0 authentication message-digest
 network 10.0.0.4 0.0.0.3 area 0
 network 10.0.0.8 0.0.0.3 area 0
 network 10.0.0.16 0.0.0.3 area 0
 network 10.1.1.1 0.0.0.0 area 0
 network 172.16.0.8 0.0.0.3 area 0
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
!
!
ip radius source-interface Loopback0 
logging trap notifications
logging source-interface Loopback0
logging host 172.16.50.1
!
!
!
!
radius server Server1
 address ipv4 172.16.50.1 auth-port 1812 acct-port 1813
 key 7 021201481F575D72
!
!
control-plane
!
!
line con 0
line aux 0
line vty 5 15
!
ntp source Loopback0
ntp server 172.16.50.1
!
end


**Configuration Settings**

* **Hostname :**
  - `hostname vIOS-Core-I` (Définit le nom de l'hôte du routeur comme vIOS-Core-I)

* **Enable Secret :**
  - `enable secret 5 $1$78b3$xtQa1A6wFCybA2fbZZWeU.` (Définit un mot de passe chiffré pour l'accès aux privilèges de niveau EXEC)

* **Username :**
  - `username admin privilege 15 secret 5 $1$SUUR$R.rWrThT1MWlk/GocKXzc0` (Crée un utilisateur nommé admin avec un mot de passe chiffré et des privilèges de niveau 15)

* **Timezone :**
  - `clock timezone UTC+2 2 0` (Définit le fuseau horaire sur UTC+2)

* **Domain Name :**
  - `ip domain-name companyXYZ.sk` (Configure le nom de domaine pour la résolution DNS)

* **Name Server :**
  - `ip name-server 172.16.50.1` (Configure l'adresse IP du serveur de noms DNS)

* **SSH Version :**
  - `ip ssh version 2` (Active le support du protocole SSH version 2 pour les connexions sécurisées)

**AAA Configuration**

* **AAA Authentication :**
  - `aaa authentication login default group radius local` (Configure l'authentification par défaut via le groupe RADIUS et la méthode locale)
  - `aaa authentication enable default group radius enable` (Configure l'authentification pour la commande "enable" via le groupe RADIUS et la méthode enable)
  - `aaa authorization exec default group radius local` (Configure l'autorisation pour les commandes EXEC via le groupe RADIUS et la méthode locale)

**Logging**

* **Syslog Configuration :**
  - `logging trap notifications` (Capture les messages syslog de niveau "notifications")
  - `logging source-interface Loopback0` (Spécifie l'interface source pour les messages syslog comme Loopback0)
  - `logging host 172.16.50.1` (Redirige les messages syslog vers le serveur syslog à l'adresse IP 172.16.50.1)

**Interface Configuration**

* **Loopback Interface :**
  - `interface Loopback0`
  - `ip address 10.1.1.1 255.255.255.255` (Configure une adresse IP pour l'interface Loopback0)

* **Physical Interfaces :**
  - Configuration détaillée pour GigabitEthernet0/2, GigabitEthernet0/1, GigabitEthernet0/0, GigabitEthernet0/3

**Routing**

* **OSPF Configuration :**
  - `router ospf 1`
  - `router-id 10.1.1.1` (Définit l'ID du routeur OSPF comme 10.1.1.1)
  - `area 0 authentication message-digest` (Active l'authentification par message digest pour la zone OSPF 0)

* **OSPF Interface Configuration :**
  - Configuration détaillée pour les interfaces GigabitEthernet0/2, GigabitEthernet0/1, GigabitEthernet0/0, GigabitEthernet0/3 avec l'utilisation de MD5 pour l'authentification OSPF, ainsi que la spécification du type de réseau comme point-à-point.


**NTP Configuration**

* **NTP Configuration :**
  - `ntp source Loopback0` (Spécifie l'interface source pour la synchronisation NTP comme Loopback0)
  - `ntp server 172.16.50.1` (Configure le serveur NTP avec l'adresse IP 172.16.50.1)

**Radius Server Configuration**

* **Radius Server :**
  - `radius server Server1`
  - `address ipv4 172.16.50.1 auth-port 1812 acct-port 1813` (Spécifie l'adresse IP du serveur RADIUS, ainsi que les ports d'authentification et d'accounting)
  - `key 7 021201481F575D72` (Configure la clé partagée pour l'authentification RADIUS, chiffrée)
