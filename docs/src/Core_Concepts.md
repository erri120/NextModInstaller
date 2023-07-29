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

Steps in the installation can have requirements. Aside from requiring a previous step, the installer can also require external dependencies. To facilitate these requirements, a dependency management system is required.

### Metadata

Aside from containing the steps of the installation process, the manifest of the installer must contain the following metadata relevant to the dependency system:

1) An immutable globally unique identifier of the mod.
2) A version number.
3) A list of all external dependencies using the previous metadata to identify them.

A 128-bit UUID ([RFC 4122](https://www.rfc-editor.org/rfc/rfc4122)) should guarantee uniqueness across space and time, as long as it's generated correctly. Importantly, the UUID is immutable, meaning that it must not change. This aspect is critical and must be enforced by all implementations.

The version number is similarly important and the scheme must be enforced by all implementations. While UUIDs are used for resolving dependencies, version numbers are used to check for compatability. A mod might only support a specific version or a range of versions of another mod. [Semantic Versioning](https://semver.org/) is a widely known versioning scheme and might be used for the new format.

With semantic versioning, a mod can dependent on another mod using a compatability range:

- `^1.2.3` means any version in the range `>=1.2.3` and `<2.0.0`
- `~1.2.3` means any version in the range `>=1.2.3` and `<1.3.0`
- `>=1.2.3` means any version greater than or equal to `1.2.3`

The specification of the new mod installer format will contain all details once finalized, but the core concept is that version numbers can be compared and consist of parts, like major, minor and patch, that each have different meaning regarding compatability.

The biggest challenge with such a dependency system is version hygiene, or more specifically, semantic versioning compliance. Updating the major, minor and patch parts of a version number has [different meanings](https://semver.org/):

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> MAJOR version when you make incompatible API changes
>
> MINOR version when you add functionality in a backward compatible manner
>
> PATCH version when you make backward compatible bug fixes

The SemVer model might has to be modified for modding, but the core idea still remains: the new version number is constructed using the level of backwards compatability.

The main issue lies in the fact that authors often don't know if their mod is a dependency for another mod. The new mod installer format will address this issue by making dependencies clear using UUIDs and version ranges. Furthermore, if every mod uses the new format, tools can be built that gather all dependency information and provide detailed information to mod authors about their dependencies.

### Mod Requirements

### Game Requirements

## Extensibility

The base specification should be game-agnostic and cover the majority of use cases. Mod Managers that want to support this format must implement the base specification, but they are free to choose what extensions they want to support.

The manifest of the installer must be upfront about which extensions are required for the installer to work properly.
