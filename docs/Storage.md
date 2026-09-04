# **Storage (Database)**

---

GreatCosmetics stores **per-player** data in a relational database: unlocked/equipped cosmetics, visibility settings, hidden cosmetics, **backpack contents**, unlocked Pokémon Skins and their cooldowns, and owned/equipped Tags.

Config files (`cosmeticsconfig.conf`, `tags.json`, …) are the *catalog* — they are **not** in the database.

---

## **Choosing the backend**

Set it in [`mainconfig.conf`](Main Config.md):

```json
"useMySQL": false
```

### **SQLite (default)**

`useMySQL: false` — a single local file at:

```
config/GreatCosmetics/database.db
```

Zero setup, perfect for a single server. Back it up by copying the file (server stopped).

### **MySQL**

`useMySQL: true` — connects to an external MySQL server using:

```json
"mysqlHost": "localhost",
"mysqlPort": 3306,
"mysqlDatabase": "greatcosmetics",
"mysqlUser": "root",
"mysqlPassword": "password"
```

Use MySQL when you want several servers (lobby + games) to share the same wardrobe data, or when your host manages backups centrally. Create the database (`CREATE DATABASE greatcosmetics;`) and a user with full rights on it before starting — the mod creates its own tables.

!!! warning "Automatic fallback"
    If the MySQL connection fails at startup, the mod logs a warning and **falls back to local SQLite** so the server still boots. Check `latest.log` if player data looks empty after switching to MySQL.

---

## **Tables**

Created automatically. You normally never touch these directly.

| Table | Contents |
| :--- | :--- |
| `player_unlocked_cosmetics` | Which cosmetics each player owns |
| `player_equipped_cosmetics` | Currently worn cosmetics (per slot / type) |
| `player_cosmetic_settings` | Hide-helmet / chestplate / leggings / boots toggles |
| `player_hidden_cosmetics` | Individually hidden cosmetics |
| `player_backpacks` | Base64 NBT of each backpack page |
| `player_unlocked_skins` / `player_skin_cooldowns` | Pokémon Skins ownership and cooldown timestamps |
| `player_tags` | Owned Tags and the equipped one |

---

## **Migrating SQLite → MySQL**

The mod has no built-in transfer. To move existing data, export the SQLite tables and import them into MySQL with a tool like **DBeaver**, keeping the same table and column names. If you're starting fresh, just switch `useMySQL` and `/gc reload` (or restart).
