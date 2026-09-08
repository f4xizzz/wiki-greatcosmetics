# **Commands**

---

The mod registers two roots: **`/greatcosmetics`** (alias **`/gc`**) and the standalone **`/wardrobe`**.

Every subcommand has its **own permission node** — see [Permissions](Permissions.md). Operators (real OP in `ops.json`) always pass. Nodes only work if **LuckPerms** (or another Fabric permissions provider) is installed.

---

## **Player Commands**

| Command | Description | Permission |
| :--- | :--- | :--- |
| `/wardrobe` | Opens the 3D Avatar Studio for yourself. | `gc.command.wardrobe.self` |
| `/backpack` *(keybind `B`)* | Opens your equipped cosmetic backpack (or a picker if you wear several). | — |

---

## **Staff Commands**

| Command | Description | Permission |
| :--- | :--- | :--- |
| `/wardrobe <player>` | Opens the wardrobe for another player. | `gc.command.wardrobe.other` |
| `/wardrobe <player> <background>` | Opens it and teleports the player to a saved studio background. | `gc.command.wardrobe.other` |
| `/gc give <cosmetic_id> [player]` | Unlocks a cosmetic in the target's wardrobe. | `gc.command.give` |
| `/gc giveitem <cosmetic_id> [player]` | Gives the **physical item** version of a cosmetic. | `gc.command.giveitem` |
| `/gc remove <cosmetic_id> [player]` | Removes a cosmetic from the target's wardrobe. | `gc.command.remove` |
| `/gc cosmetics equip <cosmetic_id> <player>` | Force-equips a cosmetic on a player, ignoring slot/type limits. | `gc.command.cosmetics.equip` |
| `/gc cosmetics unequip <cosmetic_id> <player>` | Force-unequips a cosmetic from a player. | `gc.command.cosmetics.unequip` |
| `/gc giveskin <skin_id> [player]` | Unlocks a Pokémon Skin for the target. | `gc.command.giveskin` |
| `/gc removeskin <skin_id> [player]` | Removes a Pokémon Skin from the target. | `gc.command.removeskin` |
| `/gc tags give <tag_id> <player>` | Grants ownership of a chat Tag (custom tags only). | `gc.command.tags.give` |
| `/gc tags remove <tag_id> <player>` | Removes a granted Tag. | `gc.command.tags.remove` |
| `/gc npc equip <cosmetic_id>` | Equips a cosmetic on the NPC / Armor Stand you are looking at. | `gc.command.npc.equip` |
| `/gc npc remove <slot>` | Clears a virtual slot on the entity you are looking at. | `gc.command.npc.remove` |
| `/gc uuid` | Copies the UUID of the entity you are looking at (for NPC configs). | `gc.command.uuid` |
| `/gc wardrobe setbackground <name>` | Saves your current location as a named studio background. | `gc.command.wardrobe.setbackground` |

---

## **Admin / Owner Commands**

| Command | Description | Permission |
| :--- | :--- | :--- |
| `/gc reload` | Reloads all configs, re-syncs the catalog and re-pushes the resource pack. | `gc.command.reload` |
| `/gc debug` | Toggles verbose debug logging in the server console (and forwards client debug). | `gc.command.debug` |
| `/gc activation <key>` | Validates and activates the mod license for this server IP. **Never blocked by the license gate.** | `gc.command.activation` |

---

## **Keybinds**

Configurable in **Options → Controls → GreatCosmetics**:

| Default key | Action |
| :--- | :--- |
| `B` | Open your cosmetic backpack. |
| `U` | Toggle the server UI (`/ui on` / `/ui off`) — only useful if your server provides that command. |
| `Y` | Run `/warps` — server-dependent. |
| `P` | Run `/pc` — opens the Cobblemon PC. |

!!! note "License-locked server"
    On a dedicated server **without a valid license**, every `/gc` and `/wardrobe` command is blocked except `/gc activation`. Players see a "no valid license" message. Singleplayer is never affected.
