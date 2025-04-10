# Ansible Role — Chrony NTP Configuration

Ce projet Ansible configure **Chrony** sur une machine Debian pour assurer une synchronisation horaire fiable et sécurisée avec un serveur NTP (ex. un contrôleur de domaine Active Directory).

## 📦 Structure du projet

chrony_project/
├── inventory/
│   └── hosts
├── playbook.yml
└── roles/
└── chrony/
├── tasks/
│   └── main.yml
├── templates/
│   └── chrony.conf.j2
└── handlers/
└── main.yml

## Lancer le playbook


**cd chrony_project**
**ansible-playbook -i inventory/hosts playbook.yml**


## Rôle chrony

tasks/main.yml
	1.	Installe Chrony
	2.	Déploie le fichier de config depuis un template Jinja2
	3.	Assure que le service est actif et redémarré si besoin


## Vérification sur la machine distante
**chronyc tracking**
**chronyc sources -v**

## Pré-requis
	•	Accès SSH fonctionnel
	•	Paquet openssh-server installé sur les cibles
	•	Clé SSH configurée pour l’utilisateur distant

