# **Armazenamento (Banco de Dados)**

---

O GreatCosmetics guarda os dados **por jogador** num banco relacional: cosméticos desbloqueados/equipados, configurações de visibilidade, cosméticos escondidos, **conteúdo das mochilas**, Skins de Pokémon desbloqueadas e seus cooldowns, e Tags possuídas/equipadas.

Os arquivos de config (`cosmeticsconfig.conf`, `tags.json`, …) são o *catálogo* — eles **não** ficam no banco.

---

## **Escolhendo o backend**

Defina no [`mainconfig.conf`](Main Config.md):

```json
"useMySQL": false
```

### **SQLite (padrão)**

`useMySQL: false` — um único arquivo local em:

```
config/GreatCosmetics/database.db
```

Zero setup, perfeito pra um servidor único. Faça backup copiando o arquivo (servidor parado).

### **MySQL**

`useMySQL: true` — conecta num servidor MySQL externo usando:

```json
"mysqlHost": "localhost",
"mysqlPort": 3306,
"mysqlDatabase": "greatcosmetics",
"mysqlUser": "root",
"mysqlPassword": "password"
```

Use MySQL quando quiser que vários servidores (lobby + jogos) compartilhem os mesmos dados de guarda-roupa, ou quando o seu host gerencia backups centralmente. Crie o banco (`CREATE DATABASE greatcosmetics;`) e um usuário com permissão total nele antes de iniciar — o mod cria as próprias tabelas.

!!! warning "Fallback automático"
    Se a conexão com o MySQL falhar no startup, o mod loga um aviso e **cai pro SQLite local** pra o servidor ainda subir. Cheque o `latest.log` se os dados dos jogadores parecerem vazios depois de mudar pro MySQL.

---

## **Tabelas**

Criadas automaticamente. Normalmente você nunca mexe nelas direto.

| Tabela | Conteúdo |
| :--- | :--- |
| `player_unlocked_cosmetics` | Quais cosméticos cada jogador possui |
| `player_equipped_cosmetics` | Cosméticos usados no momento (por slot / tipo) |
| `player_cosmetic_settings` | Toggles de esconder capacete / peitoral / calça / botas |
| `player_hidden_cosmetics` | Cosméticos escondidos individualmente |
| `player_backpacks` | NBT em Base64 de cada página de mochila |
| `player_unlocked_skins` / `player_skin_cooldowns` | Posse e timestamps de cooldown das Skins de Pokémon |
| `player_tags` | Tags possuídas e a equipada |

---

## **Migrando SQLite → MySQL**

O mod não tem transferência embutida. Pra mover os dados existentes, exporte as tabelas do SQLite e importe no MySQL com uma ferramenta tipo **DBeaver**, mantendo os mesmos nomes de tabela e coluna. Se você está começando do zero, só troque `useMySQL` e `/gc reload` (ou reinicie).
