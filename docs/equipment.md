# Creature Equipment

Each creature can carry one Equipment item and one Consumable item. Equipment provides persistent modifiers while equipped. Consumables are single-use items that can be used during combat or exploration.

## Slots

| Slot | Limit | Purpose |
| ---- | ----- | ------- |
| Equipment | 1 item | Persistent stat, skill, combat, or recovery modifier. |
| Consumable | 1 item | One-time healing, curing, SP recovery, or emergency combat effect. |

Creatures cannot equip multiple equipment items unless a future rule explicitly increases slot count.

## Equipment Effects

Equipment should usually improve one combat axis and avoid solving every weakness at once.

| Effect Type | Examples |
| ----------- | -------- |
| Stat Bonus | `+10 PATK`, `+15 SP`, `+8 SPD` |
| Skill Bonus | `+5 ACC`, `+8 ATP`, `-5 SPC` |
| Recovery Bonus | `+5% turn-start SP recovery`, `+10% exploration SP recovery cap` |
| Defensive Bonus | `+10 PDEF`, `+10 SDEF`, `+5 EVA` |
| Conditional Bonus | `+10 ACC when below 50% HP`, `+10 ATP for Oceanic skills` |

## Recommended Equipment Scale

Equipment should scale by tier so lower-tier equipment is useful without letting equipment erase tier gaps.

| Tier | Minor Bonus | Major Bonus |
| ---- | ----------- | ----------- |
| 1 | +3 stat or +2 skill value | +5 stat or +4 skill value |
| 2 | +6 stat or +4 skill value | +10 stat or +7 skill value |
| 3 | +10 stat or +7 skill value | +18 stat or +12 skill value |
| 4 | +16 stat or +10 skill value | +28 stat or +18 skill value |
| 5 | +24 stat or +15 skill value | +40 stat or +25 skill value |

`ATP`, `ACC`, and `SPC` are skill values. `HP`, `SP`, `PATK`, `PDEF`, `SATK`, `SDEF`, `SPD`, and `EVA` are creature stats.

## Equipment Modifier Rules

- Equipment stat bonuses apply before combat starts and can increase effective stats above normal trained values.
- Equipment cannot raise effective ACC above **100** before the final hit chance clamp.
- Equipment can raise skill ATP above tier skill caps, but large ATP bonuses should be treated as major equipment effects.
- Equipment can reduce SPC, but final skill SP Cost should not go below **0**.
- Equipment can alter ATT, but ATT should still use the combat delay clamp from [Combat](./combat.md).
- Equipment can change exploration SP recovery caps, but cannot increase current SP above max SP.

## Modifier Order

Apply equipment before combat actions are resolved:

1. Start with the creature's trained base stats.
2. Apply equipment stat bonuses to produce effective stats.
3. Apply skill SKL bonuses to the selected skill.
4. Apply equipment skill bonuses to ATP, ACC, SPC, or ATT.
5. Apply temporary combat modifiers from statuses, consumables, terrain, or future effects.
6. Clamp values according to the relevant combat formula.

This order keeps permanent training, skill mastery, equipment, and temporary effects distinct.

## Suggested Equipment Shape

Equipment can be represented with explicit modifier fields:

```json
{
  "id": "focus_charm",
  "name": "Focus Charm",
  "tier": 1,
  "modifiers": {
    "stats": {},
    "skillAtp": 0,
    "skillAcc": 4,
    "skillSpCost": 0,
    "skillAtt": 0,
    "turnStartSpRecoveryPercent": 0,
    "basicActionSpRecoveryPercent": 0,
    "explorationSpCapPercent": 0
  }
}
```

Positive `skillSpCost` increases SP Cost. Negative `skillSpCost` reduces SP Cost. Final SP Cost cannot go below 0.

## Consumables

Consumables are carried by a creature and are consumed when used.

| Consumable Type | Examples |
| --------------- | -------- |
| Healing | Restore 25% HP, restore flat HP |
| SP Recovery | Restore 25% SP, restore flat SP |
| Cure | Remove Poison, Burn, Sleep, Freeze, Paralyze, Confuse, or Stun |
| Defensive | Apply Guarded, reduce next incoming damage |
| Offensive | Temporarily increase ACC, ATP, PATK, or SATK |

## Consumable Timing

Using a consumable is a combat action unless a specific item says otherwise.

| Property | Default Value |
| -------- | ------------- |
| ATT | 60 |
| SPC | 0 |
| TGT | Self or 1 Ally, depending on item |

The user still receives normal 5% turn-start SP recovery before using a consumable. Consumables do not trigger skill SKL growth.

## Suggested Consumable Shape

```json
{
  "id": "small_tonic",
  "name": "Small Tonic",
  "att": 60,
  "target": "Self",
  "consumeOnUse": true,
  "effects": {
    "restoreHpPercent": 25,
    "restoreSpPercent": 0,
    "cures": []
  }
}
```

Consumables should be visible in timeline previews because using one costs action time.

## Consumable Use Rules

- A creature can use its held consumable on its own action.
- The consumable is removed after use, even if the effect has no value because the target is already healthy or cured.
- Healing and SP recovery cannot exceed max HP or max SP.
- Cure consumables remove only the statuses listed in their effect.
- Consumables can target allies only if their `TGT` allows it.
- Consumables do not train skills and do not count as skill use for SKL.

## Example Equipment

| Name | Tier | Effect |
| ---- | ---- | ------ |
| Focus Charm | 1 | +4 skill ACC |
| Power Band | 2 | +7 skill ATP |
| Stamina Bell | 2 | +10 SP |
| Quick Anklet | 3 | +12 SPD |
| Deep Reservoir | 3 | +10% exploration SP recovery cap |
| Guard Shell | 4 | +22 PDEF and +22 SDEF |
| Apex Lens | 5 | +15 skill ACC, +10 skill ATP |

## Example Consumables

| Name | Effect |
| ---- | ------ |
| Small Tonic | Restore 25% HP |
| Stamina Drop | Restore 25% SP |
| Antidote | Cure Poison |
| Warming Herb | Cure Freeze |
| Bitter Root | Cure Sleep or Confuse |
| Guard Powder | Apply Guarded until the next incoming damaging skill |

## Balance Notes

- Equipment should make a creature feel specialized, not universally stronger.
- Accuracy equipment is powerful because hit chance is clamped after EVA and modifiers.
- ATP equipment is powerful because it scales through PATK/SATK and type effectiveness.
- SP equipment is powerful because it increases max SP, turn-start recovery, and basic-action recovery.
- Consumables create tactical safety but are limited by the one-consumable slot.
