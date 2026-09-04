# **Dev Studio**

---

The **Dev Studio** is the in-game editor. Everything it changes is written to the config files **and broadcast to every online player instantly** — no restart, usually no `/gc reload`.

---

## **Access**

* Open `/wardrobe` → **Dev Studio** tab.
* Requires a **real server operator** account, and the **full server jar** (the client-only jar has the Dev Studio stripped out).
* `gc.dev` alone gives you the admin controls *inside* the Tags and Party tabs, but not this panel.

The menu has five pages: **Cosmetics**, **Effects**, **Cosmetics Types**, **Server Config**, **Slots**.

---

## **Cosmetics page**

A searchable grid with a **type filter**. Two create buttons:

* **+ Cosmetic** — a new standard cosmetic (`new_cosmetic_XXXX`).
* **+ Armor** — a new armor-based cosmetic bound to a real item (see [Armor Cosmetics](Armor Cosmetics.md)).

Click a cosmetic to open the editor. `S` saves, `X` deletes (with confirm), `<` goes back.

### Editor sections

| Section | Fields |
| :--- | :--- |
| **Identification** | Main ID (file name), Icon Name, Display Name, Slot, Type, Permission. *(Armor cosmetics show "Real Item" instead of the ID.)* |
| **3D Models** | One block per **part** — see below. |
| **Status & Combat** | Armor Points, Toughness, Max Durability, Auto-Feed. → [Attributes](Attributes.md) |
| **Backpack** | Is Backpack?, Rows, Pages, Name. → [Backpacks](Backpacks.md) |
| **Special Effects** | Allows Flight?, Fly / Ground / Swim Speed, `>> Select Effects` (potion), Effect Visual, Fly Particle. → [Attributes](Attributes.md) |
| **Lure System** | `>> Configure LURE` opens the bonus editor. → [Lure System](Lure System.md) |
| **Sounds** | Idle / Equip / Unequip / Walk / Fly / Shift / Backpack sounds, each with volume + pitch. → [Sounds](Sounds.md) |

---

## **Editing a part**

Each part in **3D Models** has:

* **Part N (Model/ID)** — the flat icon / vanilla model name.
* **Part N (GeckoLib Model ID)** — a GeckoLib geometry name (takes priority when set).
* **Part N: Exact Path** — toggle: treat the two fields above as full relative paths instead of just file names.
* **`>> Config Part N`** — opens the transform popup.
* **`X Remove Part N`** — deletes the part.
* **`+ Add Part`** — adds another part.

Full explanation on [Parts & Models](Parts and Models.md), including the **3D gizmo** (hold `X`, `Y` or `Z` and drag outside the panel to move / rotate / scale the selected part live).

The transform popup: gizmo tool (Move / Rotate / Scale), **Anchor**, **Scale XYZ**, **Normal values** (Offset / Rotation XYZ), and **Sneak values** (Shift Offset / Rotation XYZ, used while the player is sneaking).

### Left sidebar

Appears while a part is selected:

* **S** — toggle the sneak preview so you see the Sneak values in action.
* **Alpha slider** — fade the player's body (not the cosmetic) to see parts clearly.
* **+ / −** — only for GeckoLib parts: nudge the gizmo pivot (saved to `gizmo_dev_config.json`).

---

## **Effects page**

Create and edit **particle effects** — `particleId`, count, tick interval, position offsets, spread and speed, with a live 3D preview and a 3D gizmo for the offsets. See [Particle Effects](Particle Effects.md). Attach an effect to a cosmetic via **Special Effects → Select Effects**.

---

## **Cosmetics Types page**

Define accessory **types** — Type ID, Base Slot, Limit Per Player, Permission. Types are how you cap "one necklace at a time" separately from the slot limit. See [Slots & Types](Slots and Types.md).

---

## **Slots page**

Edit the nine virtual **slots** — Name (must be one of the nine), Default Limit, Extra Permission (the base node for limit tiers). See [Slots & Types](Slots and Types.md).

---

## **Server Config page**

Edits `mainconfig.conf` live: Auto Detect Models, MySQL settings, Force Resource Pack + Texture URL/ID/SHA1, and the **startup commands** list. See [Main Config](Main Config.md).

---

## **Unsaved changes**

Leaving an editor with pending edits shows a popup: **Save**, **Don't Save**, or **Continue** editing. `Esc` triggers the same prompt.

---

!!! tip "Testing without owning things"
    Turn on **Dev Mode** (the `Dev: ON` toggle in the equipped-slots drawer, or it auto-enables when an operator opens the Dev/Tags/Party tab). Every cosmetic and Tag becomes previewable without a `/gc give`.
