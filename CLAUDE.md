# ClashDeck - Claude Code Project Instructions

## 1. Project Overview

ClashDeck is a multiplayer, attribute-based card battle game featuring characters organized by genres, universes, and franchises.

The goal is to build a reliable, maintainable game with real-time multiplayer support.

Follow the project's documentation as the source of truth. Do not invent or silently change game rules.

## 2. Before Starting Any Task

Before making changes:

1. Read `README.md`.
2. Read `docs/CURRENT_STATUS.md`.
3. Read `docs/ROADMAP.md`.
4. Read `docs/GAME_RULES.md`.
5. Read `docs/ARCHITECTURE.md`.
6. Read `docs/DECISIONS.md`.
7. Read `docs/TESTING.md`.
8. Read relevant files under `docs/features/`.
9. Inspect the existing code, package files, and Git status.

Identify the current milestone and the next incomplete task.

Do not assume the documentation or code is up to date without inspecting it.

## 3. Technology Stack

### Frontend
- Next.js with App Router
- React
- TypeScript
- Tailwind CSS

### Game Server
- Node.js
- TypeScript
- Socket.IO

### Shared Packages
- `@clashdeck/shared`: shared types, schemas, and event contracts.
- `@clashdeck/game-engine`: pure game rules and battle logic.

### Planned Supporting Technologies
- PostgreSQL for persistent data
- Prisma for database access
- Zod for runtime validation
- Vitest for unit and integration tests

Do not introduce additional dependencies without a clear reason.

## 4. Project Structure

```text
clashdeck/
├── apps/
│   ├── web/
│   └── game-server/
├── packages/
│   ├── shared/
│   └── game-engine/
├── docs/
│   └── features/
├── data/
├── tests/
├── CLAUDE.md
├── README.md
└── package.json
```

Keep code in the appropriate application or package. Do not place all game logic inside frontend components or the server entry point.

## 5. Architecture Rules

### Game Engine
- Keep game rules independent of React and Socket.IO.
- Use deterministic, testable functions wherever possible.
- Keep card comparisons, round resolution, tie handling, and match completion in the game engine.
- Do not mix UI logic with game rules.

### Authoritative Server
- The server determines all game outcomes.
- Never trust clients to declare winners, change card ownership, choose unauthorized cards, or modify attributes.
- Validate every client action.
- Prevent invalid actions, duplicate submissions, and out-of-turn moves.
- Keep each match's state isolated from other matches.

### Shared Package
- Keep shared types and event contracts in `packages/shared`.
- Validate network input at runtime.
- Avoid duplicating shared definitions across the frontend and server.

### Card and Category System
- Store card data separately from UI code.
- Support genres, franchises/universes, and categories through data-driven definitions.
- Allow hosts to select eligible cards according to the documented game rules.
- Use globally consistent attribute ratings across universes.
- Do not dynamically rescale ratings according to the selected match category.

## 6. Game Rules

The currently planned game modes are:

1. **Stack Duel:** Players reveal their top cards and compare a selected attribute.
2. **Open-Hand Duel:** Players choose a card from their available hand and select an attribute.

Prioritize Stack Duel for the initial playable version unless the roadmap says otherwise.

Initial implementation should focus on:
- Card data model
- Global attributes and ratings
- Category and universe selection
- Deck creation and shuffling
- Round resolution
- Tie handling
- Card transfer
- Turn management
- Match completion
- Multiplayer synchronization

Special mechanics, including Ultimate, Fusion, Counter, and Attribute Switch, should be added only after the basic game works reliably.

If a rule is missing or ambiguous, explain the ambiguity and ask for a decision when it materially affects gameplay or architecture. Do not silently invent major rules.

## 7. Development Workflow

Work on **one milestone at a time**.

For each task:

1. Inspect the existing implementation.
2. Identify the task's scope and dependencies.
3. Present a short plan before significant changes.
4. Ask for approval when a major product or architecture decision is needed.
5. Implement the smallest complete solution.
6. Add or update tests.
7. Run relevant checks.
8. Fix regressions caused by the changes.
9. Update relevant documentation.
10. Update `docs/CURRENT_STATUS.md`.
11. Report the results and the next recommended task.

Do not ask for approval for every small implementation detail. Use reasonable defaults when the decision is minor and consistent with existing documentation.

Do not implement multiple unrelated milestones in one task.

## 8. Code Quality

- Use TypeScript types instead of `any` whenever practical.
- Prefer small, focused functions and clear names.
- Avoid unnecessary abstractions and duplicated logic.
- Handle errors explicitly.
- Validate untrusted input.
- Keep secrets and credentials out of source control.
- Use environment variables for configuration.
- Never hardcode production credentials.
- Follow existing formatting and naming conventions.
- Avoid unrelated refactoring.

Do not add placeholder implementations and describe them as complete functionality.

## 9. Testing and Verification

Use appropriate tests for each change.

- Unit-test game-engine logic.
- Test attribute comparisons and tie scenarios.
- Test invalid actions and turn order.
- Test deck and card ownership invariants.
- Test match completion and edge cases.
- Test server event handling and multiplayer synchronization.
- Run TypeScript checks, linting, tests, and builds where configured.

Never claim a command passed unless you actually ran it and verified the result.

If a check cannot run, report why and identify what remains unverified.

## 10. Documentation

Keep documentation synchronized with implementation.

Update relevant files when behavior or architecture changes:

- `docs/GAME_RULES.md`: gameplay rules.
- `docs/ARCHITECTURE.md`: system structure and responsibilities.
- `docs/ROADMAP.md`: milestones and planned work.
- `docs/DECISIONS.md`: significant technical decisions.
- `docs/CURRENT_STATUS.md`: completed work, current state, blockers, and next task.
- `docs/TESTING.md`: testing strategy and commands.
- `docs/features/`: detailed feature specifications.
- `README.md`: setup and usage instructions when necessary.

Document decisions that will matter in future sessions. Do not rely on conversation history alone.

## 11. Git Safety

- Inspect `git status` before editing.
- Preserve the user's existing changes.
- Do not discard, overwrite, or revert user changes.
- Do not run destructive Git commands without explicit authorization.
- Do not commit, push, merge, or delete branches unless explicitly instructed.
- Do not amend or rewrite existing commits without permission.
- Never include secrets in commits.

## 12. Copyright and Content

For public or commercial releases, use original or properly licensed character names, artwork, images, and other assets.

Prototype data may use clearly identified placeholders. Do not assume copyrighted artwork is free to use.

## 13. Communication Style

Keep responses concise and practical.

At the end of each task, report:

- **Completed:** What changed.
- **Files:** Which files were created or modified.
- **Checks:** Commands run and their actual results.
- **Remaining:** Known issues or incomplete work.
- **Next:** One recommended next task.

Do not claim a task is complete if essential functionality or verification is missing.

## 14. Main Objective

Build ClashDeck incrementally into a working multiplayer game.

Prioritize correctness, clear architecture, testable game logic, reliable synchronization, and maintainable documentation over adding features quickly.

Always continue from the actual repository state and the latest documented progress.