# **Dev Studio**

---

The **Dev Studio** is the in-game editor. Everything it changes is written to the config files **and broadcast to every online player instantly** — no restart, usually no `/gc reload`.

---

## **Access**

* Open `/wardrobe` → **Dev Studio** tab.
* Requires a **real server operator** account, and the **full server jar** (the client-only jar has the Dev Studio stripped out).
* `gc.dev` alone gives you the admin controls *inside* the Tags and Party tabs, but not this panel.

The menu has **Cosmetics**, **Effects**, **Cosmetics Types**, **Server Config**, **Slots**, and **Chat Tags** (only shown if the server has **LuckPerms** — see [Permissions](Permissions.md)).

---

## **Cosmetics page**

A searchable grid with a **type filter**. Two create buttons:

* **+ Cosmetic** — a new standard cosmetic (`new_cosmetic_XXXX`).
* **+ Armor** — a new armor-based cosmetic bound to a real item (see [Armor Cosmetics](Armor Cosmetics.md)).

Click a cosmetic to open the editor. **S** saves, **C** duplicates it (`<id>_copy`, `_copy2`…), **X** deletes (with confirm), **<** goes back. Hover any of the four for a tooltip.

### Editor sections

| Section | Fields |
| :--- | :--- |
| **Identification** | Main ID (file name), Icon Name, Model Texture, Display Name, **Tooltip Description** (extra MiniMessage lines shown under the name in the wardrobe), Slot, Type, Permission, **Granted Permissions**, **Minecraft Tags**. *(Armor cosmetics show "Real Item" instead of the ID.)* |
| **Icon** | Only for virtual cosmetics with no dedicated flat icon — frames the 3D model when it's used as its own wardrobe-grid icon. See [Making Models](Making Models.md#the-icon-of-a-3d-model). |
| **Auto-Unlock** | **Unlock Permission** / **Unlock Tag** — a player holding either one gets the cosmetic automatically, without a database row, and loses it the moment they no longer qualify. See [Permissions](Permissions.md#auto-unlock). |
| **3D Models** | One block per **part** — see below. |
| **Variants** | Optional. Alternative placements of the same model, each with its own effects too — see below. *(virtual cosmetics only)* |
| **Status & Combat** | Armor Points, Toughness, Max Durability, Auto-Feed. → [Attributes](Attributes.md) |
| **Backpack** | Is Backpack?, Rows, Name. → [Backpacks](Backpacks.md) |
| **Special Effects** | Allows Flight?, Fly / Ground / Swim Speed, `>> Select Effects` (potion effects — these now also apply from **armor cosmetics**, see below), Effect Visual, Fly Particle, **Shift Particle** (plays only while sneaking). → [Attributes](Attributes.md), [Particle Effects](Particle Effects.md) |
| **Cobblemon Effects** | `>> Cobblemon Effects` opens the Lure + Scanners editor (only shown if the server has Cobblemon). Every field has a hover tooltip. → [Cobblemon Effects](Lure System.md) |
| **Sounds** | Idle / Walk / Fly / Shift sounds, each with volume + pitch, plus **Sound Interval** and **Idle Sound Interval** (ticks between repeats). → [Sounds](Sounds.md) |

!!! note "Granted Permissions and Minecraft Tags"
    Comma-separated lists. Every node in **Granted Permissions** and every tag in **Minecraft Tags** is applied to the player while the cosmetic is worn **and** its `Permission` gate passes, and removed the instant it's unequipped — the same mechanism [Tags](Tags.md) already use. This also works for **armor cosmetics** worn as the real item.

---

## **Editing a part**

Each part in **3D Models** has:

* **Part N (Model/ID)** — the flat icon / vanilla model name.
* **Part N (GeckoLib Model ID)** — a GeckoLib geometry name (takes priority when set).
* **Part N: Exact Path** — toggle: treat the two fields above as full relative paths instead of just file names.
* **`>> Config Part N`** — opens the transform popup.
* **`+ Duplicate Part N`** — inserts an exact copy of the part right after it.
* **`X Remove Part N`** — deletes the part.
* **`+ Add Part`** — adds another part.

Armor cosmetics show a **Part N: Anchor** dropdown directly in the list (`HEAD`/`BODY`/`RIGHT_ARM`/`LEFT_ARM`/`RIGHT_LEG`/`LEFT_LEG`) — the real 3D armor model renders on that bone. A **`>> Split into N body parts`** button rebuilds the part list to match the armor slot (chestplate → torso + arms, leggings → torso + legs, boots → legs), each following its own bone.

Full explanation on [Parts & Models](Parts and Models.md), including the **3D gizmo** (hold `X`, `Y` or `Z` and drag outside the panel to move / rotate / scale the selected part live).

The transform popup: gizmo tool (Move / Rotate / Scale), **Anchor**, **Scale XYZ**, **Normal values** (Offset / Rotation XYZ), and **Sneak values** (Shift Offset / Rotation XYZ, used while the player is sneaking).

---

## **Variants**

A **variant** is an alternative *placement* of the cosmetic — same model, different position — and can also carry its own particle effects. Example: a scarf cosmetic with a `neck` variant and a `waist` variant.

* `+ Add Variant` creates one and opens its editor immediately; `X Remove Variant N` deletes it.
* Each variant row has a **Variant ID** field (`[a-z0-9_]`, unique in the cosmetic).
* `>> Config Variant N` opens the editor: **Display Name** (what players see in the picker), **Slot** (blank = inherit the base cosmetic's slot — only affects slot limits), **Anchor**, **Offset / Rotation / Scale** (with the live 3D gizmo and preview, same as a normal part), and an **=== EFFECTS ===** section — **Effect Visual** / **Fly Particle** / **Shift Particle** left **empty** inherit the base cosmetic's; filling in at least one gives the variant its own set instead.
* When a cosmetic has ≥1 variant, players clicking it in the wardrobe get a picker: **Default** (the base placement) + each variant. Only **one** variant (or Default) of a cosmetic can be worn at a time — they must unequip before switching.
* Variants are free — anyone who owns the cosmetic can use any variant.
* Don't add variants to a **backpack** cosmetic (all variants would share one backpack).

---

## **The gizmo toolbar**

A cluster of on-screen buttons appears around the 3D preview whenever a Part or an Effect is selected — none of them need the sidebar panel to be open.

**Left sidebar** (next to the transform popup):

| Button | Does |
| :--- | :--- |
| **S** | Toggle the sneak preview, so you see the Sneak values in action. |
| **Alpha slider** | Fade the player's body (not the cosmetic) to see parts clearly. |
| **C** | Toggle whether the player's *actually equipped* cosmetics also show in the preview, alongside the one you're editing (on by default in the Effects page, off elsewhere). |
| **P** | Toggle particle visibility in your own preview (same setting as the Preview tab's toggle). |
| **+ / −** | Only for GeckoLib parts: nudge the gizmo pivot (saved to `gizmo_dev_config.json`). |
| **E** | *(Effects page only, editing a member of a group)* Isolate — hide every other member of the group so only the one you're editing shows. |

**Bottom-left corner:** **D** — shows the gizmo's raw debug numbers (only while a part/effect is selected).

**Center-right of the screen:** three colour-coded buttons (**X** red, **Y** green, **Z** blue) — snap that axis's offset back to zero (or the Sneak offset, while previewing Sneak) in one click, instead of dragging the gizmo back by hand.

**Bottom-right corner** *(part selected)*: **↔** mirror horizontally (flips `scaleX`), **↕** mirror vertically (flips `scaleY`), **↺** reset the part (offset/rotation back to 0, scale back to 1).

**Top-right corner:** **Anim** — cycles the live preview through `AUTO → idle → walk → run → fly → swim → fall → sneak`, forcing that animation state so you can check every clip without actually doing it in-game. GeckoLib parts only.

---

## **Undo / Redo**

`Ctrl+Z` undoes, `Ctrl+Shift+Z` (or `Ctrl+Y`) redoes — works in the **Cosmetics** and **Effects** editors (not inside a group editor or the list view). Edits are coalesced: it only records a step once you pause for ~400 ms, so you don't have to undo one keystroke at a time.

---

## **Effects page**

Create and edit **particle effects and effect groups** — simple bursts or geometric shapes (circle, helix, beam, pulse), with colour, presets, a live 3D preview and a 3D gizmo for the offsets. Has its own search bar and an All / Effects / Groups filter. See [Particle Effects](Particle Effects.md) for the full field reference. Attach an effect (or group) to a cosmetic via **Special Effects → Effect Visual / Fly Particle / Shift Particle**.

---

## **Cosmetics Types page**

Define accessory **types** — Type ID, Base Slot, Limit Per Player, Permission (and the `gc.extratypeslot.*` tier nodes). Types are how you cap "one necklace at a time" separately from the slot limit. See [Slots & Types](Slots and Types.md).

---

## **Slots page**

The nine virtual **slots** are fixed — you can't rename, add or delete them. Edit only **Default Limit** and **Permission** (the base node for tier limits, `/gc extraslot`, etc.) per slot. See [Slots & Types](Slots and Types.md).

---

## **Chat Tags page**

*(Only visible if the server has LuckPerms.)* A dedicated editor for the same catalog the wardrobe's **Tags** tab already lets `gc.dev` players edit — list every Tag (group Tags first, then custom ones), **+ New Tag**, click one to edit Display Name / Description / Prefix / Permissions / Minecraft Tag. Group Tags can be edited but not deleted. See [Tags](Tags.md).

---

## **Server Config page**

Edits `mainconfig.conf` live: Auto Detect Models, MySQL settings, Force Resource Pack + Texture URL/ID/SHA1 (kept in sync with `server.properties` automatically), **Effect Block Groups** (LuckPerms groups whose cosmetics still *show* but grant nothing), the Lure HUD toggle, and the **startup commands** list. See [Main Config](Main Config.md).

---

## **Unsaved changes**

Leaving an editor with pending edits shows a popup: **Save**, **Don't Save**, or **Continue** editing. `Esc` triggers the same prompt.

---

!!! tip "Testing without owning things"
    Turn on **Dev Mode** (the `Dev: ON` toggle in the equipped-slots drawer, or it auto-enables when an operator opens the Dev/Tags/Party tab). Every cosmetic and Tag becomes previewable without a `/gc give`.
