# 🖥️ Infrastructure Cloud de Supervision Centralisée sous AWS avec Zabbix

## 📌 Description du projet

Ce projet consiste à **concevoir et déployer une infrastructure cloud de supervision centralisée** sur **Amazon Web Services (AWS)** en utilisant l’outil open-source **Zabbix**, déployé de manière **conteneurisée avec Docker**.

L’objectif principal est de superviser un **environnement hybride Linux / Windows**, en collectant et visualisant des métriques système essentielles telles que :

* l’utilisation CPU,
* l’utilisation mémoire,
* l’état général des services,
* la disponibilité des hôtes.

Le projet met en œuvre les bonnes pratiques cloud en matière de **sécurité réseau, scalabilité et supervision proactive** .

---

## 🏗️ Architecture globale

L’architecture repose sur :

* Un **VPC dédié** sur AWS (CIDR : `10.0.0.0/16`)
* Un **sous-réseau public** (`10.0.0.0/24`)
* Une **Internet Gateway** pour l’accès externe
* Des **Security Groups** stricts pour contrôler les flux réseau
* Trois **instances EC2** distinctes :

  * Serveur Zabbix
  * Client Linux
  * Client Windows 

---

## ☁️ Ressources AWS utilisées

| Rôle           | Type EC2  | OS                  | Fonction             |
| -------------- | --------- | ------------------- | -------------------- |
| Serveur Zabbix | t3.large  | Ubuntu 22.04 LTS    | Supervision centrale |
| Client Linux   | t3.medium | Ubuntu 22.04 LTS    | Agent Zabbix         |
| Client Windows | t3.large  | Windows Server 2022 | Agent Zabbix         |



---

## 🔐 Sécurité réseau (Security Groups)

### Zabbix-Server-SG

* `22` : SSH
* `80 / 443` : Interface Web
* `10051` : Communication serveur Zabbix

### Agents-SG

* `10050` : Agent Zabbix
* `22` : Administration Linux
* `3389` : RDP Windows



---

## 🐳 Déploiement Zabbix avec Docker

Le serveur Zabbix est déployé via **Docker Compose**, incluant :

* **MySQL** (base de données)
* **Zabbix Server**
* **Zabbix Web (Nginx)**

Les variables sensibles sont stockées dans un fichier `.env`.

### Commandes principales

```bash
docker-compose up -d
docker ps
```

L’interface Web est accessible via l’IP publique du serveur Zabbix sur le port `8080` .

---

## 🧩 Configuration des agents Zabbix

### 🔹 Linux

* Installation depuis le dépôt officiel Zabbix
* Configuration des paramètres :

  * `Server`
  * `ServerActive`
  * `Hostname`
* Activation du service au démarrage

### 🔹 Windows

* Installation via le package MSI officiel
* Enregistrement manuel de l’hôte dans l’interface Zabbix

Les deux hôtes sont ensuite liés aux **templates officiels Zabbix** pour une supervision automatique .

---

## 📊 Monitoring et alertes

* Création d’un **dashboard global**
* Visualisation centralisée des métriques Linux & Windows
* Mise en place d’un **trigger CPU** pour tester les alertes proactives
* Vérification du bon fonctionnement des notifications internes



---

## ✅ Résultats obtenus

✔ Infrastructure cloud fonctionnelle
✔ Supervision centralisée opérationnelle
✔ Agents Linux & Windows correctement supervisés
✔ Alertes et dashboards validés

---

## 🚀 Améliorations possibles

* Intégration de **Grafana**
* Notifications avancées (Email, Slack, Telegram)
* Supervision de services applicatifs
* Haute disponibilité du serveur Zabbix



---

## 👤 Auteur

**NAIT ALI Khalid**
🎓 Cycle Ingénieur – Génie Informatique
📅 Année universitaire : 2025 – 2026
🎓 Encadrant : Prof. Azeddine Khiat


