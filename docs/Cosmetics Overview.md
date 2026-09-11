# **Cosmetics Overview**

---

A **cosmetic** is one wearable entry in the catalog. It occupies one virtual slot, renders one or more 3D **parts** on the player, and can carry stats, abilities, effects, Lure bonuses and sounds.

The catalog lives in **`config/GreatCosmetics/cosmeticsconfig.conf`** (JSON despite the extension). You rarely edit it by hand — the [Dev Studio](Dev Studio.md) writes it for you and broadcasts changes live. This page explains what each field means.

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
| **tooltipDescription** | Optional MiniMessage lines (`\n`-separated) shown under the Display Name in the wardrobe. Blank = nothing extra. |
| **grantedPermissions** / **minecraftTags** | Comma-separated in the editor. Applied to the player while the cosmetic is worn and its `permission` gate passes; removed on unequip. See [Permissions](Permissions.md). |
| **unlockPermission** / **unlockTag** | If set, any player holding that node or scoreboard tag gets the cosmetic automatically — no database row, no `/gc give`. Lost the moment they no longer qualify. See [Permissions § Auto-Unlock](Permissions.md#auto-unlock). |
| **variants** | Optional alternative placements of the same model, each choosable separately in the wardrobe. See [Dev Studio § Variants](Dev Studio.md#variants). |
| **parts** | The list of 3D pieces — see [Parts & Models](Parts and Models.md). |

Plus the optional systems: **armor / toughness**, **EnableFly + speed multipliers**, **AutoFeed**, **effects** (potion — also works on [armor cosmetics](Armor Cosmetics.md)), **effectVisual / flyParticle / shiftParticle**, **isBackpack**, **lure**, **sounds** — each has its own page.

!!! warning "The mod itself has no cosmetic content"
    GreatCosmetics is the framework, not a model pack. A fresh `cosmeticsconfig.conf` has **no example virtual cosmetic** at all, and the couple of small examples the mod *does* include (an armor cosmetic — see [Armor Cosmetics](Armor Cosmetics.md) — plus a few flat/GeckoLib test models) are safe to keep and use on your server, but aren't meant to be your actual content. **The cosmetics shown in the mod's showcase video are not included with the mod** — you'll need to bring your own models (built by you following the pattern below and [Making Models](Making Models.md), bought — or soon to be sellable — from the official SaSDevelopment Discord, from anywhere else, or repurposed from another mod's armor). Still stuck after reading the docs? Hop into the [Discord](https://discord.gg/GbbbNvQG3N) and ask.

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
