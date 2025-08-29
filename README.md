# Advanced NPC System for Roblox

## Overview

This repository contains a sophisticated NPC (Non-Player Character) system designed for Roblox games, featuring intelligent zombie AI with advanced pathfinding, player detection, and dynamic behavior patterns. The system provides a robust foundation for creating engaging zombie survival games with realistic NPC behaviors.

## Features

### 🧠 Intelligent AI Behaviors
- **Player Detection**: NPCs can detect players within a configurable range and begin pursuit
- **Adaptive Pathfinding**: Uses Roblox's PathfindingService for intelligent navigation around obstacles
- **Multi-State Behavior**: Seamless transitions between patrolling, chasing, and returning to spawn
- **Terrain Analysis**: Smart terrain evaluation for walkable surfaces and slope detection

### 🏃‍♂️ Advanced Movement System
- **Dynamic Speed Control**: Different speeds for patrolling vs. chasing
- **Intelligent Jumping**: Context-aware jumping for obstacles and elevation changes
- **Stuck Detection**: Sophisticated system to detect and resolve stuck situations
- **Water Interaction**: Special water-based mechanics with explosive effects

### 🎯 Combat & Interaction
- **Proximity-based Damage**: Automatic damage dealing when in close range
- **Sound Integration**: Integrated sound system for different AI states
- **Health Management**: Randomized health values for variety
- **Explosion Mechanics**: Dramatic water-based explosion effects

### ⚙️ Highly Configurable
All behavior parameters are easily adjustable through a central configuration table, including:
- Detection and chase ranges
- Movement speeds
- Jump parameters
- Damage values
- Timing controls

## Installation

### Prerequisites
- Roblox Studio
- ServerScriptService for module placement
- ServerStorage for zombie model storage

### Setup Steps

1. **Place the NPC Module**
   ```lua
   -- Place NPCModule in ServerScriptService/Modules/
   ```

2. **Prepare Zombie Model**
   - Create or import a zombie model named "Sentinel"
   - Place it in ServerStorage
   - Ensure the model has:
     - Humanoid component
     - HumanoidRootPart
     - Proper character structure

3. **Set Up Spawn Points**
   - Create parts named "ZombieSpawn" in Workspace
   - Position them where you want zombies to appear
   - The system will automatically spawn zombies at these locations

4. **Sound System (Optional)**
   - Create NPCSound module in ServerScriptService/Modules/
   - Implement sound functions for enhanced immersion

## Usage

### Basic Implementation

```lua
local ZombieAI = require(game.ServerScriptService.Modules.NPCModule)

-- Initialize the system (spawns zombies at all ZombieSpawn parts)
ZombieAI:Init()

-- Manually spawn a zombie at a specific location
local spawnPart = workspace.ZombieSpawn -- Your spawn part
ZombieAI:SpawnZombieAt(spawnPart)
```

### Configuration

The system uses a centralized CONFIG table for easy customization:

```lua
local CONFIG = {
    DetectionRange = 30,        -- Player detection distance
    ChaseAbandonRange = 50,     -- Distance to abandon chase
    PatrolSpeed = 7,            -- Speed while patrolling
    ChaseSpeed = 17,            -- Speed while chasing
    AttackDamage = 15,          -- Damage per attack
    HealthRange = {50, 100},    -- Random health range
    PatrolRadius = 25,          -- Patrol area around spawn
    JumpHeight = 12,            -- Maximum jump height
    -- ... many more configurable options
}
```

## Code Structure

### Core Components

1. **ZombieAI Module**: Main orchestrator handling spawning and AI lifecycle
2. **State Management**: Individual zombie state tracking for complex behaviors
3. **Pathfinding System**: Advanced navigation with fallback strategies
4. **Terrain Analysis**: Multi-point terrain evaluation for accurate movement
5. **Jump Logic**: Context-aware jumping system with cooldowns

### Key Functions

- `isWalkable(position)`: Evaluates terrain walkability with slope analysis
- `getValidPatrolPosition()`: Finds suitable patrol destinations
- `handleChase()`: Manages player pursuit behavior
- `handlePatrol()`: Controls patrolling patterns
- `handleWater()`: Manages water-based mechanics

### AI States

The system implements a state machine with these primary states:
- **Patrolling**: Random movement around spawn area
- **Chasing**: Active pursuit of detected players
- **Returning**: Navigation back to spawn point
- **Stuck Recovery**: Automatic resolution of movement issues

## Advanced Features

### Terrain Intelligence
- Multi-point sampling for accurate walkability detection
- Slope angle calculation and limits
- Water detection and avoidance
- Obstacle recognition and navigation

### Movement Optimization
- Smoothed target positioning to reduce jitter
- Elevation-aware pathfinding
- Dynamic waypoint validation
- Intelligent descent and climbing behaviors

### Performance Considerations
- Efficient raycast operations with filtered parameters
- Throttled path updates to prevent excessive computation
- Cached waypoint systems for patrol routes
- Optimized stuck detection algorithms

## Technical Details

### Dependencies
- **PathfindingService**: For navigation computation
- **ServerStorage**: Zombie model storage
- **Workspace**: Terrain analysis and spawning
- **NPCSound Module**: Audio system integration (optional)

### Performance Notes
- The system uses 0.05-second update intervals for smooth behavior
- Raycasting is optimized with proper filtering
- Path computation is throttled to balance responsiveness and performance

## Customization Examples

### Adjusting Aggression
```lua
CONFIG.DetectionRange = 50      -- More aggressive detection
CONFIG.ChaseSpeed = 25          -- Faster pursuit
CONFIG.AttackDamage = 25        -- Higher damage
```

### Creating Patrol Zones
```lua
CONFIG.PatrolRadius = 40        -- Larger patrol area
CONFIG.PatrolTimeout = 10       -- Longer patrol intervals
```

### Jump Behavior Tuning
```lua
CONFIG.JumpHeight = 20          -- Higher jumps
CONFIG.JumpCooldown = 1         -- More frequent jumping
```

## Contributing

This NPC system is designed to be modular and extensible. Key areas for enhancement include:
- Additional AI behaviors and states
- More sophisticated group AI mechanics
- Enhanced sound and visual effects integration
- Performance optimizations for large-scale deployments

## Credits

This advanced NPC system demonstrates sophisticated game AI principles including:
- Finite State Machine implementation
- Advanced pathfinding with fallback strategies
- Realistic movement and physics integration
- Modular, maintainable code architecture

Perfect for zombie survival games, tower defense scenarios, or any Roblox experience requiring intelligent NPC behaviors.