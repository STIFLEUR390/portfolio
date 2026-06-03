# Laravel 13 + Inertia.js v3 : pourquoi j'ai choisi cette stack pour KwikTalk

> **Projet lié :** [KwikTalk](../PROJET-15-kwiktalk.md)

KwikTalk est une application SaaS de gestion de contacts WhatsApp. Pour ce projet, j'ai choisi une stack que je n'avais encore jamais utilisée en production : **Laravel 13 + Inertia.js v3**. Voici pourquoi.

## Le dilemme : SPA ou server-side ?

J'avais deux options classiques :

1. **SPA complète** (Vue 3 + Laravel API) — plein de flexibilité, mais double codebase, gestion de tokens CORS, complexité
2. **Livewire** — simple, server-side, mais pas une vraie SPA, moins fluide pour des interfaces complexes

Inertia.js est le **pont** entre les deux : on écrit des composants Vue 3, mais ils sont rendus côté serveur. Pas d'API à construire, pas de CORS, pas de double validation.

## Comment Inertia.js change la donne

### Route unique, composants multiples

Au lieu d'avoir une API Laravel ET un router Vue, tout part de Laravel :

```php
// Laravel : une route, un contrôleur, un composant Inertia
Route::inertia('/contacts', 'Contacts/Index')
  ->name('contacts.index')
  ->middleware('auth');
```

```vue
<!-- Vue 3 : un composant qui reçoit ses props du serveur -->
<script setup lang="ts">
defineProps<{
  contacts: PaginatedData<Contact>
  groups: Group[]
}>()
</script>
```

Plus de double routage. Plus de duplication de validation. Les props sont typées (TypeScript strict) et viennent directement du backend.

### Avantages concrets pour KwikTalk

KwikTalk a des interfaces complexes : gestion de contacts, campagnes de messages, templates, facturation. Inertia.js permet :

- **État partagé** — les données viennent du serveur, pas besoin de synchroniser un store Pinia avec une API
- **Navigation instantanée** — Inertia interpole les pages sans rechargement complet
- **Formulaires progressifs** — validation Laravel côté serveur + feedback visuel Vue 3
- **Pas de CORS** — tout est sur le même domaine

## shadcn-vue + Tailwind v4

Le frontend utilise **shadcn-vue** (port de shadcn/ui pour Vue), ce qui donne :
- Des composants accessibles et stylés prêts à l'emploi
- Une personnalisation totale via Tailwind
- Une cohérence visuelle sans réinventer chaque bouton

## RBAC avec Spatie Permission

Les permissions sont déclarées côté Laravel, exposées à Inertia, et utilisées dans les templates Vue :

```php
// Laravel : middleware de permission
Route::middleware('can:view-contacts')->group(function () {
    Route::inertia('/contacts', ...);
});
```

```vue
<!-- Vue 3 : affichage conditionnel -->
<Button v-if="can('delete-contacts')" variant="destructive">
  Supprimer
</Button>
```

## Ce que j'ai appris

- **Inertia.js est le meilleur des deux mondes** — la puissance de Vue 3 sans la complexité d'une API séparée
- **Laravel 13** est stable et mature, même en version récente
- **shadcn-vue** accélère considérablement le développement UI
- **DDEV** est un excellent remplacement à Docker Compose manuel pour le dev Laravel
- Le pattern Inertia + Fortify + Spatie Permission est **très productif** pour des apps SaaS

Si vous hésitez entre Livewire et une SPA complète pour votre prochain projet Laravel, essayez Inertia.js. C'est le sweet spot que je cherchais.