# Chess Board Logic

> A fully interactive chess board with complete piece movement rules, check/checkmate detection, and responsive UI.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://basic-chess-board-logic.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/basic-chess-board-logic)

---

## Purpose

Chess is one of the most complex logic problems you can solve in a browser. This project
teaches you to represent a board as a data structure, implement rule-based movement validation
for six different piece types, detect game-ending conditions (check, checkmate, stalemate),
and render interactive state (highlighted valid moves). The algorithmic thinking here — 
exploring possible moves, filtering by legality — is directly applicable to any rule engine.

## Tech Stack

- **Frontend:** React 19, TypeScript, Tailwind CSS 4
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** Zustand (game state)
- **Deployment:** Netlify

## Build Steps

1. **Represent the board.** Use an 8x8 2D array (or a Map with algebraic notation keys). Each cell holds `null` or a piece object: `{ type: 'king' | 'queen' | 'rook' | 'bishop' | 'knight' | 'pawn', color: 'white' | 'black' }`. Initialize with the standard starting position.
2. **Render the board.** An 8x8 CSS Grid with alternating light/dark squares. Render piece icons (Unicode chess symbols or SVGs) in occupied cells. Highlight the selected piece and its valid moves. Show file (a-h) and rank (1-8) labels.
3. **Implement movement rules.** For each piece type, write a function that returns all squares it can theoretically move to (ignoring check). Rook: rows and columns until blocked. Bishop: diagonals until blocked. Queen: both. Knight: L-shapes. Pawn: forward (+ double on first move, + diagonal capture). King: one square in any direction.
4. **Add move validation.** A move is legal only if: the destination is reachable by the piece's movement rules, the path isn't blocked (except knight), and making the move doesn't leave your own king in check. Filter theoretical moves through a "leaves king safe" check.
5. **Detect check and checkmate.** Check: any enemy piece can reach your king. Checkmate: you're in check AND no legal move escapes it. Stalemate: you're NOT in check but have no legal moves. Implement by trying all possible moves for the current player.
6. **Handle special moves.** Castling (king + rook swap if neither has moved and no squares are attacked), en passant (pawn captures diagonally after opponent's double-move), and pawn promotion (pawn reaches last rank — show piece selection UI).
7. **Add game management.** Turn indicator, move history (algebraic notation), captured pieces display, undo/redo, and new game reset. Store game state in Zustand for reactive UI updates.

## Deployment

Deploy on Netlify as a static React app. No backend or environment variables needed.
Pure logic — no external APIs.

## Tips

- The "does this move leave my king in check?" validation requires temporarily applying the move, checking if the king is attacked, then undoing it. This is the most expensive operation — optimize by only checking pieces that could attack the king.
- TypeScript discriminated unions are perfect for chess pieces: `type Piece = { type: 'pawn'; color: Color } | { type: 'rook'; color: Color; hasMoved: boolean }` — each piece type can carry its own extra state.
- Extension: add an AI opponent (minimax with alpha-beta pruning), move timers, or online multiplayer via WebSockets.

## README Guidance

The project repo's README should include a short description, a screenshot of the board with
highlighted valid moves, the live demo link, tech stack, features (all rules, check/checkmate,
special moves), and local dev instructions.
