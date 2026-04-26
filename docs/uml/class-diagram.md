# Diagramme de classes

Le diagramme ci-dessous decrit les principales entites du domaine metier et leurs relations, telles qu'elles apparaissent dans `stock-api`.

## Version dessinee

![Diagramme de classes](./class-diagram.svg)

```mermaid
classDiagram

    class User {
        +UUID id
        +String email
        +String fullName
        +String passwordHash
        +String avatarUrl
        +AuthProvider provider
        +UserRole role
        +Boolean isActive
        +Boolean emailVerified
    }

    class Workspace {
        +UUID id
        +String name
        +String description
        +String currency
        +String timezone
        +String locale
        +String logoUrl
        +Boolean isActive
    }

    class WorkspaceMember {
        +UUID id
        +MemberRole role
        +Instant invitedAt
        +Instant acceptedAt
    }

    class Category {
        +UUID id
        +String name
        +String description
        +String color
    }

    class Product {
        +UUID id
        +String sku
        +String barcode
        +String name
        +String description
        +String unit
        +BigDecimal unitPrice
        +BigDecimal unitCost
        +BigDecimal currentStock
        +BigDecimal minStockThreshold
        +BigDecimal maxStockThreshold
        +BigDecimal reorderPoint
        +BigDecimal safetyStock
        +Integer leadTimeDays
        +Boolean isActive
        +String abcClass
    }

    class StockMovement {
        +UUID id
        +MovementType type
        +BigDecimal quantity
        +BigDecimal unitPrice
        +String reference
        +String note
        +Instant movementDate
    }

    class StockAlert {
        +UUID id
        +AlertType type
        +String message
        +Boolean isRead
        +Boolean isResolved
        +Instant createdAt
        +Instant resolvedAt
    }

    class MlModel {
        +UUID id
        +String modelPath
        +Json features
        +Json metrics
        +Instant trainedAt
        +Boolean isActive
    }

    class SalesForecast {
        +UUID id
        +LocalDate forecastDate
        +BigDecimal predictedQty
        +BigDecimal confidence
        +Integer horizonDays
        +Instant generatedAt
    }

    User "1" --> "0..*" Workspace : owns
    User "1" --> "0..*" WorkspaceMember : joins
    Workspace "1" --> "0..*" WorkspaceMember : contains

    Workspace "1" --> "0..*" Category : organizes
    Category "0..1" --> "0..*" Category : parent_of
    Workspace "1" --> "0..*" Product : stores
    Category "0..1" --> "0..*" Product : classifies

    Workspace "1" --> "0..*" StockMovement : tracks
    Product "1" --> "0..*" StockMovement : affected_by
    User "1" --> "0..*" StockMovement : performs

    Workspace "1" --> "0..*" StockAlert : generates
    Product "1" --> "0..*" StockAlert : triggers

    Workspace "1" --> "0..*" MlModel : trains
    Product "1" --> "0..*" MlModel : has_model

    Workspace "1" --> "0..*" SalesForecast : predicts
    Product "1" --> "0..*" SalesForecast : has_forecast
```

## Points importants

- `Workspace` est l'entite centrale du systeme
- `WorkspaceMember` porte le role collaboratif (`OWNER`, `MANAGER`, `OPERATOR`, `VIEWER`)
- `Product` concentre les seuils et informations de stock
- `StockMovement` alimente a la fois la gestion operationnelle, la BI et le ML
- `MlModel` et `SalesForecast` relient le machine learning au metier
