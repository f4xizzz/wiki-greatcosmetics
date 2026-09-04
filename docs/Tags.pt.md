# **Tags**

---

**Tags** são prefixos de chat selecionáveis. O jogador escolhe uma na aba **Tags** do guarda-roupa; o mod aplica através do **LuckPerms**.

Arquivo de catálogo: **`config/GreatCosmetics/tags.json`**. Exige o **LuckPerms** pra de fato mudar o prefixo do chat — sem ele, as Tags são só prévia.

---

## **Dois tipos de Tag**

### Tags Personalizadas

Criadas pela staff no editor de Tags (ou na mão no `tags.json`). Um jogador **possui** uma Tag personalizada se tiver **qualquer** node da lista `permissions` dela, ou recebeu via `/gc tags give`.

### Tags de Grupo

Importadas **automaticamente** dos seus grupos do LuckPerms no startup e no `/gc reload`:

* `displayName`, `weight` e `tag` (prefixo) são lidos do grupo.
* Um jogador possui a Tag só por estar **naquele grupo**.
* Elas **nunca são deletáveis** e não podem ser distribuídas com `/gc tags give`.
* Grupos listados no `tagGroupBlacklist` (no `mainconfig.conf`, `default` por padrão) são pulados.

No join o mod auto-equipa a Tag de grupo de maior weight do jogador se ele não tiver outra Tag equipada.

---

## **Campos da Tag**

| Campo | Significado |
| :--- | :--- |
| **id** | Identificador único (também o nome do grupo do LuckPerms pras Tags de grupo). |
| **displayName** | Nome MiniMessage mostrado no menu de Tags e no tooltip. |
| **description** | Linha MiniMessage opcional mostrada sob o nome no hover. |
| **tag** | O prefixo de chat de verdade (MiniMessage), ex: `<gradient:#f00:#00f>[VIP]</gradient> `. Aplicado como um prefix node do LuckPerms (weight 1000) enquanto equipado. |
| **permissions** | Nodes **concedidos ao jogador** enquanto essa Tag está equipada, e os nodes que marcam a posse de uma Tag personalizada. |
| **minecraftTag** | Command tag `/tag` opcional adicionado ao jogador enquanto equipado — útil pra datapacks / scoreboards. |
| **isGroupTag** / **weight** | Definidos automaticamente pras Tags de grupo. |

---

## **Editor**

Aba Tags → toggle **DEV** (precisa de `gc.dev` ou OP) → **+ Create New Tag**, ou o lápis ✏ no hover pra editar. Campos: ID, Display Name, Description, TAG (prefixo), Permissions (separadas por vírgula), Minecraft Tag. **Save** grava no `tags.json` e transmite; **DELETE TAG** remove uma Tag personalizada.

---

## **Regras de equipar**

* Clicar numa Tag que você possui equipa ela e remove a anterior.
* Você sempre pode **trocar** de Tag mas nunca fica com **nenhuma** — tentar remover a Tag de grupo do seu cargo atual mantém ela (você recebe uma mensagem de "não pode remover a tag do seu cargo"). Remover qualquer outra Tag cai pra sua melhor Tag de grupo, ou pra nada só se você não pertence a nenhum grupo com tag.

---

## **Comandos**

| Comando | Efeito |
| :--- | :--- |
| `/gc tags give <tag_id> <jogador>` | Concede uma Tag **personalizada** (cria uma linha de posse em `player_tags`). |
| `/gc tags remove <tag_id> <jogador>` | Revoga uma Tag personalizada concedida (também desequipa se estiver usando). |

Tags de grupo não podem ser dadas ou removidas por comando — gerencie a associação ao grupo do LuckPerms.

---

## **Exemplo de entrada no `tags.json`**

```json
{
  "vip": {
    "displayName": "<gold>VIP",
    "description": "<gray>Disponível pra membros VIP.",
    "tag": "<gold>[VIP] ",
    "permissions": ["greatcosmetics.tag.vip"],
    "minecraftTag": "gc_tag_vip"
  }
}
```
