# Instruções para agentes de IA — projeto "Inscrições da Oficina"

Você é o agente de IA de um exercício de Spec Driven Development (SDD). A pessoa manda **um prompt por vez** e você
executa **só o que o prompt pede**. Siga este arquivo ao pé da letra.

## REGRA Nº 1 — Contexto mínimo: nada de skills, ferramentas extras ou arquivos a mais
- **Nunca use skills**, slash commands, comandos personalizados, "rules", agentes, subagentes, workflows, plugins, servidores MCP, busca na web ou documentação externa. Mesmo que estejam disponíveis ou sejam sugeridos pela ferramenta: ignore.
- **Nunca carregue na janela de contexto** nada além do que o prompt cita. Não leia a pasta inteira, não indexe o projeto, não abra `node_modules/`, `public/styles.css`, `public/components.html`, `public/fonts/`, `templates/` (a não ser que o prompt cite o template), nem os incrementos que o prompt não citou. Em `tests/`, leia só `tests/helpers.js` e escreva só o `tests/0N.test.js` do incremento, e só no P5.
- Os únicos arquivos que você lê são: `AGENTS.md` (este), `CONSTITUTION.md`, `DESIGN.md` (só no P4 e P5) e os arquivos listados no prompt. Nada mais.
- Não peça mais contexto. Se algo faltar, escolha a opção mais simples e registre em "Dúvidas resolvidas".
- Não use memória de conversas anteriores: cada prompt se resolve só com os arquivos citados.

## PASSO 0 — Antes de qualquer prompt, leia estes arquivos, nesta ordem
1. `CONSTITUTION.md` — regras fixas (stack, proibições, padrões). Se este arquivo e a constituição discordarem, a constituição vence.
2. `DESIGN.md` — receita da tela. Todo HTML da tela usa as classes daquele arquivo. Você NUNCA escreve CSS.
3. Os arquivos do incremento que o prompt citar, por exemplo `case/01-cadastro/spec.md`, `case/01-cadastro/plan.md`, `case/01-cadastro/tasks.md`.

## PASSO 1 — Descubra qual tipo de prompt recebeu
| Se o prompt pede para... | Tipo | Você cria/edita SOMENTE | Molde a seguir |
|---|---|---|---|
| listar arquivos / dizer o que `server.js` faz | P0 | nada | — |
| escrever `spec.md` | P1 | `case/0N-<nome>/spec.md` | `templates/spec.md` |
| escrever `plan.md` | P2 | `case/0N-<nome>/plan.md` | `templates/plan.md` |
| escrever `tasks.md` | P3 | `case/0N-<nome>/tasks.md` | `templates/tasks.md` |
| implementar as tarefas | P4 | `server.js`, `public/index.html`, `public/app.js` e marcar `[x]` em `tasks.md` | `DESIGN.md` para a tela |
| testar: criar testes e rodar `npm test` | P5 | `tests/0N.test.js` (um por incremento) e, se um teste falhar, `server.js` / `public/app.js` | `templates/tests.md` |

## PASSO 2 — Regras que valem para TODOS os tipos
- O arquivo que o prompt manda criar **já existe**? Então não escreva nada e responda só: `O arquivo <caminho> já existe. Nada foi alterado.`
- **Nunca** altere `spec.md`. Se a spec for ambígua, escolha a opção mais simples e registre na tabela "Dúvidas resolvidas" do `plan.md`.
- **Nunca** edite: `templates/`, `CONSTITUTION.md`, `DESIGN.md`, `AGENTS.md`, `public/styles.css`, `public/components.html`, `public/fonts/`.
- **Nunca** crie arquivos que o prompt não pediu (README, `.env`, config de lint, CI, pastas novas, etc.).
- **Nunca** instale dependência, mude a porta 3000, use TypeScript, bundler, framework de frontend ou banco de dados.
- **Nunca** rode `git`, apague arquivos ou mexa em `node_modules/`.
- **Nunca** use skills, slash commands, MCP, busca na web ou subagentes, e **nunca** leia arquivos que o prompt não citou (ver REGRA Nº 1).
- Cada tarefa (`tasks.md`) e cada decisão técnica (`plan.md`) cita a regra da spec que satisfaz, no formato `(R2)`.
- Limites: `spec.md` ≤ 60 linhas, `plan.md` ≤ 40 linhas, `tasks.md` ≤ 20 itens.
- Nomes de campos, rotas e variáveis em **inglês** (`name`, `email`, `/participants`). Textos que aparecem na tela em **português**.

## PASSO 3 — No P4 (implementar), faça exatamente isto
1. Leia `tasks.md` e execute as tarefas **na ordem**, uma por uma.
2. Backend em `server.js`: mantenha `module.exports = { app, resetData }` e o bloco `if (require.main === module)` no fim. Erros sempre `res.status(400|404|409).json({ error: 'mensagem' })`.
3. Tela em `public/index.html`: **não remova** o cabeçalho (`.bd-header`), o banner (`.bd-hero`) nem o rodapé (`.bd-footer`). Coloque o conteúdo novo **dentro de** `<main class="bd-content" id="app">`, copiando os blocos prontos de `DESIGN.md`.
4. Comportamento em `public/app.js`: use `fetch`, crie elementos com as classes de `DESIGN.md`, mostre o `error` da API em `#message`.
5. Mantenha tudo que já existia dos incrementos anteriores.
6. Marque `[x]` em cada tarefa concluída em `tasks.md`.

## PASSO 3b — No P5 (testar), faça exatamente isto
1. Leia `spec.md` e `plan.md` do incremento, `templates/tests.md` e `tests/helpers.js`. **Não** leia `server.js` nem `public/` para escrever os testes: o teste descreve a spec, não o código.
2. Se `tests/0N.test.js` **não existir**, crie-o copiando o esqueleto de `templates/tests.md`: um `test('C1: <título>', ...)` por cenário de aceite, na ordem da spec. Rota, método e código de status vêm do `plan.md`; mensagens vêm da spec, letra por letra.
3. O cenário "todos os cenários do incremento anterior continuam valendo" não vira `test()`: `npm test` já roda os arquivos anteriores.
4. Se `tests/0N.test.js` **já existir**, não o reescreva.
5. Rode `npm test`. Se algum teste falhar, corrija `server.js` ou `public/app.js` e rode de novo, até `fail 0`. **Nunca** altere o teste nem a spec para o teste passar. Nunca apague testes de incrementos anteriores.
6. Nunca instale framework de teste: só `node:test` e `node:assert/strict`, que já vêm no Node.

## PASSO 4 — Como responder
- Responda em **português**.
- **Grave os arquivos direto na pasta** (você sempre tem acesso a ela). Não cole o conteúdo na conversa.
- Depois de gravar, responda com **uma linha só**, neste formato:
  - `Arquivo criado: case/01-cadastro/plan.md`
  - `Arquivos alterados: server.js, public/index.html, public/app.js, case/01-cadastro/tasks.md`
- Nada de explicação, resumo, "aqui está", próximos passos ou perguntas de volta.
- Exceções: no P0 responda a linha pedida; no P5 responda `C1 PASSA`, `C2 FALHA` (uma linha por cenário, conforme o resultado de `npm test`) e depois a linha `Arquivos criados/alterados: tests/01.test.js, server.js`.

## Comandos do projeto
- `npm start` → sobe em `http://localhost:3000`. O servidor **não recarrega sozinho**; a pessoa faz `Ctrl+C` e `npm start`.
- `npm test` → roda todos os `tests/*.test.js` com `node:test`. Saída esperada no fim: `fail 0`.
