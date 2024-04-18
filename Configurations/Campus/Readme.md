

# Partie campus

Cette partie va traiter la partie campus du réseau, le role de cette partie et de relier tous les équipement internes de l'entreprises entre eux, qu'il soit équipement terminaux tel que les ordinateurs terminaux, les différents types de switches et le firewall qui assure un degré d'isolation


### Contenu :

1. **Introduction**
2. **Composants de l'architecture**
3. **Résumé de la configuration**
4. **Mesures de sécurité**
5. **Conclusion**



## 1. Introduction
la partie campus est la partie constituant la major partie du réseau, dans cet architecture elle suit le modéle en trois couches principales
- la couche d'accés
- la couche de distribution
- la couche cœur
chaqu'une a son importance et son role a jouer dans le bon fonctionnement du réseau de l'entreprise, 



## 2. Composants et architecture

- **Couche d'accés** : deux switches OpenSwitch qui fournissent l'accés au réseau a travers des machines clientes, c'est aussi a leur niveau que les machines sont segmentés en un sous réseau adéquat
les quatres machines présentes dans la couche d'accés sont des machines fonctionnant sur tiny core linux

- **Couche de distribution** : cette couche consiste en deux switches multicouches qui fonctionne en Arista vEOS, leur fonction principale est de connecter la couche d'accés avec la couche coeur du réseau. Deplus, étant des switches de niveau 3, c'est aussi le point ou se fait le routage inter vlans de la couche inferieur.

- **Couche cœur** : elle consiste elle aussi en deux switches Cisco vIOS-l2, étant uniquement de couche 3, ces switches ont pour tache de lier les switches de la couche de distribution a un firewall



## 3. Résumé de la configuration

- **Configuration des adresses statiques** : sur les interfaces des switches
- **Configuration des VLANS** : configuration de 4 vlans différentes et affectation sur les interfaces trunk et access sur les swithces d'accés et de distributions
- **Configuration NTP** : affecation du serveur ntp et de la timezone a suivre
- **Configuration Telnet** : sur les switches pour y acceder a travers le réseau
- **Configuration adressages dynamique** : pour les machines clients via le serveur DHCP
- **Configuration ip helper** : pour permettre la propagation des requétes DHCP entre le serveurs et les machines clients
- **Configuration DNS** : spécifier le serveur DNS chargé de fournir les noms
- **Configuration routage OSPF** : dans le but d'améliorer les performances et la sécurité, les zones ospf seront limitées aux interfaces inter switches seulement, le reste des interfaces sont passives
- **Configuration VRRP** : qui est un protocole qui permet la redondance entre les switche de niveau 3 qui assurent le routage inter VLAN.
- **Configuraiton des clients RADIUS** : pour permettre l'authentification des utilisateurs qui accédent aux équipements


## 4. Mesures de sécurité

- **Sécurisation des interfaces non utilisées** : affectation a un vlan commun, no-routing et shutdown
- **Sauvegarde des logs** : les logs sont configurés pour étre stoqués sur le serveur
- **Mots de passe de connexion** : mise en place des mots de passes sur tous les niveaux de tous les équipements
- **Mot de passe OSPF** : permet d'échanger les informations de routes OSPF avec plus de sécurité
- **Authentification par RADIUS** : pour pouvoire authentifier tous les utilisateurs qui accédent aux équipement réseau de maniére plus sur a travers le serveur RADIUS



## 5. Conclusion
En conclusion, la partie campus du réseau constitue le cœur de l'infrastructure de l'entreprise, interconnectant efficacement tous les équipements internes. Sa conception en trois couches garantit une gestion optimale du trafic. Les mesures de sécurité mises en place, telles que la sécurisation des interfaces et l'authentification par RADIUS, assurent un réseau fiable et sécurisé, prêt à répondre aux besoins de l'entreprise.