# **Dependencies**

---

GreatCosmetics's current release runs on **Fabric** for Minecraft `1.21.1` (Java `21+`). A NeoForge build is in testing.

The mod needs **only Fabric Loader + Fabric API**. Everything else is optional — Cobblemon and LuckPerms each *unlock extra features* when present, but the mod loads, the wardrobe works, and cosmetics render on a plain Fabric server without them.

## **Required — Fabric**

| Dependency | Notes |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.16` | Mod loader. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` or newer | Core hooks the Fabric build uses. |

That's it. The **GeckoLib** renderer, the **adventure / MiniMessage** text library, and the SQLite / MySQL JDBC drivers are shipped *inside* the GreatCosmetics jar — you never add them manually.

## **Required — NeoForge** *(in testing, not released yet)*

| Dependency | Notes |
| :--- | :--- |
| [**NeoForge**](https://neoforged.net/) `21.1.133` or newer | Mod loader. |

---

## **Optional integrations**

| Dependency | What it unlocks | Without it |
| :--- | :--- | :--- |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` | The **Party** tab, **Pokémon Skins**, the **Cobblemon Cosmetics / Lure** bonus system, and the IV / nature / ability / size **scanners**. | Those features are hidden. Any Lure/scanner data already saved on a cosmetic is kept in the file and ignored. All other cosmetic features work normally. |
| [**LuckPerms**](https://luckperms.net/) | Permission nodes (per-slot / per-type limits, per-cosmetic `permission`, granted permissions, command permissions) **and** the automatic group-based chat **Tags** tab. | Only server operators can use restricted features; the **Tags** tab and the Dev Studio **Chat Tags** page are hidden. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) | — | Only needed *because Cobblemon needs it*. Not required by GreatCosmetics itself. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) | — | Only needed *because Cobblemon needs it* on some setups. Not required by GreatCosmetics itself. |
| **MySQL server** | External database instead of the built-in local SQLite. See [Storage](Storage.md). | Uses the bundled SQLite file — fine for most servers. |
| A resource-pack host (Dropbox / GitHub / your own web server) | The **Forced Resource Pack** feature. See [Resource Pack](Resource Pack.md). | Ship the pack in your modpack instead. |

!!! tip "Running on a Cobblemon server"
    The common case. Install Cobblemon (which pulls in Kotlin + Architectury) and LuckPerms, drop in GreatCosmetics, and every feature is available. Nothing extra to configure.

!!! note "Running on a plain Fabric server"
    Also supported. Skip Cobblemon and LuckPerms entirely — the wardrobe, slots, GeckoLib models, particle effects, backpacks, armor cosmetics, sounds and NPC cosmetics all work. The Pokémon-specific tabs simply don't appear.

---

!!! info "Need another integration?"
    If your server relies on a permission or chat system we don't support yet, open a ticket on our [Discord](https://discord.gg/GbbbNvQG3N) — we evaluate and prioritize requested integrations.
