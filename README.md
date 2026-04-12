# ✦ Meridian — Project Instance Manager v1.2.0

> Gestionnaire d'instances et d'intents pour Windows avec intégration GitHub, export ZIP, notes auto, thèmes et panneau de détails.

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

`powershell
pip install PySide6
python src/main.py
` 

> Cette application est développée pour Windows et utilise PySide6 pour l'interface graphique.

---

## Fonctionnalités principales

### Gestion des projets
- Créer, renommer et supprimer des **instances** et des **intents**.
- Ouvrir le dossier dans l'Explorateur Windows, un terminal ou VS Code.
- Exporter chaque projet en .zip vers data/backups/ ou un dossier personnalisé.
- Importer des projets depuis une archive .zip.

### Panneau Détails du projet
- Affiche le type de projet, le statut, le langage, la catégorie, le repo Git, la branche, la source du token, la date de création et le chemin.
- Le panneau est **toggable** pour masquer/afficher les détails pour plus de clarté.

### Notes et auto-save
- Éditeur de notes intégré pour chaque instance ou intent.
- Sauvegarde manuelle avec un bouton dédié.
- Sauvegarde automatique des notes activable dans les paramètres avec intervalle utilisateur (en secondes).

### Suppression sûre et performante
- Suppression de dossiers volumineux effectuée dans un **thread en arrière-plan** pour éviter le freeze de l'UI.
- Barre de progression visible pendant la suppression.

### Git et GitHub
- Intégration GitHub via **OAuth Device Flow** sans copier/coller de token.
- Configuration du repo Git, push initial, commit & push, pull, merge, status, log, checkout et clone.
- Priorité des tokens : PAT instance > token OAuth global > accès public.
- Protection du token GitHub possible par mot de passe avec chiffrement.

### Personnalisation de projet
- Couleur, emoji, catégorie, statut et langage par projet.
- Gestion des statuts personnalisés avec emoji, couleur et nom.
- Gestion des catégories personnalisées avec autocomplétion.

### Configuration de l'application
- Choix du thème et de la police de l'interface.
- Emplacements de stockage personnalisés pour Instances et Intents.
- Activation/désactivation de la confirmation de suppression.
- Activation de l'auto-save et réglage de l'intervalle.
- Export/import de la configuration au format JSON.

### Thèmes et apparence
- Support des thèmes personnalisés via `theme_dialog.py` et `theme_manager.py`.
- Apparence sombre par défaut avec styles modernes.

### Chiffrement et sécurité
- Dialog pour chiffrer/déchiffrer les projets (actions disponibles dans l'UI).
- Gestion des tokens protégés pour GitHub et des actions sécurisées.

### Diagnostics et robustesse
- Contrôle de santé automatique au démarrage.
- Migration de configuration transparente entre versions.
- Gestion des erreurs d'accès Windows et de chemins corrompus.

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
- Version actuelle : **1.2.0**
- Voir CHANGELOG.md pour l'historique complet des versions et des améliorations.

---

## Compilation Nuitka (optionnelle)

Le projet contient un environnement env/ et peut être compilé avec Nuitka si vous souhaitez générer un exécutable Windows.

---

**Merci d'utiliser Meridian.**
