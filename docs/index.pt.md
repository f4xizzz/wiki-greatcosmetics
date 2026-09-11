# **Introdução**

---

## **Bem-vindo ao GreatCosmetics**

O **GreatCosmetics** é um framework completo de cosméticos para servidores **Fabric** `1.21.1` (NeoForge em testes). Ele dá aos seus jogadores um *Avatar Studio* 3D para escolher e equipar cosméticos em nove slots virtuais do corpo, além de tags de chat, mochilas de armazenamento e efeitos de partícula — tudo editável **dentro do jogo**, sem reiniciar, pelo **Dev Studio** embutido.

Ele precisa **só da Fabric API**. Adicione o **[Cobblemon](Dependencies.md)** e destrava as skins de Pokémon, a aba Party e o sistema de bônus *Lure* do Cobblemon; adicione o **LuckPerms** pra slots com tier de permissão e tags de chat automáticas por grupo. Sem nenhum dos dois, o mod ainda roda e todo recurso não-Pokémon funciona.

Todo texto que o mod mostra (menus, chat, nomes de item) fica em arquivos JSON editáveis e é renderizado com **MiniMessage**, então você controla o idioma, as cores e a formatação sem mexer no código.

---

!!! warning "O mod não vem com nenhuma model de cosmético"
    O GreatCosmetics é o **framework** — o guarda-roupa, os slots, o Dev Studio, os efeitos, a rede. Ele **não** vem com uma biblioteca de cosméticos. De fábrica você só ganha alguns **exemplos** pequenos embutidos (pode deixar e usar no seu servidor numa boa, sem pegadinha), não um pacote de conteúdo.
    
    **Todo cosmético mostrado no vídeo de showcase do mod foi feito à parte e não vem junto com o mod.** Pra encher o guarda-roupa do seu servidor você precisa de models/texturas de verdade, adquiridas do jeito que preferir: pacotes de model vendidos (ou que ainda vão ser vendidos) no **Discord oficial da SaSDevelopment**, qualquer outra fonte de model, ou até armadura de outros mods reskinada e virada [Cosmético de Armadura](Armor Cosmetics.md). Veja [Criando Modelos & Texturas](Making Models.md) se você (ou seu artista) quiser montar as suas do zero.

---

## **Principais Recursos**

* **Avatar Studio 3D (`/wardrobe`):** uma prévia 3D giratória do jogador onde os cosméticos são equipados com um clique, organizados por categoria e pesquisáveis.
* **Nove slots virtuais:** `HEAD, FACE, NECK, CHEST, BACK, WAIST, LEGS, FEET, HAND` — independentes da armadura real do jogador, com limites por slot e por tipo e tiers de permissão.
* **Modelos 3D personalizados:** cosméticos renderizam como ícone chapado (Custom Model Data) **ou** como modelo **GeckoLib** animado completo, posicionado por parte com um gizmo 3D dentro do jogo. Ver [Criando Modelos & Texturas](Making Models.md).
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

O GreatCosmetics foi totalmente projetado e programado pelo **F4xizzz**, da **SaSDevelopment** — o mod Fabric/Java e o backend de licenciamento em Node.js.

---

!!! info "Comunidade Oficial"
    Dúvidas de configuração, reports de bug e novidades de update acontecem no nosso [**Discord**](https://discord.gg/GbbbNvQG3N) oficial.
    *Esta documentação é mantida atualizada para te dar a melhor experiência de setup do GreatCosmetics no seu servidor.*
