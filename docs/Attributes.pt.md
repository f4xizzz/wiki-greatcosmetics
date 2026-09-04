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
