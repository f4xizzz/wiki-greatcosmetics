# **Slots & Types**

---

GreatCosmetics limits how many cosmetics a player can wear with **two independent systems**: **virtual slots** (by body area) and **accessory types** (by category). Both are defined in [`mainconfig.conf`](Main Config.md) and editable in the [Dev Studio](Dev Studio.md).

---

## **Virtual slots**

Nine fixed names, independent from real armor:

`HEAD · FACE · NECK · CHEST · BACK · WAIST · LEGS · FEET · HAND`

Each has:

```json
"HEAD": { "defaultLimit": 1, "permission": "gc.slot.head" }
```

* **`defaultLimit`** — cosmetics a normal player may wear in that slot.
* **`permission`** — the **base node** for the tier system.

### Raising a slot limit

| Node | Effect |
| :--- | :--- |
| `gc.slot.head.3` | Sets the HEAD limit to **3** (the mod picks the **highest** tier 1–20 the player holds). |
| `gc.slot.head.bypass` | Unlimited (99) in HEAD. |
| `gc.extraslot.head.2` | **+2** on top of the normal limit (the highest single `extraslot.head.N` the player holds). |
| `gc.extraslot.all.4` | **+4** to **every** slot (added on top of the slot-specific extra). |

`gc.slot.*` **replaces** the limit with the tier value; `gc.extraslot.*` **adds** to it. They stack: base `1` + `gc.slot.head.3` → `3`, then + `gc.extraslot.all.2` → `5`.

---

## **Accessory types**

A **type** is a free-text category you assign to a cosmetic (its **Type** field). It caps how many cosmetics *of that category* a player wears, regardless of slot.

```json
"necklace": { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.necklace" }
```

* **`slot`** — informational (which body area this type belongs to).
* **`limitPerPlayer`** — max cosmetics with this exact type worn at once.
* **`permission`** — base node for tiers.

### Raising a type limit

| Node | Effect |
| :--- | :--- |
| `gc.type.necklace.2` | Raises the necklace limit to **2**. |
| `gc.type.necklace.bypass` | Unlimited (99) for necklaces. |

A cosmetic with type `default` has **no** type limit — only its slot limit applies.

---

## **How a check runs when a player equips**

1. Is the player **owner** (or has the `permission` node, or Dev Mode)? If not → blocked.
2. **Slot count** for the target slot vs. the resolved slot limit (`defaultLimit` → `gc.slot` tier → `+ extraslot`).
3. **Type count** for the cosmetic's type vs. the resolved type limit.

If any check fails, the player gets a message and a sound; nothing is equipped.

Operators and Dev Mode bypass all slot/type limits. `/gc cosmetics equip` also force-equips ignoring limits.

---

## **Example: a "3 hats for VIP" setup**

`mainconfig.conf`:

```json
"HEAD": { "defaultLimit": 1, "permission": "gc.slot.head" }
```

LuckPerms:

```
lp group vip permission set gc.slot.head.3 true
```

Now VIPs wear up to 3 HEAD cosmetics; everyone else wears 1.
