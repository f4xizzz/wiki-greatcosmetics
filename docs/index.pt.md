# **Introdução**

---

## **Bem-vindo ao GreatCosmetics**

O **GreatCosmetics** é um framework completo de cosméticos para servidores **Cobblemon** em **Fabric** e **NeoForge**. Ele dá aos seus jogadores um *Avatar Studio* 3D para escolher e equipar cosméticos em nove slots virtuais do corpo, além de tags de chat, skins de Pokémon, mochilas de armazenamento, efeitos de partícula e um sistema de bônus de *Lure* do Cobblemon — tudo editável **dentro do jogo**, sem reiniciar, pelo **Dev Studio** embutido.

Todo texto que o mod mostra (menus, chat, nomes de item) fica em arquivos JSON editáveis e é renderizado com **MiniMessage**, então você controla o idioma, as cores e a formatação sem mexer no código.

---

## **Principais Recursos**

* **Avatar Studio 3D (`/wardrobe`):** uma prévia 3D giratória do jogador onde os cosméticos são equipados com um clique, organizados por categoria e pesquisáveis.
* **Nove slots virtuais:** `HEAD, FACE, NECK, CHEST, BACK, WAIST, LEGS, FEET, HAND` — independentes da armadura real do jogador, com limites por slot e por tipo e tiers de permissão.
* **Modelos 3D personalizados:** cosméticos renderizam como ícone chapado (Custom Model Data) **ou** como modelo **GeckoLib** animado completo, posicionado por parte com um gizmo 3D dentro do jogo.
* **Dev Studio in-game:** cria e edita cosméticos, efeitos de partícula, tipos de acessório, slots e configuração do servidor ao vivo — as mudanças são transmitidas pra todos os jogadores online.
* **Tags de Chat:** prefixos personalizados mais tags automáticas de grupo do **LuckPerms**, com editor dentro do jogo.
* **Skins de Pokémon:** skins por aspect para os Pokémon do time do jogador, com cooldown, formas alternativas e grupos temáticos.
* **Mochilas Cosméticas:** mochilas vestíveis que também funcionam como armazenamento de itens paginado.
* **Bônus de Lure do Cobblemon:** taxa de shiny, IV/EV, chance de captura, hidden ability, bônus de pesca e mais, anexados a qualquer cosmético.
* **Efeitos de Partícula e Sons:** rastros de partícula e sons por ação (equipar, andar, voar, agachar, parado…).
* **Conversão Armadura → Cosmético:** transforma itens de armadura reais em cosméticos do guarda-roupa automaticamente.
* **Resource Pack Forçado:** o mod pode enviar o texture pack pros clientes no join e no `/gc reload`, sem editar `server.properties`.

---

## **Desenvolvimento e Autoria**

O GreatCosmetics foi totalmente projetado e programado pelo **F4xizzz** — o mod Fabric/Java e o backend de licenciamento em Node.js.

---

!!! info "Comunidade Oficial"
    Dúvidas de configuração, reports de bug e novidades de update acontecem no nosso [**Discord**](https://discord.gg/aDCgBbvRe5) oficial.
    *Esta documentação é mantida atualizada para te dar a melhor experiência de setup do GreatCosmetics no seu servidor.*
