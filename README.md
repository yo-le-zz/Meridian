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

> En v1.0.7+, ces chemins sont entièrement personnalisables depuis **⚙ Paramètres → Emplacement de stockage**.

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

### Connexion compte GitHub (v1.0.8) 🆕
- **Connexion via OAuth Device Flow** — aucun token à coller, authentification dans le navigateur
- Le compte connecté apparaît dans la sidebar avec son login GitHub
- **Token OAuth réutilisé automatiquement** pour toutes les instances liées à GitHub
- Option de protection du token OAuth par mot de passe (Whirlpool + XOR)
- Déconnexion propre depuis la sidebar ou le menu **🐙 GitHub**
- Restauration automatique de la session au démarrage

#### Priorité des tokens lors d'un push
| Situation | Token utilisé |
|---|---|
| Instance avec PAT spécifique | PAT de l'instance (prioritaire) |
| Instance sans PAT + compte connecté | Token OAuth du compte GitHub |
| Aucun token | Push en mode public uniquement |

### GitHub (instances uniquement)
- Lier un repository GitHub (sauvegardé dans `data/config.json`)
- Git Init local
- Push initial complet (`add`, `commit`, `remote add`, `push`)
- Commit & Push avancé vers une ou plusieurs branches simultanées
- Options : `--force`, `--follow-tags`, `--no-verify`
- Option : lier sans pousser (décocher "Push initial")
- Chiffrement du token PAT : Whirlpool + XOR (SHA-512 en fallback)
- Dialog de configuration affiche le compte OAuth connecté si disponible

### Emplacement de stockage personnalisé (v1.0.7)
- Choisir un dossier arbitraire pour stocker les Instances et les Intents
- Indépendant du disque sélectionné dans la barre latérale
- Configurable via **⚙ Paramètres → Emplacement de stockage**
- Rétro-compatible : laisser vide pour garder le comportement `{Disque}\Meridian\...`

### Diagnostic & Réparation automatique (v1.0.7+)
Détection automatique de problèmes au démarrage et via **⚙ Paramètres → Lancer un diagnostic** :

| Problème détecté | Catégorie | Action automatique |
|---|---|---|
| `config.json` corrompu ou illisible | `config` | Réparation avec récupération des données |
| Entrées pointant vers des dossiers absents | `data` | Suppression des entrées orphelines |
| `git` absent du PATH | `dependency` | Lien vers le téléchargement |
| `PySide6` manquant | `dependency` | Réinstallation via `pip` |
| Client ID OAuth non configuré | `config` | Avertissement (v1.0.8) |

### Project Builder
- Lance `Project_Builder.exe` dans un terminal `cmd`
- Répertoire de travail positionné sur le dossier sélectionné

---

## Configuration de l'OAuth GitHub (v1.0.8)

### 1. Créer une OAuth App

1. Allez sur https://github.com/settings/developers
2. Cliquez **"New OAuth App"**
3. Remplissez :
   - **Application name** : Meridian
   - **Homepage URL** : `http://localhost` (non utilisée)
   - **Authorization callback URL** : `http://localhost` (non utilisée avec Device Flow)
4. Cochez **"Enable Device Flow"** (important !)
5. Cliquez **"Register application"**
6. Copiez le **Client ID** affiché

### 2. Configurer Meridian

Ouvrez `src/core.py` et remplacez :

```python
GITHUB_CLIENT_ID = "Iv23liYOUR_CLIENT_ID"   # ← À remplacer
```

par votre Client ID :

```python
GITHUB_CLIENT_ID = "Iv23liAbCdEfGhIjKl"    # ← Votre vrai Client ID
```

> ⚠  Ne générez **pas** de Client Secret — le Device Flow n'en a pas besoin.  
> ⚠  Ne committez pas votre Client ID dans un repo public.

### Scopes demandés
`repo` — accès complet aux repos publics et privés (lecture + écriture).

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

### OAuth Device Flow (v1.0.8)

Le Device Flow est le seul flux OAuth qui fonctionne sans serveur web ni callback URL.

```
1. POST /login/device/code       → device_code + user_code + verification_uri
2. Affichage du user_code dans l'UI
3. L'utilisateur visite verification_uri et entre le code
4. Sondage de POST /login/oauth/access_token toutes les N secondes
5. Réponse : access_token (token OAuth)
6. GET /api/user                 → login, name, avatar_url
7. Sauvegarde dans config.json (token optionnellement chiffré)
```

### Priorité des tokens (v1.0.8)

`core.get_effective_token(instance_path)` applique la règle :
1. PAT spécifique à l'instance (vault de session ou config)
2. Token OAuth du compte GitHub connecté (session mémoire)
3. Chaîne vide (repos publics)

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

### Rétro-compatibilité

`config.json` est migré automatiquement depuis toutes les versions antérieures :
- v1.0.5 → v1.0.6 : ajout de `github_branches`, `github_token_protected`
- v1.0.6 → v1.0.7 : ajout de `storage`, `_schema_version`
- v1.0.7 → v1.0.8 : ajout de `github_account` (session OAuth)

---

## Changelog

### v1.0.8
- 🐙 **Connexion compte GitHub** via OAuth Device Flow (sans coller de token)
- 🔑 Token OAuth persisté dans `config.json` (chiffrable par mot de passe)
- 🔄 Restauration automatique de la session au démarrage
- 🃏 Carte de compte GitHub dans la sidebar (login, statut, déconnexion)
- 📋 Indicateur de source du token dans le panneau d'instance
- ⚡ `get_effective_token()` : priorité PAT instance > OAuth global
- 🩺 Avertissement diagnostic si `GITHUB_CLIENT_ID` non configuré
- 🔒 Token OAuth optionnellement chiffré (même algo Whirlpool + XOR)
- 🧵 `OAuthPollWorker` : sondage non-bloquant dans un QThread dédié
- Migration automatique `config.json` vers schéma v3

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