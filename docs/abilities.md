# Common Abilities

Common abilities are type-linked secondary effects that skills can apply through the `ABL` property. A skill with `ABL` attempts to apply its type's ability after the skill hits.

## Ability Table

| Type | Ability | Category | Description |
| ---- | ------- | -------- | ----------- |
| Oceanic | Freeze | Primary status | The target is encased in ice and cannot act until thawed or broken by a qualifying effect. |
| Volcanic | Burn | Primary status | The target takes damage over time and suffers reduced Physical Attack. |
| Earthen | Constrict | Control | The target's Speed is reduced, delaying future timeline actions. Severe forms may prevent action. |
| Aerial | Paralyze | Primary status | The target's Speed is reduced and it may lose actions to paralysis. |
| Crawly | Poison | Primary status | The target takes damage over time. Strong variants may stack or intensify later. |
| Spooky | Sleep | Primary status | The target skips actions until it wakes or is disturbed. |
| Mental | Confuse | Secondary status | The target may misdirect attacks, hit itself, or suffer reduced accuracy. |
| Physical | Stun | Secondary status | The target loses one upcoming action or has that action delayed. |

## Applying Abilities

1. The skill must have `ABL` enabled.
2. The skill must hit after ACC vs EVA is resolved.
3. The target must not be immune through equipment, consumables, traits, or future rules.
4. The ability applies after damage unless the ability specifically says it applies before damage.

## Suggested Default Durations

| Ability | Default Duration |
| ------- | ---------------- |
| Freeze | Until thawed, broken, or cured. |
| Burn | 3 affected creature actions. |
| Constrict | 3 affected creature actions. |
| Paralyze | 3 affected creature actions. |
| Poison | 4 affected creature actions. |
| Sleep | 1 to 3 affected creature actions. |
| Confuse | 2 to 4 affected creature actions. |
| Stun | 1 affected creature action. |

Durations are counted by the affected creature's actions on the [Combat](./combat.md) timeline, not by full combat rounds.

## Suggested Mechanical Defaults

These values are starting points for testing.

| Ability | Suggested Effect |
| ------- | ---------------- |
| Freeze | Target cannot act. Ends when hit by Volcanic damage, cured, or thawed by a future rule. |
| Burn | End-of-action damage equal to 1/8 max HP; PATK reduced by 20%. |
| Constrict | SPD reduced by 25%; future action delays are recalculated with reduced effective SPD. |
| Paralyze | SPD reduced by 40%; 20% chance to lose an action when acting. |
| Poison | End-of-action damage equal to 1/8 max HP. |
| Sleep | Target skips actions; taking damage may wake it depending on future tuning. |
| Confuse | 35% chance to misfire; confused attacks use reduced ACC. |
| Stun | Target's next action is skipped or delayed by one normal action delay. |

## Stacking Rules

- A creature can only have one primary status at a time: Freeze, Burn, Poison, Sleep, or Paralyze.
- If a new primary status applies while another primary status is active, the new status replaces the old one.
- Confuse and Stun are secondary statuses and can coexist with one primary status.
- Constrict is a control effect and can coexist unless a future rule classifies it as primary.
- Reapplying the same status refreshes duration unless a specific ability says otherwise.

## Cure Methods

| Method | Notes |
| ------ | ----- |
| Consumables | Antidotes, warming herbs, bitter roots, and similar items can remove specific statuses. |
| Skills | Future healing or support skills may cure one or more statuses. |
| Equipment | Equipment may grant immunity, resistance, or faster recovery. |
| Switching | If switching exists later, it may cure or pause some statuses. |

## Balance Notes

- Ability effects are powerful because they interact with the action timeline.
- Sleep, Freeze, and Stun should be watched carefully because they deny actions.
- Burn and Poison are attrition tools and become stronger in long fights.
- Constrict and Paralyze are tempo tools and become stronger with fast allies or slow enemy skills.
