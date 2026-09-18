# **O Guarda-Roupa**

---

Os jogadores abrem o **Avatar Studio** com `/wardrobe`. É uma visão 3D em tela cheia do personagem, com um painel lateral em abas. A staff pode abrir pra outra pessoa com `/wardrobe <jogador>`.

Enquanto o guarda-roupa está aberto o jogador fica parado no lugar e a HUD some; fechar (ou `Esc`) devolve ele exatamente pra onde estava — mesmo depois de um crash ou desconexão (um fail-safe teleporta ele de volta no próximo join).

---

## **Controles de câmera**

| Entrada | Ação |
| :--- | :--- |
| Segurar botão esquerdo + arrastar | Girar a visão ao redor do personagem |
| Roda do mouse | Zoom |
| Segurar botão direito + arrastar | Mover a câmera (pan) |

Algumas categorias travam o zoom pra enquadrar a área do corpo relevante (ex: escolher **Cabeça** aproxima do rosto).

---

## **Abas**

A barra de abas fica no topo. Uma aba que não está com o mouse em cima / ativa encolhe pra um **prefixo de uma letra** (`A`, `C`, `P`, `T`, `D`) — essas letras, e os nomes completos, são todos editáveis nos [arquivos de idioma](Language.md) (`wardrobe.tab.*` e `wardrobe.tab.*.short`).

**Party** só aparece quando o servidor roda **Cobblemon**; **Tags** só quando roda **LuckPerms**; **Dev Studio** só pra operadores de verdade. Num servidor Fabric puro você vê só Acessórios e Preview.

### **Acessórios**

A aba principal. Mostra todo cosmético que o jogador **possui**, numa grade de 4 colunas.

* **Dropdown de categoria** — `Todos`, depois uma entrada por slot virtual.
* **Caixa de busca** — filtra pelo nome exibido.
* **★ Favoritos** — clique na estrela de um cosmético pra fixá-lo no topo da lista.
* **Clique num cosmético** — equipa (ou desequipa se já estiver usando). Uma borda verde marca os equipados.
* **Botão X** (canto superior direito) — "Limpar Tudo": remove todos os cosméticos equipados de uma vez.
* **Hover** — um tooltip lista os atributos do cosmético: armadura, habilidades (voo / mochila / auto-feed), efeitos de poção passivos, e bônus de Lure.

### **Preview**

Toggles de visibilidade de armadura. Cada botão esconde/mostra uma peça de armadura real **pra todo mundo que vê esse jogador**:

* Capacete · Peitoral · Calça · Botas

Útil pra um cosmético de chapéu não ficar bloqueado por um capacete real.

Um quinto toggle — **Cosméticos dos outros** — é uma config **local**: desligue e *você* para de ver os cosméticos de todo mundo (os seus continuam aparecendo). Salvo por cliente em `config/GreatCosmetics/client_local.json`, nunca enviado ao servidor.

### **Party**

Skins de Pokémon pro time do jogador. Escolha um slot do time com as setas, navegue nas skins disponíveis, e aplique uma (respeitando o cooldown e a espécie). Uma prévia 3D ao vivo deixa você ciclar poses, formas alternativas e shiny antes de confirmar. Ver [Skins de Pokémon](Pokemon Skins.md).

### **Tags**

Seletor de prefixo de chat (precisa do **LuckPerms**). Tags possuídas primeiro, as trancadas (com um 🔒) depois. Clique pra equipar. Staff com `gc.dev` ganha um toggle **DEV** aqui pra previsualizar e gerenciar Tags — incluindo botões **Add** / **Set** pros grupos do LuckPerms. Ver [Tags](Tags.md).

### **Dev Studio**

Só visível pra **operadores de verdade**. O editor in-game de cosméticos, efeitos, tipos, slots e config do servidor. Ver [Dev Studio](Dev Studio.md).

---

## **Gaveta de slots equipados**

Uma pequena gaveta na lateral mostra os nove slots virtuais do jogador e o que está equipado em cada um. Operadores / quem tem `gc.dev` também ganha um toggle **Dev: ON/OFF** aqui — o Dev Mode faz todo cosmético e Tag aparecer como possuído pra você previsualizar.

---

## **Cenários de estúdio**

`/gc wardrobe setbackground <nome>` salva sua posição atual como uma cena nomeada. Aí `/wardrobe <jogador> <nome>` abre o guarda-roupa pra esse jogador **naquele lugar** — ótimo pra um "provador" decorado. Salvo em `config/GreatCosmetics/studios.json`.

---

## **O Bloco Wardrobe**

Um móvel colocável, animado com GeckoLib, que abre a mesma tela de guarda-roupa sem precisar de comando nenhum — clique com o botão direito e ele toca uma animação de **abrir**, fechando de novo (troca instantânea, sem blend do GeckoLib no meio) quando o jogador sai.

* Encontre na aba de criativo **GreatCosmetics**, ou `/give <jogador> greatcosmetics:wardrobe`.
* É um **multiblock**: um footprint de 18 células (um retângulo plano 3×3, mais uma camada idêntica invisível bem atrás pra dar profundidade). Só o bloco que você clicou pra colocar é visível/interativo — o resto é colisão sólida mas invisível, e quebrar **qualquer** célula da estrutura remove tudo de uma vez.
* Clicar com o botão direito abre o guarda-roupa com a câmera **travada**: o jogador fica de frente pro bloco (então fica de costas pra ele, de frente pra câmera) e arrastar pra girar a visão fica desativado — só o zoom da roda do mouse continua funcionando. Nada na barra de abas (troca de página, filtro de categoria, etc) consegue mexer na câmera também.
* Dois controles extras aparecem que não existem na visão do comando `/wardrobe`:
    * **Setas `<` / `>`** (no mesmo estilo das setas de trocar Pokémon da aba Party) — giram o personagem 30° pra esquerda/direita pra você ver de ângulos diferentes sem mexer na câmera travada.
    * Um **botão de foco** (canto superior direito, acima da gaveta de slots equipados) que cicla o ponto de foco vertical da câmera entre **Head**, **Body**, **Legs** e **Feet**.
* A aba **Dev Studio** fica escondida aqui mesmo pra operadores de verdade — o bloco é pensado como um provador pro jogador, não um atalho de admin.

---

## **Menu de Ações Rápidas**

Aperte **`V`** (alterável em *Controles → GreatCosmetics*) em qualquer lugar do mundo pra abrir um menu radial ("roda") — a mesma ideia de layout da roda de interação com Pokémon do Cobblemon — listando atalhos rápidos pra quaisquer [Special Effects](Attributes.pt.md#special-effects-habilidades-ativas) que o jogador tenha equipado no momento:

| Slot | Sempre aparece? | Comportamento |
| :--- | :--- | :--- |
| **Open PC** | Sempre | Roda `/pc` na hora, de qualquer lugar. |
| **Heal Party Now** | Só se um cosmético de Heal Ability estiver equipado | Cura a party Cobblemon na hora, pulando o Shift-hold. |
| **Pollinate Now** | Só se um cosmético de Pollinator estiver equipado | Dispara o burst de bone meal na hora, pulando o Shift-hold. |
| **Vein Miner** / **Tree Capitator** | Só se essa habilidade estiver equipada | Liga/desliga pra sessão atual — o próprio botão da roda fica **verde** (ligado) ou **vermelho** (desligado) como indicador. Desligar não mexe na config do cosmético, e reseta sozinho no relogin. |

Clique num slot (ou clique num espaço vazio pra cancelar) — nenhum outro clique, atalho de teclado ou menu consegue abrir por cima enquanto esse já está na tela.
