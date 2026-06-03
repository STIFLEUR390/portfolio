# Livewire vs Sanctum : deux philosophies d'authentification Laravel

> **Projet lié :** [Auth Solutions & Boilerplates](../PROJET-13-auth-boilerplates.md)

En explorant l'authentification Laravel, j'ai construit des projets avec deux approches radicalement différentes : **Livewire** (server-side) et **Sanctum** (SPA token-based). Voici ce que j'en retiens.

## Livewire : l'authentification server-side

Livewire permet de créer des interfaces dynamiques sans écrire une ligne de JavaScript. L'auth se fait via les sessions PHP classiques.

### Comment ça marche

```php
// Livewire component : formulaire de connexion
class LoginForm extends Component
{
    public $email;
    public $password;

    public function login()
    {
        $this->validate([
            'email' => 'required|email',
            'password' => 'required',
        ]);

        if (Auth::attempt($this->only('email', 'password'))) {
            return redirect()->intended('/dashboard');
        }

        $this->addError('email', 'Identifiants incorrects.');
    }

    public function render()
    {
        return view('livewire.login-form');
    }
}
```

Le formulaire est rendu côté serveur, les mises à jour se font via AJAX (Wire). Zéro JavaScript à écrire.

**Avantages :**
- Simple à mettre en œuvre
- Sécurité maximum (tout se passe côté serveur)
- Compatible avec les templates Blade + AdminLTE
- Pas de gestion de tokens

**Inconvénients :**
- Pas de véritable SPA — chaque interaction recharge partiellement la page
- Moins adapté pour une API publique

## Sanctum : l'authentification SPA token-based

Sanctum permet une authentification via **tokens API** (stateless) ou **cookies** (stateful). Parfait pour des SPA Vue.js.

### Comment ça marche

```javascript
// Côté Vue 3 : connexion avec Sanctum
async function login(email, password) {
  // Étape 1 : GET CSRF cookie (pour SPA first-party)
  await axios.get('/sanctum/csrf-cookie')

  // Étape 2 : POST login
  const response = await axios.post('/api/login', { email, password })

  // Le token est stocké côté client
  localStorage.setItem('auth_token', response.data.token)
}

// Chaque requête authentifiée inclut le token
axios.defaults.headers.common['Authorization'] = `Bearer ${token}`
```

**Avantages :**
- Architecture SPA complète (Vue 3, React, etc.)
- API REST réutilisable (mobile, tiers)
- Tokens avec scopes et permissions
- CSRF protection automatique

**Inconvénients :**
- Gestion des tokens côté client (stockage, refresh, expiration)
- Plus de code à écrire (interceptors axios, guards de route)

## Comparatif

| Critère | Livewire | Sanctum |
|---------|----------|---------|
| Complexité | Faible | Moyenne |
| Expérience utilisateur | Quasi-SPA | SPA complète |
| API réutilisable | Non | Oui |
| Sécurité | ✅✅ (serveur) | ✅ (tokens) |
| Idéal pour | Apps Laravel monolithes | APIs + SPA / mobile |
| Courbe d'apprentissage | Douce | Modérée |

## Mon choix selon le projet

- **Dashboard admin** (AdminLTE, Blade) → **Livewire**. Rapide à développer, sécurisé, pas besoin de SPA.
- **Marketplace, application interactive** → **Sanctum**. La flexibilité d'une SPA Vue 3 + la réutilisabilité de l'API.
- **Projet solo ou équipe réduite** → **Livewire**. Moins de code, moins de bugs.
- **API publique + clients multiples** → **Sanctum**. C'est fait pour ça.

Les deux sont excellents. Le choix dépend du contexte, pas du dogme.