# Companion Skills

Every skill is defined by a set of core properties that determine how it behaves in battle.

## Skill Properties

| ID  | Name             | Description                                      |
| --- | ---------------- | ------------------------------------------------ |
| ATP | Attack Power     | Raw damage dealt by the skill.                   |
| ATR | Attack Ratio (%) | Percentage split between Physical and Special.   |
| ACC | Accuracy         | Base hit chance before to-hit calculations.      |
| TGT | Target Type      | Who the skill affects (single, self, all, etc.). |
| SPC | SP Cost          | Stamina Points consumed to use the skill.        |
| SKL | Skill Level      | Experience tracker for individual skills.         |
| ABL | Ability          | Secondary effects like Burn, Heal, etc.          |
| T#  | Tier             | The tier level of the skill.                     |
| TYP | Type             | Elemental type from [Types](./types.md).         |

---

## Property Details

### Accuracy (ACC)
The base probability that an attack will land before the final to-hit formula is applied. Values cap at **100**.

### Attack Ratio (ATR)
Determines the split between Physical and Special damage. A ratio of 100% means fully Physical, while 0% means fully Special.

### Type (TYP)
Every skill belongs to one of the types defined in [Types](./types.md). Damage effectiveness is calculated according to the [Type Chart](./typechart.md).

---

## Skill Progression

### Skill Level (SKL)
Each time a skill is used successfully, its SKL increases by **1**. The maximum SKL value is **500**.

#### SKL Bonuses
As a skill's level grows, it receives the following bonuses:

| Bonus Type  | Formula                                              | Maximum Effect          |
| ----------- | ---------------------------------------------------- | ----------------------- |
| ATP Bonus   | `0.04 × SKL`                                         | +20 ATP                 |
| ACC Bonus   | `0.04 × SKL`                                         | +20 ACC                 |
| SPC Reduction | `-1 × ((Base SPC / 2) / 500) × SKL`               | Up to 50% SP cost cut   |

### Skill Evolution
Skills can evolve into more powerful variants once they reach their tier's SKL cap. Evolution thresholds are:

| Tier | SKL Threshold |
| ---- | ------------- |
| 1    | 50            |
| 2    | 100           |
| 3    | 200           |
| 4    | 350           |

When a skill hits its threshold, it may evolve into an upgraded version with improved stats or new effects.

---

## Skill Builder System

To keep custom skills balanced, a builder ratio system ties stat improvements to SP Cost and Accuracy trade-offs. All values are tier-dependent.

### Default Values by Tier

| Stat       | Tier 1 | Tier 2 | Tier 3 | Tier 4 | Tier 5 |
| ---------- | ------ | ------ | ------ | ------ | ------ |
| ATP        | 10     | 20     | 50     | 70     | 90     |
| ACC        | 90     | 90     | 90     | 90     | 90     |
| SP Cost    | 3      | 10     | 20     | 30     | 40     |

### Improvement Costs (SP paid per stage)

| Improvement                              | Tier 1 | Tier 2 | Tier 3 | Tier 4 | Tier 5 |
| ---------------------------------------- | ------ | ------ | ------ | ------ | ------ |
| Cost for +10 ACC or adding an ABL        | 5      | 10     | 15     | 20     | 30     |
| Cost per ATP stage                       | 3      | 6      | 12     | 18     | 24     |
| ACC reduction per ATP stage              | 15     | 15     | 15     | 15     | 15     |
| Bonus ATP gained per stage               | 3      | 6      | 10     | 16     | 22     |

### Target Type Cost (in stages)

Adding wider target coverage increases the SP or ACC cost in stages:

| Target       | Stage Cost |
| ------------ | ---------- |
| 1 Enemy      | 0 (base)   |
| Self         | +1 stage   |
| Everyone     | +2 stages  |
| All Enemies  | +3 stages  |
| All Allies   | +3 stages  |

---

## Tier Maximums

### ATP Caps

| Tier | Max ATP |
| ---- | ------- |
| 1    | 25      |
| 2    | 50      |
| 3    | 100     |
| 4    | 150     |
| 5    | 200     |
