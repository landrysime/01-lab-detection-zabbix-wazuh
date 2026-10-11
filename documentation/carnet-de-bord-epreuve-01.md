# Carnet de bord — Épreuve 01 : Lab détection d'intrusion (Zabbix + Wazuh)

> Ce document se remplit au fur et à mesure du projet. Chaque phase indique QUOI capturer, POURQUOI, et à QUEL livrable final ça sert. Une fois complété, son contenu devient la base du README GitHub et du rapport final.

---

## Phase 0 — Préparation de l'environnement

**Ce qu'on fait :** activation Hyper-V, création du commutateur virtuel isolé.

**À capturer :**
- [ ] Capture du Gestionnaire Hyper-V actif (feature activée)
- [ ] Capture de la configuration du commutateur virtuel (type Interne, nom)

**Pourquoi :** preuve que l'environnement est isolé dès le départ — un recruteur/évaluateur doit voir que tu as pensé la sécurité du lab lui-même, pas juste celle de la cible.

**Alimente :** le livrable "Schéma d'architecture" (section réseau)

**Statut :** ⬜ à faire / 🟡 en cours / ✅ fait

---

## Phase 1 — Provisionnement des VMs

**Ce qu'on fait :** création de Kali, de la cible (Ubuntu + DVWA), de Wazuh, de Zabbix.

**À capturer, pour CHAQUE VM :**
- [ ] Capture des paramètres de création (génération, RAM, réseau assigné)
- [ ] Capture de l'IP obtenue une fois démarrée (`ip a` ou équivalent)

**Pourquoi :** documente la reproductibilité — quelqu'un d'autre doit pouvoir recréer le même lab à partir de tes notes.

**Alimente :** le livrable "Procédure de déploiement documentée"

**Statut :** ⬜ / 🟡 / ✅

---

## Phase 2 — Vérification de la chaîne bout en bout (baseline)

**Ce qu'on fait :** on confirme que Wazuh et Zabbix voient la cible AVANT toute attaque.

**À capturer :**
- [ ] Capture du dashboard Zabbix montrant la cible "Up" avec ses métriques de base
- [ ] Capture du dashboard Wazuh montrant l'agent cible "Active" et des événements normaux qui remontent (logs système, pas d'alerte de sécurité)
- [ ] Note l'horodatage exact de cette vérification

**Pourquoi : c'est l'étape la plus importante à documenter.** Cette capture "avant" est ta référence — sans elle, impossible de prouver ensuite que les alertes qui apparaîtront sont bien dues à ton attaque et pas à autre chose. C'est l'équivalent d'un "état des lieux" avant travaux.

**Alimente :** point de départ de la "Timeline chronométrée"

**Statut :** ⬜ / 🟡 / ✅

---

## Phase 3 — Exécution du scénario d'attaque

**Ce qu'on fait :** depuis Kali, on attaque la cible (reconnaissance → exploitation).

**À capturer, pour CHAQUE étape offensive :**
- [ ] Capture du terminal Kali montrant la commande lancée ET son résultat
- [ ] Horodatage précis de chaque commande (active `date` avant/après ou garde l'historique shell avec timestamps : `HISTTIMEFORMAT="%F %T "`)
- [ ] Une phrase de contexte : que fait cette commande, pourquoi cette étape

**Pourquoi :** c'est la preuve que l'attaque est réelle et volontaire, pas un incident random. L'horodatage précis est indispensable pour calculer le délai de détection en Phase 4.

**Alimente :** le livrable "Scénario d'attaque détaillé" + la "Timeline chronométrée"

**Statut :** ⬜ / 🟡 / ✅

---

## Phase 4 — Observation de la détection

**Ce qu'on fait :** on retourne sur Wazuh/Zabbix pour voir ce qui a été détecté.

**À capturer, pour CHAQUE alerte pertinente :**
- [ ] Capture de l'alerte dans le dashboard Wazuh (règle déclenchée, sévérité, horodatage de l'alerte)
- [ ] Mets en regard l'horodatage de l'action offensive (Phase 3) et celui de l'alerte → calcule le delta en secondes/minutes

**Pourquoi :** c'est le cœur de la preuve de valeur du projet — "j'ai détecté une intrusion en X secondes" est une phrase qui parle immédiatement à un recruteur, bien plus qu'une simple liste d'outils installés.

**Alimente :** le livrable "Timeline chronométrée" (tableau final action → log → alerte → délai)

**Statut :** ⬜ / 🟡 / ✅

---

## Phase 5 — Rédaction du rapport final

**Ce qu'on fait :** on compile tout en un document type "compte-rendu d'incident".

**Structure attendue :**
1. Résumé exécutif (3-4 lignes : contexte, ce qui a été testé, résultat clé)
2. Architecture du lab (schéma + description)
3. Scénario d'attaque (chronologie des actions offensives)
4. Détections observées (tableau action → alerte → délai)
5. Recommandations (ce qu'on ferait en conditions réelles pour améliorer la détection)

**À capturer :**
- [ ] Le tableau récapitulatif final de tous les délais mesurés
- [ ] Une conclusion synthétique du niveau de détection obtenu

**Alimente :** le livrable "Rapport final format compte-rendu d'incident" — c'est la pièce maîtresse du README GitHub

**Statut :** ⬜ / 🟡 / ✅

---

## Récapitulatif des livrables (cf. barème de l'épreuve)

| Livrable | Phase source | Statut |
|---|---|---|
| Schéma d'architecture du lab | Phase 0-1 | ⬜ |
| Procédure de déploiement documentée | Phase 1 | ⬜ |
| Scénario d'attaque détaillé | Phase 3 | ⬜ |
| Timeline chronométrée | Phase 2-4 | ⬜ |
| Rapport final (compte-rendu d'incident) | Phase 5 | ⬜ |
