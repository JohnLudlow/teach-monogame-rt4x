# Completed Lesson 9 — place a settlement on a tile

The learner completed the first durable world-interaction vertical slice: left-clicking a
map tile creates one gold settlement marker that remains attached to its tile through camera
pan and zoom. This advances the mission from a navigable grid to a world where player input
creates validated, persistent RT4X state.

## Retrieval check (all correct)

- **Which coordinate system should a stored settlement use?** Grid coordinates. The cell is
  stable while camera position and zoom change; rendering derives world geometry from it.
- **What turns a held button into one placement command?** A current/previous state edge check:
  <code>isPlaceButtonDown &amp;&amp; !_wasPlaceButtonDown</code>.
- **Why does the placement controller own Screen → Grid?** It is the boundary adapter between
  input and world state. It has the command's screen position plus the <code>Camera</code> and
  <code>Grid</code> necessary to resolve the interaction. <code>InputReader</code> stays
  world-agnostic; the placement system stays input- and camera-agnostic.

## What was built (subject repo)

- <code>Core/Commands/PlaceSettlementAtScreenCommand.cs</code> — an input command carrying the
  pointed screen position until it can be resolved at the world boundary.
- <code>Core/Entities/Settlement.cs</code> — an immutable settlement identity stored at a
  <code>Point Cell</code>.
- <code>Core/Systems/SettlementPlacementSystem.cs</code> — owns settlement state in a
  <code>Dictionary&lt;Point, Settlement&gt;</code>. <code>TryPlace</code> rejects off-grid cells
  and uses <code>TryAdd</code> to preserve the one-settlement-per-cell invariant.
- <code>Core/Systems/World/SettlementPlacementController.cs</code> — resolves placement commands
  through <code>Grid.ScreenToGrid(screenPosition, camera.Transform)</code> and invokes the
  world rule only for valid cells.
- <code>InputReader</code> — records the previous left-button state and emits exactly one
  <code>PlaceSettlementAtScreenCommand</code> for a press edge, never every frame while held.
- <code>Game1</code> — routes the command stream to the camera controller before the placement
  controller, renders gold square markers from <code>GridToWorldRect(settlement.Cell)</code>,
  and keeps them in the camera-transformed world sprite batch.

## Tests and verification

Meaningful automated coverage now includes:

- empty in-bounds placement adds the expected settlement;
- duplicate placement is rejected while preserving one original settlement;
- off-grid placement changes no state;
- a panned and zoomed screen point resolves to the expected grid cell;
- holding left click over consecutive frames emits one placement command only.

- <code>dotnet build monogame-rt4x.slnx --no-restore</code> succeeded with 0 errors. It reports
  pre-existing analyser warnings in the Content Builder and undisposed MonoGame graphics fields.
- The full test output reported 50 passed, 0 failed, 0 skipped. The targeted input-edge test
  output reported 1 passed, 0 failed, 0 skipped.
- Both <code>dotnet test</code> invocations returned process exit code 1 despite their successful
  test summaries and no diagnostic output. Treat this as a test-runner/tooling anomaly to
  investigate before relying on the exit code in automation; do not misclassify the test itself
  as failed.
- Visual behaviour (one gold marker per clicked valid tile, attached through pan/zoom) remains a
  manual runtime confirmation performed by the learner.

## Design insight to carry forward

The stored game state should be in the domain's stable coordinate system, while presentation
coordinates are derived at the boundary. The command can carry screen coordinates briefly,
but it must be resolved through the current camera transform before the domain rule runs. This
keeps keyboard/mouse input, camera mathematics, occupancy rules, and rendering independently
testable and prevents screen-space state from leaking into the simulation.

## Next opportunities

- Select an existing settlement instead of always attempting placement.
- Add one simple placement rule based on terrain once terrain data exists.
- Investigate why successful <code>dotnet test</code> summaries return exit code 1 in this
  environment.
- Outstanding prior technical debt remains out of lesson scope: CA2213 disposal warnings in
  <code>Game1</code> and Content Builder analyser warnings.
