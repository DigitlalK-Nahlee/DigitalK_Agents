# Workflow de l'équipe

## Pipeline standard

```
[Orchestrateur] Reçoit la demande → crée le ticket
      │
      ▼
[Dev Back]     Implémente la logique métier + API
      │
      ▼
[Dev Front]    Implémente l'UI (si applicable)
      │
      ▼
[Reviewer]     Relit tout le code produit
      │
   ❌ REJET ──► [Dev concerné] Corrige → retour au Reviewer
      │
   ✅ OK
      │
      ▼
[Testeur]      Écrit et exécute les tests
      │
   ❌ ÉCHEC ──► [Dev concerné] Corrige → retour au Reviewer
      │
   ✅ OK
      │
      ▼
[Orchestrateur] Compte-rendu final au dirigeant
```

## Règles globales

- **Ticket vivant** : chaque agent lit ET écrit dans le fichier ticket actif (voir "Emplacement des tickets" ci-dessous)
- **Pas de communication directe** entre agents — tout passe par le ticket
- **Limite de boucle** : max 3 itérations par agent. Au-delà → escalade orchestrateur → dirigeant
- **Git** : chaque agent commite son travail. L'orchestrateur ne commite pas.

## Emplacement des tickets

> ⚠️ `.team/tickets/` contient uniquement `TEMPLATE.md` — c'est un modèle, pas une destination.  
> **Ne jamais créer un ticket dans `.team/tickets/`**, sauf si `OBSIDIAN_VAULT_PATH` est vide.

Lire `OBSIDIAN_VAULT_PATH` dans `.team/config.md` AVANT de créer le ticket :

### Avec vault Obsidian (`OBSIDIAN_VAULT_PATH` renseigné)
- Créer le ticket dans `<OBSIDIAN_VAULT_PATH>/Tickets/<ID>-<TitreEnPascalCase>.md`
- Utiliser `TEMPLATE.md` comme modèle uniquement — ne pas le modifier, ne pas le déplacer
- Respecter les règles de `.team/OBSIDIAN_RULES.md` (wikilinks, max 20 lignes par note, log)
- Le ticket principal peut dépasser 20 lignes — mais chaque décision technique = note atomique liée

### Sans vault Obsidian (`OBSIDIAN_VAULT_PATH` vide)
- Créer le ticket dans `.team/tickets/<ID>-<titre-en-kebab-case>.md`
- Utiliser `TEMPLATE.md` comme modèle uniquement — ne pas le modifier, ne pas le déplacer

## Décision : quels agents lancer

L'orchestrateur analyse la demande AVANT de spawner quoi que ce soit et décide les agents nécessaires. Règle : **ne lancer que ce qui est utile**.

| Type de demande | Agents à lancer |
|----------------|-----------------|
| Question, conseil, analyse, explication | Aucun — l'orchestrateur répond directement |
| Correction de bug simple (1 fichier, 1 endroit) | Dev concerné (back ou front) + Reviewer |
| Fonctionnalité purement backend | Dev Back → Reviewer → Testeur |
| Fonctionnalité purement frontend | Dev Front → Reviewer → Testeur |
| Fonctionnalité fullstack | Dev Back → Dev Front → Reviewer → Testeur |
| Refactoring / renommage | Dev concerné + Reviewer (pas de testeur si pas de logique modifiée) |
| Ajout de tests uniquement | Testeur seul |
| Revue de code à la demande | Reviewer seul |

**En cas de doute**, l'orchestrateur précise au dirigeant les agents qu'il compte lancer et pourquoi, avant de les spawner.

### Cas du Testeur
Vérifier dans `config.md` si un framework de test est configuré (`TEST_FRAMEWORK`).  
- Si vide ou absent → **zapper le Testeur**, le mentionner dans le compte-rendu final
- Si renseigné → spawner le Testeur normalement

## Cas particuliers

### Blocage technique
Si un agent ne peut pas avancer (spec ambiguë, dépendance manquante), il écrit dans `## Blocages` du ticket et l'orchestrateur escalade immédiatement au dirigeant.

### Projet sans git
Les agents produisent quand même le code. L'étape commit est sautée.

## Notifications orchestrateur → dirigeant
- "Dev Back terminé — en attente de review"
- "Dev Front terminé — en attente de review"  
- "Review : corrections demandées à [Back/Front] — itération N"
- "Review approuvée — tests en cours"
- "Tests : échec — corrections demandées à [Back/Front] — itération N"
- "✅ Fonctionnalité validée et livrée"
- "⚠️ Escalade : [description du blocage]"
