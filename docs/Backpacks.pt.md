# **Mochilas**

---

Uma **mochila** é qualquer cosmético com `isBackpack` habilitado. Ela renderiza no slot `BACK` do jogador como um cosmético normal **e** funciona como armazenamento privado de itens.

---

## **Configurando uma**

No editor de cosmético do [Dev Studio](Dev Studio.md), seção **Backpack**:

| Campo | Significado |
| :--- | :--- |
| **É Mochila?** | Liga o comportamento de armazenamento. |
| **Linhas da Mochila** | Linhas de baú, `1`–`6` (9 slots cada). |
| **Nome da Mochila** | Título MiniMessage mostrado no topo do GUI do baú. |

Modelo, slot (`BACK`), atributos e sons são configurados como qualquer outro cosmético — uma mochila também pode dar armadura, voo, efeitos, bônus de Lure, etc.

---

## **Abrindo**

* O jogador precisa ter o cosmético de mochila **equipado**.
* Aperte a tecla de mochila (padrão **`B`**), ou vincule em **Opções → Controles → GreatCosmetics**.
* Se o jogador usa **várias** mochilas, um pequeno seletor aparece primeiro.

---

## **Armazenamento & segurança**

* O conteúdo é salvo no banco **a cada mudança**, não só no fechamento — um crash não perde itens.
* O conteúdo é por jogador e por cosmético-mochila. Remover o cosmético de um jogador **não** apaga os itens guardados — devolver o cosmético traz eles de volta.

---

## **Sons**

Defina um **Backpack Sound** (com volume / pitch) na seção de Sons do cosmético pra tocar um som quando a mochila abre.
