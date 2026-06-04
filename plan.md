## Plan: Add standalone puzzles page and test puzzle data

TL;DR - Create a new `puzzles.html` page with the same left sidebar as `index.html`, add a `puzzles` folder with one test puzzle file, and wire the existing `Puzzles` button in `index.html` to open the new page.

**Steps**
1. Update `index.html` sidebar `Puzzles` button so it navigates to `puzzles.html` instead of showing a coming soon message.
2. Create `puzzles.html` in the project root.
   - Include `tailwindcss` and `chess.js` like `index.html`.
   - Reuse the same sidebar markup structure and CSS class names from `index.html`.
   - Make the sidebar buttons link back to `index.html` for New match and other top-level views.
3. Build the puzzles homepage layout in `puzzles.html`.
   - Add a responsive intro area and a grid of puzzle cards.
   - Use brand accents, dark panel tones, and a desktop-first layout with a mobile fallback.
   - Each puzzle card loads a puzzle when clicked.
4. Add board and puzzle solve layout.
   - When the user picks a puzzle, render the board from the chosen puzzle FEN.
   - Show a side panel with attempt feedback and a Reveal solution button.
   - Track move attempts and show correct messages in a styled feedback box.
   - After 3 wrong attempts, show an incorrect message in red and display the solution.
   - Clicking Reveal solution immediately shows the answer and disables further attempts.
5. Add puzzle data.
   - Create `/puzzles/puzzle-1.json` with a simple easy puzzle definition.
   - Load the puzzle data from JavaScript in `puzzles.html`; use the JSON file as the source of truth for the test puzzle.
   - Implement a fallback inline object if JSON fetch is unavailable.
6. Keep the implementation self-contained and static.
   - No backend needed.
   - Use the same `Chess.js` board rendering and a minimal puzzle solve controller.

**Relevant files**
- `index.html` — update the sidebar `Puzzles` navigation.
- `puzzles.html` — new standalone page with same sidebar, puzzle grid, board, and feedback box.
- `puzzles/puzzle-1.json` — test puzzle data.

**Verification**
1. Open `index.html` and click `Puzzles`; it should navigate to `puzzles.html`.
2. On `puzzles.html`, confirm the sidebar matches the style and `New match` returns to `index.html`.
3. Confirm the puzzle grid displays at least one card, then clicking it loads the board and puzzle state.
4. Select wrong moves and verify the message changes to `Not quite. Try again`, then after 3 wrong attempts it becomes `Incorrect. Here's the solution` and reveals the answer.
5. Confirm `Reveal solution` works immediately and highlights the correct solution.

**Decisions**
- `puzzles.html` will be standalone but linked from `index.html`.
- The puzzle data will live in `/puzzles/puzzle-1.json` and be loaded into the page.
- The page will use a single-click puzzle selection flow rather than an always-visible full library.

**Further considerations**
1. If the app is ever served without a local web server, `fetch` from JSON may not work; include an inline fallback object to guarantee the page still works.
2. The board should reuse existing style concepts but can be simplified to avoid reusing every piece of `index.html` JS.
3. The sidebar can keep the same CSS and layout but does not need every button fully functional beyond navigation back to `index.html` and the current page highlight.