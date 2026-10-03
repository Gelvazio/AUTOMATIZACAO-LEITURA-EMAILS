# AUTOMATIZACAO-LEITURA-EMAILS

Painel **Caixa Gmail ao Vivo**: um Artefato do claude.ai que lê seus e-mails pelo conector Gmail do
Claude, atualiza sozinho a cada 2 horas e resume com IA.

**Link:** https://claude.ai/artifact/6EVFxPcah16vM46FLGCG6g (privado — só você abre)

## Como usar

1. Abra o link no claude.ai (navegador ou app do Claude).
2. Na primeira vez, permita o acesso ao **Gmail** quando o Claude pedir.
3. A lista mostra todos os e-mails (exceto spam/lixeira), 50 por vez — use **Carregar mais**.
4. Filtros: **Todos · Não lidos · Importantes**, ou busque com a sintaxe do Gmail
   (`from:banco`, `has:attachment`, `newer_than:2d`…) e tecle Enter.
5. Clique em um e-mail para ler o texto; **Abrir no Gmail ↗** leva à mensagem original.
6. **Atualizar agora** busca na hora; sozinho, o painel atualiza a cada 2 horas
   (somente com a página aberta — ao voltar à aba, ele recupera o atraso).
7. **Resumir** pede ao Claude um resumo por prioridade dos e-mails exibidos (gasta seu uso do Claude).

## Se aparecer "Reconecte o Gmail"

claude.ai → Configurações → Conectores → Gmail → Reconectar.

## Como alterar

Edite `artefato/painel-emails.html` e peça ao Claude para republicar no mesmo link
(`Artifact publish` com o mesmo arquivo, ou com `url` do link acima em outra conversa).

## Arquivos

| Caminho | Conteúdo |
|---------|----------|
| `artefato/painel-emails.html` | Página do painel (HTML + CSS + JS) |
| `docs/painel-leitura-emails-artefato.md` | Plano e status da tarefa |
