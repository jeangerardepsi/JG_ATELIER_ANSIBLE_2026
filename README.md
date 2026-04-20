# 🛡️ Rapport d'Atelier : Stratégies PRA & PCA sur Kubernetes

**Auteur :** Jean-Gérard HOUNKANRIN  
**Promotion :** EPSI 2026  
**Encadrant :** Boris STOCKER  
**Date :** 20 Avril 2026  

---

## 📖 Présentation du projet
Cet atelier met en œuvre un **mini-PRA** sur **Kubernetes**. Il simule la perte d'un volume de données et sa restauration via un système de sauvegarde automatisé.

---

## 🌐 Accès à l'Application (Ouverture nouvel onglet)

| Action | Lien de Test | Statut |
| :--- | :--- | :--- |
| 🏠 **Accueil** | <a href="https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/" target="_blank">Ouvrir l'Accueil</a> | OK ✅ |
| 🏥 **Santé** | <a href="https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/health" target="_blank">Vérifier Health</a> | OK ✅ |
| ➕ **Ajouter** | <a href="https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/add?message=Test_EPSI" target="_blank">Ajouter un message</a> | OK ✅ |
| 🔢 **Compteur** | <a href="https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/count" target="_blank">Voir le Compteur</a> | OK ✅ |
| 📋 **Consultation** | <a href="https://psychic-funicular-4j9jqrxw547jc799v-8080.app.github.dev/consultation" target="_blank">Consulter la base</a> | OK ✅ |

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
