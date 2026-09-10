# **Introduction**

---

## **Welcome to GreatCosmetics**

**GreatCosmetics** is a full cosmetics framework for **Fabric** `1.21.1` servers (NeoForge in testing). It gives your players a 3D *Avatar Studio* to browse and equip cosmetics on nine virtual body slots, plus chat tags, storage backpacks and particle effects — all editable **in-game**, with no restart, through the built-in **Dev Studio**.

It needs **only Fabric API**. Add **[Cobblemon](Dependencies.md)** and it unlocks Pokémon skins, the Party tab and the Cobblemon *Lure* bonus system; add **LuckPerms** for permission-tiered slots and automatic group chat tags. Without either, the mod still runs and every non-Pokémon feature works.

Every piece of text the mod shows (menus, chat, item names) is stored in editable JSON files and rendered through **MiniMessage**, so you control the language, colors and formatting without touching the code.

---

## **Main Features**

* **3D Avatar Studio (`/wardrobe`):** a rotating 3D preview of the player where cosmetics are equipped with a click, organized by category and searchable.
* **Nine virtual slots:** `HEAD, FACE, NECK, CHEST, BACK, WAIST, LEGS, FEET, HAND` — independent from the player's real armor, with per-slot and per-type limits and permission tiers.
* **Custom 3D models:** cosmetics render as flat item icons (Custom Model Data) **or** full animated **GeckoLib** models, positioned per-part with an in-game 3D gizmo. See [Making Models & Textures](Making Models.md).
* **In-game Dev Studio:** create and edit cosmetics, particle effects, accessory types, slots and server config live — changes broadcast to every online player.
* **Chat Tags:** custom prefixes plus automatic **LuckPerms** group tags, with an in-game editor.
* **Pokémon Skins:** aspect-based skins for the player's party Pokémon, with cooldowns, alternate forms and thematic groups.
* **Cosmetic Backpacks:** wearable backpacks that double as paged item storage.
* **Cobblemon Lure bonuses:** shiny rate, IV/EV, capture chance, hidden ability, fishing bonuses and more, attached to any cosmetic.
* **Particle Effects & Sounds:** trailing particles and per-action sounds (equip, walk, fly, sneak, idle…).
* **Armor → Cosmetic conversion:** turn real armor items into wardrobe cosmetics automatically.
* **Forced Resource Pack:** the mod can push its texture pack to clients on join and on `/gc reload`, no `server.properties` edits needed.

---

## **Development and Authorship**

GreatCosmetics was fully designed and programmed by **F4xizzz** — the Fabric/Java mod and the Node.js licensing backend.

---

!!! info "Official Community"
    Configuration questions, bug reports and update news happen on our official [**Discord**](https://discord.gg/YgM4Ng4QGu).
    *This documentation is kept up to date to give you the best setup experience for GreatCosmetics on your server.*
