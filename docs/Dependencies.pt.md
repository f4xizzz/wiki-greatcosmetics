# **Dependências**

---

O lançamento atual do GreatCosmetics roda em **Fabric** no Minecraft `1.21.1` (Java `21+`). Um build de NeoForge está em testes.

O mod precisa **só do Fabric Loader + Fabric API**. Todo o resto é opcional — Cobblemon e LuckPerms cada um *destrava recursos extras* quando presentes, mas o mod carrega, a mochila funciona e os cosméticos renderizam num servidor Fabric puro sem eles.

## **Obrigatórias — Fabric**

| Dependência | Observações |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.16` | Carregador de mods. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` ou mais novo | Hooks base do build Fabric. |

Só isso. O renderizador **GeckoLib**, a biblioteca de texto **adventure / MiniMessage** e os drivers JDBC de SQLite / MySQL vêm *dentro* do jar do GreatCosmetics — você nunca os adiciona manualmente.

## **Obrigatórias — NeoForge** *(em testes, ainda não lançado)*

| Dependência | Observações |
| :--- | :--- |
| [**NeoForge**](https://neoforged.net/) `21.1.133` ou mais novo | Carregador de mods. |

---

## **Integrações opcionais**

| Dependência | O que destrava | Sem ela |
| :--- | :--- | :--- |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` | A aba **Party**, as **Skins de Pokémon**, o sistema de bônus **Cobblemon Cosmetics / Lure** e os **scanners** de IV / natureza / habilidade / tamanho. | Esses recursos ficam escondidos. Dados de Lure/scanner já salvos num cosmético são mantidos no arquivo e ignorados. Todo o resto dos cosméticos funciona normal. |
| [**LuckPerms**](https://luckperms.net/) | Nodes de permissão (limites por slot / tipo, `permission` por cosmético, permissões concedidas, permissões de comando) **e** a aba de **Tags** de chat automáticas por grupo. | Só operadores usam recursos restritos; a aba **Tags** e a página **Chat Tags** do Dev Studio ficam escondidas. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) | — | Só é preciso *porque o Cobblemon precisa*. O GreatCosmetics em si não exige. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) | — | Só é preciso *porque o Cobblemon precisa* em alguns setups. O GreatCosmetics em si não exige. |
| **Servidor MySQL** | Banco de dados externo no lugar do SQLite local embutido. Ver [Armazenamento](Storage.md). | Usa o arquivo SQLite embutido — suficiente pra maioria dos servidores. |
| Um host de resource pack (Dropbox / GitHub / seu servidor web) | O recurso de **Resource Pack Forçado**. Ver [Resource Pack](Resource Pack.md). | Coloque o pack no seu modpack. |

!!! tip "Rodando num servidor Cobblemon"
    O caso comum. Instale o Cobblemon (que já traz Kotlin + Architectury) e o LuckPerms, jogue o GreatCosmetics e todo recurso fica disponível. Nada extra pra configurar.

!!! note "Rodando num servidor Fabric puro"
    Também suportado. Pule Cobblemon e LuckPerms totalmente — a mochila, os slots, os modelos GeckoLib, os efeitos de partícula, as mochilas de armazenamento, os cosméticos de armadura, os sons e os cosméticos de NPC funcionam. As abas específicas de Pokémon só não aparecem.

---

!!! info "Precisa de outra integração?"
    Se o seu servidor usa um sistema de permissão ou chat que ainda não suportamos, abra um ticket no nosso [Discord](https://discord.gg/YgM4Ng4QGu) — a gente avalia e prioriza integrações pedidas.
