# Extensibility

The mod installer format should be extensible. The base format should provide all core concepts, which should be applicable for every game. Mod Managers would be required to implement this base format, but can opt-in to implement extensions.

The manifest of the installer should specify which extensions are being used upfront. This allows implementations to quickly check if the manifest is supported or not.

Extensions shall provide game specific logic and operations, like updating files in a game specific format.
