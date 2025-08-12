# n8n Bloco 1 — Telegram → Render 1

Este pacote inclui:
- `workflows/bloco1_telegram_render1.json` — workflow pronto para importar no n8n
- `render.yaml` — blueprint para deploy do n8n no Render
- `README.md` — instruções rápidas

## Pré-requisitos
1) **Render 1** ativo com rotas:
   - `POST /upload` (multipart: `file`, `userId`, `descricao`, `date`)
   - `GET /lista/:userId/:AAAA-MM`
2) **Token** do seu bot do Telegram
3) No n8n (após deploy):
   - Credencial **Telegram API**
   - (opcional) Credencial **HTTP Header Auth** se o Render 1 exigir Authorization
   - **Env var** `RENDER1_URL=https://miguel-render-1.onrender.com`

## Como importar
1. Abra o n8n → **Import** → carregue `workflows/bloco1_telegram_render1.json`.
2. Abra os nós Telegram e selecione sua credencial **Telegram API**.
3. No nó **HTTP Request** para upload, se seu Render 1 exigir token:
   - Selecione a credencial **HTTP Header Auth** com `Authorization: Bearer <seu_token>`
4. Ative o workflow e teste no Telegram:
   - `/ping`
   - Envie uma foto/PDF → deve responder **"🧾 Prontinho! Comprovante guardado."**
   - `/lista 2025-08` (ajuste o mês)

## Observações
- O nó HTTP de upload envia o **binário** recebido do Telegram (propriedade `data`) como `file` para o Render 1.
- Se sua versão do n8n não tiver `options.sendBinaryProperty`, ligue manualmente **Send Binary Data** na UI.
- Timezone sugerido: `America/Sao_Paulo`.
- O keep-alive fica a cargo do **n8n 3** (este pacote não inclui ping).