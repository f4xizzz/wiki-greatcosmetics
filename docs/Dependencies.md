# **Dependencies**

---

GreatCosmetics's current release runs on **Fabric** for Minecraft `1.21.1` (Java `21+`). A NeoForge build is in testing.

## **Required — Fabric**

| Dependency | Notes |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.16` | Mod loader. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` or newer | Core hooks the Fabric build uses. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) `1.13.13+kotlin.2.4.10` or newer | Kotlin runtime — required by Cobblemon. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) `>= 13.0` (Fabric) | Cross-loader hooks GreatCosmetics is built on. Usually already installed by Cobblemon. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` (Fabric) | The Party tab, Pokémon Skins and the Lure system read Cobblemon data. |

## **Required — NeoForge** *(in testing, not released yet)*

| Dependency | Notes |
| :--- | :--- |
| [**NeoForge**](https://neoforged.net/) `21.1.133` or newer | Mod loader. |
| [**Kotlin for Forge**](https://modrinth.com/mod/kotlin-for-forge) `5.7.0` or newer | Kotlin runtime — required by Cobblemon. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) `>= 13.0` (NeoForge) | Cross-loader hooks GreatCosmetics is built on. Usually already installed by Cobblemon. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` (NeoForge) | Same features as on Fabric. |

!!! note "Bundled libraries"
    **GeckoLib** (the animated 3D model renderer), the **adventure / MiniMessage** text library, and the SQLite / MySQL JDBC drivers are shipped *inside* the GreatCosmetics jar on both loaders. You never add them manually.

---

## **Optional**

| Dependency | What it enables |
| :--- | :--- |
| [**LuckPerms**](https://luckperms.net/) | Permission nodes (per-slot / per-type limits, per-cosmetic permissions, command permissions) **and** the automatic group-based chat Tags. Without it, only server operators can use restricted features and group Tags are cosmetic-only. |
| **MySQL server** | Optional external database instead of the built-in local SQLite. See [Storage](Storage.md). |
| A resource-pack host (Dropbox / GitHub / your own web server) | Needed only if you use the **Forced Resource Pack** feature. See [Resource Pack](Resource Pack.md). |

---

!!! info "Need another integration?"
    If your server relies on a permission or chat system we don't support yet, open a ticket on our [Discord](https://discord.gg/YgM4Ng4QGu) — we evaluate and prioritize requested integrations.
