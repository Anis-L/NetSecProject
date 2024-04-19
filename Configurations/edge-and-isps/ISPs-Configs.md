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

* **Prefix-list**  (l'utilisation d'une liste de préfixes pour annoncer des routes)
    - `ip prefix-list static_default permit 0.0.0.0/0`
* **dynamic routing**
    - `router bgp 64501`
    - `neighbor 198.10.10.2 remote-as 64500`
    - `neighbor 198.10.10.2 ttl-security hops 1`
    - `neighbor 198.10.10.2 password isp1md5pass`
    - `neighbor 198.10.10.2 route-map static_default out`
    - `network 0.0.0.0 mask 0.0.0.0`


**NAT Configuration**
* **La configuration NAT (Network Address Translation) permet de traduire les adresses IP privées de l'entreprise en adresses IP publiques pour la communication sur Internet. La liste d'accès standard définit les adresses IP internes autorisées à être traduites, tandis que la configuration d'overload NAT spécifie l'interface utilisée pour la traduction.**

* **Standard access-list 1**
    - `ip access-list standard 1`
    - `permit 195.1.1.0 0.0.0.255`
    - `permit 198.10.10.0 0.0.0.3`
    - `deny any`
    
* **NAT Overload on the interface Gig 0/0**
    - `ip nat inside source list 1 interface GigabitEthernet 0/0 overload`


**Dns Configuration**
* **La configuration DNS (Domain Name System) configure le routeur pour utiliser des serveurs DNS spécifiques pour la résolution de noms de domaine. Cela permet au routeur de résoudre les noms de domaine en adresses IP pour les requêtes DNS effectuées par les périphériques de l'entreprise.**
    - `ip domain-lookup`
    - `ip name-server 8.8.8.8 8.8.4.4`


