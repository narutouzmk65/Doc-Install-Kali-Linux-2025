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
  - [4.2 Sélection de la langue](#42-sélection-de-la-langue)
  - [4.3 Situation géographique et clavier](#43-situation-géographique-et-clavier)
  - [4.4 Configuration réseau](#44-configuration-réseau)
  - [4.5 Nom de la machine et domaine](#45-nom-de-la-machine-et-domaine)
  - [4.6 Création des utilisateurs](#46-création-des-utilisateurs)
  - [4.7 Partitionnement du disque](#47-partitionnement-du-disque)
  - [4.8 Installation du système de base](#48-installation-du-système-de-base)
  - [4.9 Choix de l'environnement de bureau](#49-choix-de-lenvironnement-de-bureau)
  - [4.10 Gestionnaire de session et fin d'installation](#410-gestionnaire-de-session-et-fin-dinstallation)
  - [4.11 Première connexion](#411-première-connexion)
  - [4.12 Création d'un utilisateur supplémentaire en CLI](#412-création-dun-utilisateur-supplémentaire-en-cli)
  - [4.13 Modification du mot de passe root](#413-modification-du-mot-de-passe-root)

---

## 1. Origine de la distribution Kali Linux

**Kali Linux** est une distribution dérivée de **Debian**.

---

## 2. Les deux types de tests d'intrusion

### 2.1 Test d'intrusion externe (External Penetration Test)

Ce test simule une attaque venant d'Internet, comme le ferait un pirate n'ayant aucun accès interne.

**Mise en œuvre :**
- Analyse des services exposés sur Internet (scan de ports, services, versions)
- Recherche de vulnérabilités exploitables à distance
- Tentatives d'exploitation (failles web, failles réseau, mots de passe faibles…)
- Vérification de l'accès possible au système interne
- Rapport détaillé des failles trouvées

### 2.2 Test d'intrusion interne (Internal Penetration Test)

Ce test simule une attaque venant de l'intérieur du réseau, par exemple un employé malveillant ou un attaquant ayant déjà compromis un poste.

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

Une fois la configuration de votre machine virtuelle Kali Linux terminée, lancez la VM. Vous arriverez sur un menu similaire à celui-ci. Dans notre cas, il faudra sélectionner l'option **Graphical Install**.

L'option **Install** permet également d'installer Kali Linux, mais uniquement en **mode CLI (sans interface graphique)**. Pour ce TP, nous avons besoin d'un environnement graphique. Notez toutefois que la version CLI peut être intéressante pour les utilisateurs avancés de Linux.

![Menu d'installation Kali Linux](images/image1.jpg)

---

### 4.2 Sélection de la langue

Lorsque vous aurez appuyé sur la touche Entrée, l'assistant d'installation vous demandera de sélectionner une langue. Dans cet exemple, le choix est **Français**.

![Sélection de la langue](images/image2.jpg)

---

### 4.3 Situation géographique et clavier

La sélection de la situation géographique permettra de **déterminer automatiquement la disposition du clavier** (par exemple **AZERTY** pour les **Français**, **QWERTY** pour les **Anglais**), mais aussi de configurer les paramètres d'heure locale du système.

![Sélection de la situation géographique](images/image3.jpg)

Ensuite, l'assistant d'installation vous proposera de choisir la disposition de votre clavier. Normalement, si vous avez correctement défini la localisation géographique auparavant, l'assistant devrait sélectionner automatiquement la langue et la disposition adaptées.

![Configuration du clavier](images/image4.jpg)

---

### 4.4 Configuration réseau

Une fois les étapes précédentes effectuées, l'assistant proposera de configurer le réseau de votre machine virtuelle. Deux options sont disponibles :

- **La configuration automatique :** les serveurs DHCP de votre réseau se chargeront d'attribuer automatiquement les paramètres réseau (adresse IP, DNS, passerelle, serveur WINS, etc.)
- **La configuration manuelle :** vous devrez saisir vous‑même tous les paramètres réseau directement dans l'assistant

> Dans cet exemple, la **configuration automatique** a été choisie.

![Configuration réseau](images/image5.jpg)

---

### 4.5 Nom de la machine et domaine

L'étape suivante consiste à **définir le nom de votre machine**. Ce nom permettra de **l'identifier sur votre réseau**, notamment auprès du serveur DHCP si vous en utilisez un. Dans cet exemple, le nom choisi est **srv-kali-001**.

![Définition du nom de machine](images/image6.jpg)

L'étape suivante consiste à **joindre votre machine à un domaine Active Directory**, si vous en disposez d'un. Dans notre TP, nous n'en avons pas, donc cette étape n'est pas nécessaire. Toutefois, si vous aviez un domaine, vous devriez saisir **le nom de machine de votre contrôleur de domaine ainsi que le nom d'utilisateur associé** pour permettre l'intégration de la machine.

![Configuration du domaine Active Directory](images/image7.jpg)

---

### 4.6 Création des utilisateurs

La suite de l'installation consiste à **créer les utilisateurs de la machine**. Dans un premier temps, on **configurera un utilisateur standard**, qui **ne possède pas tous les droits sur le système**. Ensuite, on **configurera le compte super‑administrateur, qui dispose de l'ensemble des privilèges.**

Commencer par l'utilisateur standard — saisir un nom d'utilisateur (ex : `naruto`) :

![Création de l'utilisateur standard](images/image8.jpg)

L'assistant demandera ensuite de définir le nom d'utilisateur du super-administrateur. Le mot de passe ne sera pas demandé à ce stade — il pourra être configuré plus tard en utilisant le mot de passe par défaut qui est en général **"root"** ou **"kali"** en ligne de commande.

![Nom d'utilisateur super-administrateur](images/image9.jpg)

Définir ensuite le mot de passe de l'utilisateur standard :

![Définition du mot de passe utilisateur standard](images/image10.jpg)

---

### 4.7 Partitionnement du disque

Les utilisateurs étant configurés, on passe au partitionnement du disque dur.

L'assistant proposera plusieurs options. Dans notre cas, **choisir l'option Assisté – utiliser un disque entier** :

![Choix de la méthode de partitionnement](images/image11.jpg)

Sélectionner ensuite le disque à partitionner :

![Sélection du disque à partitionner](images/image12.jpg)

Choisir l'organisation des partitions. Dans notre cas, **tout dans une seule et même partition** :

![Schéma de partitionnement](images/image13.jpg)

Cliquer sur **Terminer** :

![Finalisation du partitionnement](images/image14.jpg)

L'assistant demandera ensuite de confirmer l'application des changements. Veillez à correctement sélectionner **Oui**, car si vous choisissez **Non la procédure se répètera en boucle et l'installation n'avancera pas.**

![Confirmation de l'application des changements](images/image15.jpg)

---

### 4.8 Installation du système de base

L'installation du système de base démarre automatiquement :

![Installation du système de base](images/image16.jpg)

---

### 4.9 Choix de l'environnement de bureau

Choisir l'environnement de bureau. Dans notre cas, sélectionner **GNOME**. Si celui‑ci n'est pas coché par défaut, pensez à l'activer avant de poursuivre l'installation.

![Sélection de l'environnement de bureau GNOME](images/image17.jpg)

L'installation des logiciels se déroule ensuite via la barre de progression :

![Installation des logiciels en cours](images/image18.jpg)

---

### 4.10 Gestionnaire de session et fin d'installation

Choisir le gestionnaire de session graphique — laisser sur **gdm3** :

![Configuration du gestionnaire de session gdm3](images/image19.jpg)

Si l'installation s'est déroulée correctement, une fenêtre de fin d'installation apparaît. Sélectionner **Continuer** pour redémarrer la VM.

Au redémarrage, appuyer sur **Entrée** pour accéder à l'OS :

![Menu de démarrage Kali Linux](images/image20.jpg)

---

### 4.11 Première connexion

Une fois que Kali Linux a redémarré, se connecter avec l'**utilisateur standard** défini lors de l'installation (identifiant et mot de passe) :

![Écran de connexion Kali Linux](images/image21.jpg)

Une fois connecté, vous avez accès au bureau de Kali Linux :

![Bureau de Kali Linux](images/image22.jpg)

---

### 4.12 Création d'un utilisateur supplémentaire en CLI

Maintenant que nous sommes connectés, nous allons ouvrir un terminal en mode administrateur afin de créer un utilisateur supplémentaire : `btssio`.

Appuyer sur la touche **Windows**, rechercher **Terminal**, puis sélectionner le **terminal rouge** (mode administrateur). Cette méthode évite d'avoir à taper `sudo` devant chaque commande. Il est également possible d'ouvrir un terminal classique et de taper `su -` avec les identifiants d'un compte administrateur.

![Recherche du terminal administrateur](images/image23.jpg)

Une fois Entrée cliqué, une fenêtre d'authentification apparaît — se connecter avec un compte admin :

![Fenêtre d'authentification administrateur](images/image24.jpg)

Si la saisie est correcte, le terminal root s'ouvre :

![Terminal root ouvert](images/image25.jpg)

Pour créer un utilisateur, exécuter la commande `adduser` suivie du nom souhaité :

```bash
adduser btssio
```

![Commande adduser btssio](images/image26.jpg)

Renseigner un mot de passe (ex : `btssio`) :

![Saisie du mot de passe du nouvel utilisateur](images/image27.jpg)

Si l'assistant demande de saisir un nom ou un prénom, appuyer simplement sur **Entrée** — ces informations ne sont pas nécessaires. Taper **y** pour valider l'ensemble des informations.

Vérifier que la création s'est bien déroulée avec la commande :

```bash
cat /etc/passwd
```

![Commande cat /etc/passwd](images/image28.jpg)

Le résultat doit afficher une ligne similaire à :

![Résultat cat /etc/passwd avec l'utilisateur btssio](images/image29.jpg)

```
btssio:x:1001:1001:,,,:/home/btssio:/bin/bash
```

---

### 4.13 Modification du mot de passe root

Pour modifier le compte root (super-admin), taper la commande `passwd` suivie du nom du compte super-admin, puis appuyer sur **Entrée** :

```bash
passwd root
```

![Commande passwd root](images/image30.jpg)

Définir ensuite le nouveau mot de passe :

![Confirmation du nouveau mot de passe root](images/image31.jpg)

```
passwd : mot de passe mis à jour avec succès
```
