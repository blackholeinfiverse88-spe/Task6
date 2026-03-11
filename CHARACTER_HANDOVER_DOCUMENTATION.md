
## Overview

This document provides **final handover documentation for all gameplay characters** used in the VR strategy battle system. It is intended for **engineering, QA, and live-ops teams** to integrate, maintain, and extend character functionality.

The characters are used in a **VR card-based battlefield deployment system**, where the player selects units from cards and deploys them into battle lanes to attack the enemy castle.

---

# 1. Game Context

### Game Type

VR Strategy / Card Deployment Battle

### Core Flow

1. Player selects a **unit card**
2. Player points to a **spawn lane**
3. Character is **instantiated in battlefield**
4. Unit **automatically navigates toward enemy base**
5. Unit attacks **enemy units or enemy castle**

---

# 2. Character Deployment System

### Spawn Method

Characters are spawned using **VR controller ray interaction**.

Steps:

1. Player selects card
2. Player points at battlefield
3. Unit spawns at **spawn socket**
4. Unit begins navigation

### Spawn Prefab Structure

```
Character_Prefab
 ├── Mesh
 ├── Animator
 ├── NavMeshAgent
 ├── Collider
 ├── HealthSystem
 ├── AttackSystem
 ├── VFX_Sockets
```

---

# 3. Character Roster

Characters available in the current build:

| Character    | Role       | Type       | Card Cost |
| ------------ | ---------- | ---------- | --------- |
| Skeleton     | Swarm Unit | Melee      | 3         |
| Demon Knight | Heavy Unit | Melee      | 7         |
| Fire Demon   | Magic Unit | Ranged     | 5         |
| Archer       | Ranged DPS | Projectile | 4         |
| Troll        | Tank Unit  | Melee      | 6         |

These characters are visible in the **card selection board** shown in the VR interface.

---

# 4. Character Behavior

## Movement

All units use:

```
Unity NavMeshAgent
```

Movement behavior:

* Move forward along lane
* Avoid obstacles
* Stop when target detected

Movement parameters:

| Parameter     | Value              |
| ------------- | ------------------ |
| Speed         | Character specific |
| Acceleration  | Medium             |
| Stop Distance | Attack range       |

---

# 5. Combat System

## Targeting Priority

Units target in the following order:

1. Enemy units in lane
2. Enemy structures
3. Enemy castle

---

## Attack Types

### Melee Attack

Used by:

* Skeleton
* Demon Knight
* Troll

Mechanic:

```
Distance check
Trigger attack animation
Apply damage
```

---

### Ranged Attack

Used by:

* Archer
* Fire Demon

Mechanic:

```
Spawn projectile
Projectile tracks target
On hit → apply damage
```

---

# 6. Health System

Each character uses a **Health Component**.

Structure:

```
HealthSystem
 ├── MaxHealth
 ├── CurrentHealth
 ├── TakeDamage()
 ├── Die()
```

Damage sources:

* Enemy melee attack
* Enemy projectile
* Castle defense

---

# 7. Animation System

Characters use **Animator Controller**.

Required animation states:

| State  | Description        |
| ------ | ------------------ |
| Idle   | Standing animation |
| Walk   | Movement           |
| Attack | Combat             |
| Hit    | Damage reaction    |
| Death  | Death animation    |

Transitions are controlled via parameters:

```
isMoving
isAttacking
isDead
```

---

# 8. Card System Integration

Characters are linked to **card UI elements**.

Card data structure:

```
UnitCard
 ├── CharacterPrefab
 ├── EnergyCost
 ├── CardIcon
 ├── SpawnCooldown
```

Example:

| Card              | Unit          | Cost |
| ----------------- | ------------- | ---- |
| Skeleton Card     | Skeleton Unit | 3    |
| Demon Knight Card | Demon Knight  | 7    |
| Fire Demon Card   | Fire Demon    | 5    |

---

# 9. Energy System

Energy bar shown in VR HUD.

Rules:

```
Energy regenerates over time
Card can be played only if energy ≥ card cost
Energy deducted on spawn
```

---

# 10. Battlefield Layout

Battlefield contains:

* Player castle
* Enemy castle
* Multiple lanes
* Water obstacles
* Spawn zones

Structure:

```
Battlefield
 ├── Player_Base
 ├── Enemy_Base
 ├── Lane_01
 ├── Lane_02
 ├── Lane_03
```

Units automatically follow **lane navigation mesh**.

---

# 11. Castle Interaction

Castles act as **final objective**.

Castle features:

* Large health pool
* Receives damage from units
* Triggers match end when destroyed

Match timer is also visible in the UI.

---

# 12. VR Interaction System

Interaction method:

```
VR Controller Raycast
```

Supported actions:

| Action      | Description |
| ----------- | ----------- |
| Point       | Aim ray     |
| Select Card | Choose unit |
| Spawn       | Deploy unit |

Player feedback:

* Highlighted card
* Spawn confirmation
* Energy deduction

---

# 13. Performance Optimization

Required optimization for VR:

### Character Limits

Maximum units active per match:

```
40–60 units
```

### Optimization Methods

* LOD models
* Animation culling
* Object pooling for projectiles
* Shared materials

---

# 14. File Structure

Project structure:

```
Assets/
 ├── Characters
 │   ├── Skeleton
 │   ├── DemonKnight
 │   ├── FireDemon
 │   ├── Archer
 │   ├── Troll
 │
 ├── Prefabs
 │   ├── Units
 │
 ├── Scripts
 │   ├── Combat
 │   ├── AI
 │   ├── Health
 │   ├── CardSystem
 │
 ├── VFX
 ├── Animations
```

---

# 15. Known Constraints

Current prototype limitations:

* Basic AI targeting
* No advanced pathfinding branching
* Limited unit variety
* Simple combat resolution

These will be expanded in future updates.

---

# 16. QA Checklist

Before final build:

* Character spawns correctly
* Card cost deducted
* Unit navigates lane
* Attack triggers correctly
* Damage applied properly
* Death animation triggers
* Unit removed from scene

---

# 17. Handover Contacts

| Role              | Responsibility            |
| ----------------- | ------------------------- |
| Game Design       | Balance and card cost     |
| Gameplay Engineer | Combat systems            |
| Technical Artist  | Character rig + animation |
| QA Team           | Gameplay validation       |

---

# 18. Final Status

Character systems are now:

```
READY FOR ENGINE INTEGRATION
READY FOR GAMEPLAY BALANCING
READY FOR QA TESTING
```

---

# End of Document
