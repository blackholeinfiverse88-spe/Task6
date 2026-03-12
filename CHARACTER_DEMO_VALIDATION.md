
## Overview

This document defines the **validation requirements and safety checks** for all playable and enemy characters before the **VR gameplay demo build** is delivered to stakeholders, testers, or public demonstrations.

The goal is to ensure that **all characters behave reliably, perform well in VR, and cannot break the demo experience**.

---

# 1. Demo Objectives

The demo build must demonstrate:

* Card-based unit spawning
* Lane-based battle progression
* Character combat interactions
* Castle attack mechanics
* Stable VR performance

All characters must support these systems **without errors, glitches, or performance drops**.

---

# 2. Character Validation Scope

Characters must be validated across the following areas:

| Area           | Validation Required                     |
| -------------- | --------------------------------------- |
| Spawn System   | Card deploys correct character          |
| Navigation     | Unit moves along lane correctly         |
| Combat         | Attacks trigger and deal damage         |
| Health         | Damage and death function correctly     |
| Animation      | All required states transition properly |
| VR Performance | No frame drops or spikes                |
| VFX            | Effects trigger without errors          |

---

# 3. Character Demo Roster

The following characters are included in the demo:

| Character    | Role         | Type       | Demo Status        |
| ------------ | ------------ | ---------- | ------------------ |
| Archer       | Ranged Unit  | Projectile | Pending Validation |
| Troll        | Tank Unit    | Melee      | Pending Validation |
| Fire Demon   | Magic Damage | Ranged     | Pending Validation |
| Demon Knight | Heavy Unit   | Melee      | Pending Validation |
| Skeleton     | Swarm Unit   | Melee      | Pending Validation |

Each character must pass **all demo validation tests** before the demo build is finalized.

---

# 4. Spawn Validation

### Test Objective

Ensure the **correct unit spawns when the card is selected**.

### Test Steps

1. Select a card in VR
2. Aim at spawn lane
3. Deploy unit
4. Confirm correct prefab spawns

### Expected Result

```text
Card → Correct Character Prefab Spawned
```

### Failure Conditions

* Wrong character spawns
* No unit appears
* Unit spawns outside battlefield

---

# 5. Movement Validation

### Test Objective

Ensure units move properly along the lane.

### Checks

* Unit starts moving immediately after spawn
* Unit follows **NavMesh path**
* Unit does not walk through obstacles
* Unit stops within attack range of enemies

### Movement Parameters

| Parameter   | Expected Behavior  |
| ----------- | ------------------ |
| Speed       | Character-specific |
| Pathfinding | Smooth             |
| Rotation    | Natural turning    |

---

# 6. Combat Validation

### Melee Units

Units tested:

* Troll
* Demon Knight
* Skeleton

Test cases:

* Attack triggers when enemy nearby
* Damage applied correctly
* Attack animation synced with damage

---

### Ranged Units

Units tested:

* Archer
* Fire Demon

Test cases:

* Projectile spawns correctly
* Projectile hits enemy
* Damage applied on impact

---

# 7. Health and Damage System

### Validation Steps

1. Unit receives damage
2. Health bar decreases
3. Unit dies at zero health
4. Death animation triggers

### Expected System Flow

```text
TakeDamage() → Health Reduced → Death Triggered
```

### Failure Conditions

* Unit becomes invincible
* Death animation not triggered
* Unit remains active after death

---

# 8. Animation Validation

All characters must support the following states:

| Animation    | Required |
| ------------ | -------- |
| Idle         | Yes      |
| Walk         | Yes      |
| Attack       | Yes      |
| Hit Reaction | Optional |
| Death        | Yes      |

### Test Checklist

* No animation freezing
* No looping attack bugs
* No animation popping

---

# 9. VR Interaction Validation

The following VR interactions must work reliably:

| Interaction      | Expected Result        |
| ---------------- | ---------------------- |
| Card selection   | Card highlights        |
| Ray targeting    | Spawn area detected    |
| Unit deployment  | Unit spawns instantly  |
| Energy deduction | Correct amount removed |

---

# 10. Battlefield Interaction

Characters must correctly interact with:

* Enemy units
* Enemy castle
* Lane obstacles

### Validation Rules

```text
Unit detects enemies
Unit attacks enemy
Unit proceeds when enemy dies
Unit attacks castle when lane clear
```

---

# 11. Castle Damage Validation

### Test

Spawn multiple units and confirm they attack the enemy castle.

Expected behavior:

* Units reach castle
* Attack animation triggers
* Castle health decreases

---

# 12. Stress Testing

### Scenario

Spawn **maximum allowed units**.

Test conditions:

| Metric       | Target  |
| ------------ | ------- |
| Units active | 40-60   |
| Frame rate   | 72+ FPS |
| Latency      | Stable  |

### Validation Result

Demo must remain **stable and responsive in VR**.

---

# 13. Visual Effects Validation

Ensure the following effects work:

| Effect     | Example              |
| ---------- | -------------------- |
| Attack VFX | Weapon swing         |
| Fire magic | Fire Demon ability   |
| Death VFX  | Dissolve or fall     |
| Spawn VFX  | Unit spawn indicator |

No missing references or broken effects allowed.

---

# 14. Audio Validation

Characters must trigger correct sounds:

| Event  | Audio           |
| ------ | --------------- |
| Spawn  | Spawn sound     |
| Attack | Weapon or spell |
| Hit    | Damage reaction |
| Death  | Death sound     |

Audio must not overlap excessively in large battles.

---

# 15. Performance Validation (VR)

### VR Requirements

| Metric       | Target    |
| ------------ | --------- |
| Frame Rate   | 72+ FPS   |
| Draw Calls   | Optimized |
| Memory Usage | Stable    |

Optimization checks:

* LOD switching
* Animation culling
* Object pooling

---

# 16. Demo Safety Checks

Characters must not:

* Fall through terrain
* Freeze mid-animation
* Attack infinitely
* Become unkillable
* Spawn outside battlefield

If any of these occur, the demo is **not approved**.

---

# 17. QA Validation Checklist

Before demo release:

* [ ] All cards spawn correct units
* [ ] Units move along lanes
* [ ] Combat works correctly
* [ ] Units die correctly
* [ ] Castle damage works
* [ ] VR controls responsive
* [ ] No crashes during battles
* [ ] Performance stable

---

# 18. Demo Approval Status

| Role              | Approval |
| ----------------- | -------- |
| Game Designer     | Pending  |
| Gameplay Engineer | Pending  |
| Technical Artist  | Pending  |
| QA Team           | Pending  |

When all validations pass:

```text
CHARACTERS APPROVED FOR DEMO BUILD
```

---

# End of Document
