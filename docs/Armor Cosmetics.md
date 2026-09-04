# **Armor Cosmetics**

---

An **armor cosmetic** ties a wardrobe cosmetic to a **real item**. When a player joins holding that item anywhere in their inventory, the mod removes the real item and unlocks the cosmetic version in their wardrobe.

It's how you turn "a custom diamond helmet skin" that already exists as an item on your server into a proper cosmetic — the player keeps the look, frees the armor slot, and can toggle it in the wardrobe.

Catalog file: **`config/greatcosmetics/armor_cosmetics.json`**.

---

## **Creating one**

Dev Studio → **Cosmetics** page → **+ Armor**. The editor is the same as a normal cosmetic except:

* The ID is **not editable** (renaming would break the map key).
* You set a **Real Item** field instead — a Minecraft/mod item id like `minecraft:diamond_helmet` or `cobblemon_armory:something`.

Everything else — Display Name, Slot, 3D model / GeckoLib model, attributes, Lure, sounds — works exactly like a standard cosmetic.

---

## **Default entry**

```json
{
  "convertedItems": {
    "diamond_helmet": {
      "itemId": "minecraft:diamond_helmet",
      "slot": "HEAD",
      "type": "armor_cosmetic"
    }
  }
}
```

* The key (`diamond_helmet`) is the cosmetic id used by `/gc give`, tags, etc.
* `itemId` is the real item it represents.

!!! warning "Item must exist"
    If `itemId` points to an item that isn't loaded (mod not installed, typo), the console prints a warning and the entry is ignored.

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
