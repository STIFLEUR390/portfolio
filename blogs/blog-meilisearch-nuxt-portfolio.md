# Ajouter MeiliSearch à un portfolio Nuxt pour une recherche full-text instantanée

> **Projet lié :** [Portfolio Website](../PROJET-08-portfolio-website.md)

Un portfolio, c'est bien. Un portfolio où on trouve instantanément ce qu'on cherche, c'est mieux. J'ai intégré **MeiliSearch** dans mon site Nuxt pour offrir une recherche full-text ultra-rapide.

## Pourquoi MeiliSearch ?

J'aurais pu utiliser Algolia (payant), Elasticsearch (lourd) ou une simple recherche côté client (limitée). MeiliSearch coche toutes les cases :
- **Open source** — pas de dépendance à un service payant
- **Rapide** — temps de réponse < 50ms
- **Typo-tolerant** — "portflio" trouve "portfolio"
- **Léger** — un binaire Rust, pas de JVM
- **Docker-ready** — un service dans mon docker-compose

## L'architecture

```
[Nuxt App] ← requête AJAX → [MeiliSearch API] ← index → [Base de données]
```

Les données des projets sont indexées dans MeiliSearch au build ou à chaque mise à jour. La recherche côté client envoie une requête directe à MeiliSearch via son API REST.

## Indexation des projets

```javascript
// Concept : structurer les données pour la recherche
const projectIndex = {
  id: 'tcf-canada',
  title: 'TCF Canada Suite',
  tags: ['AdonisJS', 'TypeScript', 'Vue', 'scraping'],
  description: 'Application de scraping et d\'archivage...',
  technologies: ['AdonisJS 7', 'TypeScript', 'SQLite'],
  year: 2026
}
```

MeiliSearch accepte la recherche sur tous les champs avec des poids différents (le titre plus important que la description).

## Dockerisation

```yaml
services:
  meilisearch:
    image: getmeili/meilisearch:v1.0
    ports:
      - "7700:7700"
    volumes:
      - ./meili_data:/meili_data
    environment:
      MEILI_MASTER_KEY: ${MEILI_KEY}
```

Un service Docker, un volume persistant, une clé API — prêt en 5 minutes.

## Résultats

- Recherche **instantanée** dans tous les projets
- **Typo-tolérante** — utile pour les visiteurs qui ne connaissent pas l'orthographe exacte
- **Filtrable par technologie, année, type de projet**
- Zéro dépendance externe (pas d'appel API payant)

## Ce que j'ai appris

- **MeiliSearch est incroyablement simple** à mettre en place comparé à Elasticsearch. La documentation est claire, l'API est propre.
- La recherche full-text est un **élément différenciant** pour un portfolio — ça montre de l'attention au détail.
- Docker rend le déploiement trivial : `docker compose up` et c'est prêt.

Si vous avez un site avec du contenu textuel, ajoutez MeiliSearch. C'est le meilleur rapport simplicité/valeur ajoutée que j'ai trouvé.