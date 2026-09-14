# Lab-detection-zabbix+wazuh
🏢 Contexte professionnel

Vous êtes administrateur systèmes et réseaux junior au sein d'une PME industrielle. La direction IT vous confie une mission suite à un audit externe qui a pointé une absence totale de détection d'intrusion sur le SI : aucune alerte n'est remontée en cas de comportement anormal sur les serveurs critiques. Vous devez prouver, avant validation budgétaire d'une solution commerciale, qu'une architecture de détection open source est viable.

🎯 Mission demandée
Déployer une supervision infrastructure (Zabbix) et une détection comportementale (Wazuh) sur un environnement représentatif.
Simuler une attaque réaliste contre une machine volontairement vulnérable du parc.
Démontrer la capacité de détection en mesurant le délai entre l'action malveillante et la génération de l'alerte.
Produire un rapport exploitable par une équipe SOC.
🛠️ Stack imposée

Zabbix · Wazuh · Kali Linux / Metasploit · Metasploitable ou DVWA · VMs locales ou AWS Free Tier

✅ Livrables attendus
Schéma d'architecture du lab (draw.io ou équivalent)
Procédure de déploiement documentée (Zabbix + agents, Wazuh manager + agents)
Scénario d'attaque détaillé (étape par étape, outils utilisés)
Timeline chronométrée : action attaquant → log brut généré → règle déclenchée → alerte visible
Rapport final au format "compte-rendu d'incident" (résumé exécutif + détail technique + recommandations)

📊 Barème d'évaluation
Critère	Points
Architecture cohérente et documentée	20
Attaque réaliste et variée (pas un seul scan)	20
Détection effective avec preuve (capture d'écran/log)	30
Mesure du délai de détection	15
Qualité et clarté du rapport final	15

⏱️ Durée indicative
