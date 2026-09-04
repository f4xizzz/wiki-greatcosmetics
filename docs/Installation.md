# **Installation**

---

## **Server Requirements**

| Requirement | Version |
| :--- | :--- |
| Minecraft | 1.21.1 |
| Fabric Loader | 0.18.3 or higher |
| Fabric API | 0.116.9+1.21.1 or higher |
| Java | 21 or higher |
| Cobblemon | 1.7.3 |
| Fabric Language Kotlin | 1.13.13+kotlin.2.4.10 or higher |

See [Dependencies](Dependencies.md) for download links.

---

## **Step 1 — Drop in the jar**

1. Place the GreatCosmetics `.jar` in your server's `mods/` folder (alongside Cobblemon, Fabric API and Fabric Language Kotlin).
2. Start (or restart) the server.
3. On first startup the mod creates the folder **`config/GreatCosmetics/`** with all its default config files, and generates a starter cosmetic so you can confirm it loaded.

!!! note "Same jar for players"
    There's only one jar — give players the exact same file you put on the server (same version). The Dev Studio and other admin tools are already restricted to operators and players with the specific permission, so there's no separate stripped-down build to distribute.

---

## **Step 2 — Configure the basics**

Open `config/GreatCosmetics/` and adjust:

| File | What to set | Page |
| :--- | :--- | :--- |
| `mainconfig.conf` | Database mode, slot/type limits, forced resource pack, startup commands | [Main Config](Main Config.md) |
| `lang/*.json` | Language, colors and every message the mod shows | [Language & MiniMessage](Language.md) |

Everything else (cosmetics, tags, effects, skins) is best edited **in-game** — see [Dev Studio](Dev Studio.md).

---

## **Step 3 — Activate the license**

On a **dedicated server**, GreatCosmetics stays locked until you activate a license key:

1. Join your server as an operator.
2. Run: `/gc activation GREATCOSMETICS-XXXX-XXXX`

This binds the key to your server instance and creates `config/GreatCosmetics/license.json`.

!!! warning "One server per key"
    On first activation the key is bound to that server instance. Your public IP can change without breaking activation, but a key cannot be shared or run on a second, different server. Contact support to migrate a key to a new machine.

!!! info "Singleplayer / LAN"
    In singleplayer or an integrated LAN world the mod is **always active** — no key needed. Activation is a dedicated-server concept.

Full details on [License & Activation](License.md).

---

## **Step 4 — Reload**

After editing config files, apply everything without a restart:

`/gc reload`

This reloads every config, recomputes model data, re-pushes the resource pack to online players and re-syncs the whole catalog.

---

### Done — the wardrobe is live. Players open it with `/wardrobe`.
