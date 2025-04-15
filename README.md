# Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Example Input/Output](#example-inputoutput)
4. [How to Compile and Run](#how-to-compile-and-run)
5. [Code Structure and Logic](#code-structure-and-logic)
    - [Global Constants and Variables](#global-constants-and-variables)
    - [ANSI Color Definitions](#ansi-color-definitions)
    - [Animation Functions](#animation-functions)
    - [Difficulty Selection and Instructions](#difficulty-selection-and-instructions)
    - [Game Initialization](#game-initialization)
    - [Input Handling](#input-handling)
    - [Game Board Display](#game-board-display)
    - [Game Logic](#game-logic)
    - [Win/Loss Detection](#winloss-detection)
6. [Game Loop Breakdown](#game-loop-breakdown)
7. [Edge Cases Handled](#edge-cases-handled)
8. [Terminal Compatibility](#terminal-compatibility)
9. [Conclusion](#conclusion)

---

## Project Overview

This project is a complete implementation of the classic **Minesweeper** game using C++ in a console environment. It leverages standard C++ libraries and ANSI escape codes to render a fully playable, colored, and animated game in the terminal window.

## Features

- Console-based interactive Minesweeper game
- Supports 3 difficulty levels: Beginner (9x9, 10 mines), Intermediate (16x16, 40 mines), Advanced (24x24, 99 mines)
- Safe first move logic: the first revealed cell and its neighbors are guaranteed to be free of mines
- Recursive reveal of empty (zero-adjacent-mine) cells
- Flagging functionality for suspected mine locations
- Input validation and user-friendly messages
- Colored board output using ANSI escape sequences
- ASCII-based animations for loading, explosions, and celebrations

## Example Input/Output

=== CHOOSE DIFFICULTY LEVEL ===  
0 - Beginner (9x9, 10 mines)  
1 - Intermediate (16x16, 40 mines)  
2 - Advanced (24x24, 99 mines)  
Enter your choice (0-2): 0

Enter your move (row, column) and action (r for reveal, f for flag): 4 4 r  
[board updates with revealed cell]

Enter your move (row, column) and action (r for reveal, f for flag): 2 3 f  
[board shows a flag at (2,3)]

## How to Compile and Run

Make sure you're using a C++ compiler that supports C++11 or later.

**For Linux/macOS:**

g++ minesweeper.cpp -o minesweeper  
./minesweeper

**For Windows:**

Replace `usleep` with `Sleep`, include `<windows.h>`, and then compile with your IDE or with:  
g++ minesweeper.cpp -o minesweeper.exe  
minesweeper.exe

## Code Structure and Logic

This section explains how the code is structured and what each part does.

### Global Constants and Variables

- `SIDE` - board size depending on difficulty
- `MINES` - total number of mines
- `MAXSIDE`, `MAXMINES` - upper limits to support multiple difficulty levels
- `remainingMines` - keeps track of unflagged mines

### ANSI Color Definitions

Defines escape codes for red, green, yellow, blue, cyan, and reset. These enhance the terminal experience.

### Animation Functions

- `loadingAnimation(duration)`  
  Creates a "Loading..." effect using dots, to simulate processing.

- `explosionAnimation()`  
  Prints an ASCII animation in red to indicate when the user steps on a mine.

- `celebrationAnimation()`  
  Prints an ASCII-style firework animation in yellow when the player wins.

### Difficulty Selection and Instructions

- `chooseDifficultyLevel()`  
  Prompts the user to pick a game mode and sets `SIDE` and `MINES` accordingly.

- `displayInstructions()`  
  Shows basic gameplay instructions with a brief delay between each line.

### Game Initialization

- `initialise(realBoard, myBoard)`  
  Fills both game boards with dashes ('-') and triggers a loading animation.

- `placeMines(mines, realBoard, firstRow, firstCol)`  
  Randomly places mines after the first move. The first clicked cell and its neighbors will never contain mines.

### Input Handling

- `makeMove(x, y, action)`  
  Receives user input in the form: row, column, and action (either `r` to reveal or `f` to flag). Input is validated to ensure it's within bounds.

### Game Board Display

- `printBoard(board)`  
  Displays the current state of the board with coordinates. Uses color codes for flags, numbers, and hidden cells.

### Game Logic

- `countAdjacentMines(row, col, realBoard)`  
  Returns the number of mines around the specified cell.

- `isValid(row, col)`  
  Checks if the row and column are within board boundaries.

- `revealCell(row, col, myBoard, realBoard, visited, movesLeft)`  
  Reveals a cell. If it's a 0, recursively reveals all connected zero cells. Decreases `movesLeft` for each revealed cell.

- `flagCell(row, col, myBoard, remainingMines)`  
  Flags a cell if it's unflagged; unflags if already flagged. Adjusts `remainingMines`.

### Win/Loss Detection

- `playMinesweeper()`  
  Main game loop that:
  - Displays the board
  - Accepts and validates moves
  - Triggers recursive reveal or flag logic
  - Checks if a mine was triggered (loss) or all safe cells are revealed (win)

  On win, triggers `celebrationAnimation()`. On loss, triggers `explosionAnimation()` and displays the full mine board.

## Game Loop Breakdown

1. **Start**
   - Print instructions
   - Let the player choose difficulty
   - Initialize and clear boards

2. **Gameplay**
   - Prompt move (row, column, action)
   - If it’s the first move, mines are placed excluding first cell and neighbors
   - On 'r':
     - If mine: trigger explosion, show full board, end game
     - If safe: reveal, possibly cascade reveal
   - On 'f':
     - Flag/unflag the cell

3. **End**
   - Win: all safe cells revealed
   - Loss: stepped on mine
   - Show corresponding animation

## Edge Cases Handled

- First click is always safe
- Invalid coordinates are rejected
- Invalid actions (not `r` or `f`) are rejected
- Already revealed or flagged cells can't be re-revealed
- Number of remaining mines (for flags) is tracked accurately

## Terminal Compatibility

This game uses ANSI escape codes and `system("clear")` to manage terminal output. Works best on:

- Linux terminal
- macOS Terminal
- Windows (with ANSI support or via WSL / Git Bash)

## Conclusion

This project demonstrates a fully playable Minesweeper implementation in the terminal using only C++. It involves recursion, board management, flagging, and user interaction through simple terminal inputs, making it a good beginner-to-intermediate level C++ game project.

You can further improve this by:
- Adding a timer
- Implementing custom difficulty input
- Adding score or leaderboard
- Using ncurses for enhanced rendering

---

**Happy Sweeping!**
