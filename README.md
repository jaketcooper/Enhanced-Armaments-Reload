See issue: https://github.com/Nova-Committee/Enhanced-Armaments-Reload/pull/31

Summary

Improve runtime safety and multiplayer robustness by adding defensive checks and switching global state to per-player tracking.
Why

Prevents NullPointerExceptions and index/collection out-of-bounds errors when reading item rarity and building tooltips.
Makes bow-hand tracking and periodic armor healing safe and deterministic in multiplayer by storing per-player state instead of shared static fields.
Prevents negative durability values and health overflow when abilities modify damage/health.
Ensures rarity data loading creates its directory reliably and cleans up formatting.
Key changes

Guard against null rarity values early to avoid NPEs when rendering UI or processing events.
Add bounds and emptiness checks before accessing tooltip list indexes, attribute modifier collections, and armor/mainhand item stacks.
Replace shared static bow-hand variable with a per-player weak map to correctly track which hand fired a projectile in multiplayer contexts.
Replace a single global healing counter with a per-player timer map so each player heals independently and safely.
Clamp durability and health updates so values remain within valid ranges.
Ensure rarity files directory is created if missing and tidy minor formatting/cleanup.
Benefits

Reduces crashes and unexpected behavior caused by missing or malformed item metadata.
Fixes multiplayer desynchronization and incorrect behavior caused by shared mutable state.
Improves stability of tooltip rendering and combat/healing logic.
Makes file loading more robust across environments.
Relates

General stability/bugfixes for item rarity, tooltips, combat, and player updates.
