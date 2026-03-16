# Mini Système de Fichiers UNIX

## Simulation d’un système de fichiers inspiré d’UNIX

Ce projet consiste à développer un mini système de fichiers inspiré d’UNIX, implémenté en C, permettant de simuler la gestion de fichiers et de répertoires dans un environnement simplifié.

Le système repose sur un fichier unique simulant une partition, dans lequel sont stockées toutes les données du système de fichiers.

Ce projet a été réalisé dans le cadre d’un projet de systèmes d’exploitation.

---

# Objectifs du projet

Les objectifs principaux étaient :

- Implémenter un système de fichiers fonctionnel
- Gérer les fichiers et répertoires
- Implémenter un système de permissions
- Gérer les liens symboliques et liens durs
- Optimiser la gestion de l’espace disque
- Ajouter une gestion des commandes concurrentes

Ce projet permet d’illustrer plusieurs concepts fondamentaux des systèmes d’exploitation.

---

# Fonctionnalités principales

Le système de fichiers permet d’effectuer les opérations suivantes :

### Gestion des fichiers

- création de fichiers
- suppression de fichiers
- copie de fichiers
- déplacement de fichiers
- lecture et écriture de contenu

### Gestion des répertoires

- création de répertoires
- navigation dans l’arborescence
- gestion de la hiérarchie des dossiers

### Gestion des permissions

Chaque fichier possède des droits d’accès similaires aux permissions UNIX permettant de contrôler :

- lecture
- écriture
- modification

Les opérations sont autorisées ou refusées en fonction des permissions de l’utilisateur. :contentReference[oaicite:1]{index=1}

---

# Structures de données principales

Le système repose sur plusieurs structures importantes :

### File

Structure représentant un fichier avec ses métadonnées :

- nom
- taille
- propriétaire
- permissions
- contenu
- table de pages mémoire

Elle permet de simuler la gestion de l’espace mémoire d’un fichier. :contentReference[oaicite:2]{index=2}

---

### Directory

Structure représentant un répertoire contenant :

- nom du répertoire
- date de création
- liste de fichiers
- lien vers le répertoire parent

Elle permet de modéliser une hiérarchie de dossiers. :contentReference[oaicite:3]{index=3}

---

### PageTableEntry

Structure utilisée pour simuler une pagination mémoire, permettant d’allouer les blocs mémoire utilisés par les fichiers.

Chaque fichier peut être stocké sur plusieurs pages physiques. :contentReference[oaicite:4]{index=4}

---

### User

Structure permettant de gérer les utilisateurs et leurs droits d’accès.

Chaque utilisateur possède :

- un nom
- un mot de passe

---

### FileSystemState

Structure centrale du système regroupant :

- les utilisateurs
- les répertoires
- l’état courant du système

Elle représente l’état global du système de fichiers.

---

### Job

Structure utilisée pour représenter les commandes exécutées dans une file d’attente, facilitant la gestion des opérations concurrentes.

---

# Algorithmes utilisés

## Gestion de l’espace disque

L’espace disque est simulé à l’aide d’un bitmap, où chaque bit représente un bloc :

- `0` → bloc libre  
- `1` → bloc occupé  

L’allocation des blocs utilise l’algorithme First Fit, qui consiste à trouver le premier bloc libre disponible. :contentReference[oaicite:5]{index=5}

---

## Gestion des fichiers

La gestion des fichiers repose sur des algorithmes simples :

### Création

1. Vérifier qu’un fichier du même nom n’existe pas
2. Vérifier la disponibilité de l’espace
3. Ajouter le fichier dans le répertoire courant

### Suppression

1. Identifier les blocs utilisés
2. Libérer les blocs dans le bitmap
3. Supprimer l’entrée dans la table du répertoire

### Déplacement et copie

Les fichiers peuvent être copiés ou déplacés entre répertoires en vérifiant :

- l’existence du fichier source
- la capacité du répertoire cible

---

# Gestion des liens

Le système implémente deux types de liens :

### Lien dur (Hard Link)

Un lien dur partage les mêmes blocs mémoire que le fichier original.

Le contenu reste accessible tant qu’au moins un lien existe.

---

### Lien symbolique (Symbolic Link)

Le lien symbolique stocke simplement le chemin vers le fichier cible.

Si le fichier cible est supprimé, le lien devient danglant.

---

# Gestion de la concurrence

Un système de file d’attente circulaire permet de gérer les commandes utilisateur.

Fonctionnement :

1. les commandes sont ajoutées à la file
2. un thread scheduler traite les commandes
3. les ressources sont protégées par des mutex

Cela permet d’éviter les conflits d’accès aux ressources du système de fichiers. :contentReference[oaicite:6]{index=6}

---

# Extensions implémentées

Plusieurs fonctionnalités avancées ont été ajoutées :

### Gestion des accès concurrents

- ordonnanceur de commandes
- file d’attente FIFO
- synchronisation avec mutex

### Sauvegarde et restauration

- sauvegarde du système de fichiers
- restauration depuis un backup

### Formatage du système

- réinitialisation complète
- recréation des structures de base

---

# Technologies utilisées

- Langage C
- Makefile
- POSIX Threads (pthread)
- structures de données
- gestion mémoire simulée

---

# Ce que ce projet m’a apporté

Ce projet m’a permis de :

- comprendre le fonctionnement interne d’un système de fichiers
- manipuler des structures de données complexes
- implémenter des algorithmes de gestion mémoire
- travailler avec la concurrence et les threads
- renforcer mes compétences en programmation système en C

---

# Auteurs

Projet réalisé par :

- **Ines Boukais**
- Samah Ikram Farez
- Ali Gouarab

Année universitaire : **2024 / 2025**

---

## Rapport
[📄 Voir le rapport](rapport.pdf)
