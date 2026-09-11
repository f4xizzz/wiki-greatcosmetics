# **Armor Cosmetics**

---

An **armor cosmetic** ties a wardrobe cosmetic to a **real item**. When a player joins holding that item anywhere in their inventory, the mod removes the real item and unlocks the cosmetic version in their wardrobe.

It's how you turn "a custom diamond helmet skin" that already exists as an item on your server into a proper cosmetic — the player keeps the look, frees the armor slot, and can toggle it in the wardrobe.

Catalog file: **`config/GreatCosmetics/armor_cosmetics.json`**.

---

## **Creating one**

Dev Studio → **Cosmetics** page → **+ Armor**. The editor is the same as a normal cosmetic except:

* The ID is **not editable** (renaming would break the map key).
* You set a **Real Item** field instead — a Minecraft/mod item id like `minecraft:diamond_helmet` or `cobblemon_armory:something`.

Everything else — Display Name, Slot, 3D model, attributes, potion effects, granted permissions/tags, Lure, sounds — works exactly like a standard cosmetic, and applies **while the real item is worn in its real armor slot** (it never occupies a virtual slot the way normal cosmetics do).

The parts render the **real 3D armor model** (the actual vanilla/mod armor mesh, not a flat icon), placed on the bone matching each part's **Anchor** — see [Dev Studio → Editing a part](Dev Studio.md#editing-a-part) for the auto-split button that lays out a chestplate/leggings/boots into the right body parts automatically, and the [3D gizmo](Parts and Models.md#the-3d-gizmo) for nudging each one.

---

## **Default entry**

A fresh install (no `armor_cosmetics.json` yet) generates one example — a **Turtle Shell**, chosen because it's a natural way to show that armor points/toughness/tooltip *and* potion effects can all come from an armor cosmetic:

```json
{
  "convertedItems": {
    "turtle_helmet": {
      "itemId": "minecraft:turtle_helmet",
      "slot": "HEAD",
      "type": "armor_cosmetic",
      "effects": ["minecraft:water_breathing:1"]
    }
  }
}
```

* The key (`turtle_helmet`) is the cosmetic id used by `/gc give`, tags, etc.
* `itemId` is the real item it represents.
* `effects` grants **Water Breathing** while the piece is worn — see [Granting potion effects](#granting-potion-effects) below. (This entry only generates on a brand-new install; an existing `armor_cosmetics.json` with the old `diamond_helmet` example is left untouched — edit or delete it by hand if you want the new example instead.)

!!! warning "Item must exist"
    If `itemId` points to an item that isn't loaded (mod not installed, typo), the console prints a warning and the entry is ignored.

---

## **Granting potion effects**

An armor cosmetic's **Special Effects → `>> Select Effects`** field (the same one a normal cosmetic uses) works here too: any potion effect listed there is applied while the real item is worn, and removed the moment it's taken off.

This is **not** the mod reading a vanilla effect off the real item — it's independent of whatever the real item would normally do. The stock example above is a good illustration: a real Turtle Shell's Water Breathing is hard-coded by vanilla Minecraft to that exact item in the real head slot, it isn't exposed as something the mod could "copy" — so the armor cosmetic instead grants Water Breathing itself, through its own `effects` list, for as long as the piece is equipped (not only while underwater, unlike the vanilla effect). Use the same field to attach any potion effect to any armor cosmetic, regardless of what the real item does normally.

---

## **How the conversion works**

On player join:

1. The mod scans the player's inventory for any real item registered here.
2. It **removes** the item and calls `unlockCosmetic` for the matching cosmetic id.
3. The player gets a chat message ("Your *X* became a cosmetic! …", text in `lang/messages.json`).
4. The cosmetic version now shows in the wardrobe.

`/gc give <armor_cosmetic_id>` also works — it unlocks the cosmetic without needing the physical item.

`/gc giveitem <armor_cosmetic_id>` gives the **real item** back (so a player can trade or drop it).

---

## **Removing an armor cosmetic**

Deleting it from the Dev Studio removes it from the catalog. Players who already had it unlocked keep the wardrobe entry until you also `/gc remove` it from them; the real-item ↔ cosmetic mapping is dropped so joining with the item no longer converts it.
