# Hex

This project is a turn-based PvE battle game played out on a hex-based tile map. It is currently in the pre-alpha phase, exploring the game concept
iterating to build it's unique identity. This idea was inspired by classic video games such as Clair Obscur: Expedition 33, Slay the Spire, and World
of Warcraft to name a few.

## Project Overview

This game is structured around a few core gameplay systems:
- **Units** represent player and enemy combatants.
- **Actions** define what units can do, such as attacking, moving, or firing projectiles.
- **Map spaces** define positioning, movement, targeting, and directional logic.
- **Battle systems** coordinate turn flow, active units, teams, and combat state.
- **Visual playback systems** separate combat results from how they are animated on screen.

The architecture is designed so that gameplay rules can be extended without tightly coupling them to Unity visuals or scene objects.

## Architecture Highlights

### Data-Driven Configuration

Config data in the game is built using Scriptable Objects for flexibility and real-time data tweaking while in play mode. Some examples include:
- Damage scaling
- Energy costs
- Travel distance
- Perfect hit thresholds
- Health and attack stats
- Visual prefabs and effects

### Action-Based Combat System

Combat behavior is modeled through reusable action classes.

Each action is responsible for answering three main questions:

1. **Can this action be performed?**
2. **What does it cost?**
3. **What happens when it is performed?**

This keeps ability logic isolated and makes it straightforward to add new abilities without modifying a large central combat class.

Example action types include:

- Basic attacks
- Cleave attacks
- Piercing projectiles
- Sniper-style attacks
- Unit summoning
- Energy manipulation
- Area or directional attacks

### Separation of Logic and Visuals

The project separates gameplay results from visual playback.

An action first produces a result, such as:

- Which units were damaged
- How much health changed
- Whether the action was a perfect hit
- Which spaces a projectile traveled through

A separate visual handler can then animate that result with projectiles, unit animations, popup text, hit feedback, and UI updates.

This makes the core combat rules easier to test, reason about, and reuse independently from presentation.

### Interface-Oriented Design

Core systems use interfaces to reduce coupling between features.

Examples include abstractions for:

- Units
- Game services
- Actions
- Tooltip providers
- Targetable or selectable objects

This allows gameplay features to depend on behavior rather than concrete MonoBehaviour implementations.

### Service-Based Game Systems

Shared game systems are organized into services and managers, such as:

- Unit management
- Map lookup and path queries
- Object pooling
- Tooltip handling
- Popup text display
- Visual playback
- Targeting and selection

This helps keep scene components focused while centralizing domain-level operations.

### Object Pooling for Runtime Effects

Temporary visual elements such as popup text and projectiles are reused through pooling.

This reduces unnecessary allocations during combat and keeps gameplay effects responsive during repeated action playback.

## Built With

- Unity
- C#
- Unity Input System
- Unity Addressables
- Newtonsoft JSON
- UniTask

## Architecture philosophy

This project was designed and built with the following as core pillars in order to keep things as flexible as possible when I come up with new ideas
I want to add or changes I want to make:

- Data-driven design
- Modular combat systems
- Interface-based programming
- Separation of gameplay and visuals
- Runtime object pooling
- Scalable feature organization
