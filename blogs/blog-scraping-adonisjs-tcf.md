# Web Scraping avec AdonisJS : archiver les sujets du TCF Canada

> **Projet lié :** [TCF Canada Suite](../PROJET-01-tcf-canada-suite.md)

Le TCF Canada publie régulièrement des sujets d'expression écrite et orale sur divers sites. Les candidats passent un temps fou à chercher ces sujets manuellement. J'ai voulu créer un outil qui automatise cette collecte.

## Le problème

Les sujets sont publiés sur des pages web avec des structures très différentes selon la source. Chaque URL peut pointer vers :
- Un sujet d'expression écrite
- Un sujet d'expression orale
- Une page d'index listant plusieurs sujets

Je voulais que l'utilisateur n'ait qu'à **coller une URL** pour que l'application détecte automatiquement le type de sujet et l'archive.

## Pourquoi AdonisJS ?

J'ai choisi AdonisJS 7 pour plusieurs raisons :
- **Edge templates** — rendu serveur simple sans nécessiter de SPA
- **Session Auth** intégrée, parfaite pour une application à utilisateurs
- **SQLite** en base — zéro configuration, le fichier suit le projet
- **CLI intégré** — génération rapide de contrôleurs, migrations, etc.

## L'approche scraping

Le cœur du projet repose sur une logique de **détection intelligente** :

```javascript
// Concept : analyser l'URL et le contenu pour déterminer le type
function detectSubjectType(url, htmlContent) {
  if (url.includes('expression-orale')) return 'oral'
  if (url.includes('expression-ecrite')) return 'written'
  // fallback : analyse du contenu HTML
  if (htmlContent.includes('expression orale')) return 'oral'
  return 'unknown'
}
```

L'utilisateur entre une URL, l'application scrape le contenu, détecte le type et l'archive automatiquement avec la date et la source.

## Ce que j'en retiens

- Le **scraping** est un processus délicat : les sites changent, les sélecteurs cassent. Une approche par patterns plutôt que par sélecteurs CSS stricts est plus robuste.
- **AdonisJS** est excellent pour des apps CRUD + scraping : pas de lourdeur, tout est dans le framework.
- L'**archivage structuré** de données non structurées (pages web) est un problème fascinant, surtout quand chaque source a son propre format.

## Leçon pour un portfolio

Ce projet montre ma capacité à :
- Analyser un besoin utilisateur concret
- Choisir la bonne stack (AdonisJS plutôt que Laravel ici pour sa légèreté)
- Implémenter du web scraping fiable
- Livrer une application fonctionnelle avec auth intégrée