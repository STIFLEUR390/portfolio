# TCF Canada Suite

**Période :** 2023 – 2026  
**Statut :** Actif  
**Type :** Plateforme SaaS — Préparation au TCF Canada

## Stack technique

`Laravel 10` `PHP 8.2` `Livewire 3` `Filament 3` `MySQL` `Redis` `Vue 3` `AdonisJS 7` `TypeScript` `Stripe` `NotchPay` `Flutterwave` `Pest`

## Problématique

Les candidats au **TCF Canada** (Test de Connaissance du Français pour le Canada) ont besoin d'une plateforme centralisée pour se préparer aux 4 compétences de l'examen (CE, CO, EE, EO). Pas de solution SaaS complète existante avec quiz chronométrés, abonnements, corrections et suivi des progrès. En parallèle, les sujets récents d'examen sont dispersés sur plusieurs sites sans archivage centralisé.

## Solutions

Deux applications complémentaires :

### 🏗️ tool-tcf-canada — Plateforme SaaS (2023–2026)

Plateforme complète de préparation au TCF Canada avec :

- **Quiz interactifs chronométrés** — 4 compétences TCF (CE, CO, EE, EO)
- **Tests de compréhension** écrite et orale avec QCM
- **Expression écrite et orale** avec soumission, correction et feedback
- **Système d'abonnement** multi-passerelles de paiement (Stripe, NotchPay, Flutterwave)
- **Codes promo** et réductions
- **Tableau de bord** utilisateur avec statistiques et suivi des progrès
- **Interface administrateur** avec Filament 3 (gestion des utilisateurs, quiz, paiements)
- **Paiements et factures** — historique, remboursements, expiration d'abonnement
- **Tests automatisés** avec Pest PHP

### 🕷️ TCF Subjects (2026)

Application AdonisJS 7 de **scraping intelligent** : l'utilisateur colle une URL de sujet, l'application détecte automatiquement le type d'épreuve, extrait le contenu et l'archive.

### 📚 Projets associés

- **ToolTCF** (2024) — Outil Vue 3 de préparation
- **TCF Canada Docs** (2024) — Documentation avec Docus

## Résultats

- ✅ Plateforme SaaS complète avec abonnements et multi-paiements
- ✅ Quiz interactifs pour les 4 compétences du TCF Canada
- ✅ Panel admin Filament 3 pour la gestion complète
- ✅ Tests Pest automatisés (unit + feature)
- ✅ Scraping et archivage automatisé des sujets d'examen
- ✅ Déploiement avec DDEV local + production

## Détails techniques

**Architecture :**
- Service Layer + Actions Pattern (Laravel)
- Livewire 3 pour les interactions temps réel (sans SPA)
- Filament 3 pour le panel admin complet
- Multi-passerelles de paiement avec abstraction
- Cache Redis pour les performances
- Notifications email et in-app

**Qualité :**
- Pest PHP pour les tests
- PHPStan analyse statique
- Laravel Pint pour le formatage
- Claude Code intégré dans le workflow

## Lien

[GitHub — tool-tcf-canada](https://github.com/STIFLEUR390/tool-tcf-canada)  
[GitHub — tcf-subjects](https://github.com/STIFLEUR390/tcf-subjects)  
[GitHub — tooltcf](https://github.com/STIFLEUR390/tooltcf)  
[GitHub — tcfcanada-docs](https://github.com/STIFLEUR390/tcfcanada-docs)