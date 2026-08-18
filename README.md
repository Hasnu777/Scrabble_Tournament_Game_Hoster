# Scrabble Tournament Game Hoster

A desktop app for administering and playing Scrabble tournament matches, built as a project for **AQA A-Level Computer Science**. An administrator logs in, hosts games between two players, and match data — moves, scores, and results — is persisted to a local SQLite database.

## Features

- **Admin login flow** — a `LogIn_Window` gates access; only an authenticated administrator can start or load a game
- **Game hosting** — `HomeScreen_Window` lets the admin start a new game (selecting a language) or load an existing saved game from file
- **Full match tracking** — a relational SQLite schema (`ScrabbleTournamentGame.db`) tracks:
  - `Administrators` — accounts running the tournament
  - `Players` — participants, linked to the game they played
  - `Games` — one row per match, with players, language, date, and result
  - `AdminGames` / `PlayerGames` — join tables linking admins and players to the games they hosted/played
  - `GameHistory` — move-by-move log: words played, score, and whether a turn was an exchange or a pass
- **Multi-language support** — language is selected per game (defaults to English)
- **Windows build** — a `windowsV2` package with the packaged/updated UI

## Tech Stack

- **Python**
- **SQLite3** (via the standard library `sqlite3` module)
- Custom `windowsV2` / `GameFiles` modules for the UI and game logic

## Project Structure

```
├── main.py              # Entry point: creates DB tables, runs login → home screen → game flow
├── GameFiles/            # Core game logic (MainGame window, Scrabble rules/board)
├── windowsV2/             # UI windows (LogIn_Window, HomeScreen_Window)
├── assets/                # Images/UI assets
├── data/                  # Supporting data (e.g. word lists / language files)
├── ScrabbleTournamentGame.db          # Production database
├── ScrabbleTournamentGameFORTESTING.db # Test database
└── word_lists.db          # Dictionary/word-validation data
```

## How It Works

1. `main.py` initializes the SQLite schema (creates all tables if they don't already exist).
2. `LogIn_Window` runs and requires a valid administrator login before continuing.
3. Once logged in, `HomeScreen_Window` runs, letting the admin either:
   - pick a language and start a **new game**, or
   - select a save file to **load an existing game**.
4. `MainGame.CreateGameWindow` launches the actual Scrabble match with the selected players.
5. Match data (moves, scores, passes/exchanges) is written to `GameHistory` as the game progresses.

## Getting Started

### Dependencies
`pygame`, `pygame_gui`, `tkinter`, `CustomTkinter`, `sqlite3` are required libraries. `pip install <insert_library>` for each is sufficient.

```bash
git clone https://github.com/Hasnu777/Scrabble_Tournament_Game_Hoster.git
cd Scrabble_Tournament_Game_Hoster
python main.py
```

## Testing

See `List of Testing Requirements [COMPLETED].txt` and `List of Testing Requirements v2 [Beta].txt` for the manual test plan used to validate functionality against the A-Level coursework spec.

## Background

Originally built for AQA A-Level Computer Science coursework, as a full-stack (UI + relational database) desktop application demonstrating database design, GUI programming, and game-logic implementation in Python.
