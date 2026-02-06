---
description: "Créer une nouvelle saga ou un volume"
argument-hint: "[saga \"Nom\" | volume \"Titre\"]"
allowed-tools: ["Read", "Write", "Bash", "Glob", "AskUserQuestion"]
---

# /new-story

Crée une nouvelle saga ou ajoute un volume.

## Usage

```bash
/new-story saga "Nom"         # Crée une nouvelle saga
/new-story volume "Titre"       # Ajoute un volume à la saga active
```

## Settings (à consulter)

```
packages/settings/naming-conventions.md   # Slugification, format volume-N-[titre]
```

## Process : saga

1. **Résoudre** : nom → slug (selon naming-conventions.md)
2. **Vérifier** : n'existe pas
3. **Demander** : titre du premier volume
4. **Créer l'arborescence** :
```
apps/[saga]/
├── context/
│   ├── saga.md
│   ├── characters/
│   └── arcs/
├── .logbook/               # Vide, sera peuplé par /validate
├── volume-1-[titre]/
│   └── chapters/
└── playground/
    └── .scripts/
```
5. **Initialiser** : saga.md
6. **Confirmer** : prêt à écrire avec `/write`

## Process : volume

1. **Détecter** : saga active
2. **Calculer** : prochain numéro (volume-N+1)
3. **Résoudre** : titre → slug
4. **Créer** : `apps/[saga]/volume-[N]-[titre]/chapters/`
5. **Mettre à jour** : saga.md
6. **Confirmer** : volume créé

## Fichiers générés

### context/saga.md
```yaml
---
name: "[Nom]"
created: "[date]"
---

# [Nom]

## Thèmes
- [à définir]

## Arc principal
[à définir]

## Volumes

### Volume 1 — [Titre]
- **Dossier** : `volume-1-[slug]`
- **Statut** : Non commencé
```

### .logbook/

Dossier vide à la création. Sera peuplé automatiquement par `/validate` avec des fichiers individuels :
```
.logbook/
├── 001-v1-c01.md   # Créé par /validate du chapitre 1
├── 002-v1-c02.md   # Créé par /validate du chapitre 2
└── ...
```
