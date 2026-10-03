# Painel Gmail — Organizar com IA + Agir nos e-mails

**Objetivo:** Acrescentar ao artefato "Caixa Gmail ao Vivo" botões que executam **uma ação por
clique** nos e-mails (lido/não lido, estrela, importante, marcadores, spam, arquivar, lixeira) e
ferramentas de **organização com IA** (classificar, sugerir marcadores, limpeza em massa, resumir
conversa, extrair dados).

**Tech Stack:** HTML + CSS + JavaScript (módulos ES), capabilities `mcp` (Gmail) e `sample` (Claude).

**Criado em:** 2026-10-03 17:55
**Concluído em:** —
**Tempo decorrido:** —

**Link do artefato (mantido):** https://claude.ai/artifact/6EVFxPcah16vM46FLGCG6g

---

## 📜 Regras do painel (uma ação por botão)

### A. Agir nos e-mails

| # | Regra / Botão | O que faz no Gmail | Ferramenta | Desfazer |
|---|---------------|--------------------|------------|----------|
| A1 | **Marcar como lido** | Remove o rótulo `UNREAD` da conversa | `unlabel_thread` | A2 |
| A2 | **Marcar como não lido** | Adiciona `UNREAD` | `label_thread` | A1 |
| A3 | **Estrela** / **Tirar estrela** | Adiciona / remove `STARRED` | `label_thread` / `unlabel_thread` | botão inverso |
| A4 | **Importante** / **Não importante** | Adiciona / remove `IMPORTANT` | `label_thread` / `unlabel_thread` | botão inverso |
| A5 | **Aplicar marcador…** | Escolhe um marcador existente e aplica | `list_labels` + `label_thread` | A6 |
| A6 | **Remover marcador…** | Tira um marcador da conversa | `unlabel_thread` | A5 |
| A7 | **Criar marcador** | Cria marcador novo (ex.: Banco, Escola, Boletos) com cor | `create_label` | — (apagar pelo Gmail) |
| A8 | **Marcar como spam** | Só quando for o caso: pede confirmação no painel antes | `mark_thread_spam` | A9 |
| A9 | **Não é spam** | Tira do spam (filtro "Spam") | `unmark_thread_spam` | A8 |
| A10 | **Arquivar** | Remove `INBOX` (sai da caixa de entrada, não apaga) | `unlabel_thread` | "Desfazer" (devolve `INBOX`) |
| A11 | **Lixeira** | Move para a lixeira (recuperável por 30 dias), com confirmação | `trash_thread` | "Desfazer" (`untrash_thread`) |

**Como as ações são feitas:**
- Cada e-mail tem uma **caixa de seleção**. Há **"Selecionar todos"** e **"Limpar seleção"**.
- A **barra de ações** aparece quando há seleção; cada botão faz **uma única ação** em todos os
  selecionados (uma conversa por vez, com progresso "3 de 12…").
- Ao abrir um e-mail, os mesmos botões aparecem só para ele.
- Ações de risco (**spam**, **lixeira**, qualquer ação em **mais de 10** e-mails) pedem confirmação
  dentro do painel (o artefato não aceita `confirm()`).
- Após cada ação: aviso "Feito: 12 e-mails marcados como lidos · Desfazer" e lista atualizada.
- **Nunca** apaga definitivamente (não existe botão de esvaziar lixeira).

### B. Filtros

| # | Filtro | Consulta Gmail |
|---|--------|----------------|
| B1 | Todos | (sem filtro; exclui spam/lixeira) |
| B2 | Não lidos | `is:unread` |
| B3 | Importantes | `is:important` |
| B4 | Com estrela | `is:starred` |
| B5 | Caixa de entrada | `in:inbox` |
| B6 | Spam | `in:spam` (para usar "Não é spam") |
| B7 | Por marcador | seletor com os seus marcadores (`label:<id>`) |
| B8 | Por categoria da IA | chips Urgente · Responder · Informativo · Promoção · Possível spam (depois de "Classificar") |
| B9 | Busca livre | sintaxe do Gmail (`from:`, `has:attachment`, `newer_than:7d`…) |

### C. Organizar com IA (cada botão = uma chamada ao Claude, só quando você clica)

| # | Botão | O que faz |
|---|-------|-----------|
| C1 | **Classificar** | Claude classifica os e-mails exibidos em Urgente · Responder · Informativo · Promoção · Possível spam e mostra chips coloridos na lista (guardado no seu navegador) |
| C2 | **Sugerir marcadores** | Claude sugere um marcador para cada e-mail (usa os seus, ou propõe novo como Banco/Escola/Boletos). Cada sugestão tem botão **Aplicar**; e há **Aplicar todas as sugestões** (cria os marcadores que faltam), com confirmação |
| C3 | **Limpeza em massa** | Claude aponta newsletters/promoções antigas; elas ficam pré-selecionadas para você decidir **Arquivar** ou **Lixeira** (A10/A11) |
| C4 | **Resumir conversa** | No e-mail aberto: lê a conversa inteira e resume decisões, pedidos e prazos |
| C5 | **Extrair dados** | Dos e-mails exibidos: boletos (valor, vencimento), rastreios, datas de reunião/prova — em tabela |
| C6 | **Resumir** (já existe) | Resumo geral por prioridade |

**Regras de segurança da IA:**
- A IA **só sugere**; nada muda no Gmail sem você clicar no botão da ação.
- "Possível spam" é só uma sugestão — marcar como spam continua exigindo A8 + confirmação.
- O conteúdo dos e-mails é tratado como dado (instruções dentro dos e-mails são ignoradas).
- Cada chamada gasta o seu uso do Claude.

---

## Arquivos previstos

O painel passa de ~860 linhas e ultrapassaria o limite de 1000 → divide-se por responsabilidade:

| Arquivo | Responsabilidade |
|---------|------------------|
| `artefato/painel-emails.html` | Estrutura da página (modificar) |
| `artefato/estilos.css` | Estilos e tokens de tema (novo; sai do HTML) |
| `artefato/js/constantes.js` | Constantes, rótulos, mensagens, filtros |
| `artefato/js/gmail-repositorio.js` | Chamadas ao conector Gmail (ler, rotular, spam, lixeira, marcadores) |
| `artefato/js/ia-servico.js` | Pedidos ao Claude (classificar, sugerir, limpeza, resumir, extrair) |
| `artefato/js/estado.js` | Estado do painel + seleção + classificações (localStorage) |
| `artefato/js/visao-lista.js` | Desenho da lista, chips, detalhe do e-mail |
| `artefato/js/visao-acoes.js` | Barra de ações, confirmações, aviso com "Desfazer" |
| `artefato/js/visao-ia.js` | Painéis de resultado da IA (sugestões, tabela de dados) |
| `artefato/js/principal.js` | Inicialização e ligação dos eventos |
| `README.md` | Atualizar com as novas regras |

## Riscos

| Risco | Mitigação |
|-------|-----------|
| Ações alteram o Gmail de verdade | Uma ação por clique, confirmação para spam/lixeira/lote >10, "Desfazer" |
| Muitas chamadas em lote (ex.: 50 e-mails) | Executa uma por vez, mostra progresso, para no primeiro erro de autorização |
| Falha no meio do lote | Relata quantas foram feitas e quais falharam; não repete escrita automaticamente |
| Classificação da IA errada | Só sugestão; você decide |
| Módulos ES em arquivos separados | Publicados juntos via `files`; checagem com `node --check` |
| Novas permissões | Na 1ª ação o claude.ai pede para liberar as novas ferramentas do Gmail |

---

## Status Geral

| Passo | Descrição | Status | Criado em | Concluído em | Tempo decorrido |
|-------|-----------|--------|-----------|--------------|-----------------|
| 1 | Separar CSS e constantes | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 2 | Repositório Gmail (escritas + marcadores) | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 3 | Estado + seleção múltipla | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 4 | Barra de ações A1–A11 + confirmações + Desfazer | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 5 | Filtros B1–B9 | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 6 | IA C1–C5 | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 7 | `node --check` em todos os módulos | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 8 | Republicar no mesmo link (novas ferramentas no manifesto) | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 9 | Atualizar README | ⬜ Pendente | 2026-10-03 17:55 | — | — |
| 10 | Commit + graphify | ⬜ Pendente | 2026-10-03 17:55 | — | — |

**Manifesto do conector (passo 8):** `search_threads`, `get_thread`, `list_labels`, `create_label`,
`label_thread`, `unlabel_thread`, `mark_thread_spam`, `unmark_thread_spam`, `trash_thread`,
`untrash_thread`.

**Verificação (passo 7):**

```powershell
Get-ChildItem artefato\js\*.js | ForEach-Object { Copy-Item $_ "$env:TEMP\$($_.BaseName).mjs"; node --check "$env:TEMP\$($_.BaseName).mjs" }
```

Esperado: nenhuma saída de erro. Validação visual fica com você no claude.ai (regra: não abrir navegador).

---

## Resultado final

—
