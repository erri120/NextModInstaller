# Core Concepts

> This page includes the core concepts of the new mod installer format. Since the format is still WIP, these can change and aren't finalized until they appear in the specification.

1) Reduce the amount of RTFM/layer 8 issues by providing the user with a guided installation process.
2) Use a dependency system.
3) Allow the format to be extended.

## Guided Installation

> A deterministic finite-state machine (DFSM) is a computational model with a finite number of states that processes input symbols sequentially, transitioning between states based on each input. For any given state and input symbol, there is only one unique next state, making its behavior predictable and unambiguous.

The installer is a DFSM, as it follows a predefined sequence of steps and progresses from one state to another based on user input. Each step in the installation process corresponds to a state, and the transitions are determined by the user's actions or the system's feedback (e.g., selecting installation options).

Real-world complexities may introduce non-determinism to some extent, but the aim is to minimize non-deterministic behavior and ensure the installer follows a clear, well-defined sequence of steps. As such, the deterministic property of a DFSM must not be influenced by the implementation and has to be enforce by the specification.

At the core, a step in the installation process has pre-defined requirements and outputs. The outputs can be requirements for other steps. Each step has two or more choices. A step where the user can select nothing, or is forced to select one thing, is not allowed. However, you can have transitions between steps that display some information to the user. These transitions are not allowed to change the state of the DFSM and are purely informational.

## Dependencies

## Extensibility

The base specification should be game-agnostic and cover the majority of use cases. Mod Managers that want to support this format must implement the base specification, but they are free to choose what extensions they want to support.

The manifest of the installer must be upfront about which extensions are required for the installer to work properly.
