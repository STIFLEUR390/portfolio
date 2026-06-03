# BookShelf

**Période :** 2025  
**Statut :** Terminé  
**Type :** Application web — Exploration de livres

## Stack technique

`HTML5` `CSS3` `Bootstrap 5` `JavaScript` `Vue 3 (CDN)` `OpenLibrary API`

## Problématique

Explorer des livres via l'API publique **OpenLibrary** peut être fastidieux sans une interface dédiée. L'objectif était de créer une application légère, sans build, utilisable immédiatement dans le navigateur.

## Solution

Application web 100% frontend qui interroge l'API OpenLibrary pour rechercher et explorer des livres :

- **Recherche par mot-clé** — titre, auteur, sujet
- **Filtres** — par genre (type) et année (1970–2025)
- **Grille de résultats** — 4 livres par ligne, 20 par page
- **Pagination dynamique** — navigation complète entre les pages
- **Couvertures** — affichage automatique via l'API Covers avec fallback
- **Deux versions** — JavaScript natif + Vue.js 3 (CDN) pour démonstration pédagogique
- **Interface responsive** — Bootstrap 5

## Résultats

- ✅ Application 0 build : ouvrir `index.html` et ça marche
- ✅ Gestion des états : chargement, erreur, données vides
- ✅ Pagination complète avec navigation
- ✅ Image par défaut si couverture non disponible
- ✅ Version pédagogique montrant la migration Vanilla JS → Vue 3

## Lien

[GitHub — book-shelf](https://github.com/STIFLEUR390/book-shelf)