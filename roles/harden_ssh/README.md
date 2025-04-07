# Rôle Ansible : harden_ssh

## 🎯 Objectif

Ce rôle Ansible a pour objectif de **renforcer la sécurité des connexions SSH** sur une machine Linux Debian-like en conformité avec les recommandations d’une PSSI.

Il permet d'appliquer des réglages de durcissement sur le service `sshd`, de restreindre les paramètres de chiffrement, et d'afficher une bannière légale.  
Il est destiné à être utilisé dans des environnements **Linux** (Debian), dans un cadre de **formation**, **test**, ou de **préparation à la production**.

---

## 📦 Fonctions assurées

Ce rôle réalise les actions suivantes :
- Copie du fichier `crypto.conf` dans `/etc/ssh/sshd_config.d/` (paramètres cryptographiques)
- Copie du fichier `harden.conf` dans `/etc/ssh/sshd_config.d/` (paramètres de sécurité avancés)
- Copie du fichier `issue.net` dans `/etc/` (bannière légale)
- Redémarrage automatique du service `ssh`

---

## ⚙️ Variables disponibles

Ce rôle ne nécessite pas de variable pour fonctionner dans sa version actuelle.  

---

## 🧰 Prérequis

- Système cible : **Debian 11+**
- Ansible version : `>= 2.11`
- L’utilisateur Ansible doit avoir les **droits sudo**
- `sudo` doit être installé et configuré pour demander un mot de passe (sans `NOPASSWD`)
- Connexion SSH avec **clé privée configurée**
- Utilisation recommandée avec l’option `--ask-become-pass`

---

## 🚀 Exemple d’utilisation

```yaml
- name: Appliquer le durcissement SSH
  hosts: debian
  become: true
  roles:
    - role: harden_ssh
```

Exécution recommandée :

```bash
ansible-playbook -i inventory/hosts.yml playbooks/playbook_harden_ssh.yml -l debian --become --ask-become-pass
```

---

## 🔍 Testé sur

- ✅ Debian 12
- ✅ Debian 11
- ⛔ Ubuntu (à tester)
- ⛔ CentOS (non applicable dans ce rôle)

---

## 📚 Ressources

- [Documentation officielle Ansible](https://docs.ansible.com/)
- [ANSSI – Guide d’hygiène informatique](https://www.ssi.gouv.fr/guide/hygiene-informatique/)
- [CIS Benchmark SSH – Center for Internet Security](https://www.cisecurity.org/benchmark/ssh)
- [Rôle SSH de dev-sec](https://github.com/dev-sec/ansible-ssh-hardening)

---

## ✍️  Auteur

Rôle développé dans le cadre de la formation **Administrateur d’Infrastructures Sécurisées** à la **Wild Code School**.

**Auteur** : Julien GREGOIRE
**Date** : 07/04/2025
**Contact** : julien.gregoire@wildcodeschool.com

---

## ✅ État du rôle

| Élément                            | Statut     |
|-----------------------------------|------------|
| Code testé en local               | ✅ Oui     |
| Variables documentées             | ✅ Oui     |
| README à jour                     | ✅ Oui     |
| Conformité PSSI / bonnes pratiques| ✅ Oui     |



