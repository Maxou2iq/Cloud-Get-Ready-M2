# Plan d’adressage IP – Projet Cloud Get Ready

## 1. Schéma de découpage
- VLAN 10 – Management : 10.10.10.0/24
- VLAN 20 – Production : 10.10.20.0/24
- VLAN 30 – SAN/NAS : 10.10.30.0/24
- VLAN 40 – Migration : 10.10.40.0/24

---

## 2. Tableau d’adressage

### VLAN 10 – Management (10.10.10.0/24)
| Équipement              | Adresse IP   | Remarque                 |
|--------------------------|--------------|--------------------------|
| Passerelle / firewall    | 10.10.10.1   | Gateway mgmt             |
| Hyperviseur 1 (mgmt)     | 10.10.10.11  | Proxmox node 1           |
| Hyperviseur 2 (mgmt)     | 10.10.10.12  | Proxmox node 2           |
| Hyperviseur 3 (mgmt)     | 10.10.10.13  | Proxmox node 3           |
| SAN/NAS (mgmt)           | 10.10.10.20  | TrueNAS mgmt             |

### VLAN 20 – Production (10.10.20.0/24)
| Équipement              | Adresse IP   | Remarque                 |
|--------------------------|--------------|--------------------------|
| Passerelle / firewall    | 10.10.20.1   | Gateway prod             |
| VM Linux test            | 10.10.20.50  | VM de validation réseau  |
| VM Windows test          | 10.10.20.51  | VM de validation appli   |
| Pool VMs prod            | 10.10.20.100–10.10.20.200 | Réservé aux VMs |

### VLAN 30 – SAN/NAS (10.10.30.0/24)
| Équipement              | Adresse IP   | Remarque                 |
|--------------------------|--------------|--------------------------|
| SAN/NAS (iSCSI/NFS)      | 10.10.30.20  | Stockage partagé         |
| Hyperviseur 1 (storage)  | 10.10.30.11  | Lien iSCSI multipath     |
| Hyperviseur 2 (storage)  | 10.10.30.12  | Lien iSCSI multipath     |
| Hyperviseur 3 (storage)  | 10.10.30.13  | Lien iSCSI multipath     |

### VLAN 40 – Migration (10.10.40.0/24)
| Équipement              | Adresse IP   | Remarque                 |
|--------------------------|--------------|--------------------------|
| Hyperviseur 1 (migration)| 10.10.40.11  | Live migration           |
| Hyperviseur 2 (migration)| 10.10.40.12  | Live migration           |
| Hyperviseur 3 (migration)| 10.10.40.13  | Live migration           |

---

## 3. Réservations
- .1 → passerelles VLAN (firewall/routeur)  
- .10 – .50 → équipements physiques (hyperviseurs, SAN, supervision)  
- .51 – .200 → VMs / workloads  
- .201 – .254 → réserves futures  

---

## 4. Notes
- Chaque hyperviseur a 3 interfaces : management, stockage, migration.  
- Le SAN est accessible uniquement via VLAN 30.  
- Les plages sont cohérentes et extensibles pour d’autres VLANs (ex. 10.10.50.0/24 pour la supervision, 10.10.60.0/24 pour la DMZ).

