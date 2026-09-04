# **Licença & Ativação**

---

O GreatCosmetics é um mod pago. Num **servidor dedicado** ele fica travado até você ativar uma chave de licença. A chave é então vinculada ao servidor e validada contra o nosso backend.

**Singleplayer e mundos LAN integrados estão sempre ativos** — sem chave, sem checagem de internet.

---

## **Ativando**

1. Compre uma chave no nosso [Discord](https://discord.gg/aDCgBbvRe5) — você recebe uma chave `GREATCOSMETICS-XXXX-XXXX` após o pagamento.
2. Entre no seu servidor como operador de verdade.
3. Rode:

    `/gc activation GREATCOSMETICS-XXXX-XXXX`

Ao dar certo o servidor grava `config/GreatCosmetics/license.json` e destrava tudo. A licença é revalidada contra o backend a cada 4 horas.

!!! info "Um servidor por chave"
    Na primeira ativação a chave é vinculada àquela instância de servidor. O seu IP público pode mudar (IP dinâmico, troca de host) sem quebrar a ativação, mas a chave não funciona em um segundo servidor diferente ao mesmo tempo. Fale com o suporte no Discord pra migrar uma chave pra outra máquina.

!!! info "Queda do backend não te derruba"
    Se o backend ficar temporariamente fora do ar, um servidor já ativado continua rodando por um período de tolerância enquanto tenta de novo em segundo plano. Você só perde o acesso se a chave for realmente revogada ou expirar.

---

## **Enquanto sem licença**

Num servidor dedicado sem licença válida:

* Todo comando `/gc` e `/wardrobe` é bloqueado (os jogadores veem um aviso de "sem licença válida"), **exceto `/gc activation`**.
* Abrir o guarda-roupa, equipar cosméticos/tags/skins, mochilas e todas as ações do Dev Studio ficam bloqueadas.
* O mod ainda carrega — ele só não faz nada até ser ativado.

---

## **Tipos de chave**

| Formato | Comportamento |
| :--- | :--- |
| `GREATCOSMETICS-XXXX-XXXX` | Chave normal. Vinculada ao seu servidor. Vitalícia, salvo se emitida como temporária. |
| `GREATCOSMETICS-XXXX-XXXX` *(temporária)* | Igual, mas expira numa data definida; o mod se trava quando a data passa. |

---

## **`license.json`**

Gravado e gerenciado pelo mod. **Não** edite — um arquivo inválido simplesmente falha na verificação e o mod fica travado até você rodar `/gc activation` de novo. Não commite esse arquivo no controle de versão; ele é por servidor.

---

## **Resolvendo problemas de ativação**

| Sintoma | Causa / solução |
| :--- | :--- |
| "Activation failed. Invalid key, or bound to another server." | Chave já vinculada a outro servidor, revogada, ou digitada errado. |
| A ativação trava e falha na primeira tentativa | O backend estava dormindo (cold start ~30–60 s). Rode o comando de novo. |
| Funciona, depois trava | Chave temporária expirou, a chave foi revogada, ou o backend ficou fora do ar além do período de tolerância. |
