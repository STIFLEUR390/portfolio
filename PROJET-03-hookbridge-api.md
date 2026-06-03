# HookBridge API

**Période :** 2025  
**Statut :** Terminé  
**Type :** API REST — Gestion de webhooks

## Stack technique

`Laravel` `PHP 8.3` `MySQL` `REST API` `Eloquent` `API Resources` `Repository Pattern`

## Problématique

Les systèmes modernes échangent via des webhooks et callbacks. Gérer manuellement les inscriptions aux webhooks, les configurations de callback et l'historique des événements devient rapidement complexe sans une API dédiée.

## Solution

Une API Laravel complète pour centraliser la gestion des projets et leurs configurations pour le service **HookBridge** :

- **Gestion de projets** — CRUD complet pour organiser les endpoints
- **Configuration de webhooks** — définition des URLs, événements déclencheurs, payloads
- **Gestion des callbacks** — configuration et suivi des retours
- **Architecture métier** — Repository Pattern, Services, Policies, Traits
- **API versionnée** — routes API v1 avec ressources RESTful

## Détails d'architecture

- **Repository Pattern** pour la persistance des données
- **Policies** pour la sécurisation des accès
- **Services** dédiés pour la logique métier
- **API Resources** pour la transformation des réponses
- **Jobs & Notifications** pour le traitement asynchrone
- **Traits** pour la réutilisation de comportements communs

## Résultats

- ✅ API REST complète et versionnée
- ✅ Architecture Laravel professionnelle (Repository, Service, Policy)
- ✅ Gestion centralisée des configurations de webhooks
- ✅ Code modulaire, réutilisable et testable

## Lien

[GitHub — hookbridge-api](https://github.com/STIFLEUR390/hookbridge-api)