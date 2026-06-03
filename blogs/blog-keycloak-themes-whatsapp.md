# Keycloak : créer un thème WhatsApp personnalisé de A à Z

> **Projet lié :** [Keycloak WhatsApp Theme](../PROJET-07-keycloak-themes.md)

Keycloak est un des meilleurs solutions SSO (Single Sign-On) open-source. Mais ses pages d'authentification par défaut sont… fonctionnelles, sans plus. Quand on veut offrir une expérience utilisateur fluide, un thème personnalisé fait toute la différence.

## Pourquoi WhatsApp ?

L'idée : proposer un thème qui soit **instantanément reconnaissable**. L'interface WhatsApp est familière à des milliards d'utilisateurs. En l'utilisant comme inspiration visuelle, les utilisateurs se sentent immédiatement à l'aise sur les pages de connexion.

## Comprendre l'architecture des thèmes Keycloak

Keycloak utilise **FreeMarker** comme moteur de templates. Un thème se structure ainsi :

```
themes/
  mon-theme/
    login/
      login.ftl          # Page de connexion
      register.ftl        # Page d'inscription
      reset-password.ftl  # Mot de passe oublié
      confirm.ftl         # Confirmation email
      passkey.ftl         # Authentification passkey
    account/
      account.ftl         # Gestion de compte
    resources/
      css/
        styles.css
      img/
        logo.png
```

Chaque fichier `.ftl` est un template HTML avec des variables FreeMarker injectées par Keycloak.

## Les pages personnalisées

Pour le thème WhatsApp, j'ai couvert :

1. **Login** — Interface de connexion avec le champ utilisateur/mot de passe aux couleurs WhatsApp (vert caractéristique #25D366)
2. **Register** — Formulaire d'inscription complet
3. **Reset Password** — Flux de réinitialisation de mot de passe
4. **Confirm Email** — Page de confirmation avec instruction claire
5. **Passkey** — Authentification sans mot de passe (modernité)

## Déploiement avec Docker

Le projet inclut un `docker-compose.yaml` et un `docker-compose.whatsapp.yaml` pour :

```yaml
# Concept : monter le thème dans le conteneur Keycloak
volumes:
  - ./themes/whatsapp:/opt/keycloak/themes/whatsapp
```

Avec un guide complet (`GUIDE_THEMES.md`) expliquant comment créer ses propres thèmes, de la structure au déploiement.

## Ce que j'ai appris

- **FreeMarker** est puissant mais a ses particularités (échappement, macros). Bien comprendre le moteur de templates évite des heures de debug.
- Un **guide complet** (GUIDE_THEMES.md) double la valeur du projet — les autres développeurs peuvent réutiliser le travail pour créer leurs propres thèmes.
- La **personnalisation des pages d'auth** est un excellent moyen d'améliorer l'expérience utilisateur sans toucher au backend.

## Résultat

Un thème Keycloak professionnel, dockerisé, documenté, avec 5+ templates personnalisés — prêt à être déployé en production.