# **Licença & Ativação**

---

O GreatCosmetics é um mod pago. Num **servidor dedicado** ele fica travado até você ativar uma chave de licença; a chave é vinculada permanentemente ao IP do servidor por um backend assinado.

**Singleplayer e mundos LAN integrados estão sempre ativos** — sem chave, sem checagem de internet.

---

## **Ativando**

1. Compre uma chave no nosso [Discord](https://discord.gg/aDCgBbvRe5) — você recebe uma chave `GREATCOSMETICS-XXXX-XXXX` após o pagamento.
2. Entre no seu servidor como operador de verdade.
3. Rode:

    `/gc activation GREATCOSMETICS-XXXX-XXXX`

Ao dar certo o servidor grava `config/greatcosmetics/license.json` e destrava tudo. Esse arquivo é verificado (offline, via assinatura RSA) a cada boot e revalidado contra o backend a cada 4 horas.

!!! warning "Um IP por chave"
    O backend vincula a chave ao **primeiro IP** que a ativar. Você não pode mover uma chave pra um IP novo nem compartilhar. Fale com o suporte no Discord pra resetar uma chave que você legitimamente precisa migrar.

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
| `GREATCOSMETICS-XXXX-XXXX` | Chave normal. Travada por IP, integridade do jar checada. Vitalícia, salvo se emitida como temporária. |
| `GREATCOSMETICS-XXXX-XXXX` *(temporária)* | Igual, mas expira numa data definida; o mod se trava quando a data passa. |
| `GREATCOSMETICS-DEV-XXXX-XXXX` | Chave de desenvolvedor. **Sem trava de IP, sem checagem de hash do jar.** Pros seus próprios ambientes de teste. |

---

## **`license.json`**

```json
{
  "license_key": "GREATCOSMETICS-XXXX-XXXX",
  "expires_at": -1,
  "signature": "assinatura-RSA-em-base64"
}
```

**Não** edite — a `signature` é verificada contra a chave pública embutida no mod a cada startup. Uma assinatura adulterada trava o mod. Não commite esse arquivo no controle de versão; ele é por servidor.

---

## **Resolvendo problemas de ativação**

| Sintoma | Causa / solução |
| :--- | :--- |
| "Activation failed. Invalid key, or bound to another IP." | Chave já usada em outro IP, revogada, ou digitada errado. |
| A ativação trava e falha na primeira tentativa | O backend estava dormindo (cold start ~30–60 s). Rode o comando de novo. |
| "Integrity check failed. Adulterated JAR." | O hash do seu jar não está registrado pra essa release ainda — use uma chave `-DEV-`, ou peça ao suporte pra registrar o hash da release. |
| Funciona, depois trava algumas horas depois | Chave temporária expirou, ou a revalidação de 4h falhou (chave revogada / servidor offline). |
| Log diz "possible illegal mixin injection … Locking the mod" | Outro mod está mexendo nas classes de licença. O mod se trava (o servidor continua rodando). Remova o mod ofensor ou fale com o suporte. |
