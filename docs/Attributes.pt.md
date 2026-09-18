# **Atributos & Habilidades**

---

Qualquer cosmético pode dar efeitos de gameplay reais enquanto equipado. Configure na seção **Status & Combat** e **Special Effects** do editor de cosmético do [Dev Studio](Dev Studio.md).

---

## **Status & Combate**

| Campo | Efeito |
| :--- | :--- |
| **Armor Points** (`armor`) | Adiciona pontos de armadura (como usar armadura). Mostrado no tooltip como 🛡. |
| **Toughness** (`toughness`) | Adiciona resistência de armadura. Mostrado como ❈. |
| **Max Durability** (`maxDurability`) | Se > 0, o item físico mostra uma barra de durabilidade. **Só cosmético** — nunca quebra de verdade. |

---

## **Voo**

| Campo | Efeito |
| :--- | :--- |
| **Allows Flight?** (`EnableFly`) | Concede voo estilo criativo enquanto equipado. Removido de forma limpa ao desequipar (a menos que o jogador esteja no Criativo/Espectador). |
| **Fly Speed** (`flySpeedMultiplier`, padrão 1.0) | Multiplica a velocidade de voo. `2.0` = duas vezes mais rápido. |

O jogador vê uma mensagem de action-bar `✈ Voo ativado/desativado` (texto configurável em `lang/messages.json`).

---

## **Velocidade de movimento**

| Campo | Efeito |
| :--- | :--- |
| **Ground Speed** (`groundSpeedMultiplier`, padrão 1.0) | Multiplicador de velocidade de andar/correr no chão. |
| **Swim Speed** (`swimSpeedMultiplier`, padrão 1.0) | Multiplicador de velocidade de nado na água. |

Se um jogador usa vários cosméticos com bônus de velocidade, só o **maior** multiplicador se aplica (eles não somam nem multiplicam). A mesma regra de "o maior vence" vale pros efeitos de poção passivos.

---

## **Auto-Feed**

**Auto-Feed** (`AutoFeed`) — mantém a fome do jogador cheia enquanto o cosmético está sendo usado.

---

## **Efeitos de poção passivos**

**Special Effects → Select Effects** abre uma grade com todo status effect do Minecraft. Clique num pra ciclar o nível (`OFF → I → II → III → IV → V`). Os efeitos de todo cosmético equipado são reaplicados continuamente como efeitos permanentes e escondidos (sem partículas, sem spam de ícone na HUD).

Guardados como strings `namespace:effect:level` (ex: `minecraft:water_breathing:1`).

!!! note "Convenção de nível"
    Nível `1` no editor = amplificador `0` (Efeito I). Nível `2` = Efeito II, etc.

---

## **Rastros de partícula visuais**

Duas listas separadas por vírgula em **Special Effects**. Cada entrada é o **id de um [Efeito de Partícula](Particle Effects.md)** que você definiu na página Effects do Dev Studio (não um nome de partícula do Minecraft cru):

| Campo | Quando toca |
| :--- | :--- |
| **Effect Visual** (`effectVisual`) | Sempre, enquanto o cosmético está equipado. |
| **Fly Particle** (`flyParticle`) | Só enquanto o jogador está voando. |

Então o fluxo é: crie o efeito de partícula uma vez (tipo de partícula, count, spread, interval, offset), depois referencie o id dele aqui. Um efeito pode ser reusado por muitos cosméticos.

---

## **Bônus de Lure do Cobblemon**

Um sistema separado e grande: taxa de shiny, IVs garantidos, ganho de EV, chance de captura, hidden ability, bônus de pesca e mais. Ver [Sistema de Lure](Lure System.md).

---

## **Special Effects (habilidades ativas)**

Um cosmético também pode conceder uma *habilidade ativa*, editável na seção **Special Effects** do Dev Studio (ou, pras quatro marcadas **Cobblemon**, dentro do popup **Cobblemon Effects** — ver [Cobblemon Effects](Lure System.pt.md) — só aparecem num servidor rodando Cobblemon). Ver [Integração com Cobblemon](Cobblemon Integration.pt.md) pra entender como as que dependem do Cobblemon funcionam por baixo dos panos.

Cada habilidade também pode ser acionada pela roda de **Ações Rápidas** (tecla padrão `V`, ver [O Wardrobe](The Wardrobe.pt.md#menu-de-acoes-rapidas)) em vez de segurar Shift.

| Habilidade | Gatilho | Efeito |
| :--- | :--- | :--- |
| **Heal Ability** *(Cobblemon)* | Segurar Shift por {cooldown}s, ou clicar **Heal Party Now** nas Ações Rápidas | Cura a party Cobblemon inteira (HP, status, PP) — igual uma máquina de cura. Não funciona em batalha. Cooldown por cosmético; vestir vários usa o menor. |
| **Shiny & HA Radar** *(Cobblemon)* | Passivo, sempre ativo enquanto equipado | Avisa o jogador (som em loop + distância na actionbar) quando um Pokémon selvagem **shiny** OU com **Hidden Ability** entra num alcance configurável. Fica quieto de novo quando ele sai do alcance. |
| **Vein Miner** | Segurar Shift ao quebrar um bloco elegível | Quebra o "veio" conectado inteiro daquele mesmo bloco/tag de uma vez (com teto de segurança). Itens vão direto pro inventário. A lista de blocos/tags é **obrigatória** — vazio desativa (sem padrão "mina qualquer coisa"). |
| **Tree Capitator** | Segurar Shift ao quebrar um log | Derruba a árvore conectada inteira (qualquer madeira, vanilla ou de mod, via `#minecraft:logs`), mesmo comportamento de inventário do Vein Miner. |
| **Pollinator** | Clicar **Pollinate Now** nas Ações Rápidas (ou segurar Shift 15s) | Aplica bone meal em toda planta fertilizável (plantações, mudas, etc) num raio esférico, usando a MESMA chance aleatória de crescer do bone meal real — não é um crescimento instantâneo garantido. Raio, "usos" de bone meal por planta e cooldown configuráveis. |
| **Auto Harvest** | Passivo, num timer | Colhe automaticamente toda plantação totalmente madura no raio. Não replanta — combine com Auto Planting. |
| **Auto Planting** | Passivo, num timer | Planta sementes em farmland vazio no raio. Prioridade de semente: mão direita → mão esquerda → hotbar slot 1-9. Não colhe. |
| **Auto Watering** | Passivo, num timer | Uma versão mais suave e contínua do Pollinator — 1 "uso" de bone meal por planta fertilizável no raio a cada intervalo. |
| **Item Giver** | Passivo, num timer | Dá um item + quantidade configurados direto pro inventário (dropa no chão se cheio). |
| **Combat Sounds** | Passivo, ao acertar/ser acertado | Toca um som quando o jogador leva dano e/ou causa dano. Configurado na seção **Sounds** do cosmético — ver [Sons](Sounds.pt.md#combat-sounds). |

Vein Miner, Tree Capitator, Auto Harvest, Auto Planting, Auto Watering, Item Giver e Combat Sounds são **mecânicas 100% vanilla** — funcionam identicamente com ou sem Cobblemon instalado.

!!! tip "Ligar/desligar Vein Miner e Tree Capitator sem desequipar"
    Como esses dois ficam sempre ativos enquanto equipados, a roda de Ações Rápidas dá um círculo on/off pra cada um (verde = ligado, vermelho = desligado) — uma preferência de sessão que não mexe na config do cosmético e reseta no logout.

### **Scanners** *(Cobblemon)*

Também configurados no popup **Cobblemon Effects** (ver [Cobblemon Effects](Lure System.pt.md), que cobre os bônus de Lure ao lado dos quais eles ficam). Enquanto equipado, cada scanner acrescenta informação acima (ou ao lado) do nome de todo Pokémon próximo — calculado no servidor, já que dados de IV/nature/ability de Pokémon selvagem normalmente não chegam no cliente.

| Scanner | Mostra |
| :--- | :--- |
| **IVs Scanner** | O IV de cada stat (HP/Atk/Def/SpA/SpD/Spe), colorido, acima do nome. |
| **Nature Scanner** | A nature do Pokémon, logo abaixo da linha de IVs. |
| **Ability Scanner** | A habilidade do Pokémon, em vermelho, à direita do nome. |
| **Size Scanner** | A categoria de tamanho (XS-XL), em amarelo negrito, à esquerda do nome. |
| **Dex Scanner** | Todo Pokémon selvagem mirado (cruz de mira) a 5+ blocos de distância é registrado automaticamente como visto na Pokédex — sem precisar de item. |

### **Permissões Concedidas & Minecraft Tags** *(LuckPerms)*

Além do único gate `permission` (quem pode sequer usar o cosmético), um cosmético pode **conceder** coisas enquanto equipado:

* **Granted Permissions** — uma lista separada por vírgula de nodes de permissão do LuckPerms aplicados como *transient* (só na sessão, nunca gravados na storage do LuckPerms) enquanto o cosmético está equipado e o gate dele passa. Removidos no instante em que é desequipado.
* **Minecraft Tags** — uma lista separada por vírgula de scoreboard tags vanilla (`/tag`) adicionadas do mesmo jeito, pra usar em `/execute if entity @s[tag=...]` ou datapacks.

Ver [Integração com LuckPerms](LuckPerms Integration.pt.md) pro panorama completo, incluindo o interruptor "bloquear efeitos pra esse grupo" que vale pro servidor inteiro.
