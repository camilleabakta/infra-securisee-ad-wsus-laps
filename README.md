# Infrastructure Sécurisée : AD, WSUS & LAPS

![Windows Server](https://img.shields.io/badge/Windows%20Server-2019-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-1.0-0078D6?style=for-the-badge&logo=microsoft&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1-5391FE?style=for-the-badge&logo=powershell&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)



## Aperçu du Projet

Ce projet a pour objectif de résoudre deux vulnérabilités critiques couramment observées dans les environnements Windows :
1. **Mots de passe administrateur locaux statiques** identiques sur toutes les machines
2. **Absence de contrôle** sur les mises à jour de sécurité

La solution implémente une infrastructure centralisée et sécurisée en combinant :
- **Active Directory** pour la gestion des identités
- **LAPS** (Local Administrator Password Solution) pour la rotation automatique des mots de passe
- **WSUS** (Windows Server Update Services) pour le contrôle des correctifs

## Technologies Utilisées
Composant	Version	Rôle
Windows Server	2019	Système d'exploitation serveur
Active Directory	Domain Services	Gestion des identités et authentification
DNS	Windows Server	Résolution de noms
LAPS	6.2.0	Gestion des mots de passe administrateur locaux
WSUS	10.0.17763	Gestion centralisée des mises à jour
Windows 10	22H2 Professionnel	Système client
PowerShell	5.1+	Automatisation et configuration

## Déploiement
Prérequis

2 Machines virtuelles ou physiques avec Windows Server 2019

1+ Machine(s) cliente(s) Windows 10 Professionnel

Connexion réseau entre toutes les machines

Accès Internet pour le serveur WSUS

Étapes d'Installation

1. Configuration du Contrôleur de Domaine
powershell

Exemple de commandes PowerShell utilisées
Import-Module ServerManager
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSForest -DomainName "entreprise.local" -DomainNetbiosName "ENTREPRISE"

2. Installation de WSUS
powershell
Install-WindowsFeature -Name UpdateServices -IncludeManagementTools

3. Déploiement de LAPS
powershell

Extension du schéma Active Directory
Update-AdmPwdADSchema

Configuration des permissions
Set-AdmPwdComputerSelfPermission -OrgUnit "OU=PC,DC=entreprise,DC=local"

4. Configuration des GPO
Téléchargez les fichiers GPO depuis le dossier GPO/

Importez-les dans la Gestion des stratégies de groupe

Liez-les aux Unités d'Organisation appropriées

Scripts d'Automatisation
Le dossier scripts/ contient des scripts PowerShell pour automatiser certaines tâches :

Deploy-LAPS.ps1 : Installation et configuration de LAPS

Configure-WSUS.ps1 : Configuration de base de WSUS

Join-Domain.ps1 : Script pour joindre des machines au domaine

## Documentation

Points Clés de Sécurité
Rotation automatique des mots de passe : LAPS génère des mots de passe complexes valides 30 jours

Audit des accès : Toutes les consultations/réinitialisations de mots de passe sont traçables

Contrôle des mises à jour : Approbation manuelle des correctifs critiques

Segmentation réseau : Unités d'organisation par département avec GPO spécifiques

## Contexte Académique
Ce projet a été réalisé dans le cadre d'un stage de Licence Professionnelle Cybersécurité, avec pour thème :

"Mise en œuvre d'une infrastructure sécurisée et managée avec Active Directory, LAPS et WSUS"

Auteur : ABAKTA Haana Camille

Tuteur de stage : Florent ADADE - Senior Manager IT - Cyber Security à Yas Togo

Période : 01 Août 2025 - 31 Octobre 2025

## Contribution
Les contributions sont les bienvenues ! Pour contribuer :

Forkez le projet

Créez une branche (git checkout -b feature/Amelioration)

Commitez vos changements (git commit -m 'Ajout d'une nouvelle fonctionnalité')

Pushez vers la branche (git push origin feature/Amelioration)

Ouvrez une Pull Request

### Licence
Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.

### Soutien
Si ce projet vous a été utile, n'hésitez pas à :
Star le dépôt

### Proposer des améliorations

## Contact
ABAKTA Haana Camille

GitHub: https://github.com/camilleabakta

LinkedIn: www.linkedin.com/in/haana-camille-abakta-a80926335

Email: camilleabakta@gmail.com
