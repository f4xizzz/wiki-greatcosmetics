# **Integrations**

---

GreatCosmetics runs on **any Fabric server** — see [Dependencies](Dependencies.md) for the full list. Two mods unlock extra features when installed alongside it:

* **[Cobblemon Integration](Cobblemon Integration.md)** — Party tab, Pokémon Skins, Lure bonuses, Scanners, Heal Ability, Shiny & HA Radar, Shiny Effect.
* **[LuckPerms Integration](LuckPerms Integration.md)** — Chat Tags, Dev Studio Chat Tags page, per-cosmetic Granted Permissions, Effect-Blocked Groups.

Both are optional and both follow the same rule:

!!! info "The golden rule"
    Nothing in GreatCosmetics ever *requires* Cobblemon or LuckPerms to boot or to save data. Fields that belong to one of these integrations (Lure bonuses, scanners, Granted Permissions, …) are still stored in the cosmetic's config file even without the matching mod installed — they simply do nothing until it's present. Add the mod later, `/gc reload`, and everything that was already configured turns on immediately. Nothing needs re-entering.

---

## **Other optional integrations**

Small enough not to need their own page:

| Mod | Unlocks | Without it |
| :--- | :--- | :--- |
| [**Player Animation Lib**](https://modrinth.com/mod/playeranimator) *(client-side, "playeranimator")* | Fully suppresses another mod's custom idle animation (e.g. Emotecraft) while the wardrobe's **Breathing** toggle is off. | The Breathing toggle still zeroes vanilla's own idle sway, but a *third-party* animation mod's own idle motion (if the player has one installed) keeps playing — there's no way to reach into another mod's animation system without this library. |

See [Dependencies](Dependencies.md) for MySQL and resource-pack hosting, which aren't "integrations" in this sense — they're alternate backends GreatCosmetics talks to directly.

---

!!! info "Need another integration?"
    Open a ticket on our [Discord](https://discord.gg/GbbbNvQG3N) — we evaluate and prioritize requested integrations.
