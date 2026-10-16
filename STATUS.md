# STATUS — Caixa Gmail ao Vivo

**Objetivo:** Ler, organizar e agir nos e-mails do Gmail num painel do claude.ai (conector Gmail +
IA do Claude), atualizado a cada 2 horas, para ganhar tempo na caixa de entrada.
**Partes interessadas:** Gelvazio (decide, aprova e usa) · Claude (executa)
**Links:** [Regras](CLAUDE.md) · [Planos](docs/) ·
[Artefato](https://claude.ai/artifact/6EVFxPcah16vM46FLGCG6g)
**Próximo passo:** aguardando o "sim" do usuário para executar a Etapa 3 (item 3.1).

Legenda: ⬜ Pendente · 🔄 Em progresso · ✅ Concluído · ⛔ Bloqueado

## Escopo

- **Entra:** leitura, filtros, ações A1–A11 (lido, estrela, importante, marcadores, spam, arquivar,
  lixeira), organização com IA C1–C6, atualização automática de 2 h.
- **Não entra:** enviar e-mail, apagar definitivamente, atualização com a página fechada, WhatsApp.
- **Critério de pronto:** sintaxe validada (`node --check`), artefato republicado no mesmo link e
  testado pelo usuário no claude.ai.
- **Premissas e restrições:** conector Gmail conectado; não abrir navegador para validar; não
  escrever testes; arquivos ≤ 1000 linhas e funções ≤ 45 linhas.

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
| 2.4 | Regras de gestão de projetos no CLAUDE.md global + STATUS.md no modelo | ✅ Concluído | 2026-10-03 18:18 |

## Etapa 3 — Estrutura do código

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 3.1 | Separar CSS em `artefato/estilos.css` · `MEDIO · effort medium` | ⬜ Pendente | — |
| 3.2 | Constantes em `artefato/js/constantes.js` · `MEDIO · effort medium` | ⬜ Pendente | — |
| 3.3 | Repositório Gmail `artefato/js/gmail-repositorio.js` · `MEDIO · effort medium` | ⬜ Pendente | — |
| 3.4 | Estado + seleção `artefato/js/estado.js` · `MEDIO · effort medium` | ⬜ Pendente | — |

## Etapa 4 — Agir nos e-mails (A1–A11)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 4.1 | Seleção múltipla (caixas, Selecionar todos, Limpar) · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.2 | A1/A2 Lido / Não lido · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.3 | A3 Estrela · A4 Importante · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.4 | A5/A6 Aplicar / Remover marcador · A7 Criar marcador · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.5 | A8/A9 Spam / Não é spam (com confirmação) · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.6 | A10 Arquivar · A11 Lixeira (com confirmação) · `MEDIO · effort medium` | ⬜ Pendente | — |
| 4.7 | Confirmação na página + progresso + Desfazer · `MEDIO · effort medium` | ⬜ Pendente | — |

## Etapa 5 — Filtros (B1–B9)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 5.1 | Com estrela · Caixa de entrada · Spam · `MEDIO · effort medium` | ⬜ Pendente | — |
| 5.2 | Por marcador · `MEDIO · effort medium` | ⬜ Pendente | — |
| 5.3 | Por categoria da IA · `MEDIO · effort medium` | ⬜ Pendente | — |

## Etapa 6 — Organizar com IA (C1–C6)

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 6.1 | C1 Classificar · `MEDIO · effort medium` | ⬜ Pendente | — |
| 6.2 | C2 Sugerir marcadores (+ Aplicar / Aplicar todas) · `MEDIO · effort medium` | ⬜ Pendente | — |
| 6.3 | C3 Limpeza em massa · `PESADO · effort high` | ⬜ Pendente | — |
| 6.4 | C4 Resumir conversa · `MEDIO · effort medium` | ⬜ Pendente | — |
| 6.5 | C5 Extrair dados · `MEDIO · effort medium` | ⬜ Pendente | — |
| 6.6 | C6 Resumir (migrado para o painel de IA) · `MEDIO · effort medium` | ⬜ Pendente | — |

## Etapa 7 — Entrega

| Item | Descrição | Status | Concluído em |
|------|-----------|--------|--------------|
| 7.1 | `node --check` em todos os módulos · `MEDIO · effort medium` | ⬜ Pendente | — |
| 7.2 | Republicar no mesmo link (manifesto com novas ferramentas) · `MEDIO · effort medium` | ⬜ Pendente | — |
| 7.3 | README atualizado · `LEVE · effort low` | ⬜ Pendente | — |
| 7.4 | Commit + graphify · `LEVE · effort low` | ⬜ Pendente | — |
| 7.5 | Teste no claude.ai pelo usuário · `LEVE · effort low` | ⬜ Pendente | — |

---

## Riscos

| Risco | Chance | Impacto | Plano B | Situação |
|-------|--------|---------|---------|----------|
| Ações alteram o Gmail de verdade | Média | Alto | Confirmação para spam/lixeira/lote > 10 + Desfazer | Aberto |
| Conector Gmail desconectar | Média | Alto | Aviso "Reconecte o Gmail" no painel | Ocorreu em 2026-10-03, resolvido |
| Falha no meio de um lote | Baixa | Médio | Relatar feitos/falhos, sem repetir escrita sozinho | Aberto |
| IA classificar errado | Média | Baixo | IA só sugere; usuário decide | Aberto |
| Módulos JS em arquivos separados não carregarem | Baixa | Alto | `node --check` + teste do usuário; voltar a arquivo único | Aberto |

## Bloqueios

| Data | Item | Motivo | O que destrava | Resolvido em |
|------|------|--------|----------------|--------------|
| 2026-10-03 | 1.1 | Conector Gmail com conexão invalidada | Usuário reconectar no claude.ai | 2026-10-03 |

## Registro de decisões

| Data | Decisão | Quem | Por quê |
|------|---------|------|---------|
| 2026-10-03 | Usar Artefato + conector Gmail do Claude (sem servidor) | Gelvazio | Pedido do usuário |
| 2026-10-03 | Mostrar todos os e-mails, 50 por página | Gelvazio | Pedido do usuário |
| 2026-10-03 | Botão Resumir com IA só ao clicar | Gelvazio | Evitar gasto de uso |
| 2026-10-03 | Plano da Etapa 1 aprovado | Gelvazio | Respondeu "SIM" |
| 2026-10-03 | Acrescentar ações A1–A11 e IA C1–C6, uma ação por botão | Gelvazio | Pedido do usuário |
| 2026-10-03 | Dividir o código em CSS + módulos JS | Claude | Passaria de 1000 linhas |

## Pendências (ficou para depois)

| Item | Motivo | Quando retomar |
|------|--------|----------------|
| Rascunho de resposta com IA | Não pedido nesta fase | Quando o usuário pedir |
| Integração com Google Agenda | Não pedido nesta fase | Quando o usuário pedir |
| Aviso pelo WhatsApp / atualização com página fechada | Exige automação fora do artefato | Projeto AUTOMATIZACAO-WHATSAPP |

## Lições aprendidas

| Data | O que aconteceu | Lição / nova regra |
|------|-----------------|--------------------|
| 2026-10-03 | Sessão poderia cair no meio da tarefa | Regra global: `STATUS.md` em toda tarefa, retomar de onde parou |
| 2026-10-03 | Faltavam decisões, riscos e lições no acompanhamento | Regra global: modelo de gestão de projetos no `STATUS.md` |
