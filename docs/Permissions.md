# **Permissions**

---

GreatCosmetics uses the **Fabric permissions API** (provided by **LuckPerms**). A player passes a check if they are a real server operator (`ops.json`) **or** hold the node. Without a permissions mod, only operators pass and all group-based Tags become preview-only.

---

## **Command Nodes**

| Node | Command |
| :--- | :--- |
| `gc.command.wardrobe.self` | `/wardrobe` |
| `gc.command.wardrobe.other` | `/wardrobe <player>` |
| `gc.command.wardrobe.setbackground` | `/gc wardrobe setbackground` |
| `gc.command.give` | `/gc give` |
| `gc.command.giveitem` | `/gc giveitem` |
| `gc.command.remove` | `/gc remove` |
| `gc.command.cosmetics.equip` / `.unequip` | `/gc cosmetics equip` / `unequip` |
| `gc.command.giveskin` / `gc.command.removeskin` | `/gc giveskin` / `removeskin` |
| `gc.command.tags.give` / `gc.command.tags.remove` | `/gc tags give` / `remove` |
| `gc.command.npc.equip` / `gc.command.npc.remove` | `/gc npc equip` / `remove` |
| `gc.command.display` | `/gc display` / `remove` / `clear` |
| `gc.command.uuid` | `/gc uuid` |
| `gc.command.extraslot` | `/gc extraslot` |
| `gc.command.extratypeslot` | `/gc extratypeslot` |
| `gc.command.reload` / `gc.command.debug` / `gc.command.inspect` | `/gc reload` / `debug` / `inspect` |
| `gc.command.activation` | `/gc activation` |

---

## **Dev Studio Access**

| Node | Grants |
| :--- | :--- |
| `gc.dev` | Full Dev Studio: create/edit/delete cosmetics, effects, types, slots, and server config. Also lets the player toggle **Dev Mode** in the wardrobe (preview every cosmetic/tag without owning it). |
| `gc.perm.devmode` | Just the **Dev Mode** bypass — equip any cosmetic for testing without owning it. Node name is configurable via `devModePermission` in `mainconfig.conf`. |

!!! warning
    The **Dev Studio tab** additionally requires the player to be a **real operator**. `gc.dev` alone reveals the admin controls inside the Tags / Party tabs but not the full Dev Studio panel.

---

## **Owning Cosmetics**

* A cosmetic with a non-empty **`permission`** field is only shown/equippable to players who hold that exact node (or who unlocked it via `/gc give`, or who have Dev Mode).
* Players otherwise unlock cosmetics through `/gc give`, the physical item (`/gc giveitem`), or automatic armor conversion.

---

## **Auto-Unlock**

A cosmetic can also set an **Unlock Permission** and/or an **Unlock Tag** (Dev Studio → cosmetic editor → **Auto-Unlock** section). Whoever holds that permission node **or** that vanilla scoreboard tag gets the cosmetic automatically — no `/gc give`, no database row. It's **dynamic**: the moment the player no longer holds either one (LuckPerms group changed, `/tag remove`…), they lose access, and it's force-unequipped if they had it on.

This is different from the `permission` gate above: `permission` only decides *visibility/equippability* for a cosmetic the player must still separately own; Unlock Permission / Unlock Tag grant **ownership itself**, live.

---

## **Permissions and Tags granted BY a cosmetic**

Independent of the `permission` gate, a cosmetic (including an [armor cosmetic](Armor Cosmetics.md)) can have its own **Granted Permissions** and **Minecraft Tags** fields (comma-separated in the Dev Studio editor):

* Every node in **Granted Permissions** is added to the player as a **transient** LuckPerms permission (never written to LuckPerms storage) while the cosmetic is worn and its `permission` gate passes.
* Every tag in **Minecraft Tags** is applied as a vanilla `/tag`-style scoreboard tag under the same condition — handy for datapacks or `/execute if entity @s[tag=...]`.

Both are removed the instant the cosmetic is unequipped, and re-applied automatically on rejoin if it's still worn. Bonuses from several equipped cosmetics stack (the union of everything granted).

---

## **Slot Limits**

Each virtual slot has a base limit (`defaultLimit` in `mainconfig.conf`). Players raise it with tiered nodes off the slot's `permission` base (default `gc.slot.<slot>`):

| Node pattern | Effect |
| :--- | :--- |
| `gc.slot.<slot>.<N>` | Sets the slot's absolute limit to **N** (highest tier held, 1–20 wins). |
| `gc.slot.<slot>.bypass` | Unlimited (99) for that slot. |
| `gc.extraslot.<slot>.<N>` | **Adds** N extra items on top of the normal limit. |
| `gc.extraslot.all.<N>` | Adds N extra items to **every** slot. |

`<slot>` is lowercase: `head, face, neck, chest, back, waist, legs, feet, hand`.

---

## **Type Limits**

Accessory *types* (e.g. `necklace`, `scarf`) also carry a `limitPerPlayer` and a `permission` base (default `gc.type.<type>`):

| Node pattern | Effect |
| :--- | :--- |
| `gc.type.<type>.<N>` | Raises the per-player limit for that type to **N**. |
| `gc.type.<type>.bypass` | Unlimited (99) for that type. |
| `gc.extratypeslot.<type>.<N>` | **Adds** N extra items on top of the normal limit for that type. |
| `gc.extratypeslot.all.<N>` | Adds N extra items to **every** type. |

---

## **Tag Nodes**

* Each Tag lists its own `permissions` array — a player "owns" a custom Tag if they hold **any** node in that list (or received it via `/gc tags give`).
* **Group Tags** are owned automatically by being in the matching **LuckPerms group**.

See [Tags](Tags.md).
