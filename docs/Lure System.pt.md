# **Sistema de Lure**

---

O sistema **Lure** deixa um cosmético dar bônus de gameplay do **Cobblemon**: melhores chances de shiny, IVs garantidos, chance de captura, hidden abilities, EXP, amizade e bônus de pesca.

Configure na seção **`>> Configure LURE`** do editor de cosmético do [Dev Studio](Dev Studio.md). Só faz algo com o **Cobblemon** instalado.

---

## **Como os números funcionam**

* **`enabled`** precisa estar ligado pra qualquer bônus valer.
* Os bônus de **todo** cosmético de Lure equipado são **somados** (diferente dos efeitos de velocidade/poção, que pegam o maior).
* Campos de "chance" são probabilidades `0.0`–`1.0` (`0.25` = 25%). Campos de "multiplier" multiplicam a quantidade base.
* Os rolls de shiny e IV acontecem **na captura**, não no spawn (uma decisão de design deliberada) — então o jogador tem que de fato capturar o Pokémon.

---

## **Campos**

| Campo | Tipo | Efeito | Quando |
| :--- | :--- | :--- | :--- |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance de re-rolar uma captura não-shiny pra shiny | Na captura |
| **Lure IV** (`lureIV`) | contagem | Número de IVs forçados a 31 na captura | Na captura |
| **IV Chance** (`lureChanceIV`) | chance | Chance de aplicar os IVs garantidos | Na captura |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance de dar ao Pokémon capturado a hidden ability | Na captura |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance de subir um spawn pro bucket "ultra raro" | No spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance de transformar uma captura **falha** em sucesso | No arremesso da ball |
| **EXP Multiplier** (`lureEXP`) + **Exp All Multiplier** (`lureExpAllMultiplier`) | multiplier | Experiência extra ganha pelos Pokémon do dono (os dois valores somam) | No ganho de EXP |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Amizade extra ganha | Na atualização de amizade |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Chance de shiny extra, só na pesca (soma com o Shiny Multiplier) | Ao pescar um Pokémon |
| **Fishing IV** (`lurePescaIv`) + **Fishing IV Chance** (`lurePescaIvChance`) | contagem + chance | IVs garantidos extras, só na pesca | Ao pescar um Pokémon |
| **Fishing Speed** (`lurePescaVelocidade`) | valor | Adiciona níveis do encantamento "Lure" do Cobblemon à vara pra fisgadas mais rápidas | Ao lançar a vara |

---

## **Ainda não implementado**

Estes campos existem no editor mas atualmente **não fazem nada** — estão reservados pra mecânicas futuras:

* **Affected Type** (`lureTYPE`)
* **Fishing Ultra Rare** (`lurePescaUltraRare`)
* **Fishing Lure** (`lureDePesca`)
* **EV Multiplier** (`lureEV`) — o ganho de EV é decidido dentro da lógica de batalha do Cobblemon, que não expõe um hook.

---

## **Exemplo: um chapéu "Shiny Charm"**

```json
"lure": {
  "enabled": true,
  "lureShinyMultiplier": 0.05,
  "lureChanceIV": 0.5,
  "lureIV": 3
}
```

Usar isso dá +5% de chance de shiny numa captura e 50% de chance de 3 IVs perfeitos. O tooltip do guarda-roupa lista todos os bônus ativos automaticamente.
