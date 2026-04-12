# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0] - 2026-04-12

### 🎉 Nouvelles fonctionnalités

- **Nouvelle colonne Détails du projet** : affiche le type, statut, langage, catégorie, repo Git, branche, source du token et chemin.
- **Afficher/Masquer le panneau Détails** à côté du journal de logs.
- **Auto-save des notes** paramétrable depuis les paramètres, avec intervalle utilisateur en secondes.
- **Suppression de dossiers en arrière-plan** : suppression en thread non bloquant et barre de progression.

### 🛠 Améliorations

- Ajout du champ `language` aux projets et intents.
- Détection automatique du langage du projet si aucun langage n'est renseigné.

### 🎉 Nouvelles fonctionnalités majeures

#### 📊 Statuts de projets personnalisables
- **Création de statuts personnalisés** avec ID, nom, couleur et emoji
- **Autocomplétion** des statuts dans les champs de saisie
- **Interface de gestion** via Édition → 📊 Gérer les statuts
- **Rétro-compatibilité** avec les statuts par défaut existants
- **Fusion automatique** des statuts par défaut et personnalisés

#### � Catégories améliorées
- **Autocomplétion intelligente** des catégories personnalisées
- **Recherche insensitive** à la casse et mode contient
- **QCompleter** avec suggestions en temps réel
- **Intégration transparente** avec les catégories par défaut
- **Sauvegarde automatique** dans la configuration

#### �️ Robustesse accrue
- **Gestion d'erreurs Windows** "Win error : 2" améliorée
- **Fallbacks silencieux** pour éviter les plantages
- **Récupération automatique** en cas de problèmes de fichiers
- **Compatibilité Nuitka** renforcée pour l'exécutable compilé

### � Améliorations

#### 📋 Interface utilisateur
- **QCompleter** pour une meilleure expérience de saisie
- **Suggestions contextuelles** dans les formulaires
- **Gestion centralisée** des statuts et catégories
- **Messages d'erreur** plus clairs et informatifs

#### � Architecture technique
- **Refactoring** du système de configuration
- **Fonctions utilitaires** pour les statuts personnalisés
- **Gestion d'exceptions** Windows spécifiques
- **Cache optimisé** pour les performances

### 🐛 Corrections

- Correction de l'erreur "Win error : 2" après compilation
- Stabilisation de l'accès aux fichiers de configuration
- Amélioration de la gestion des permissions Windows
- Optimisation de la mémoire et des performances

---

## [1.0.8] - 2026-XX-XX

### 🐙 Connexion compte GitHub
- OAuth Device Flow (sans coller de token)
- Token OAuth persisté et chiffrable
- Restauration automatique de session
- Carte de compte GitHub dans la sidebar

### ⚡ Améliorations
- Priorité des tokens (PAT > OAuth > public)
- Diagnostic automatique amélioré
- Migration automatique config.json v3

---

## [1.0.7] - 2026-XX-XX
### ✨ Fonctionnalités
- Emplacement de stockage personnalisable
- Diagnostic automatique au démarrage
- Validation des noms sécurisée
- Cache functools pour performances

### 🔧 Technique
- Écriture atomique de config.json
- Suppression des magic numbers
- Refactoring majeur du core

---

## [1.0.6] - 2026-XX-XX

- Push avancé multi-branches
- Chiffrement token PAT Whirlpool + XOR
- Dialog de push avec options avancées

---

## [1.0.5] - 2026-XX-XX

- Version initiale publique
