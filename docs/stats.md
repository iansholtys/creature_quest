# Companion Stats

Companion stats define combat performance, resource pools, timeline speed, and training direction. Stat values are bounded primarily by a creature's [Tier](./tiers.md), but equipment and temporary combat effects can modify effective values.

## Stat List

| ID | Name | Primary Use |
| -- | ---- | ----------- |
| HP | Hit Points | Determines how much damage a creature can take before defeat. |
| SP | Stamina Points | Resource spent to use skills and recovered during combat or exploration. |
| PATK | Physical Attack | Increases damage from the Physical portion of skills. |
| PDEF | Physical Defense | Reduces incoming Physical damage. |
| SATK | Special Attack | Increases damage from the Special portion of skills. |
| SDEF | Special Defense | Reduces incoming Special damage. |
| SPD | Speed | Reduces action delay on the combat timeline. |
| EVA | Evasion | Reduces incoming hit chance, subject to combat clamps. |

## Base Stats And Effective Stats

Base stats are the trained values stored on the creature. Effective stats are the values used by combat after equipment, statuses, consumables, terrain, or other temporary modifiers are applied.

`Effective Stat = max(1, Base Stat + Equipment Bonus + Temporary Modifier)`

HP and SP are resource stats. When max HP or max SP changes, current HP or current SP should be clamped to the new maximum.

## Tier Caps

Base stats cannot exceed the creature's tier max stat from [Tiers](./tiers.md). Equipment can temporarily push effective stats above tier caps, but this should be treated as borrowed power and not permanent training progress.

| Tier | Name | Base Stat Cap |
| ---- | ---- | ------------- |
| 1 | Baby | 50 |
| 2 | Basic | 100 |
| 3 | Greater | 200 |
| 4 | Elite | 350 |
| 5 | Legendary | 550 |

## Combat Formulas Using Stats

### Timeline Speed

SPD reduces the time before a creature's next action:

`Action Delay = clamp(20, 160, round(ATT x (100 / (100 + SPD / 2))))`

See [Combat](./combat.md) for timeline details.

### Damage Stats

Physical damage compares PATK to PDEF:

`Physical Stat Multiplier = clamp(0.35, 1.85, sqrt(Effective Attacker PATK / Effective Defender PDEF))`

Special damage compares SATK to SDEF:

`Special Stat Multiplier = clamp(0.35, 1.85, sqrt(Effective Attacker SATK / Effective Defender SDEF))`

### Evasion

EVA applies diminishing returns and cannot make a creature impossible to hit:

`Evasion Penalty = min(40, 50 x (Defender EVA / (Defender EVA + 150)))`

`Final Hit Chance = clamp(10, 95, Effective ACC - Evasion Penalty + Hit Modifiers)`

## Stat Roles

### HP

HP is survivability against all damage types. HP training comes from taking damage in combat.

### SP

SP determines how many skills a creature can use before relying on Basic Attack, Basic Defense, or SP recovery. SP also affects recovery values because turn-start recovery and basic-action recovery are percentage based.

### PATK And SATK

PATK and SATK matter based on a skill's [Attack Ratio](./skills.md). A skill with `ATR 100` uses only PATK. A skill with `ATR 0` uses only SATK. Mixed skills use both.

### PDEF And SDEF

PDEF and SDEF reduce incoming damage based on the attacker's physical/special split. Basic Defense temporarily increases both by 50% against the next damaging skill.

### SPD

SPD is a timeline stat, not a simple turn-order stat. High SPD can let a creature act repeatedly with fast low-ATT skills.

### EVA

EVA reduces hit chance but uses diminishing returns and hard clamps. High EVA creatures are evasive, not untouchable.

## Balance Notes

- HP and SP are strong because they change survivability and action economy.
- PATK/SATK are strongest when paired with high ATP skills and type advantage.
- PDEF/SDEF are strongest when paired with Basic Defense and defensive equipment.
- SPD is strongest when paired with low-ATT skills.
- EVA should be tested carefully because it changes expected damage over time.
