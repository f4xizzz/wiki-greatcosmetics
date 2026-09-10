# **Parts & Models**

---

A cosmetic renders as one or more **parts**. Each part is either a **flat icon** (a floating item model) or a **GeckoLib** 3D model, anchored to a body point and transformed with offset / rotation / scale.

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
* `animations/item/<name>.animation.json` — optional

GeckoLib parts play their idle animation automatically.

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

## **Checklist for a new model**

1. Drop the files in your resource pack (icon **or** `.geo` + texture).
2. `/gc reload` (or restart the client) so it scans the pack.
3. Dev Studio → **+ Cosmetic** → set Slot, Type, Display Name.
4. In **3D Models**, type the file name into **Model/ID** (flat) or **GeckoLib Model ID** (3D). Turn on **Exact Path** if the file is in a subfolder/namespace.
5. `>> Config Part` → position it with the gizmo.
6. `S` to save. It's live for everyone.
