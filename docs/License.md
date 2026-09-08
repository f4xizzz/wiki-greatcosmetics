# **License & Activation**

---

GreatCosmetics is a paid mod. On a **dedicated server** it stays locked until you activate a license key. The key is then bound to that server and validated against our backend.

**Singleplayer and integrated LAN worlds are always active** — no key, no internet check.

!!! tip "Free trial"
    Grab a free `GREATCOSMETICS-TRIAL-XXXX-XXXX` key on our [Discord](https://discord.gg/YgM4Ng4QGu) to try the mod on your server. One trial key works on any server; each server gets its own countdown that starts on its first activation, and the mod locks itself when that trial runs out.

---

## **Activating**

1. Get a key on our [Discord](https://discord.gg/YgM4Ng4QGu) — a free `GREATCOSMETICS-TRIAL-XXXX-XXXX` trial key, or a `GREATCOSMETICS-XXXX-XXXX` full key after purchase.
2. Join your server as a real operator.
3. Run:

    `/gc activation GREATCOSMETICS-XXXX-XXXX`

On success the server writes `config/GreatCosmetics/license.json` and unlocks everything. The license is re-validated against the backend every 4 hours.

!!! info "One server per key"
    On first activation the key is bound to that server instance. Your public IP can change (dynamic IP, host migration) without breaking activation, but the key will not work on a second, different server at the same time. Contact support on Discord to move a key to a new machine.

!!! info "Backend outages don't take you down"
    If the backend is temporarily unreachable, an already-activated server keeps running for a grace period while it retries in the background. You only lose access if the key is actually revoked or expires.

---

## **While unlicensed**

On a dedicated server without a valid license:

* Every `/gc` and `/wardrobe` command is blocked (players see a "no valid license" notice), **except `/gc activation`**.
* Opening the wardrobe, equipping cosmetics/tags/skins, backpacks and all Dev Studio actions are blocked.
* The mod still loads — it just does nothing until activated.

---

## **Key types**

| Format | Behaviour |
| :--- | :--- |
| `GREATCOSMETICS-XXXX-XXXX` | Full key. Bound to your server. Lifetime unless issued as temporary. |
| `GREATCOSMETICS-XXXX-XXXX` *(temporary)* | Same, but expires at a set date; the mod locks itself when the date passes. |
| `GREATCOSMETICS-TRIAL-XXXX-XXXX` | Free trial. Works on any server; each server gets its own N-day countdown starting at its first activation. Locks when the trial ends. |

---

## **`license.json`**

Written and managed by the mod. Do **not** edit it — an invalid file simply fails verification and the mod stays locked until you run `/gc activation` again. Don't commit this file to version control; it's per-server.

---

## **Troubleshooting activation**

| Symptom | Cause / fix |
| :--- | :--- |
| "Activation failed. Invalid key, or bound to another server." | Key already bound elsewhere, revoked, or mistyped. |
| Activation hangs then fails on the first try | The backend was asleep (cold start ~30–60 s). Run the command again. |
| Works, then locks later | Temporary key expired, the key was revoked, or the backend was unreachable past the grace period. |
