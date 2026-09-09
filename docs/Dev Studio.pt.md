# **Dev Studio**

---

O **Dev Studio** é o editor dentro do jogo. Tudo que ele muda é gravado nos arquivos de config **e transmitido pra todos os jogadores online na hora** — sem reiniciar, geralmente sem `/gc reload`.

---

## **Acesso**

* Abra `/wardrobe` → aba **Dev Studio**.
* Exige uma conta de **operador de verdade**, e o **jar completo do servidor** (o jar client-only tem o Dev Studio removido).
* Só o `gc.dev` te dá os controles de admin *dentro* das abas Tags e Party, mas não este painel.

O menu tem cinco páginas: **Cosmetics**, **Effects**, **Cosmetics Types**, **Server Config**, **Slots**.

---

## **Página Cosmetics**

Uma grade pesquisável com um **filtro de tipo**. Dois botões de criar:

* **+ Cosmetic** — um cosmético padrão novo (`new_cosmetic_XXXX`).
* **+ Armor** — um cosmético baseado em armadura vinculado a um item real (ver [Cosméticos de Armadura](Armor Cosmetics.md)).

Clique num cosmético pra abrir o editor. `S` salva, `X` apaga (com confirmação), `<` volta.

### Seções do editor

| Seção | Campos |
| :--- | :--- |
| **Identification** | Main ID (nome do arquivo), Icon Name, Display Name, Slot, Type, Permission. *(Cosméticos de armadura mostram "Real Item" no lugar do ID.)* |
| **3D Models** | Um bloco por **parte** — ver abaixo. |
| **Variants** | Opcional. Posicionamentos alternativos do mesmo model — cada um com id, nome, slot e anchor/offset/rotação/escala próprios. `+ Add Variant`, `>> Config Variant N`, `X Remove Variant N`. Ver abaixo. *(só cosmético virtual)* |
| **Status & Combat** | Armor Points, Toughness, Max Durability, Auto-Feed. → [Atributos](Attributes.md) |
| **Backpack** | Is Backpack?, Rows, Pages, Name. → [Mochilas](Backpacks.md) |
| **Special Effects** | Allows Flight?, Fly / Ground / Swim Speed, `>> Select Effects` (poção), Effect Visual, Fly Particle. → [Atributos](Attributes.md) |
| **Cobblemon Cosmetics** | `>> Cobblemon Cosmetics` abre o editor de Lure + IVs Scanner. Cada campo tem tooltip por hover. → [Cobblemon Cosmetics](Lure System.md) |
| **Sounds** | Sons de Idle / Equip / Unequip / Walk / Fly / Shift / Backpack, cada um com volume + pitch. → [Sons](Sounds.md) |

---

## **Editando uma parte**

Cada parte em **3D Models** tem:

* **Part N (Model/ID)** — o nome do ícone chapado / modelo vanilla.
* **Part N (GeckoLib Model ID)** — um nome de geometria GeckoLib (tem prioridade quando definido).
* **Part N: Exact Path** — toggle: tratar os dois campos acima como caminhos relativos completos em vez de só nomes de arquivo.
* **`>> Config Part N`** — abre o popup de transform.
* **`X Remove Part N`** — apaga a parte.
* **`+ Add Part`** — adiciona outra parte.

Explicação completa em [Partes & Modelos](Parts and Models.md), incluindo o **gizmo 3D** (segure `X`, `Y` ou `Z` e arraste fora do painel pra mover / girar / escalar a parte selecionada ao vivo).

O popup de transform: ferramenta do gizmo (Mover / Girar / Escala), **Anchor**, **Scale XYZ**, **Valores normais** (Offset / Rotation XYZ), e **Valores de Sneak** (Shift Offset / Rotation XYZ, usados enquanto o jogador está agachado).

---

## **Variants**

Uma **variante** é um *posicionamento* alternativo do cosmético — mesmo model, posição diferente. Ex: um cachecol com uma variante `neck` e uma `waist`.

* `+ Add Variant` cria; `X Remove Variant N` apaga.
* Cada linha tem um campo **Variant ID** (`[a-z0-9_]`, único no cosmético).
* `>> Config Variant N` abre o editor: **Display Name** (o que aparece no menu pro jogador), **Slot** (vazio = herda o slot do cosmético base — só afeta o limite de slot), **Anchor** e **Offset / Rotation / Scale**. O model em si vem da 1ª part do cosmético base.
* Quando um cosmético tem ≥1 variante, ao clicar nele no guarda-roupa o jogador vê um menu: **Padrão** (o posicionamento base) + cada variante. Só **uma** variante (ou o Padrão) pode ser usada por vez — tem que desequipar pra trocar.
* Variantes são grátis — quem tem o cosmético usa qualquer variante.
* Não coloque variante num cosmético **mochila** (todas compartilhariam o mesmo baú).

### Barra lateral esquerda

Aparece enquanto uma parte está selecionada:

* **S** — alterna a prévia de sneak pra você ver os valores de Sneak em ação.
* **Slider de alpha** — deixa o corpo do jogador transparente (não o cosmético) pra ver as partes com clareza.
* **+ / −** — só pra partes GeckoLib: ajusta o pivô do gizmo (salvo em `gizmo_dev_config.json`).

---

## **Página Effects**

Cria e edita **efeitos de partícula** — `particleId`, count, tick interval, offsets de posição, spread e speed, com uma prévia 3D ao vivo e um gizmo 3D pros offsets. Ver [Efeitos de Partícula](Particle Effects.md). Anexe um efeito a um cosmético via **Special Effects → Select Effects**.

---

## **Página Cosmetics Types**

Define **tipos** de acessório — Type ID, Base Slot, Limit Per Player, Permission. Os tipos são como você limita "um colar por vez" separado do limite de slot. Ver [Slots & Tipos](Slots and Types.md).

---

## **Página Slots**

Edita os nove **slots** virtuais — Name (tem que ser um dos nove), Default Limit, Extra Permission (o node base pros tiers de limite). Ver [Slots & Tipos](Slots and Types.md).

---

## **Página Server Config**

Edita o `mainconfig.conf` ao vivo: Auto Detect Models, configurações de MySQL, Force Resource Pack + Texture URL/ID/SHA1, e a lista de **comandos de boot**. Ver [Config Principal](Main Config.md).

---

## **Alterações não salvas**

Sair de um editor com edições pendentes mostra um popup: **Salvar**, **Não Salvar**, ou **Continuar** editando. `Esc` dispara o mesmo aviso.

---

!!! tip "Testar sem possuir as coisas"
    Ligue o **Dev Mode** (o toggle `Dev: ON` na gaveta de slots equipados, ou ele auto-liga quando um operador abre a aba Dev/Tags/Party). Todo cosmético e Tag fica previsualizável sem um `/gc give`.
