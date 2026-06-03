# Kit — Opinionated Laravel API Starter

**Période :** 2026  
**Statut :** Actif  
**Type :** API Starter Kit — Backend modulaire

## Stack technique

`Laravel 12` `PHP 8.5` `Sanctum` `SQLite` `Scribe` `OpenAPI` `Saloon` `Stripe` `Spatie Data` `Spatie Permission` `Pest` `PHPStan` `DDEV`

## Problématique

Démarrer un projet Laravel avec une API token-based, c'est toujours la même rengaine : configurer Sanctum, organiser les routes, structurer les contrôleurs, mettre en place la validation, la documentation, les tests… Des heures de boilerplate avant d'écrire la première ligne de business logic.

## Solution

**Kit** est un starter API Laravel opinionated qui fournit tout le socle technique prêt à l'emploi :

### Architecture API

- **Authentification Sanctum** — Tokens personal access, login, register, me
- **Routes versionnées** — `/v1/auth/register`, `/v1/auth/login`, `/v1/auth/me`
- **Contrôleurs invokables** — Un contrôleur = une action (single-responsibility)
- **Form Request + DTO** — Validation + objets de transfert de données
- **JSON:API Resources** — Réponses API normalisées
- **Localisation API** — `Accept-Language` header + `Content-Language` response
- **Sunset middleware** — Dépréciation et retrait progressif des endpoints

### Documentation & Qualité

- **Scribe** — Documentation API automatique par attributs PHP 8
- **OpenAPI** — Génération de contrat OpenAPI pour les clients
- **OpenAPI Contract Tests** — Tests qui vérifient que le runtime correspond à la spec
- **PHPStan** — Analyse statique niveau strict
- **Pest** — Tests unitaires et feature
- **Pint + Rector** — Formatage et refactoring automatique

### Fonctionnalités embarquées

- **Stripe** — Paiements et gestion d'abonnements
- **Saloon** — Client HTTP avec cache, rate limiting et pagination
- **Laravel Excel** — Import/export de fichiers
- **Laravel AI** — Intégration AI
- **Spatie Data** — DTO avec validation et transformation
- **Spatie Permission** — RBAC complet
- **Laravel Phone** — Validation de numéros de téléphone internationaux
- **Sentry** — Monitoring des erreurs
- **Spatie Query Builder** — Filtrage, tri, inclusion de relations

### DevOps

- **DDEV** — Environnement Docker reproductible
- **SQLite-first** — Développement sans dépendance MySQL
- **GitHub Actions** — CI complète + dépendances quotidiennes automatisées
- **Agent configs** — `.cursor`, `.claude`, `.opencode`, `.windsurf`

## Résultats

- ✅ Starter API prêt en 3 commandes (`composer install`, setup script, serve)
- ✅ Documentation générée automatiquement avec Scribe
- ✅ Contrat OpenAPI testé (runtime ↔ spec synchronisés)
- ✅ Architecture invokable propre (single-responsibility controllers)
- ✅ Déploiement DDEV + production-ready
- ✅ Kit complet avec paiements, HTTP client, RBAC, AI

## Lien

[GitHub — kwiktalk-api](https://github.com/STIFLEUR390/kwiktalk-api)