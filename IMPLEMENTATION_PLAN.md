Overview

This plan outlines the implementation for the PXL Sweeper browser game as a static single-page web app. It organizes the work into dependency-ordered phases that each produce a reviewable milestone, from initial project scaffolding through playable game behavior and final stabilization.

Assumptions

- The project is a single-page browser-based Minesweeper-style game built as a static web app.
- `REQUIREMENTS.md` and `GEMINI.md` are the only available project documents today.
- The implementation will use an npm-compatible workflow with a root `package.json` and commands such as `npm test`, `npm run lint`, and `npm run build`.
- Deployment target is static hosting / local browser preview.
- Risk tolerance is medium: deliver the core game with basic quality checks and no unnecessary features.

Delivery strategy

- Hybrid: start with a small infrastructure slice, then deliver the game as vertical feature slices.
- Justification: the static site build and npm workflow are needed before game logic and UI can be implemented, but subsequent work should still be shipped as thin, reviewable increments.
- This fits a course-style review cadence by keeping each phase small, concrete, and independently verifiable.

Phase list

- Phase 1: Establish static app scaffold and npm validation baseline
- Phase 2: Implement Minesweeper board generation and rule engine
- Phase 3: Build the browser UI and tile interaction layer
- Phase 4: Add game state control, win/loss handling, and restart flow
- Phase 5: Stabilize tests, docs, and release readiness

Detailed phases

Phase 1: Establish static app scaffold and npm validation baseline

Goal

Create the minimal static web app structure and dependency harness so the project has a reproducible build and test baseline.

Scope

- Add `package.json` with scripts for test, lint, and build.
- Add `index.html`, core stylesheet, and starter JavaScript entrypoint.
- Add baseline project metadata and any minimal tooling config required for the chosen workflow.

Expected files to change

- `package.json`
- `index.html`
- `src/index.js` or `src/app.js`
- `src/styles.css`
- `REQUIREMENTS.md` if necessary to confirm implementation assumptions
- `TODO.md`

Dependencies

- No implementation dependency beyond current docs.
- Depends on project acceptance of npm-based static site workflow.

Risks

- Low: this phase is scaffolding only.
- Risk arises if the chosen build/test tooling does not match course expectations or team conventions.

Tests and checks to run

- `npm test` (or placeholder `npm run test` if test command is configured)
- `npm run lint` if linting is configured
- `npm run build` or local static page verification

Review check before moving work to `DONE.md`

- Confirm `package.json` exists and defines at least `test`, `lint`, and `build` scripts.
- Confirm `index.html` loads the starter app entrypoint in a browser or local preview.
- Confirm `TODO.md` has phase-specific items for the next work slice.
- Confirm no feature work beyond scaffold is included.

Exact `TODO.md` entries to refresh from this phase

- [ ] Create `package.json` with npm scripts for test, lint, and build.
- [ ] Add `index.html`, base stylesheet, and app entrypoint file.
- [ ] Verify the app scaffold loads in a browser or local preview.

Exit criteria for moving items to `DONE.md`

- `package.json` contains runnable commands and is committed.
- A browser preview of `index.html` successfully loads the starter app entrypoint.
- `TODO.md` is updated with the next phase tasks.

Phase 2: Implement Minesweeper board generation and rule engine

Goal

Deliver the core game model: board layout, mine placement, neighbor counts, reveal propagation, flagging, and win/loss determination.

Scope

- Implement board generation with a default grid size and mine density.
- Implement safe reveal behavior, including recursive reveals for zero-adjacent-mine cells.
- Implement cell flagging and board status checks for win/loss.
- Add unit tests for game logic behaviors.

Expected files to change

- `src/game.js`, `src/board.js`, or equivalent game engine module(s)
- `tests/game.test.js` or `src/game.test.js`
- `package.json` if test dependencies are added
- `README.md` or `REQUIREMENTS.md` only if acceptance details change
- `TODO.md`

Dependencies

- Phase 1 must be complete.
- Requires agreed default game parameters if not defined in requirements.

Risks

- Medium: board generation and reveal logic are the most error-prone parts of the game.
- Main failure modes: incorrect neighbor counts, infinite recursion on reveal, incorrect win/loss state.

Tests and checks to run

- `npm test` targeting the game engine unit tests
- `npm run lint`
- `npm run build` if build tooling bundles the module

Review check before moving work to `DONE.md`

- Confirm unit tests cover mine placement, reveal propagation, flagging, and win/loss detection.
- Confirm game engine behavior matches the expected Minesweeper rules in `REQUIREMENTS.md`.
- Confirm the implementation is isolated from UI concerns.
- Confirm `TODO.md` contains the next phase tasks.

Exact `TODO.md` entries to refresh from this phase

- [ ] Implement board generation and mine adjacency rules in a game engine module.
- [ ] Add unit tests for reveal propagation, flagging, and win/loss state.
- [ ] Verify the game engine passes all unit tests.

Exit criteria for moving items to `DONE.md`

- Game engine module exists and implements core Minesweeper rules.
- Unit tests pass and cover the major game engine behaviors.
- `TODO.md` is updated for UI integration.

Phase 3: Build the browser UI and tile interaction layer

Goal

Connect the game engine to the browser UI so users can reveal tiles and flag mines on a playable board.

Scope

- Render the board as a grid of clickable elements.
- Implement left-click reveal and right-click or alternate interaction flag toggling.
- Display tile states: hidden, revealed number, empty, flagged, mine on loss.
- Keep the game loop disabled until Phase 4 finalizes state transitions.

Expected files to change

- `src/ui.js`, `src/app.js`, or equivalent UI module(s)
- `index.html` for board container markup
- `src/styles.css`
- `tests/ui.test.js` or browser interaction tests if available
- `TODO.md`

Dependencies

- Phase 1 and Phase 2 must be complete.
- Requires basic HTML/CSS structure from Phase 1.

Risks

- Medium: UI interaction is sensitive to event handling and accessibility behavior.
- Main failure modes: click handlers not matching expected actions, broken board rendering, conflicting right-click behavior.

Tests and checks to run

- `npm test` including any UI interaction tests
- `npm run lint`
- manual browser check of reveal and flag interaction
- `npm run build`

Review check before moving work to `DONE.md`

- Confirm the browser renders a board grid and user interactions reveal and flag cells.
- Confirm hidden tiles remain hidden until revealed and flagged tiles visually differ.
- Confirm the board UI uses a single-page static interaction without page reloads.
- Confirm `TODO.md` contains the next phase tasks.

Exact `TODO.md` entries to refresh from this phase

- [ ] Render the game board in the browser from the game engine state.
- [ ] Implement tile reveal and flag interactions in the UI.
- [ ] Verify board rendering and tile interactions manually in a browser.

Exit criteria for moving items to `DONE.md`

- The UI renders the board and supports reveal and flag actions.
- Manual browser verification shows tile states update correctly.
- `TODO.md` is updated for game state control polish.

Phase 4: Add game state control, win/loss handling, and restart flow

Goal

Complete the playable game loop by handling game status, end conditions, and restart controls.

Scope

- Display game status: playing, won, lost.
- Lock the board after win or loss.
- Reveal all mines on loss and preserve flagged tiles.
- Add a restart/new game control.
- Implement any required game status messaging in the UI.

Expected files to change

- `src/ui.js` or `src/app.js`
- `src/game.js` or `src/board.js` if status APIs are extended
- `index.html`
- `src/styles.css`
- `tests/game.test.js`, `tests/ui.test.js`
- `TODO.md`

Dependencies

- Phase 1, Phase 2, and Phase 3 must be complete.
- Requires a working board UI and game engine.

Risks

- Medium: state transitions can expose edge cases from earlier phases.
- Main failure modes: game not locking after end, incorrect win conditions, restart leaving stale state.

Tests and checks to run

- `npm test` including end-condition tests
- `npm run lint`
- manual browser check of win, loss, and restart behavior
- `npm run build`

Review check before moving work to `DONE.md`

- Confirm the game reports win/loss correctly and prevents further board interaction after end.
- Confirm restart resets the board and status cleanly.
- Confirm loss reveals mines and flags remain visible if expected.
- Confirm `TODO.md` contains the final stabilization tasks.

Exact `TODO.md` entries to refresh from this phase

- [ ] Implement win/loss detection and board lockout after game end.
- [ ] Add restart/new game control and verify it resets all game state.
- [ ] Verify win, loss, and restart behavior manually in a browser.

Exit criteria for moving items to `DONE.md`

- Game status transitions work correctly and end games are handled.
- Restart creates a fresh new board state.
- `TODO.md` is updated for the stabilization phase.

Phase 5: Stabilize tests, docs, and release readiness

Goal

Finalize the project with a stable build, updated documentation, and clear release readiness for static hosting.

Scope

- Add or update project documentation and README references.
- Run full test, lint, and build verification.
- Confirm the static app can be served locally or deployed as-is.
- Review and close out any remaining `TODO.md` entries.

Expected files to change

- `README.md` or `REQUIREMENTS.md` if needed
- `IMPLEMENTATION_PLAN.md`
- `TODO.md`
- `DONE.md`
- `package.json` if build/test scripts are adjusted
- optional `docs/` if project convention requires it

Dependencies

- Phases 1 through 4 must be complete.

Risks

- Low to medium: leftover issues are usually integration or documentation gaps.
- Main failure mode: missing release documentation or incomplete verification.

Tests and checks to run

- `npm test`
- `npm run lint`
- `npm run build`
- manual browser smoke test of the final app

Review check before moving work to `DONE.md`

- Confirm all phase TODO items are either complete or explicitly carried forward in `TODO.md`.
- Confirm documentation reflects how to run, test, and preview the app.
- Confirm final build succeeds and the static app loads in a browser.
- Confirm the final diff is focused on project completion, not new feature work.

Exact `TODO.md` entries to refresh from this phase

- [ ] Run full test, lint, and build verification for the final app.
- [ ] Update project documentation with run/build instructions.
- [ ] Confirm `TODO.md` and `DONE.md` accurately reflect completed work.

Exit criteria for moving items to `DONE.md`

- The final app builds cleanly and passes all configured checks.
- Documentation is present and matches the implemented project.
- `TODO.md` and `DONE.md` are synchronized with the final implementation.

Dependency notes

- Phase 1 is the foundational scaffold and must be complete before any implementation phase begins.
- Phase 2 depends on the static project baseline from Phase 1.
- Phase 3 depends on the game engine from Phase 2.
- Phase 4 depends on both UI interactions from Phase 3 and the game model from Phase 2.
- Phase 5 depends on completion of all prior phases and focuses on stability and release readiness.

Review policy

- Expect each phase to remain small enough for one review cycle; diffs should generally be limited to one feature slice or one coherent module.
- If a phase proposal exceeds roughly 250 lines of implementation or changes more than three core modules, split it into smaller phases before implementation.
- Oversized phases are not allowed to proceed unchanged; they must be re-planned into smaller reviewable increments.
- Review must verify requirement traceability, scope containment, regression risk, and documentation updates.

Definition of done for the plan

- The game is implemented as a static single-page browser app that meets the core Minesweeper-style requirements.
- The project includes a working `package.json` with build, test, and lint scripts.
- The app passes configured automated checks and manual browser smoke tests.
- `TODO.md` and `DONE.md` reflect the completed work and remaining tasks accurately.
- Implementation and usage documentation are available and up to date.

Open questions

- Should the game support multiple difficulty levels or only a single default board size for this course project?
- Which exact npm command names are expected by the course workflow (`test`, `lint`, `build`, etc.)?
- Does the course require a hosted deployment preview, or is local static preview sufficient?
- Are there any specific accessibility or browser compatibility requirements not documented in `REQUIREMENTS.md`?
