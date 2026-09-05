# FRAYMUS Agent Handoff Contract

## Mission

Evolve the historical MarioRemake Java engine into a renderer-independent FRAYMUS foundation while preserving the proven order of construction.

## Current branch

`fraymus-foundation`

Base reference commit:

`589c4cd912cd833e4216ebd30d2091758429fd23`

## How another agent should work

Before changing code:

1. Read `FRAYMUS_BUILD_ORDER.md`.
2. Identify exactly one milestone or explicitly assigned bounded task.
3. Inspect the existing implementation before inventing replacements.
4. Keep changes small and independently testable.
5. Do not add a new framework merely because it is convenient.
6. Do not introduce OpenGL/LWJGL/GLFW/GLSL/ImGui into FRAYMUS Core.

## Parallel-safe tasks

An agent can work independently on:

- Java interfaces
- unit tests
- deterministic clock tests
- episode schemas
- serialization schemas
- renderer abstraction prototypes
- Java2D rendering prototypes
- headless runner tests
- source bundle generation
- documentation

## Integration rule

No agent should silently change architecture outside its assigned boundary. If a dependency is required, document it first.

## Preferred implementation style

Use ordinary Java classes with clear ownership and small interfaces. Favor composition over deep inheritance. Avoid unnecessary allocations in simulation hot paths. Keep external dependencies at module boundaries.

## Verification rule

A class existing is not evidence of completion. Every implementation task should include a runnable test or demonstration whenever practical.

## First implementation target

FOUNDATION-001: renderer separation.

The desired result is that a simulation/world can be created, updated, and tested without opening an OpenGL window.

## Important distinction

The historical MarioRemake code is the reference implementation. FRAYMUS is its controlled evolution. Do not claim that a subsystem is equivalent merely because it has similarly named classes; prove the behavior with tests or a visible demonstration.

## Handoff format

When returning work, report:

- files changed
- interfaces/classes added
- behavior implemented
- tests added
- commands used to verify it
- expected output
- known limitations
- next recommended milestone
