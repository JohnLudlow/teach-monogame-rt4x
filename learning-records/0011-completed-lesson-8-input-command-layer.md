# Completed Lesson 8 — input command layer and drag-panning

The learner completed Lesson 8: lifting input out of <code>Game1</code> into a device-agnostic
command layer, adding middle-mouse drag-panning, and keeping the camera untouched by device
specifics.

## Retrieval check (all correct)

- **Why can drag reuse the camera code?** Handling is separated into the command system,
  distinct from both input handlers and camera; both devices emit the same PanCommand.
- **Why divide the drag delta by zoom?** So movement feels consistent (not fast when zoomed in).
  Sharpened in discussion: the precise invariant is that the grabbed world point stays under the
  cursor — at 2× zoom one world unit spans two screen pixels, so an N-pixel drag is N/2 world units.
- **Why is InputReader testable?** It isn't tied to camera or device singletons; it just appends
  command objects to a list based on the parameters passed — a pure function returning data.

## Final architecture (four-folder ECS-role split; learner-driven)

Over the design conversation the learner refined the layout, ending on a clean ECS-role split:

- <code>Core/Entities/</code> — identities (Camera).
- <code>Core/Systems/</code> — behaviour (InputReader, CameraController under Systems/Input).
- <code>Core/Components/</code> — data attached to entities (InputBindings under Components/Input).
- <code>Core/Commands/</code> — transient intents (InputCommand + PanCommand/ZoomCommand records).

Notable reasoning during design:
- Chose a command/intent layer over direct control ("I'd just need to change it again later").
- Correctly identified CameraController as a *system*, not an entity, distinguishing pure ECS
  from Godot/Unity node/MonoBehaviour fusion where it would be an entity/node.
- Drove the 4th folder (Commands) to fix the category error of filing a command under Components.
- Middle-mouse drag referenced via a binding (DragButton enum) so it is configurable later.
- Rebinding designed-for but not implemented (no config file/UI yet) — deliberate scope line.

## State

Subject game: rebinding-ready input command layer feeding a CameraController over a pickable,
pan/zoom/drag camera. Lesson 7's inline input is now the intentional "before" that Lesson 8 refactors.

## Next options (offered)

- Load InputBindings from config (the rebinding designed for).
- Add SelectCellCommand so clicking a tile does something (one new switch case).
- Clamp camera to map edges; render culling.
- Outstanding tech debt (not lesson work): CA2213 undisposed IDisposable fields in Game1.
