# ENGINE FLAG MAPPING (Unity Card System)

This document defines all engine flags required to convert character cards into Unity-ready data objects.
All characters must have locked stats + clear engine flags with no ambiguity.

---

## 1) Combat Type Flags

### isMelee (bool)
TRUE if unit attacks in close range (Range <= 2.0)

### isRanged (bool)
TRUE if unit attacks from distance (Range > 2.0)

### isTank (bool)
TRUE if unit has high survivability for its elixir tier.

General Rule:
- HP >= 900 for 4 elixir
- HP >= 1300 for 5 elixir
- HP >= 1800 for 6 elixir

---

## 2) aggressionProfile (enum)

Defines combat personality and movement style.

Allowed Values:
- Defensive (holds position, safer AI)
- Balanced (normal attack and defense)
- Aggressive (pushes lane quickly)
- Assassin (targets weak backline)
- Support (stays behind allies, utility role)

---

## 3) karmaTag (enum)

Defines karma alignment.

Allowed Values:
- Aggressive
- Defensive
- Disciplined
- Risk

---

## 4) aiPriorityClass (enum)

Defines what the AI prefers to target first.

Allowed Values:
- TowerPusher (prioritizes tower)
- BacklineHunter (targets weak/ranged units)
- TankBreaker (targets high HP units)
- CrowdControl (targets groups)
- Balanced (normal targeting)
- SupportCaster (plays safe behind frontline)

---

## 5) Mapping Logic Rules

### Troops
- Usually Aggressive or Balanced
- aiPriorityClass often TowerPusher or Balanced

### Champions
- Stronger combat identity
- aiPriorityClass often BacklineHunter / TankBreaker

### Spirits
- Low-cost utility
- aiPriorityClass often Balanced or SupportCaster

### Buildings
- Always Defensive
- Always isTank: true
- MovementSpeed: None

### Spells
- No movement
- Damage is instant or AoE
- AttackCooldown refers to spell cast delay

---

## 6) Final Requirement

All characters must contain:
- isMelee / isRanged / isTank
- aggressionProfile
- karmaTag
- aiPriorityClass

No placeholder values are allowed.
