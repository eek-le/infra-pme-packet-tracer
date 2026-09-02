# Infrastructure Réseau d'Entreprise Segmentée et Sécurisée (Cisco Packet Tracer)


## Présentation du Projet
Ce projet présente la conception et la configuration d'une infrastructure réseau complète pour PME, garantissant la haute disponibilité, la sécurité des accès et une segmentation stricte des flux selon les meilleures pratiques du marché.


## Architecture et Topologie Réseau

### 1. Plan de Segmentation (VLANs et Adressage)
  | Nom du VLAN | ID VLAN | Usage / Équipements rattachés | Plage d'adressage |
- | **VLAN_USERS** | 10 | Utilisateurs Postes fixes, PC Portables (Wi-Fi_Entreprise) | `172.16.1.0/24` |
- | **VLAN_SERVERS** | 20 | Serveur d'Entreprise, Imprimante | `172.16.2.0/24` |
- | **VLAN_MGMT** | 30 | Administration (Switchs, APs, Router) | `172.16.3.0/24` |
- | **VLAN_GUEST** | 40 | Wi-Fi Invités / Visiteurs | `172.16.4.0/24` |
- | **VLAN_NATIVE** | 99 | VLAN Natif (Blackhole / Inutilisé) | Unassigned |


## Equipement et Configuration 

### Box FAI (Box)
- **DMZ :** configuré vers le routeur d'entreprise

### Routeur d'entreprise (RT-01)
- **NAT Overvoad/PAT :** traduction d'adresses sur l'interface WAN Gig0/0
- **Pools DHCP et Routage Inter-VLAN (Router-on-a-Stick) :** activation de serveurs DHCP via les sub-interfaces pour filtrer les communications inter-services.

### Switch (SW-01)
- **Repartion des ports :** definit le plan d'affectation des ports sur le switch
- **Access, Trunk et Encapsulation 802.1Q :** creation de vlans et mis en place du trunk sur toutes les liaisons inter-équipements (Routeur <-> Switch <-> Access Points).
- **VLAN Natif :** le VLAN Natif par défaut (VLAN 1) a été désactivé et remplacé par un VLAN Natif dédié (VLAN 99 Blackhole) sans aucun accès pour garantir la protection VLAN Hopping
- **Désactivation des ports inutilisés**
- **Spanning tree :** pour éviter les boucles réseau.

### Access Points (AP-01 et AP-02)
- **SSIDs Wi-Fi Mapping :**
  * `Wi-fi_entreprise` (WPA2) -> Mappé directement sur le **VLAN 10 (USERS)**.
  * `Wi-fi_visiteurs` (sans mot de passe) -> Mappé et isolé sur le **VLAN 40 (GUEST)**.
Particulierement, à cause des limitations de Packet tracer, il est impossible de deployer un controlleur d'APs et qu'un seul AP puisse diffuser plusieurs SSIDs, alors chaques APs du réseau diffuse uniquement un seul SSID neamoins cela paraît transparent pour les utilisateurs.


## Schéma du Lab et Fichiers

* **Fichier du Lab :** Le fichier d'architecture `.pkt` est disponible à la racine de ce dépôt.
* **Outil utilisé :** Cisco Packet Tracer

## Pour l'acces au management des equipements, veuillez consulter le fichier `administration.md` 

