# Common Abilities

Each type from [Types](./types.md) is associated with a signature ability it can inflict on opponents. These abilities are modeled after classic status conditions found in creature collector games like Pokémon, and take effect when a skill with the corresponding ABL property hits its target.

## Ability Types

| Type     | Ability   | Description                                                                                              |
| -------- | --------- | -------------------------------------------------------------------------------------------------------- |
| Oceanic  | Freeze    | The target is encased in ice and cannot move until hit by a Fire-type attack or a thawing effect.         |
| Volcanic | Burn      | The target takes gradual damage each turn and suffers reduced Physical Attack for the duration.           |
| Earthen  | Constrict | The target's Speed is lowered, making it easier to outspeed. Severe cases may prevent action entirely.    |
| Aerial   | Paralyze  | The target's Speed drops significantly and has a chance to be fully paralyzed and skip its turn each round.|
| Crawly   | Poison      | The target takes gradual damage each turn. Certain variants can deal extra damage or stack over time.     |
| Spooky   | Sleep       | The target falls asleep and skips turns until it wakes up, which can happen naturally or when attacked.   |
| Mental   | Confuse     | The target attacks itself for a few turns with reduced accuracy, striking randomly between foes and self. |
| Physical | Stun        | The target is momentarily dazed and cannot act for one turn, similar to being flinched or frozen in place. |

## Duration & Recovery

- **Turn-Based**: Most abilities last for **3–5 turns** unless cured by an item or a healing skill.
- **Sleep**: Lasts **1–3 turns** but can be extended by certain Spooky-type skills.
- **Freeze**: Lasts until the target is hit by a Volcanic-type attack or a dedicated defrost ability.
- **Poison & Burn**: Tick at the end of each turn, dealing damage equal to a fraction of the target's max HP (typically 1/8 per tick).
- **Cure Methods**: Healing items, ally support skills, or switching out the affected creature can remove most status effects.

## Stacking Rules

- A creature can only have **one** primary status effect at a time (Freeze, Burn, Poison, Sleep, Paralyze).
- If hit by a new status while already afflicted, the new one replaces the old unless it fails its accuracy check.
- Confuse and Stun are considered secondary effects and can coexist with primary statuses in some cases.
