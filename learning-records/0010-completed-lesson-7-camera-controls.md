# Completed Lesson 7 — camera controls (pan and zoom)

The learner completed Lesson 7, wiring keyboard panning and mouse-wheel zoom into the
camera built in Lesson 6, drawing the world through the camera transform, and confirming
the hovered-cell highlight stays correct through pan and zoom.

## Retrieval check (all correct)

- **Why multiply pan by <code>ElapsedGameTime.TotalSeconds</code>?** Frame timing isn't perfectly
  regular — 60 FPS doesn't mean Update/Draw are exactly 1/60s apart — so scaling by actual
  elapsed time ties movement to wall-clock time. (Sharper than the usual "different hardware"
  framing; learner reasoned from frame-to-frame variance.)
- **What is <code>ScrollWheelValue</code>?** A running total since game start; remember the previous
  value and subtract to get this frame's delta (and its direction).
- **Zoom-toward-cursor steps?** Cache world-under-cursor before zooming, apply the zoom, then
  pan by the difference between old and new world-under-cursor so the tile stays under the mouse.

## Notable

- Answer 1 showed strong systems reasoning (frame variance from GC/VSync/load), not rote recall.
- The shared-transform payoff landed: picking + drawing use one <code>_camera.Transform</code>, so the
  highlight tracks correctly during pan/zoom.

## State of the interaction loop

The subject game now has a controllable camera (WASD/arrow pan, wheel zoom, zoom-to-cursor,
frame-rate independent) over a pickable grid — the core strategy-game interaction loop.

## Next options (offered at end of Lesson 7)

- Clamp the camera to the map edges (uses existing Grid bounds + GridToWorld).
- Render culling: draw only visible cells (ScreenToWorld on viewport corners).
- Place/select something on a tile (start of unit/building interaction).
- Also outstanding tech debt (not lesson work): CA2213 undisposed IDisposable fields in Game1.
