# **Dev Studio**

---

O **Dev Studio** é o editor dentro do jogo. Tudo que ele muda é gravado nos arquivos de config **e transmitido pra todos os jogadores online na hora** — sem reiniciar, geralmente sem `/gc reload`.

---

## **Acesso**

* Abra `/wardrobe` → aba **Dev Studio**.
* Exige uma conta de **operador de verdade**, e o **jar completo do servidor** (o jar client-only tem o Dev Studio removido).
* Só o `gc.dev` te dá os controles de admin *dentro* das abas Tags e Party, mas não este painel.

O menu tem **Cosmetics**, **Effects**, **Cosmetics Types**, **Server Config**, **Slots**, e **Chat Tags** (só aparece se o servidor tiver **LuckPerms** — ver [Permissões](Permissions.md)).

---

## **Página Cosmetics**

Uma grade pesquisável com um **filtro de tipo**. Dois botões de criar:

* **+ Cosmetic** — um cosmético padrão novo (`new_cosmetic_XXXX`).
* **+ Armor** — um cosmético baseado em armadura vinculado a um item real (ver [Cosméticos de Armadura](Armor Cosmetics.md)).

Clique num cosmético pra abrir o editor. **S** salva, **C** duplica (`<id>_copy`, `_copy2`…), **X** apaga (com confirmação), **<** volta. Passe o mouse em qualquer um dos quatro pra ver o tooltip.

### Seções do editor

| Seção | Campos |
| :--- | :--- |
| **Identification** | Main ID (nome do arquivo), Icon Name, Model Texture, Display Name, **Tooltip Description** (linhas extras em MiniMessage mostradas abaixo do nome no guarda-roupa), Slot, Type, Permission, **Granted Permissions**, **Minecraft Tags**. *(Cosméticos de armadura mostram "Real Item" no lugar do ID.)* |
| **Icon** | Só pra cosmético virtual sem ícone chapado próprio — enquadra o modelo 3D quando ele é usado como o próprio ícone na grade do guarda-roupa. Ver [Fazendo Models](Making Models.md#the-icon-of-a-3d-model). |
| **Auto-Unlock** | **Unlock Permission** / **Unlock Tag** — quem tiver um dos dois ganha o cosmético automaticamente, sem linha no banco, e perde no instante em que deixa de qualificar. Ver [Permissões](Permissions.md#auto-unlock). |
| **3D Models** | Um bloco por **parte** — ver abaixo. |
| **Variants** | Opcional. Posicionamentos alternativos do mesmo model, cada um podendo ter seus próprios efeitos também — ver abaixo. *(só cosmético virtual)* |
| **Status & Combat** | Armor Points, Toughness, Max Durability, Auto-Feed. → [Atributos](Attributes.md) |
| **Backpack** | Is Backpack?, Rows, Name. → [Mochilas](Backpacks.md) |
| **Special Effects** | Allows Flight?, Fly / Ground / Swim Speed, `>> Select Effects` (efeitos de poção — agora também valem pra **cosmético de armadura**, ver abaixo), Effect Visual, Fly Particle, **Shift Particle** (toca só enquanto agachado). → [Atributos](Attributes.md), [Efeitos de Partícula](Particle Effects.md) |
| **Cobblemon Effects** | `>> Cobblemon Effects` abre o editor de Lure + Scanners (só aparece se o servidor tiver Cobblemon). Cada campo tem tooltip por hover. → [Cobblemon Effects](Lure System.md) |
| **Sounds** | Sons de Idle / Walk / Fly / Shift, cada um com volume + pitch, mais **Sound Interval** e **Idle Sound Interval** (ticks entre repetições). → [Sons](Sounds.md) |

!!! note "Granted Permissions e Minecraft Tags"
    Listas separadas por vírgula. Todo node em **Granted Permissions** e toda tag em **Minecraft Tags** é aplicado ao jogador enquanto o cosmético está equipado **e** o gate `Permission` passa, e removido no instante em que ele desequipa — o mesmo mecanismo que as [Tags](Tags.md) já usam. Isso também funciona pra **cosmético de armadura** vestido como o item real.

---

## **Editando uma parte**

Cada parte em **3D Models** tem:

* **Part N (Model/ID)** — o nome do ícone chapado / modelo vanilla.
* **Part N (GeckoLib Model ID)** — um nome de geometria GeckoLib (tem prioridade quando definido).
* **Part N: Exact Path** — toggle: tratar os dois campos acima como caminhos relativos completos em vez de só nomes de arquivo.
* **`>> Config Part N`** — abre o popup de transform.
* **`+ Duplicate Part N`** — insere uma cópia exata da parte logo depois dela.
* **`X Remove Part N`** — apaga a parte.
* **`+ Add Part`** — adiciona outra parte.

Cosméticos de armadura mostram um dropdown **Part N: Anchor** direto na lista (`HEAD`/`BODY`/`RIGHT_ARM`/`LEFT_ARM`/`RIGHT_LEG`/`LEFT_LEG`) — o modelo 3D real da armadura renderiza naquele osso. Um botão **`>> Split into N body parts`** reconstrói a lista de partes pra combinar com o slot da armadura (peitoral → torso + braços, calça → torso + pernas, bota → pernas), cada uma seguindo o próprio osso.

Explicação completa em [Partes & Modelos](Parts and Models.md), incluindo o **gizmo 3D** (segure `X`, `Y` ou `Z` e arraste fora do painel pra mover / girar / escalar a parte selecionada ao vivo).

O popup de transform: ferramenta do gizmo (Mover / Girar / Escala), **Anchor**, **Scale XYZ**, **Valores normais** (Offset / Rotation XYZ), e **Valores de Sneak** (Shift Offset / Rotation XYZ, usados enquanto o jogador está agachado).

---

## **Variants**

Uma **variante** é um *posicionamento* alternativo do cosmético — mesmo model, posição diferente — e também pode ter seus próprios efeitos de partícula. Ex: um cachecol com uma variante `neck` e uma `waist`.

* `+ Add Variant` cria e já abre o editor dela; `X Remove Variant N` apaga.
* Cada linha tem um campo **Variant ID** (`[a-z0-9_]`, único no cosmético).
* `>> Config Variant N` abre o editor: **Display Name** (o que aparece no menu pro jogador), **Slot** (vazio = herda o slot do cosmético base — só afeta o limite de slot), **Anchor**, **Offset / Rotation / Scale** (com o gizmo 3D e a prévia ao vivo, igual uma parte normal) e uma seção **=== EFFECTS ===** — deixar **Effect Visual** / **Fly Particle** / **Shift Particle** **vazios** herda os do cosmético base; preencher pelo menos um dá à variante o próprio conjunto.
* Quando um cosmético tem ≥1 variante, ao clicar nele no guarda-roupa o jogador vê um menu: **Padrão** (o posicionamento base) + cada variante. Só **uma** variante (ou o Padrão) pode ser usada por vez — tem que desequipar pra trocar.
* Variantes são grátis — quem tem o cosmético usa qualquer variante.
* Não coloque variante num cosmético **mochila** (todas compartilhariam o mesmo baú).

---

## **Barra de ferramentas do gizmo**

Um conjunto de botões aparece ao redor da prévia 3D sempre que uma Part ou um Effect está selecionado — nenhum deles precisa do painel lateral aberto.

**Barra lateral esquerda** (do lado do popup de transform):

| Botão | Faz |
| :--- | :--- |
| **S** | Alterna a prévia de sneak, pra você ver os valores de Sneak em ação. |
| **Slider de alpha** | Deixa o corpo do jogador transparente (não o cosmético) pra ver as partes com clareza. |
| **C** | Alterna se os cosméticos *realmente equipados* do jogador também aparecem na prévia, junto com o que você está editando (ligado por padrão na página Effects, desligado no resto). |
| **P** | Alterna a visibilidade de partícula na sua própria prévia (mesma preferência do toggle da aba Preview). |
| **+ / −** | Só pra partes GeckoLib: ajusta o pivô do gizmo (salvo em `gizmo_dev_config.json`). |
| **E** | *(só na página Effects, editando um membro de grupo)* Isolar — esconde todos os outros membros do grupo pra só o que você está editando aparecer. |

**Canto inferior esquerdo:** **D** — mostra os números crus de debug do gizmo (só com uma part/effect selecionado).

**Centro-direita da tela:** três botões coloridos (**X** vermelho, **Y** verde, **Z** azul) — zera o offset daquele eixo (ou o offset de Sneak, na prévia de Sneak) com um clique, em vez de arrastar o gizmo de volta na mão.

**Canto inferior direito** *(com uma part selecionada)*: **↔** espelha horizontalmente (inverte `scaleX`), **↕** espelha verticalmente (inverte `scaleY`), **↺** reseta a parte (offset/rotação voltam a 0, escala volta a 1).

**Canto superior direito:** **Anim** — faz a prévia ao vivo ciclar por `AUTO → idle → walk → run → fly → swim → fall → sneak`, forçando aquele estado de animação pra você conferir cada clipe sem precisar fazer aquilo de verdade no jogo. Só pra partes GeckoLib.

---

## **Undo / Redo**

`Ctrl+Z` desfaz, `Ctrl+Shift+Z` (ou `Ctrl+Y`) refaz — funciona nos editores de **Cosmetics** e **Effects** (não dentro do editor de grupo nem na lista). As edições são agrupadas: só grava um passo depois de ~400 ms parado, então você não precisa desfazer tecla por tecla.

---

## **Página Effects**

Cria e edita **efeitos de partícula e grupos de efeito** — bursts simples ou formas geométricas (círculo, hélice, feixe, pulso), com cor, presets, prévia 3D ao vivo e um gizmo 3D pros offsets. Tem sua própria busca e um filtro All / Effects / Groups. Ver [Efeitos de Partícula](Particle Effects.md) pra referência completa dos campos. Anexe um efeito (ou grupo) a um cosmético via **Special Effects → Effect Visual / Fly Particle / Shift Particle**.

---

## **Página Cosmetics Types**

Define **tipos** de acessório — Type ID, Base Slot, Limit Per Player, Permission (e os nodes de tier `gc.extratypeslot.*`). Os tipos são como você limita "um colar por vez" separado do limite de slot. Ver [Slots & Tipos](Slots and Types.md).

---

## **Página Slots**

Os nove **slots** virtuais são fixos — não dá pra renomear, adicionar ou apagar. Edite só **Default Limit** e **Permission** (o node base pros limites em tier, `/gc extraslot`, etc.) por slot. Ver [Slots & Tipos](Slots and Types.md).

---

## **Página Chat Tags**

*(Só aparece se o servidor tiver LuckPerms.)* Um editor dedicado pro mesmo catálogo que a aba **Tags** do guarda-roupa já deixa jogadores com `gc.dev` editarem — lista toda Tag (as de grupo primeiro, depois as personalizadas), **+ New Tag**, clique numa pra editar Display Name / Description / Prefix / Permissions / Minecraft Tag. Tags de grupo podem ser editadas mas não apagadas. Ver [Tags](Tags.md).

---

## **Página Server Config**

Edita o `mainconfig.conf` ao vivo: Auto Detect Models, configurações de MySQL, Force Resource Pack + Texture URL/ID/SHA1 (mantido sincronizado com o `server.properties` automaticamente), **Effect Block Groups** (grupos do LuckPerms cujos cosméticos continuam *aparecendo* mas não dão nada), o toggle da HUD de Lure, e a lista de **comandos de boot**. Ver [Config Principal](Main Config.md).

---

## **Alterações não salvas**

Sair de um editor com edições pendentes mostra um popup: **Salvar**, **Não Salvar**, ou **Continuar** editando. `Esc` dispara o mesmo aviso.

---

!!! tip "Testar sem possuir as coisas"
    Ligue o **Dev Mode** (o toggle `Dev: ON` na gaveta de slots equipados, ou ele auto-liga quando um operador abre a aba Dev/Tags/Party). Todo cosmético e Tag fica previsualizável sem um `/gc give`.
