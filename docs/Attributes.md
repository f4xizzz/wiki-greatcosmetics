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

---

## **Special Effects**

A cosmetic can also grant an *active ability*, editable in the Dev Studio's **Special Effects** section (or, for the four marked **Cobblemon**, inside the **Cobblemon Effects** popup — see [Cobblemon Effects](Lure System.md) — they only appear on a server running Cobblemon). See [Integrations](Integrations.md) for how the Cobblemon-gated ones work under the hood.

Each ability can also be reached from the **Quick Actions** wheel (default key `V`, see [The Wardrobe](The Wardrobe.md#quick-actions-menu)) instead of holding Shift.

| Ability | Trigger | Effect |
| :--- | :--- | :--- |
| **Heal Ability** *(Cobblemon)* | Hold Shift {cooldown}s, or click **Heal Party Now** in Quick Actions | Fully heals the player's Cobblemon party (HP, status, PP) — same as a healing machine. Doesn't work mid-battle. Per-cosmetic cooldown; wearing several uses the shortest. |
| **Shiny & HA Radar** *(Cobblemon)* | Passive, always on while equipped | Warns the player (looping sound + action-bar distance) when a wild **shiny** or **Hidden Ability** Pokémon comes within a configurable range. Goes quiet once it leaves range. |
| **Vein Miner** | Hold Shift while breaking a matching block | Breaks the whole connected "vein" of that same block/tag in one go (safety cap on max blocks). Items go straight to the inventory. Blocks/tags list is **required** — blank disables it (no "mine anything" default). |
| **Tree Capitator** | Hold Shift while breaking a log | Fells the whole connected tree (any wood, vanilla or modded, via `#minecraft:logs`), same inventory behavior as Vein Miner. |
| **Pollinator** | Click **Pollinate Now** in Quick Actions (or hold Shift 15s) | Bone-meals every fertilizable plant (crops, saplings, etc.) in a spherical radius, using the same random grow chance as real bone meal — not a guaranteed instant grow. Configurable radius, bone-meal "uses" per plant, and cooldown. |
| **Auto Harvest** | Passive, on a timer | Harvests every fully-grown crop in radius automatically. Doesn't replant — pair with Auto Planting. |
| **Auto Planting** | Passive, on a timer | Plants seeds into empty farmland in radius. Seed priority: main hand → off hand → hotbar slot 1-9. Doesn't harvest. |
| **Auto Watering** | Passive, on a timer | A gentler, continuous version of Pollinator — one bone-meal "use" per fertilizable plant in radius every interval. |
| **Item Giver** | Passive, on a timer | Gives a configured item + quantity straight to the inventory (drops on the ground if full). |
| **Combat Sounds** | Passive, on hit | Plays a sound when the player takes damage and/or deals damage. Configured in the cosmetic's **Sounds** section — see [Sounds](Sounds.md#combat-sounds). |

Vein Miner, Tree Capitator, Auto Harvest, Auto Planting, Auto Watering, Item Giver and Combat Sounds are **pure vanilla mechanics** — they work identically with or without Cobblemon installed.

!!! tip "Toggling Vein Miner / Tree Capitator without unequipping"
    Since these two are always-on while equipped, the Quick Actions wheel gives each one an on/off circle (green = on, red = off) — a per-session preference that doesn't touch the cosmetic's config and resets on logout.

### **Scanners** *(Cobblemon)*

Also configured in the **Cobblemon Effects** popup (see [Cobblemon Effects](Lure System.md), which covers the Lure bonuses these sit alongside). While equipped, each scanner adds information above (or beside) every nearby Pokémon's name tag — computed server-side, since wild Pokémon IV/nature/ability data doesn't normally reach the client.

| Scanner | Shows |
| :--- | :--- |
| **IVs Scanner** | Every stat's IV (HP/Atk/Def/SpA/SpD/Spe), colored, above the name. |
| **Nature Scanner** | The Pokémon's nature, right under the IV line. |
| **Ability Scanner** | The Pokémon's ability, in red, to the right of the name. |
| **Size Scanner** | The size category (XS-XL), in yellow bold, to the left of the name. |
| **Dex Scanner** | Any wild Pokémon looked at (crosshair) from 5+ blocks away is auto-registered as seen in the Pokédex — no item needed. |

### **Granted Permissions & Minecraft Tags** *(LuckPerms)*

Beyond the single `permission` gate (who can use the cosmetic at all), a cosmetic can **grant** things while equipped:

* **Granted Permissions** — a comma-separated list of LuckPerms permission nodes applied as *transient* (session-only, never written to LuckPerms storage) while the cosmetic is worn and its gate passes. Removed the instant it's unequipped.
* **Minecraft Tags** — a comma-separated list of vanilla scoreboard tags (`/tag`) added the same way, for use in `/execute if entity @s[tag=...]` or datapacks.

See [Integrations](Integrations.md#luckperms) for the full LuckPerms picture, including the server-wide "block effects for this group" switch.
