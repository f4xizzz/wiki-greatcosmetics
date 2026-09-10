# **Efeitos de Partícula**

---

Um **efeito de partícula** é um emissor de partículas nomeado e reutilizável que você anexa a cosméticos (como rastro, ou rastro só de voo). Os efeitos são definidos na página **Effects** do [Dev Studio](Dev Studio.md) e guardados em **`config/GreatCosmetics/effects.json`**. Os **grupos de efeito** juntam vários efeitos que disparam juntos, guardados em **`config/GreatCosmetics/effect_groups.json`**.

---

## **Campos do efeito**

```json
{
  "sparkle_trail": {
    "particleId": "minecraft:end_rod",
    "shape": "SIMPLE",
    "count": 3,
    "tickInterval": 5,
    "speed": 0.0,
    "spreadX": 0.2, "spreadY": 0.4, "spreadZ": 0.2,
    "offsetX": 0.0, "offsetY": 1.0, "offsetZ": 0.0,
    "colorR": -1, "colorG": -1, "colorB": -1
  }
}
```

| Campo | Significado |
| :--- | :--- |
| **particleId** | Qualquer id de partícula do Minecraft (`minecraft:flame`, `minecraft:soul_fire_flame`, `minecraft:end_rod`…). |
| **shape** | `SIMPLE` (o emissor clássico) ou uma forma geométrica — `CIRCLE`, `HELIX`, `BEAM`, `PULSE`. Ver [Formas](#formas). |
| **count** | Partículas geradas por rajada. **Só `SIMPLE`** — as formas geram uma partícula por ponto da forma. |
| **tickInterval** | Ticks entre rajadas (`20` = uma/segundo, `5` = 4×/segundo). |
| **speed** | Velocidade da partícula — `0` = elas ficam paradas, maior = elas disparam pra fora. |
| **spreadX / Y / Z** | Caixa de espalhamento aleatório ao redor de cada ponto de spawn (jitter). |
| **offsetX / Y / Z** | Posição relativa ao jogador — `Y: 1.0` é mais ou menos a altura do peito. `X` é pros lados, `Z` é frente/trás. Gira com o corpo do jogador. |
| **colorR / G / B** | `0–255` cada, ou `-1` = sem cor custom. Ver [Cor (RGB)](#cor-rgb). |

---

## **Criando um**

Dev Studio → **Effects** → **+ New Effect**. O editor tem uma **prévia 3D ao vivo** e um **gizmo 3D**: segure `X`, `Y` ou `Z` e arraste fora do painel pra mover o offset visualmente. **S** salva e transmite pra todo jogador online.

O editor é de cima pra baixo:

1. **=== EFFECT PRESET ===** — um dropdown que preenche todos os campos de um template, aí você ajusta. Ver [Presets](#presets).
2. **=== SHAPE ===** — `SIMPLE` / `CIRCLE` / `HELIX` / `BEAM` / `PULSE`. Mudar isso troca os campos abaixo.
3. **=== CONFIGURATION ===** — id da partícula, count, tick interval.
4. **shape params** *(só quando shape ≠ SIMPLE)* — raio, pontos, strands, rotação, animação…
5. **=== COLOR ===** — o toggle **Custom Color** e os sliders R/G/B.
6. **=== 3D TOOL / OFFSETS / SPREAD ===** — posição e jitter.

---

## **Cor (RGB)**

Ligue o **Custom Color** e defina os três sliders (`0–255`).

O Minecraft só deixa **três tipos de partícula** carregar uma cor arbitrária: `minecraft:dust`, `minecraft:dust_color_transition` e `minecraft:entity_effect`. Se o Custom Color está ligado e você escolheu **qualquer outra** partícula (`flame`, `end_rod`, …), o mod renderiza como **dust colorido** em vez de ignorar a cor — o editor mostra um aviso amarelo quando isso acontece. Então "ligar cor → ter uma partícula colorida" sempre vale; escolha `minecraft:dust` explicitamente se quiser o visual de dust sem surpresa.

Desligue o **Custom Color** pras cores naturais da partícula.

---

## **Formas** {#formas}

Com **shape ≠ SIMPLE**, o efeito desenha uma figura geométrica em volta do jogador a cada `tickInterval` em vez de uma rajada solta. Campos extras aparecem:

| Campo | Formas | Significado |
| :--- | :--- | :--- |
| **radius** | todas | Tamanho da figura. |
| **points** | todas | Partículas por anel / por volta. |
| **strands** | CIRCLE, HELIX | Cópias paralelas (uma hélice dupla = `2`). |
| **phase** | todas | Ângulo inicial, graus. |
| **clockwise** | todas | Direção. |
| **rotX / rotY / rotZ** | todas | Inclina a figura inteira, graus (um anel inclinado = `rotX` ≈ 30). |
| **helixHeight / turns / reverse** | HELIX | Altura, número de voltas, direção do percurso. |
| **beamHeight / spacing / upwards** | BEAM | Altura da coluna, espaço entre partículas, pra cima ou pra baixo. |
| **endRadius / endPoints / rings / outwards** | PULSE | Tamanho final, densidade final, número de anéis, expandir ou contrair. |
| **animTicks** | todas | `0` = a figura inteira a cada `tickInterval`. `> 0` = a figura é *traçada/expandida* ao longo de `animTicks`, aí pausa por `tickInterval`, aí repete. Um `Pulse Out` com `animTicks: 40` = um anel que cresce de `radius` a `endRadius` em ~2 s. |

`count` é ignorado pelas formas (uma partícula por ponto). `speed` e `spread` ainda valem como jitter por partícula.

!!! warning "Orçamento de partículas"
    Uma forma grande pode gerar centenas de partículas por tick. O mod limita `points ≤ 200`, `strands ≤ 12`, `rings ≤ 24` e o total por spawn em ~1200, mas mantenha `points`/`strands` na moral ou vai afogar o FPS e a rede.

---

## **Presets**

O dropdown **=== EFFECT PRESET ===** carrega um template pronto no efeito atual — `Ring`, `Ring (Tilted)`, `Halo`, `Helix`, `Double Helix`, `Rising Helix`, `Beam Up`, `Beam Down`, `Pulse Out`, `Pulse In`, `Nova`, `Simple Aura`, … Escolher um sobrescreve **todos** os campos; aí você edita por cima. O campo em si fica vazio — é uma ação, não um valor.

---

## **Grupos de efeito**

Um **grupo** é 2+ efeitos que tocam juntos. Dev Studio → **Effects** → **+ New Group** (do lado de *+ New Effect*). Os grupos aparecem na lista com borda ciano e um prefixo `[G]`.

No editor de grupo:

* **Add Existing Effect** — escolhe um id de efeito que já está no catálogo.
* **Create New Effect** — cria um efeito que vive *dentro do grupo* (ele **não** aparece na lista de Effects e não está no `effects.json` — fica no JSON do grupo).
* **Group Preset** — um template combo (`Vortex`, `Smash`, `Twin Halo`) que enche o grupo com vários efeitos de uma vez.
* **Edit** num membro → abre o editor daquele efeito "em contexto de grupo": os **outros** membros também aparecem no preview. O botão **E** da barra lateral (acima do **S**) isola — só o efeito que você está editando aparece. **< Back** volta pro grupo.

Um **id de grupo é usado exatamente onde um id de efeito é usado** (os campos *Effect Visual* / *Fly Particle* do cosmético). O mod expande pros membros na hora do spawn; cada membro mantém o próprio `tickInterval`.

---

## **Anexando a um cosmético**

No editor de cosmético, seção **Special Effects**:

* **Effect Visual** — lista separada por vírgula de ids de efeito **ou grupo**; toca sempre enquanto o cosmético está sendo usado.
* **Fly Particle** — igual, mas só enquanto o jogador está voando.

Um efeito (ou grupo) pode ser referenciado por qualquer quantidade de cosméticos.

---

!!! note "Sync"
    Efeitos e grupos são transmitidos pra todos os jogadores online ao salvar. Se um jogador entrou antes do efeito existir, o `/gc reload` (ou o próximo join dele) pega.
