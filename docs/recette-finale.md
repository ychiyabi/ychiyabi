# Recette finale

Cette fiche sert de base de validation finale et de démonstration du projet.

## Environnement validé

- `docker compose up -d`
- web disponible sur `http://localhost:5174`
- API disponible sur `http://localhost:8080/api/v1`
- Swagger disponible sur `http://localhost:8080/api/v1/swagger-ui.html`
- PostgreSQL exposé sur `localhost:5433`

## Comptes de démonstration

| Email | Mot de passe | Usage conseillé |
| --- | --- | --- |
| `admin@stock.ma` | `Test@1234` | démo complète |
| `manager@stock.ma` | `Test@1234` | gestion |
| `operateur@stock.ma` | `Test@1234` | opérations |

## Parcours à valider

### 1. Authentification email
- connexion avec `admin@stock.ma`
- récupération du profil utilisateur
- déconnexion

### 2. Authentification Google
- accès à l'endpoint OAuth d'information
- validation de la configuration de callback
- vérification du flux en environnement de démo si les credentials Google sont actifs

### 3. Workspaces
- lecture de la liste des workspaces
- consultation du workspace courant
- création d'un workspace de test
- mise à jour des informations du workspace

### 4. Catégories
- lecture des catégories du workspace
- création d'une catégorie de test

### 5. Produits
- lecture des produits du workspace
- consultation du détail produit
- création d'un produit de test lié à la catégorie créée

### 6. Mouvements
- lecture des mouvements
- création d'un mouvement `IN` ou `OUT` de test pour le produit créé

### 7. Alertes
- lecture des alertes
- lecture du compteur d'alertes

### 8. BI
- chargement du dashboard BI
- chargement du trend de ventes
- chargement du top produits
- chargement de l'ABC analysis

### 9. ML
- forecast sur un produit seed existant
- optimisation de stock sur un produit seed existant

### 10. Mobile
- ouverture de l'application Expo
- connexion
- navigation dashboard / produits / mouvements / alertes / workspaces / BI / ML

## Recette API exécutée

Les vérifications suivantes ont déjà été exécutées sur l'environnement courant :

- démarrage complet via Docker Compose
- health API
- accès web
- routes web principales servies correctement (`/`, `/login`, `/dashboard`, `/bi`)
- migrations Flyway
- données seed marocaines
- connexion email `admin@stock.ma`
- récupération du profil `/auth/me`
- contrôle du point d'information OAuth `/auth/oauth2/info`
- redirection d'entrée OAuth confirmée vers Google (`302`)
- lecture de la liste des workspaces
- création d'un workspace temporaire de recette
- création d'une catégorie temporaire
- création d'un produit temporaire
- création d'un mouvement de stock temporaire
- lecture du compteur d'alertes
- lecture des endpoints BI principaux
- lecture des endpoints ML principaux
- démarrage du mobile Expo en mode web sur `http://localhost:8081`
- suppression logique du workspace temporaire de recette

## Validation manuelle restante

Ces points restent à valider manuellement sur support graphique :

- flux Google OAuth complet dans le navigateur
- navigation visuelle complète dans `stock-web`
- navigation mobile Expo sur appareil ou émulateur

## Commandes utiles

### Démarrage

```bash
docker compose up -d
```

### Tests backend

```bash
cd stock-api
mvn test
```

### Tests frontend web

```bash
cd stock-web
npm test
npm run build
```

### Documentation des tests

- inventaire global : [`docs/tests-et-couverture.md`](./tests-et-couverture.md)
- tests backend détaillés : [`stock-api/docs/tests/`](../stock-api/docs/tests/)
- documentation des modules API : [`stock-api/docs/modules/README.md`](../stock-api/docs/modules/README.md)
- tests frontend détaillés : [`stock-web/docs/tests/`](../stock-web/docs/tests/)

### Mobile

```bash
cd stock-mobile
npm start
```

## Remarques

- la partie BI est intégrée dans `stock-web`
- la base de démonstration est désormais marocaine (`MAD`, `Africa/Casablanca`)
- la documentation globale des tests renvoie vers chaque suite backend et frontend
- cette fiche peut être réutilisée comme support de recette avant soutenance
