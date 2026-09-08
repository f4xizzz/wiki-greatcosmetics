# **Main Config**

---

The file **`config/GreatCosmetics/mainconfig.conf`** holds server-wide settings: virtual slots, accessory types, the database, the forced resource pack and startup commands. It is generated on first startup and re-saved (with any missing keys filled in) every time it loads.

Apply changes with `/gc reload`.

---

## **Default Template**

```json
{
  "autoDetectModels": true,
  "compactStatusBars": true,
  "lureHud": true,
  "devModePermission": "gc.perm.devmode",
  "tagGroupBlacklist": ["default"],

  "useMySQL": false,
  "mysqlHost": "localhost",
  "mysqlPort": 3306,
  "mysqlDatabase": "greatcosmetics",
  "mysqlUser": "root",
  "mysqlPassword": "password",

  "slots": {
    "HEAD":  { "defaultLimit": 1, "permission": "gc.slot.head" },
    "FACE":  { "defaultLimit": 1, "permission": "gc.slot.face" },
    "NECK":  { "defaultLimit": 1, "permission": "gc.slot.neck" },
    "CHEST": { "defaultLimit": 1, "permission": "gc.slot.chest" },
    "BACK":  { "defaultLimit": 1, "permission": "gc.slot.back" },
    "WAIST": { "defaultLimit": 1, "permission": "gc.slot.waist" },
    "LEGS":  { "defaultLimit": 1, "permission": "gc.slot.legs" },
    "FEET":  { "defaultLimit": 1, "permission": "gc.slot.feet" },
    "HAND":  { "defaultLimit": 1, "permission": "gc.slot.hand" }
  },

  "types": {
    "necklace": { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.necklace" },
    "scarf":    { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.scarf" }
  },

  "forceTexture": false,
  "textureId": "greatcosmetics",
  "textureUrl": "",
  "textureSha1": "",

  "startupCommands": []
}
```

---

## **Parameters**

### **1. Models**

* **`autoDetectModels`** *(default `true`)* — lets the mod scan the resource pack and auto-generate the Custom Model Data overrides on the ghost item. Leave this on unless you build the item model JSON by hand.

### **2. HUD**

Both are client-visible toggles synced from the server; change them here and `/gc reload`.

* **`compactStatusBars`** *(default `true`)* — when a player's **maximum** health or armor goes past two full rows (20 points), the HUD shows one bar plus an `xN` multiplier instead of stacking squashed rows (health) or clipping the overflow (armor). Purely visual, and it only ever triggers if a player actually has >20 max health/armor from attributes or equipment — a vanilla-stats server never sees it. Set `false` for 100% vanilla bars.
* **`lureHud`** *(default `true`)* — shows the **aggregated Lure bonuses** (the summed total of every equipped Lure cosmetic / cosmetic-armor with `enabled: true`, exactly as the server applies them) in a column to the right of the hotbar. Hidden when no Lure is active, when the HUD is hidden (F1), or while a GUI is open. See [Lure System](Lure System.md).

### **3. Dev Mode**

* **`devModePermission`** *(default `gc.perm.devmode`)* — the permission node that grants the **Dev Mode** bypass (equip any cosmetic for testing without owning it). Change it if you want a different node name.

### **4. Tag Group Blacklist**

* **`tagGroupBlacklist`** — LuckPerms group names that are **never** imported as chat Tags (case-insensitive). Add internal/administrative groups here so they don't clutter the Tags menu. `default` is blacklisted out of the box. See [Tags](Tags.md).

### **5. Database**

* **`useMySQL`** *(default `false`)* — `false` uses the built-in local **SQLite** file (`config/GreatCosmetics/` … `greatcosmetics.db`). `true` connects to the MySQL server below.
* **`mysqlHost` / `mysqlPort` / `mysqlDatabase` / `mysqlUser` / `mysqlPassword`** — connection details, used only when `useMySQL` is `true`.

Full explanation on [Storage (Database)](Storage.md).

### **6. Slots**

`slots` maps each of the nine virtual slot names to:

* **`defaultLimit`** — how many cosmetics a normal player can wear in that slot.
* **`permission`** — the **base** node for the tiered limit system (`<base>.<N>`, `<base>.bypass`). See [Slots & Types](Slots and Types.md).

You can remove slots you don't want, but the nine names above are the only valid ones.

### **7. Types**

`types` is a free-form map — the key is the type name you'll type into a cosmetic's **Type** field. Each type has:

* **`slot`** — informational; which virtual slot this type belongs to.
* **`limitPerPlayer`** — max cosmetics of this type a player may wear at once.
* **`permission`** — base node for `<base>.<N>` / `<base>.bypass` tiers.

### **8. Forced Resource Pack**

Instead of `resource-pack` / `resource-pack-sha1` in `server.properties` (which need a restart), the mod can push the pack itself:

* **`forceTexture`** *(default `false`)* — enable pushing the pack on join and on `/gc reload`.
* **`textureId`** — any string; identifies the pack to the client (does not need to be a UUID).
* **`textureUrl`** — a **direct download** link to the `.zip` pack.
* **`textureSha1`** — leave blank; the mod computes the real SHA-1 automatically. Only set it if you host somewhere that needs a fixed value.

See [Resource Pack](Resource Pack.md).

### **9. Startup Commands**

* **`startupCommands`** — a list of commands run **as console** a few seconds after the server finishes starting (later than `SERVER_STARTED`, so mods/plugins that load slowly are ready). Example:

```json
"startupCommands": [ "lp group vip permission set gc.slot.head.3 true" ]
```

The Dev Studio → **Server Config** page can edit this list in-game.
