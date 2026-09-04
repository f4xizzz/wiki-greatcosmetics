# **Migrating (Legacy)**

---

GreatCosmetics evolved from an older cosmetics system that stored cosmetics as **`carved_pumpkin` items with a `custom_model_data` number**. If your server used that, players may still be holding those old items. The migration system swaps them for the new cosmetic entries automatically.

Config file: **`config/GreatCosmetics/legacy_cosmetic_migration.json`**.

---

## **How it works**

The file is a map of **old `custom_model_data` number → new cosmetic id**:

```json
{
  "1": "party_hat",
  "42": "cool_scarf",
  "77": "wizard_robe"
}
```

On join (and continuously), the mod scans the player's inventory. When it finds a `carved_pumpkin` with `custom_model_data: 42`, it:

1. Removes the old item.
2. Unlocks and equips the cosmetic `cool_scarf` for the player.
3. Sends a chat message ("Your old cosmetic was automatically migrated to: …", text in `lang/messages.json`).

---

## **Setting it up**

1. List every old CMD number and the new cosmetic id it should become. The new cosmetic must **already exist** in the catalog (create it in the [Dev Studio](Dev Studio.md) first).
2. `/gc reload`.

!!! warning "Missing target"
    If a mapping points to a cosmetic id that doesn't exist yet, the mod logs a warning and **skips** that item (it is not removed) until you create the cosmetic or fix the id. Nothing is lost.

---

## **Migrating from the `lang.json` file**

Unrelated to the item migration: older builds kept all text in one `config/GreatCosmetics/lang.json`. The current build automatically imports your customized values into the new split `lang/*.json` files and renames the old file to `lang.json.migrated`. See [Language & MiniMessage](Language.md).

---

## **Migrating the database**

To move player data between SQLite and MySQL, see [Storage → Migrating](Storage.md#migrating-sqlite--mysql).
