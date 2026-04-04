# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.9] - 2026-04-01

### 🎉 Nouvelles fonctionnalités majeures

#### 📊 Statuts de projets
- **5 statuts personnalisables** avec codes couleur :
  - ✅ **Fini** - Vert
  - 🔧 **À améliorer** - Orange  
  - 🆕 **Commencé récemment** - Bleu clair
  - 🔄 **En cours** - Bleu
  - ❌ **Abandonné** - Rouge
- Indicateurs visuels dans l'interface principale
- Filtrage par statut

#### 🏗️ Project Builder amélioré
- **Renommage** : `Project_Builder.exe` → `ProjectsBuilder.exe`
- **Support CLI** : `ProjectsBuilder.exe --path="chemin/du/projet"`
- Intégration directe depuis l'interface

#### 🎨 Personnalisation avancée
- **Couleurs personnalisées** pour chaque projet
- **Emojis et icônes** personnalisables
- **Thèmes** par projet
- Interface adaptable aux préférences utilisateur

#### 📁 Système de catégories
- **Création de catégories** personnalisées
- **Glisser-déposer** des projets entre catégories
- Organisation hiérarchique des dossiers
- Synchronisation avec l'explorateur Windows

#### 🔐 Chiffrement de projets
- **Chiffrement complet** du contenu des projets
- **Algorithmes** : Whirlpool ou SHA-512
- **Mot de passe** sécurisé avec hachage
- **Options de rechiffrement** :
  - Manuel via bouton
  - Automatique à la fermeture

#### ⚙️ Onglet Configuration
- **Panneau central** pour toutes les options
- **Export/Import** de configuration complète
- **Sauvegarde/restauration** des préférences
- **Paramètres avancés** de l'application

### 🚀 Améliorations

#### 📋 Interface utilisateur
- **Zone de notes** agrandie et améliorée
- **Redimensionnement** avec la souris pour tous les panneaux
- **Bouton "Ouvrir avec..."** pour choisir l'application
- **Adaptation automatique** des boutons à l'espace disponible
- **Meilleur menu d'options** réorganisé

#### 📦 Gestion des projets
- **Git Clone** intégré directement dans l'interface
- **Empaquetage complet** de tous les projets en ZIP
- **Export/import** de configuration et projets
- **Sélection multiple** pour actions groupées

#### 📝 Logs améliorés
- **Catégorisation** des logs (Git, Système, Erreurs, etc.)
- **Filtrage** par type et gravité
- **Export** des logs
- **Recherche** dans les logs

### 🔧 Modifications techniques

#### 🛠️ Architecture
- **Refactoring** du système de configuration
- **Optimisation** des performances
- **Migration** automatique depuis v1.0.8
- **Compatibilité** ascendante maintenue

#### 📚 Documentation
- **README.md** mis à jour pour v1.0.9
- **Nouvelle section** de personnalisation
- **Guide** de chiffrement
- **Exemples** d'utilisation avancée

### 🐛 Corrections

- Correction de bugs mineurs d'affichage
- Stabilisation de la connexion GitHub
- Optimisation de la mémoire

---

## [1.0.8] - 2025-XX-XX

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

## [1.0.7] - 2025-XX-XX

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

## [1.0.6] - 2025-XX-XX

- Push avancé multi-branches
- Chiffrement token PAT Whirlpool + XOR
- Dialog de push avec options avancées

---

## [1.0.5] - 2025-XX-XX

- Version initiale publique
