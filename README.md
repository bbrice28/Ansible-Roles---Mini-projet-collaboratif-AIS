# Ansible Roles — Mini-projet collaboratif AIS

Ce dépôt GitHub est le support d’un projet collaboratif réalisé dans le cadre de la formation **Administrateur d’Infrastructures Sécurisées (AIS)** à la Wild Code School. 
Il rassemble des **rôles Ansible individuels** créés et maintenus par les élèves et le formateur, chacun portant sur l'automatisation d'une tâche d'administration ou de sécurisation issue de l'expérience en entreprise ou des ateliers de formation.


---

## 📚 Sommaire

- [🎯 Objectifs pédagogiques](#-objectifs-p%C3%A9dagogiques)
- [🤝 Contribuer](#-contribuer)
- [📌 Exemples de rôles possibles](#-exemples-de-r%C3%B4les-possibles)
    - [Rôles d’administration Linux](#r%C3%B4les-dadministration-linux)
    - [Rôles Windows](#r%C3%B4les-windows)
    - [Rôles Réseau](#r%C3%B4les-r%C3%A9seau-mat%C3%A9rielemulation-cisco-juniper-etc)
- [📁 Contenu du dépôt](#-contenu-du-d%C3%A9p%C3%B4t)
- [⚙️ Fichier `.gitignore`](#%EF%B8%8F-fichier-gitignore)
- [🐍 Installation d’Ansible dans un environnement virtuel](#-installation-dans-un-environnement-virtuel)
- [🛠️ Fichier `ansible.cfg`](#%EF%B8%8F-fichier-ansiblecfg)
- [🧭 Inventaire](#-inventaire-inventoryhostsyml)
- [▶️ Playbooks](#%EF%B8%8F-playbooks)
- [📦 Initialiser un nouveau rôle](#-initialiser-un-nouveau-r%C3%B4le)
- [✅ Bonnes pratiques attendues](#-bonnes-pratiques-attendues)
- [👨‍🏫 Formateur référent](#-formateur-r%C3%A9f%C3%A9rent)


---

## 🎯 Objectifs pédagogiques

L'objectif est double :
1. **Renforcer la compétence des élèves sur Ansible** en appliquant concrètement l'approche *Infrastructure as Code* à des cas d'usage réels.
2. **Capitaliser sur l'expérience de chacun** pour constituer une base de rôles Ansible réutilisables, bien documentés et testés, pouvant servir de référence ou de point de départ pour d'autres projets.

Chaque élève identifie une **procédure de configuration fréquente** (par exemple : création d’un utilisateur, configuration réseau, déploiement d’un service, durcissement d’un système, etc.), puis conçoit un **rôle Ansible modulaire et documenté** pour l’automatiser.


---

## 🤝 Contribuer
1. Forker le dépôt si besoin
2. Travailler dans une branche dédiée à ton rôle (`feature/nom_du_role`)
3. Générer l'arborescence du rôle (voir [## 📦 Initialiser un nouveau rôle])
4. Ajouter le code et la documentation
5. Modifier l'inventaire pour qu'il colle à ton lab
6. Tester le rôle localement dans ton lab
7. Soumettre un **Pull Request** si tout est OK


---

## 📌 Exemples de rôles possibles

### Rôles d’administration Linux
- Création d’utilisateurs système avec clé SSH et sudo (avec gestion des droits par groupe)
- Vérification des mises à jour de sécurité disponibles
- Configuration d’un service systemd personnalisé
- Installation de paquets standards (curl, vim, git, unzip, etc.)
- Configuration NTP/chrony pour la synchronisation horaire sécurisée
- Déploiement d’un environnement bash/zsh standardisé (fichier `.bashrc`, alias, prompt, etc.)
- Configuration d’une rotation de logs via `logrotate`
- Gestion d’un fichier `/etc/hosts` partagé dans le parc
- Configuration d’un proxy système pour apt, wget, etc.
- Installation et configuration de `fail2ban` (filtrage bruteforce SSH, Apache, etc.)
- Installation de PostgreSQL ou MariaDB avec utilisateur et base initiale
- Installation et configuration de NGINX ou Apache
- Désactivation des services inutiles (ex. cups, avahi, bluetooth…)
- Gestion des permissions des fichiers sensibles (`/etc/shadow`, `/etc/ssh`, etc.)
- Déploiement de règles `ufw` ou `iptables` sécurisées
- Installation de `clamav` + scan planifié
- Audit du système avec `lynis`


### Rôles Windows
- Création de comptes locaux avec stratégie de mot de passe
- Activation de la journalisation avancée (audit) dans les stratégies locales
- Installation d’un service
- Désactivation de services non nécessaires sur poste client
- Application de paramètres de registre pour durcir la machine


### Rôles Réseau (matériel/émulation Cisco, Juniper, etc.)
- Configuration de VLANs sur un switch
- Ajout d’un utilisateur local avec privilèges en SSH
- Configuration de base sécurisée d’un routeur (mot de passe enable, ssh only, bannière ...)
- Sauvegarde automatique de la configuration courante
- Déploiement de SNMPv3 pour supervision



---

## 📁 Contenu du dépôt


```bash
.
├── ansible.cfg                  # Fichier de configuration Ansible
├── inventory/                   # Répertoire contenant l'inventaire principal
│   └── hosts.yml
├── logs/                        # Logs d'exécution
│   └── ansible.log
├── modele_readme_role           # Modèle de fichier à utiliser dans ton rôle
├── playbooks/                   # Playbooks associés aux rôles
│   └── playbook_harden_ssh.yml
├── roles/                       # Répertoire des rôles Ansible
│   └── harden_ssh/              # Exemple de rôle réalisé par le formateur
├── requirements.txt             # Dépendances Python
├── LICENSE
└── README.md                    # Ce fichier
```


### ⚙️ Fichier `.gitignore`

Ce projet utilise un fichier `.gitignore` pour **ne pas versionner** :

- `.venv` (environnement virtuel Python)
- les fichiers de logs (`logs/ansible.log`) 

---

### 🐍 Installation d’Ansible dans un environnement virtuel

1. Installer le module venv :

```bash
sudo apt update && sudo apt install python3-venv
```

2. Créer un environnement virtuel :

```bash
python3 -m venv .venv
```

3. L’activer :

```bash
source ./.venv/bin/activate
```

4. Installer les dépendances :

```bash
pip install -r requirements.txt
```

> [!info]
> Le fichier `requirements.txt` est généré avec `pip freeze > requirements.txt` depuis le venv.


---

### 🛠️ Fichier `ansible.cfg`

Ce fichier configure Ansible en prenant en compte l'arborescence du projet.


---

### 🧭 Inventaire (`inventory/hosts.yml`)

Il s’agit d’un **squelette d’inventaire évolutif**, pensé pour représenter tout un parc hétérogène.

Deux axes d’organisation :
- **Technique** : par type de machine (`linux`, `windows`, `reseau`)
- **Fonctionnel** : par rôle ou service (`glpi`, `ad`, `firewalls`, etc.)

Cette structure permet à chaque machine d'appartenir à plusieurs groupes :
- `srv-glpi` est à la fois dans `linux` → `debian` → `glpi`
- `dc01` est dans `windows`, `ad`, `dns`, `dhcp`


---

## ▶️ Playbooks

Tous les playbooks sont placés dans le dossier `playbooks/`.  
Chaque playbook :
- Commence par `playbook_`
- Est dédié à un rôle ou une action spécifique (ex : `playbook_harden_ssh.yml`)
- Doit être **lisible et ciblé** (pas de playbook "fourre-tout")


---



# 📦 Initialiser un nouveau rôle

Chaque rôle que tu crées est placé dans un sous-dossier du répertoire `roles/` et comprend :
- Une structure de rôle Ansible classique (`tasks/`, `defaults/`, `handlers/`, etc.)
- Un fichier `README.md` propre au rôle, décrivant :
  - le but du rôle
  - les variables disponibles
  - les prérequis éventuels
  - un exemple d’utilisation

Exemple :
```bash
roles/
├── harden_ssh/
│ ├── README.md
│ ├── tasks/
│ ├── defaults/
│ └── ...
├── windows_user_creation/
│ ├── README.md
│ ├── tasks/
│ ├── defaults/
│ └── ...
```

> [!success] Modèle :
> Un modèle de fichier README.md est présent à la racine du projet : `modele_readme_role`


Place-toi dans le dossier `roles/` puis lance :

```bash
ansible-galaxy role init <nom_du_role>
```

Structure classique d’un rôle :

|Dossier|Utilité|
|---|---|
|`defaults/`|Valeurs par défaut des variables|
|`tasks/`|Tâches principales du rôle|
|`files/`|Fichiers statiques à copier|
|`handlers/`|Handlers déclenchés par des changements|
|`meta/`|Dépendances ou infos sur le rôle|
|`templates/`|Fichiers Jinja2 à déployer dynamiquement|
|`tests/`|Scénarios de tests|
|`vars/`|Variables spécifiques (non surchargées par défaut)|



## ✅ Bonnes pratiques attendues
- Le rôle doit être **testé** dans un environnement de lab
- Le code doit être **modulaire, lisible, et idempotent**
- Les noms des variables doivent être explicites
- Le `README.md` doit permettre à un tiers de comprendre et utiliser le rôle sans contact direct avec son auteur
- Éviter les chemins ou valeurs en dur : privilégier la personnalisation par variables


---

**Formateur référent :** Julien GREGOIRE
**Contact :** julien.gregoire@wildcodeschool.com 
**Formation :** Administrateur d’Infrastructures Sécurisées – Wild Code School

