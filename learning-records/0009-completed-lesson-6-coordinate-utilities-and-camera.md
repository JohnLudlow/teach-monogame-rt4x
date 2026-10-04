# Completed Lesson 6 — coordinate utilities, camera, and Game1 refactor

The learner completed the full Lesson 6 refactor, replacing the inline mouse-to-cell math
in <code>Game1</code> with reusable, unit-tested classes.

## Retrieval check (all correct)

- **Who owns the view matrix / who turns world→cell?** <code>Camera</code> owns the transform;
  <code>Transforms.WorldToGrid</code> does world→cell, with convenience wrappers on <code>Grid</code>. ✓
- **Why a dirty flag on <code>Camera.Transform</code>?** Avoids recomputing the scale/translate
  matrices when nothing changed; <code>_dirty</code> tracks whether a rebuild is needed. ✓
- **What does <code>ScreenToGrid</code> return off-grid, and why useful?** <code>null</code>, usable as an
  in-bounds check — learner explicitly noted this *assumes null has only one meaning*, spotting
  the overloaded-null smell (future fix: <code>TryScreenToGrid(out Point)</code> or a result type). ✓

## What was built (subject repo)

- <code>Core/Utilities/Transforms.cs</code> — static conversions: ScreenToWorld, WorldToScreen,
  WorldToGrid (Math.Floor), GridToWorld (cell centre), and learner-added GridToWorldRect
  (corner-anchored cell bounds for drawing/hit-testing).
- <code>Core/Entities/Camera.cs</code> — Position/Zoom with lazy dirty-flagged Transform
  (CreateScale * CreateTranslation), Zoom clamped [0.1, 5], Pan helper. Learner initially added
  INotifyPropertyChanged, then removed it as scope creep (may add elsewhere later).
- <code>Core/Entities/Grid.cs</code> — WorldToGrid/GridToWorld/GridToWorldRect wrappers,
  IsValidGridPosition (half-open bounds), ScreenToGrid returning Point?. Grid moved into
  Core.Entities namespace (also cleared the CA1050 warning).
- <code>Game1.cs</code> — inline math + buggy bounds check deleted; hovered cell now
  <code>_grid.ScreenToGrid(mousePos, _camera.Transform)</code>; highlight drawn via GridToWorldRect.

## Verification

- 43 unit tests pass (Transforms 19, Camera 9, Grid 15) covering conversions, negatives/floor,
  half-open boundaries, round-trip, camera dirty-flag + clamp, ScreenToGrid null-when-off-grid,
  and a camera-transformed pick. Core + tests are warning-clean under AnalysisMode=All.
- <code>Game1</code> builds (0 errors). Runtime highlight is a manual visual check (needs a display).

## Design insights / architecture notes for later

- Learner is following an ECS direction; deliberately kept Camera in Entities (a camera is an
  entity under ECS) and Transforms in Utilities (free functions). Future: Camera data vs
  transform-building may split into component + system.
- Overloaded-null in ScreenToGrid: fine today (one failure reason), revisit if a second appears.
- Pre-existing tech debt to address later (not Lesson 6): CA2213 undisposed IDisposable fields in
  Game1 (Texture2D/SpriteBatch/GraphicsDeviceManager); NU1903 vulnerable transitive deps in
  ContentBuilder; CA1724/CA1050 on the ContentBuilder <code>Builder</code> type.

## Next

- Manual run to confirm the highlight tracks the mouse and clears off-grid.
- The coordinate-systems arc (Lessons 4–6) is complete. Natural next lesson: Camera controls
  (WASD pan, wheel zoom) — the "Coming soon" card the index/Lesson 6 already point to.
