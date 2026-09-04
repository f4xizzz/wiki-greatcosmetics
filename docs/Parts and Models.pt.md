# **Partes & Modelos**

---

Um cosmético renderiza como uma ou mais **partes**. Cada parte é ou um **ícone chapado** (um modelo de item flutuante) ou um modelo 3D **GeckoLib**, ancorado a um ponto do corpo e transformado com offset / rotação / escala.

---

## **Os dois modos de renderização**

### 1. Ícone chapado / modelo vanilla

Defina **`customModelData_or_ID`** com um nome. O mod procura, nesta ordem:

1. `assets/greatcosmetics/textures/icons/<nome>.png` — um ícone chapado simples (o mais comum).
2. `assets/greatcosmetics/models/<nome>.json` — um modelo de item vanilla personalizado.

A parte é desenhada como esse modelo de item flutuando na âncora.

### 2. Modelo GeckoLib

Defina **`geoModelId`** com um nome. Isso **tem prioridade** sobre o ícone chapado. O mod procura, em **qualquer** namespace:

* `geo/item/<nome>.geo.json` — obrigatório
* `textures/item/<nome>.png` — obrigatório (o mod também tenta a pasta que espelha o caminho do `.geo`)
* `animations/item/<nome>.animation.json` — opcional

Partes GeckoLib tocam a animação de idle automaticamente.

### Modo Caminho Exato

Com **`useExactPath`** ligado, os dois campos acima deixam de ser "só o nome do arquivo" e viram um **caminho relativo completo** resolvido por igualdade exata em qualquer namespace:

| Modo | Valor do campo | Resolve pra |
| :--- | :--- | :--- |
| Off | `cigar` | `.../models/cigar.json` (namespace `greatcosmetics` pra modelos vanilla) |
| On | `sas/cigar` | `.../models/sas/cigar.json` em **qualquer** namespace |
| On (Geo) | `item/hat` | `.../geo/item/hat.geo.json` em qualquer namespace |

Use quando seus arquivos estão em subpastas ou no namespace de outro mod, ou quando dois arquivos têm o mesmo nome.

---

## **Âncoras**

Onde a parte se prende:

`HEAD`, `BODY`, `RIGHT_ARM`, `LEFT_ARM`, `RIGHT_LEG`, `LEFT_LEG`

A âncora segue a animação da parte do corpo (a cabeça vira, os braços balançam), aí o offset/rotação/escala da parte são aplicados por cima.

---

## **Transforms**

| Grupo | Campos | Usado |
| :--- | :--- | :--- |
| **Escala** | `scaleX/Y/Z` (padrão 1.0) | Sempre |
| **Valores normais** | `offsetX/Y/Z`, `rotationX/Y/Z` | Em pé |
| **Valores de Sneak** | `shiftOffsetX/Y/Z`, `shiftRotationX/Y/Z` | Enquanto o jogador está agachado |

Os valores de Sneak existem porque a pose de agachar do vanilla dobra o corpo — um chapéu que fica certo em pé pode clipar agachado, então você ajusta uma posição separada pra ele.

---

## **O gizmo 3D**

No Dev Studio, selecione uma parte (clique nela no outliner ou abra `>> Config Part`). Aí, **em qualquer lugar fora do painel**:

1. Segure **`X`**, **`Y`** ou **`Z`** — trava o eixo.
2. Arraste o mouse — a parte **move**, **gira** ou **escala** ao vivo (escolha o modo com os botões Mover / Girar / Escala no popup).

Os campos de texto atualizam enquanto você arrasta, e vice-versa. Alterne o botão **S** da barra lateral pra editar a pose de Sneak do mesmo jeito.

---

## **Várias partes**

Adicione partes com **`+ Add Part`**. Um único cosmético pode combinar, por exemplo, um chapéu GeckoLib no `HEAD` mais um ícone chapado de pena deslocado pro lado — cada um com o seu próprio transform. Não há limite rígido; mantenha razoável pra performance.

---

## **Checklist pra um modelo novo**

1. Coloque os arquivos no seu resource pack (ícone **ou** `.geo` + textura).
2. `/gc reload` (ou reinicie o cliente) pra ele escanear o pack.
3. Dev Studio → **+ Cosmetic** → defina Slot, Type, Display Name.
4. Em **3D Models**, digite o nome do arquivo em **Model/ID** (chapado) ou **GeckoLib Model ID** (3D). Ligue **Exact Path** se o arquivo estiver numa subpasta/namespace.
5. `>> Config Part` → posicione com o gizmo.
6. `S` pra salvar. Já está no ar pra todo mundo.
