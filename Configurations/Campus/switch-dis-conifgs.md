**Configuration Settings**

* **Boot System :**
  - `boot system flash:/vEOS-lab.swi` (Définit le système de démarrage sur le fichier vEOS-lab.swi situé dans la mémoire flash)

* **Transceiver Default Mode :**
  - `transceiver qsfp default-mode 4x10G` (Définit le mode par défaut du transceiver QSFP à 4x10G)

* **Logging**

  - `logging trap notifications` (Définit le niveau de gravité des journaux à "notifications")
  - `logging host 172.16.50.1` (Configure le serveur syslog à l'adresse IP 172.16.50.1)
  - `logging source-interface Loopback0` (Spécifie l'interface source pour les journaux comme Loopback0)

* **Hostname :**
  - `hostname vEOS-Dis-I` (Définit le nom de l'hôte du commutateur comme vEOS-Dis-I)

* **Name Server :**
  - `ip name-server vrf default 172.16.50.1` (Configure le serveur de noms DNS avec l'adresse IP 172.16.50.1 dans le VRF par défaut)

* **NTP Configuration :**
  - `ntp source Loopback0` (Configure l'interface Loopback0 comme source pour la synchronisation NTP)
  - `ntp server 172.16.50.1` (Configure le serveur NTP avec l'adresse IP 172.16.50.1)

* **RADIUS Server :**
  - `radius-server key 7 071B245F5A584B56` (Définit la clé de chiffrement pour le serveur RADIUS)
  - `radius-server host 172.16.50.1` (Configure l'adresse IP du serveur RADIUS)

**Spanning Tree**

* **Spanning Tree Mode :**
  - `spanning-tree mode mstp` (Définit le mode de spanning tree sur Multiple Spanning Tree Protocol)

**AAA Configuration**

* **Authentication, Authorization, and Accounting (AAA) :**
  - `aaa authentication login default group radius local` (Configure l'authentification pour les connexions telnet avec le groupe RADIUS et la méthode locale en cas d'échec)
  - `aaa authentication enable default group radius local` (Configure l'authentification pour la commande "enable" avec le groupe RADIUS et la méthode locale en cas d'échec)
  - `aaa authorization console` (Configure l'autorisation pour la console)
  - `aaa authorization exec default group radius local` (Configure l'autorisation pour les connexions exec avec le groupe RADIUS et la méthode locale en cas d'échec)
  - `no aaa root` (Désactive le compte root pour l'authentification)

* **User Configuration :**
  - `username admin privilege 15 role network-admin secret sha512 $6$DYjKa2m1a4SmsTLt$ZBUvPOayYeM2HpmGX6nebngi1IwTybGAoGOiJJlNYF1ti7mWR5Hb0N8iXA0DioJsBhpQjSZHSRsp/b1e0QIKq/` (Configure un utilisateur nommé admin avec le privilège 15 et un mot de passe chiffré)

**Clock and Timezone Configuration**

* **Clock Timezone :**
  - `clock timezone Europe/Bratislava` (Définit le fuseau horaire sur Europe/Bratislava)

**VLAN Configuration**

* **VLANs :**
  - `vlan 10,20,30,40` (Crée plusieurs VLANs avec les IDs respectifs 10, 20, 30, et 40)

**Interface Configuration**

* **Physical Interfaces :**
  - Configuration détaillée pour Ethernet1, Ethernet2, Ethernet3, Ethernet4, Ethernet5, Ethernet6, Ethernet7

* **Loopback Interface :**
  - `interface Loopback0`
  - `ip address 10.1.1.6/32` (Configure une adresse IP pour l'interface Loopback0 avec un masque de sous-réseau /32)

* **VLAN Interfaces :**
  - Configuration détaillée pour Vlan10, Vlan20, Vlan30, Vlan40

**Routing**

* **IP Routing :**
  - `ip routing` (Active le routage IP sur le commutateur)

* **OSPF Configuration :**
  - `router ospf 1` (Démarre la configuration OSPF avec le processus ID 1)
  - `router-id 10.1.1.6` (Définit l'ID du routeur OSPF comme 10.1.1.6)

* **Passive Interfaces :**
  - `passive-interface Ethernet4` (Met l'interface Ethernet4 en mode passif pour OSPF, empêchant l'envoi de paquets de routage OSPF sur cette interface)
  - `passive-interface Ethernet5` (Met l'interface Ethernet5 en mode passif pour OSPF)
  - `passive-interface Ethernet6` (Met l'interface Ethernet6 en mode passif pour OSPF)
  - `passive-interface Vlan10` (Met l'interface Vlan10 en mode passif pour OSPF)
  - `passive-interface Vlan20` (Met l'interface Vlan20 en mode passif pour OSPF)
  - `passive-interface Vlan30` (Met l'interface Vlan30 en mode passif pour OSPF)
  - `passive-interface Vlan40` (Met l'interface Vlan40 en mode passif pour OSPF)

* **Network Configuration :**
  - `network 10.0.0.0/30 area 0.0.0.0` (Annonce le réseau 10.0.0.0/30 dans la zone OSPF 0.0.0.0)
  - `network 10.0.0.8/30 area 0.0.0.0` (Annonce le réseau 10.0.0.8/30 dans la zone OSPF 0.0.0.0)
  - `network 10.0.0.20/30 area 0.0.0.0` (Annonce le réseau 10.0.0.20/30 dans la zone OSPF 0.0.0.0)
  - `network 10.1.1.6/32 area 0.0.0.0` (Annonce l'adresse IP de l'interface Loopback0 dans la zone OSPF 0.0.0.0)
  - `network 10.1.1.8/30 area 0.0.0.0` (Annonce le réseau 10.1.1.8/30 dans la zone OSPF 0.0.0.0)
  - `network 192.168.10.0/24 area 0.0.0.0` (Annonce le réseau 192.168.10.0/24 dans la zone OSPF 0.0.0.0)
  - `network 192.168.20.0/24 area 0.0.0.0` (Annonce le réseau 192.168.20.0/24 dans la zone OSPF 0.0.0.0)
  - `network 192.168.30.0/24 area 0.0.0.0` (Annonce le réseau 192.168.30.0/24 dans la zone OSPF 0.0.0.0)
  - `network 192.168.40.0/24 area 0.0.0.0` (Annonce le réseau 192.168.40.0/24 dans la zone OSPF 0.0.0.0)

* **LSA Limit :**
  - `max-lsa 12000` (Définit le nombre maximal d'LSA que le routeur peut gérer à 12000)
