# **Dependências**

---

O lançamento atual do GreatCosmetics roda em **Fabric** no Minecraft `1.21.1` (Java `21+`). Um build de NeoForge está em testes.

## **Obrigatórias — Fabric**

| Dependência | Observações |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.16` | Carregador de mods. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` ou mais novo | Hooks base do build Fabric. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) `1.13.13+kotlin.2.4.10` ou mais novo | Runtime do Kotlin — exigido pelo Cobblemon. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) `>= 13.0` (Fabric) | Hooks cross-loader que o GreatCosmetics usa. Normalmente o Cobblemon já instala. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` (Fabric) | A aba Party, as Skins de Pokémon e o sistema de Lure leem dados do Cobblemon. |

## **Obrigatórias — NeoForge** *(em testes, ainda não lançado)*

| Dependência | Observações |
| :--- | :--- |
| [**NeoForge**](https://neoforged.net/) `21.1.133` ou mais novo | Carregador de mods. |
| [**Kotlin for Forge**](https://modrinth.com/mod/kotlin-for-forge) `5.7.0` ou mais novo | Runtime do Kotlin — exigido pelo Cobblemon. |
| [**Architectury API**](https://modrinth.com/mod/architectury-api) `>= 13.0` (NeoForge) | Hooks cross-loader que o GreatCosmetics usa. Normalmente o Cobblemon já instala. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.8.0` (NeoForge) | As mesmas features do Fabric. |

!!! note "Bibliotecas embutidas"
    O **GeckoLib** (renderizador dos modelos 3D animados), a biblioteca de texto **adventure / MiniMessage** e os drivers JDBC de SQLite / MySQL vêm *dentro* do jar do GreatCosmetics nos dois loaders. Você nunca os adiciona manualmente.

---

## **Opcionais**

| Dependência | O que habilita |
| :--- | :--- |
| [**LuckPerms**](https://luckperms.net/) | Os nodes de permissão (limites por slot / tipo, permissões por cosmético, permissões de comando) **e** as Tags de chat automáticas por grupo. Sem ele, só operadores usam recursos restritos e as Tags de grupo ficam só visuais. |
| **Servidor MySQL** | Banco de dados externo opcional no lugar do SQLite local embutido. Ver [Armazenamento](Storage.md). |
| Um host de resource pack (Dropbox / GitHub / seu próprio servidor web) | Necessário só se você usar o recurso de **Resource Pack Forçado**. Ver [Resource Pack](Resource Pack.md). |

---

!!! info "Precisa de outra integração?"
    Se o seu servidor usa um sistema de permissão ou chat que ainda não suportamos, abra um ticket no nosso [Discord](https://discord.gg/YgM4Ng4QGu) — a gente avalia e prioriza integrações pedidas.
