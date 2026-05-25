# Training

Creature Quest does not use a traditional experience and level system. Creatures improve through usage, daily training, innate talent, and long-term care.

Training is split into three systems:

| System | When It Happens | Purpose |
| ------ | --------------- | ------- |
| Combat Training | After combat | Rewards stats and skills used during battle. |
| Daily Training Regimen | During rest or downtime | Lets players guide long-term growth ratios. |
| Dojos | While creatures are away from the party | Lets unused companions keep progressing slowly. |

## Combat Training

Combat training records what happened during the fight, then applies stat growth after combat ends. This prevents stat changes from shifting formulas mid-fight.

### Stat Training Values

| Stat | Training Trigger | Growth |
| ---- | ---------------- | ------ |
| HP | Creature takes damage. | +0.05 |
| SP | Creature uses a skill. | +0.025 |
| PATK | Creature hits with an attack that is at least 50% Physical. | +0.05 |
| PDEF | Creature is hit by an attack that is at least 50% Physical. | +0.05 |
| SATK | Creature hits with an attack that is at least 50% Special. | +0.05 |
| SDEF | Creature is hit by an attack that is at least 50% Special. | +0.05 |
| SPD | Creature participates in combat. | +0.1 per combat |
| EVA | Creature dodges an attack. | +0.1 |

Growth values are fractional progress toward the next stat point. The exact implementation can store fractional progress separately from whole stat values.

### Combat Training Rules

- Training is based on actual combat events, not intent.
- A missed attack does not train PATK or SATK, but it can still count as skill use if SP was spent and the skill was attempted.
- Basic Attack can train PATK because it is 100% Physical.
- Basic Defense can contribute defensive learning if it helps absorb a hit, but it should not train a normal skill's SKL.
- Damage over time from Poison or Burn can train HP for the victim, but should not train the attacker's PATK or SATK unless a future rule explicitly says it does.
- Equipment bonuses do not increase base stat caps, but using equipment in combat can still create training opportunities.

## Skill Use In Combat

Each skill tracks `SKL`, or skill level, separately from creature stats.

| Event | SKL Result |
| ----- | ---------- |
| Skill is used successfully | +1 SKL |
| Skill misses | No SKL by default; this can be revisited if misses feel too punishing. |
| Basic Attack or Basic Defense | No SKL unless converted into tracked skills later. |
| Consumable use | No SKL. |

SKL bonuses and evolution thresholds are documented in [Skills](./skills.md).

## Daily Training Regimen

Every night, and during meaningful downtime, companions grow through daily training. Daily training distributes a pool of growth points across stats according to an assigned percentage ratio.

### Default Daily Growth

The baseline daily pool is **1 stat point worth of growth** distributed by ratio. Food, medicine, equipment, facilities, story effects, or future systems may increase this pool.

### Allocation Rules

- Each stat normally has an assignable range of 5% to 20%.
- The total allocation across all eight stats must equal 100%.
- [Innate Talent](./innate-talent.md) modifies allocation ranges for positive and negative stats.
- A positive innate stat can be assigned up to 30%.
- A negative innate stat can be assigned up to 10%.
- Daily training cannot raise a base stat above the creature's tier cap.

### Example Allocation

For a creature with Mighty (PATK positive) and Weary (SP negative):

| Stat | Example Allocation |
| ---- | ------------------ |
| HP | 11% |
| SP | 9% |
| PATK | 25% |
| PDEF | 11% |
| SATK | 11% |
| SDEF | 11% |
| SPD | 11% |
| EVA | 11% |

This totals 100%, leans into the positive trait, and respects the reduced SP maximum.

## Dojos

Dojos let companions outside the active party continue to train while the player travels.

### Dojo Rules

- A dojo has a limited number of creature slots.
- A creature assigned to a dojo does not receive combat training from the active party's battles.
- Dojo growth is slower than normal daily training unless upgraded by facilities, teachers, or story rewards.
- Dojos can eventually help a creature reach tier stat caps, but they should take time.

## Training Caps

Base stats cannot exceed the tier max stat from [Tiers](./tiers.md). If training would exceed the cap, excess growth can be discarded or stored only if a future tier-up/evolution system supports it.

## Balance Notes

- Combat training rewards specialization but should not punish defensive or support play.
- Daily training lets players correct unlucky combat usage over time.
- Innate talent should guide growth identity, not lock a creature into one build forever.
- Dojos are a catch-up system, not a replacement for actively using companions.
