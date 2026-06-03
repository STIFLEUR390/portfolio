# Architecture Laravel : Repository, Service, Policy — Ce que j'ai appris sur HookBridge

> **Projet lié :** [HookBridge API](../PROJET-03-hookbridge-api.md)

Quand j'ai commencé avec Laravel, tout tenait dans les contrôleurs. Puis le code grossit, les contrôleurs deviennent des fourre-tout, et maintenir devient un enfer. HookBridge API a été l'occasion de structurer proprement.

## Le problème initial

HookBridge est une API de gestion de webhooks et callbacks. Concrètement :
- Création de projets avec configuration
- Endpoints webhooks avec secrets et événements
- Callbacks avec validation et historique
- Notifications asynchrones

Sans structure, chaque contrôleur aurait contenu : validation + requêtes SQL + logique métier + transformation de réponse → des milliers de lignes impossibles à tester.

## La solution en couches

### 1. Repository Pattern

Les repositories encapsulent l'accès aux données :

```
App/Repositories/
├── ProjectRepository.php
├── WebhookRepository.php
└── CallbackRepository.php
```

Chaque repository contient **uniquement** des requêtes Eloquent. Pas de logique métier, juste "comment récupérer/enregistrer les données".

### 2. Service Layer

Les services contiennent la **logique métier** :

```
App/Services/
├── WebhookService.php      # Traitement des payloads webhook
├── CallbackService.php     # Logique de callback
└── NotificationService.php # Envoi des notifications
```

Un contrôleur appelle un service, le service utilise un repository si besoin.

### 3. Policies

Les policies gèrent les **autorisations** :

```php
// Exemple : seul le propriétaire du projet peut configurer ses webhooks
public function configure(User $user, Project $project)
{
    return $user->id === $project->user_id;
}
```

### 4. Traits pour le cross-cutting

Des traits réutilisables pour la pagination, les réponses formatées, la validation, etc.

## Le résultat

```
Contrôleur (10 lignes)
  → Service (50 lignes, logique métier)
    → Repository (20 lignes, requêtes)
      → Policy (5 lignes, autorisation)
```

Chaque couche a une responsabilité unique. Tester devient trivial : on mock le repository, on teste le service.

## Le retour d'expérience

- **Ne pas over-engineer** — Pour une CRUD simple, Repository + Service c'est trop. J'ai appris à doser : un pattern par besoin, pas par dogme.
- **Les Policies Laravel sont sous-estimées** — Elles permettent une séparation nette des autorisations, bien plus clean que des `if` dans les contrôleurs.
- **La cohérence paie** — Une fois la structure en place, ajouter une nouvelle entité prend 10 minutes au lieu d'une heure.

Si vous démarrez un projet Laravel qui va durer, prenez le temps de poser cette architecture dès le départ. La refactorisation après coup est toujours plus douloureuse.