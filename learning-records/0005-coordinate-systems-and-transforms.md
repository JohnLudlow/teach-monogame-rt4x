# Coordinate Systems and Transforms

Coordinate translation utilities have been implemented in the subject repository. The learner has built a `Transforms` class with methods for converting between screen, world, and grid coordinates, plus a `Camera` class for managing the view transform.

The lesson focused on understanding the five coordinate systems (Input, Screen, World, Grid, Local), the relationship between them, and the mathematics of transform matrices.

## Key insights

- Coordinate conversions are the foundation for camera systems, input handling, and spatial logic
- Matrix order matters: scale then translate for camera transforms
- Screen-to-grid conversions require: screen → world → grid (two steps)
- World-to-grid: subtract origin, divide by cell size (truncate for integer grid coordinates)
- Grid-to-world: multiply by cell size, add origin

## Open questions / fog of war

- Should the coordinate utilities be static methods or extension methods?
- How should sub-pixel precision be handled (Vector2 vs Point)?
- Should the Camera class be integrated with the Grid class, or kept separate?

## Files created

- `FourxGame.MonoGame.Core/Transforms.cs` — coordinate conversion utilities
- `FourxGame.MonoGame.Core/Camera.cs` — camera transform management

## Next steps

- Integrate coordinate utilities with the existing Grid class
- Add unit tests for coordinate conversions
- Update the highlight-hovered-cell feature to use world coordinates