# Companion Skills

Skills are the primary combat actions creatures use beyond Basic Attack, Basic Defense, consumables, and future special actions. A skill is defined by power, accuracy, timing, cost, target, type, and optional ability effects.

## Skill Properties

| ID | Name | Description |
| -- | ---- | ----------- |
| ATP | Attack Power | Raw skill power before stat multipliers and type effectiveness. |
| ATR | Attack Ratio (%) | Percentage split between Physical and Special damage. |
| ACC | Accuracy | Base hit chance before EVA and final combat clamps. |
| ATT | Attack Time | How long the skill takes to resolve on the combat timeline. Lower is faster. |
| TGT | Target Type | Who the skill affects. |
| SPC | SP Cost | Stamina Points consumed to use the skill. |
| SKL | Skill Level | Usage-based progression for the individual skill. |
| ABL | Ability | Optional secondary effect such as Burn, Poison, or Stun. |
| T# | Tier | Skill tier used for builder defaults, costs, and caps. |
| TYP | Type | Elemental type from [Types](./types.md). |

## Property Details

### Attack Power (ATP)

ATP is the skill's base power. It is not final damage by itself. Combat damage also uses `ATR`, offensive and defensive stats, type effectiveness, equipment, and variance.

### Attack Ratio (ATR)

ATR determines the Physical/Special split.

| ATR | Meaning |
| --- | ------- |
| 100 | Fully Physical. Uses PATK vs PDEF. |
| 50 | Half Physical, half Special. Uses both stat pairs. |
| 0 | Fully Special. Uses SATK vs SDEF. |

### Accuracy (ACC)

ACC is the skill's accuracy before defender EVA and combat clamps. ACC caps at **100** before the final hit chance formula.

### Attack Time (ATT)

ATT determines how soon the user can act again after using the skill.

| ATT | Feel |
| --- | ---- |
| 20 | Extremely fast. Can create repeated actions with high SPD. |
| 40 | Fast. Useful for tempo and finishing. |
| 80 | Default speed. |
| 120 | Slow heavy action. |
| 140+ | Very slow. Must justify the delay with power, accuracy, ability, or coverage. |

The default ATT is **80**. Lower ATT values are faster and must be paid for through the builder. Faster ATT can be taken up to **3 stages**, each reducing ATT by 20.

Increasing ATT by **+20** makes a skill slower. Each slower ATT stage can pay for one ATP, ACC, or ABL upgrade stage instead of paying with SP Cost or ACC.

### Type (TYP)

Every damaging skill belongs to a type from [Types](./types.md). Damage effectiveness is calculated using the [Type Chart](./typechart.md).

### Ability (ABL)

ABL means the skill can apply its type's common ability from [Abilities](./abilities.md). Ability effects apply only after the skill hits unless a specific skill says otherwise.

## Skill Progression

### Skill Level (SKL)

Each time a skill is used successfully, its SKL increases by **1**. The maximum SKL value is **500**.

### SKL Bonuses

| Bonus Type | Formula | Maximum Effect |
| ---------- | ------- | -------------- |
| ATP Bonus | `0.04 x SKL` | +20 ATP |
| ACC Bonus | `0.04 x SKL` | +20 ACC |
| SPC Reduction | `-1 x ((Base SPC / 2) / 500) x SKL` | Up to 50% SP cost cut |

SKL bonuses are applied before [Equipment](./equipment.md) and temporary combat modifiers unless a future rule specifies a different order.

### Skill Evolution

Skills can evolve into more powerful variants once they reach their tier's SKL threshold.

| Tier | SKL Threshold |
| ---- | ------------- |
| 1 | 50 |
| 2 | 100 |
| 3 | 200 |
| 4 | 350 |

Tier 5 skills do not currently have a documented evolution threshold. They may instead be final forms or require unique story conditions.

## Skill Builder System

The builder ratio system ties improvements to SP Cost, Accuracy, and Attack Time trade-offs. All values are tier-dependent.

### Default Values By Tier

| Stat | Tier 1 | Tier 2 | Tier 3 | Tier 4 | Tier 5 |
| ---- | ------ | ------ | ------ | ------ | ------ |
| ATP | 10 | 20 | 50 | 70 | 90 |
| ACC | 90 | 90 | 90 | 90 | 90 |
| ATT | 80 | 80 | 80 | 80 | 80 |
| SP Cost | 3 | 10 | 20 | 30 | 40 |

### Improvement Costs

| Improvement | Tier 1 | Tier 2 | Tier 3 | Tier 4 | Tier 5 |
| ----------- | ------ | ------ | ------ | ------ | ------ |
| Cost for +10 ACC or adding an ABL | 5 | 10 | 15 | 20 | 30 |
| Cost per ATP stage | 3 | 6 | 12 | 18 | 24 |
| Cost per -20 ATT speed stage | 3 | 6 | 12 | 18 | 24 |
| ACC reduction per ACC-paid stage | 15 | 15 | 15 | 15 | 15 |
| Bonus ATP gained per stage | 3 | 6 | 10 | 16 | 22 |

### Stage Payment Options

ATP stages, +10 ACC stages, ABL stages, and -20 ATT speed stages may be paid for with SP Cost or ACC penalties. For mixed costs, each stage can choose its own payment method.

Slower ATT stages can also pay for ATP, +10 ACC, or ABL upgrades. Each **+20 ATT** stage pays for one upgrade stage. Slower ATT stages do not pay for faster ATT stages or wider target coverage.

### Target Type Cost

Adding wider target coverage increases the SP or ACC cost in stages.

| Target | Stage Cost | Notes |
| ------ | ---------- | ----- |
| 1 Enemy | 0 | Default offensive target. |
| Self | +1 | Common for buffs, heals, or defensive actions. |
| Everyone | +2 | Affects all creatures, including allies and enemies. |
| All Enemies | +3 | Strong offensive coverage. |
| All Allies | +3 | Strong support coverage. |

Target stages can be paid with SP Cost or ACC penalties. They cannot be paid by slower ATT under the current builder rules.

## Tier Maximums

### ATP Caps

| Tier | Max ATP |
| ---- | ------- |
| 1 | 25 |
| 2 | 50 |
| 3 | 100 |
| 4 | 150 |
| 5 | 200 |

ATP caps apply to builder-created base ATP. SKL bonuses, equipment, and temporary combat modifiers can raise effective ATP above this cap.

## Worked Builder Example

A Tier 2 Aerial skill starts with:

| Property | Value |
| -------- | ----- |
| ATP | 20 |
| ACC | 90 |
| ATT | 80 |
| SPC | 10 |

The designer adds:

- +2 ATP stages for +12 ATP.
- +1 ACC stage for +10 ACC.
- ABL for Paralyze.
- -1 ATT speed stage, making ATT 60.

If the designer pays one ATP stage with ACC, one ATP stage with SP, the ACC stage with SP, the ABL with +20 ATT, and the ATT speed stage with SP:

| Property | Result |
| -------- | ------ |
| ATP | 32 |
| ACC | 85 |
| ATT | 80 |
| SPC | 28 |
| ABL | Paralyze |

The skill became stronger and gained an ability, but its ATT returned to default because the ability was paid for by slowing it back down.

## Export Shape

A test or implementation skill can use this shape:

```json
{
  "name": "Storm Pin",
  "tier": 2,
  "type": "Aerial",
  "target": "1 Enemy",
  "atp": 32,
  "acc": 85,
  "att": 80,
  "spCost": 28,
  "attackRatioPhysicalPercent": 50,
  "ability": "Paralyze",
  "skillLevel": 0
}
```

## Balance Notes

- ATT is a major power lever because it changes how often a creature acts.
- ACC is strongest when paired with high ATP or dangerous abilities.
- SP Cost matters more in long fights because SP recovery is percentage based.
- Wider targets should be expensive because they multiply value across multiple creatures.
- Low-ATP fast skills are useful for finishing blows and timeline manipulation.
