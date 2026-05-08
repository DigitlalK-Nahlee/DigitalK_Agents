# DigitalK Agents — Équipe d'ingénierie autonome

Une équipe d'agents IA orchestrés, importable dans n'importe quel projet.

## Intégration sur un projet existant

```bash
git submodule add https://github.com/<org>/DigitalK_Agents .team
```

Puis configurer `.team/config.md` (chemin Obsidian, git activé, etc.)

## Utilisation

Parler à l'orchestrateur (Claude) en français naturel :
> "Je veux ajouter une fonctionnalité de login par email"

L'orchestrateur analyse, crée le ticket, distribue le travail à l'équipe et te notifie à chaque étape.

## Structure

```
.team/
├── ROLES/          ← instructions système de chaque agent
│   ├── back.md
│   ├── front.md
│   ├── reviewer.md
│   └── tester.md
├── WORKFLOW.md     ← pipeline et règles de boucle
├── OBSIDIAN_RULES.md ← règles de documentation
├── config.md       ← configuration par projet
└── tickets/        ← un fichier par fonctionnalité
    └── TEMPLATE.md
```

## L'équipe

| Rôle | Responsabilité |
|------|---------------|
| Orchestrateur | Reçoit les demandes, distribue, notifie |
| Dev Back | Logique métier, APIs, base de données |
| Dev Front | UI, composants, intégration API |
| Reviewer | Revue de code, validation qualité |
| Testeur | Tests, critères d'acceptance |
