# **Attributes & Abilities**

---

Any cosmetic can grant real gameplay effects while equipped. Configure these in the [Dev Studio](Dev Studio.md) cosmetic editor (**Status & Combat** and **Special Effects** sections).

---

## **Status & Combat**

| Field | Effect |
| :--- | :--- |
| **Armor Points** (`armor`) | Adds armor points (like wearing armor). Shown in the tooltip as 🛡. |
| **Toughness** (`toughness`) | Adds armor toughness. Shown as ❈. |
| **Max Durability** (`maxDurability`) | If > 0, the physical item shows a durability bar. **Cosmetic only** — it never actually breaks. |

---

## **Flight**

| Field | Effect |
| :--- | :--- |
| **Allows Flight?** (`EnableFly`) | Grants creative-style flight while equipped. Removed cleanly when unequipped (unless the player is in Creative/Spectator). |
| **Fly Speed** (`flySpeedMultiplier`, default 1.0) | Multiplies flight speed. `2.0` = twice as fast. |

The player sees an action-bar `✈ Flight enabled/disabled` message (text configurable in `lang/messages.json`).

---

## **Movement speed**

| Field | Effect |
| :--- | :--- |
| **Ground Speed** (`groundSpeedMultiplier`, default 1.0) | Walk/run speed multiplier on the ground. |
| **Swim Speed** (`swimSpeedMultiplier`, default 1.0) | Swim speed multiplier in water. |

If a player wears several cosmetics with a speed bonus, only the **highest** multiplier applies (they don't stack or multiply). The same "highest wins" rule applies to passive potion effects.

---

## **Auto-Feed**

**Auto-Feed** (`AutoFeed`) — keeps the player's hunger topped up while the cosmetic is worn.

---

## **Passive potion effects**

**Special Effects → Select Effects** opens a grid of every Minecraft status effect. Click one to cycle its level (`OFF → I → II → III → IV → V`). Every equipped cosmetic's effects are re-applied continuously as permanent, hidden (no particles, no HUD icon spam) effects.

Stored as `namespace:effect:level` strings (e.g. `minecraft:water_breathing:1`).

!!! note "Level convention"
    Level `1` in the editor = amplifier `0` (Effect I). Level `2` = Effect II, etc.

---

## **Visual particle trails**

Two comma-separated lists in **Special Effects**. Each entry is the **id of a [Particle Effect](Particle Effects.md)** you defined in the Dev Studio's Effects page (not a raw Minecraft particle name):

| Field | When it plays |
| :--- | :--- |
| **Effect Visual** (`effectVisual`) | Always, while the cosmetic is equipped. |
| **Fly Particle** (`flyParticle`) | Only while the player is flying. |

So the workflow is: create the particle effect once (particle type, count, spread, interval, offset), then reference its id here. One effect can be reused by many cosmetics.

---

## **Cobblemon Lure bonuses**

A separate, large system: shiny rate, guaranteed IVs, EV gain, capture chance, hidden ability, fishing bonuses and more. See [Lure System](Lure System.md).
