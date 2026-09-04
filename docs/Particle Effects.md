# **Particle Effects**

---

A **particle effect** is a named, reusable particle emitter you attach to cosmetics (as a trail, or a fly-only trail). Defined in the [Dev Studio](Dev Studio.md) **Effects** page and stored in **`config/GreatCosmetics/effects.json`**.

---

## **Effect fields**

```json
{
  "sparkle_trail": {
    "particleId": "minecraft:end_rod",
    "count": 3,
    "tickInterval": 5,
    "speed": 0.0,
    "spreadX": 0.2,
    "spreadY": 0.4,
    "spreadZ": 0.2,
    "offsetX": 0.0,
    "offsetY": 1.0,
    "offsetZ": 0.0
  }
}
```

| Field | Meaning |
| :--- | :--- |
| **particleId** | Any Minecraft particle id (`minecraft:flame`, `minecraft:soul_fire_flame`, `minecraft:end_rod`…). |
| **count** | Particles spawned each burst. |
| **tickInterval** | Ticks between bursts (`20` = once/second, `5` = 4×/second). |
| **speed** | Particle velocity — `0` = they hang in place, higher = they shoot outward. |
| **spreadX / Y / Z** | Random spread box around the spawn point. |
| **offsetX / Y / Z** | Position relative to the player — `Y: 1.0` is roughly chest height. `X` is sideways, `Z` is front/back. |

---

## **Creating one**

Dev Studio → **Effects** → **+ New Effect**. The editor has a **live 3D preview** and a **3D gizmo**: hold `X`, `Y` or `Z` and drag outside the panel to move the offset visually. **S** saves.

The Particle ID field has autocomplete for every registered particle (vanilla + mods).

---

## **Attaching it to a cosmetic**

In the cosmetic editor, **Special Effects** section:

* **Effect Visual** — comma-separated list of effect **ids**; plays always while the cosmetic is worn.
* **Fly Particle** — same, but only while the player is flying.

One effect can be referenced by any number of cosmetics.

---

!!! note "Sync"
    Effects broadcast to all online players when saved. If a player joined before the effect existed, `/gc reload` (or their next join) picks it up.
