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

### **Party**

Pokémon Skins for the player's Cobblemon party. Pick a party slot with the arrows, browse available skins, and apply one (subject to its cooldown and species match). A live 3D preview lets you cycle poses, alternate forms and shiny before committing. See [Pokemon Skins](Pokemon Skins.md).

### **Tags**

Chat prefix selector. Owned Tags are listed first, locked ones (with a 🔒) after. Click to equip. Staff with `gc.dev` get a **DEV** toggle here to preview and manage Tags. See [Tags](Tags.md).

### **Dev Studio**

Only visible to **real operators** (and only in the full server jar). The in-game editor for cosmetics, effects, types, slots and server config. See [Dev Studio](Dev Studio.md).

---

## **Equipped slots drawer**

A small drawer on the side shows the player's nine virtual slots and what's equipped in each. Operators / `gc.dev` holders also get a **Dev: ON/OFF** toggle here — Dev Mode makes every cosmetic and Tag appear as owned so you can preview them.

---

## **Studio backgrounds**

`/gc wardrobe setbackground <name>` saves your current position as a named scene. Then `/wardrobe <player> <name>` opens the wardrobe for that player **at that location** — handy for a decorated "dressing room" build. Saved in `config/greatcosmetics/studios.json`.
