# **Tags**

---

**Tags** are selectable chat prefixes. A player picks one in the **Tags** tab of the wardrobe; the mod applies it through **LuckPerms**.

Catalog file: **`config/greatcosmetics/tags.json`**. Requires **LuckPerms** to actually change the chat prefix — without it, Tags are preview-only.

---

## **Two kinds of Tag**

### Custom Tags

Created by staff in the Tags editor (or by hand in `tags.json`). A player **owns** a custom Tag if they hold **any** node in its `permissions` list, or received it via `/gc tags give`.

### Group Tags

Imported **automatically** from your LuckPerms groups on startup and on `/gc reload`:

* `displayName`, `weight` and `tag` (prefix) are read from the group.
* A player owns the Tag simply by being **in that group**.
* They are **never deletable** and can't be handed out with `/gc tags give`.
* Groups listed in `tagGroupBlacklist` (in `mainconfig.conf`, `default` by default) are skipped.

On join the mod auto-equips the player's highest-weight group Tag if they have no other Tag equipped.

---

## **Tag fields**

| Field | Meaning |
| :--- | :--- |
| **id** | Unique identifier (also the LuckPerms group name for group Tags). |
| **displayName** | MiniMessage name shown in the Tags menu and tooltip. |
| **description** | Optional MiniMessage line shown under the name on hover. |
| **tag** | The actual chat prefix (MiniMessage), e.g. `<gradient:#f00:#00f>[VIP]</gradient> `. Applied as a LuckPerms prefix node (weight 1000) while equipped. |
| **permissions** | Nodes **granted to the player** while this Tag is equipped, and the nodes that mark ownership of a custom Tag. |
| **minecraftTag** | Optional vanilla `/tag` command tag added to the player while equipped — useful for datapacks / scoreboards. |
| **isGroupTag** / **weight** | Set automatically for group Tags. |

---

## **Editor**

Tags tab → **DEV** toggle (needs `gc.dev` or OP) → **+ Create New Tag**, or the ✏ pencil on hover to edit. Fields: ID, Display Name, Description, TAG (prefix), Permissions (comma-separated), Minecraft Tag. **Save** writes to `tags.json` and broadcasts; **DELETE TAG** removes a custom Tag.

---

## **Equipping rules**

* Clicking a Tag you own equips it and removes the previous one.
* You can always **switch** Tags but never end up with **none** — trying to remove your current role's group Tag keeps it (you get a "can't remove your role's tag" message). Removing any other Tag falls back to your best group Tag, or to nothing only if you belong to no tagged group.

---

## **Commands**

| Command | Effect |
| :--- | :--- |
| `/gc tags give <tag_id> <player>` | Grant a **custom** Tag (creates a `player_tags` ownership row). |
| `/gc tags remove <tag_id> <player>` | Revoke a granted custom Tag (also unequips it if worn). |

Group Tags can't be given or removed by command — manage the LuckPerms group membership instead.

---

## **Example `tags.json` entry**

```json
{
  "vip": {
    "displayName": "<gold>VIP",
    "description": "<gray>Available to VIP members.",
    "tag": "<gold>[VIP] ",
    "permissions": ["greatcosmetics.tag.vip"],
    "minecraftTag": "gc_tag_vip"
  }
}
```
