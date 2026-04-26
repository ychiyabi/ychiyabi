# Diagrammes de sequence

Ce fichier propose deux diagrammes de sequence Mermaid representatifs du projet :

1. authentification email
2. entrainement et prediction ML

## 1. Authentification email

![Diagramme de sequence - authentification](./sequence-auth.svg)

```mermaid
sequenceDiagram
    actor U as Utilisateur
    participant W as Stock Web / Mobile
    participant AC as AuthController
    participant AS as AuthService
    participant UR as UserRepository
    participant JP as JwtTokenProvider

    U->>W: saisir email + mot de passe
    W->>AC: POST /auth/login
    AC->>AS: login(loginRequest)
    AS->>UR: rechercher l'utilisateur par email
    UR-->>AS: utilisateur trouve
    AS->>AS: verifier le mot de passe
    AS->>JP: generateAccessToken(user)
    JP-->>AS: accessToken
    AS->>JP: generateRefreshToken(user)
    JP-->>AS: refreshToken
    AS-->>AC: AuthResponse(user, tokens)
    AC-->>W: 200 OK + session
    W-->>U: ouverture du dashboard
```

## 2. Entrainement ML et generation de prevision

![Diagramme de sequence - ML](./sequence-ml.svg)

```mermaid
sequenceDiagram
    actor U as Utilisateur
    participant V as Vue ML (Web)
    participant MC as MlController
    participant MS as MlService
    participant FES as FeatureEngineeringService
    participant SMR as StockMovementRepository
    participant XGT as XGBoostTrainer
    participant MLR as MlModelRepository
    participant XGP as XGBoostPredictor
    participant SFR as SalesForecastRepository

    U->>V: lancer l'entrainement d'un produit
    V->>MC: POST /workspaces/{workspaceId}/ml/train/{productId}
    MC->>MS: trainModel(workspaceId, productId)
    MS->>FES: buildDailySalesTimeSeries(...)
    FES->>SMR: lire les mouvements OUT et LOSS
    SMR-->>FES: historique des mouvements
    FES-->>MS: serie temporelle completee
    MS->>FES: buildFeatureVectors(timeSeries)
    FES-->>MS: features d'entrainement
    MS->>XGT: train(vectors, modelPath)
    XGT-->>MS: modelPath + rmse + mae
    MS->>MLR: sauvegarder le modele actif
    MLR-->>MS: modele enregistre
    MS-->>MC: ModelTrainingResponse
    MC-->>V: resultat de l'entrainement

    U->>V: demander une prevision
    V->>MC: GET /workspaces/{workspaceId}/ml/forecast/{productId}
    MC->>MS: forecast(workspaceId, productId, horizonDays)
    MS->>FES: reconstruire l'historique recent
    FES-->>MS: historique
    MS->>XGP: predict(modelPath, futureVectors)
    XGP-->>MS: quantites predites
    MS->>SFR: supprimer anciennes previsions
    MS->>SFR: enregistrer nouvelles previsions
    SFR-->>MS: previsions persistantes
    MS-->>MC: ForecastResponse
    MC-->>V: courbe de prevision
```

## Utilisation dans le rapport

- le premier diagramme peut etre utilise dans la partie **authentification / securite**
- le second diagramme peut etre utilise dans la partie **ML / XGBoost**
- si besoin, ces diagrammes peuvent etre exportes en image avant insertion dans le document Word
