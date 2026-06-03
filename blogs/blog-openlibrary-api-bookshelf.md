# Explorer l'API OpenLibrary avec JavaScript et Vue.js

> **Projet lié :** [BookShelf](../PROJET-04-bookshelf.md)

OpenLibrary est une API publique fantastique : elle donne accès à des millions de livres, gratuitement, sans authentification. J'ai voulu construire une application qui l'exploite pleinement — en deux versions.

## L'API OpenLibrary

Pas de clé API, pas de quota limitant a priori. Juste des endpoints REST :

```
Recherche :   https://openlibrary.org/search.json?q=harry+potter
Couvertures : https://covers.openlibrary.org/b/id/{id}-L.jpg
Détails :     https://openlibrary.org/works/{key}.json
```

L'API retourne des résultats paginés avec titre, auteur, année, couverture et identifiants.

## Le concept de BookShelf

Une application **zéro build** : ouvrir `index.html` dans un navigateur et ça marche. Pas de npm install, pas de serveur, pas de build step.

### Version 1 : JavaScript natif

La première version utilise **Vanilla JS** avec :
- Fetch API pour les appels HTTP
- DOM manipulation directe pour l'affichage
- Bootstrap 5 pour le design responsive
- Gestion manuelle de la pagination et des filtres

```javascript
// Concept : requête à OpenLibrary
async function searchBooks(query, page = 1) {
  const response = await fetch(
    `https://openlibrary.org/search.json?q=${query}&page=${page}`
  )
  const data = await response.json()
  return { books: data.docs, total: data.numFound }
}
```

La pagination est dynamique : 20 livres par page, 4 par ligne, avec une navigation complète.

### Version 2 : Vue.js 3 (CDN)

J'ai migré la même logique vers **Vue 3 en CDN** pour comparer :

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

La logique devient plus propre : données réactives, computed properties pour les filtres, templates déclaratifs. Même résultat, mais le code est plus maintenable.

## Gestion des états

Un point important : chaque appel API peut échouer (réseau, limite, erreur). L'application gère :
- **Loading** — spinner pendant la requête
- **Success** — affichage des résultats
- **Error** — message d'erreur clair
- **Empty** — "aucun résultat trouvé"

## Ce que j'ai appris

- **OpenLibrary est une ressource incroyable** pour apprendre à manipuler des API. Gratuite, bien documentée, riche.
- **CDN Vue.js** est parfait pour des prototypes ou des applications légères — pas besoin de Vite/Webpack pour être productif.
- **Deux versions** du même projet (Vanilla JS vs Vue 3) est un excellent exercice pédagogique pour comprendre ce qu'un framework apporte vraiment.

## Pour un portfolio

Ce projet montre :
- La capacité à intégrer une API publique
- La maîtrise du JavaScript asynchrone (async/await, Fetch API)
- La connaissance de Vue.js 3 (même en version CDN)
- L'attention aux détails UX (états loading/error/empty)