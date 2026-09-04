# **Language & MiniMessage**

---

Every piece of text the mod shows a player — GUI labels, chat feedback, item names and lore, action-bar messages — lives in editable JSON under **`config/greatcosmetics/lang/`**. There is no built-in "language" toggle: you edit the values to whatever language, wording and colors you want.

Console log lines are **not** in here — they stay in English inside the code.

---

## **The files**

One file per area. Keys are namespaced by file (`commands.reload.start`, `accessories.category.head`, …).

| File | Covers |
| :--- | :--- |
| `general.json` | Shared errors, the `/gc reload` flow, license messages |
| `commands.json` | Feedback for `/gc *` and `/wardrobe *` |
| `messages.json` | Server → player chat / action-bar (equip, flight, tags, effects, skins, armor conversion, join kick) |
| `items.json` | Cosmetic item name fallback, lore, Lure attribute lines, the Scanner tooltip |
| `wardrobe.json` | Screen title, tab names, panel title, the Preview tab toggles |
| `accessories.json` | Category names, "Clear All", search placeholder, every tooltip line |
| `party.json` | Pokémon Skins list, preview mode, pose / form / shiny labels |
| `tags.json` | Tags menu headers, tooltips, editor field labels |
| `backpack.json` | Backpack picker title, the "Page X/Y" overlay |
| `devstudio.json` | Every Dev Studio label, divider, button and popup |

On load, the mod fills in any **missing** keys from its English defaults and rewrites the file — your customized values are never overwritten. New keys added by future updates appear automatically.

---

## **Formatting — MiniMessage**

Values are parsed with **[MiniMessage](https://docs.advntr.dev/minimessage/format.html)**. You can use:

| Feature | Example |
| :--- | :--- |
| Named colors | `<red>`, `<gold>`, `<light_purple>` |
| Hex colors | `<#ff8800>` |
| Gradients | `<gradient:#ff0000:#0000ff>Rainbow</gradient>` |
| Decorations | `<bold>`, `<italic>`, `<underlined>`, `<st>` (strikethrough), `<reset>` |
| Hover | `<hover:show_text:'<yellow>Click to copy!'>...</hover>` |
| Click | `<click:copy_to_clipboard:'value'>...</click>` |

**Legacy codes still work** as a fallback — `&a`, `&l`, `§c`, and `&#rrggbb` are converted automatically before parsing. So `&a&lTEST` renders bold green.

Chat messages support real hover/click; GUI text is drawn with the legacy renderer, so hover/click there is ignored but colors (including hex) still apply.

---

## **Placeholders**

Some values contain `{name}` tokens the mod substitutes at runtime, e.g.:

```json
"commands.give.received": "<green>You received the cosmetic: <white>{item}",
"messages.cosmetic.slot_limit": "<red>[!] You've reached the item limit for the {slot} slot (Limit: {limit})."
```

Keep the token spelled exactly (`{item}`, `{slot}`, `{limit}`, `{id}`, `{player}`, `{value}`, …) — remove it and the substitution just won't happen.

---

## **Example**

```json
// accessories.json
"accessories.category.head": "<gradient:#a855f7:#6d28d9><bold>Head</bold></gradient>",
"accessories.tooltip.fly": " <yellow>✦ <white>Grants Flight"
```

`/gc reload`, reopen the wardrobe — the Head category renders with a purple gradient.

---

## **Client vs. server**

Client and server each read **their own** `config/greatcosmetics/lang/` from disk — there is **no network sync**. Distribute the same `lang/` folder with your modpack. If they differ, the GUI uses the client's copy and chat uses the server's.

---

## **Migrating an old `lang.json`**

Older builds used a single `config/greatcosmetics/lang.json`. On first run of a new build the mod imports any values you customized there into the new split files (under their new key names) and renames the old file to `lang.json.migrated`.
