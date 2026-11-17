# Othello-Projet-java

🇬🇧 [English version](README.md)

Projet Orthello (java) réalisé à l'IUT : implémentation en **Java** d'un jeu de plateau à deux équipes sur une grille **hexagonale**, avec des **anneaux** et des **pions**, et la suppression de lignes alignées. Le jeu se joue pour l'instant en **interface console** (CUI).

Le projet est composé de deux modules Maven :

- **`HexagonalCoordinate`** : bibliothèque de gestion des coordonnées hexagonales.
- **`sae21`** : le jeu lui-même (modèle, fabriques, interface console).

## Fonctionnalités

- Plateau hexagonal géré par deux systèmes de coordonnées : **cubiques** et **doublées**
- Deux équipes (`Team`) qui jouent à tour de rôle
- Jetons de deux types : **anneaux** (`Ring`) et **pions** (`Pawn`)
- Actions de jeu : **déplacement** (`Move`) et **suppression d'une ligne** (`RemoveLine`)
- Gestion de l'état de la partie (`State`)
- Interface console (`CUIMain`)
- Tests unitaires (JUnit) sur les coordonnées, les fabriques, les actions, l'état et les jetons

## Technologies

- **Java** (version indiquée dans les `pom.xml`)
- **Maven** pour la compilation et les dépendances
- **JUnit** pour les tests
- Projet développé sous **Eclipse** (fichiers `.classpath` et `.settings`)

## Prérequis

- JDK 17 ou supérieur (à adapter selon les `pom.xml`)
- Maven 3.8 ou supérieur

## Installation et lancement

```bash
git clone https://github.com/matheorim/sae-21.git
cd sae-21
git checkout CUIMain
```

Le module `sae21` dépend de `HexagonalCoordinate`. Installe d'abord la bibliothèque, puis compile le jeu :

```bash
cd HexagonalCoordinate
mvn clean install

cd ../sae21
mvn clean compile
```

Pour lancer le jeu, exécute la classe `ui.CUIMain`, depuis ton IDE (clic droit sur `CUIMain.java` → Run) ou avec Maven si le plugin `exec-maven-plugin` est configuré :

```bash
mvn exec:java -Dexec.mainClass="ui.CUIMain"
```

## Lancer les tests

Dans chaque module :

```bash
mvn test
```

## Structure du projet

```
sae-21/
├── HexagonalCoordinate/                 # Bibliothèque de coordonnées
│   ├── pom.xml
│   └── src/
│       ├── main/java/coordinate/
│       │   ├── Coordinate.java          # Base des coordonnées
│       │   ├── CoordinateCube.java      # Coordonnées cubiques
│       │   ├── CoordinateDoubled.java   # Coordonnées doublées
│       │   ├── Direction.java           # Directions sur la grille
│       │   ├── Mode.java
│       │   ├── Point.java
│       │   └── DifferentAxisException.java
│       └── test/java/testCoordinate/    # Tests des coordonnées
│
└── sae21/                               # Le jeu
    ├── pom.xml
    └── src/
        ├── main/java/
        │   ├── factory/                 # Fabriques (cube / doublées)
        │   ├── model/
        │   │   ├── Model.java           # Modèle principal du jeu
        │   │   ├── Team.java            # Équipes
        │   │   ├── action/              # Action, Move, RemoveLine
        │   │   ├── factory/             # Fabriques du modèle
        │   │   ├── state/               # IState, State
        │   │   └── tokens/              # Token, Pawn, Ring
        │   └── ui/
        │       └── CUIMain.java         # Interface console
        └── test/java/                   # Tests unitaires
```

## Architecture

- **Coordonnées** : `Coordinate` est étendue par `CoordinateCube` et `CoordinateDoubled`, deux façons de repérer une case sur une grille hexagonale. `Direction` donne les six directions possibles et `DifferentAxisException` signale une opération entre coordonnées incompatibles.
- **Fabriques** (patron *Factory*) : `IFactory` est implémentée par `FactoryCube` et `FactoryDoubled`, pour créer les éléments du jeu selon le système de coordonnées choisi.
- **Actions** (patron *Command*) : `Action` est implémentée par `Move` et `RemoveLine`, ce qui rend les coups faciles à appliquer et à tester.
- **État** : `State` (via `IState`) décrit l'état courant du plateau et de la partie.
- **Jetons** : `Token` est la classe de base de `Ring` et `Pawn`.

## Branches

| Branche | Contenu |
|---|---|
| `CUIMain` | Branche principale, avec l'interface console |
| `master` | Version équivalente de la branche principale |

## Équipe

Groupe 9, IUT : **matheorim** et les autres membres du groupe (à compléter).
