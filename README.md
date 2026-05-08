# DigitalK Agents — Équipe d'ingénierie autonome

Une équipe d'agents IA orchestrés, importable dans n'importe quel projet via git submodule.

---

## Intégration sur un projet existant

### 1. Ajouter l'équipe comme submodule

```bash
git submodule add https://github.com/DigitlalK-Nahlee/DigitalK_Agents .team
git submodule update --init
```

### 2. Configurer `.team/config.md`

Ouvrir `.team/config.md` et renseigner les valeurs selon le projet :

```
OBSIDIAN_VAULT_PATH=   ← chemin absolu vers le vault Obsidian (laisser vide si aucun)
GIT_ENABLED=true       ← false si le projet n'a pas de git
LANG=fr
MAX_ITERATIONS=3       ← nb max de corrections avant escalade au dirigeant
```

Exemple avec vault :
```
OBSIDIAN_VAULT_PATH=D:\Perso\MonProjet\docs
GIT_ENABLED=true
LANG=fr
MAX_ITERATIONS=3
```

### 3. Intégrer `CLAUDE.md` à la racine du projet

Claude lit automatiquement `CLAUDE.md` au démarrage — c'est ce qui lui explique son rôle d'orchestrateur. **Ne pas écraser un `CLAUDE.md` existant.**

**Si le projet n'a pas encore de `CLAUDE.md` :**
```bash
cp .team/CLAUDE.md ./CLAUDE.md
```

**Si le projet a déjà un `CLAUDE.md` :**  
Ajouter manuellement le contenu de `.team/CLAUDE.md` à la fin du `CLAUDE.md` existant du projet. Les deux contenus doivent coexister.

### 4. Ouvrir Claude Code à la racine du projet

```bash
cd MonProjet
claude
```

Claude lit `CLAUDE.md` au démarrage et est immédiatement opérationnel comme orchestrateur.

---

## Utilisation au quotidien

Parler à l'orchestrateur en français naturel :

> "Je veux ajouter une fonctionnalité de login par email"

L'orchestrateur :
1. Analyse la demande et crée un ticket dans `.team/tickets/`
2. Distribue les tâches à chaque agent dans l'ordre
3. Notifie à chaque étape clé
4. Gère les boucles de correction automatiquement
5. Rend compte du résultat final

---

## Fichiers à connaître

| Fichier | Rôle | À modifier ? |
|---------|------|--------------|
| `.team/config.md` | Configuration par projet | **Oui** — à chaque nouveau projet |
| `.team/ROLES/back.md` | Instructions du Dev Back | Optionnel — pour adapter au stack |
| `.team/ROLES/front.md` | Instructions du Dev Front | Optionnel — pour adapter au stack |
| `.team/ROLES/reviewer.md` | Instructions du Reviewer | Rarement |
| `.team/ROLES/tester.md` | Instructions du Testeur | Optionnel — pour adapter au framework de test |
| `.team/OBSIDIAN_RULES.md` | Règles de documentation Obsidian | Si tes règles Obsidian changent |
| `.team/WORKFLOW.md` | Pipeline et règles de boucle | Rarement |
| `.team/tickets/TEMPLATE.md` | Template de ticket | Rarement |
| `.team/tickets/` | Tickets générés (un par fonctionnalité) | Ne pas modifier manuellement |

---

## Adapter les rôles à ton stack (optionnel)

Si ton projet utilise un stack spécifique, préciser dans les fichiers de rôles.

Exemple dans `.team/ROLES/back.md`, ajouter en tête :
```
## Stack du projet
- Langage : TypeScript / Node.js
- Framework : NestJS
- Base de données : PostgreSQL avec Prisma
```

Exemple dans `.team/ROLES/front.md` :
```
## Stack du projet
- Framework : React Native
- State management : Zustand
- Navigation : Expo Router
```

---

## Mettre à jour l'équipe

```bash
cd .team
git pull origin master
cd ..
git add .team
git commit -m "chore: mise à jour de l'équipe agents"
```

---

## Structure complète

```
.team/
├── config.md             ← configuration par projet (à remplir)
├── WORKFLOW.md           ← pipeline et règles de boucle
├── OBSIDIAN_RULES.md     ← règles de documentation Obsidian
├── ROLES/
│   ├── back.md           ← instructions Dev Back
│   ├── front.md          ← instructions Dev Front
│   ├── reviewer.md       ← instructions Reviewer
│   └── tester.md         ← instructions Testeur
└── tickets/
    ├── TEMPLATE.md       ← template de ticket
    └── <id>-<titre>.md   ← tickets générés automatiquement
```

---

## L'équipe

| Rôle | Responsabilité |
|------|----------------|
| **Orchestrateur** (toi, Claude) | Reçoit les demandes, distribue, notifie |
| **Dev Back** | Logique métier, APIs, base de données |
| **Dev Front** | UI, composants, intégration API |
| **Reviewer** | Revue de code, validation qualité |
| **Testeur** | Tests, critères d'acceptance |
