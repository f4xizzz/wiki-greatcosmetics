# **Criando Modelos & Texturas**

---

Este é o guia prático: **o que é o modelo de um cosmético**, a diferença entre um modelo **chapado / vanilla** e um modelo **GeckoLib**, **em qual pasta cada arquivo vai**, e como desenhar as texturas. Quando terminar aqui, [Partes & Modelos](Parts and Models.md) cobre os campos de posicionamento e [Resource Pack](Resource Pack.md) cobre como levar o pack pros jogadores.

---

## **Os três modos de renderização**

Uma [parte](Parts and Models.md) de um cosmético é desenhada de um de três jeitos. Você escolhe por parte, no Dev Studio.

| Modo | O que é | Você fornece | Anima? | Use pra |
| :--- | :--- | :--- | :--- | :--- |
| **Ícone chapado** | Um único PNG mostrado como um sprite flutuante (como um item na mão). Sem arquivo de modelo nenhum. | um `.png` | Não | Emblemas, distintivos 2D, testes rápidos, cosméticos "adesivo" |
| **Modelo vanilla** | Um modelo de item normal do Minecraft — o mesmo formato JSON de qualquer item ou bloco vanilla: uma caixa de cuboides ("elements") com textura mapeada por UV. | um `.json` + o `.png` dele | Não | Chapéus blocados, props 3D simples, qualquer coisa que você faria como item model de resource pack |
| **Modelo GeckoLib** | Um modelo de ossos e cubos no **formato Bedrock** (`.geo.json`) com textura própria e um arquivo de animação opcional. Renderizado em 3D de verdade com animação por osso. | `.geo.json` + `.png` (+ `.animation.json` opcional) | **Sim** | Asas, capas, caudas, antenas, qualquer coisa curva / orgânica / que deva se mexer |

**Regra de bolso:** se nunca se mexe e é uma forma chapada → ícone chapado. Se nunca se mexe mas tem profundidade → modelo vanilla. Se deve tremular, balançar, girar, ou se curva em volta do corpo → GeckoLib.

!!! info "Ícone chapado vs modelo vanilla — mesmo campo"
    Os dois usam o campo **`Model ID`** da parte. O mod procura primeiro um `textures/icons/<nome>.png` (ícone chapado); se não tiver, procura um `models/<nome>.json` (modelo vanilla). GeckoLib é um **campo separado** (`GeckoLib Model`) e sempre ganha quando preenchido.

---

## **Ferramentas necessárias**

* **[Blockbench](https://www.blockbench.net/)** (grátis) — modela tanto item models vanilla *quanto* modelos GeckoLib, pinta texturas e faz as animações do GeckoLib. É a única ferramenta de modelagem que você precisa.
* **Qualquer editor de imagem com transparência** — GIMP, Krita, Aseprite, Photoshop, Paint.NET — pros ícones chapados ou retoque de textura. A aba de pintura do Blockbench já resolve o simples.
* Uma **pasta de resource pack** pra jogar os arquivos prontos. Veja [Resource Pack](Resource Pack.md) pra como ele chega nos jogadores — tudo abaixo é sobre *o que* vai *onde* dentro dele.

---

## **Caminhos das pastas**

Tudo que um cosmético precisa fica em **`assets/<namespace>/`** dentro de um resource pack (ou dentro do jar do mod, pros que já vêm de fábrica).

```
seu_pack.zip
└── assets/
    ├── greatcosmetics/                 ← ícones chapados & modelos vanilla TÊM que ficar aqui
    │   ├── textures/
    │   │   └── icons/
    │   │       └── wizard_hat.png      ← ícone chapado  → Model ID: wizard_hat
    │   └── models/
    │       └── crown.json              ← modelo vanilla → Model ID: crown
    │
    └── meupack/                        ← arquivos GeckoLib podem ser em QUALQUER namespace
        ├── geo/
        │   └── item/
        │       └── dragon_wings.geo.json        ← GeckoLib Model: dragon_wings
        ├── textures/
        │   └── item/
        │       └── dragon_wings.png             ← a textura dele (nome igual ao do geo)
        └── animations/
            └── item/
                └── dragon_wings.animation.json  ← opcional (ver Animações por estado)
```

| Tipo de arquivo | Pasta | Namespace | Casado por |
| :--- | :--- | :--- | :--- |
| Ícone chapado | `textures/icons/` | **só `greatcosmetics`** | nome do arquivo → **Model ID** da parte |
| Modelo vanilla | `models/` | **só `greatcosmetics`** | nome do arquivo → **Model ID** da parte |
| Geometria GeckoLib | `geo/…/` (normalmente `geo/item/`) | **qualquer** namespace carregado | nome do arquivo (sem `.geo.json`) → **GeckoLib Model** da parte |
| Textura GeckoLib | `textures/…/` (normalmente `textures/item/`) | qualquer | nome do arquivo igual ao do geo — ou o caminho espelhado `geo/x` → `textures/x` |
| Animação GeckoLib | `animations/…/` (normalmente `animations/item/`) | qualquer | nome do arquivo igual ao do geo |

Notas:

* **Só o nome do arquivo importa** pro GeckoLib (a menos que você use Caminho Exato). `geo/item/dragon_wings.geo.json`, `geo/dragon_wings.geo.json`, `geo/cosmetics/dragon_wings.geo.json` todos resolvem de `GeckoLib Model: dragon_wings`. Mantenha os nomes **únicos** no pack inteiro.
* Se dois arquivos têm o mesmo nome em pastas diferentes, ligue o toggle **Exact Path** da parte e digite o caminho relativo completo (`item/dragon_wings`, `hats/wizard_hat`).
* A textura GeckoLib é achada tentando o **caminho espelhado primeiro** (`geo/item/x.geo.json` → `textures/item/x.png`), depois pelo nome solto em qualquer lugar. É por isso que manter geo e textura em pastas `item/` espelhadas é o padrão seguro.
* `autoDetectModels` no [`mainconfig.conf`](Main Config.md) (ligado por padrão) é o que faz o mod escanear o pack e conectar o Custom Model Data. Deixe ligado.

---

## **Texturas**

### Textura de ícone chapado

* **Formato:** PNG, RGBA (precisa ter canal alfa — as partes transparentes têm que ser *de verdade* transparentes, não brancas).
* **Tamanho:** `16×16` é o visual clássico. `32×32`, `64×64`, `128×128` também funcionam — maior = mais nítido, mas mantenha potência de dois e não exagere.
* **Estilo:** é renderizado igual a um item na mão, então pixel-art fica melhor. Bordas suaves com anti-aliasing ficam borradas na grade da mochila.
* Salve como `assets/greatcosmetics/textures/icons/<nome>.png`. Esse `<nome>` é o que você digita no **Model ID** da parte (ou no **Icon Name** do cosmético, se vários cosméticos compartilham um ícone).

### Textura de modelo vanilla

Um modelo vanilla é um `.json` que lista cuboides e um bloco `textures` apontando pros PNGs:

```json
{
  "textures": { "0": "greatcosmetics:item/crown", "particle": "greatcosmetics:item/crown" },
  "elements": [
    { "from": [4,0,4], "to": [12,4,12],
      "faces": {
        "north": { "uv": [0,0,8,4], "texture": "#0" },
        "up":    { "uv": [0,4,8,12], "texture": "#0" }
      }
    }
  ]
}
```

* O **espaço UV é sempre `0–16`** independente do tamanho real em pixels do PNG — `uv: [0,0,8,4]` quer dizer "a metade esquerda, quarto de cima da textura".
* Coloque o PNG onde o bloco `textures` diz — ex: `greatcosmetics:item/crown` → `assets/greatcosmetics/textures/item/crown.png`.
* **Caminho mais fácil:** no Blockbench, `File → New → Java Block/Item Model`, construa, pinte, aí `File → Export → Java Model` pro `.json` e `File → Export → Textures`. Jogue o `.json` em `models/` e ajuste os caminhos de textura pro seu namespace.

### Textura de modelo GeckoLib

* O cabeçalho do `.geo.json` declara o tamanho da textura:

  ```json
  "description": { "identifier": "geometry.dragon_wings",
                   "texture_width": 64, "texture_height": 64 }
  ```

* Seu PNG **tem que ter exatamente `texture_width × texture_height`**. Se você redimensionar a textura do modelo no Blockbench, esse cabeçalho atualiza sozinho — sempre re-exporte o geo depois de mudar o tamanho da textura.
* O GeckoLib usa **box UV** por padrão (o Blockbench desdobra cada cubo na folha pra você). Pinte dentro dessas ilhas; pintar fora delas não faz nada.
* Exporte a textura do Blockbench (`File → Export → Textures`, ou botão direito na textura → *Save As*) e coloque do lado do geo numa pasta espelhada: geo em `meupack/geo/item/`, textura em `meupack/textures/item/`, **mesmo nome base**.
* Transparência funciona — use pra bordas de pena, buracos, etc.

!!! tip "Um modelo, várias skins"
    Faça o modelo uma vez, aí crie vários cosméticos que cada um define uma **Model Texture** diferente (ver abaixo). Ótimo pra variantes de cor do mesmo chapéu.

---

## **Passo a passo — um cosmético de ícone chapado**

1. Desenhe um PNG `32×32` com fundo transparente. Salve como
   `assets/greatcosmetics/textures/icons/star_badge.png` no seu pack.
2. Leve o pack pro seu cliente (pasta do modpack, ou o [Forced Resource Pack](Resource Pack.md)).
3. No jogo: `/gc reload` — ou só relogue — pra o mod escanear o pack.
4. `/wardrobe` → **Dev Studio** (aba `D`) → **Cosmetics** → **+ Cosmetic**.
5. Defina **Main ID** `star_badge`, um **Display Name**, um **Slot** (ex: `FACE`), deixe **Type** `default`.
6. Em **3D MODELS**, na Part 1, digite `star_badge` em **Model ID**. Deixe GeckoLib vazio.
7. `>> Config Part` → ajuste o **Offset Y** até ficar onde você quer. Salve com o **S** da barra lateral.
8. `/gc give star_badge <você>` → abra a mochila → equipe.

---

## **Passo a passo — um chapéu GeckoLib**

**No Blockbench:**

1. `File → New → Bedrock Model`.
2. `File → Project` (ou o painel de configurações do projeto) → defina **Texture Size** como `64 × 64`.
3. Modele o chapéu. O mod centraliza automaticamente um modelo GeckoLib no meio da própria caixa delimitadora dele ao ancorar num ponto do corpo, então modelar fora da origem tá tranquilo — um modelo centrado em `[0,0,0]` continua sendo um hábito legal, mas não é mais necessário pra um posicionamento padrão bom. Ajuste fino a partir daí com o Offset.
4. Pinte (aba **Paint**) ou `File → Export → Export Texture` uma folha em branco e pinte no seu editor de imagem, depois re-importe.
5. *(Opcional)* aba **Animate** → crie uma animação em loop e nomeie exatamente `idle` (ou `fly`, `walk`, … — ver [Animações por estado](Parts and Models.md#animacoes-por-estado)). Pule isso pra um chapéu estático.
6. `File → Export → Export Bedrock Geometry` → `wizard_hat.geo.json`.
7. `File → Export → Export Texture` → `wizard_hat.png`.
8. *(Se animou)* `File → Export → Export Bedrock Animations` → `wizard_hat.animation.json`.

**No seu resource pack:**

```
assets/meupack/geo/item/wizard_hat.geo.json
assets/meupack/textures/item/wizard_hat.png
assets/meupack/animations/item/wizard_hat.animation.json   (só se você animou)
```

**No jogo:**

1. `/gc reload`.
2. Dev Studio → Cosmetics → **+ Cosmetic** → Main ID `wizard_hat`, Slot `HEAD`.
3. Part 1 → **GeckoLib Model**: `wizard_hat`. Deixe Model ID vazio.
4. `>> Config Part` → use o [gizmo 3D](Parts and Models.md#o-gizmo-3d) (`X`/`Y`/`Z` + arrastar) pra posicionar, girar e escalar na cabeça. Defina uma **pose de Sneak** com o botão **S** da barra lateral se clipar agachado.
5. Salve. Já está no ar pra todo jogador online que tem o pack.

Se o chapéu ficar **invisível**: o console imprime um `WARNING` dizendo qual arquivo faltou — quase sempre o nome do `.geo.json` ou do `.png` não bate, ou o PNG não está numa pasta `textures/` escaneada.

!!! info "Sem mais flicker em modelos animados"
    Modelos GeckoLib animados mais antigos — principalmente os feitos a partir de geometria rippada de Pokémon do Cobblemon (asas, capas, etc.) — costumavam tremular ou dar "z-fight" (a textura parecia uma camada brigando com a outra), mais visível em modelos animados. Dois bugs causavam isso: várias instâncias do mesmo modelo compartilhando um único relógio de animação, e o GeckoLib renderizando sem back-face culling enquanto os próprios modelos do Cobblemon esperam isso ligado. Os dois foram corrigidos — nada pra configurar, modelos animados (rippados do Cobblemon ou não) agora renderizam limpo.

---

## **O campo Model Texture**

No cosmético (não na parte), o **Model Texture** sobrescreve a textura de **todos** os modelos daquele cosmético — GeckoLib *e* vanilla.

* Vazio → o mod usa a textura cujo nome bate com o modelo (o comportamento normal).
* Um nome de arquivo → essa textura é usada no lugar. Nome solto → `textures/item/<nome>.png`; adicione um caminho pra uma subpasta; ou um `namespace:caminho` completo.
* Pra um **modelo vanilla** o mod serve uma *cópia* do JSON do modelo com a textura trocada, então o `.json` original no seu pack fica intocado e ainda pode ser usado por outros cosméticos com a skin padrão.

Use pra fazer um modelo e reskinar por cosmético (versões vermelha/azul/dourada de uma capa a partir de um único `.geo.json`).

---

## **O ícone de um modelo 3D** {#the-icon-of-a-3d-model}

Quando um cosmético **não tem Icon Name** e nem um PNG de ícone chapado, a grade da mochila mostra o **próprio modelo 3D** como ícone. O GeckoLib tem um único transform fixo de GUI, então um modelo feito pro corpo costuma sair gigante ou desenquadrado naquele quadradinho.

A seção **=== ICON ===** corrige só o ícone (nunca o modelo vestido): arraste a caixa de preview pra mover, scroll pra zoom, botão direito pra girar — ou digite em **Icon Scale / Offset / Rotation**. **Reset icon framing** volta ao normal. Isso não faz nada pra um ícone PNG.

Se o **Icon Scale** não foi mexido (ainda no padrão `1.0`), o mod agora calcula uma escala inicial automaticamente a partir dos limites do próprio modelo, mirando em algo perto do tamanho normal de um ícone de item — em vez de sempre começar chapado em `1.0`, que costumava sair grande demais ou pequeno demais. Os controles manuais acima continuam funcionando do mesmo jeito pra ajuste fino ou pra sobrescrever; o auto-scale só deixa o ponto de partida bem mais perto do certo antes de você mexer em qualquer coisa. Ele não gira o modelo sozinho — a "frente" de um modelo é subjetiva, então a rotação continua manual.

---

## **Erros comuns**

| Sintoma | Causa |
| :--- | :--- |
| Tudo é o xadrez roxo/preto | Cliente sem resource pack, ou ele falhou ao baixar. Veja o `latest.log`. |
| Ícone chapado mostra um item genérico | PNG não está em `assets/greatcosmetics/textures/icons/` (namespace ou pasta errados), ou o nome não bate com o Model ID. |
| Modelo GeckoLib invisível | Falta o `.geo.json` ou o `.png`; nomes não batem; textura fora de qualquer pasta `textures/`. O console diz o arquivo. |
| Modelo GeckoLib texturizado errado / UVs embaralhadas | O tamanho do PNG não bate com `texture_width`/`texture_height` do geo, ou duas texturas têm o mesmo nome e pegou a errada — espelhe as pastas (`geo/item/x` + `textures/item/x`) ou use **Exact Path**. |
| Modelo aparece mas nunca anima | `.animation.json` faltando, ou nenhum clip chamado `idle`/`walk`/`fly`/… — ver [Animações por estado](Parts and Models.md#animacoes-por-estado). |
| As mudanças não aparecem | Você não deu `/gc reload` depois de editar o pack, ou o cliente ainda está no pack antigo em cache. |
| Ícone no menu gigante / cortado | É um ícone de modelo 3D — enquadre na seção **=== ICON ===**. |
