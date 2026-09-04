# **License & Activation**

---

GreatCosmetics is a paid mod. On a **dedicated server** it stays locked until you activate a license key; the key is permanently bound to that server's IP by a signed backend.

**Singleplayer and integrated LAN worlds are always active** — no key, no internet check.

---

## **Activating**

1. Buy a key on our [Discord](https://discord.gg/aDCgBbvRe5) — you receive a `GREATCOSMETICS-XXXX-XXXX` key after payment.
2. Join your server as a real operator.
3. Run:

    `/gc activation GREATCOSMETICS-XXXX-XXXX`

On success the server writes `config/greatcosmetics/license.json` and unlocks everything. This file is checked (offline, via RSA signature) on every boot and re-validated against the backend every 4 hours.

!!! warning "One IP per key"
    The backend binds the key to the **first IP** that activates it. You cannot move a key to a new IP or share it. Contact support on Discord to reset a key you legitimately need to migrate.

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
| `GREATCOSMETICS-XXXX-XXXX` | Normal key. IP-locked, jar-integrity checked. Lifetime unless issued as temporary. |
| `GREATCOSMETICS-XXXX-XXXX` *(temporary)* | Same, but expires at a set date; the mod locks itself when the date passes. |
| `GREATCOSMETICS-DEV-XXXX-XXXX` | Developer key. **No IP-lock, no jar-hash check.** For your own test environments. |

---

## **`license.json`**

```json
{
  "license_key": "GREATCOSMETICS-XXXX-XXXX",
  "expires_at": -1,
  "signature": "base64-RSA-signature"
}
```

Do **not** edit it — the `signature` is verified against the mod's embedded public key on every startup. A tampered signature locks the mod. Don't commit this file to version control; it's per-server.

---

## **Troubleshooting activation**

| Symptom | Cause / fix |
| :--- | :--- |
| "Activation failed. Invalid key, or bound to another IP." | Key already used on another IP, revoked, or mistyped. |
| Activation hangs then fails on the first try | The backend was asleep (cold start ~30–60 s). Run the command again. |
| "Integrity check failed. Adulterated JAR." | Your jar's hash isn't registered for this release yet — use a `-DEV-` key, or ask support to register the release hash. |
| Works, then locks a few hours later | Temporary key expired, or the 4-hour re-validation failed (key revoked / server offline). |
| Log says "possible illegal mixin injection … Locking the mod" | Another mod is touching the license classes. The mod locks itself (the server keeps running). Remove the offending mod or contact support. |
