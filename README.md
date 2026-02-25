<p align="center">
  <h1 align="center">HeartopiaManager</h1>
  <p align="center">
    Advanced all-in-one toolkit for <b>Heartopia</b><br/>
    Built on MelonLoader · Unity Il2Cpp · .NET 6.0
  </p>
  <p align="center">
    <img src="https://img.shields.io/badge/version-23.0.0-0078D4?style=flat-square" alt="Version"/>
    <img src="https://img.shields.io/badge/.NET-6.0-512BD4?style=flat-square" alt=".NET"/>
    <img src="https://img.shields.io/badge/MelonLoader-0.6.x-00C853?style=flat-square" alt="MelonLoader"/>
    <img src="https://img.shields.io/badge/platform-Windows%20x64-grey?style=flat-square" alt="Platform"/>
    <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="Status"/>
  </p>
</p>

---

## Overview

HeartopiaManager is a feature-rich MelonLoader mod for Heartopia that provides automation, visual overlays, movement enhancements, reverse-engineering tools, and quality-of-life improvements — all accessible through a clean in-game IMGUI interface with **7 organized tabs**, fully rebindable keybinds, and persistent configuration.

---

## Table of Contents

- [Features](#features)
  - [Farming & Collection](#farming--collection)
  - [Automation & Scheduling](#automation--scheduling)
  - [Visuals & ESP](#visuals--esp)
  - [Movement & Physics](#movement--physics)
  - [Performance & Display](#performance--display)
  - [Teleportation](#teleportation)
  - [Homeland & Inventory](#homeland--inventory)
  - [Music](#music)
  - [Debug & Reverse Engineering](#debug--reverse-engineering)
- [Requirements](#requirements)
- [Installation](#installation)
- [Build from Source](#build-from-source)
- [Usage](#usage)
- [Configuration](#configuration)
- [Keybinds](#keybinds)
- [Architecture](#architecture)

---

## Features

### Farming & Collection

| Feature | Description |
|:---|:---|
| **Auto-Farm** | Teleport-based resource farming with two modes: **Legacy** (nearest-node loop with configurable interval) and **Advanced** (full state-machine with zone rotation, camera scanning, cooldown tracking, retry queue, per-type cycle selection) |
| **Smart Farm Mode** | Skip resources on cooldown automatically, only visit available nodes |
| **Smart F-Key** | Auto-press interact key when near a collectible — configurable range (2–15m) |
| **Auto-Catch (Insects)** | Full insect catching loop: teleport near target, face it, press interact, retry on miss. Configurable TP distance, step forward, facing delay, F-press cooldown, retry offset. Tracks swing count, caught count, and success rate |
| **Auto-Catch (Full Map)** | Scan the entire map for insects instead of just nearby — unlimited range mode |
| **Bird Vacuum** | Attract birds toward the player. Instant teleport or smooth interpolation mode. Per-species filtering, configurable radius (10–100m), distance, height offset, animation freeze |
| **Oakee Vacuum** | Same vacuum system for oakees — instant or smooth mode, configurable radius |
| **Pet Keep-Away** | Push pets (Choco/Wola) away from the player to avoid interference during farming. Configurable min distance (2–20m) and parcel zone radius (15–150m) |
| **Tree Farm** | Waypoint-based tree chopping: save positions, auto-equip axe, teleport between points, chop with configurable press count and timing. Save/load waypoint sets |
| **Auto Repair** | Automatically repair tools, or trigger manual repair on demand |
| **Equip Tool** | One-click equip: Axe, Net, Rod, Scanner, Sprinkler, Pad |

### Automation & Scheduling

| Feature | Description |
|:---|:---|
| **Automation Scheduler** | Chain multiple tasks in sequence: **Farm → Teleport → Cook → Done**. Configurable durations per step (1–900 min each). Supports single-type or multi-type farm selection with presets |
| **Scheduler Presets** | One-click configurations: `Truffle 15 + Cook 10`, `Oyster 15 + Cook 10`, `All Mushrooms 20 + Cook 15`, `Blueberry 10 + Cook 5`, `Raspberry 10 + Cook 5` |
| **Auto-Cook** | Automated cooking: detect and click Cook/Confirm/Collect buttons. 360° rotation mode, player proximity detection (auto-pause when others are near), optional time-scale speed boost |
| **Multi-Stove Cook** | Patrol between saved stove positions, cook at each one. Configurable wait time, click loops, click delay, auto-speed multiplier. Player detection pause. Save/load stove sets |
| **Auto-Mission** | Full quest automation: scan HUD for active quest, teleport to targets/NPCs, auto-interact, auto-handle dialogue, track progress. 4-phase scanning (quest text, NPC tracking, map widgets, world NPCs) |
| **Lobby Auto-Join** | State-machine for automated lobby navigation: Join Friend Room, Join My Town, Start Game — handles panel opening, tab selection, refresh, and click sequences |
| **Anti-AFK** | Prevent idle kick by periodically toggling the bag panel. OS-level fallback (simulated input) when game is in background. Configurable interval (15–120s) |

### Visuals & ESP

| Feature | Description |
|:---|:---|
| **ESP (2D / 3D)** | Full entity overlay with two rendering modes: screen-space GUI labels or world-space 3D markers |
| **Entity Types** | Individual toggles for: Blueberries, Raspberries, Black Truffle, Oyster Mushroom, Button Mushroom, Shiitake, Penny Bun (Cepe), NPCs, Clams, Oysters, Bubbles, Insects, Birds, Fish, Oakees, Animals, Meteorites, Other Players |
| **ESP Display Options** | Show/hide boxes, labels, distance. Filter to available-only (hide cooldown). Show behind walls. RGB rainbow mode |
| **Box Modes** | Four rendering styles per entity: `Full`, `Box`, `Corner Box`, `None` |
| **Snap Lines** | Draw lines from crosshair to every tracked entity |
| **Skeleton Rendering** | Bone visualization on other players, with separate self-skeleton toggle |
| **Chams** | Material override highlighting for other players and self |
| **Radar** | On-screen minimap overlay with configurable size (100–400px) |
| **Silent Aim** | Auto-target nearest entity within FOV circle. Configurable radius (50–500px), TP distance, auto-click with interval. Per-type target filters (Animals, Insects, Birds, Fish, Bubbles, Oakees). Optional 360° mode |
| **Mushroom Scanner** | BRG (BatchRendererGroup) based detection — finds mushroom positions through the game's render system. Auto-scan every 5s. Detects: Oyster, Button, Penny Bun, Shiitake, Black Truffle |
| **Invisible Mode** | Hide player model from other players |

### Movement & Physics

| Feature | Description |
|:---|:---|
| **Fly Mode** | Free-flight in camera direction. Configurable speed (5–80). Optional noclip (traverse walls) and anti-fall (prevent falling below map) |
| **Speed Hack** | Game time-scale modification (0.5–15×) with quick presets (×1, ×2, ×5, ×7, ×10) |
| **Player Speed** | Direct `moveSpeed` modification via XDPhysics reflection (1–10×) with presets (×1, ×2, ×3, ×5) |
| **Super Jump** | Configurable jump force (8–40), gravity (0.2–1.5), infinite jumps toggle, max jump count (2–10) |
| **Noclip** | Disable player collider to walk through walls and objects |

### Performance & Display

| Feature | Description |
|:---|:---|
| **Performance Tweaks** | Master toggle with individual options: FPS cap (0–144, 0 = unlimited), No Shadows, No Fog, No V-Sync, No Anti-Aliasing, Low LOD, Low Particles/Lights, Low Draw Distance, Low-Res Textures |
| **FOV Control** | Adjustable field of view (30–120°) with quick presets (60/90/120) and reset to default |

### Teleportation

| Feature | Description |
|:---|:---|
| **Quick TP** | One-click teleport to predefined locations, shops, NPCs, houses, events, fast travel points, bus stops |
| **NPC Database** | 18 NPCs with known positions (including event NPCs) |
| **House Locations** | 11 houses with coordinates |
| **Event Locations** | 7 events: Bug Catching, Fishing, Bird Watching, Duck Puzzle, Bubble Machine, Cooking, Gardening |
| **Shop Locations** | 4 shops |
| **Wild Animal Guide** | 8 animals (Capybara, Deer, Panda, Sea Otter, Alpaca, Fox, Bunny, Ferret) with location, food preference, and weather info |
| **Custom Positions** | Save, rename, delete personal teleport points. Persist across sessions |
| **Home / Waypoint** | Set and return to a home position |
| **Numpad Navigation** | Directional teleport via numpad: Forward/Back (8/2), Left/Right (4/6), Up/Down (7/9) with configurable distances |
| **World Scanner** | Scan for bus stops, shops, and POIs in the current scene |
| **Player TP** | Teleport to other players visible on the map (up to 5 shown) |

### Homeland & Inventory

| Feature | Description |
|:---|:---|
| **Overlap Bypass** | Remove furniture placement restrictions — place objects anywhere via Harmony-patched `Physics.CheckBox` and `OverlapBox`. On-screen indicator when active |
| **Homeland Scanner** | Discover `HomeLand`, `DynamicObj`, `DynamicArea` types and methods at runtime |
| **Bulk Sell** | Scan inventory for items by sprite ID, batch-select matching items, sell in bulk. Auto-confirm sell panel |

### Music

| Feature | Description |
|:---|:---|
| **Instrument Calibration** | Step-by-step guided note position learning for Luth (15 notes), Piano (20 notes: white + black keys), and Flute |
| **Partition Playback** | Load `.txt` sheet music files, play via simulated mouse clicks at configurable BPM (presets: 60/90/120/150/200/300/450) with speed multiplier (0.25–3×) |
| **Humanize Mode** | Add random timing offsets (±ms) for natural-sounding playback |
| **Partition Manager** | Browse, reload, and manage sheet music files from `Mods/Heartopia Music Manager/` |

### Debug & Reverse Engineering

| Feature | Description |
|:---|:---|
| **Debug Overlay** | On-screen HUD: player position (XYZ), rotation, zone name, FPS, cache age, ESP entity counts, auto-catch stats, error count |
| **Runtime Inspector** | Search types across all loaded assemblies by name. Browse instances via `FindObjectsOfType`. Dump fields, properties, and values. Edit field values at runtime. Auto-discover interesting types. Export results to file |
| **Network Protocol Scanner** | Scan assemblies for network-related types and methods (Send, Receive, RPC, Protocol keywords). Targets: `EcsClient`, `XDTDataAndProtocol`, `Realtime`, `LiveQuery`, `GameApp`. Export results with filtering |
| **Deep Protocol Scan** | In-depth XD stack analysis — classify methods by direction (Client→Server, Server→Client). Export as `.md` |
| **Network Monitor** | Real-time hook and log of network calls (SEND/RECV). Live scrolling log with type, method, and payload. Export and clear |
| **Live Scanner** | Scan by radius (5–500m), scan UI hierarchy, scan active panels, dump full scene, dump all objects. Copy paths and teleport to results |
| **NPC Scanner** | Discover all NPCs in the current scene |
| **Sprite Dumper** | Dump all active UI sprites with their IDs |
| **File Logging** | Toggle debug logging to disk (`C:\Users\...\Desktop\Log-Heartopia`) |
| **Panic Stop** | One-key kill switch to disable all active automation instantly |

---

## Requirements

- **Heartopia** via Steam
- **MelonLoader 0.6.x** — Il2Cpp build, .NET 6.0 runtime
- **Windows x64**
- **.NET 6.0 SDK** — build from source only

---

## Installation

1. Install [MelonLoader](https://github.com/LavaGang/MelonLoader) into the Heartopia game directory
2. Drop `HeartopiaManager.dll` into the `Mods/` folder
3. Launch the game — the mod initializes automatically on startup

---

## Build from Source

```bash
dotnet build HeartopiaManager/HeartopiaManager.csproj -c Release
```

The post-build step automatically deploys `HeartopiaManager.dll` to `<GamePath>/Mods/`.

> **Note:** The `.csproj` references game assemblies at `C:\Program Files (x86)\Steam\steamapps\common\Heartopia\`. Adjust the `<GamePath>` property if your installation path differs.

---

## Usage

### Opening the Menu

| Action | Key |
|:---|:---|
| Toggle menu | `Insert` |
| Save position | `F12` |
| Panic stop (kill all) | `End` |

### GUI Layout

The interface is a dark-themed IMGUI window with **7 tabs**:

| Tab | Content |
|:---|:---|
| **Farm** | Auto-Farm (legacy + advanced), resource browser, Smart F-Key, data loading, BRG scan, cycle selection |
| **Auto** | Automation Scheduler, Auto-Cook, Multi-Stove, Auto-Mission, Auto-Catch, Pet Keep-Away, Tree Farm |
| **Exploit** | Speed Hack, Player Speed, Fly, Super Jump, Noclip, Performance tweaks, FOV, Anti-AFK, Invisible, Bird/Oakee Vacuum, Auto Repair, Equip Tool, Overlap Bypass, Bulk Sell, Silent Aim |
| **TP** | Quick TP, Shops, NPCs, Houses, Events, Fast Travel, Bus Stops, Wild Animals, Custom Positions, World Scanner, Numpad navigation |
| **ESP** | ESP toggles (2D/3D), entity filters (berries, mushrooms, NPCs, dynamic objects, players), box modes, skeleton, snap lines, chams, radar, RGB mode |
| **Debug** | Debug overlay, Inspector, Network Scanner, Deep Scan, Network Monitor, Live Scanner, NPC Scanner, Sprite Dumper |
| **Settings** | Rebindable keybinds (4 categories), Lobby Auto-Join, Hide Player ID, Save Config / Load Data |

---

## Configuration

All settings persist in `Mods/Heartopia_Config.txt` using a simple `key=value` format. The config loads at startup and can be saved/reloaded from the Settings tab.

**Persisted settings include:**
- All keybinds (Farm, Exploit, ESP, Misc categories)
- Movement parameters (fly speed, jump force, gravity, speed multipliers)
- ESP toggles, distances, box mode, display options
- Auto-catch timing (TP distance, step, interval, delays, cooldowns)
- Vacuum settings (radius, distance, height, species filter)
- Pet keep-away distances
- Per-resource-type cycle toggles
- Window position and size
- Performance toggle states

---

## Keybinds

All keybinds are **fully rebindable** from the Settings tab. Default assignments:

| Category | Key | Action |
|:---|:---|:---|
| **Farm & Collect** | `F6` | Auto-Farm |
| | `F1` | Auto-Cook |
| | `F3` | Bird Vacuum |
| | `F4` | Oakee Vacuum |
| **Exploits** | `F8` | Speed Hack |
| | `F5` | Fly |
| | — | Super Jump |
| | `F7` | Invisible |
| **ESP & Radar** | `F9` | Radar |
| | `F10` | ESP |
| **Misc** | `F11` | Debug |
| | `F12` | Save Position |
| | `End` | Panic Stop |

**Numpad navigation:** `8`/`2` = Forward/Back, `4`/`6` = Left/Right, `7`/`9` = Up/Down

---

## Architecture

Single `partial class HeartopiaManager : MelonMod` split across **21 source files**:

```
HeartopiaManager/
│
├── Core.cs              Entry point — OnStart, OnUpdate, OnLateUpdate, main loop
├── GUI.cs               IMGUI window, tab routing, dark theme, helper methods
├── GUI.Debug.cs         Debug overlay HUD and Debug tab content
├── GUI.Settings.cs      Settings tab — keybind editor, lobby, display options
│
├── AutoFarm.cs          Legacy + advanced farming state machine
├── AutoCook.cs          Auto-cook, stove patrol, player detection
├── AutoCatch.cs         Insect catching loop, pet keep-away
├── TreeFarm.cs          Waypoint-based tree chopping
│
├── ESP.cs               ESP rendering, radar, silent aim, world scan
├── Movement.cs          Fly, speed hack, super jump, noclip (XDPhysics)
├── Vacuum.cs            Bird & oakee vacuum systems
├── MusicManager.cs      Instrument calibration, partition playback
├── QuestMission.cs      Quest scanner, auto-mission system
│
├── BulkSell.cs          Inventory sprite scanning, batch sell
├── BypassOverlap.cs     Furniture overlap bypass, homeland scanner
├── BrgScanner.cs        Mushroom detection via BatchRendererGroup
├── Lobby.cs             Lobby auto-join state machine
│
├── Inspector.cs         Runtime type/instance/field inspector
├── NetworkScanner.cs    Network protocol analysis & live monitor
│
├── Config.cs            Settings persistence (save/load)
├── Data.cs              Static data — NPCs, houses, events, shops, fish DB
├── Shared.cs            Shared structs & enums
└── Misc.cs              Anti-AFK, Harmony patches (CharacterController,
                         Transform, Physics.CheckBox, OverlapBox)
```

### Design Patterns

- **Il2Cpp safety** — Null-check every `GameObject`/`Transform` before access. No LINQ on Il2Cpp collections. `catch` blocks log via `RecordDebugError` instead of swallowing silently
- **Object cache** — `GetCachedAllObjects()` with 1–3s refresh interval replaces per-frame `FindObjectsOfType` calls
- **State machines** — `AdvancedFarmState`, `TreeFarmState`, `LobbyJoinState`, `SchedulerState` drive multi-step automation with clean state transitions
- **Harmony patches** — Isolated patch classes in `Misc.cs` intercept `CharacterController.Move`, `Transform.set_position/rotation`, `Physics.CheckBox` (4 overloads), `Physics.OverlapBox/NonAlloc`, `XDPhysics.OverlapBox/NonAlloc`
- **XDPhysics reflection** — Runtime discovery of the game's physics API via reflection, avoiding hard Il2Cpp binding dependencies
- **Config persistence** — 60+ key-value pairs auto-saved to `Mods/Heartopia_Config.txt`, backward-compatible parsing

---

## Disclaimer

This project is provided for **educational and research purposes only**. Use at your own risk. The authors are not responsible for any consequences resulting from the use of this software.

---

## License

All rights reserved.
