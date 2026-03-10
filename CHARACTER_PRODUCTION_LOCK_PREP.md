

## Overview

This document defines the final preparation steps required to **lock all characters for production**. Once completed, character assets should be considered **final and stable for integration**, animation, gameplay balancing, and deployment.

Production lock ensures:

* Visual consistency
* Rigging and animation compatibility
* Gameplay stat stability
* Performance optimization for runtime environments (VR / real-time engine)

---

# 1. Character List (Final Roster)

| Character        | Role           | Type       | Status       |
| ---------------- | -------------- | ---------- | ------------ |
| Knight           | Frontline Tank | Melee      | Pending Lock |
| Archer           | Ranged DPS     | Projectile | Pending Lock |
| Troll            | Heavy Unit     | Melee      | Pending Lock |
| Fire Demon       | High Damage    | Magic      | Pending Lock |
| Ice Guardian     | Defense Unit   | Magic      | Pending Lock |
| Skeleton Warrior | Swarm Unit     | Melee      | Pending Lock |

---

# 2. Final Model Requirements

Each character must include:

### Geometry

* Finalized mesh topology
* Target polygon count approved
* Clean edge flow for deformation
* No non-manifold geometry
* No n-gons (tri/quad only)

### Poly Budget (Example Targets)

| Unit Type          | Target Poly Count |
| ------------------ | ----------------- |
| Small Units        | 4k – 8k           |
| Standard Units     | 8k – 15k          |
| Boss / Heavy Units | 15k – 25k         |

---

# 3. Texture Requirements

### Texture Maps

Each character must include:

* Albedo / Base Color
* Normal Map
* Roughness Map
* Metallic Map (if required)
* Emissive Map (magic characters only)

### Texture Resolution

| Asset Type     | Resolution |
| -------------- | ---------- |
| Small Units    | 1024       |
| Standard Units | 2048       |
| Boss Units     | 4096       |

### Naming Convention

```
CHAR_<Name>_ALB
CHAR_<Name>_NRM
CHAR_<Name>_RGH
CHAR_<Name>_MET
CHAR_<Name>_EMS
```

Example:

```
CHAR_Knight_ALB
CHAR_Knight_NRM
```

---

# 4. Rigging Requirements

All characters must include:

* Final skeleton hierarchy
* Standard humanoid rig structure (where applicable)
* Consistent bone naming
* IK handles for arms/legs (optional)
* Root bone for gameplay control

### Required Bones

```
Root
Spine_01
Spine_02
Neck
Head
Clavicle_L / R
UpperArm_L / R
LowerArm_L / R
Hand_L / R
UpperLeg_L / R
LowerLeg_L / R
Foot_L / R
```

---

# 5. Animation Set (Minimum)

Each character must support the following animations:

| Animation    | Description         |
| ------------ | ------------------- |
| Idle         | Default stance      |
| Walk / Move  | Navigation movement |
| Attack       | Primary attack      |
| Hit Reaction | Damage response     |
| Death        | Death animation     |
| Ability      | Special attack      |

Optional:

* Cast
* Spawn
* Victory

---

# 6. Gameplay Data Lock

All gameplay values must be finalized.

| Character  | HP  | Attack | Attack Speed | Range | Cost |
| ---------- | --- | ------ | ------------ | ----- | ---- |
| Knight     | TBD | TBD    | TBD          | Melee | TBD  |
| Archer     | TBD | TBD    | TBD          | Long  | TBD  |
| Troll      | TBD | TBD    | Slow         | Melee | TBD  |
| Fire Demon | TBD | High   | Medium       | Magic | TBD  |

Once approved:

* Values move to **Gameplay Config File**
* Changes require **design review**

---

# 7. Collider Setup

Each character must include:

* Capsule collider for body
* Hitbox for damage detection
* Attack collider (for melee units)
* Projectile spawn point (ranged units)

Naming example:

```
COL_Body
COL_Attack
SOCKET_Projectile
```

---

# 8. VFX Hooks

Characters must contain predefined sockets for effects.

| Socket    | Usage                 |
| --------- | --------------------- |
| FX_Hand_L | Spell casting         |
| FX_Hand_R | Weapon effects        |
| FX_Head   | Aura / status effects |
| FX_Feet   | Movement effects      |

---

# 9. Performance Validation

All characters must pass runtime performance checks.

Checklist:

* No frame drops in battle scenes
* GPU memory usage validated
* LOD levels implemented
* Texture compression applied

### LOD Structure

| LOD  | Poly Reduction |
| ---- | -------------- |
| LOD0 | 100%           |
| LOD1 | 60%            |
| LOD2 | 30%            |

---

# 10. File Structure

```
/Characters
    /Knight
        Knight_Model.fbx
        Knight_Rig.fbx
        Knight_Textures
        Knight_Animations
    /Archer
    /Troll
    /FireDemon
```

---

# 11. Naming Convention

```
CHAR_<CharacterName>_<AssetType>
```

Examples:

```
CHAR_Knight_Model
CHAR_Knight_Rig
CHAR_Knight_Idle
CHAR_Archer_Attack
```

---

# 12. QA Checklist Before Lock

All characters must pass the following:

* [ ] Mesh clean
* [ ] UVs finalized
* [ ] Textures approved
* [ ] Rig tested
* [ ] Animations exported
* [ ] Gameplay stats confirmed
* [ ] Colliders configured
* [ ] VFX sockets added
* [ ] LODs created
* [ ] Performance tested

---

# 13. Production Lock Approval

| Role             | Name | Status  |
| ---------------- | ---- | ------- |
| Art Director     |      | Pending |
| Technical Artist |      | Pending |
| Game Designer    |      | Pending |
| QA               |      | Pending |

When all approvals are completed:

**Character Status → PRODUCTION LOCKED**

---

# 14. Post-Lock Policy

After production lock:

Allowed:

* Bug fixes
* Performance improvements

Not Allowed:

* Major design changes
* Model redesign
* Animation overhaul

Changes require **formal change request approval**.

---

# End of Document
