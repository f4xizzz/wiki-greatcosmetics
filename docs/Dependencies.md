# **Dependencies**

---

## **Required**

| Dependency | Notes |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.18.3` | Mod loader. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` or newer | Core hooks the mod is built on. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) `1.13.13+kotlin.2.4.10` or newer | Required by Cobblemon and by GreatCosmetics. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.7.3` | The Party tab, Pokémon Skins and the Lure system read Cobblemon data. |
| **GeckoLib** (Fabric, 1.21.1) | Renders the animated 3D cosmetic models. **Bundled inside the mod jar** — you do not install it separately. |
| **Minecraft** `1.21.1` · **Java** `21+` | Server and client. |

!!! note "Bundled libraries"
    GeckoLib, the **adventure / MiniMessage** text library, and the SQLite / MySQL JDBC drivers are shipped *inside* the GreatCosmetics jar. You never add them manually.

---

## **Optional**

| Dependency | What it enables |
| :--- | :--- |
| [**LuckPerms**](https://luckperms.net/) | Permission nodes (per-slot / per-type limits, per-cosmetic permissions, command permissions) **and** the automatic group-based chat Tags. Without it, only server operators can use restricted features and group Tags are cosmetic-only. |
| **MySQL server** | Optional external database instead of the built-in local SQLite. See [Storage](Storage.md). |
| A resource-pack host (Dropbox / GitHub / your own web server) | Needed only if you use the **Forced Resource Pack** feature. See [Resource Pack](Resource Pack.md). |

---

!!! info "Need another integration?"
    If your server relies on a permission or chat system we don't support yet, open a ticket on our [Discord](https://discord.gg/aDCgBbvRe5) — we evaluate and prioritize requested integrations.
