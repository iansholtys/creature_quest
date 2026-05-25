# Companion Types

Every creature and damaging skill has a type. Type controls theme, common abilities, and damage effectiveness through the [Type Chart](./typechart.md).

## Type Table

| Type | Common Themes | Common Ability | Description |
| ---- | ------------- | -------------- | ----------- |
| Oceanic | Water and Ice | Freeze | Creatures of sea, rivers, rain, frost, and deep pressure. They control flow, cold, and endurance. |
| Volcanic | Fire and Rock | Burn | Creatures of flame, magma, ash, and stone. They pressure enemies with heat and explosive force. |
| Earthen | Grass and Ground | Constrict | Creatures of soil, roots, vines, and stonebound life. They restrain, drain, and outlast foes. |
| Aerial | Flying and Electric | Paralyze | Creatures of sky, wind, storms, and lightning. They rely on speed, disruption, and precision. |
| Crawly | Bug and Poison | Poison | Creatures of insects, venom, toxins, and swarms. They win through attrition and pressure. |
| Spooky | Ghost and Dark | Sleep | Creatures of shadows, spirits, fear, and dreams. They interrupt opponents and distort tempo. |
| Mental | Psychic and Fairy | Confuse | Creatures of thought, charm, illusion, and willpower. They disrupt choices and punish mistakes. |
| Physical | Normal and Fighting | Stun | Creatures of raw force, martial skill, and direct impact. They favor clear pressure and reliable hits. |

## Creature Type

A creature's type defines its defensive matchup on the type chart and its likely signature ability. Future creatures may support dual types, but the current rules assume one type per creature.

## Skill Type

A skill's type defines its attacking matchup and its available common ability. A creature can learn off-type skills if future content allows it, but same-type skills should usually be the most thematic and common.

## Ability Pairing

The common type ability is documented in [Abilities](./abilities.md). A skill only applies the ability if it has the `ABL` property enabled and the skill hits.

## Design Notes

- Type identity should influence skill names, ability effects, and creature fantasy.
- Type advantage is intentionally strong at 2x damage.
- Type disadvantage at 0.5x damage can make a higher-tier matchup much harder.
- Equipment and consumables can cover weaknesses but should not erase type identity.
