# **Integrations**

---

GreatCosmetics runs on **any Fabric server** — see [Dependencies](Dependencies.md) for the full list. This page is the map of what changes when two specific mods are also installed: **Cobblemon** and **LuckPerms**. Both are optional and both follow the same rule:

!!! info "The golden rule"
    Nothing in GreatCosmetics ever *requires* Cobblemon or LuckPerms to boot or to save data. Fields that belong to one of these integrations (Lure bonuses, scanners, Granted Permissions, …) are still stored in the cosmetic's config file even without the matching mod installed — they simply do nothing until it's present. Add the mod later, `/gc reload`, and everything that was already configured turns on immediately. Nothing needs re-entering.

---

## **Cobblemon**

Requires **Cobblemon `1.8.0`** or newer (see [Dependencies](Dependencies.md)). Everything below is either hidden from the UI or silently inert without it.

| Feature | Where | Details |
| :--- | :--- | :--- |
| **Party tab** | `/wardrobe` | Lets a player browse and apply [Pokémon Skins](Pokemon Skins.md) to their party. |
| **Cobblemon Effects popup** | Dev Studio → cosmetic editor → `>> Cobblemon Effects` | Holds everything below. |
| **Lure bonuses** | Cobblemon Effects popup | Shiny odds, guaranteed IVs, EV gain, capture chance, hidden ability, EXP, friendship, wild-spawn type boost, fishing bonuses. See [Cobblemon Effects](Lure System.md). |
| **Scanners** (IVs / Nature / Ability / Size / Dex) | Cobblemon Effects popup | Show extra info above/beside nearby Pokémon while equipped. See [Cobblemon Effects § Scanners](Lure System.md#scanners). |
| **Heal Ability** | Cobblemon Effects popup | Heals the player's whole party, HP/status/PP, on a Shift-hold or a Quick Actions click. See [Special Effects](Attributes.md#special-effects). |
| **Shiny & HA Radar** | Cobblemon Effects popup | Warns the player when a wild shiny/Hidden-Ability Pokémon is nearby. See [Special Effects](Attributes.md#special-effects). |
| **Shiny Effect** | Cobblemon Effects popup | Applies Cobblemon's own shiny particle + sound to the *player*, using the real Cobblemon asset (not a generic particle). |
| **Pokémon Skins** | Party tab / Dev Studio | An entire cosmetic sub-system for reskinning a Pokémon species (see [Pokémon Skins](Pokemon Skins.md)) — the whole feature needs Cobblemon by definition. |

### **Without Cobblemon**

* The **Party** tab doesn't appear in the wardrobe.
* The Cobblemon Effects popup (and everything inside it) doesn't appear in the Dev Studio.
* Any Lure/scanner/Heal Ability/Radar/Shiny Effect values already saved on a cosmetic stay in the config file untouched — they just don't do anything until Cobblemon comes back.
* Every other cosmetic feature (models, sounds, attributes, backpacks, armor cosmetics, particle effects, NPC cosmetics, Tags, the wardrobe itself) works exactly the same.

---

## **LuckPerms**

GreatCosmetics uses the **Fabric permissions API**, which LuckPerms implements — see [Permissions](Permissions.md) for the full node reference. This section is the "what needs LuckPerms specifically" overview.

| Feature | Where | Details |
| :--- | :--- | :--- |
| **Chat Tags** | `/wardrobe` → Tags tab | Prefix selector; owning a **custom** Tag needs a permission node, owning a **group** Tag needs LuckPerms group membership. See [Tags](Tags.md). |
| **Dev Studio → Chat Tags** | Dev Studio | The in-game Tag editor — same data as the Tags tab. |
| **Granted Permissions** *(per cosmetic)* | Dev Studio → cosmetic editor | A comma-separated list of permission nodes applied as **transient** (session-only) LuckPerms permissions while the cosmetic is equipped and its own `permission` gate passes. Removed on unequip. See [Permissions § Permissions and Tags granted BY a cosmetic](Permissions.md#permissions-and-tags-granted-by-a-cosmetic). |
| **Effect-Blocked Groups** | Dev Studio → Server Config | A server-wide, comma-separated list of LuckPerms groups whose players get **no cosmetic effects at all** — particles, potion effects, flight, speed, Lure, scanners, granted permissions/tags. The cosmetic model still renders; only the *gameplay effects* are suppressed. Handy for a "cosmetics-only, no gameplay advantage" rank. Empty by default (nobody blocked). |
| **Slot / type limits, command nodes** | Everywhere | Tiered nodes like `gc.slot.<slot>.<N>` or `gc.command.wardrobe.self`. See [Permissions](Permissions.md). |

!!! note "Minecraft Tags don't need LuckPerms"
    A cosmetic's **Minecraft Tags** field (vanilla scoreboard `/tag`) is completely independent of LuckPerms — it works on any Fabric server. Only **Granted Permissions** (real permission nodes) needs a permissions plugin behind it.

### **Without LuckPerms**

* Only real server operators (`ops.json`) pass any permission check — the Fabric permissions API falls back to op-only.
* The **Tags** tab and the Dev Studio **Chat Tags** page are hidden entirely.
* A cosmetic's **Granted Permissions** field still saves but never applies (no permission plugin to hand nodes to). Its **Minecraft Tags** field keeps working regardless (see note above).
* **Effect-Blocked Groups** has nothing to check membership against, so it's effectively a no-op.
* Slot/type/command permission checks still work (any Fabric permissions API backend other than LuckPerms would also work here) — LuckPerms is simply the one most servers already run.

---

## **Other optional integrations**

| Mod | Unlocks | Without it |
| :--- | :--- | :--- |
| [**Player Animation Lib**](https://modrinth.com/mod/playeranimator) *(client-side, "playeranimator")* | Fully suppresses another mod's custom idle animation (e.g. Emotecraft) while the wardrobe's **Breathing** toggle is off. | The Breathing toggle still zeroes vanilla's own idle sway, but a *third-party* animation mod's own idle motion (if the player has one installed) keeps playing — there's no way to reach into another mod's animation system without this library. |

See [Dependencies](Dependencies.md) for MySQL and resource-pack hosting, which aren't "integrations" in this sense — they're alternate backends GreatCosmetics talks to directly.

---

!!! info "Need another integration?"
    Open a ticket on our [Discord](https://discord.gg/GbbbNvQG3N) — we evaluate and prioritize requested integrations.
