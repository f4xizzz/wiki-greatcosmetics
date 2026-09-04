# **NPC Cosmetics**

---

You can equip GreatCosmetics cosmetics on **any living entity** — EasyNPC NPCs, Armor Stands, mobs — not just players. The mod renders the cosmetic on the entity the same way it renders it on players, so custom 3D / GeckoLib parts show correctly.

Runtime state is kept in **`config/greatcosmetics/npc_cosmetics.json`** (keyed by entity UUID) and re-synced to players on join and `/gc reload`.

---

## **Equipping**

1. Stand within **5 blocks** and look directly at the entity.
2. Run:

    `/gc npc equip <cosmetic_id>`

The cosmetic is registered against that entity's UUID and appears for everyone.

!!! note "Why not `/data` or the armor slot?"
    The cosmetic system never reads the entity's real equipment slot — it renders purely from its own registry. Putting the item in the armor slot would show a broken/flat item (or nothing on an NPC whose renderer ignores that slot). Always use `/gc npc equip`.

---

## **Removing**

Look at the entity and run:

`/gc npc remove <slot>`

`<slot>` is one of `head, face, neck, chest, back, waist, legs, feet, hand`. This clears every cosmetic in that virtual slot on the target.

---

## **Getting an entity's UUID**

`/gc uuid` — look at an entity within 5 blocks and run it. The UUID is printed with a **click-to-copy** link, for use in other configs or datapacks.

---

## **Permissions**

| Node | Command |
| :--- | :--- |
| `gc.command.npc.equip` | `/gc npc equip` |
| `gc.command.npc.remove` | `/gc npc remove` |
| `gc.command.uuid` | `/gc uuid` |
