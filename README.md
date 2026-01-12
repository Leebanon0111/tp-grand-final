# tp-grand-final(readme)
Projet – Durcissement ANSSI d’un Windows Server avec Vagrant & Ansible
 Objectif du projet

Ce projet a pour objectif de déployer automatiquement une infrastructure de laboratoire et d’appliquer un durcissement de sécurité conforme aux recommandations de l’ANSSI sur un Windows Server, à l’aide de Vagrant, VMware Desktop et Ansible.

Il s’agit d’un TP de cybersécurité / administration systèmes mettant en œuvre :

l’Infrastructure as Code (IaC),

le principe du moindre privilège,

la réduction de la surface d’attaque,

la traçabilité et la journalisation des événements.

 Architecture du laboratoire

L’infrastructure déployée automatiquement est la suivante :

Machine	OS	Rôle
admin	Ubuntu 22.04	Machine d’administration (Ansible)
winsrv	Windows Server 2022	Serveur Windows durci (cible ANSSI)
node01	RedHat 9	Nœud Linux (cluster HA – futur)
node02	RedHat 9	Nœud Linux (cluster HA – futur)
 Plan d’adressage réseau
Machine	Adresse IP
admin	192.168.56.10
node01	192.168.56.11
node02	192.168.56.12
winsrv	192.168.56.20

Réseau host-only VMware (isolé du réseau réel).

 Technologies utilisées

Vagrant – orchestration des machines virtuelles

VMware Desktop – hyperviseur

Ansible – automatisation et durcissement

WinRM – communication Ansible ↔ Windows

Windows Server 2022

Ubuntu 22.04

RedHat 9

 Mesures de sécurité appliquées (conformes ANSSI)

Le playbook Ansible applique les actions suivantes :

 1. Mise à jour du système

Installation des correctifs critiques et de sécurité

Redémarrage automatique si nécessaire

 2. Pare-feu Windows

Activation du pare-feu sur tous les profils (Domain / Private / Public)

Autorisation exclusive du RDP depuis le réseau d’administration

 3. Comptes et privilèges

Renommage du compte Administrateur local

Génération automatique d’un mot de passe complexe

Application du principe du moindre privilège

 4. Chiffrement des données

Activation de BitLocker sur le disque système (si supporté par la VM)

Chiffrement fort (XTS-AES-256)

 En environnement virtualisé, BitLocker peut être ignoré automatiquement si non supporté (TPM absent).

 5. Réduction de la surface d’attaque

Désactivation et suppression de SMBv1

Conformité aux recommandations Microsoft & ANSSI

 6. Journalisation et audit

Augmentation de la taille du journal de sécurité

Activation de l’audit :

connexions réussies

connexions échouées

 Structure du projet
projet/
├─ Vagrantfile
└─ ansible/
   ├─ inventory.ini
   └─ windows_hardening.yml

 Lancement du projet
Prérequis

Vagrant installé

VMware Desktop installé

16 Go de RAM recommandés

Accès administrateur sur la machine hôte

Démarrage

À la racine du projet :

vagrant up


 Le processus est entièrement automatisé :

Création des machines virtuelles

Activation de WinRM sur Windows Server

Installation d’Ansible sur la VM admin

Exécution automatique du playbook de durcissement

 Connexion Ansible ↔ Windows

Protocole : WinRM

Port : 5985 (HTTP – labo uniquement)

Authentification : Basic

Cible : 192.168.56.20

 Le mode HTTP non chiffré est volontairement utilisé uniquement dans un environnement de laboratoire.

 Références et bonnes pratiques

Recommandations ANSSI – Hygiène informatique

CIS Benchmarks Windows Server

Microsoft Security Baseline

Principe Zero Trust

Infrastructure as Code (IaC)

 Évolutions possibles

Passage de WinRM en HTTPS (5986)

Intégration Active Directory

Centralisation des logs (SIEM)

Ajout de Zabbix ou Wazuh

Hardening Linux (node01 / node02)

 Contexte pédagogique

Projet réalisé dans un cadre de formation en informatique / cybersécurité, visant à démontrer :

la maîtrise des outils d’automatisation,

l’application concrète de normes de sécurité,

une approche professionnelle de l’administration système.

Si tu veux, je peux aussi te fournir :

une version plus académique (rapport de soutenance),

une check-list ANSSI commentée,

ou un schéma d’architecture pour le rendu.
