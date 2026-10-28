# Completed Lesson 6 — coordinate utilities, camera, and Game1 refactor

The learner completed the full Lesson 6 refactor, replacing the inline mouse-to-cell math in `Game1`
with reusable, unit-tested classes.

## Retrieval check (all correct)

- **Who owns the view matrix / who turns world→cell?** `Camera` owns the transform;
  `Transforms.WorldToGrid` does world→cell, with convenience wrappers on `Grid`. ✓
- **Why a dirty flag on `Camera.Transform`?** Avoids recomputing the scale/translate matrices when
  nothing changed; `_dirty` tracks whether a rebuild is needed. ✓
- **What does `ScreenToGrid` return off-grid, and why useful?** `null`, usable as an in-bounds check
  — learner explicitly noted this _assumes null has only one meaning_, spotting the overloaded-null
  smell (future fix: `TryScreenToGrid(out Point)` or a result type). ✓

## What was built (subject repo)

- `Core/Utilities/Transforms.cs` — static conversions: ScreenToWorld, WorldToScreen, WorldToGrid
  (Math.Floor), GridToWorld (cell centre), and learner-added GridToWorldRect (corner-anchored cell
  bounds for drawing/hit-testing).
- `Core/Entities/Camera.cs` — Position/Zoom with lazy dirty-flagged Transform (CreateScale *
  CreateTranslation), Zoom clamped [0.1, 5], Pan helper. Learner initially added
  INotifyPropertyChanged, then removed it as scope creep (may add elsewhere later).
- `Core/Entities/Grid.cs` — WorldToGrid/GridToWorld/GridToWorldRect wrappers, IsValidGridPosition
  (half-open bounds), ScreenToGrid returning Point?. Grid moved into Core.Entities namespace (also
  cleared the CA1050 warning).
- `Game1.cs` — inline math + buggy bounds check deleted; hovered cell now
  `_grid.ScreenToGrid(mousePos, _camera.Transform)`; highlight drawn via GridToWorldRect.

## Verification

- 43 unit tests pass (Transforms 19, Camera 9, Grid 15) covering conversions, negatives/floor,
  half-open boundaries, round-trip, camera dirty-flag + clamp, ScreenToGrid null-when-off-grid, and
  a camera-transformed pick. Core + tests are warning-clean under AnalysisMode=All.
- `Game1` builds (0 errors). Runtime highlight is a manual visual check (needs a display).

## Design insights / architecture notes for later

- Learner is following an ECS direction; deliberately kept Camera in Entities (a camera is an entity
  under ECS) and Transforms in Utilities (free functions). Future: Camera data vs transform-building
  may split into component + system.
- Overloaded-null in ScreenToGrid: fine today (one failure reason), revisit if a second appears.
- Pre-existing tech debt to address later (not Lesson 6): CA2213 undisposed IDisposable fields in
  Game1 (Texture2D/SpriteBatch/GraphicsDeviceManager); NU1903 vulnerable transitive deps in
  ContentBuilder; CA1724/CA1050 on the ContentBuilder `Builder` type.

## Next

- Manual run to confirm the highlight tracks the mouse and clears off-grid.
- The coordinate-systems arc (Lessons 4–6) is complete. Natural next lesson: Camera controls (WASD
  pan, wheel zoom) — the "Coming soon" card the index/Lesson 6 already point to.
