# Painel de Leitura de E-mails (Artefato Claude + conector Gmail)

**Objetivo:** Publicar um Artefato no claude.ai que lê os e-mails do Gmail pelo conector do Claude,
atualiza sozinho a cada 2 horas, tem botão "Atualizar agora" e botão "Resumir" (resumo com IA).

**Tech Stack:** HTML + CSS + JavaScript (página única de Artefato), capability `mcp`
(conector **Gmail**, ferramentas `search_threads` e `get_thread`), capability `sample` (resumo com
Claude). Sem servidor, sem banco, sem dependências externas.

**Criado em:** 2026-10-03 17:21
**Concluído em:** 2026-10-03 17:56
**Tempo decorrido:** ~25 min

---

## Escopo

- Listar **todos** os e-mails (todas as pastas, exceto spam/lixeira — padrão do Gmail), mais
  recentes primeiro, 50 por página, com botão **"Carregar mais"** (paginação por `pageToken`).
- Cada item: remetente, assunto, trecho, data, marcação de **não lido**, link "Abrir no Gmail".
- Campo de **busca** (sintaxe do Gmail) e filtros rápidos: Todos · Não lidos · Importantes.
- **Atualização automática a cada 2 h** (`watchTool` com `refetchInterval: 7200000`).
- Botão **"Atualizar agora"** (`callTool` com `cache: {refresh: true}`).
- Indicador **"Atualizado às HH:MM"** (a partir de `cache.storedAt`) e "próxima atualização".
- Botão **"Resumir"**: envia remetente/assunto/trecho dos e-mails exibidos ao Claude (`sample`) e
  mostra um resumo com prioridades. Só roda quando você clica.
- Tratamento de erros por código (reconectar Gmail, conector ausente, indisponível etc.).
- Tema claro/escuro, layout responsivo (celular).

**Fora do escopo:** responder/apagar/marcar e-mails (somente leitura), WhatsApp, testes automáticos.

## Arquivos previstos

| Arquivo | Ação |
|---------|------|
| `C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS\docs\painel-leitura-emails-artefato.md` | Este plano |
| `C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS\artefato\painel-emails.html` | Página do Artefato (HTML + CSS + JS, estrutura separada por seções e constantes no topo) |
| `C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS\README.md` | Como abrir/republicar o painel |

## Riscos e dependências

| Risco | Mitigação |
|-------|-----------|
| Conector Gmail desconectar no futuro | ✅ Reconectado em 2026-10-03; o painel mostra aviso "Reconecte o Gmail" se acontecer de novo |
| A atualização de 2 h só ocorre **com a página aberta** (o polling pausa com a aba oculta e recupera ao voltar) | Indicado na própria página; ao abrir, sempre busca se o dado tiver passado do prazo |
| Formato da resposta do `search_threads` | ✅ Confirmado em chamada real: `{nextPageToken, resultCountEstimate, threads[{id, messageCount, viewUrl, messages[{sender, subject, snippet, date, labelIds, viewUrl}]}]}` |
| "Todos" = até 50 por página (limite da API) | Botão "Carregar mais" |
| Resumo com IA consome seu uso do Claude | Só ao clicar em "Resumir" |
| Conteúdo dos e-mails é dado não confiável | Renderizado com `textContent` (sem HTML injetado) |
| Página com `mcp` fica privada (não pode ser pública) | Artefato privado por padrão |

---

## Status Geral

| Passo | Descrição | Status | Criado em | Concluído em | Tempo decorrido |
|-------|-----------|--------|-----------|--------------|-----------------|
| 1 | Criar pasta `docs/` + `git init` | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:21 | 00:30 |
| 2 | Criar `artefato/painel-emails.html` (estrutura + estilos) | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 3 | Implementar leitura Gmail (`watchTool` 2 h + "Atualizar agora" + paginação + filtros) | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 4 | Implementar botão "Resumir" (`sample`) | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 5 | Tratamento de erros por código | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 6 | Checar sintaxe do JS com `node --check` | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 7 | Publicar Artefato (`capabilities: mcp Gmail + sample`) | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 8 | Criar `README.md` | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |
| 9 | Commit | ✅ Concluído | 2026-10-03 17:21 | 2026-10-03 17:56 | — |

---

### Passo 1: Criar pasta `docs/` + `git init`

**Status:** ✅ Concluído (autorizado pelo usuário)

---

### Passo 2: Estrutura e estilos

**Status:** ✅ Concluído

**Arquivo:** Criar `C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS\artefato\painel-emails.html`

**Ação:** Cabeçalho (título, "Atualizado às", botões Atualizar/Resumir), barra de busca e filtros,
lista de e-mails, área de resumo, rodapé com "Carregar mais". Tokens de cor em `:root` com modo
escuro. Nomes de funções/classes em português.

**Verificação:** leitura do código (sem navegador, conforme regra do usuário).

---

### Passo 3: Leitura do Gmail

**Status:** ✅ Concluído

**Ação:** `const mcp = await claude.use("mcp")`; `mcp.watchTool("Gmail", "search_threads",
{query, pageSize: 50}, tratarEvento, {refetchInterval: 7200000})`. "Atualizar agora" →
`mcp.callTool(..., {cache: {refresh: true}})`. Trocar filtro/busca → cancela o watch anterior e
registra um novo. "Carregar mais" → `callTool` com `pageToken`.

---

### Passo 4: Botão "Resumir"

**Status:** ✅ Concluído

**Ação:** `const sample = await claude.use("sample")`; monta a lista (remetente, assunto, trecho,
data) dos e-mails exibidos e pede resumo em português: urgentes, pedem resposta, informativos,
promoções. Resposta exibida em streaming (`onText`). Botão escondido se `sample` for `null`.

---

### Passo 5: Erros

**Status:** ✅ Concluído

**Ação:** mensagens específicas para `needs_reauth`, `server_not_connected`, `selection_required`,
`not_in_manifest`, `server_unavailable` (1 nova tentativa), `tool_error`, `not_granted`; dados
antigos continuam visíveis em erros transitórios.

---

### Passo 6: Checagem de sintaxe

**Status:** ✅ Concluído

**Verificação:**

```powershell
node --check C:\Users\gelva\AppData\Local\Temp\...\scratchpad\painel-emails.js
```

Esperado: sem saída (sintaxe válida). O script é extraído do HTML para um `.js` temporário.

---

### Passo 7: Publicar

**Status:** ✅ Concluído

**Ação:** `Artifact publish` com `capabilities: { mcp: { servers: [{ server: "Gmail", tools:
["search_threads", "get_thread"] }] }, sample: {} }`, ícone `mail`.

---

### Passo 8: README

**Status:** ✅ Concluído

**Arquivo:** Criar `C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS\README.md` (link do artefato, como
reconectar o Gmail, como republicar).

---

### Passo 9: Commit

**Status:** ✅ Concluído

```powershell
git -C C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS add .
git -C C:\fontes\AUTOMATIZACAO-LEITURA-EMAILS commit -m "Painel de leitura de e-mails (artefato + conector Gmail)"
```

---

## Resultado final

- Artefato publicado: https://claude.ai/artifact/6EVFxPcah16vM46FLGCG6g (privado)
- Capabilities: mcp (Gmail: search_threads, get_thread) + sample
- Sintaxe do JS validada com node --check
- Pendente: validação visual pelo usuário no claude.ai (regra: não abrir navegador)

