# **FAQs**

---

## **Frequently Asked Questions**

### **1. Players open `/wardrobe` but every cosmetic is missing / broken.**

Almost always the **resource pack** isn't loaded on the client. GreatCosmetics ships models and textures in its own jar for the built-in cosmetics, but any cosmetic you add yourself needs a resource pack on the client with the matching `models/`, `textures/icons/`, `geo/` and `textures/` files. Enable the [Forced Resource Pack](Resource Pack.md) or add the pack to the modpack.

---

### **2. The server says "no valid license" and nothing works.**

You are on a dedicated server without an activated key. Run `/gc activation GREATCOSMETICS-XXXX-XXXX`. If activation fails:

* The key may already be bound to another server (keys are single-server).
* The licensing backend may be waking up — the first request after idle can take up to a minute; try again.
* Make sure you are running the unmodified official jar.

See [License & Activation](License.md).

---

### **3. Do I need LuckPerms?**

Not to run the mod, but strongly recommended. Without it: only operators can use `/gc` subcommands or the Dev Studio, per-slot/per-type limit tiers do nothing, per-cosmetic permission gating can't be used, and **group Tags** show but never apply a real prefix.

---

### **4. Where do I add my own 3D models?**

Drop the files into a resource pack and reference them by name in the Dev Studio. Conventions:

* **Flat icon:** `assets/greatcosmetics/textures/icons/<name>.png`
* **Vanilla model:** `assets/greatcosmetics/models/<name>.json`
* **GeckoLib model:** `geo/item/<name>.geo.json` + `textures/item/<name>.png` (+ optional `animations/item/<name>.animation.json`) — in **any** namespace.

See [Parts & Models](Parts and Models.md).

---

### **5. Can cosmetics give real stats (armor, flight, speed)?**

Yes. Any cosmetic can grant armor points, toughness, creative-style flight, ground/fly/swim speed multipliers, auto-feed, and permanent potion effects. See [Attributes & Abilities](Attributes.md). It can also carry Cobblemon **Lure** bonuses (shiny rate, IVs, capture chance, fishing…) — see [Lure System](Lure System.md).

---

### **6. A player's real diamond helmet turned into a cosmetic. Why?**

You configured that item in `armor_cosmetics.json` (or the Dev Studio "+ Armor" button). When a player joins holding a matching real item, the mod removes it from the inventory and unlocks the cosmetic version in the wardrobe. See [Armor Cosmetics](Armor Cosmetics.md).

---

### **7. I edited a config file and nothing changed.**

Run `/gc reload`. For `mainconfig.conf` and the `lang/` files this is enough. Cosmetic **models** (GeckoLib `.geo`) also need the client's resource pack to be current — `/gc reload` re-pushes it if you use the Forced Resource Pack.

---

### **8. How do I translate the mod / change its messages?**

Everything is in `config/greatcosmetics/lang/*.json`, one file per area, all rendered through MiniMessage. Edit the values, `/gc reload`. See [Language & MiniMessage](Language.md).

---

!!! tip "Still stuck?"
    Open a **support ticket** on our [Discord](https://discord.gg/aDCgBbvRe5) with your `latest.log` and a description of what you expected.
