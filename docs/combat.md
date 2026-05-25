# Combat

Combat should reward training, type matchups, skill choice, timing, equipment, consumable timing, and SP management. Tiers should matter because they create higher stat ceilings and stronger skill caps, but tier should not be a hard win/loss rule by itself.

## Combat Goals

- A creature near the top of one tier can threaten a creature near the bottom of the next tier.
- A one-tier disadvantage should be hard but playable with better training, type advantage, good timing, and SP management.
- A two-tier disadvantage should usually be a losing fight unless the lower-tier creature has major advantages, strong defensive timing, favorable status effects, and some luck.
- Combat is timeline-based, not strict alternating turns.
- Fast creatures using fast skills should sometimes act twice before a slower opponent acts again.
- No creature should ever become impossible to hit through Evasion alone.
- Equipment should create specialization without erasing tier differences.
- Consumables should provide tactical recovery or cures, but the one-consumable slot makes them limited.

## Core Combat Stats

Combat uses the stats from [Stats](./stats.md):

| Stat | Combat Use |
| ---- | ---------- |
| HP   | Damage capacity. A creature is defeated at 0 HP. |
| SP   | Resource spent on skills. Recharges during combat and exploration. |
| PATK | Increases damage from the Physical portion of a skill. |
| PDEF | Reduces damage from the Physical portion of a skill. |
| SATK | Increases damage from the Special portion of a skill. |
| SDEF | Reduces damage from the Special portion of a skill. |
| SPD  | Reduces time before the creature's next action. |
| EVA  | Reduces incoming hit chance, subject to hit chance clamps. |

Equipment from [Equipment](./equipment.md) can modify effective stats and skill values during combat.

## Tiers In Combat

Tiers from [Tiers](./tiers.md) do not directly multiply hit chance or damage. Their combat impact comes from stat caps, stronger skill defaults, ATP caps, and skill progression.

| Tier Gap | Expected Result |
| -------- | --------------- |
| Same tier | Mostly decided by stats, type matchup, skill quality, and decisions. |
| +1 enemy tier | Hard, but a trained lower-tier creature can win against an early or poorly matched higher-tier creature. |
| +2 enemy tiers | Very difficult. The lower-tier creature likely needs type advantage, status luck, strong defensive timing, and a large training edge. |
| +3 or more enemy tiers | Usually not practical unless the higher-tier creature is heavily weakened or constrained. |

This keeps a late Tier 2 creature capable of beating an early Tier 3 creature without making Tier 2 reliably competitive into Tier 4.

## Timeline Combat

Combat uses an action timeline. Each creature has a `nextActionAt` value. The creature with the lowest `nextActionAt` acts next.

### Starting Timeline

At combat start:

`nextActionAt = 0`

If multiple creatures are tied, the higher SPD creature acts first. If SPD is also tied, break the tie randomly.

### Action Delay

After a creature acts, add delay based on the chosen action's Attack Time (ATT) and the creature's Speed (SPD):

`Action Delay = clamp(20, 160, round(ATT x (100 / (100 + SPD / 2))))`

`nextActionAt += Action Delay`

Lower delay means the creature acts again sooner. ATT comes from [Skills](./skills.md), where the default is **80**, faster skills can reach **20** through three speed stages, and slower skills can exceed **80** when ATT is used to pay for upgrades.

### Timing Examples

| Creature | SPD | Skill ATT | Action Delay |
| -------- | --- | --------- | ------------ |
| Average creature, normal skill | 100 | 80 | 53 |
| Average creature, fast skill | 100 | 40 | 27 |
| Slow creature, normal skill | 40 | 80 | 67 |
| Fast creature, fast skill | 200 | 40 | 20 |
| Fast creature, slow heavy skill | 200 | 120 | 60 |

A fast creature using a fast skill can act twice before a slow creature using a normal or slow skill acts again.

### Turn Preview

The combat UI should eventually show the next ten action slots. This preview should simulate the timeline using each creature's current `nextActionAt`, SPD, active statuses, and selected or predicted skill ATT.

When the player highlights a skill, the preview should update to show how that skill changes upcoming action order.

## Turn Start

When a creature's action begins:

1. Recover SP equal to **5% of max SP**.
2. Resolve start-of-turn status checks.
3. Choose an action.
4. Pay SP costs.
5. Resolve the action.
6. Apply end-of-turn status ticks.
7. Add the action's timeline delay.

SP recovery cannot exceed max SP.

Equipment can modify max SP and turn-start SP recovery. Calculate max SP after equipment bonuses, then calculate recovery from that effective max SP.

## Basic Actions

Every creature has Basic Attack and Basic Defense. These are always available and cost no SP.

### Basic Attack

Basic Attack is a weak no-cost attack for finishing blows or conserving SP.

| Property | Value |
| -------- | ----- |
| ATP | 50% of the creature's tier default ATP |
| ATR | 100% Physical |
| ACC | 95 |
| ATT | 80 |
| SPC | 0 |
| TGT | 1 Enemy |
| TYP | Physical |

After Basic Attack resolves, the user recovers **10% of max SP**. This recovery is in addition to the 5% turn-start recovery.

### Basic Defense

Basic Defense is a no-cost defensive action for surviving a predicted heavy attack.

| Property | Value |
| -------- | ----- |
| ATT | 60 |
| SPC | 0 |
| TGT | Self |
| Effect | Guarded |

Guarded increases PDEF and SDEF by **50%** against the next incoming damaging skill. If the creature is not hit before its next action, Guarded expires when that next action begins.

After Basic Defense resolves, the user recovers **10% of max SP**. This recovery is in addition to the 5% turn-start recovery.

## SP Recovery Outside Combat

While walking around outside combat, SP gradually recovers up to **50% of max SP**. Equipment, food, medicine, traits, or other effects may change this exploration recovery cap.

Equipment that increases max SP also increases the value represented by the exploration cap. Equipment that specifically modifies the exploration cap changes the cap percentage before calculating the cap value.

## Equipment And Consumables

Each creature can carry one Equipment item and one Consumable item as described in [Equipment](./equipment.md).

### Equipment In Combat

Equipment modifiers are applied before combat starts and remain active while equipped.

| Modifier | Combat Timing |
| -------- | ------------- |
| Stat bonuses | Apply before timeline, hit, damage, HP, and SP calculations. |
| Skill ATP bonuses | Apply before ATP is split by ATR. |
| Skill ACC bonuses | Apply before ACC is clamped to 100 and before EVA is applied. |
| Skill SPC reductions | Apply before checking whether the user can afford the skill. |
| ATT modifiers | Apply before action delay is calculated. |
| Recovery modifiers | Apply when turn-start, basic-action, or exploration SP recovery is calculated. |

### Consumables In Combat

Using a consumable is a combat action unless the consumable says otherwise.

| Property | Default Value |
| -------- | ------------- |
| ATT | 60 |
| SPC | 0 |
| TGT | Self or 1 Ally, depending on item |

Consumables do not increase skill SKL. After use, the consumable slot is empty.

## Hit Chance

A skill's ACC is checked against the defender's EVA. Effective ACC includes SKL bonuses from [Skills](./skills.md), equipment modifiers, consumable modifiers, and temporary status modifiers. Effective ACC still caps at **100**, and final hit chance is clamped so attacks are never guaranteed and evasion never makes a creature impossible to hit.

### Evasion Penalty

`Evasion Penalty = min(40, 50 x (Defender EVA / (Defender EVA + 150)))`

This creates diminishing returns for EVA.

| Defender EVA | Evasion Penalty |
| ------------ | --------------- |
| 50 | 12.5 |
| 100 | 20.0 |
| 200 | 28.6 |
| 350 | 35.0 |
| 550 | 39.3 |

### Final Hit Chance

`Effective ACC = clamp(0, 100, Skill ACC + SKL ACC Bonus + Equipment ACC + Temporary ACC)`

`Final Hit Chance = clamp(10, 95, Effective ACC - Evasion Penalty + Hit Modifiers)`

`Hit Modifiers` includes status effects, ability effects, terrain, or other temporary combat modifiers not already included in Effective ACC.

The minimum final hit chance is **10%**. The maximum final hit chance is **95%**.

## Damage

Damage uses skill ATP, skill ATR, attacker offensive stats, defender defensive stats, equipment modifiers, type effectiveness, and a small luck range.

### Physical And Special Split

ATR from [Skills](./skills.md) determines how much of the skill is Physical or Special.

`Effective ATP = ATP + SKL ATP Bonus + Equipment ATP + Temporary ATP`

`Physical ATP = Effective ATP x (ATR / 100)`

`Special ATP = Effective ATP x (1 - ATR / 100)`

### Stat Multipliers

Physical damage compares effective PATK to effective PDEF:

`Physical Stat Multiplier = clamp(0.35, 1.85, sqrt(Effective Attacker PATK / Effective Defender PDEF))`

Special damage compares effective SATK to effective SDEF:

`Special Stat Multiplier = clamp(0.35, 1.85, sqrt(Effective Attacker SATK / Effective Defender SDEF))`

Use `1` as the minimum stat denominator if a stat is ever reduced to 0 by an effect.

### Base Damage

`Base Damage = (Physical ATP x Physical Stat Multiplier) + (Special ATP x Special Stat Multiplier)`

### Type Effectiveness

Apply the matchup multiplier from [Type Chart](./typechart.md):

`Typed Damage = Base Damage x Type Effectiveness`

Type effectiveness values currently use **0.5x**, **1x**, and **2x**.

### Damage Variance

Apply a small random variance after type effectiveness:

`Final Damage = max(1, round(Typed Damage x random(0.90, 1.10)))`

This variance is part of why a lower-tier creature can sometimes steal a close win, but it is not large enough to erase major tier gaps by itself.

### Guarded Damage

If the defender has Guarded from Basic Defense, multiply PDEF and SDEF by **1.5** before calculating damage. Guarded is consumed by the incoming damaging skill.

## Skill Effects And Status

Skills with ABL apply their type's common ability from [Abilities](./abilities.md) after the skill hits unless the target is immune or the ability fails due to a specific future rule.

Current common abilities are:

| Type | Ability |
| ---- | ------- |
| Oceanic | Freeze |
| Volcanic | Burn |
| Earthen | Constrict |
| Aerial | Paralyze |
| Crawly | Poison |
| Spooky | Sleep |
| Mental | Confuse |
| Physical | Stun |

Status durations are counted by the affected creature's actions on the timeline, not by full combat rounds. Poison and Burn tick at the end of the affected creature's action. Sleep, Freeze, Stun, Confuse, Constrict, and Paralyze can change whether the creature acts or how quickly future actions arrive.

## Training Hooks

Combat feeds the usage-based progression described in [Training](./training.md):

- Skill use can increase that skill's SKL by 1 when it is used successfully.
- Taking damage contributes HP training.
- Using skills contributes SP training.
- Hits that are at least 50% Physical contribute PATK or PDEF training.
- Hits that are at least 50% Special contribute SATK or SDEF training.
- Each combat contributes SPD training.
- Dodging attacks contributes EVA training.

Basic Attack and Basic Defense are baseline actions. They can contribute stat training, but they do not evolve through SKL unless they are later converted into normal tracked skills.

## Combat Resolution Order

Use this order when resolving a damaging skill:

1. Apply turn-start SP recovery.
2. Apply equipment, consumable, status, and temporary modifiers.
3. Confirm the user has enough SP after recovery and SPC modifiers.
4. Spend SP.
5. Roll hit chance using ACC vs EVA.
6. If the skill misses, apply miss-related training and timeline delay.
7. If the skill hits, calculate Physical and Special ATP split.
8. Apply Guarded if present.
9. Apply PATK/PDEF and SATK/SDEF stat multipliers.
10. Apply type effectiveness.
11. Apply damage variance.
12. Deal final damage, minimum 1.
13. Apply ABL status effects if the skill has an ability.
14. Apply training markers.
15. Add action delay from ATT and SPD.

## Balance Notes

- Skill ATT should be treated as a major power lever because it changes the action timeline, not just damage.
- Very fast skills should usually have lower ATP, lower ACC, higher SP cost, or some combination of those trade-offs.
- Very slow skills can justify higher ATP, better ACC, or an ABL because opponents may act before the user gets another turn.
- Type advantage is intentionally large at 2x and can let a lower-tier creature threaten a higher-tier creature.
- The hit chance clamp keeps high-EVA creatures evasive but never untouchable.
- SP recovery gives every creature fallback options, while Basic Attack and Basic Defense prevent dead turns when SP is low.
- Equipment bonuses should be visible in combat previews so players understand why hit chance, damage, SP recovery, or action timing changed.
- Consumables should be shown in the timeline preview as actions so players can see the cost of spending time to heal or cure.
