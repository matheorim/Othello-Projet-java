# Othello-Projet-java

🇫🇷 [Version française](README.fr.md)

Java project completed at the IUT: a two-team board game played on a **hexagonal** grid, with **rings** and **pawns**, where players remove aligned lines. The game is currently played through a **console interface** (CUI).

The project is made of two Maven modules:

- **`HexagonalCoordinate`**: a library for hexagonal coordinates.
- **`sae21`**: the game itself (model, factories, console interface).

## Features

- Hexagonal board handled with two coordinate systems: **cube** and **doubled**
- Two teams (`Team`) playing in turn
- Two types of tokens: **rings** (`Ring`) and **pawns** (`Pawn`)
- Game actions: **move** (`Move`) and **line removal** (`RemoveLine`)
- Game state management (`State`)
- Console interface (`CUIMain`)
- Unit tests (JUnit) covering coordinates, factories, actions, state and tokens

## Technologies

- **Java** (version set in the `pom.xml` files)
- **Maven** for build and dependencies
- **JUnit** for testing
- Developed with **Eclipse** (`.classpath` and `.settings` files)

## Requirements

- JDK 17 or higher (adjust to the `pom.xml` files)
- Maven 3.8 or higher

## Installation and launch

```bash
git clone https://github.com/matheorim/Othello-Projet-java.git
cd Othello-Projet-java
git checkout CUIMain
```

The `sae21` module depends on `HexagonalCoordinate`. Install the library first, then build the game:

```bash
cd HexagonalCoordinate
mvn clean install

cd ../sae21
mvn clean compile
```

To launch the game, run the class `ui.CUIMain`, from your IDE (right-click `CUIMain.java` → Run) or with Maven if the `exec-maven-plugin` is configured:

```bash
mvn exec:java -Dexec.mainClass="ui.CUIMain"
```

## Running the tests

In each module:

```bash
mvn test
```

## Project structure

```
Othello-Projet-java/
├── HexagonalCoordinate/                 # Coordinates library
│   ├── pom.xml
│   └── src/
│       ├── main/java/coordinate/
│       │   ├── Coordinate.java          # Base of the coordinates
│       │   ├── CoordinateCube.java      # Cube coordinates
│       │   ├── CoordinateDoubled.java   # Doubled coordinates
│       │   ├── Direction.java           # Directions on the grid
│       │   ├── Mode.java
│       │   ├── Point.java
│       │   └── DifferentAxisException.java
│       └── test/java/testCoordinate/    # Coordinates tests
│
└── sae21/                               # The game
    ├── pom.xml
    └── src/
        ├── main/java/
        │   ├── factory/                 # Factories (cube / doubled)
        │   ├── model/
        │   │   ├── Model.java           # Main game model
        │   │   ├── Team.java            # Teams
        │   │   ├── action/              # Action, Move, RemoveLine
        │   │   ├── factory/             # Model factories
        │   │   ├── state/               # IState, State
        │   │   └── tokens/              # Token, Pawn, Ring
        │   └── ui/
        │       └── CUIMain.java         # Console interface
        └── test/java/                   # Unit tests
```

## Architecture

- **Coordinates**: `Coordinate` is extended by `CoordinateCube` and `CoordinateDoubled`, two ways of locating a cell on a hexagonal grid. `Direction` provides the six possible directions and `DifferentAxisException` signals an operation between incompatible coordinates.
- **Factories** (*Factory* pattern): `IFactory` is implemented by `FactoryCube` and `FactoryDoubled` to create game elements depending on the chosen coordinate system.
- **Actions** (*Command* pattern): `Action` is implemented by `Move` and `RemoveLine`, which makes moves easy to apply and to test.
- **State**: `State` (through `IState`) describes the current state of the board and of the game.
- **Tokens**: `Token` is the base class of `Ring` and `Pawn`.

## Branches

| Branch | Content |
|---|---|
| `CUIMain` | Main branch, with the console interface |
| `master` | Equivalent version of the main branch |

## Team

Group 9, IUT: **matheorim** and the other members of the group (to be completed).
