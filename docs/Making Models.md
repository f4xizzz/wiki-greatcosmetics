# **Making Models & Textures**

---

This is the hands-on guide: **what a cosmetic model actually is**, the difference between a **flat / vanilla** model and a **GeckoLib** model, **which folders every file goes in**, and how to draw the textures. When you're done here, [Parts & Models](Parts and Models.md) covers the positioning fields and [Resource Pack](Resource Pack.md) covers shipping the pack to players.

---

## **The three render modes**

A [part](Parts and Models.md) of a cosmetic is drawn in one of three ways. You pick per part, in the Dev Studio.

| Mode | What it is | You provide | Animated? | Use it for |
| :--- | :--- | :--- | :--- | :--- |
| **Flat icon** | A single PNG shown as a floating sprite (like an item held out). No model file at all. | one `.png` | No | Emblems, 2D badges, quick tests, "sticker" cosmetics |
| **Vanilla model** | A normal Minecraft item model — the same JSON format as any vanilla item or block: a box of cuboids ("elements") with a texture mapped by UV. | one `.json` + its `.png` | No | Blocky hats, simple 3D props, anything you'd build as a resource-pack item model |
| **GeckoLib model** | A **Bedrock-format** bone-and-cube model (`.geo.json`) with its own texture and an optional animation file. Rendered in true 3D with per-bone animation. | `.geo.json` + `.png` (+ optional `.animation.json`) | **Yes** | Wings, capes, tails, antennas, anything curved / organic / that should move |

**Rule of thumb:** if it never moves and it's a flat shape → flat icon. If it never moves but has depth → vanilla model. If it should flap, sway, spin, or bends around the body → GeckoLib.

!!! info "Flat icon vs vanilla model — same field"
    Both use the part's **`Model ID`** field. The mod first looks for a `textures/icons/<name>.png` (flat icon); if there isn't one, it looks for a `models/<name>.json` (vanilla model). GeckoLib is a **separate field** (`GeckoLib Model`) and always wins when it's filled in.

---

## **Tools you need**

* **[Blockbench](https://www.blockbench.net/)** (free) — models both vanilla item models *and* GeckoLib models, paints textures, and does GeckoLib animations. This is the only modelling tool you need.
* **Any image editor with transparency** — GIMP, Krita, Aseprite, Photoshop, Paint.NET — for flat icons or touching up textures. Blockbench's built-in paint tab is enough for simple stuff.
* A **resource pack folder** to drop the finished files into. See [Resource Pack](Resource Pack.md) for how it reaches players — everything below is about *what* goes *where* inside it.

---

## **Folder paths**

Everything a cosmetic needs lives under **`assets/<namespace>/`** in a resource pack (or inside the mod jar for the built-in ones).

```
your_pack.zip
└── assets/
    ├── greatcosmetics/                 ← flat icons & vanilla models MUST be here
    │   ├── textures/
    │   │   └── icons/
    │   │       └── wizard_hat.png      ← flat icon  → Model ID: wizard_hat
    │   └── models/
    │       └── crown.json              ← vanilla model → Model ID: crown
    │
    └── mypack/                         ← GeckoLib files can be in ANY namespace
        ├── geo/
        │   └── item/
        │       └── dragon_wings.geo.json        ← GeckoLib Model: dragon_wings
        ├── textures/
        │   └── item/
        │       └── dragon_wings.png             ← its texture (name matches the geo)
        └── animations/
            └── item/
                └── dragon_wings.animation.json  ← optional (see State animations)
```

| File type | Folder | Namespace | Matched by |
| :--- | :--- | :--- | :--- |
| Flat icon | `textures/icons/` | **`greatcosmetics` only** | file name → part **Model ID** |
| Vanilla model | `models/` | **`greatcosmetics` only** | file name → part **Model ID** |
| GeckoLib geometry | `geo/…/` (usually `geo/item/`) | **any** loaded namespace | file name (minus `.geo.json`) → part **GeckoLib Model** |
| GeckoLib texture | `textures/…/` (usually `textures/item/`) | any | file name matching the geo — or the mirrored path `geo/x` → `textures/x` |
| GeckoLib animation | `animations/…/` (usually `animations/item/`) | any | file name matching the geo |

Notes:

* **Only the file name matters** for GeckoLib (unless you use Exact Path). `geo/item/dragon_wings.geo.json`, `geo/dragon_wings.geo.json`, `geo/cosmetics/dragon_wings.geo.json` all resolve from `GeckoLib Model: dragon_wings`. Keep names **unique** across your pack.
* If two files share a name in different folders, turn on the part's **Exact Path** toggle and type the full relative path (`item/dragon_wings`, `hats/wizard_hat`).
* The GeckoLib texture is found by trying the **mirrored path first** (`geo/item/x.geo.json` → `textures/item/x.png`), then by bare name anywhere. This is why keeping the geo and texture in mirrored `item/` folders is the safe default.
* `autoDetectModels` in [`mainconfig.conf`](Main Config.md) (on by default) is what makes the mod scan the pack and wire up the Custom Model Data. Leave it on.

---

## **Textures**

### Flat icon texture

* **Format:** PNG, RGBA (must have an alpha channel — the transparent parts must be *actually* transparent, not white).
* **Size:** `16×16` is the classic look. `32×32`, `64×64`, `128×128` also work — bigger = crisper, but keep it a power of two and don't go wild.
* **Style:** it's rendered exactly like an item in your hand, so pixel-art reads best. Anti-aliased soft edges will look blurry in the wardrobe grid.
* Save it as `assets/greatcosmetics/textures/icons/<name>.png`. That `<name>` is what you type into the part's **Model ID** (or into **Icon Name** on the cosmetic, if several cosmetics share one icon).

### Vanilla model texture

A vanilla model is a `.json` that lists cuboids and a `textures` block pointing at PNGs:

```json
{
  "textures": { "0": "greatcosmetics:item/crown", "particle": "greatcosmetics:item/crown" },
  "elements": [
    { "from": [4,0,4], "to": [12,4,12],
      "faces": {
        "north": { "uv": [0,0,8,4], "texture": "#0" },
        "up":    { "uv": [0,4,8,12], "texture": "#0" }
      }
    }
  ]
}
```

* The **UV space is always `0–16`** regardless of the PNG's real pixel size — `uv: [0,0,8,4]` means "the left half, top quarter of the texture".
* Put the PNG wherever the `textures` block says — e.g. `greatcosmetics:item/crown` → `assets/greatcosmetics/textures/item/crown.png`.
* **Easiest path:** in Blockbench, `File → New → Java Block/Item Model`, build it, paint it, then `File → Export → Java Model` for the `.json` and `File → Export → Textures`. Drop the `.json` in `models/` and fix the texture paths to your namespace.

### GeckoLib model texture

* The `.geo.json` header declares the texture size:

  ```json
  "description": { "identifier": "geometry.dragon_wings",
                   "texture_width": 64, "texture_height": 64 }
  ```

* Your PNG **must be exactly `texture_width × texture_height`**. If you resize the model's texture in Blockbench, that header updates automatically — always re-export the geo after changing texture size.
* GeckoLib uses **box UV** by default (Blockbench unwraps each cube onto the sheet for you). Paint inside those islands; painting outside them does nothing.
* Export the texture from Blockbench (`File → Export → Textures`, or right-click the texture → *Save As*) and place it next to the geo in a mirrored folder: geo in `mypack/geo/item/`, texture in `mypack/textures/item/`, **same base name**.
* Transparency works — use it for feathered edges, holes, etc.

!!! tip "One model, many skins"
    Build the model once, then make several cosmetics that each set a different **Model Texture** (see below). Great for colour variants of the same hat.

---

## **Walkthrough — a flat icon cosmetic**

1. Draw a `32×32` PNG with a transparent background. Save it as
   `assets/greatcosmetics/textures/icons/star_badge.png` in your pack.
2. Ship the pack to your client (modpack folder, or the [Forced Resource Pack](Resource Pack.md)).
3. In game: `/gc reload` — or just relog — so the mod scans the pack.
4. `/wardrobe` → **Dev Studio** (`D` tab) → **Cosmetics** → **+ Cosmetic**.
5. Set **Main ID** `star_badge`, a **Display Name**, a **Slot** (e.g. `FACE`), leave **Type** `default`.
6. In **3D MODELS**, on Part 1, type `star_badge` into **Model ID**. Leave GeckoLib empty.
7. `>> Config Part` → nudge **Offset Y** until it sits where you want. Save with the sidebar **S**.
8. `/gc give star_badge <you>` → open the wardrobe → equip it.

---

## **Walkthrough — a GeckoLib hat**

**In Blockbench:**

1. `File → New → Bedrock Model`.
2. `File → Project` (or the project settings panel) → set **Texture Size** to `64 × 64`.
3. Model the hat. The mod auto-centers a GeckoLib model on the middle of its own bounding box when anchoring it to a body point, so building off-origin is fine — a model centered on `[0,0,0]` is still a tidy habit, but no longer required for a good default placement. Fine-tune from there with Offset.
4. Paint it (the **Paint** tab) or `File → Export → Export Texture` a blank sheet and paint it in your image editor, then re-import.
5. *(Optional)* **Animate** tab → create a looping animation and name it exactly `idle` (or `fly`, `walk`, … — see [State animations](Parts and Models.md#state-animations)). Skip this for a static hat.
6. `File → Export → Export Bedrock Geometry` → `wizard_hat.geo.json`.
7. `File → Export → Export Texture` → `wizard_hat.png`.
8. *(If you animated)* `File → Export → Export Bedrock Animations` → `wizard_hat.animation.json`.

**In your resource pack:**

```
assets/mypack/geo/item/wizard_hat.geo.json
assets/mypack/textures/item/wizard_hat.png
assets/mypack/animations/item/wizard_hat.animation.json   (only if you animated)
```

**In game:**

1. `/gc reload`.
2. Dev Studio → Cosmetics → **+ Cosmetic** → Main ID `wizard_hat`, Slot `HEAD`.
3. Part 1 → **GeckoLib Model**: `wizard_hat`. Leave Model ID empty.
4. `>> Config Part` → use the [3D gizmo](Parts and Models.md#the-3d-gizmo) (`X`/`Y`/`Z` + drag) to position, rotate and scale it onto the head. Set a **Sneak pose** with the sidebar **S** button if it clips when crouched.
5. Save. It's live for every online player who has the pack.

If the hat is **invisible**: the console prints a `WARNING` naming the missing file — almost always the `.geo.json` or `.png` name doesn't match, or the PNG isn't in a scanned `textures/` folder.

!!! info "No more flicker on animated models"
    Older animated GeckoLib models — especially ones built from ripped Cobblemon geometry (wings, capes, etc.) — used to flicker or "z-fight" (the texture looking like one layer fighting another), most noticeable on animated models. Two bugs caused it: several instances of the same model sharing one animation clock, and GeckoLib rendering without back-face culling while Cobblemon's own models expect it on. Both are fixed — nothing to configure, animated models (Cobblemon-ripped or not) just render clean now.

---

## **The Model Texture field**

On the cosmetic (not the part), **Model Texture** overrides the texture for **all** of that cosmetic's models — GeckoLib *and* vanilla.

* Leave it **empty** → the mod uses the texture whose name matches the model (the normal behaviour).
* Set it to a file name → that texture is used instead. Bare name → `textures/item/<name>.png`; add a path for a subfolder; or a full `namespace:path`.
* For a **vanilla model** the mod serves a *copy* of the model JSON with the texture swapped, so the original `.json` in your pack is untouched and can still be used by other cosmetics with its default skin.

Use it to build one model and reskin it per cosmetic (red/blue/gold versions of a cape from a single `.geo.json`).

---

## **The icon of a 3D model**

When a cosmetic has **no Icon Name** and no flat icon PNG, the wardrobe grid shows the **3D model itself** as the icon. GeckoLib has a single fixed GUI transform, so a model built for the body often comes out huge or off-centre in that little square.

The **=== ICON ===** section fixes only the icon (never the worn model): drag the preview box to move, scroll to zoom, right-drag to rotate — or type into **Icon Scale / Offset / Rotation**. **Reset icon framing** puts it back. This does nothing for a PNG icon.

If **Icon Scale** hasn't been touched (still at the default `1.0`), the mod now computes a starting scale automatically from the model's own bounds, aiming for roughly a normal item-icon size — instead of always starting flat at `1.0`, which was often way too big or way too small. The manual controls above still work exactly the same for fine-tuning or overriding; auto-scale just gets you a much closer starting point before you touch anything. It doesn't auto-rotate the model — a model's "front" is subjective, so rotation stays manual.

---

## **Common mistakes**

| Symptom | Cause |
| :--- | :--- |
| Everything is the purple/black checkerboard | Client has no resource pack, or it failed to download. Check `latest.log`. |
| Flat icon shows a generic item | PNG isn't in `assets/greatcosmetics/textures/icons/` (wrong namespace or folder), or the name doesn't match the Model ID. |
| GeckoLib model invisible | Missing `.geo.json` or `.png`; names don't match; texture not under any `textures/` folder. Console names the file. |
| GeckoLib model textured wrong / UVs scrambled | The PNG size doesn't match `texture_width`/`texture_height` in the geo, or two textures share a name and it grabbed the wrong one — mirror the folders (`geo/item/x` + `textures/item/x`) or use **Exact Path**. |
| Model shows but never animates | `.animation.json` missing, or no clip is named `idle`/`walk`/`fly`/… — see [State animations](Parts and Models.md#state-animations). |
| Changes don't show up | You didn't `/gc reload` after editing the pack, or the client is still on the old cached pack. |
| Icon in the menu is giant / cropped | It's a 3D-model icon — frame it in the **=== ICON ===** section. |
