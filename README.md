# International Draughts 10×10 (Java / JavaFX)

> A complete two-player draughts game with a modern JavaFX interface: international rules on a 10×10 board, mandatory and multiple captures, king promotion, timers, save/load and visual themes with accessibility options.

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![JavaFX](https://img.shields.io/badge/JavaFX-21-4e9a06?style=flat-square)
![OOP](https://img.shields.io/badge/OOP-encapsulation%20%C2%B7%20SRP-38f0c0?style=flat-square)

---

## Table of contents

- [Context and team](#context-and-team)
- [Features and rules](#features-and-rules)
- [Why JavaFX](#why-javafx)
- [Architecture and OOP quality](#architecture-and-oop-quality)
- [Getting started](#getting-started)
- [Retrospective](#retrospective)
- [Roadmap](#roadmap)

## Context and team

Built as a team project for an object-oriented programming course. The brief: a full game that follows the classic rules of international draughts, with a modern, intuitive graphical interface.

**Target audience:** fans of traditional strategy games, casual players who want a modern interface, and players who need visual accessibility options (colour-blindness, strong contrast).

| Contributor | Role | Main work |
|---|---|---|
| **Adama** | Backend & game logic | Game engine (`Jeu.java`, `Plateau.java`), move algorithms, capture chains, save system |
| **Michael** | Frontend & UI/UX | JavaFX interface (`Main.java`), animated backgrounds (`BackgroundAnimator`), timer, menus, themes |

## Features and rules

The game follows the classic rules of international draughts:

- **10×10 board** — 20 pieces per player (black vs white).
- **Two players** on the same machine (hot-seat).
- **Moves and captures** — diagonal moves; capturing is **mandatory**, and multiple captures in a row (chains) are handled automatically by the engine.
- **King promotion** — a piece reaching the far row becomes a king (♛/♕) and moves along long diagonals.
- **End of game** — victory is detected when a player has no pieces left or cannot move.
- **Extras** — per-player timer, move history, save/load, dynamic graphical themes.

## Why JavaFX

1. **Fluid UX** — transitions, hover effects and board rotation make the game feel alive.
2. **Robust error handling** — illegal moves never crash the app: the board shakes and a message explains why.
3. **Visual customisation** — JavaFX `Pane`s and `Node`s made it easy to build many themes and programmatic animated backgrounds, with accessibility modes supported natively.

## Architecture and OOP quality

- **Strict encapsulation** — attributes of `Piece`, `Plateau` and `Jeu` are private and only reachable through dedicated methods, so the game state stays consistent.
- **Single responsibility** — each class has one job:

| Class | Responsibility |
|---|---|
| `Piece` | Pure entity: coordinates, colour, status (man or king) |
| `Plateau` | Spatial logic: validates move geometry and applies board rules |
| `Jeu` | Turn controller: turn order, selection, capture chains |
| `Main` | GUI only: renders the state given by `Jeu` and captures clicks |
| `AppTheme`, `BackgroundAnimator` | Themes and animated backgrounds |

- **Extensible design** — the king state is a boolean for simplicity, but the structure would allow an abstract `Piece` with `Pion` and `Dame` subclasses if the rules grew more complex.

```text
src/
├── Main.java               JavaFX application and UI
├── Jeu.java                Game controller
├── Plateau.java            Board and rules
├── Piece.java              Piece entity
├── AppTheme.java           Colour themes
└── BackgroundAnimator.java Animated backgrounds
lib/                        JavaFX 21.0.2 jars
```

## Getting started

**Prerequisites:** JDK 17 or newer and the JavaFX SDK (version 21 jars are bundled in `lib/`; use the SDK matching your operating system).

```bash
git clone https://github.com/DaskoStudio/jeu-de-dames-java.git
cd jeu-de-dames-java

# PATH_TO_FX = folder containing the JavaFX jars for your OS
javac --module-path $PATH_TO_FX --add-modules javafx.controls,javafx.graphics,javafx.media -d out src/*.java
java  --module-path $PATH_TO_FX --add-modules javafx.controls,javafx.graphics,javafx.media -cp out Main
```

With IntelliJ IDEA or Eclipse, add the JavaFX libraries in *Project Structure → Libraries* and run `Main`.

## Retrospective

**Difficulties**
- **Multi-capture algorithm** — forcing a player to keep playing the same piece while a capture chain exists required rethinking state handling in `Jeu`.
- **View/model synchronisation** — preventing clicks on other squares while a move animation is still playing.

**What the project brought**
- Hands-on practice of core OOP concepts.
- Discovery of JavaFX: scenes, nodes and event handlers.
- Better teamwork and up-front software design (an implicit MVC split).

## Roadmap

1. **Solo mode (AI)** — a Minimax algorithm to play against the computer.
2. **Online multiplayer** — Java sockets (TCP/IP) to connect two remote players.
3. **Advanced history** — replay a saved game move by move.

## Tech stack

Java · JavaFX · Object-oriented programming

---

**Author** — Konaté Adama · [github.com/DaskoStudio](https://github.com/DaskoStudio)
