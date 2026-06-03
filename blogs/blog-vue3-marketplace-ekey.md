# Créer une marketplace Vue 3 de A à Z : architecture, état, routing

> **Projet lié :** [E-Key Market](../PROJET-02-ekey-market.md)

Une marketplace e-commerce, c'est bien plus qu'un catalogue. C'est un panier, un checkout, des comptes utilisateurs, un programme de fidélité, une wishlist, du suivi de commandes… J'ai tout construit avec Vue 3.

## Le défi

**E-Key Market** devait gérer :
- Un catalogue de produits avec catégories
- Un **panier** avec gestion des quantités et persistance
- Un **checkout** en plusieurs étapes
- L'**authentification** complète (register, login, reset, confirm email)
- Un **dashboard utilisateur** avec historique et tracking
- Une **wishlist** avec alertes de prix
- Un **programme de fidélité** (points, badges, récompenses)

Le tout en responsive (desktop + mobile).

## Architecture choisie

### State management avec Pinia

Pinia remplace Vuex pour la gestion d'état. Un store par domaine :

```
stores/
├── cart.store.js         # Panier (persistant dans localStorage)
├── products.store.js     # Catalogue et filtres
├── auth.store.js         # Authentification et token
├── user.store.js         # Profil et préférences
└── loyalty.store.js      # Points et badges
```

L'avantage de Pinia par rapport à Vuex : **TypeScript-ready**, **DevTools intégré**, API plus intuitive (plus de mutations, actions directes).

### Routing avec Vue Router

Des routes organisées par module :

```javascript
const routes = [
  // Publiques
  { path: '/', component: Home },
  { path: '/products/:id', component: ProductDetail },

  // Auth
  { path: '/login', component: Login },
  { path: '/register', component: Register },
  { path: '/reset-password', component: ResetPassword },

  // Utilisateur (protégées)
  { path: '/dashboard', component: Dashboard, meta: { requiresAuth: true } },
  { path: '/orders', component: Orders, meta: { requiresAuth: true } },
  { path: '/wishlist', component: Wishlist, meta: { requiresAuth: true } },

  // Checkout
  { path: '/cart', component: Cart },
  { path: '/checkout', component: Checkout },
]
```

Les **Navigation Guards** vérifient le token à chaque route protégée.

### UI avec Tailwind CSS

Tailwind a permis un développement rapide sans sortir du HTML. Le thème est cohérent : couleurs, espacements, typographie — tout dans `tailwind.config.js`.

## Les leçons

1. **Pinia est un vrai game-changer** par rapport à Vuex. Moins de boilerplate, plus de flexibilité.
2. **La persistance du panier** (localStorage + Pinia) doit être robuste — ne pas perdre le panier au refresh est critique en e-commerce.
3. **Le responsive design** avec Tailwind, c'est juste des classes. `lg:grid-cols-4 md:grid-cols-2` et c'est plié.
4. **Un programme de fidélité** ajoute une vraie valeur perçue à l'application — les utilisateurs reviennent pour leurs points.

## Résultat

Un frontend e-commerce complet, modulaire, responsive, avec une architecture d'état claire et des routes bien organisées. Prêt à être connecté à n'importe quelle API backend.