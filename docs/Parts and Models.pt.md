# **Partes & Modelos**

---

Um cosmético renderiza como uma ou mais **partes**. Cada parte é ou um **ícone chapado** (um modelo de item flutuante) ou um modelo 3D **GeckoLib**, ancorado a um ponto do corpo e transformado com offset / rotação / escala.

!!! tip "Criando os arquivos"
    Esta página é a referência dos *campos*. Pra um passo a passo de **como criar os modelos e texturas** — caminhos das pastas, Blockbench, desenhar a textura — veja [Criando Modelos & Texturas](Making Models.md).

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
* `animations/item/<nome>.animation.json` — opcional (ver [Animações por estado](#animacoes-por-estado))

### Modo Caminho Exato

Com **`useExactPath`** ligado, os dois campos acima deixam de ser "só o nome do arquivo" e viram um **caminho relativo completo** resolvido por igualdade exata em qualquer namespace:

| Modo | Valor do campo | Resolve pra |
| :--- | :--- | :--- |
| Off | `wizard_hat` | `.../models/wizard_hat.json` (namespace `greatcosmetics` pra modelos vanilla) |
| On | `hats/wizard_hat` | `.../models/hats/wizard_hat.json` em **qualquer** namespace |
| On (Geo) | `item/wizard_hat` | `.../geo/item/wizard_hat.geo.json` em qualquer namespace |

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

Sempre que uma parte (ou um efeito) está selecionada, também aparecem três botões coloridos no centro-direita da tela: **X** (vermelho), **Y** (verde), **Z** (azul) — seguindo a mesma convenção de cores dos eixos do gizmo. Clicar em um deles zera na hora o Offset daquele eixo — ou, enquanto você tá pré-visualizando a pose de Sneak com o toggle **S** da barra lateral, zera o Sneak/Shift Offset daquele eixo. Um jeito rápido de encaixar uma parte de volta bem no centro da âncora dela sem arrastar o gizmo na mão ou digitar `0` num campo.

---

## **Várias partes**

Adicione partes com **`+ Add Part`**. Um único cosmético pode combinar, por exemplo, um chapéu GeckoLib no `HEAD` mais um ícone chapado de pena deslocado pro lado — cada um com o seu próprio transform. Não há limite rígido; mantenha razoável pra performance.

---

## **Animações por estado** {#animacoes-por-estado}

*(Só partes GeckoLib — ícone chapado nunca anima.)*

Um modelo GeckoLib toca uma animação do `.animation.json` dele **conforme o que quem veste está fazendo** — parado, andando, voando, etc. **Não tem código de controlador pra escrever nem nada pra configurar**: o mod escolhe o clip só pelo **nome**. Dê a um clip um dos nomes fixos abaixo e ele toca naquele estado; um modelo cujo `.animation.json` **não tem nenhum** desses nomes fica 100% estático (o comportamento antigo).

### Os nomes fixos

| Nome | Toca quando | Cai pra |
| :--- | :--- | :--- |
| `idle` | Parado (estado padrão / de descanso) | — |
| `walk` | Andando no chão | `idle` |
| `run` | Correndo (sprint) no chão | `walk` → `idle` |
| `fly` | Voando (creative / voo cosmético) ou planando com elytra | `idle` |
| `swim` | Na água e fora do chão | `walk` → `idle` |
| `fall` | No ar, sem voar (pulo / queda) | `idle` |
| `sneak` | Agachado | *(nada — ver abaixo)* |

**Prioridade** (ganha o primeiro cujo clip existir de verdade): `sneak` → `fly` → `swim` → `fall` → `run` → `walk` → `idle`.

O `sneak` é especial: se o model **não tem** um clip de `sneak`, agachar é **transparente** — a animação não muda (quem tá andando continua no `walk`, quem tá parado continua no `idle`). Todos os outros nomes caem pela cadeia até o `idle`.

Você só precisa dos clips que interessam. Uma capa só com `idle` e `fly` funciona — andar, agachar, etc. tudo desce até o `idle` (ou, no caso do sneak, simplesmente não muda nada).

### Nomeando no Blockbench

Você não precisa renomear pra palavra pura. O mod casa um clip cujo nome **termina com** o nome fixo depois de um separador — então tudo isso conta como `idle`:

* `idle`
* `animation.asa_dragao.idle` — o padrão do Blockbench `animation.<modelo>.<ação>`
* `ground_idle` / `animation.charizard.ground_idle` — a convenção do Cobblemon (animações rippadas de Pokémon)
* `battle_idle`, `air_idle`, … — qualquer coisa terminando em `_idle` / `-idle`

Mesma coisa pros outros: `ground_walk` → `walk`, `ground_run` → `run`, `air_fly` → `fly`. Quando vários clips poderiam casar, o mais específico ganha (`.idle` > `ground_idle` > `battle_idle`). Clips com `ride` ou `test` no nome são ignorados.

!!! tip "Quer uma animação sempre ligada?"
    Um modelo que deve sempre fazer a mesma coisa (um halo girando devagar, uma chama tremendo) — é só nomear esse clip de **`idle`**. Ele fica em loop em todos os estados porque tudo cai pro `idle`.

### Notas

* Todo clip fica em **loop**. Animação de uma vez só (one-shot) não é suportada aqui.
* Cada um que veste anima independente — dois jogadores com o mesmo cosmético não sincronizam.
* O blend entre estados é suavizado em ~5 ticks.
* No Dev Studio o jogador do preview só fica parado, então você só vai ver o `idle` (ou nada). Teste as animações de movimento no mundo.

---

## **Checklist pra um modelo novo**

1. Coloque os arquivos no seu resource pack (ícone **ou** `.geo` + textura).
2. `/gc reload` (ou reinicie o cliente) pra ele escanear o pack.
3. Dev Studio → **+ Cosmetic** → defina Slot, Type, Display Name.
4. Em **3D Models**, digite o nome do arquivo em **Model/ID** (chapado) ou **GeckoLib Model ID** (3D). Ligue **Exact Path** se o arquivo estiver numa subpasta/namespace.
5. `>> Config Part` → posicione com o gizmo.
6. `S` pra salvar. Já está no ar pra todo mundo.
