# Du premier commit au déploiement : itérations sur mon portfolio Nuxt

> **Projet lié :** [Portfolio Website](../PROJET-08-portfolio-website.md)

Un portfolio n'est jamais vraiment "fini". Le mien a connu **trois versions majeures**, chacune apportant son lot d'apprentissages. Voici l'histoire.

## Version 1 : Nuxt 3 minimal (Juin 2025)

La première version était… basique. Un starter Nuxt 3, un layout, quelques pages statiques. Ça faisait le job, mais :

- **Pas de recherche** — le visiteur devait tout parcourir
- **Pas de contenu dynamique** — chaque ajout nécessitait une modification du code
- **Design générique** — le starter Nuxt ne se démarquait pas

**Leçon :** Un portfolio doit montrer ce qu'on sait faire, pas juste exister.

## Version 2 : Portfolio MeiliSearch (Juillet 2025)

J'ai décidé d'ajouter un moteur de recherche full-text. **MeiliSearch** s'est imposé comme la solution évidente :

- Un service Docker, une clé API, et c'est parti
- Indexation des projets (titre, description, technologies, année)
- Recherche typo-tolérante en temps réel depuis le frontend

L'ajout de Docker a aussi structuré le déploiement :

```yaml
services:
  nuxt:
    build: .
    ports:
      - "3000:3000"
  meilisearch:
    image: getmeili/meilisearch:v1.0
    ports:
      - "7700:7700"
```

**Leçon :** Ajouter une fonctionnalité technique concrète (recherche full-text, Docker) valorise plus qu'un design parfait.

## Version 3 : Portfolio Frontend (Juillet 2025)

La version la plus aboutie : architecture Vue 3 propre, composants modulaires, thème personnalisé. J'ai repris tout depuis zéro en appliquant les leçons des versions précédentes :

- **Architecture claire** — layouts, composants, pages bien séparés
- **Contenu dynamique** — les projets sont des données, pas du HTML statique
- **Design cohérent** — palette, typographie, espacements réfléchis
- **Responsive** — adapté desktop et mobile

## Le tableau d'évolution

| Version | Date | Stack | Taille (CSS) | Recherche | Docker |
|---------|------|-------|-------------|-----------|--------|
| Nuxt | 06/2025 | Nuxt 3 + Vue 3 | ~755KB | ❌ | ❌ |
| MeiliSearch | 07/2025 | Nuxt 3 + MeiliSearch | ~664KB | ✅ | ✅ |
| Frontend | 07/2025 | Nuxt 3 + Vue 3 refiné | ~670KB | ✅ | ✅ |

(La taille CSS vient des assets Tailwind build — pas de panique, c'est compressé au serveur.)

## Ce que je retiens

1. **Itérer est plus important que perfectionner.** Chaque version m'a appris quelque chose que je n'aurais pas découvert en réfléchissant.
2. **Les fonctionnalités techniques parlent.** Un moteur de recherche ou Docker dans un portfolio démontre des compétences concrètes.
3. **Ne pas hésiter à tout réécrire.** La V3 était bien meilleure parce que je savais exactement ce que je voulais, après avoir fait les erreurs en V1 et V2.

Mon conseil : publiez votre V1 rapidement, même imparfaite. Les retours (les vôtres et ceux des autres) guideront la V2 bien mieux que la réflexion abstraite.