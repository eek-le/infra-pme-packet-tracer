# Infrastructure Réseau d'Entreprise Segmentée et Sécurisée (Cisco Packet Tracer)


## Présentation du Projet
Ce projet présente la conception et la configuration d'une infrastructure réseau complète pour PME, garantissant la haute disponibilité, la sécurité des accès et une segmentation stricte des flux selon les meilleures pratiques du marché.


## Architecture et Topologie Réseau

### 1. Plan de Segmentation (VLANs & Adressage)
  | Nom du VLAN | ID VLAN | Usage / Équipements rattachés | Plage d'adressage |
- | **VLAN_USERS** | 10 | Utilisateurs Postes fixes, PC Portables (Wi-Fi_Entreprise) | `172.16.1.0/24` |
- | **VLAN_SERVERS** | 20 | Serveur d'Entreprise, Imprimante | `172.16.2.0/24` |
- | **VLAN_MGMT** | 30 | Administration (Switchs, APs, Router) | `172.16.3.0/24` |
- | **VLAN_GUEST** | 40 | Wi-Fi Invités / Visiteurs | `172.16.4.0/24` |
- | **VLAN_NATIVE** | 99 | VLAN Natif (Blackhole / Inutilisé) | Unassigned |


## Sécurité et Choix Techniques

- **Trunk et Encapsulation 802.1Q :** Mis en place sur toutes les liaisons inter-équipements (Routeur - Switch - Access Points).
- **Protection VLAN Hopping :** Le VLAN Natif par défaut (VLAN 1) a été désactivé et remplacé par un **VLAN Natif dédié (VLAN 99 Blackhole)** sans aucun accès.
- **SSIDs Wi-Fi Mapping :**
  * `Wi-fi_entreprise` (WPA2) -> Mappé directement sur le **VLAN 10 (USERS)**.
  * `Wi-fi_visiteurs` (sans mot de passe) -> Mappé et isolé sur le **VLAN 40 (GUEST)**.
- **Routage Inter-VLAN (Router-on-a-Stick) :** Configuré sur le routeur d'entreprise via sub-interfaces pour filtrer les communications inter-services.
* **Sortie FAI / Accès Internet :** Traduction d'adresses (NAT/PAT) configurée sur le routeur entreprise connecté à la Box FAI.


## Schéma du Lab & Fichiers

* **Fichier du Lab :** Le fichier d'architecture `.pkt` est disponible à la racine de ce dépôt.
* **Outil utilisé :** Cisco Packet Tracer

