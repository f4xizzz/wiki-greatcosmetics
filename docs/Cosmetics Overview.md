# **Cosmetics Overview**

---

A **cosmetic** is one wearable entry in the catalog. It occupies one virtual slot, renders one or more 3D **parts** on the player, and can carry stats, abilities, effects, Lure bonuses and sounds.

The catalog lives in **`config/greatcosmetics/cosmeticsconfig.conf`** (JSON despite the extension). You rarely edit it by hand — the [Dev Studio](Dev Studio.md) writes it for you and broadcasts changes live. This page explains what each field means.

---

## **Anatomy of a cosmetic**

| Field | Meaning |
| :--- | :--- |
| **id** (map key) | Unique identifier. Used by `/gc give`, tags, NPC equip, and to find the model files. |
| **DisplayName** | MiniMessage name shown in menus and on the physical item. Blank → the capitalized id. |
| **slot** | One of `HEAD, FACE, NECK, CHEST, BACK, WAIST, LEGS, FEET, HAND`. Controls which category it appears in and which [slot limit](Slots and Types.md) applies. |
| **type** | Free-text type name (e.g. `necklace`). Must match a key in `mainconfig.conf` → `types` for a type limit to apply. `default` = no type limit. |
| **permission** | If set, only players holding this node (or who unlocked it) see and equip the cosmetic. Blank = available to everyone who unlocked it. |
| **iconId** | Optional. Name of a different `textures/icons/*.png` to use as the flat icon, so several cosmetics can share one icon file. Blank = uses the id. |
| **cmd** | The Custom Model Data number the mod assigns to the flat icon. Managed automatically — don't set by hand. |
| **maxDurability** | If > 0, the physical item shows a durability bar (purely visual). |
| **parts** | The list of 3D pieces — see [Parts & Models](Parts and Models.md). |

Plus the optional systems: **armor / toughness**, **EnableFly + speed multipliers**, **AutoFeed**, **effects** (potion), **effectVisual / flyParticle**, **isBackpack**, **lure**, **sounds** — each has its own page.

---

## **How a player gets a cosmetic**

| Method | Result |
| :--- | :--- |
| `/gc give <id> [player]` | Unlocks it in the wardrobe. |
| `/gc giveitem <id> [player]` | Gives the physical item; the player still equips it via the wardrobe. |
| Holding a matching real item on join | Auto-converted (see [Armor Cosmetics](Armor Cosmetics.md)). |
| Holding the `permission` node | Appears automatically, no `/gc give` needed. |
| Operator / **Dev Mode** | Every cosmetic appears as owned. |

---

## **Minimal example**

```json
"party_hat": {
  "DisplayName": "<light_purple>Party Hat",
  "slot": "HEAD",
  "type": "default",
  "permission": "",
  "parts": [
    { "customModelData_or_ID": "party_hat", "anchor": "HEAD" }
  ]
}
```

With `assets/greatcosmetics/textures/icons/party_hat.png` in the resource pack, `/gc give party_hat <player>` and it shows up in the wardrobe's **Head** category.
