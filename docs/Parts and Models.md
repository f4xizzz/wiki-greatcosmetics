# **Parts & Models**

---

A cosmetic renders as one or more **parts**. Each part is either a **flat icon** (a floating item model) or a **GeckoLib** 3D model, anchored to a body point and transformed with offset / rotation / scale.

!!! tip "Making the files"
    This page is the reference for the *fields*. For a step-by-step on **creating the models and textures** — folder paths, Blockbench, drawing the texture — see [Making Models & Textures](Making Models.md).

---

## **The two rendering modes**

### 1. Flat icon / vanilla model

Set **`customModelData_or_ID`** to a name. The mod looks for, in order:

1. `assets/greatcosmetics/textures/icons/<name>.png` — a plain flat icon (most common).
2. `assets/greatcosmetics/models/<name>.json` — a custom vanilla item model.

The part is drawn as that item model floating at the anchor.

### 2. GeckoLib model

Set **`geoModelId`** to a name. This **takes priority** over the flat icon. The mod looks for, in **any** namespace:

* `geo/item/<name>.geo.json` — required
* `textures/item/<name>.png` — required (the mod also tries the folder that mirrors the `.geo` path)
* `animations/item/<name>.animation.json` — optional (see [State animations](#state-animations))

### Exact Path mode

With **`useExactPath`** on, the two fields above stop being "just the file name" and become a **full relative path** resolved by exact match in any namespace:

| Mode | Field value | Resolves to |
| :--- | :--- | :--- |
| Off | `wizard_hat` | `.../models/wizard_hat.json` (namespace `greatcosmetics` for vanilla models) |
| On | `hats/wizard_hat` | `.../models/hats/wizard_hat.json` in **any** namespace |
| On (Geo) | `item/wizard_hat` | `.../geo/item/wizard_hat.geo.json` in any namespace |

Use it when your files sit in subfolders or in another mod's namespace, or when two files share a name.

---

## **Anchors**

Where the part attaches:

`HEAD`, `BODY`, `RIGHT_ARM`, `LEFT_ARM`, `RIGHT_LEG`, `LEFT_LEG`

The anchor follows the body part's animation (head turns, arms swing), then the part's offset/rotation/scale are applied on top.

---

## **Transforms**

| Group | Fields | Used |
| :--- | :--- | :--- |
| **Scale** | `scaleX/Y/Z` (default 1.0) | Always |
| **Normal values** | `offsetX/Y/Z`, `rotationX/Y/Z` | While standing |
| **Sneak values** | `shiftOffsetX/Y/Z`, `shiftRotationX/Y/Z` | While the player is sneaking |

Sneak values exist because the vanilla sneak pose bends the body — a hat that sits right while standing may clip while crouched, so you tune a separate position for it.

---

## **The 3D gizmo**

In the Dev Studio, select a part (click it in the outliner or open `>> Config Part`). Then, **anywhere outside the panel**:

1. Hold **`X`**, **`Y`** or **`Z`** — locks the axis.
2. Drag the mouse — the part **moves**, **rotates** or **scales** live (pick the mode with the Move / Rotate / Scale buttons in the popup).

The text fields update as you drag, and vice-versa. Toggle the sidebar **S** button to edit the Sneak pose the same way.

---

## **Multiple parts**

Add parts with **`+ Add Part`**. A single cosmetic can combine, say, a GeckoLib hat on `HEAD` plus a flat feather icon offset to the side — each with its own transform. There's no hard limit; keep it reasonable for performance.

---

## **State animations**

*(GeckoLib parts only — flat icons never animate.)*

A GeckoLib model plays an animation from its `.animation.json` **based on what the wearer is doing** — idle, walking, flying, and so on. There is **no controller code to write and nothing to configure**: the mod picks the clip purely by its **name**. Give a clip one of the fixed names below and it plays in that state; a model whose `.animation.json` has **none** of these names stays completely static (the old behaviour).

### The fixed names

| Name | Plays when | Falls back to |
| :--- | :--- | :--- |
| `idle` | Standing still (the default / rest state) | — |
| `walk` | Moving on the ground | `idle` |
| `run` | Sprinting on the ground | `walk` → `idle` |
| `fly` | Flying (creative / cosmetic flight) or gliding with an elytra | `idle` |
| `swim` | In water and off the ground | `walk` → `idle` |
| `fall` | In the air, not flying (jumping / falling) | `idle` |
| `sneak` | Sneaking | *(nothing — see below)* |

**Priority** (the first one whose clip actually exists wins): `sneak` → `fly` → `swim` → `fall` → `run` → `walk` → `idle`.

`sneak` is special: if the model has **no** `sneak` clip, crouching is **transparent** — the animation doesn't change (a moving player keeps playing `walk`, a still one keeps `idle`). Every other name falls back down the chain to `idle`.

You only need the clips you care about. A cape with just `idle` and `fly` is fine — walking, sneaking, etc. all resolve down to `idle` (or, for sneak, just don't change anything).

### Naming in Blockbench

You don't have to rename anything to the bare word. The mod matches a clip whose name **ends with** the fixed name after a separator, so all of these count as `idle`:

* `idle`
* `animation.dragon_wings.idle` — Blockbench's default `animation.<model>.<action>`
* `ground_idle` / `animation.charizard.ground_idle` — the Cobblemon convention (ripped Pokémon animations)
* `battle_idle`, `air_idle`, … — anything ending `_idle` / `-idle`

Same for the others: `ground_walk` → `walk`, `ground_run` → `run`, `air_fly` → `fly`. When several clips could match, the more specific one wins (`.idle` beats `ground_idle` beats `battle_idle`). Clips with `ride` or `test` in the name are ignored.

!!! tip "Want an always-on animation?"
    A model that should always do the same thing (a slowly spinning halo, a flickering flame) — just name that clip **`idle`**. It loops in every state because everything falls back to `idle`.

### Notes

* Every clip **loops**. One-shot animations are not supported here.
* Each wearer animates independently — two players in the same cosmetic don't sync.
* Blending between states is smoothed over ~5 ticks.
* In the Dev Studio the preview player just stands there, so you'll only see `idle` (or nothing). Test movement animations in the world.

---

## **Checklist for a new model**

1. Drop the files in your resource pack (icon **or** `.geo` + texture).
2. `/gc reload` (or restart the client) so it scans the pack.
3. Dev Studio → **+ Cosmetic** → set Slot, Type, Display Name.
4. In **3D Models**, type the file name into **Model/ID** (flat) or **GeckoLib Model ID** (3D). Turn on **Exact Path** if the file is in a subfolder/namespace.
5. `>> Config Part` → position it with the gizmo.
6. `S` to save. It's live for everyone.
