# FRAYMUS Build Order

## Purpose

This branch is the controlled evolution path from the original MarioRemake engine toward FRAYMUS. The original tutorial's order of operations is the development spine. We do not redesign the entire system before producing a working result.

## Governing rule

**Every milestone must compile, run, and have a visible or machine-verifiable test before the next milestone begins.**

The simulation must not depend on OpenGL, GLFW, GLSL, LWJGL, or ImGui. Those may remain as historical/reference implementations, but FRAYMUS Core must be renderer-independent.

## Source sequence recovered from the original course

1. Window / application bootstrap
2. Event listeners / input
3. Scene manager + delta time
4. Rendering abstraction
5. First visible primitive
6. Camera
7. Textures
8. Entity Component System
9. Rendering/resource management
10. Spritesheets / animation foundations
11. Editor/UI foundations
12. Serialization / deserialization
13. Editor variable exposure and coordinate conversion
14. Drag/drop editor
15. Debug drawing / grid
16. Viewport and picking
17. Editor camera and gizmos
18. Properties / inspection
19. Physics integration
20. Event system + physics
21. Runtime Play/Stop
22. Refactoring and physics stabilization
23. Font/text rendering
24. Scene hierarchy
25. Animation
26. Audio (optional subsystem)
27. Physics gameplay components
28. Player controller / variable jump
29. Powerups
30. Enemy AI
31. Camera/grid/editor improvements
32. Additional enemy AI
33. Final gameplay/distribution

The original course explicitly presents these stages progressively, including window setup, scene management, ECS, serialization, editor, JBox2D, runtime, animation, audio, player physics, and AI. See the course chapter list at https://www.youtube.com/watch?v=025QFeZfeyM.

## FRAYMUS mapping

### FOUNDATION-000 — Preserve the reference

- Keep the original MarioRemake history intact.
- Work on `fraymus-foundation` or later dedicated FRAYMUS repository/branch.
- Do not destroy working historical code merely to make the new architecture cleaner.

### FOUNDATION-001 — Separate simulation from renderer

Target separation:

```text
FRAYMUS Core
  Entity / Component / Transform
  World / Scene
  Time
  Events
  Physics
  State

Renderer adapters
  Swing / Java2D
  Headless
  Optional legacy OpenGL
```

Acceptance:

- Core packages contain no OpenGL/LWJGL/GLFW imports.
- A world can update without creating a graphics window.
- Existing entity/component concepts remain recognizable.

### FOUNDATION-002 — Deterministic clock

Acceptance:

- Fixed simulation timestep is explicit.
- Accumulator logic consumes all elapsed simulation time correctly.
- A test can run N fixed steps and obtain reproducible state.

### FOUNDATION-003 — JFrame / Java2D renderer

Acceptance:

- A JFrame opens on macOS/Windows/Linux with a standard JDK.
- A world is visibly rendered without OpenGL.
- Camera, transforms, debug primitives, and entity selection can be represented.

### FOUNDATION-004 — Headless runner

Acceptance:

```text
java -jar fraymus.jar --headless
```

runs the same simulation code used by the desktop application.

### FOUNDATION-005 — Episode recorder

Acceptance:

An episode records at minimum:

- episode id
- simulation seed
- starting state hash
- observations
- actions
- simulation steps
- outcome
- final state hash
- timestamp/provenance metadata

### FOUNDATION-006 — FRAYMUS Cell ABI v0.1

Define a versioned contract for:

- identity
- input
- output
- state
- permissions
- resource limits
- episode records
- lineage
- artifact hash
- verification status

## Parallel work rule

Other agents may work ahead **only on bounded, non-conflicting artifacts**:

- tests
- interface definitions
- documentation
- schemas
- renderer prototypes
- deterministic clock tests
- episode format design
- source-bundle tooling

They must not create unrelated feature branches that bypass the build order.

## What not to do yet

Do not make these dependencies of Core:

- OpenGL
- GLFW
- GLSL shaders
- LWJGL
- ImGui
- React
- Three.js
- blockchain
- cloud-specific services

They can be adapters or later integrations.

## Definition of done

A milestone is not done because the classes exist. It is done only when:

1. Code compiles.
2. Tests pass.
3. The executable runs.
4. The intended behavior is observable.
5. The milestone is documented.
6. Git records the milestone.
7. The next milestone can build on it without guessing.
