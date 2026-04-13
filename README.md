# ✦ Meridian — Project Instance Manager v1.1.2

> Gestionnaire d'instances et d'intents pour Windows avec intégration GitHub, export ZIP, notes auto, thèmes, panneau de détails et cache de performances.

---

## Structure du projet

`	ext
Meridian/
├── src/
│   ├── main.py
│   ├── window.py
│   ├── core.py
│   ├── config_dialog.py
│   ├── customize_dialog.py
│   ├── encrypt_dialog.py
│   ├── categories_dialog.py
│   ├── status_dialog.py
│   ├── theme_dialog.py
│   ├── theme_manager.py
│   ├── zip_functions.py
│   └── custom_theme_dialog.py
├── assets/
│   └── icon.ico
├── data/
│   ├── config.json
│   └── backups/
├── dist/
├── env/
└── README.md
` 

> data/ est créé automatiquement à côté de l'exécutable ou du script Python.

---

## Installation

```powershell
pip install PySide6
python src/main.py
```

> Cette application est développée pour Windows et utilise PySide6 pour l'interface graphique.

---

## Fonctionnalités principales

### 🚀 Gestion des projets
- **Création** d'instances et d'intents avec validation de noms sécurisée
- **Renommage** et **suppression** de projets (suppression en arrière-plan pour les gros dossiers)
- **Ouverture rapide** dans l'Explorateur Windows, un terminal ou VS Code
- **Export ZIP** individuel ou global vers data/backups/ ou dossier personnalisé
- **Import ZIP** avec restauration complète des projets
- **Détection automatique** du langage de programmation

### 🎨 Personnalisation avancée
- **Couleur personnalisée** par projet avec palette de couleurs
- **Emoji** associé à chaque projet pour identification visuelle
- **Catégories** personnalisées avec autocomplétion intelligente
- **Statuts** personnalisables avec emoji, couleur et nom (Fini, En cours, À améliorer, etc.)
- **Langage** de programmation par projet avec détection automatique

### 📊 Panneau Détails du projet
- **Affichage complet** : type, statut, langage, catégorie, repo Git, branche, source du token, date de création et chemin
- **Interface togglable** pour masquer/afficher les détails selon l'espace disponible
- **Mise à jour en temps réel** lors de la sélection d'un projet

### 📝 Notes et sauvegarde automatique
- **Éditeur de notes** intégré pour chaque instance ou intent avec support du formatage
- **Sauvegarde manuelle** via bouton dédié
- **Auto-save configurable** avec intervalle utilisateur en secondes
- **Restauration automatique** des notes au lancement

### 🐙 Intégration Git et GitHub complète
- **OAuth Device Flow** : connexion GitHub sans copier/coller de token
- **Gestion des tokens** : PAT par instance, token OAuth global, accès public
- **Opérations Git** : clone, init, push (multi-branches), pull, status, log, checkout
- **Configuration de repo** avec branches multiples
- **Protection des tokens** par mot de passe avec chiffrement Whirlpool + XOR
- **Compte GitHub** avec avatar et informations de profil

### 🔒 Sécurité et chiffrement
- **Chiffrement** des projets avec algorithme robuste
- **Protection** des tokens GitHub par mot de passe
- **Vault de session** pour les tokens temporaires
- **Suppression sûre** avec confirmation et barre de progression

### 🎯 Performance et cache
- **Préchargement en cache** des instances et intents pour un accès instantané
- **Suppression en arrière-plan** des gros dossiers sans bloquer l'interface
- **Cache functools** pour les opérations répétitives
- **Interface fluide** sans temps de chargement perceptible

### 🛠️ Outils intégrés
- **Projects Builder** : lancement externe pour compilation de projets
- **Terminal intégré** : ouverture directe dans le dossier du projet
- **Explorateur Windows** : accès rapide au système de fichiers
- **Diagnostic automatique** au démarrage avec rapport de santé

### ⚙️ Configuration complète
- **Thèmes** personnalisables avec support des thèmes sombres/clair
- **Police** et taille de l'interface personnalisables
- **Emplacements** de stockage personnalisés pour Instances et Intents
- **Options** de confirmation de suppression
- **Export/import** de la configuration au format JSON
- **Migration** automatique entre versions

### 🎨 Thèmes et apparence
- **Gestionnaire de thèmes** avec création de thèmes personnalisés
- **Thème sombre** par défaut avec design moderne
- **Personnalisation** des couleurs de l'interface
- **Support** des thèmes utilisateur

### 📋 Interface utilisateur
- **Menu barre** complet avec raccourcis pour toutes les fonctionnalités
- **Sidebar** avec navigation rapide et informations système
- **Listes** d'instances et intents avec recherche et filtrage
- **Panneau de logs** pour le suivi des opérations
- **Interface responsive** avec support HiDPI

---

## Fichiers importants
- src/main.py : point d'entrée de l'application.
- src/window.py : interface graphique principale et logique de navigation.
- src/core.py : logique métier, gestion de la config, Git, export ZIP, OAuth, notes et projet.
- src/config_dialog.py : paramètres globaux de l'application.
- src/customize_dialog.py : personnalisation des projets.
- src/zip_functions.py : export/import ZIP.
- assets/icon.ico : icône de l'application.
- data/config.json : configuration utilisateur et liste des projets.

---

## Notes de version
- Version actuelle : **1.1.2**
- Voir CHANGELOG.md pour l'historique complet des versions et des améliorations.

---

## Compilation Nuitka (optionnelle)

Le projet contient un environnement env/ et peut être compilé avec Nuitka si vous souhaitez générer un exécutable Windows.

---

**Merci d'utiliser Meridian.**
