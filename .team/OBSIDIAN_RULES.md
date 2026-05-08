# Règles Obsidian pour les agents

## Structure du vault
Le chemin racine du vault est défini dans `.team/config.md` (à créer lors de l'intégration sur un projet).
Si aucun vault n'est configuré, ignorer toute la documentation Obsidian.

## Philosophie
- 1 fichier = 1 idée / décision / concept
- Taille max : 20 lignes
- Pas de hiérarchie forte — structure plate
- Les liens `[[wikilinks]]` = source de vérité
- Une note sans lien = INTERDIT

## Stratégie d'écriture
- Langue : FR
- Nommage : PascalCase explicite (ex: `AuthTokenStrategy`, `UserProfileAPI`)
- ATOMIQUE : 1 note = 1 idée
- INCRÉMENTAL : append `>>` ou patch (jamais de réécriture complète)
- Toujours vérifier si la note existe avant d'en créer une nouvelle

## Template obligatoire
```markdown
# [[NomDuNode]]

## Decision
<la décision ou le concept>

## Why
<pourquoi cette approche>

## Watchpoints
- <point de vigilance>

## Links
- [[Parent]]
```

## Règles de liens
- Toujours lier à au moins 1 nœud existant
- Si aucun nœud pertinent n'existe : créer un stub parent générique (ex: `[[API]]`, `[[Auth]]`, `[[Infra]]`)
- Domaines principaux : `[[Auth]]` `[[API]]` `[[Frontend]]` `[[Infra]]`

## Log
Chaque écriture doit être loggée dans `log.md` au format :
`YYYY-MM-DD | [[NomDuNode]] | résumé en 1 ligne`

## Gouvernance
- Si une décision change : marquer OBSOLETE en tête de note, ne jamais supprimer
- Jamais afficher le contenu complet d'une note — afficher uniquement : `✅ Memory Updated: [[NomDuNode]] (+X links)`
