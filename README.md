# FunkyIDE

**FunkyIDE** is a rework of Visual Studio Code focused on creating an all-in-one development environment for Friday Night Funkin' modding.

Instead of replacing VS Code with a completely separate editor, FunkyIDE builds directly on the VS Code source code and adds specialized tools for working with FNF projects.

> VS Code + deep FNF tooling.

Repository: https://github.com/Mystic-Red/FunkyIDE

---

## Status

FunkyIDE is currently under heavy development.

The project is being rebuilt in phases so its FNF tools can share the same project, engine, asset, timing, diagnostics, and filesystem infrastructure instead of becoming a collection of disconnected editors.

**Psych Engine** is the first major engine target.

Support for additional engines and forks is planned through an engine adapter architecture.

Not every feature described in this README is implemented yet.

---

# Why FunkyIDE?

Making an FNF mod usually means switching between several different tools:

- VS Code
- chart editors
- sprite editors
- image editors
- audio software
- JSON files
- Lua/HScript files
- engine folders
- external preview tools

FunkyIDE aims to bring much of that workflow into one environment while keeping the advantages of a full code editor.

Normal VS Code functionality should remain available, including:

- Explorer
- Search
- Source Control
- Terminal
- Command Palette
- Extensions
- Themes
- Keybindings
- Text editors
- Diff editors
- Workspaces
- Settings

FunkyIDE adds FNF-specific workflows on top of those systems rather than replacing them.

---

# Core Goals

## Real FNF Project Support

FunkyIDE should understand the project you actually opened.

That includes concepts such as:

- songs
- charts
- difficulties
- characters
- stages
- events
- note types
- scripts
- audio
- sprite atlases
- dialogue
- cutscenes
- weeks
- Freeplay data
- HUD layouts
- noteskins

The IDE should operate on real project files instead of fake demo data.

---

## Engine Adapters

FunkyIDE is designed around engine adapters.

The main IDE should not need to contain hardcoded knowledge about every FNF engine.

The general architecture is:

FNF Engine
→ Engine Adapter
→ FunkyIDE

The first major adapter targets **Psych Engine**.

Future adapters should be able to support other engines and forks without requiring the entire IDE to be rewritten.

---

## Shared Project Infrastructure

Future FunkyIDE tools should share infrastructure instead of independently scanning and parsing the project.

Shared systems are intended for things such as:

- project detection
- engine detection
- asset discovery
- project indexing
- filesystem watching
- diagnostics
- validation
- timing
- BPM maps
- audio playback
- waveforms
- images
- sprite atlases

A Chart Editor should not need to invent its own character finder.

A Character Editor should not need its own independent project scanner.

The tools should be connected.

---

# FNF Explorer

FunkyIDE is designed to include an FNF-aware project explorer alongside the normal VS Code Explorer.

Instead of only showing raw folders and files, it can organize FNF content conceptually.

For example:

- Mods
- Songs
- Characters
- Stages
- Events
- Note Types
- Scripts
- Audio
- Images
- Weeks

Entries remain connected to their real files.

The regular VS Code Explorer remains available.

---

# Planned Tools

## Chart Editor

The Chart Editor is intended to support:

- arbitrary difficulties
- note placement
- sustain notes
- custom note types
- events
- BPM changes
- sections
- snapping
- waveforms
- Inst playback
- Voices playback
- multiple vocal stems
- multi-selection
- clipboard operations
- undo and redo
- timing tools

The editor should safely load and save existing charts without destroying custom metadata.

---

## Character and Sprite Tools

Planned character and sprite functionality includes:

- character configuration
- sprite previewing
- Sparrow/XML atlases
- animations
- animation offsets
- character icons
- health colors
- reference overlays
- basic image editing
- pixel-art friendly workflows
- character creation workflows

---

## Stage Builder

The Stage Builder is intended to provide visual editing for things such as:

- stage objects
- positioning
- scaling
- rotation
- cameras
- layering
- character positions
- backgrounds
- static stage configuration

Dynamic or script-controlled behavior should remain accessible through the underlying scripts.

FunkyIDE should not pretend that arbitrary Lua or HScript can always be converted into visual stage data.

---

## Dialogue Builder

A visual workflow for creating and editing FNF dialogue while preserving access to its underlying representation.

---

## Event Editor

Tools for creating, inspecting, and editing:

- song events
- built-in engine events
- custom events
- event parameters
- event timing

---

## Cutscene Builder

FunkyIDE includes work toward a visual cutscene workflow for FNF mods.

Cutscenes should remain compatible with real project data and scripts instead of being locked into a proprietary FunkyIDE-only representation.

---

## HUD Builder

Planned HUD tooling includes:

- health bars
- health icons
- score
- combo displays
- judgements
- time bars
- custom meters
- HUD positioning
- visual states
- animations
- configurable meter behavior

The HUD system should remain generic enough to support custom mod mechanics instead of hardcoding one specific project.

---

## Noteskin Builder

Planned noteskin tooling includes:

- receptors
- notes
- sustain visuals
- note splashes
- custom note visual types
- arbitrary key counts
- atlas configuration
- imported noteskins
- previewing

---

## Freeplay and Menu Builder

Planned Freeplay/menu tools include:

- song organization
- categories
- ordering
- variants
- difficulties
- icons
- colors
- badges
- preview audio
- hidden songs
- unlock conditions
- category backgrounds
- menu previews

---

## Story and Week Builder

Visual tools are planned for creating and editing story-mode weeks and their related metadata.

---

## Game Over Editor

Planned Game Over tooling may include:

- game-over characters
- animations
- music
- sounds
- camera behavior
- retry behavior
- special states
- project-specific game-over configurations

---

# Music Maker

FunkyIDE eventually aims to include a small FNF-focused digital audio workstation.

It is not intended to replace FL Studio or another full DAW.

The goal is to provide enough integrated music tooling for common FNF workflows.

Planned concepts include:

- Browser
- Playlist
- Channel Rack
- Piano Roll
- Mixer
- samples
- chromatics
- vocal tracks
- automation
- effects
- SoundFont support
- Inst export
- Voices export
- full mix export

FunkyIDE music projects may use their own project representation, such as `.fnfmusic`, while exporting standard audio files for actual FNF engines.

---

# FNF-Aware Scripting

FunkyIDE eventually aims to expand normal VS Code scripting with FNF-specific intelligence.

Potential features include:

- engine API autocomplete
- hover documentation
- parameter hints
- asset references
- song IDs
- character IDs
- stage IDs
- event names
- note types
- HUD elements
- project-aware diagnostics

Optional visual scripting may be added for constructs that can be represented safely.

FunkyIDE should not attempt to destructively convert arbitrary handwritten Lua or HScript into visual nodes and rewrite the source.

---

# Raw Source Access

Visual editors should complement source editing rather than replace it.

If FunkyIDE can visually edit something, the user should still be able to access the underlying:

- JSON
- XML
- Lua
- HScript
- configuration
- engine data

A visual editor should never trap a project inside FunkyIDE.

---

# Non-Destructive Editing

FNF mods frequently contain custom information FunkyIDE may not understand.

Examples include:

- custom JSON properties
- engine-fork extensions
- custom events
- custom note types
- unusual metadata
- scripts
- mod-specific fields

FunkyIDE should preserve unknown information whenever reasonably possible.

Opening a file and pressing Save should not silently delete fields merely because FunkyIDE does not recognize them.

---

# Project and Mod Awareness

FunkyIDE should understand that an FNF workspace is not always one simple folder.

For example, a user may open:

- an entire engine source repository
- one standalone mod
- a workspace containing several mods
- a folder nested inside a project
- a multi-root workspace

The project system should distinguish between concepts such as:

- engine root
- project root
- mod root
- active mod
- shared content
- base content
- overridden content

Future editors should also be able to identify where discovered content came from.

---

# Custom Difficulties

FunkyIDE should not assume every song only contains:

- Easy
- Normal
- Hard

Custom difficulty names should be treated as first-class project data.

Examples could include:

- Encore
- Nightmare
- Remix
- Old
- Erect
- V2

or anything else defined by a mod.

---

# Timing

Several FunkyIDE tools need to agree on timing.

Shared timing infrastructure should eventually handle:

- BPM
- BPM changes
- song position
- beats
- steps
- measures
- snapping
- chart timing
- event timing

The Chart Editor, Event Editor, Music Maker, Cutscene Builder, and other time-based tools should not each implement incompatible timing systems.

---

# Security

FNF mods should be treated as untrusted projects.

FunkyIDE should not execute arbitrary project code just to inspect it.

This includes:

- Lua
- HScript
- JavaScript
- shell scripts
- executables

Static analysis may be used where appropriate.

Running the game, scripts, build tools, or other executable project content should happen only through explicit workflows.

---

# Performance

FunkyIDE should be capable of working with large mods and repositories.

Project discovery should avoid:

- decoding every image during startup
- loading every audio file into memory
- rescanning the entire workspace after every tiny change
- blocking the workbench during large filesystem operations

Where appropriate, FunkyIDE should use:

- incremental indexing
- caching
- lazy loading
- filesystem events
- cancellation
- asynchronous work

---

# Engine Launching

FunkyIDE eventually needs to launch the user's actual configured FNF engine or build.

An internal preview is not a replacement for testing the real game.

Engine adapters should eventually be able to describe:

- executable location
- build commands
- launch commands
- arguments
- working directory
- selected song
- selected difficulty
- debug options

Where possible, FunkyIDE should capture relevant game output and crash information.

---

# Architecture Direction

The exact source structure may evolve as the rework progresses, but FunkyIDE is based around several conceptual systems.

Examples include:

- `FnfEngineAdapter`
- `PsychEngineAdapter`
- `FnfEngineRegistry`
- `FnfProjectService`
- `FnfAssetDiscoveryService`

Neutral project models may represent concepts such as:

- `FnfSong`
- `FnfChart`
- `FnfCharacter`
- `FnfStage`
- `FnfDialogue`
- `FnfEvent`
- `FnfHudLayout`
- `FnfNoteskin`
- `FnfCutscene`
- `FnfFreeplayMenu`
- `FnfWeek`
- `FnfMusicProject`

These names describe the architectural direction and may change as the codebase evolves.

The current implementation is always the source of truth.

---

# Rework Roadmap

FunkyIDE is being rebuilt in phases.

## Phase 0 — Foundation

Focus:

- audit the existing codebase
- preserve useful old work
- establish a known build baseline
- establish FunkyIDE architecture
- project services
- engine adapters
- Psych Engine detection
- project lifecycle
- logging
- diagnostics foundations
- minimal project visibility

## Phase 1 — FNF Project Support

Focus:

- real Psych Engine project discovery
- mod discovery
- project indexing
- songs
- difficulties
- characters
- stages
- scripts
- events
- note types
- asset origins
- incremental updates
- FNF Explorer

## Later Phases

Planned later work includes:

- Chart Editor
- Character and Sprite tools
- Dialogue Builder
- Stage Builder
- Music Maker
- Event Editor
- Cutscene tooling
- Freeplay/Menu Builder
- HUD Builder
- Noteskin Builder
- Game Over Editor
- Story/Week Builder
- Shader tooling
- FNF-aware Script Editor
- visual scripting for supported constructs
- real engine launch/testing integration

The exact order may change as the architecture and project evolve.

---

# Platform

Windows is an important development and target platform for FunkyIDE.

The project should avoid unnecessarily platform-specific assumptions and should use VS Code's existing cross-platform infrastructure where practical.

---

# Development Philosophy

FunkyIDE follows a few important principles:

1. Keep VS Code useful.
2. Integrate with the existing VS Code architecture instead of fighting it.
3. Use real FNF project data.
4. Psych Engine comes first, but should not become hardcoded into every feature.
5. Share project, asset, timing, and diagnostic infrastructure.
6. Preserve unknown/custom mod data.
7. Keep raw source accessible.
8. Treat project code as untrusted.
9. Prefer real working functionality over impressive mockups.
10. Rework existing functionality instead of endlessly creating duplicate versions.

---

# Contributing

FunkyIDE is still early in its rework.

Large architectural changes should be discussed carefully before implementation.

When adding a new editor or system:

- inspect the current architecture first
- reuse shared project services
- avoid duplicating parsers and filesystem scanners
- keep engine-specific behavior behind adapters where practical
- preserve unknown project data
- provide raw source access
- follow existing VS Code patterns
- avoid breaking normal VS Code functionality

---

# Disclaimer

FunkyIDE is an independent project.

It is not affiliated with or endorsed by:

- The Funkin' Crew
- Psych Engine
- Microsoft
- Visual Studio Code

Friday Night Funkin', Psych Engine, Visual Studio Code, and other referenced projects belong to their respective owners.

FunkyIDE does not intend to bundle copyrighted assets from FNF or third-party mods.

Test and built-in assets should be original, generated, public-domain, or permissively licensed.

---

# License

See the repository's license file for the current licensing terms.

Because FunkyIDE is based on the Visual Studio Code source code, all modifications and redistribution must remain compatible with the licenses and notices applicable to the upstream source and any included dependencies.

---

# FunkyIDE

One editor.

Code, charts, sprites, stages, music, scripts, and the rest of the FNF modding workflow.
