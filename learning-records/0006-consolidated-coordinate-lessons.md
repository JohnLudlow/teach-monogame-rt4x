# Consolidated the coordinate-systems lessons (4–6)

Lessons 4, 5, and 6 all covered aspects of coordinate conversion but contradicted
each other in style and substance. They were reorganized into a single coherent arc
with a consistent format, a table of contents, a series map, and prev/next navigation.

This is a reorganization record (akin to an ADR): it captures the canonical decisions
made to remove the contradictions, so future lessons stay consistent with them.

## What was wrong

- **Inconsistent format.** Lesson 5 put the lesson number in its `<h1>`; Lesson 6 did
  not. Kickers, titles, and footers diverged. No lesson had a table of contents or
  prev/next navigation.
- **Contradictory implementations.** Old Lesson 5 used `Grid.Width`/`Height`/`CellSize`
  and `(int)` truncation with `Matrix.CreateTranslation(-Position)` plus an explicit
  `UpdateTransform()`. Old Lesson 6 used `GridSizeX`/`GridSizeY`/`GridCellSize`,
  `Math.Floor`, `CreateTranslation(+Position)`, and a lazy `Transform` getter.
- **Old Lesson 6 called out earlier lessons** for doing inline conversions rather than
  using a utility class, but the lessons it criticized were never framed to lead into it.

## Canonical decisions (adhere to these going forward)

- **Grid fields:** `Origin` (`Vector2`), `GridCellSize`, `GridSizeX`, `GridSizeY`
  (`int`). These match the real `FourxGame.MonoGame.Core/Entities/Grid.cs`.
- **World → Grid uses `Math.Floor`**, not an `(int)` cast, so negative world
  coordinates map to the correct cell instead of collapsing across the origin.
- **Camera** owns a lazily-evaluated `Transform` getter guarded by a dirty flag; setters
  for `Position`/`Zoom` mark it dirty. `Transform` is read-only from outside.
- **Camera transform order:** `Matrix.CreateScale(Zoom) * Matrix.CreateTranslation(Position.X, Position.Y, 0)`
  — scale first, then translate.
- **`Grid.ScreenToGrid` returns `Point?`** — `null` means off-grid, folding the bounds
  check into the conversion.
- **Screen → Grid is always Screen → World → Grid** (no direct step).

## New lesson arc

- **Lesson 4 — Highlight the hovered cell** (skill, screen-space, inline math). Now
  framed as the intentional "before" state: you feel the pain of inline conversion first.
- **Lesson 5 — Understand coordinate systems** (knowledge, theory-only). The five spaces,
  transform matrices, the conversion chain, and the traps — grounded in the reference doc.
- **Lesson 6 — Build coordinate utilities and camera** (skill, the refactor). One canonical
  implementation that lifts Lesson 4's math into `Transforms`, `Camera`, and `Grid`
  methods, and explicitly replaces the inline version.

## Files changed

- `docs/assets/course.css` — added `.toc`, `.series`, and `.lesson-nav` chrome shared by all lessons.
- `docs/lessons/0004-highlight-the-hovered-cell.html` — reformatted; reframed inline math.
- `docs/lessons/0005-understand-coordinate-systems.html` — new knowledge lesson (replaces
  `0005-implement-coordinate-translation-utilities.html`, deleted).
- `docs/lessons/0006-build-coordinate-utilities-and-camera.html` — new canonical skill lesson
  (replaces `0006-integrate-coordinate-utilities-and-camera.html`, deleted).
- `docs/reference/coordinate-systems-and-transforms.html` — aligned to the canonical decisions.

## Next steps

- Learner works through Lessons 4 → 5 → 6 and implements `Transforms.cs` and `Camera.cs`
  in the subject repo (they do not yet exist there).
- Add round-trip unit tests (`WorldToGrid(GridToWorld(cell)) == cell`) in
  `FourxGame.MonoGame.UnitTests`.
- Author the "Camera controls" lesson (WASD pan, wheel zoom) that Lesson 6 links forward to.
