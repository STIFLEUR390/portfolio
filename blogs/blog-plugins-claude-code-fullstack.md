# Construire 7 plugins Claude Code pour le développement fullstack

> **Projet lié :** [Fullstack Dev Skills](../PROJET-06-fullstack-dev-skills.md)

Claude Code est un assistant AI puissant, mais sa véritable force réside dans sa capacité à être **enrichi par des plugins** (skills). Après des mois à l'utiliser au quotidien pour du développement fullstack, j'ai remarqué un pattern : je répétais toujours les mêmes instructions.

## L'idée

Et si je transformais mes configurations récurrentes en **plugins réutilisables** ? Chaque plugin regrouperait des skills spécialisés par domaine, avec des instructions précises, des contraintes et des bonnes pratiques.

## Les 7 plugins

| Plugin | Pourquoi ? | Contenu |
|--------|-----------|---------|
| **Frontend** | Nuxt 4, Vue 3, Tailwind — des conventions UI précises | Composants, accessibilité, shadcn-vue |
| **Backend** | Laravel 12+, PHP 8.3 — beaucoup de boilerplate | API REST, GraphQL, Redis, Eloquent |
| **Cross-Platform** | NativePHP et Tauri — deux mondes différents | Desktop Rust, mobile PHP |
| **Database** | Schémas, indexes, optimisation | MySQL, PostgreSQL, migrations |
| **Design** | Cohérence visuelle entre projets | Design tokens, systèmes de composants |
| **DevOps** | Docker, CI/CD — infrastructure reproductible | GitHub Actions, Docker Compose |
| **Practices** | Git, tests, sécurité — la qualité | TDD, OWASP, code review, debug |

## Comment ça marche ?

Chaque plugin contient des **skills** (fichiers de configuration) qui définissent comment Claude Code doit se comporter pour une tâche donnée :

```
skills/
  frontend/
    nuxt-ui.skill.md       # Créer des composants Nuxt UI
    vue3-composition.skill.md  # Utiliser la Composition API
    shadcn-vue.skill.md    # Intégrer shadcn-vue accessible
```

Un skill, c'est un fichier markdown avec :
- Un **déclencheur** (quand ce skill est pertinent)
- Des **instructions précises** (pas de place à l'interprétation)
- Des **contraintes** (versions, conventions de nommage)
- Des **exemples** (code à suivre)

## La vente en marketplace

Les plugins sont disponibles sur la **Marketplace Claude Code** :

```bash
/plugin marketplace add STIFLEUR390/fullstack-dev-skills
/plugin install frontend@fullstack-dev-skills
```

Une commande, et Claude Code sait exactement comment coder du Laravel 12 ou du Nuxt 4.

## Leçons

- **La réutilisabilité paie** — J'estime gagner ~30% de temps sur chaque projet depuis que j'utilise ces plugins.
- **Documenter pour les autres** m'a forcé à clarifier mes propres pratiques.
- Un bon plugin ne dit pas "quoi faire" mais **"comment le faire ici"** — le contexte du projet compte.

Si vous utilisez Claude Code, créez ne serait-ce qu'un plugin pour votre stack principale. Vous serez surpris de la différence.