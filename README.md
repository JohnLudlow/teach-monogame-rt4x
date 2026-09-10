# Teaching me how to make a 4x game in monogame

This is a "teach" repository for the `monogame-rt4x` repository. It uses the [mattpocock / teach](https://github.com/mattpocock/skills/blob/main/skills/productivity/teach/SKILL.md)
skill, along with other skills from [JohnLudlow/agents](https://github.com/JohnLudlow/agents) to help me learn all the skills necessary to create such a game.

## Terms used in this repository

| Term          | Meaning                                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| teach repo    | a repo using the `teach` skill and containing related resources to learn how to develop a `subject` repo                            |
| subject repo  | a repo containing the results of the teaching, usually a submodule of the related teach repo                                        |
| agent         | any AI agent of any kind acting in any repo, always subject to `./AGENTS.md`, `./CONTRIBUTING.md` and other guidance                |
| teach agent   | an agent acting in the ***teach repository*** using the ***teach skill***, or any (sub)agent acting on a ***teach agent***'s behalf |
| user          | ambiguous - can mean a user of the AI, but could also mean player when taking about matters such as game user interface             |
| player        | a person playing the game being developed in the subject repo                                                                       |
| 4x            | eXplore, eXpand, eXploit, eXterminate                                                                                               |
| realtime      | continuous play (not turn-based). May include time controls and active pause                                                        |
| time controls | controls that allow the player to control how fast the game runs, speeding through slower parts and slowing or pausing when needed  |
| active pause  | pause the game but allowing the player to continue to interact with the game, including giving instructions                         |

## What are we learning?

We are learning how to make videogames, in particular (in this case) a fantasy real-time 4x game using MonoGame (v3.8.5+).

### What is a real-time 4x?

A real-time 4x (RT4X) game is a game that combines real-time (with variable time controls) mechanics with 4x / empire building mechanics. Examples include Stellaris (scifi 4X) and Songs of Syx (fantasy city-builder with empire mechanics).

- Realtime means extended events (such as sieges) happen continuously, rather than being boxed into turns. An extended battle or siege could be interrupted by a relief army, for example
- Time controls allow players to control the speed of the game - speeding up to get through slow parts and slowing down or even pausing when more attention is needed
- Typical 4x mechanics
  - Exploration
  - City management
  - Resource management
  - Diplomacy
  - Army management and combat
  - Research (technologies and civics)
- Original fantasy setting with custom races

### 2D or 3D?

We can do some experiments in different ways.

- 2D topdown
- 3D with a fixed camera
- 3D with a tilting camera

Some givens:

- I want simple lo-fi graphics. Lo-poly if 3D or pixelart if 2D

- I want underground cities (a la Moria/Khazad-dum) as a mechanic so underground.
  Games like Dwarf Fortress achieve this via z-levels, while games like Age Of Wonders
  4 achieve it by having an underground layer. Teach me about both strategies

### What needs to be taught?

- Getting the game running
- Generating terrain

### Any reference games to think about?

- Kohan
  - Army management mechanics

- Songs of Syx
  - Visual style

- Dwarf Fortress
  - 3D terrain manipulation / Z-levels

- Age of Wonders 4
  - Faction customisation

## What's our tech stack? Why?

- Monogame 3.8.5+
  - Considered Monogame, Stride, Raylib. Monogame is mature and well-featured, and 3.8.5 introduces important fixes
  - The `GameEngineAdapter` project is plodding along, but I wanted to actually do something and wanted to see how this g oes.
- .NET 10
  - I like it

## Any constraints?

- Content management is performed using the new [content builder project][content-builder-project] rather than the MCGB config file.
- All agent action is human-in-the-loop. The goal is for the human to learn how to do something, not have the agent do the thing.
- All lesson reference material is stored in the teach project. This is where the ***teach agent*** should act.
- All exercise output is stored in the `/monogame-rt4x` submodule / subfolder. This is where the user / human should (usually) act.
- The user in this case is not an artist in any shape or form so focus on lo-fi graphics

[content-builder-project]: https://docs.monogame.net/articles/getting_started/content_pipeline/content_builder_project.html

## Project structure

```yaml
- /teach-monogame-rt4x/:   # teach root
  - /docs/:                # documents related to teaching the user, such as lesson notes and samples
  - /monogame-rt4x:        # subject root - the teach agent is teaching the user how to develop this repository. This repo is the goal
    - /docs/:              # docs for the subject repo
  - /exercises/:           # exercises, prototypes and experiments that are not part of the subject but used to support learning
```

### How do we manage our docs, roadmap and plans?

#### Teach documents

```yaml
purpose:  Docs supporting the user's learning, such as lesson content
location: /docs/
```

#### Exercises

```yaml
purpose:  When the user wants to make a toy sample or try something without changing the subject repo
location: /exercises/
```

#### Subject code and documents

```yaml
purpose:  The code the teach agent is teaching the user to develop - the goal of this whole thing
location: /monogame-rt4x/*
```

The `monogame-rt4x` subfolder / submodule will contain code (mapped by the slnx in that repo root) that is developed as part of a lesson.
Documents for the subject project will go to `monogame-rt4x/docs`. The goal is for someone to be able to use the subject repo independently
without needing to use the teach repo (for example, once the teach phase has completed), so all documents and artifacts relevant to that
purpose belong in that repo.

#### Project roadmap, issues and tasks

This repo uses github.com as its issue management system. The root project is at <https://github.com/users/JohnLudlow/projects/11/> and all work
will be done against issues on that project, showing the progress of the learning exercise.

Lessons will be linked to issues in the teach repository, while implementation will be linked to issues in the subject repository.
