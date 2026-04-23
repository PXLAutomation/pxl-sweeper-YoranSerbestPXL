You are reviewing a REQUIREMENTS.md document for a small, single-page Minesweeper web app.

Your role is NOT to summarize or lightly edit. Your role is to rigorously audit, challenge, and improve the document so that it becomes precise, minimal, and implementation-ready.

---

## Review Objectives

You must evaluate the document across these dimensions:

### 1. Clarity & Precision
- Identify vague, ambiguous, or subjective language (e.g., "fast", "intuitive", "clean")
- Replace with concrete, testable statements
- Ensure every requirement can be verified

### 2. Consistency & Contradictions
- Detect conflicting requirements (explicit or implicit)
- Check alignment between sections (e.g., Interaction vs Functional Requirements)
- Highlight undefined behaviors or edge cases

### 3. Scope Control (CRITICAL)
- Identify any feature creep or unnecessary complexity
- Challenge anything that violates:
  - single-page constraint
  - static layout
  - minimal scope
- Suggest simplifications where possible

### 4. Completeness (without expansion)
- Identify missing *essential* details required for implementation
- Do NOT add features—only fill necessary gaps
- Pay special attention to:
  - edge cases (first click, win/loss states, invalid inputs)
  - interaction details (exact click behavior)
  - state transitions

### 5. Hidden Complexity
- Call out requirements that seem simple but are complex to implement
- Flag risky areas (e.g., board generation, mobile gestures, chording)
- Suggest safer alternatives if they reduce complexity

### 6. Testability
- For each requirement, ask: “How would I verify this works?”
- If unclear, rewrite it to be testable

---

## Output Format

### Part 1: Critical Issues
List the most important problems:
- Ambiguities
- Contradictions
- Scope risks
- Missing essential details

Be direct and specific.

---

### Part 2: Line-by-Line Improvements
- Rewrite problematic sections or sentences
- Replace vague wording with precise requirements
- Keep it minimal—no fluff

---

### Part 3: Simplification Opportunities
- Identify places where the design can be reduced in complexity
- Recommend removals or constraints

---

### Part 4: Edge Case Audit
Explicitly verify or define behavior for:
- First click
- Clicking flagged tiles
- Clicking revealed tiles
- Win condition
- Loss condition
- Restart behavior
- Rapid/multiple inputs

Add missing rules if needed.

---

### Part 5: Final Improved REQUIREMENTS.md
Produce a fully revised version that:
- Is shorter or equal in length
- Has higher precision
- Removes ambiguity
- Enforces constraints strictly

---

## Strict Rules

- Do NOT introduce new features
- Do NOT expand scope
- Prefer deletion over addition
- If something is unclear, resolve it decisively (do not leave it vague)
- Challenge weak decisions instead of accepting them

---

## Mindset

Act like this document will be handed to a developer who cannot ask questions.

If they would hesitate or guess, the document is not good enough.

Begin the review.

## Project Setup Requirements

- The project shall include a `package.json` file in the repository root.
- The `package.json` file shall define the project's runnable commands in a consistent way.
- The `package.json` file shall include at least a `test` script so the same test command can be run every time.
- If the project uses ES module imports in JavaScript, `package.json` shall set `"type": "module"`.
- The project shall remain compatible with a plain JavaScript, static-site workflow.