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
3. On first startup the mod creates the folder **`config/greatcosmetics/`** with all its default config files, and generates a starter cosmetic so you can confirm it loaded.

!!! note "Client-only jar"
    The build also produces a `*-client.jar` with the **Dev Studio removed** and no database drivers. Give that one to your players in the modpack; keep the full jar on the server. Both must be the same version.

---

## **Step 2 — Configure the basics**

Open `config/greatcosmetics/` and adjust:

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

This binds the key to your server's IP and creates `config/greatcosmetics/license.json`.

!!! warning "One server per key"
    The security system permanently binds a key to the **first IP** that validates it. Key sharing and multi-activation are not possible. `-DEV-` keys are the exception (no IP-lock, no jar-hash check).

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
