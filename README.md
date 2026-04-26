# PFE Stock Management

Monorepo du système intelligent de gestion et d'optimisation des stocks.

## Contenu

- `stock-api` : API Spring Boot, PostgreSQL, JWT, OAuth2 Google, Flyway, XGBoost
- `stock-web` : interface web de gestion **et BI** en Vue 3 / Vite / Vuetify
- `stock-mobile` : application mobile Expo / React Native

## Prérequis

- Docker + Docker Compose v2
- Java 17+ et Maven 3.9+ pour lancer `stock-api` hors Docker
- Node.js 20+ et npm pour `stock-web`
- Node.js 20+ et Expo CLI pour `stock-mobile`

## Lancement rapide avec Docker

Créer un fichier `.env` à la racine :

```env
DB_USERNAME=postgres
DB_PASSWORD=postgres
JWT_SECRET=stock-management-super-secret-key-pfe-2025-hs256-ok
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
AUTHORIZED_REDIRECT_URIS=http://localhost:5174/auth/callback
CORS_ORIGINS=http://localhost:5174,http://localhost:8080
```

Puis lancer :

```bash
docker compose up -d
```

## Accès

- Web : `http://localhost:5174`
- API : `http://localhost:8080/api/v1`
- Swagger : `http://localhost:8080/api/v1/swagger-ui.html`
- PostgreSQL : `localhost:5433`

## Données de démonstration

Les migrations Flyway créent automatiquement le schéma et les données de seed.

Comptes disponibles :

| Email | Mot de passe |
| --- | --- |
| `admin@stock.ma` | `Test@1234` |
| `manager@stock.ma` | `Test@1234` |
| `operateur@stock.ma` | `Test@1234` |

## Lancement en local sans Docker

### API

```bash
cd stock-api
mvn spring-boot:run
```

### Web

```bash
cd stock-web
npm install
npm run dev
```

### Mobile

```bash
cd stock-mobile
npm install
npm start
```

## Notes

- La partie BI est intégrée à `stock-web`.
- Les migrations SQL se trouvent dans `stock-api/src/main/resources/db/migration`.
- La documentation XGBoost se trouve dans `stock-api/docs/xgboost-explication.md`.
- La fiche de recette finale se trouve dans `docs/recette-finale.md`.
- La documentation mobile se trouve dans `stock-mobile/README.md`.
