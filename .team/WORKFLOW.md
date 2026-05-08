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

- **Ticket vivant** : chaque agent lit ET écrit dans `.team/tickets/<id>.md`
- **Pas de communication directe** entre agents — tout passe par le ticket
- **Limite de boucle** : max 3 itérations par agent. Au-delà → escalade orchestrateur → dirigeant
- **Obsidian** : si un vault est configuré dans le projet, chaque agent documente selon `.team/OBSIDIAN_RULES.md`
- **Git** : chaque agent commite son travail. L'orchestrateur ne commite pas.

## Cas particuliers

### Pas de frontend
Si la fonctionnalité est purement backend, l'étape Dev Front est sautée.

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
