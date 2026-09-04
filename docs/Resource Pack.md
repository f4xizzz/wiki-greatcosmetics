# **Resource Pack**

---

The cosmetics that ship with the mod have their models and textures **inside the jar**. Anything you add yourself lives in a **resource pack** that must reach the client.

---

## **What goes in the pack**

All under `assets/greatcosmetics/` unless noted:

| Path | Purpose |
| :--- | :--- |
| `textures/icons/<name>.png` | Flat inventory-style icon (16×16 or larger). The most common case. |
| `models/<name>.json` | A vanilla item model (optional — only if you want a custom flat/3D vanilla model instead of a plain icon). |
| `geo/item/<name>.geo.json` | A **GeckoLib** geometry file — in **any** namespace, not just `greatcosmetics`. |
| `textures/item/<name>.png` | The texture for that GeckoLib model — any namespace. |
| `animations/item/<name>.animation.json` | Optional GeckoLib animation — any namespace. |

The **name** is what you type into the cosmetic's part field in the [Dev Studio](Parts and Models.md). With **Exact Path** mode on, the field becomes a full relative path (`folder/name`) resolved in any namespace.

`autoDetectModels` in `mainconfig.conf` (default on) lets the mod scan the pack and wire up the Custom Model Data overrides for you.

---

## **Getting the pack to clients**

### Option A — Modpack

Ship the resource pack in your modpack / server pack. Simplest if you control the client install.

### Option B — Forced Resource Pack (recommended)

Let the mod push the pack on join and on `/gc reload`. In [`mainconfig.conf`](Main Config.md):

```json
"forceTexture": true,
"textureId": "greatcosmetics",
"textureUrl": "https://your-host.example/greatcosmetics-pack.zip",
"textureSha1": ""
```

* **`textureUrl`** must be a **direct download** of the `.zip` (Dropbox `?dl=1`, a GitHub release asset, your own web server…). Google Drive share links do **not** work.
* Leave **`textureSha1`** empty — the mod downloads the file, computes the real SHA-1, and caches it. It re-checks on `/gc reload` and re-pushes if the file changed.
* **`textureId`** is any label; it just needs to change if you want clients to treat it as a different pack.

!!! note "Only one forced pack"
    Minecraft applies one server resource pack at a time. If your server already forces a pack via `server.properties` or another mod, merge the GreatCosmetics assets into that pack instead of using `forceTexture`.

---

## **Light / Dark textures**

Players can run `/lightmode` or `/darkmode` on the client to switch the wardrobe GUI theme; the mod reloads client resources so a pack that provides both light and dark variants swaps instantly.

---

## **Troubleshooting**

* **Everything is a purple/black missing texture** → the client has no pack, or the pack failed to download. Check the client's `latest.log` for a resource pack download error.
* **One cosmetic looks generic while others are fine** → that cosmetic's `models/<id>.json` or `textures/icons/<id>.png` is missing. The console prints a `WARNING` naming the file it expected.
* **GeckoLib model is invisible** → the `geo/item/<name>.geo.json` **or** `textures/item/<name>.png` is missing; the console prints which one.
* Always `/gc reload` after changing the pack so the forced-pack SHA-1 updates.
