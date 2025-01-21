# RUST-SigTerm

## Table des Matières

- [Introduction](#introduction)
- [Description](#description)
- [Fonctionnalités](#fonctionnalités)
- [Architecture du Projet](#architecture-du-projet)
- [Installation](#installation)
  - [Prérequis](#prérequis)
  - [Étapes d'installation](#étapes-dinstallation)
- [Utilisation](#utilisation)
  - [Lancer le Serveur](#lancer-le-serveur)
  - [Lancer le Client](#lancer-le-client)
  - [Commandes Disponibles](#commandes-disponibles)
- [Configuration](#configuration)
- [Sécurité](#sécurité)
  - [Mécanismes de Sécurité](#mécanismes-de-sécurité)
  - [Améliorations Futures](#améliorations-futures)

---

## Introduction

**RUST-SigTerm** est une solution de messagerie sécurisée construite en Rust, visant à fournir des communications privées et fiables entre utilisateurs. Ce projet met l'accent sur une sécurité robuste grâce à l'utilisation d'algorithmes modernes de chiffrement et de techniques de gestion des erreurs.

---

## Description

Le projet repose sur un modèle client-serveur. Les messages envoyés entre les utilisateurs sont chiffrés et passent par un serveur centralisé. Les principales fonctionnalités incluent la gestion des utilisateurs, la prévention des abus (anti-spam), et un chiffrement avancé pour garantir la confidentialité des messages.

---

## Fonctionnalités

### Principales
- **Chiffrement AES-256-GCM** : Garantit la confidentialité des communications.
- **Multi-Clients** : Prise en charge simultanée de plusieurs connexions.
- **Commandes Utilisateur** :
  - `/help` : Liste des commandes disponibles.
  - `/list` : Affiche les utilisateurs connectés.
  - `/quit` : Déconnexion propre.
- **Anti-Spam** : Prévention des abus via des limites de fréquence.
- **Journalisation** : Suivi des événements critiques (connexions, erreurs).
- **Gestion des Erreurs** : Retour d'informations sécurisées en cas de problème.

### Avancées
- Modularité du code pour une extension facile.
- Intégration d'un fichier de configuration `config.toml`.
- Support pour une éventuelle utilisation avec Docker.

---

## Architecture du Projet

Le projet suit une architecture modulaire et bien organisée pour faciliter la maintenance :

```plaintext
.
├── Cargo.toml       # Dépendances et métadonnées
├── src/             # Code source principal
│   ├── bin/         # Points d'entrée pour le serveur et le client
│   ├── client/      # Modules spécifiques au client
│   ├── crypto/      # Gestion du chiffrement et des clés
│   ├── logger.rs    # Gestion des journaux
│   ├── messages.rs  # Gestion des messages
│   ├── server/      # Modules spécifiques au serveur
│   ├── storage/     # Gestion des clés et des données persistantes
│   └── util/        # Fonctions utilitaires
├── config.toml      # Configuration personnalisée
├── docker/          # Configuration pour Docker (optionnelle)
└── Readme.md        # Documentation
```

---

## Installation

### Prérequis
Avant de commencer, assurez-vous d'avoir installé :
- **Rust** : [Installer via rustup](https://rustup.rs/).
- (Optionnel) **Docker** : Pour exécuter dans un conteneur.

### Étapes d'installation

1. **Cloner le dépôt**
   ```bash
   git clone https://github.com/MatthieuBarraque/Rust-Cipher-SecureComms.git
   cd Rust-Cipher-SecureComms
   ```

2. **Construire le projet**
   Utilisez Cargo pour compiler le code en mode production :
   ```bash
   cargo build --release
   ```

3. **Configurer le fichier TOML (Optionnel)**
   Modifiez `config.toml` pour adapter l'application à vos besoins.

---

## Utilisation

### Lancer le Serveur
Dans un terminal :
```bash
./target/realese/secure_chat
```
Le serveur démarre et attend les connexions sur le port spécifié dans `config.toml`.

### Lancer le Client
Dans un autre terminal :
```bash
./target/realese/client
```
Suivez les instructions pour choisir un nom d'utilisateur et commencer à chatter.

### Commandes Disponibles
- **/help** : Affiche les commandes disponibles.
- **/list** : Liste les utilisateurs connectés.
- **/quit** : Quitte proprement le serveur.

---

## Configuration

Le comportement du projet peut être ajusté avec `config.toml` :

```toml
[server]
address = "127.0.0.1"
port = 7878

[security]
max_messages_per_sec = 5
```

Pour appliquer des configurations personnalisées, placez ce fichier dans le répertoire racine et modifiez `src/main.rs` pour qu'il le charge dynamiquement.

---

## Sécurité

### Mécanismes de Sécurité
1. **Chiffrement** :
   - Algorithme AES-256-GCM pour protéger les messages.
   - Gestion des clés de session unique par utilisateur.

2. **Anti-Spam** :
   - Limite la fréquence des messages pour éviter les abus.

3. **Validation des Messages** :
   - Les messages sont vérifiés avant traitement.

4. **Journalisation** :
   - Les événements critiques sont enregistrés avec un système de niveaux (INFO, WARNING, ERROR).

### Améliorations Futures
- **Échange de Clés Sécurisé** : Implémentation de Diffie-Hellman.
- **Chiffrement de Bout en Bout** : Garantir que seuls l'expéditeur et le destinataire peuvent lire les messages.
- **TLS** : Protéger les communications réseau contre les interceptions.

---
