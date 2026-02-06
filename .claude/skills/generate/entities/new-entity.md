---
description: "Créer une nouvelle entité (personnage, lieu, faction...)"
argument-hint: '[-c|-r|-l|-f|-o|-cr|-e] "Nom" [--quick]'
allowed-tools: ["Read", "Write", "Glob", "Task"]
---

# /new-entity

Crée une nouvelle entité dans `core/`.

**Skill** : `brain`
**Agent** : `brain-entity-builder`

## Types

| Flag  | Type         | Destination                                |
| ----- | ------------ | ------------------------------------------ |
| `-c`  | character    | `core/characters/[slug].md`                |
| `-r`  | relationship | `core/characters/relationships/[a]-[b].md` |
| `-l`  | location     | `core/world/locations/[slug].md`           |
| `-f`  | faction      | `core/world/factions/[slug].md`            |
| `-o`  | object       | `core/world/objects/[slug].md`             |
| `-cr` | creature     | `core/world/creatures/[slug].md`           |
| `-e`  | event        | `core/world/events/[slug].md`              |

## Options

| Option    | Description                             |
| --------- | --------------------------------------- |
| `--quick` | Crée le fichier vide sans brainstorming |

## Settings (à consulter)

```
packages/settings/naming-conventions.md   # Noms de fichiers ([lastname]-[firstname].md)
```

## Process

1. **Résoudre** : nom → slug → chemin (selon naming-conventions.md)
2. **Vérifier** : n'existe pas déjà
3. **Template** : lire `packages/templates/entities/[type].md`
4. **Contexte** : `core/world/universe.md`, entités existantes
5. **Mode brainstorm** (par défaut) :
   - Questions une par une
   - Challenge des réponses plates
   - Proposition de connexions
6. **Mode --quick** :
   - Remplace `[Nom]` dans le template
   - Écrit directement
7. **Créer** : le fichier avec le contenu généré
8. **Connexions** : proposer de créer les relations suggérées

## Exemples

```bash
/new-entity -c "Mel D'Almeris"      # Nouveau personnage (brainstorm)
/new-entity -r "Mel" "Kira"          # Nouvelle relation
/new-entity -l "Tour Noire" --quick  # Lieu sans brainstorm
```
