# 🚀 Rapport d'Atelier : Automatisation et Gestion de Configuration avec Ansible

**Auteur :** Jean-Gérard HOUNKANRIN  
**Promotion :** EPSI 2026  
**Encadrant :** Boris STOCKER  
**Environnement :** GitHub Codespaces (Ubuntu)

---

## 📖 Présentation du projet
Ce projet illustre les principes de l'**Infrastructure as Code (IaC)**. À travers cet atelier, j'ai mis en place une chaîne d'automatisation permettant de provisionner, configurer et personnaliser un serveur web **Nginx**. L'objectif est de s'affranchir des configurations manuelles pour garantir un déploiement fiable, rapide et reproductible.

---

## ⚙️ Guide de déploiement

### 1. Pré-requis
* Système Linux (Debian/Ubuntu préféré)
* Ansible installé
* Connexion SSH ou locale configurée

### 2. Procédure technique
Pour déployer l'intégralité du service, exécutez les commandes suivantes dans l'ordre :

```bash
# Génération de l'inventaire local
echo "localhost ansible_connection=local" > inventory.ini

# Exécution du Playbook principal
ansible-playbook -i inventory.ini playbook.yml
```

---

## 🧠 Expertise Théorique (Séquence 4)

### Q1 : Pourquoi Ansible est-il qualifié d'outil "déclaratif" ?
Contrairement aux scripts Bash classiques qui sont **impératifs** (on liste les ordres pas à pas), Ansible est **déclaratif**. On lui décrit l'**état final souhaité**. 
* **Le principe :** On ne dit pas "Exécute apt-get install", on écrit `state: present`. 
* **L'intérêt :** Cela permet l'**idempotence**. Ansible vérifie l'état actuel de la machine. Si le service est déjà configuré, il ne fait rien, évitant ainsi de corrompre un système déjà fonctionnel ou de dupliquer des lignes de configuration.

### Q2 : Pourquoi l’utilisation de variables est-elle essentielle ?
Les variables sont le socle de la **flexibilité** en automatisation. Elles permettent de :
* **Séparer le code de la donnée :** On maintient un Playbook "propre" et générique.
* **Mutualisation :** Un même Playbook peut déployer un serveur de Test ou de Production simplement en changeant un fichier de variables.
* **Maintenance simplifiée :** Modifier une valeur à un seul endroit (le fichier `vars`) met à jour l'intégralité de l'infrastructure associée.

### Q3 : En quoi Ansible facilite-t-il la gestion de plusieurs serveurs ?
Ansible brille par sa capacité de **passage à l'échelle (Scalability)** :
* **Inventaire structuré :** On peut regrouper les machines par types (ex: `[web]`, `[db]`).
* **Exécution parallèle :** Ansible peut configurer des centaines de serveurs simultanément via SSH.
* **Consistance :** Il garantit que l'intégralité d'un parc informatique possède exactement les mêmes versions logicielles et correctifs de sécurité, éliminant le risque de "dérive de configuration".

### Q4 : Quels sont les avantages et les limites d’Ansible en DevOps ?
* **Avantages :** * **Agentless :** Aucun logiciel à installer sur les cibles, ce qui réduit la surface d'attaque et la consommation de ressources.
    * **Lisibilité :** Le format YAML est compréhensible par les développeurs et les administrateurs, facilitant la collaboration DevOps.
* **Limites :** * **Performances :** Pour des parcs de plus de 10 000 machines, les outils avec agents (comme Salt) sont parfois plus rapides.
    * **Orchestration complexe :** Bien qu'excellent pour la configuration, Ansible est moins adapté que Terraform pour la gestion du cycle de vie pur des ressources Cloud (Provisioning).

### Q5 : Quelle est la différence entre les modules `copy` et `template` ?
* **Le module `copy`** est purement statique : il transfère un fichier binaire ou texte tel quel, comme un simple copier-coller.
* **Le module `template`** est dynamique : il utilise le moteur **Jinja2**. Il analyse le fichier source, remplace les variables (ex: `{{ author }}`) par leurs valeurs réelles au moment de l'exécution, puis génère le fichier final sur le serveur. C'est l'outil indispensable pour personnaliser les fichiers de configuration selon le contexte de chaque machine.

---

## 🌐 Résultat Final
Une fois le déploiement terminé, la page d'accueil affiche dynamiquement :
* Le titre de l'atelier
* Le nom de l'étudiant (**Jean-Gérard HOUNKANRIN**)
* Le nom de l'encadrant (**Boris STOCKER**)
* Un lien direct vers le campus de l'**EPSI Paris**.

