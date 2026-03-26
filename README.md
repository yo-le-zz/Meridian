# ✦ Meridian — Project Instance Manager

> **Gestionnaire de dossiers de projets pour Windows.**  
> Créez, organisez et versionez vos instances et intents sur n'importe quel disque,  
> avec intégration GitHub, export/import ZIP et chiffrement des tokens PAT.

---

## Architecture du projet

```
Meridian/
├── src/
│   ├── main.py       → Point d'entrée
│   ├── window.py     → Interface PySide6
│   └── core.py       → Logique métier
│
├── assets/
│   └── icon.ico      → Icône de l'application
│
├── data/             → Créé automatiquement à côté du script / de l'exe
│   ├── config.json   → Registre de toutes les instances et intents
│   ├── config.json.bak → Sauvegarde automatique avant réparation
│   └── backups/      → Archives .zip exportées automatiquement
│
├── dist/             → Sortie de compilation Nuitka
└── README.md
```

> **`data/` est toujours à côté de l'exécutable** — en mode développement comme en mode compilé Nuitka.

---

## Architecture sur le disque externe (par défaut)

```
D:\Meridian\
├── Instances\
│   ├── MonProjet\        ← dossier vide, l'utilisateur fait ce qu'il veut
│   └── AutreProjet\
│
└── Intents\
    ├── SearchIntent\
    └── WelcomeIntent\
```

> En v1.0.7, ces chemins sont entièrement personnalisables depuis **⚙ Paramètres → Emplacement de stockage**.

---

## Installation & lancement

```bash
pip install PySide6
python src/main.py
```

---

## Fonctionnalités

### Instances et Intents
- Créer un dossier vide (instance ou intent) sur le disque de son choix **ou dans un dossier personnalisé**
- Supprimer définitivement
- **Exporter** en `.zip` (backup auto dans `data/backups/` ou dossier personnalisé)
- **Importer** depuis un `.zip`
- Ouvrir dans l'Explorateur Windows
- Ouvrir un terminal `cmd` positionné sur le dossier
- Ouvrir VS Code dans le dossier

### GitHub (instances uniquement)
- Lier un repository GitHub (sauvegardé dans `data/config.json`)
- Git Init local
- Push initial complet (`add`, `commit`, `remote add`, `push`)
- Commit & Push avancé vers une ou plusieurs branches simultanées
- Options : `--force`, `--follow-tags`, `--no-verify`
- Option : lier sans pousser (décocher "Push initial")
- Chiffrement du token PAT : Whirlpool + XOR (SHA-512 en fallback)

### Emplacement de stockage personnalisé (v1.0.7)
- Choisir un dossier arbitraire pour stocker les Instances et les Intents
- Indépendant du disque sélectionné dans la barre latérale
- Configurable via **⚙ Paramètres → Emplacement de stockage**
- Rétro-compatible : laisser vide pour garder le comportement `{Disque}\Meridian\...`

### Diagnostic & Réparation automatique (v1.0.7)
Détection automatique de problèmes au démarrage et via **⚙ Paramètres → Lancer un diagnostic** :

| Problème détecté | Catégorie | Action automatique |
|---|---|---|
| `config.json` corrompu ou illisible | `config` | Réparation avec récupération des données |
| Entrées pointant vers des dossiers absents | `data` | Suppression des entrées orphelines |
| `git` absent du PATH | `dependency` | Lien vers le téléchargement |
| `PySide6` manquant | `dependency` | Réinstallation via `pip` |

- **Données** : tentative de récupération maximale, archive de l'ancien fichier en `.bak`
- **Dépendances** : réinstallation sans toucher aux données utilisateur
- **Échec** : diagnostic clair affiché avec le détail de l'erreur

### Project Builder
- Lance `Project_Builder.exe` dans un terminal `cmd`
- Répertoire de travail positionné sur le dossier sélectionné

---

## Chemin du Project Builder

```
D:\my programme\Project_builder\Project_Builder.exe
```

Pour modifier : éditer `PROJECT_BUILDER` dans `src/core.py`.

---

## Compilation Nuitka

```bash
python -m nuitka ^
  --standalone ^
  --onefile ^
  --enable-plugin=pyside6 ^
  --windows-icon-from-ico=assets/icon.ico ^
  --windows-console-mode=disable ^
  --include-data-dir=assets=assets ^
  --output-dir=dist ^
  --output-filename=Meridian.exe ^
  src/main.py
```

> Après compilation, placer le dossier `assets/` à côté de `Meridian.exe` dans `dist/`.  
> Le dossier `data/` sera créé automatiquement au premier lancement.

### Pré-requis

```bash
pip install nuitka PySide6
```

Compilateur C requis : **Visual Studio Build Tools** ou **MinGW-w64**.

---

## Architecture technique

### Détection Nuitka vs mode script

`core.py` détecte automatiquement l'environnement :

```python
@functools.cache
def get_app_dir() -> Path:
    try:
        _ = __compiled__          # Variable injectée par Nuitka
        return Path(sys.executable).parent
    except NameError:
        return Path(__file__).resolve().parent.parent
```

### Cache avec functools (v1.0.7)

Les fonctions pures (chemins, disponibilité Whirlpool) sont mises en cache via `@functools.cache` pour éviter les appels répétés au système de fichiers.  
La configuration est mise en cache en mémoire et invalidée automatiquement à chaque écriture.

### Écriture atomique de la config (v1.0.7)

`config.json` est écrit via un fichier temporaire `.tmp` puis renommé, évitant toute corruption en cas d'interruption.

### Validation des noms (v1.0.7)

Chaque nom d'instance ou d'intent est validé avant création (`core.validate_name`) :
- Non vide, ≤ 128 caractères
- Sans caractères réservés Windows : `\ / : * ? " < > |`
- Sans séquences de traversée de chemin (`..`)

### Rétro-compatibilité (v1.0.7)

`config.json` est migré automatiquement depuis toutes les versions antérieures :
- v1.0.5 → v1.0.6 : ajout de `github_branches`, `github_token_protected`
- v1.0.6 → v1.0.7 : ajout de `storage` (emplacements personnalisés), `_schema_version`

---

## Changelog

### v1.0.7
- ✨ Emplacement de stockage personnalisable (instances et intents)
- 🩺 Diagnostic automatique au démarrage + réparation guidée
- 🔐 Validation des noms (sécurité anti path-traversal)
- ⚡ Cache `functools` pour les fonctions pures
- 💾 Écriture atomique de `config.json` (résistance aux crashs)
- 🧹 Suppression des magic numbers (constantes nommées)
- 🔄 Migration automatique depuis toutes les versions antérieures
- 🛠 Refactoring : `_find_entry` / `_update_entry` / `_get_note` / `_set_note`

### v1.0.6
- Push avancé multi-branches (GitQueue)
- Chiffrement token PAT Whirlpool + XOR
- Dialog de push avec options avancées

### v1.0.5
- Version initiale publique
