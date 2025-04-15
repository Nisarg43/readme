# Console-Based Minesweeper in C++

This project implements a **terminal-based Minesweeper game in C++**. The logic, gameplay, and board representation are all handled manually using standard C++ features, along with basic terminal control (e.g., clearing the screen and setting delays).

---

## Table Of Content
1.[Board State Representation
](#Board State Representation)

## 🗂️ File Overview

- `minesweeper.cpp` – Contains all game logic, board generation, user input, win/loss checks, and supporting functions.

---

## 🔄 High-Level Game Flow

1. **Main Function Entry Point**
   - Calls the `title()` function to show a splash screen.
   - Displays instructions through `instructions()` function.
   - Enters the main game loop via `playGame()`.

2. **Gameplay Loop**
   - The game board is initialized.
   - The player is repeatedly prompted for input.
   - The board is updated and printed after each move.
   - Win/loss conditions are checked and the loop exits accordingly.

---

## 🧠 Core Logic Description

### `playGame()`

- Initializes key game state:
  - `actualBoard` – stores the real state of the board with mines.
  - `userBoard` – stores what the player sees.
  - `revealed` – boolean grid for revealed cells.
  - `flagged` – boolean grid for flagged cells.
- Accepts user input to reveal or flag cells.
- Checks for valid input, bounds, and repeats.
- Checks for win/loss after every reveal.

### `setBoard()`

- Sets difficulty by asking user input (easy, medium, hard).
- Based on difficulty, it calculates board size and number of mines.

### `placeMines()`

- Randomly places mines on the board ensuring:
  - The first revealed cell is always safe.
  - No duplicate mine placement.
- Uses a loop and random generation (`rand()`) to place all mines.

### `countAdjacentMines()`

- For a given cell, counts how many of the surrounding 8 cells contain mines.
- This number determines what gets shown when a cell is revealed.

### `revealCells()`

- Implements **flood fill** algorithm:
  - If the revealed cell has no adjacent mines, all neighboring cells are automatically revealed recursively.
- Prevents revisiting already revealed cells using `revealed` grid.

### `printBoard()`

- Prints the current game state in the terminal.
- Based on the `userBoard` and flag/reveal state, shows appropriate characters.
- Uses symbols like `*`, numbers, or space for unrevealed, numbered, and empty cells.

### `checkWin()`

- A player wins when all **non-mine cells** are revealed.
- It counts the total number of revealed cells and compares with expected number.

---

## 🎯 Input and Interaction

- The player enters 3 values per turn:
  - Row index
  - Column index
  - Action (`r` for reveal, `f` for flag)
- The code checks input validity:
  - Input must be within board boundaries.
  - The cell must not be already revealed.

### Input Example: Enter your move (row, column) and action (r for reveal, f for flag) -> 2 3 r


### ScreenShot

![screenshot_1744721382581.png](<https://media-hosting.imagekit.io/82128bb7d240488f/screenshot_1744721382581.png?Expires=1839329382&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=WDoC4jZ1yaPxkGQVhYt7d7oJr5RzizQmdemqNlrwT2zykHSZTwOaEAHYIw8LlRXDDuY-czE8VuYVqWPXgcly-uUCTAqMoaL2qwBkQvHED8VZ-2tntnWlRAaFvw6-1xAKceR-vNIBDVAZqdoBvbySujpHGRBP8SbTFWoR~NHbSsnT5wQAtPGm5ftuReliC~wfHW-TDRuSEP2gWCuoEKsx2MKCAS2tjHCZkjEFbDhFaZSE2aq38PhmallNYKnDyKv72UOVQPpRFGBse7VK9JDmWAwK-zlMtpP7tFfY9Y8S6oTVgI~~-M5sGTuYYPHi3UHM0ItUUgK4nSumgqNSHAg-MQ__>)


---

## Board State Representation

- **Mine cells** are represented with a `.`.
- **Flagged cells** are marked with a custom symbol (e.g., `F` or 🚩).
- **Numbered cells** represent count of adjacent mines.
- **Unrevealed cells** are shown with a placeholder character.

---

## 💥 Loss and 🎉 Win Logic

- If the user reveals a cell containing a mine:
  - Game over sequence is triggered (explosion).
- If all non-mine cells are revealed:
  - Win screen is shown with a celebration.
- Post-game, the board is fully revealed for reference.

---

## 🔧 Utility Functions

### `clearScreen()`
- Clears the terminal screen for better user experience.

### `delay()`
- Uses `usleep()` to create time delays.
- Useful for animations and pacing.

### `title()`
- Displays game title using ASCII or characters.

### `instructions()`
- Displays rules and how to play.

### `printFinalBoard()`
- Called at game end to reveal the full board.
- Shows mines, flags, and all numbers regardless of previous state.

---

## ⚙️ Random Number Generation

- Mines are placed randomly using `rand()`.
- `srand(time(0))` seeds the random number generator to ensure randomness between games.

---

## 🧪 Validations and Edge Case Handling

- Prevents:
  - Revealing flagged cells.
  - Flagging already revealed cells.
  - Out-of-bounds access.
  - Flagging the same cell multiple times.

- First move protection:
  - Ensures the first selected cell is always safe.
  - Adjusts mine placement accordingly.

---

## 🔐 Game State Management

- All key state (mines, flags, reveals) are stored in separate 2D vectors:
  - `actualBoard` – character representation of real content
  - `userBoard` – display board
  - `revealed` – bool grid
  - `flagged` – bool grid

- This separation allows for flexible update and check logic.

---

## 📈 Scalability

- Board size and mine count are adjustable based on difficulty.
- You can add custom difficulty by modifying the `setBoard()` function.
- Board printing scales with larger boards but may require minor spacing tweaks.

---

## 🛠 How to Modify for Your Use

- **To change mine symbol**: update print functions and `actualBoard` generation.
- **To enable user-defined sizes**: allow custom input in `setBoard()`.
- **To disable animations**: remove or comment out `delay()` calls.

---

## 📦 Compilation & Execution

```bash
g++ -std=c++11 -o minesweeper minesweeper.cpp
./minesweeper
