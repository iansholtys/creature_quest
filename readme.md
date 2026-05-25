# Creature Quest

Creature Quest is a creature companion system built around usage-based growth, timeline combat, type matchups, custom skills, equipment, and tactical SP management.

Creatures do not use a traditional level system. Their long-term strength comes from tier limits, stat training, skill practice, innate talent, equipment, and the choices made in combat.

## Design Pillars

- Creatures improve by doing things, not by collecting generic experience points.
- Tiers define potential, but a tier gap should not be an automatic win or loss.
- Combat uses a timeline where `SPD` and skill `ATT` determine action order.
- Skills are built with explicit trade-offs between `ATP`, `ACC`, `ATT`, `SPC`, target coverage, and abilities.
- Types and abilities create meaningful matchup decisions.
- Equipment and consumables create specialization and tactical safety without replacing training.

## Core Documents

| Document | Purpose |
| -------- | ------- |
| [Tiers](./docs/tiers.md) | Creature rarity, stat ceilings, and expected tier gaps. |
| [Stats](./docs/stats.md) | Combat stats, stat meanings, and effective stat rules. |
| [Types](./docs/types.md) | The eight companion types and their themes. |
| [Type Chart](./docs/typechart.md) | Type effectiveness multipliers used in damage. |
| [Abilities](./docs/abilities.md) | Common status abilities associated with each type. |
| [Skills](./docs/skills.md) | Skill properties, progression, builder costs, and caps. |
| [Combat](./docs/combat.md) | Timeline combat, SP recovery, hit chance, damage, and resolution order. |
| [Equipment](./docs/equipment.md) | Creature equipment and consumable slots. |
| [Training](./docs/training.md) | Combat training, daily training, and dojo training. |
| [Innate Talent](./docs/innate-talent.md) | Growth dispositions and trait names. |

## Test Tools

The `test/` folder contains standalone HTML tools for balance testing. These files are not production UI.

| Tool | Purpose |
| ---- | ------- |
| [Skill Creator](./test/skill-creator.html) | Build and inspect skill values from the skill builder rules. |
| [Creature Creator](./test/creature-creator.html) | Build combat-ready creature JSON with stats, skills, equipment, and consumables. |

## Current Scope

These documents are a rules draft and balancing reference. Values are intended to be tested and adjusted as the combat simulator and game UI become more concrete.
