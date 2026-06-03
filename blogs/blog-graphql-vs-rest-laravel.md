# GraphQL vs REST avec Laravel : mon retour d'expérience

> **Projet lié :** [Todo GraphQL](../PROJET-10-todo-graphql.md)

REST, c'est la norme. GraphQL, c'est la promesse de flexibilité totale. J'ai voulu construire le même projet (une todolist) avec les deux approches pour me faire mon propre avis.

## Le projet test : une todolist

Une todolist, c'est simple : des tâches avec un titre, un statut, une date. Mais les interactions sont variées :
- Lister les tâches (avec filtres et tris)
- Créer / modifier / supprimer
- Marquer comme terminée
- Rechercher par mots-clés

Parfait pour comparer.

## Approche REST

Avec une API REST Laravel classique :

```
GET    /api/taches           → liste (avec ?status=done&sort=created_at)
POST   /api/taches           → créer
PUT    /api/taches/{id}      → modifier
DELETE /api/taches/{id}      → supprimer
```

**Avantages :**
- Simple, prévisible, bien supporté
- Cache HTTP facile (ETags, Cache-Control)
- Outillage standard (Postman, insomnia)

**Inconvénients :**
- **Over-fetching** — l'API renvoie toujours le même payload, même si le client ne veut qu'un champ
- **Multi-endpoints** — pour charger une tâche + son auteur + ses commentaires, il faut 3 requêtes
- **Versioning** — changer le payload = nouvelle version d'API

## Approche GraphQL

Avec Lighthouse (PHP GraphQL server pour Laravel) :

```graphql
query {
  tasks(status: DONE) {
    id
    title
    created_at
    author {
      name
    }
  }
}
```

**Avantages :**
- **Requêtes exactes** — le client reçoit uniquement ce qu'il demande
- **Nested queries** — une seule requête pour charger la tâche, l'auteur ET les commentaires
- **Pas de versioning** — on ajoute des champs, on ne casse jamais le contrat

**Inconvénients :**
- **Complexité** — le schéma GraphQL, les résolveurs, les types, c'est plus de code
- **Cache** — le cache HTTP devient compliqué (tous les appels sont des POST)
- **Performance** — N+1 problem si mal implémenté (mais Lighthouse a des solutions)

## Mon verdict

| Critère | REST | GraphQL |
|---------|------|---------|
| Simplicité initiale | ✅✅ | ✅ |
| Documentation auto | ✅ (Swagger) | ✅✅ (Introspection) |
| Performance requêtes | ✅✅ | ✅ (si bien fait) |
| Flexibilité client | ✅ | ✅✅ |
| Cache | ✅✅ | ✅ |
| Outillage | ✅✅ | ✅ |

**Si je devais recommencer :**
- Pour une **API publique** (consommateurs inconnus) → REST. Simple, standard, tout le monde sait l'utiliser.
- Pour un **client-first** (SPA, mobile) → GraphQL. La flexibilité côté client est imbattable.
- Pour une **todolist** → REST. GraphQL est overkill ici.

GraphQL brille vraiment quand le client a des besoins de données complexes et variables. Pour le reste, REST fait très bien le job.