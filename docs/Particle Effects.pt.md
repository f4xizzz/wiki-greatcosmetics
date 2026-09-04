# **Efeitos de Partícula**

---

Um **efeito de partícula** é um emissor de partículas nomeado e reutilizável que você anexa a cosméticos (como rastro, ou rastro só de voo). Definido na página **Effects** do [Dev Studio](Dev Studio.md) e guardado em **`config/greatcosmetics/effects.json`**.

---

## **Campos do efeito**

```json
{
  "sparkle_trail": {
    "particleId": "minecraft:end_rod",
    "count": 3,
    "tickInterval": 5,
    "speed": 0.0,
    "spreadX": 0.2,
    "spreadY": 0.4,
    "spreadZ": 0.2,
    "offsetX": 0.0,
    "offsetY": 1.0,
    "offsetZ": 0.0
  }
}
```

| Campo | Significado |
| :--- | :--- |
| **particleId** | Qualquer id de partícula do Minecraft (`minecraft:flame`, `minecraft:soul_fire_flame`, `minecraft:end_rod`…). |
| **count** | Partículas geradas por rajada. |
| **tickInterval** | Ticks entre rajadas (`20` = uma/segundo, `5` = 4×/segundo). |
| **speed** | Velocidade da partícula — `0` = elas ficam paradas, maior = elas disparam pra fora. |
| **spreadX / Y / Z** | Caixa de espalhamento aleatório ao redor do ponto de spawn. |
| **offsetX / Y / Z** | Posição relativa ao jogador — `Y: 1.0` é mais ou menos a altura do peito. `X` é pros lados, `Z` é frente/trás. |

---

## **Criando um**

Dev Studio → **Effects** → **+ New Effect**. O editor tem uma **prévia 3D ao vivo** e um **gizmo 3D**: segure `X`, `Y` ou `Z` e arraste fora do painel pra mover o offset visualmente. **S** salva.

O campo Particle ID tem autocomplete pra toda partícula registrada (vanilla + mods).

---

## **Anexando a um cosmético**

No editor de cosmético, seção **Special Effects**:

* **Effect Visual** — lista separada por vírgula de **ids** de efeito; toca sempre enquanto o cosmético está sendo usado.
* **Fly Particle** — igual, mas só enquanto o jogador está voando.

Um efeito pode ser referenciado por qualquer quantidade de cosméticos.

---

!!! note "Sync"
    Os efeitos são transmitidos pra todos os jogadores online ao salvar. Se um jogador entrou antes do efeito existir, o `/gc reload` (ou o próximo join dele) pega.
