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

### **Party**

Skins de Pokémon pro time do jogador. Escolha um slot do time com as setas, navegue nas skins disponíveis, e aplique uma (respeitando o cooldown e a espécie). Uma prévia 3D ao vivo deixa você ciclar poses, formas alternativas e shiny antes de confirmar. Ver [Skins de Pokémon](Pokemon Skins.md).

### **Tags**

Seletor de prefixo de chat. Tags possuídas primeiro, as trancadas (com um 🔒) depois. Clique pra equipar. Staff com `gc.dev` ganha um toggle **DEV** aqui pra previsualizar e gerenciar Tags. Ver [Tags](Tags.md).

### **Dev Studio**

Só visível pra **operadores de verdade** (e só no jar completo do servidor). O editor in-game de cosméticos, efeitos, tipos, slots e config do servidor. Ver [Dev Studio](Dev Studio.md).

---

## **Gaveta de slots equipados**

Uma pequena gaveta na lateral mostra os nove slots virtuais do jogador e o que está equipado em cada um. Operadores / quem tem `gc.dev` também ganha um toggle **Dev: ON/OFF** aqui — o Dev Mode faz todo cosmético e Tag aparecer como possuído pra você previsualizar.

---

## **Cenários de estúdio**

`/gc wardrobe setbackground <nome>` salva sua posição atual como uma cena nomeada. Aí `/wardrobe <jogador> <nome>` abre o guarda-roupa pra esse jogador **naquele lugar** — ótimo pra um "provador" decorado. Salvo em `config/greatcosmetics/studios.json`.
