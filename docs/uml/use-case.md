# Diagramme de cas d'utilisation

Le diagramme suivant represente les principaux acteurs et cas d'utilisation du systeme de gestion et d'optimisation des stocks.

## Version dessinee

![Diagramme de cas d'utilisation](./use-case.svg)

```mermaid
flowchart LR
    visiteur[Visiteur]
    utilisateur[Utilisateur authentifie]
    owner[Owner]
    manager[Manager]
    operator[Operateur]
    google[Google OAuth]

    subgraph systeme[Plateforme Stock Management]
        UC1((S'inscrire))
        UC2((Se connecter))
        UC3((Se connecter avec Google))
        UC4((Consulter le profil))
        UC5((Gerer les workspaces))
        UC6((Gerer les membres))
        UC7((Gerer les categories))
        UC8((Gerer les produits))
        UC9((Enregistrer un mouvement de stock))
        UC10((Consulter les alertes))
        UC11((Consulter les tableaux de bord BI))
        UC12((Entrainer un modele ML))
        UC13((Generer une prevision de demande))
        UC14((Optimiser le stock))
        UC15((Utiliser la plateforme depuis le web))
        UC16((Utiliser la plateforme depuis le mobile))
    end

    visiteur --> UC1
    visiteur --> UC2
    visiteur --> UC3
    google --> UC3

    utilisateur --> UC4
    utilisateur --> UC5
    utilisateur --> UC7
    utilisateur --> UC8
    utilisateur --> UC9
    utilisateur --> UC10
    utilisateur --> UC11
    utilisateur --> UC12
    utilisateur --> UC13
    utilisateur --> UC14
    utilisateur --> UC15
    utilisateur --> UC16

    owner --> UC6
    owner --> UC5

    manager --> UC6
    manager --> UC7
    manager --> UC8
    manager --> UC9

    operator --> UC7
    operator --> UC8
    operator --> UC9
```

## Lecture rapide

- le **visiteur** peut s'inscrire et se connecter
- l'**utilisateur authentifie** accede aux fonctions metier et analytiques
- le **owner** et le **manager** disposent d'un perimetre plus large sur les workspaces et les membres
- l'**operateur** participe aux operations quotidiennes de stock
- **Google OAuth** intervient dans le flux d'authentification externe
