# Completed Lesson 4 — hovered-cell picking with inline math

The learner completed Lesson 4, implementing mouse-to-cell picking in screen space with
inline conversion math in <code>Game1</code>, and highlighting the hovered cell.

## Retrieval check (both correct)

- **What is subtracted from the mouse position before dividing by <code>CellSize</code>?**
  Grid origin x and y. ✓
- **Where is hovered-cell state updated?** In <code>Update</code>; <code>Draw</code> renders
  based on that state. ✓ The learner restated the Update/Draw split cleanly.

## Key insights confirmed

- The Update/Draw separation (from Lesson 1) is holding as a durable mental model across
  lessons — the learner reached for it unprompted.
- Screen-space picking is understood as: subtract origin, divide by cell size, bounds-check.

## Zone of proximal development / next

- The inline math now lives in <code>Game1</code> exactly as Lesson 4 intended — the deliberate
  "before" state. This is the setup for the coordinate-systems arc.
- Next: Lesson 5 (Understand coordinate systems) — theory-only, builds the vocabulary and
  the traps (Math.Floor for negatives, invert-not-transpose, Screen→World→Grid chain).
- Then Lesson 6 (Build coordinate utilities and camera) — refactor the inline math into
  <code>Transforms</code>, <code>Camera</code>, and <code>Grid</code> methods.
