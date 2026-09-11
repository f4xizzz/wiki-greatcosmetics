# **Particle Effects**

---

A **particle effect** is a named, reusable particle emitter you attach to cosmetics (as a trail, or a fly-only trail). Effects are defined in the [Dev Studio](Dev Studio.md) **Effects** page and stored in **`config/GreatCosmetics/effects.json`**. **Effect groups** bundle several effects that fire together, stored in **`config/GreatCosmetics/effect_groups.json`**.

---

## **Effect fields**

```json
{
  "sparkle_trail": {
    "particleId": "minecraft:end_rod",
    "shape": "SIMPLE",
    "count": 3,
    "tickInterval": 5,
    "speed": 0.0,
    "spreadX": 0.2, "spreadY": 0.4, "spreadZ": 0.2,
    "offsetX": 0.0, "offsetY": 1.0, "offsetZ": 0.0,
    "colorR": -1, "colorG": -1, "colorB": -1
  }
}
```

| Field | Meaning |
| :--- | :--- |
| **particleId** | Any Minecraft particle id (`minecraft:flame`, `minecraft:soul_fire_flame`, `minecraft:end_rod`…). |
| **shape** | `SIMPLE` (the classic emitter) or a geometric shape — `CIRCLE`, `HELIX`, `BEAM`, `PULSE`. See [Shapes](#shapes). |
| **count** | Particles spawned each burst. **`SIMPLE` only** — shapes spawn one particle per point of the shape. |
| **tickInterval** | Ticks between bursts (`20` = once/second, `5` = 4×/second). |
| **followPlayer** | `false` (default) = the particle spawns stationary — it hangs in place or drifts by its own `speed`, becoming a trail left behind a moving player. `true` = it spawns already carrying the player's current velocity and travels along with them instead of trailing. Works for `SIMPLE` and shapes alike (each point of a shape gets the player's velocity individually). |
| **speed** | Particle velocity — `0` = they hang in place, higher = they shoot outward. |
| **spreadX / Y / Z** | Random spread box around each spawn point (jitter). |
| **offsetX / Y / Z** | Position relative to the player — `Y: 1.0` is roughly chest height. `X` is sideways, `Z` is front/back. Rotates with the player's body. |
| **colorR / G / B** | `0–255` each, or `-1` = no custom colour. See [Colour (RGB)](#colour-rgb). |

---

## **Creating one**

Dev Studio → **Effects** → **+ New Effect**. The editor has a **live 3D preview** and a **3D gizmo**: hold `X`, `Y` or `Z` and drag outside the panel to move the offset visually. **S** saves and broadcasts to every online player.

The editor is laid out top-to-bottom:

1. **=== EFFECT PRESET ===** — a dropdown that fills in every field from a template, then you tweak. See [Presets](#presets).
2. **=== SHAPE ===** — `SIMPLE` / `CIRCLE` / `HELIX` / `BEAM` / `PULSE`. Changing this swaps the fields below.
3. **=== CONFIGURATION ===** — particle id, count, tick interval, **Follow Player** toggle.
4. **shape params** *(only when shape ≠ SIMPLE)* — radius, points, strands, rotation, animation…
5. **=== COLOR ===** — the **Custom Color** toggle and R/G/B sliders.
6. **=== 3D TOOL / OFFSETS / SPREAD ===** — position and jitter.

---

## **Colour (RGB)**

Turn on **Custom Color** and set the three sliders (`0–255`).

Minecraft only lets **three particle types** carry an arbitrary colour: `minecraft:dust`, `minecraft:dust_color_transition` and `minecraft:entity_effect`. If Custom Color is on and you picked **any other** particle (`flame`, `end_rod`, …), the mod renders it as **coloured dust** instead of ignoring the colour — the editor shows a yellow note when that's happening. So "enable colour → get a coloured particle" always holds; pick `minecraft:dust` explicitly if you want the dust look with no surprises.

Turn Custom Color **off** for the particle's natural colours.

---

## **Shapes**

With **shape ≠ SIMPLE**, the effect draws a geometric figure around the player each `tickInterval` instead of a loose burst. Extra fields appear:

| Field | Shapes | Meaning |
| :--- | :--- | :--- |
| **radius** | all | Size of the figure. |
| **points** | all | Particles per ring / per revolution. |
| **strands** | CIRCLE, HELIX | Parallel copies (a double helix = `2`). |
| **phase** | all | Starting angle, degrees. |
| **clockwise** | all | Direction. |
| **rotX / rotY / rotZ** | all | Tilt the whole figure, degrees (a tilted ring = `rotX` ≈ 30). |
| **helixHeight / turns / reverse** | HELIX | Height, number of twists, direction of travel. |
| **beamHeight / spacing / upwards** | BEAM | Column height, gap between particles, up or down. |
| **endRadius / endPoints / rings / outwards** | PULSE | End size, end density, number of rings, expand or contract. |
| **animTicks** | all | `0` = the whole figure every `tickInterval`. `> 0` = the figure is *traced/expanded* over `animTicks`, then pauses for `tickInterval`, then repeats. A `Pulse Out` with `animTicks: 40` = a ring that grows from `radius` to `endRadius` over ~2 s. |

`count` is ignored by shapes (one particle per point). `speed` and `spread` still apply as per-particle jitter.

!!! warning "Particle budget"
    A big shape can spawn hundreds of particles per tick. The mod caps `points ≤ 200`, `strands ≤ 12`, `rings ≤ 24` and the total per spawn at ~1200, but keep `points`/`strands` sane or you'll drown FPS and the network.

---

## **Presets**

The **=== EFFECT PRESET ===** dropdown loads a ready-made template into the current effect — `Ring`, `Ring (Tilted)`, `Halo`, `Helix`, `Double Helix`, `Rising Helix`, `Beam Up`, `Beam Down`, `Pulse Out`, `Pulse In`, `Nova`, `Simple Aura`, … Picking one overwrites **every** field; you then edit on top. The field itself stays empty — it's an action, not a value.

---

## **Effect groups**

A **group** is 2+ effects that play together. Dev Studio → **Effects** → **+ New Group** (next to *+ New Effect*). Groups show in the list with a cyan border and a `[G]` prefix.

In the group editor:

* **Add Existing Effect** — pick an effect id already in the catalog.
* **Create New Effect** — makes an effect that lives *inside the group* (it does **not** appear on the Effects list and isn't in `effects.json` — it's stored in the group's JSON).
* **Group Preset** — a combo template (`Vortex`, `Smash`, `Twin Halo`) that fills the group with several effects at once.
* **Edit** a member → opens that effect's editor "in group context": the **other** members also show in the preview. The sidebar **E** button (above **S**) isolates — only the effect you're editing shows. **< Back** returns to the group.

A **group id is used exactly where an effect id is used** (the cosmetic's *Effect Visual* / *Fly Particle* / *Shift Particle* fields). The mod expands it to its members at spawn time; each member keeps its own `tickInterval`.

---

## **Attaching it to a cosmetic**

In the cosmetic editor, **Special Effects** section:

* **Effect Visual** — comma-separated list of effect **or group** ids; plays always while the cosmetic is worn.
* **Fly Particle** — same, but only while the player is flying.
* **Shift Particle** — same, but only while the player is sneaking/crouching.

One effect (or group) can be referenced by any number of cosmetics.

!!! note "Variants can override these"
    A [variant](Dev Studio.md#variants) has its own Effect Visual / Fly Particle / Shift Particle lists. Leave a variant's list empty and it inherits the base cosmetic's; fill in at least one id and it's used **instead of** the base list while that variant is worn.

---

!!! note "Sync"
    Effects and groups broadcast to all online players when saved. If a player joined before the effect existed, `/gc reload` (or their next join) picks it up.
