# MonoGame RT4X Resources

## Knowledge

- [MonoGame documentation](https://docs.monogame.net/)
  Official API and how-to documentation. Use for: framework lifecycle, graphics, input, audio, content, and deployment.
- [MonoGame: Content Builder Project](https://docs.monogame.net/articles/getting_started/content_pipeline/content_builder_project.html)
  Official guide for the required code-first content-pipeline setup. Use for: adding and building game assets without an MGCB config file.
- [MonoGame `SpriteBatch` API](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SpriteBatch.html)
  Official API reference. Use for: `Begin`/`End`, drawing textures into destination rectangles, and tinting simple 2D visuals such as grid lines.
- [MonoGame `Texture2D` API](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html)
  Official API reference. Use for: creating code-generated textures such as a reusable 1x1 white pixel and uploading data with `SetData`.
- [MonoGame `Mouse` API](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Mouse.html)
  Official API reference. Use for: sampling the current mouse position during `Update`.
- [MonoGame `MouseState` API](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.MouseState.html)
  Official API reference. Use for: reading cursor coordinates and button state when mapping input to grid cells.
- [MonoGame: Getting Started](https://docs.monogame.net/articles/getting_started/index.html)
  Official setup and first-project guidance. Use for: verifying the local toolchain and understanding the generated project.
- [Microsoft: .NET game development with MonoGame](https://learn.microsoft.com/en-us/dotnet/core/tutorials/top-level-templates#monogame)
  Microsoft-maintained orientation to available templates and tooling. Use for: .NET CLI project creation and troubleshooting.

## Wisdom (Communities)

- [MonoGame GitHub Discussions](https://github.com/MonoGame/MonoGame/discussions)
  Maintainer and practitioner discussion space. Use for: framework-specific design and tooling questions after reducing them to a reproducible example.
- [MonoGame Discord](https://discord.gg/monogame)
  Active community linked from MonoGame’s official channels. Use for: quick feedback and examples from experienced MonoGame developers.

## Gaps

- Choose trustworthy primary sources for terrain generation, pathfinding, and GOAP when those systems become the next lesson.
- Select trustworthy primary sources for click selection, camera transforms, and tile rendering as interaction deepens.
