# STATUS — Caixa Gmail ao Vivo

Andamento do projeto por etapas. Cada item é atualizado assim que é finalizado.
Legenda: ⬜ Pendente · 🔄 Em progresso · ✅ Concluído · ⛔ Bloqueado

**Artefato:** https://claude.ai/artifact/6EVFxPcah16vM46FLGCG6g
**Regras:** [CLAUDE.md](CLAUDE.md) · **Planos:** [docs/](docs/)

---

## Etapa 1 — Painel de leitura (2026-10-03)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 1.1 | Listar todos os e-mails (50 por página + Carregar mais) | ✅ Concluído | 2026-10-03 17:45 |
| 1.2 | Atualização automática a cada 2 h | ✅ Concluído | 2026-10-03 17:45 |
| 1.3 | Botão Atualizar agora | ✅ Concluído | 2026-10-03 17:45 |
| 1.4 | Busca + filtros Todos / Não lidos / Importantes | ✅ Concluído | 2026-10-03 17:45 |
| 1.5 | Abrir e-mail (texto) + Abrir no Gmail | ✅ Concluído | 2026-10-03 17:45 |
| 1.6 | Resumir com IA | ✅ Concluído | 2026-10-03 17:45 |
| 1.7 | Publicação do artefato | ✅ Concluído | 2026-10-03 17:45 |

## Etapa 2 — Regras e documentação

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 2.1 | Plano `docs/painel-organizar-com-ia-e-acoes.md` | ✅ Concluído | 2026-10-03 17:55 |
| 2.2 | `CLAUDE.md` do projeto com as regras A, B, C, D | ✅ Concluído | 2026-10-03 18:05 |
| 2.3 | `STATUS.md` (este arquivo) | ✅ Concluído | 2026-10-03 18:10 |

## Etapa 3 — Estrutura do código

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 3.1 | Separar CSS em `artefato/estilos.css` | ⬜ Pendente | — |
| 3.2 | Constantes em `artefato/js/constantes.js` | ⬜ Pendente | — |
| 3.3 | Repositório Gmail `artefato/js/gmail-repositorio.js` | ⬜ Pendente | — |
| 3.4 | Estado + seleção `artefato/js/estado.js` | ⬜ Pendente | — |

## Etapa 4 — Agir nos e-mails (A1–A11)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 4.1 | Seleção múltipla (caixas, Selecionar todos, Limpar) | ⬜ Pendente | — |
| 4.2 | A1/A2 Lido / Não lido | ⬜ Pendente | — |
| 4.3 | A3 Estrela · A4 Importante | ⬜ Pendente | — |
| 4.4 | A5/A6 Aplicar / Remover marcador · A7 Criar marcador | ⬜ Pendente | — |
| 4.5 | A8/A9 Spam / Não é spam (com confirmação) | ⬜ Pendente | — |
| 4.6 | A10 Arquivar · A11 Lixeira (com confirmação) | ⬜ Pendente | — |
| 4.7 | Confirmação na página + progresso + Desfazer | ⬜ Pendente | — |

## Etapa 5 — Filtros (B1–B9)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 5.1 | Com estrela · Caixa de entrada · Spam | ⬜ Pendente | — |
| 5.2 | Por marcador | ⬜ Pendente | — |
| 5.3 | Por categoria da IA | ⬜ Pendente | — |

## Etapa 6 — Organizar com IA (C1–C6)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 6.1 | C1 Classificar | ⬜ Pendente | — |
| 6.2 | C2 Sugerir marcadores (+ Aplicar / Aplicar todas) | ⬜ Pendente | — |
| 6.3 | C3 Limpeza em massa | ⬜ Pendente | — |
| 6.4 | C4 Resumir conversa | ⬜ Pendente | — |
| 6.5 | C5 Extrair dados | ⬜ Pendente | — |
| 6.6 | C6 Resumir (migrado para o painel de IA) | ⬜ Pendente | — |

## Etapa 7 — Entrega

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 7.1 | `node --check` em todos os módulos | ⬜ Pendente | — |
| 7.2 | Republicar no mesmo link (manifesto com novas ferramentas) | ⬜ Pendente | — |
| 7.3 | README atualizado | ⬜ Pendente | — |
| 7.4 | Commit + graphify | ⬜ Pendente | — |
| 7.5 | Teste no claude.ai pelo usuário | ⬜ Pendente | — |
