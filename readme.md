# Documentation Kali Linux 2025-1

---

## Sommaire

- [1. Origine de la distribution Kali Linux](#1-origine-de-la-distribution-kali-linux)
- [2. Les deux types de tests d'intrusion](#2-les-deux-types-de-tests-dintrusion)
  - [2.1 Test d'intrusion externe](#21-test-dintrusion-externe-external-penetration-test)
  - [2.2 Test d'intrusion interne](#22-test-dintrusion-interne-internal-penetration-test)
- [3. Outils pré-installés dans Kali Linux](#3-outils-pré-installés-dans-kali-linux)
- [4. Installation et configuration de Kali Linux](#4-installation-et-configuration-de-kali-linux)
  - [4.1 Lancement de l'installation](#41-lancement-de-linstallation)
  - [4.2 Langue et localisation](#42-langue-et-localisation)
  - [4.3 Configuration réseau](#43-configuration-réseau)
  - [4.4 Nom de la machine et domaine](#44-nom-de-la-machine-et-domaine)
  - [4.5 Création des utilisateurs](#45-création-des-utilisateurs)
  - [4.6 Partitionnement du disque](#46-partitionnement-du-disque)
  - [4.7 Choix de l'environnement de bureau](#47-choix-de-lenvironnement-de-bureau)
  - [4.8 Gestionnaire de session et fin d'installation](#48-gestionnaire-de-session-et-fin-dinstallation)
  - [4.9 Première connexion](#49-première-connexion)
  - [4.10 Création d'un utilisateur supplémentaire en CLI](#410-création-dun-utilisateur-supplémentaire-en-cli)
  - [4.11 Modification du mot de passe root](#411-modification-du-mot-de-passe-root)

---

## 1. Origine de la distribution Kali Linux

**Kali Linux** est une distribution dérivée de **Debian**.

---

## 2. Les deux types de tests d'intrusion

### 2.1 Test d'intrusion externe (External Penetration Test)

Ce test simule une attaque provenant d'Internet, comme le ferait un pirate n'ayant aucun accès interne.

**Mise en œuvre :**
- Analyse des services exposés sur Internet (scan de ports, services, versions)
- Recherche de vulnérabilités exploitables à distance
- Tentatives d'exploitation (failles web, failles réseau, mots de passe faibles…)
- Vérification de l'accès possible au système interne
- Rapport détaillé des failles trouvées

### 2.2 Test d'intrusion interne (Internal Penetration Test)

Ce test simule une attaque provenant de l'intérieur du réseau, par exemple un employé malveillant ou un attaquant ayant déjà compromis un poste.

---

## 3. Outils pré-installés dans Kali Linux

| Outil | Rôle |
|---|---|
| **Nmap** | Scanner de ports et de services. Permet d'identifier les machines, services ouverts, versions, OS… |
| **Metasploit Framework** | Plateforme d'exploitation de failles. Permet de lancer des attaques automatisées et d'exploiter des vulnérabilités. |
| **Wireshark** | Analyseur de paquets réseau. Sert à capturer et analyser le trafic en détail. |
| **Hydra** | Outil de force brute pour tester des mots de passe sur de nombreux protocoles (SSH, FTP, HTTP…). |
| **Burp Suite** | Suite d'outils pour tester la sécurité des applications web (proxy, scanner, repeater…). |

---

## 4. Installation et configuration de Kali Linux

### 4.1 Lancement de l'installation

Une fois la configuration de votre machine virtuelle Kali Linux terminée, lancez la VM. Vous arriverez sur le menu d'installation GRUB.

Sélectionnez l'option **Graphical Install**.

> **Note :** L'option `Install` permet également d'installer Kali Linux, mais uniquement en mode **CLI** (sans interface graphique). Pour ce TP, l'environnement graphique est requis. La version CLI peut toutefois être intéressante pour les utilisateurs avancés.

---

### 4.2 Langue et localisation

1. Sélectionnez votre **langue** (ex : Français)
2. Choisissez votre **situation géographique** — cela détermine automatiquement :
   - La disposition du clavier (AZERTY pour les Français, QWERTY pour les Anglais)
   - Les paramètres d'heure locale du système

L'assistant sélectionne automatiquement la disposition adaptée si la localisation a été correctement définie.

---

### 4.3 Configuration réseau

L'assistant vous proposera deux options :

- **Configuration automatique** : les serveurs DHCP de votre réseau attribuent automatiquement les paramètres réseau (adresse IP, DNS, passerelle, serveur WINS, etc.)
- **Configuration manuelle** : vous saisissez vous-même tous les paramètres réseau

> Dans cet exemple, la **configuration automatique** a été choisie.

---

### 4.4 Nom de la machine et domaine

**Nom de la machine :** Ce nom permet d'identifier la machine sur le réseau (ex : `srv-kali-001`).

**Domaine Active Directory :** Si vous disposez d'un domaine AD, vous devrez saisir :
- Le nom de machine du contrôleur de domaine
- Le nom d'utilisateur associé au contrôleur de domaine

> Dans ce TP, aucun domaine AD n'est utilisé — cette étape est ignorée.

---

### 4.5 Création des utilisateurs

L'installation crée deux types de comptes :

1. **Utilisateur standard** — ne possède pas tous les droits sur le système
2. **Super-administrateur (root)** — dispose de l'ensemble des privilèges

**Étapes :**

1. Saisir le **nom complet** de l'utilisateur standard (ex : `naruto`)
2. Saisir le **nom d'utilisateur** du super-administrateur (ex : `hinata`)
3. Définir le **mot de passe** de l'utilisateur standard

> Le mot de passe du compte root peut être configuré plus tard via la commande `passwd root`. Les mots de passe par défaut sont généralement `root` ou `kali`.

---

### 4.6 Partitionnement du disque

1. Choisir la méthode : **Assisté – utiliser un disque entier** (recommandé)
2. Sélectionner le disque à partitionner
3. Choisir le schéma de partitionnement : **Tout dans une seule partition** (recommandé pour les débutants)
4. Valider en sélectionnant **Terminer le partitionnement et appliquer les changements**
5. Confirmer en sélectionnant **Oui**

> ⚠️ Si vous choisissez **Non**, la procédure se répètera en boucle et l'installation n'avancera pas.

L'installation du système de base démarre ensuite automatiquement.

---

### 4.7 Choix de l'environnement de bureau

Sélectionnez l'environnement de bureau souhaité. Dans ce TP : **GNOME**.

> Si GNOME n'est pas coché par défaut, pensez à l'activer avant de poursuivre.

L'installation des logiciels se déroule ensuite via une barre de progression.

---

### 4.8 Gestionnaire de session et fin d'installation

- Choisir le gestionnaire de session graphique : laisser sur **gdm3**
- Une fois l'installation terminée, cliquer sur **Continuer** pour redémarrer la VM
- Appuyer sur **Entrée** au redémarrage pour accéder à l'OS

---

### 4.9 Première connexion

Après le redémarrage, connectez-vous avec l'**utilisateur standard** créé pendant l'installation (identifiant + mot de passe).

Vous aurez alors accès au bureau de Kali Linux.

---

### 4.10 Création d'un utilisateur supplémentaire en CLI

Pour créer un utilisateur supplémentaire (ex : `btssio`) :

1. Appuyer sur la touche **Windows** et rechercher **Terminal**
2. Sélectionner le **terminal rouge** (mode administrateur) — cela évite de taper `sudo` devant chaque commande

   > Alternative : ouvrir un terminal classique et taper `su -` puis entrer les identifiants d'un compte administrateur.

3. Créer l'utilisateur avec la commande :

```bash
adduser btssio
```

4. Définir un mot de passe (ex : `btssio`)
5. Pour les champs nom/prénom, appuyer simplement sur **Entrée** (non obligatoires)
6. Taper **y** pour valider

**Vérifier la création de l'utilisateur :**

```bash
cat /etc/passwd
```

Le résultat doit afficher une ligne similaire à :

```
btssio:x:1001:1001:,,,:/home/btssio:/bin/bash
```

---

### 4.11 Modification du mot de passe root

Pour définir ou modifier le mot de passe du super-administrateur root :

```bash
passwd root
```

Saisir puis confirmer le nouveau mot de passe. Le terminal affichera :

```
passwd : mot de passe mis à jour avec succès
```
