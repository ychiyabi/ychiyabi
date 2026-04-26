# Tests et couverture du projet

Cette page centralise les tests actuellement présents dans le monorepo, ce qu'ils vérifient, et où trouver leur documentation détaillée.

## Commandes globales

```bash
cd stock-api && mvn test
cd stock-web && npm test
cd stock-web && npm run build
```

## Vue d'ensemble

| Projet | Type | Fichier de test | Ce que ça sécurise | Documentation |
| --- | --- | --- | --- | --- |
| `stock-api` | contrôleur | `AuthControllerTest` | statuts HTTP auth, validation d'entrée, logout | [`stock-api/docs/tests/AuthControllerTest.md`](../stock-api/docs/tests/AuthControllerTest.md) |
| `stock-api` | sécurité | `JwtTokenProviderTest` | signature JWT, claims, refresh token, rejet d'un token altéré | [`stock-api/docs/tests/JwtTokenProviderTest.md`](../stock-api/docs/tests/JwtTokenProviderTest.md) |
| `stock-api` | service | `CategoryServiceTest` | hiérarchie catégories, product count, garde-fous de suppression | [`stock-api/docs/tests/CategoryServiceTest.md`](../stock-api/docs/tests/CategoryServiceTest.md) |
| `stock-api` | service | `ProductServiceTest` | unicité SKU/barcode, fallbacks, statut stock | [`stock-api/docs/tests/ProductServiceTest.md`](../stock-api/docs/tests/ProductServiceTest.md) |
| `stock-api` | service BI | `BiServiceTest` | KPI dashboard, marge, alertes critiques, ABC | [`stock-api/docs/tests/BiServiceTest.md`](../stock-api/docs/tests/BiServiceTest.md) |
| `stock-api` | service ML | `FeatureEngineeringServiceTest` | série journalière, lags, rolling averages, vecteur futur | [`stock-api/docs/tests/FeatureEngineeringServiceTest.md`](../stock-api/docs/tests/FeatureEngineeringServiceTest.md) |
| `stock-web` | store | `auth.spec.js` | persistance session, erreurs login, refresh, logout | [`stock-web/docs/tests/auth-store.spec.md`](../stock-web/docs/tests/auth-store.spec.md) |
| `stock-web` | routeur | `index.spec.js` | guards d'accès, redirections login/dashboard | [`stock-web/docs/tests/router-guards.spec.md`](../stock-web/docs/tests/router-guards.spec.md) |

## Détail par sous-projet

### `stock-api`

Les tests backend sont orientés logique métier et sécurité :

- **authentification** : endpoints d'accès et JWT
- **catalogue** : catégories et produits
- **BI** : agrégations critiques pour la soutenance
- **ML/XGBoost** : préparation déterministe des données avant apprentissage

Documentation associée :

- docs de tests : [`stock-api/docs/tests/`](../stock-api/docs/tests/)
- docs modules : [`stock-api/docs/modules/README.md`](../stock-api/docs/modules/README.md)
- explication ML : [`stock-api/docs/xgboost-explication.md`](../stock-api/docs/xgboost-explication.md)

### `stock-web`

Les tests frontend actuels ciblent les briques les plus transverses :

- **store auth** pour la session utilisateur
- **guards routeur** pour les règles d'accès aux pages

Documentation associée :

- [`stock-web/docs/tests/auth-store.spec.md`](../stock-web/docs/tests/auth-store.spec.md)
- [`stock-web/docs/tests/router-guards.spec.md`](../stock-web/docs/tests/router-guards.spec.md)

## Ce que cette base de tests apporte

- elle couvre les flux les plus visibles de la démo
- elle sécurise les règles métier critiques sans dépendre de scénarios UI fragiles
- elle fournit une documentation traçable test par test pour le rapport ou la soutenance
