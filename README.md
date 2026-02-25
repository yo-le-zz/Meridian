# ✦ Meridian — Project Instance Manager

> Application Windows de gestion d'instances et d'intents de projet.
> Interface moderne, intégration GitHub, export/import zip, désinstallation propre.

---

## Téléchargement

Télécharge la dernière version dans l'onglet [**Releases**](../../releases).

Récupère l'archive `.zip`, extrais-la dans le dossier de ton choix et lance `Meridian.exe`.

---

## Pré-requis

- Windows 10 / 11
- Un ou plusieurs disques secondaires (autre que `C:`)
- Git installé et accessible dans le `PATH` *(uniquement pour l'intégration GitHub)*

---

## Installation

1. Extrais l'archive dans le dossier de ton choix, par exemple :
   ```
   C:\Users\Toi\Apps\Meridian\
   ```
2. Lance `Meridian.exe` depuis ce dossier.
3. **Ne déplace pas `Meridian.exe` seul** — il a besoin de tous les fichiers du dossier pour fonctionner.

Au premier lancement, Meridian crée automatiquement un dossier `data/` à côté de l'exe :

```
Meridian\
├── Meridian.exe
├── ...              (fichiers de dépendances Nuitka)
├── assets\
│   └── ico\
│       └── app.ico
└── data\            ← créé automatiquement
    ├── config.json  → ta configuration, tes instances et intents enregistrés
    └── backups\     → tes exports .zip automatiques
```

> Le dossier `data/` contient toute ta configuration.
> Si tu déplaces Meridian, déplace **tout le dossier** d'un bloc.

---

## Architecture sur tes disques

Meridian organise tout dans un conteneur à la racine du disque choisi :

```
D:\Meridian\
├── Instances\
│   ├── MonProjet\       ← dossier vide, tu y mets ce que tu veux
│   └── AutreProjet\
│
└── Intents\
    ├── SearchIntent\    ← dossier vide, tu y mets ce que tu veux
    └── WelcomeIntent\
```

Chaque instance et chaque intent est un **dossier complètement vide à la création**.
Tu y mets ce que tu veux : du code, des fichiers de config, tu lances Project Builder, etc.

---

## Fonctionnalités

### Instances & Intents

| Action | Description |
|--------|-------------|
| Créer | Crée un dossier vide sur le disque de ton choix |
| Supprimer | Suppression définitive après confirmation |
| Exporter en .zip | Backup automatique dans `data/backups/` ou dans un dossier personnalisé |
| Importer depuis .zip | Restaure une instance ou un intent depuis une archive |
| Ouvrir l'Explorateur | Ouvre le dossier dans l'Explorateur Windows |
| Ouvrir un terminal | Ouvre un `cmd` positionné directement sur le dossier |

### GitHub *(instances uniquement)*

| Action | Description |
|--------|-------------|
| Lier un repo | Enregistre l'URL du repo GitHub dans la config |
| Git Init | Initialise un dépôt git local dans le dossier |
| Push initial | `add` → `commit` → `remote add` → `push -u origin main` |
| Lier sans pusher | Configure le repo sans déclencher le push |

### Project Builder

Lance l'exécutable **Project Builder** dans un terminal `cmd` avec le dossier de l'instance comme répertoire de travail.

Chemin attendu par défaut :
```
D:\my programme\Project_builder\Project_Builder.exe
```

---

## Désinstallation

Meridian dispose d'un **wizard de désinstallation intégré** accessible depuis la barre de menu :

**`⚠ Désinstaller`** → *Désinstaller Meridian…*

### Étapes du wizard

**1 — Avertissement**
Liste exactement ce qui sera supprimé. Aucune action irréversible à ce stade.

**2 — Backup de tes données** *(facultatif mais recommandé)*
Meridian peut exporter toutes tes instances et intents en `.zip` et déplacer tes backups existants vers un dossier de ton choix avant de se supprimer.

**3 — Confirmation finale**
Résumé complet de ce qui va se passer, puis confirmation.

### Ce qui se passe ensuite

- Meridian se ferme immédiatement
- Un script temporaire dans `%TEMP%` prend le relais
- Il supprime le dossier entier de l'application
- Il se supprime lui-même
- La fenêtre de terminal se ferme toute seule

> ⚠ Les instances et intents sur tes disques secondaires **ne sont pas supprimés** par la désinstallation.
> Seul le dossier de l'application est effacé.

---

## Chemin du Project Builder

Chemin attendu par défaut :
```
D:\my programme\Project_builder\Project_Builder.exe
```

Si ton Project Builder est ailleurs, contacte-moi pour une build personnalisée.
