# Projet 01 — Lab de détection d'intrusion (Wazuh + Zabbix)

Déploiement d'un laboratoire de détection d'intrusion open source de bout en bout, soumis à trois scénarios d'attaque contrôlés, avec mesure du **délai de détection** et corrélation **MITRE ATT&CK**.

**Stack :** Hyper-V · Debian 12/13 · Wazuh 4.9.2 · Zabbix 8.0 · Kali Linux (Nmap · Hydra · SQLmap) · DVWA

---

## Contexte

Suite à un audit externe pointant l'absence de détection d'intrusion sur le SI, la mission est de prouver qu'une architecture de détection **open source** est viable avant toute validation budgétaire d'une solution commerciale : déployer la supervision, simuler des attaques réalistes, et mesurer concrètement ce qui est détecté — et en combien de temps.

## Architecture

Quatre VMs sur un réseau interne isolé `192.168.100.0/24` (Hyper-V, switch virtuel sans accès Internet pendant les phases d'attaque).

| VM | IP | OS | Rôle |
|---|---|---|---|
| VMServerWazuh | 192.168.100.60 | Debian 12 | Wazuh all-in-one (Manager + Indexer + Dashboard) |
| VMZabbix | 192.168.100.50 | Debian 13 | Zabbix 8.0 — supervision infrastructure |
| debian-cible | 192.168.100.30 | Debian 13 | DVWA (Docker) + agents Wazuh/Zabbix |
| Kali | 192.168.100.40 | Kali Linux | Machine attaquante |

![Architecture du lab](Architecture%20Lab%20intrusion%20P1.png)

## Scénarios d'attaque et détection

| Attaque | Outil | Détection Wazuh | Résultat |
|---|---|---|---|
| Reconnaissance réseau | `nmap -sV -sC -O -p-` | Rule 510 (level 7), ×23 | **1re alerte en 3 min 42 s** |
| Brute force SSH | `hydra` + rockyou.txt | Rule 5712 (level 10) | 135 tentatives, brute force confirmé en < 10 min |
| Injection SQL | `sqlmap` sur DVWA | Gravité critique | 5 comptes + hash MD5 extraits (4 techniques d'injection) |

**6 tactiques MITRE ATT&CK** identifiées sur 9 règles déclenchées : Credential Access (T1110), Lateral Movement (T1021.004), Privilege Escalation (T1548.003), Defense Evasion (T1078), Initial Access (T1190).

En parallèle, Zabbix a supervisé l'impact système : pic CPU à 1,05 % pendant le scan (baseline < 0,1 %), 100 % de disponibilité maintenue, 214 éléments collectés.

## Livrables

- **[Rapport final (PDF)](doc4-rapport-final.pdf)** — format compte-rendu d'incident SOC : résumé exécutif, timeline chronométrée, cartographie MITRE, recommandations.
- **[Carnet de bord](Documentation/)** — procédure de déploiement, guides d'installation.
- **[Schéma d'architecture](architecture-lab-detection%20P1.drawio)** (draw.io) + export PNG.
- **[Captures](Screenshots/)** — Wazuh, Zabbix, DVWA, phases d'attaque, MITRE.
- **[Rapports Wazuh](Rapport%20Wazuh/)** — export MITRE ATT&CK, rapport brute force Hydra.

## Recommandations issues du lab

Requêtes préparées (PDO/MySQLi) contre l'injection SQL · remplacement de MD5 par bcrypt/Argon2 · Fail2ban sur SSH · `PermitRootLogin no` · validation stricte des entrées · maintien des règles Wazuh 5712 / 5758 / 31103.

## Compétences démontrées

Déploiement SIEM + supervision (Wazuh/Zabbix) · gestion d'agents sur VMs Linux · scénario d'attaque contrôlé (Nmap/Hydra/SQLmap) · analyse d'alertes et corrélation MITRE ATT&CK · rapport d'incident format SOC avec délais de détection mesurés.

---

*Projet réalisé en autonomie — Styve Landry SIME KOUNOU — styvelandry1@outlook.fr — octobre 2026*
