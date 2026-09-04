# **Dependências**

---

## **Obrigatórias**

| Dependência | Observações |
| :--- | :--- |
| [**Fabric Loader**](https://fabricmc.net/use/) `>= 0.18.3` | Carregador de mods. |
| [**Fabric API**](https://modrinth.com/mod/fabric-api) `0.116.9+1.21.1` ou mais novo | Hooks base do mod. |
| [**Fabric Language Kotlin**](https://modrinth.com/mod/fabric-language-kotlin) `1.13.13+kotlin.2.4.10` ou mais novo | Exigido pelo Cobblemon e pelo GreatCosmetics. |
| [**Cobblemon**](https://modrinth.com/mod/cobblemon) `1.7.3` | A aba Party, as Skins de Pokémon e o sistema de Lure leem dados do Cobblemon. |
| **GeckoLib** (Fabric, 1.21.1) | Renderiza os modelos 3D animados dos cosméticos. **Já vem dentro do jar do mod** — você não instala separado. |
| **Minecraft** `1.21.1` · **Java** `21+` | Servidor e cliente. |

!!! note "Bibliotecas embutidas"
    GeckoLib, a biblioteca de texto **adventure / MiniMessage** e os drivers JDBC de SQLite / MySQL vêm *dentro* do jar do GreatCosmetics. Você nunca os adiciona manualmente.

---

## **Opcionais**

| Dependência | O que habilita |
| :--- | :--- |
| [**LuckPerms**](https://luckperms.net/) | Os nodes de permissão (limites por slot / tipo, permissões por cosmético, permissões de comando) **e** as Tags de chat automáticas por grupo. Sem ele, só operadores usam recursos restritos e as Tags de grupo ficam só visuais. |
| **Servidor MySQL** | Banco de dados externo opcional no lugar do SQLite local embutido. Ver [Armazenamento](Storage.md). |
| Um host de resource pack (Dropbox / GitHub / seu próprio servidor web) | Necessário só se você usar o recurso de **Resource Pack Forçado**. Ver [Resource Pack](Resource Pack.md). |

---

!!! info "Precisa de outra integração?"
    Se o seu servidor usa um sistema de permissão ou chat que ainda não suportamos, abra um ticket no nosso [Discord](https://discord.gg/aDCgBbvRe5) — a gente avalia e prioriza integrações pedidas.
