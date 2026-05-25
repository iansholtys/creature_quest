# Type Chart

The type chart determines damage effectiveness after base damage has been calculated. Look up the defender's type as the row and the attacker's skill type as the column.

## Effectiveness Matrix

| Defender / Attacker | Oceanic | Volcanic | Earthen | Aerial | Crawly | Spooky | Mental | Physical |
| ------------------- | ------- | -------- | ------- | ------ | ------ | ------ | ------ | -------- |
| Oceanic | 1 | 2 | 1 | 0.5 | 1 | 1 | 0.5 | 2 |
| Volcanic | 0.5 | 1 | 2 | 1 | 1 | 0.5 | 2 | 1 |
| Earthen | 1 | 0.5 | 1 | 2 | 0.5 | 2 | 1 | 1 |
| Aerial | 2 | 1 | 0.5 | 1 | 2 | 1 | 1 | 0.5 |
| Crawly | 1 | 1 | 2 | 0.5 | 1 | 1 | 2 | 0.5 |
| Spooky | 1 | 2 | 0.5 | 1 | 1 | 1 | 0.5 | 2 |
| Mental | 2 | 0.5 | 1 | 1 | 0.5 | 2 | 1 | 1 |
| Physical | 0.5 | 1 | 1 | 2 | 2 | 0.5 | 1 | 1 |

## Multipliers

| Value | Meaning |
| ----- | ------- |
| 2 | Strong advantage. Damage is doubled. |
| 1 | Neutral matchup. Damage is unchanged. |
| 0.5 | Resistance. Damage is halved. |

## Combat Order

Type effectiveness is applied after ATP, ATR, PATK/SATK, and PDEF/SDEF are calculated, but before random damage variance.

`Typed Damage = Base Damage x Type Effectiveness`

## Reading Examples

- Volcanic attacking Oceanic is 2x because the Oceanic defender row and Volcanic attacker column is `2`.
- Oceanic attacking Volcanic is 0.5x because the Volcanic defender row and Oceanic attacker column is `0.5`.
- Aerial attacking Earthen is 2x because the Earthen defender row and Aerial attacker column is `2`.
- Physical attacking Spooky is 2x because the Spooky defender row and Physical attacker column is `2`.

## Balance Notes

- A 2x matchup can let a lower-tier creature threaten a higher-tier creature.
- A 0.5x matchup can make even a strong skill feel inefficient.
- Type advantage should be visible in combat previews before a player commits to a skill.
- If dual types are added later, define whether multipliers stack, average, or use the strongest value.
