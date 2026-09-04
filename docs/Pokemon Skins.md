# **Pokémon Skins**

---

A **Pokémon Skin** applies a Cobblemon **aspect** (like `summer`, `clone`, `mega`) to one of the player's party Pokémon, changing its look. Players manage them in the **Party** tab of the wardrobe.

Catalog file: **`config/GreatCosmetics/pokeskins.json`**. Requires **Cobblemon**.

---

## **Skin fields**

```json
[
  {
    "id": "pikachu_summer",
    "displayName": "Beach Pikachu",
    "species": "pikachu",
    "aspect": "summer",
    "cooldownMinutes": 60,
    "altForms": [],
    "group": ""
  }
]
```

| Field | Meaning |
| :--- | :--- |
| **id** | Unique identifier. Used by `/gc giveskin`. |
| **displayName** | MiniMessage name shown in the Party list. |
| **species** | Cobblemon species name the skin applies to — the player can only use it on that species. |
| **aspect** | The Cobblemon aspect string applied to the Pokémon. Can be a plain aspect (`summer`), a form (`f=alola`), or a composite feature (`battle_bond=ash`). |
| **cooldownMinutes** | Minutes before the player can re-apply this skin. `0` = no cooldown. |
| **altForms** | Optional list of extra aspects the **preview** can cycle (mega, gmax, regional…). Only affects the preview button; the applied skin is still `aspect`. |
| **group** | Optional theme name (`"League of Legends"`, `"Arcane"`…) used to visually group related skins in the list. Colors come from `skin_groups.json`. |

---

## **Using a skin (player)**

1. `/wardrobe` → **Party** tab.
2. Pick a party slot with the **`<` / `>`** arrows.
3. Browse the skins list; incompatible ones (wrong species / not owned) show a red status.
4. **Preview** (👁) shows the skin on a dummy Pokémon — cycle pose, alternate form and shiny before committing.
5. Click a compatible, owned, off-cooldown skin to apply it.

The **DEV** toggle (needs `gc.dev` / OP) shows every skin as owned for testing.

---

## **Skin groups & colors**

`config/GreatCosmetics/skin_groups.json` maps a group name to a color used for its header in the list:

```json
{ "League of Legends": "#c8aa6e", "Arcane": "#3b0e6d" }
```

---

## **Granting skins**

| Command | Effect |
| :--- | :--- |
| `/gc giveskin <skin_id> [player]` | Unlocks the skin for the target. |
| `/gc removeskin <skin_id> [player]` | Removes it. |

Ownership and per-skin cooldowns are stored in the database.

---

## **Clearing skins**

In Dev Mode, the Party tab has **Clear Current** (this Pokémon) and **Clear Party** (all six) buttons that strip every GreatCosmetics skin aspect. Players can also just apply a different skin.
