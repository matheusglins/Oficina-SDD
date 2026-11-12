# Kit SDD — Inscrições da Oficina

**Spec Driven Development em uma frase:** você escreve *o quê* (a spec), revisa, e só então o agente de IA decide *o como* e escreve o código.
O código é consequência da spec, não o contrário. Funciona com qualquer agente, porque tudo é markdown e prompt.

## Os 4 artefatos
| Arquivo | O que é | Quem escreve |
|---|---|---|
| `CONSTITUTION.md` | Regras fixas do projeto (stack, proibições, padrões) | Pronto no kit |
| `case/0N-<nome>/spec.md` | **O quê**: regras de negócio e cenários de aceite | Você (ou o agente com P1, revisado por você) |
| `case/0N-<nome>/plan.md` | **Como**: endpoints, modelo, tela | Agente (P2), revisado por você |
| `case/0N-<nome>/tasks.md` | Passos pequenos e verificáveis | Agente (P3), revisado por você |
| `tests/0N.test.js` | Um teste por cenário de aceite da spec | Agente (P5), a partir da spec e do plano |

**Instruções base para qualquer agente:** `AGENTS.md` na raiz (padrão aberto lido por Codex, Cursor, Copilot, Kilo e outros).
`CLAUDE.md`, `GEMINI.md` e `.github/copilot-instructions.md` só apontam para ele. Não edite nenhum dos quatro.
Regra de contexto que eles impõem: **o agente não usa skills, slash commands, MCP, busca na web nem subagentes, e só lê os arquivos
que o prompt cita.** Se a sua ferramenta tiver skills ou MCP ligados, desligue antes de começar: cada um gasta cota e confunde o modelo.

**Visual pronto:** `public/styles.css` + `public/fonts/` + `DESIGN.md` são o design kit (identidade visual da Pitang, funciona offline). O agente monta a tela com essas classes
e não escreve CSS. Veja os componentes em `http://localhost:3000/components.html` depois do `npm start`.

## Setup (5 minutos)
1. `node -v` → precisa ser 20 ou maior.
2. Nesta pasta: `npm install` e depois `npm start`.
3. Abra `http://localhost:3000`. Deve aparecer "Esqueleto pronto" abaixo do cabeçalho com a logo da Pitang e do banner rosado.
4. Abra a pasta no VS Code (File > Open Folder; aceite "confiar nos autores"), abra seu agente de IA em modo agente e rode o prompt **P0** de `PROMPTS.md`.

## O ciclo (repita por incremento)
```
briefing → P1 (ou escrever à mão) → REVISAR spec → P2 → REVISAR plano → P3 → REVISAR tarefas → P4 → Ctrl+C e npm start → conferir na tela → P5 (testes: um por cenário, npm test fail 0)
```
Três revisões humanas obrigatórias. Nunca rode o P4 sem ter lido o plano. O P5 fecha o incremento: gera `tests/0N.test.js` a partir dos cenários de aceite e roda `npm test`.
**Os prompts já vêm preenchidos por incremento em `PROMPTS.md`: copie e cole, não troque nada.** Siga a seção do incremento em que você está. A pasta `templates/` são moldes vazios de propósito; não edite.
**O servidor não recarrega sozinho:** depois de qualquer mudança no `server.js`, reinicie o servidor. A receita passo a passo
(onde clicar, o que apertar) está no topo de `PROMPTS.md`, em "Como reiniciar o servidor".

O case está em `case/briefing.md`. A spec do incremento 1 já vem pronta em `case/01-cadastro/spec.md` como exemplo: comece por ela e vá direto ao P2 (não existe P1 no incremento 1).

## Onde colar os prompts
Qualquer agente que **lê e escreve a pasta** (modo agente). Chat web não serve: ele não enxerga os arquivos.

| Agente | Observação |
|---|---|
| GitHub Copilot (modo Agent) | **Plano Free, sem cartão: é o que guia a oficina.** Use `#file` se precisar. |
| Claude Code | lê `CLAUDE.md` → `AGENTS.md` |
| Codex (CLI ou extensão) | lê `AGENTS.md` |
| Cursor | lê `AGENTS.md` |
| Kilo Code (VS Code, modelos gratuitos) | lê `AGENTS.md` |
| Gemini CLI | lê `GEMINI.md` → `AGENTS.md` |

## Depois da oficina
O mesmo ciclo existe com ferramentas prontas: Spec Kit (GitHub), OpenSpec, Superpowers (skills.sh), Kiro. Comece pelo método; a ferramenta vem depois.
