# KwikTalk — Gestion WhatsApp Business

**Période :** 2026  
**Statut :** Actif  
**Type :** Application SaaS — Gestion de contacts WhatsApp

## Stack technique

`Laravel 13` `PHP 8.4+` `Inertia.js v3` `Vue 3` `TypeScript` `Tailwind CSS v4` `shadcn-vue` `Fortify` `Spatie Permission` `Evolution Go API` `DDEV` `Pest` `MySQL/PostgreSQL/SQLite`

## Problématique

Les entreprises qui utilisent WhatsApp Business API ont besoin de gérer efficacement leurs contacts, groupes, campagnes de messages et templates. Les solutions existantes sont soit trop coûteuses, soit trop limitées. L'objectif : construire une plateforme complète de gestion de contacts WhatsApp avec une architecture moderne Laravel 13 + Inertia.js.

## Solution

**KwikTalk** est une application SaaS de gestion de contacts WhatsApp intégrée à l'**API Evolution Go** :

### Fonctionnalités principales

- **📱 WhatsApp Integration** — Synchronisation et gestion des contacts et groupes WhatsApp via l'API Evolution Go
- **👥 Gestion de contacts** — Organisation en groupes, import depuis Excel, recherche avancée
- **💬 Gestion des messages** — Messages entrants/sortants, campagnes, suivi
- **📝 Templates de messages** — Création de templates réutilisables avec variables dynamiques
- **🔒 RBAC** — Contrôle d'accès granulaire via Spatie Laravel Permission
- **💳 Abonnements & facturation** — Plans, abonnements, factures PDF (dompdf)
- **📍 Instances WhatsApp** — Gestion des instances connectées à l'API Evolution Go
- **👤 Espace utilisateur** — Dashboard, profil, wallet, transactions
- **📄 Génération de documents** — Factures, rapports PDF avec Spatie PDF + Browsershot

### Architecture

```
Backend : Laravel 13 + Fortify (auth) + Spatie Permission (RBAC)
Frontend : Vue 3 + TypeScript + shadcn-vue + Tailwind CSS v4
Transport : Inertia.js v3 (SPA sans API)
Dev : DDEV (Docker) + Pest (tests) + Pint (formatting)
```

### Qualité logicielle

- **Pest PHP** — Tests unitaires et feature
- **Laravel Pint** — Formatage de code
- **ESLint + Prettier** — Linting frontend
- **TypeScript strict** — Type safety côté frontend
- **Laravel AI** — Intégration AI pour fonctionnalités intelligentes
- **Sentry** — Monitoring des erreurs en production

## Résultats

- ✅ Application SaaS complète avec Laravel 13 + Inertia.js v3
- ✅ Intégration WhatsApp via Evolution Go API
- ✅ RBAC complet avec Spatie Permission
- ✅ Génération de factures et documents PDF
- ✅ DDEV pour environnement de développement reproductible
- ✅ Architecture moderne avec shadcn-vue et Tailwind v4
- ✅ Documentation complète (installation, architecture, onboarding)

## Lien

[GitHub — kwiktalk-inertiajs](https://github.com/STIFLEUR390/kwiktalk-inertiajs)