# TCF Canada Suite

**Période :** 2024 – 2026  
**Statut :** Actif  
**Type :** Application web

## Stack technique

`AdonisJS 7` `TypeScript` `Vue 3` `Edge Templates` `SQLite` `Session Auth` `Web Scraping`

## Problématique

Les candidats au **TCF Canada** (Test de Connaissance du Français pour le Canada) ont besoin de s'entraîner sur des sujets récents d'expression écrite et orale. Les sujets sont publiés sur divers sites web sans structure centralisée, rendant leur recherche et leur archivage laborieux.

## Solution

Une suite d'applications web qui centralise, archive et structure les sujets d'examen :

- **TCF Subjects** (2026) — Application AdonisJS 7 avec scraping intelligent : l'utilisateur colle une URL de sujet, et l'application détecte automatiquement le type d'épreuve (expression écrite/orale), extrait le contenu et l'archive dans une base SQLite avec session auth.
- **ToolTCF** (2024) — Outil Vue 3 pour la préparation aux épreuves du TCF Canada
- **TCF Canada Docs** (2024) — Documentation complète de la plateforme avec Docus

## Résultats

- ✅ Scraping automatisé et classification intelligente des sujets
- ✅ Interface simple : collage d'URL → archivage instantané
- ✅ Authentification par session pour les utilisateurs
- ✅ Base de données évolutive de sujets réels

## Lien

[GitHub — tcf-subjects](https://github.com/STIFLEUR390/tcf-subjects)  
[GitHub — tooltcf](https://github.com/STIFLEUR390/tooltcf)  
[GitHub — tcfcanada-docs](https://github.com/STIFLEUR390/tcfcanada-docs)