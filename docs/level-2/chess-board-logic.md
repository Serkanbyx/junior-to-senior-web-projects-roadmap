# Chess Board Logic

> A fully interactive chess board with complete piece movement rules, check/checkmate detection, and pure logic implementation.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://basic-chess-board-logic.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/basic-chess-board-logic)

---

## Purpose

Chess is a masterclass in algorithmic thinking. You'll implement the rules of chess from
scratch — no chess libraries. Every piece has movement logic, captures are validated,
check is detected (is the king under attack?), and checkmate ends the game. It teaches
complex state machines, 2D array manipulation, and pure function design.

## Tech Stack

- **Framework:** React 19, TypeScript, Vite
- **Styling:** Tailwind CSS v4
- **State:** Zustand (board state, turn, move history, check status)
- **Deployment:** Netlify

## Build Steps

1. **Represent the board.** 8x8 2D array. Each cell: `null` or `{ type: 'pawn'|'rook'|..., color: 'white'|'black' }`. Initialize with standard starting position. Zustand holds the board and turn state.

2. **Implement piece movement rules.** Each piece type has a function: `getValidMoves(position, board) => Move[]`. Pawn (forward + capture diagonally), Rook (straight lines), Bishop (diagonals), Queen (both), Knight (L-shape), King (one square any direction).

3. **Add movement constraints.** A move is only valid if it doesn't leave your own king in check. After generating valid moves, filter out any that would result in self-check. This requires simulating each move and checking for threats.

4. **Implement check detection.** After each move, check if the opponent's king is under attack by any piece. Scan all pieces of the current player and check if any can reach the opponent's king position.

5. **Implement checkmate and stalemate.** Checkmate: king is in check AND no legal move removes the check. Stalemate: king is NOT in check BUT no legal moves exist. Both require checking all possible moves for the player.

6. **Build the UI.** Render the 8x8 board with Tailwind grid. Click a piece to select (show valid moves highlighted). Click a valid square to move. Show captured pieces, move history, and turn indicator.

7. **Add special moves.** Castling (king + rook swap if neither has moved and no check through), en passant (pawn captures), pawn promotion (pawn reaches last rank → choose piece).

## Tips

- The "does this move leave me in check?" validation is the most important constraint. For every candidate move: copy the board, apply the move, check if own king is attacked. If yes, the move is illegal. This prevents all impossible game states.
- Pure functions for move generation: `getValidMoves(piece, position, board)` takes immutable inputs and returns a list. No side effects. This makes the logic testable and debuggable.
- Extension: add move notation (algebraic), undo/redo, game timer, PGN export, or AI opponent (minimax algorithm).
