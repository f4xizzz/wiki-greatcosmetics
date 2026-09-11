# **Comandos**

---

O mod registra duas raízes: **`/greatcosmetics`** (alias **`/gc`**) e o comando separado **`/wardrobe`**.

Cada subcomando tem o **seu próprio node de permissão** — ver [Permissões](Permissions.md). Operadores de verdade (OP no `ops.json`) sempre passam. Os nodes só funcionam com **LuckPerms** (ou outro provedor de permissões do Fabric) instalado.

---

## **Comandos de Jogador**

| Comando | Descrição | Permissão |
| :--- | :--- | :--- |
| `/wardrobe` | Abre o Avatar Studio 3D pra você mesmo. | `gc.command.wardrobe.self` |
| `/backpack` *(tecla `B`)* | Abre sua mochila cosmética equipada (ou um seletor se você usa várias). | — |

---

## **Comandos de Staff**

| Comando | Descrição | Permissão |
| :--- | :--- | :--- |
| `/wardrobe <jogador>` | Abre o guarda-roupa pra outro jogador. | `gc.command.wardrobe.other` |
| `/wardrobe <jogador> <background>` | Abre e teleporta o jogador pra um cenário de estúdio salvo. | `gc.command.wardrobe.other` |
| `/gc give <cosmetic_id> [jogador]` | Desbloqueia um cosmético no guarda-roupa do alvo. | `gc.command.give` |
| `/gc giveitem <cosmetic_id> [jogador]` | Dá a versão **item físico** do cosmético. | `gc.command.giveitem` |
| `/gc remove <cosmetic_id> [jogador]` | Remove um cosmético do guarda-roupa do alvo. | `gc.command.remove` |
| `/gc cosmetics equip <cosmetic_id> <jogador>` | Força equipar um cosmético num jogador, ignorando limites de slot/tipo. | `gc.command.cosmetics.equip` |
| `/gc cosmetics unequip <cosmetic_id> <jogador>` | Força desequipar um cosmético de um jogador. | `gc.command.cosmetics.unequip` |
| `/gc extraslot <jogador> <slot\|ALL> add\|set\|remove <quantidade>` | Concede (ou define, ou remove) um bônus **aditivo** por jogador no limite de um slot virtual — guardado no banco de dados, separado dos nodes de permissão `gc.extraslot.*` e que se acumula com eles. Use `ALL` pra afetar todo slot de uma vez. | `gc.command.extraslot` |
| `/gc extratypeslot <jogador> <tipo\|ALL> add\|set\|remove <quantidade>` | Igual ao `/gc extraslot`, mas pra **tipos de acessório** em vez de slots virtuais. | `gc.command.extratypeslot` |
| `/gc giveskin <skin_id> [jogador]` | Desbloqueia uma Skin de Pokémon pro alvo. | `gc.command.giveskin` |
| `/gc removeskin <skin_id> [jogador]` | Remove uma Skin de Pokémon do alvo. | `gc.command.removeskin` |
| `/gc tags give <tag_id> <jogador>` | Concede a posse de uma Tag de chat (só tags personalizadas). | `gc.command.tags.give` |
| `/gc tags remove <tag_id> <jogador>` | Remove uma Tag concedida. | `gc.command.tags.remove` |
| `/gc npc equip <cosmetic_id>` | Equipa um cosmético no NPC / Armor Stand que você está olhando. | `gc.command.npc.equip` |
| `/gc npc remove <slot>` | Limpa um slot virtual na entidade que você está olhando. | `gc.command.npc.remove` |
| `/gc display <cosmetic_id>` | Cria um armor stand invisível e travado na sua posição "usando" o cosmético — só a model 3D dele aparece, como um corpo invisível vestindo a peça. Sobrevive a restart. | `gc.command.display` |
| `/gc display remove` | Apaga o display que você está olhando (máx 5 blocos). | `gc.command.display` |
| `/gc display clear` | Apaga todo `/gc display` nos chunks carregados de todos os mundos. | `gc.command.display` |
| `/gc uuid` | Copia o UUID da entidade que você está olhando (pra configs de NPC). | `gc.command.uuid` |
| `/gc wardrobe setbackground <nome>` | Salva sua posição atual como um cenário de estúdio nomeado. | `gc.command.wardrobe.setbackground` |

---

## **Comandos de Admin / Dono**

| Comando | Descrição | Permissão |
| :--- | :--- | :--- |
| `/gc reload` | Recarrega todas as configs, re-sincroniza o catálogo e reenvia o resource pack. | `gc.command.reload` |
| `/gc debug` | Liga/desliga o log de debug detalhado no console do servidor (e encaminha o debug do client). | `gc.command.debug` |
| `/gc activation <chave>` | Valida e ativa a licença do mod pro IP deste servidor. **Nunca é bloqueado pelo gate de licença.** | `gc.command.activation` |

---

## **Teclas**

Configuráveis em **Opções → Controles → GreatCosmetics**:

| Tecla padrão | Ação |
| :--- | :--- |
| `B` | Abre sua mochila cosmética. |
| `U` | Alterna a UI do servidor (`/ui on` / `/ui off`) — só útil se o seu servidor tiver esse comando. |
| `Y` | Roda `/warps` — depende do servidor. |
| `P` | Roda `/pc` — abre o PC do Cobblemon. |

!!! note "Servidor sem licença"
    Num servidor dedicado **sem licença válida**, todo comando `/gc` e `/wardrobe` é bloqueado, exceto `/gc activation`. Os jogadores veem uma mensagem de "sem licença válida". O singleplayer nunca é afetado.
