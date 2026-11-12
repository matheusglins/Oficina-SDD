# Constituição do projeto "Inscrições da Oficina"

Regras fixas. Valem para todos os incrementos. O agente lê este arquivo antes de qualquer tarefa.

## Stack (não negociável)
- Node.js >= 20. Única dependência: `express`. Porta 3000. `npm start` sobe tudo.
- Backend em `server.js`. Frontend estático em `public/index.html` + `public/app.js` (HTML + JS puro, sem build).
- Visual: `public/styles.css` é o design kit (identidade visual da Pitang) e **não é editado**. A tela usa só as classes de `DESIGN.md` / `public/components.html`.
- Dados em um array em memória dentro de `server.js`. Sem banco, sem arquivo, sem persistência.
- `server.js` exporta `{ app, resetData }` e só escuta a porta quando executado diretamente (`require.main === module`).

## O agente NUNCA
- instala outra dependência, muda a porta, cria TypeScript, bundler ou framework de frontend;
- escreve CSS (nem `<style>`, nem `style=""`, nem outro `.css`); monta a tela com as classes do design kit;
- usa skills, slash commands, MCP, busca na web, subagentes ou qualquer ferramenta além de ler/escrever os arquivos citados e rodar `npm test`;
- carrega na janela de contexto arquivos que o prompt não citou (nem `node_modules/`, nem `tests/`, nem `public/styles.css`, nem outros incrementos);
- altera a spec; se a spec for ambígua, escolhe a opção mais simples e registra em "Dúvidas resolvidas" do plano;
- explica o que fez em prosa longa: responde só com os arquivos pedidos.

## Padrões
- API JSON em `/participants`. Erros sempre `{ "error": "mensagem" }` com status HTTP adequado: 400 entrada inválida, 404 não encontrado, 409 conflito.
- Nomes de campos, rotas e variáveis em inglês; textos de tela em português.
- Cada tarefa cita a regra da spec que satisfaz (ex.: `R2`).
- Todo incremento termina com `tests/0N.test.js`: **um teste por cenário de aceite** da spec, com `node:test` nativo, rodável com `npm test`. O teste nasce da spec e do plano, não do código. `tests/helpers.js` não é editado.
- Teste que falha significa código errado: corrige-se `server.js`/`public/app.js`, nunca o teste nem a spec.
