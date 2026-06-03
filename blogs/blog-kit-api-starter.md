# Opinionated API Starter : ce que j'ai mis dans Kit et pourquoi

> **Projet lié :** [Kit — API Starter](../PROJET-16-kit-api.md)

Après avoir démarré des dizaines de projets Laravel, j'ai remarqué un pattern : je passe les 2 premières heures à configurer les mêmes choses. J'ai décidé de créer **Kit**, un starter API qui embarque toutes mes décisions architecturales.

## Les décisions fortes

### 1. Contrôleurs invokables

Un contrôleur = une action. Finies les classes avec 6 méthodes :

```php
// ✅ Avant (Laravel standard)
class ContactController {
  public function index() { ... }
  public function store() { ... }
  public function show($id) { ... }
  public function update($id) { ... }
  public function destroy($id) { ... }
}
```

```php
// ✅ Après (invokable)
class RegisterController {
  public function __invoke(RegisterRequest $request) {
    // Une seule responsabilité
  }
}
```

**Pourquoi :** Chaque action est testable isolément. Pas de tentation de mutualiser du code qui n'a pas à l'être. Single Responsibility Principle appliqué aux contrôleurs.

### 2. Routes versionnées sans préfixe `/api`

Plus de `/api/v1/auth/login`. Juste `/v1/auth/login` :

```
GET    /v1/auth/me
POST   /v1/auth/register
POST   /v1/auth/login
```

La config se fait dans `bootstrap/app.php` avec `apiPrefix: ''`.

### 3. Scribe + OpenAPI Contract Tests

La documentation API est générée automatiquement par **Scribe** à partir d'attributs PHP 8. Mais surtout, j'ai ajouté des **OpenAPI Contract Tests** :

```php
// Concept : un test qui vérifie que l'API correspond à sa spec
test('api matches openapi spec')
  ->expect(fn () => $this->get('/v1/auth/register'))
  ->toMatchOpenApiSpec()
```

Si tu changes le comportement sans mettre à jour la spec, le test échoue. Si tu mets à jour la spec sans changer le comportement, le test échoue aussi. Les deux doivent être synchronisés en permanence.

### 4. SQLite-first

En développement, pas de MySQL. SQLite, un fichier, zéro configuration :

```bash
touch database/database.sqlite
php artisan migrate
```

**Pourquoi :** Plus besoin de lancer un conteneur MySQL en dev. Les tests sont plus rapides. La CI est plus simple. Et SQLite gère très bien les volumétries de développement.

### 5. Localisation API

Le header `Accept-Language` détermine la langue de la réponse, et `Content-Language` indique celle utilisée :

```
> Accept-Language: fr
< Content-Language: fr
< { "message": "Inscription réussie" }
```

### 6. Sunset middleware

Les API évoluent. Les endpoints meurent. Le Sunset middleware permet de marquer un endpoint comme déprécié et de planifier sa suppression :

```php
Route::middleware('sunset:2026-09-01')->group(function () {
    Route::get('/v1/old-endpoint', ...);
});
```

Le header `Sunset: Sat, 01 Sep 2026` est automatiquement ajouté à la réponse, prévenant les clients.

## Les packages inclus

| Package | Utilité |
|---------|---------|
| **Saloon** | Client HTTP avec cache, rate-limiting, pagination |
| **Stripe** | Paiements et abonnements |
| **Laravel Excel** | Import/export fichiers |
| **Laravel AI** | Fonctionnalités AI |
| **Spatie Data** | DTO avec validation |
| **Spatie Permission** | RBAC |
| **Laravel Phone** | Validation téléphone |
| **Sentry** | Monitoring |

## Résultat

Un nouveau projet Laravel API est opérationnel en **30 secondes** :
```bash
git clone kit mon-projet
cd mon-projet && composer install && composer run setup
php artisan serve
# API prête sur /v1/auth/register
```

J'ai transformé 2h de setup répétitif en 30s de clone. Et chaque nouveau projet bénéficie de toutes les améliorations que j'apporte à Kit.