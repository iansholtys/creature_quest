# Innate Talent

Innate talent is a creature's natural growth disposition. It does not directly change current combat stats. Instead, it changes how easily the creature can grow certain stats through [Training](./training.md).

Each creature randomly receives one positive growth trait and one negative growth trait. If both traits affect the same stat, they cancel out and the creature is considered Balanced.

## Growth Modifier

| Trait Type | Growth Change |
| ---------- | ------------- |
| Positive | +10% growth allocation range for the selected stat. |
| Negative | -10% growth allocation range for the selected stat. |
| Balanced | No growth modifier. |

In daily training, assignable stat percentages normally range from 5% to 20%. A positive trait can raise that stat's maximum to 30%. A negative trait can lower that stat's maximum to 10%.

## Trait Names

| Stat | Positive (+10%) | Negative (-10%) |
| ---- | --------------- | --------------- |
| HP | Vitalized | Frail |
| SP | Enduring | Weary |
| PATK | Mighty | Feeble |
| PDEF | Ironclad | Brittle |
| SATK | Arcane | Dull |
| SDEF | Warded | Exposed |
| SPD | Swift | Sluggish |
| EVA | Elusive | Clumsy |
| N/A | Balanced | Balanced |

## Examples

- Mighty / Weary means PATK is easier to emphasize, but SP is harder to emphasize.
- Swift / Brittle means SPD can grow aggressively, but PDEF cannot receive as much daily training focus.
- Vitalized / Vitalized cancels out and becomes Balanced.

## Random Generation

For simple generation:

1. Roll one stat for the positive trait.
2. Roll one stat for the negative trait.
3. If the stats match, set both trait names to Balanced.
4. Otherwise, apply the corresponding trait names and growth allocation modifiers.

## Combat Notes

- Innate talent should not modify hit chance, damage, SP recovery, or timeline speed directly.
- Its combat impact appears over time because trained stats eventually differ.
- Equipment can temporarily cover a bad innate talent, but it does not change the growth disposition.
