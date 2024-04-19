**Configuration Settings**

* **Hostname :**
  - `hostname OpenSwitch-Acc-I` (Définit le nom de l'hôte du commutateur comme OpenSwitch-Acc-I)

* **NTP Server :**
  - `ntp server 172.16.50.1` (Configure un serveur NTP avec l'adresse IP 172.16.50.1 pour la synchronisation horaire)

**Logging**

* **Syslog Server :**
  - `logging 172.16.50.1 severity notice` (Redirige les journaux système vers le serveur syslog à l'adresse IP 172.16.50.1 avec une gravité de notice)

**VLAN Configuration**

* **VLANs :**
  - `vlan 1`, `vlan 10`, `vlan 20`, `vlan 40`, `vlan 999` (Crée plusieurs VLANs avec les IDs respectifs 1, 10, 20, 40 et 999)
  - `no shutdown` (Active toutes les VLANs créées)

**Spanning Tree**

* **Spanning Tree Configuration :**
  - `spanning-tree config-name 70:72:cf:03:e5:3f` (Configure le nom de configuration pour le spanning tree)

**Interface Configuration**

* **Physical Interfaces :**
  - `interface eth1`, `interface eth2`, `interface eth3`, `interface eth4`, `interface eth5`, `interface eth6`, `interface eth7` (Configure plusieurs interfaces physiques)
  - `no shutdown` (Active les interfaces)
  - `no routing` (Désactive le routage sur les interfaces)
  - `vlan trunk native <vlan-id>` (Définit la VLAN native sur les interfaces trunk)
  - `vlan trunk allowed <vlan-id>` (Autorise les VLANs spécifiées sur les interfaces trunk)
  - `vlan access <vlan-id>` (Associe les interfaces à des VLANs spécifiques en mode d'accès)

* **Interface VLAN20 :**
  - `interface vlan20`
  - `no shutdown` (Active l'interface VLAN20)
  - `ip address 192.168.20.250/24` (Configure une adresse IP statique pour l'interface VLAN20 avec masque de sous-réseau /24)

* **Management Interface :**
  - `interface mgmt`
  - `ip static 10.1.1.9/30` (Configure une adresse IP statique pour l'interface de gestion avec masque de sous-réseau /30)
  - `default-gateway 10.1.1.10` (Définit la passerelle par défaut pour l'interface de gestion)
  - `nameserver 172.16.50.1` (Configure le serveur de noms avec l'adresse IP 172.16.50.1 pour la résolution DNS)

**Routing**

* **Default Route :**
  - `ip route 0.0.0.0/0 192.168.20.254` (Configure une route par défaut vers la passerelle 192.168.20.254)

