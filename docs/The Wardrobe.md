# **The Wardrobe**

---

Players open the **Avatar Studio** with `/wardrobe`. It's a full-screen 3D view of their character with a tabbed side panel. Staff can open it for someone else with `/wardrobe <player>`.

While the wardrobe is open the player is frozen in place and the HUD is hidden; closing it (or `Esc`) returns them exactly where they were — even after a crash or disconnect (a fail-safe teleports them back on next join).

---

## **Camera controls**

| Input | Action |
| :--- | :--- |
| Left-click + drag | Rotate the view around the character |
| Scroll wheel | Zoom in / out |
| Right-click + drag | Pan the camera |

Some categories lock the zoom to frame the relevant body area (e.g. picking **Head** zooms to the face).

---

## **Tabs**

The tab bar sits at the top. A tab that isn't hovered/active collapses to a **one-letter prefix** (`A`, `C`, `P`, `T`, `D`) — those letters, and the full names, are all editable in the [language files](Language.md) (`wardrobe.tab.*` and `wardrobe.tab.*.short`).

**Party** only appears when the server runs **Cobblemon**; **Tags** only when it runs **LuckPerms**; **Dev Studio** only for real operators. On a plain Fabric server you'll just see Accessories and Preview.

### **Accessories**

The main tab. Shows every cosmetic the player **owns**, in a 4-column grid.

* **Category dropdown** — `All`, then one entry per virtual slot.
* **Search box** — filters by displayed name.
* **★ Favorites** — click the star on a cosmetic to pin it to the top of the list.
* **Click a cosmetic** — equips it (or unequips it if already worn). A green border marks equipped items.
* **X button** (top-right) — "Clear All": removes every equipped cosmetic at once.
* **Hover** — a tooltip lists the cosmetic's attributes: armor, abilities (flight / backpack / auto-feed), passive potion effects, and Lure bonuses.

### **Preview**

Armor visibility toggles. Each button hides/shows one real armor piece **for everyone who sees this player**:

* Helmet · Chestplate · Leggings · Boots

Useful so a hat cosmetic isn't blocked by a real helmet.

A fifth toggle — **Others' cosmetics** — is a **local** setting: turn it off and *you* stop seeing everyone else's cosmetics (your own still render). Saved per-client in `config/GreatCosmetics/client_local.json`, never sent to the server.

### **Party**

Pokémon Skins for the player's Cobblemon party. Pick a party slot with the arrows, browse available skins, and apply one (subject to its cooldown and species match). A live 3D preview lets you cycle poses, alternate forms and shiny before committing. See [Pokemon Skins](Pokemon Skins.md).

### **Tags**

Chat prefix selector (needs **LuckPerms**). Owned Tags are listed first, locked ones (with a 🔒) after. Click to equip. Staff with `gc.dev` get a **DEV** toggle here to preview and manage Tags — including **Add** / **Set** buttons for LuckPerms groups. See [Tags](Tags.md).

### **Dev Studio**

Only visible to **real operators**. The in-game editor for cosmetics, effects, types, slots and server config. See [Dev Studio](Dev Studio.md).

---

## **Equipped slots drawer**

A small drawer on the side shows the player's nine virtual slots and what's equipped in each. Operators / `gc.dev` holders also get a **Dev: ON/OFF** toggle here — Dev Mode makes every cosmetic and Tag appear as owned so you can preview them.

---

## **Studio backgrounds**

`/gc wardrobe setbackground <name>` saves your current position as a named scene. Then `/wardrobe <player> <name>` opens the wardrobe for that player **at that location** — handy for a decorated "dressing room" build. Saved in `config/GreatCosmetics/studios.json`.

---

## **The Wardrobe Block**

A placeable, GeckoLib-animated piece of furniture that opens the same wardrobe view without any command — right-click it and it plays an **open** animation, closing again (instant snap, no in-between GeckoLib blend) once the player leaves.

* Find it in the **GreatCosmetics** creative tab, or `/give <player> greatcosmetics:wardrobe`.
* It's a **multiblock**: an 18-cell footprint (a flat 3×3 rectangle, plus an identical invisible layer right behind it for depth). Only the block you clicked to place is visible/interactive — the rest is solid but invisible collision, and breaking *any* cell of the structure removes the whole thing.
* Right-clicking opens the wardrobe with the camera **locked**: the player faces the block (so their back is to it, front to the camera) and dragging to rotate the view is disabled — only the scroll-wheel zoom still works. Nothing in the tab bar (page switches, category filters, etc.) is allowed to nudge the camera either.
* Two extra controls appear that don't exist in the `/wardrobe` command view:
    * **`<` / `>` arrows** (styled like the Party tab's Pokémon-switch arrows) — spin the character 30° left/right so you can see it from different angles without touching the locked camera.
    * A **focus button** (top-right, above the equipped-slots drawer) that cycles the camera's vertical focus point between **Head**, **Body**, **Legs** and **Feet**.
* The **Dev Studio** tab is hidden here even for real operators — the block is meant as a player-facing fitting room, not an admin shortcut.

---

## **Quick Actions Menu**

Press **`V`** (rebindable under *Controls → GreatCosmetics*) anywhere in the world to open a radial "wheel" menu — same layout idea as Cobblemon's Pokémon interact wheel — listing quick shortcuts for whatever [Special Effects](Attributes.md#special-effects) the player currently has equipped:

| Slot | Always shown? | Behavior |
| :--- | :--- | :--- |
| **Open PC** | Always | Runs `/pc` instantly, from anywhere. |
| **Heal Party Now** | Only if a Heal Ability cosmetic is equipped | Heals the Cobblemon party right away, skipping the Shift-hold. |
| **Pollinate Now** | Only if a Pollinator cosmetic is equipped | Triggers the bone-meal burst right away, skipping the Shift-hold. |
| **Vein Miner** / **Tree Capitator** | Only if that ability is equipped | Toggles it on/off for the current session — the wheel button itself turns **green** (on) or **red** (off) as an on/off indicator. Turning it off doesn't touch the cosmetic's config, and resets automatically on relog. |

Click a slot (or click empty space to cancel) — no other click, keyboard shortcut, or menu can open this while it's already up.
