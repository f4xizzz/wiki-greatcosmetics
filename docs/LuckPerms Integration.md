# **LuckPerms Integration**

---

GreatCosmetics uses the **Fabric permissions API**, which LuckPerms implements — see [Permissions](Permissions.md) for the full node reference. This page is the "what needs LuckPerms specifically" overview.

| Feature | Where | Details |
| :--- | :--- | :--- |
| **Chat Tags** | `/wardrobe` → Tags tab | Prefix selector; owning a **custom** Tag needs a permission node, owning a **group** Tag needs LuckPerms group membership. See [Tags](Tags.md). |
| **Dev Studio → Chat Tags** | Dev Studio | The in-game Tag editor — same data as the Tags tab. |
| **Granted Permissions** *(per cosmetic)* | Dev Studio → cosmetic editor | A comma-separated list of permission nodes applied as **transient** (session-only) LuckPerms permissions while the cosmetic is equipped and its own `permission` gate passes. Removed on unequip. See [Permissions § Permissions and Tags granted BY a cosmetic](Permissions.md#permissions-and-tags-granted-by-a-cosmetic). |
| **Effect-Blocked Groups** | Dev Studio → Server Config | A server-wide, comma-separated list of LuckPerms groups whose players get **no cosmetic effects at all** — particles, potion effects, flight, speed, Lure, scanners, granted permissions/tags. The cosmetic model still renders; only the *gameplay effects* are suppressed. Handy for a "cosmetics-only, no gameplay advantage" rank. Empty by default (nobody blocked). |
| **Slot / type limits, command nodes** | Everywhere | Tiered nodes like `gc.slot.<slot>.<N>` or `gc.command.wardrobe.self`. See [Permissions](Permissions.md). |

!!! note "Minecraft Tags don't need LuckPerms"
    A cosmetic's **Minecraft Tags** field (vanilla scoreboard `/tag`) is completely independent of LuckPerms — it works on any Fabric server. Only **Granted Permissions** (real permission nodes) needs a permissions plugin behind it.

---

## **Without LuckPerms**

* Only real server operators (`ops.json`) pass any permission check — the Fabric permissions API falls back to op-only.
* The **Tags** tab and the Dev Studio **Chat Tags** page are hidden entirely.
* A cosmetic's **Granted Permissions** field still saves but never applies (no permission plugin to hand nodes to). Its **Minecraft Tags** field keeps working regardless (see note above).
* **Effect-Blocked Groups** has nothing to check membership against, so it's effectively a no-op.
* Slot/type/command permission checks still work (any Fabric permissions API backend other than LuckPerms would also work here) — LuckPerms is simply the one most servers already run.
