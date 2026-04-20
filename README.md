# 🛡️ Rapport d'Atelier : Stratégies PRA & PCA sur Kubernetes

**Auteur :** Jean-Gérard HOUNKANRIN  
**Promotion :** EPSI 2026  
**Encadrant :** Boris STOCKER  
**Date :** 20 Avril 2026  

---

## 📖 Présentation du projet
Atelier PRA/PCA sur Kubernetes : Mise en place d'une application Flask résiliente avec sauvegardes automatisées par CronJob.

> **💡 Conseil de navigation :** Pour ne pas quitter cette page, maintenez la touche **Ctrl** (ou Cmd) enfoncée en cliquant sur les liens ci-dessous pour les ouvrir dans un **nouvel onglet**.

---

## 🌐 État des Routes et Accès Application

| Action | Lien de Test (Accès externe) | Statut |
| :--- | :--- | :--- |
| 🏠 **Accueil** | [Ouvrir l'Accueil](https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/) | OK ✅ |
| 🏥 **Santé** | [Vérifier Health](https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/health) | OK ✅ |
| ➕ **Ajouter** | [Ajouter un message](https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/add?message=Test_EPSI) | OK ✅ |
| 🔢 **Compteur** | [Voir le Compteur](https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/count) | OK ✅ |
| 📋 **Consultation** | [Consulter la base](https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/consultation) | OK ✅ |

---

## 🚀 Expertise Théorique (Séquence 5)

### Q1 : Perte de données
La perte est définitive si l'on perd le **PVC pra-data** ET le **PVC pra-backup**. Le Pod Flask est **stateless**, sa perte n'impacte pas les données.

### Q2 : Résilience
Les données sont préservées grâce à la **redondance asynchrone** (CronJob minute) vers le volume indépendant `pra-backup`.

### Q3 : KPI (Métriques)
* **RPO** : 1 Minute.
* **RTO** : ~2 à 5 Minutes.

### Q4 : Limites Production
Présence de **SPOF** (stockage local unique), base SQLite non distribuée et manque de monitoring/alerting.

### Q5 : Architecture cible
Utilisation d'un stockage objet distant (**Amazon S3**) et d'une base de données managée (**RDS**) pour une haute disponibilité géographique.

---

## 🛠️ Ateliers de Validation (Séquence 6)
* **Atelier 1** : Route `/status` ajoutée avec succès (format JSON).
* **Atelier 2** : Procédure de restauration granulaire validée via `50-job-restore.yaml`.
