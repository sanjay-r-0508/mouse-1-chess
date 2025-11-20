## Quick Overview (30‑Second Pitch)

I worked on Mouse 1 Chess, a responsive single-page web app with an adjustable-strength AI opponent. It runs entirely client-side (HTML/CSS/JavaScript) and uses `chess.js` from a CDN for game rules. The UI renders an interactive board with move highlighting, status messaging, and a difficulty slider. The AI uses a minimax search with alpha–beta pruning and a material-based evaluation so users can practice against increasingly stronger play without a backend.
---

## Project Summary (1–2 Minutes)

 - **What it does:**
	 - Renders an 8×8 board with Lichess SVG pieces and smooth interactions (`createBoard`, `handleSquareClick`).
	 - Lets users select moves, highlights legal destinations, animates piece movement, and tracks status (`updateStatus`).
	 - Offers a five-level difficulty slider that maps to AI search depth.
	 - Runs fully in the browser; no build or server required — just open `index.html`.

 - **Why it matters:**
	 - **Accessibility:** instant load, mobile-friendly, zero install.
	 - **Learning tool:** adjustable AI provides a sparring partner for beginners to intermediates.
	 - **Demo of AI-in-the-browser:** shows how classic minimax can deliver engaging gameplay at small depths.

 - **Tech stack:**
	 - HTML5 + CSS3 (glassmorphism styling, responsive grid).
	 - Vanilla JavaScript (ES6); chess rules via `chess.js`.
	 - Piece assets from the Lichess CDN; can be deployed to any static host (GitHub Pages, Netlify, Hugging Face Spaces).

---

## Detailed Technical Explanation (3–5 Minutes)

1. **Architecture**
	 - Single HTML file containing markup, embedded CSS, and JS logic.
	 - `chess.js` maintains the authoritative game state; the DOM reflects it.
	 - No backend — state lives in the `Chess()` instance and DOM nodes.

2. **Core Components**
	 - **Board rendering:** `createBoard` loops over ranks/files, builds squares, attaches click handlers, and queries pieces via `chess.get`.
	 - **Interaction logic:** `handleSquareClick` restricts selection to the player's color, highlights legal moves using `chess.moves({ verbose: true })`, and executes moves via `makeMove`.
	 - **AI engine:** `makeAiMove` calls `getBestMove`, which runs minimax with alpha–beta pruning (`minimax`) over legal moves and evaluates boards with a material-only function (`evaluateBoard` using `pieceValues`).
	 - **Status/UX:** `updateStatus` displays check/checkmate/draw/turn; CSS classes like `selected` and `possible-move` control highlighting; `animateMove` provides subtle motion.

3. **Workflow**
	 - Page load → `createBoard` and `updateDifficulty`.
	 - Player turn: select piece → highlight → pick destination → `makeMove` → animate → board refresh → AI moves after a short delay.
	 - AI turn: compute best move at chosen depth, execute, re-render, and hand control back to the player.

4. **Difficulty Mapping**
	 - Slider values 1–5 map to minimax depths of roughly 2–6 plies, trading strength for latency.

5. **Deployment & Testing**
	 - Serve statically (open file directly or run `python -m http.server`).
	 - Manual testing: verify legal move enforcement, status updates, AI strength differences, and responsive layout.

---

## Key Points to Emphasize

 - **Frontend craftsmanship:** responsive grid, glassmorphism panel, hover/animation polish without frameworks.
 - **AI implementation:** minimax + alpha–beta in the browser; explain trade-offs and potential upgrades (move ordering, positional heuristics, Web Workers).
 - **User experience:** visual move cues, clear status text, smooth difficulty adjustments.
 - **Simplicity and deployability:** zero build, CDN dependencies, can work offline if assets are bundled.
 - **Extensibility:** add undo/history, configurable promotions, stronger evaluation functions as next steps.

---

## Structured Explanation Framework

1. **Start:** “Mouse 1 Chess is a static web chess app with an adjustable AI opponent.”
2. **Architecture:** HTML/CSS UI, `chess.js` state, minimax AI, no backend.
3. **Contributions:** call out the parts you developed (board rendering, AI logic, UX polish).
4. **Challenges/Solutions:** e.g., keeping the AI responsive as depth increases; ensuring UI highlighting matches `chess.js` state.
5. **Impact:** an instant-play chess trainer that demonstrates client-side AI and is easy to host/share.

---

## Common Interview Q&A

 - **Q:** How does the AI work?
	 - **A:** Minimax search with alpha–beta pruning over `chess.js` game states and a material-only evaluation; the slider controls search depth.

 - **Q:** Why no backend or frameworks?
	 - **A:** The goal was a lightweight, instantly deployable demo — `chess.js` + vanilla JS keeps the footprint minimal and maintenance simple.

 - **Q:** How do you ensure move legality?
	 - **A:** All validation is performed by `chess.js` (`chess.moves`, `chess.move`), so the UI cannot create illegal states.

 - **Q:** What would you improve next?
	 - **A:** Add positional heuristics, move ordering, undo/move history, configurable promotions, and offload deep searches to a Web Worker.

 - **Q:** How does the difficulty slider affect gameplay?
	 - **A:** It increases minimax depth (2–6 plies); higher depths explore more future moves and yield stronger but slower AI.

---

## Code Snippets to Reference

Typical functions to point to in `index.html`:

```js
function createBoard() { ... }
function handleSquareClick(e) { ... }
function makeMove(from, to) { ... }
function makeAiMove() { ... }
function getBestMove(game, depth) { ... }
function minimax(game, depth, alpha, beta, isMaximizing) { ... }
function evaluateBoard(board) { ... }
```

---

## Technical Metrics to Mention

 - **Board size:** 560 px desktop / 320 px mobile.
 - **Difficulty depths:** 2–6 plies.
 - **Piece evaluation:** P=1, N/B=3, R=5, Q=9 (king excluded from material eval).
 - **Dependencies:** `chess.js` from CDN, Lichess SVG assets.
 - **Latency:** typically <500 ms at depth ≤4; up to 1–3 s at depth 6 on modest hardware.

---

## Domain Knowledge Notes

 - Castling, en passant, and promotion are handled by `chess.js`.
 - Game state helpers like `chess.in_checkmate`, `chess.in_draw`, and `chess.turn` drive UI feedback.
 - Material-only evaluation limits strategic depth; discuss positional heuristics or neural networks as possible improvements.

---

## Sample Opening Statement

 "I built Mouse 1 Chess, a single-page chess web app that pairs a polished UI with a minimax-based AI opponent."

