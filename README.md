# Cloud Get Ready – Projet Master 2 Réseau & Sécurité

## 1. Contexte
Ce projet a pour objectif de concevoir et documenter une infrastructure cloud privé prête à l’emploi, répondant aux exigences de haute disponibilité, de sécurité et d’évolutivité.  
La solution repose sur un cluster d’hyperviseurs, un stockage centralisé de type SAN/NAS, ainsi qu’une segmentation réseau stricte.

## 2. Objectifs principaux
- Étudier et comparer différentes solutions d’hyperviseurs.  
- Étudier et comparer plusieurs solutions de stockage SAN/NAS.  
- Concevoir une architecture réseau segmentée par VLAN (management, production, SAN, migration).  
- Mettre en place la haute disponibilité (HA) et limiter les points de défaillance uniques (SPOF).  
- Documenter l’ensemble du projet dans un dépôt GitHub structuré et reproductible.  

## 3. Architecture prévue
- **Hyperviseur** : choix entre Proxmox, VMware ESXi et OpenStack/KVM.  
- **Stockage** : choix entre TrueNAS, Ceph et Openfiler.  
- **Réseau** : VLAN 10 (Management), VLAN 20 (Production), VLAN 30 (SAN), VLAN 40 (Migration).  
- **Haute disponibilité** : cluster d’hyperviseurs avec stockage partagé, support de la migration à chaud.  

## 4. Plan d’adressage
L’adressage suit un découpage professionnel basé sur le réseau privé 10.x.x.x :

| VLAN  | Nom        | Sous-réseau     | Exemple d’équipements        |
|-------|------------|-----------------|------------------------------|
| 10    | Management | 10.10.10.0/24   | Hyperviseurs, firewall, SAN  |
| 20    | Production | 10.10.20.0/24   | Machines virtuelles          |
| 30    | SAN        | 10.10.30.0/24   | Baie SAN, interfaces storage |
| 40    | Migration  | 10.10.40.0/24   | Li
