# Prompts do ciclo SDD

**Copie e cole. Não há nada para trocar.** Os prompts já vêm preenchidos para cada incremento, na ordem em que a
oficina acontece. Ache a seção do incremento em que você está e desça.

- Os prompts são para **agente no VS Code** (GitHub Copilot em modo Agent, Claude Code, Codex, Cursor, Kilo Code...), que lê a pasta sozinho e grava os arquivos.
- Chat web (sem acesso à pasta) **não é suportado** na oficina. Quem ficar sem agente chama um facilitador.

Regra de ouro: **um prompt, uma resposta, um arquivo**. Não converse. Se a saída vier errada, ajuste a spec e rode o prompt de novo.
Todo incremento termina no P5, que gera **um teste por cenário de aceite** e roda `npm test`.
Depois de qualquer prompt que mexa em código (P4, P5), **reinicie o servidor** seguindo a receita abaixo.
O servidor não recarrega sozinho: ele continua rodando o código antigo até você derrubá-lo.

### Como reiniciar o servidor (faça isso depois de todo P4 e P5)

1. No VS Code, clique **dentro do painel Terminal**, na parte de baixo da janela. É o mesmo terminal onde você digitou
   `npm start` no começo; ele mostra a linha `Inscrições da Oficina rodando em http://localhost:3000`.
   Se o painel estiver fechado, abra pelo menu **Terminal > Novo Terminal** (atalho `Ctrl+'`).
2. Com o cursor piscando no terminal, aperte **`Ctrl+C`**. Isso encerra o servidor antigo.
   Atenção: `Ctrl+C` com o cursor no editor de código só copia texto e não encerra nada.
   Se aparecer `Terminate batch job (Y/N)?`, digite `Y` e aperte `Enter`.
3. No mesmo terminal, digite `npm start` e aperte `Enter`. Espere aparecer de novo a linha
   `Inscrições da Oficina rodando em http://localhost:3000`.
4. No navegador, recarregue a página com **`Ctrl+F5`**.
   A lista vai aparecer vazia: é normal, os dados somem a cada reinício.

Sinal de que esqueceu de reiniciar: a tela nova aparece, mas não mostra nada ou se comporta como o incremento anterior.

---

## Antes de começar

### P0 · Teste de fumaça
```
Liste os arquivos desta pasta e diga em uma linha o que server.js faz. Não altere nada.
Não use skills, ferramentas extras, MCP nem busca na web.
```
Mão levantada quando o agente responder.

---

## Incremento 1 — Cadastro  (`case/01-cadastro/`)

> **A spec deste incremento já vem pronta.** Não existe P1 aqui. Comece lendo `case/01-cadastro/spec.md`
> (repare na R2 e no cenário C3) e vá direto ao P2.

### P2 · Plano
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md e case/01-cadastro/spec.md.
Escreva case/01-cadastro/plan.md seguindo templates/plan.md.
Se case/01-cadastro/plan.md já existir, não escreva nada e me avise.
Não implemente nada. Não contradiga a spec nem a constituição.
Se a spec for ambígua, escolha a opção mais simples e registre em "Dúvidas resolvidas".
Máximo 40 linhas. Crie o arquivo só com o conteúdo gerado.
```
**Revise antes de seguir:** o plano contradiz a spec em algum ponto? Inventou alguma coisa?

### P3 · Tarefas
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/01-cadastro/spec.md e case/01-cadastro/plan.md.
Escreva case/01-cadastro/tasks.md seguindo templates/tasks.md: no máximo 20 tarefas,
cada uma pequena, citando a regra (R?) que satisfaz e como verificar.
A última tarefa é rodar todos os cenários de aceite.
Se case/01-cadastro/tasks.md já existir, não escreva nada e me avise.
Crie o arquivo só com o conteúdo gerado.
```
**Revise antes de seguir:** cada tarefa cita uma regra? Tarefa sem regra é invenção.

### P4 · Implementar
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md, DESIGN.md, case/01-cadastro/spec.md, case/01-cadastro/plan.md e case/01-cadastro/tasks.md.
Implemente todas as tarefas em server.js, public/index.html e public/app.js. Respeite a constituição.
Na tela, copie os blocos prontos de DESIGN.md para dentro de <main id="app"> em public/index.html,
mantendo o cabeçalho, o banner e o rodapé. Não escreva CSS, nem <style>, nem style="".
Marque as tarefas concluídas em tasks.md. Responda só com os arquivos alterados, sem explicações.
```
Depois: **reinicie o servidor** (receita "Como reiniciar o servidor", no topo deste arquivo), abra `http://localhost:3000` e rode os cenários na mão
(cadastrar Ana, tentar " Ana@Mail.com ", tentar nome "A"). Em seguida, **P5**: ele gera os testes e roda `npm test`.

### P5 · Testar (sempre: um teste por cenário de aceite)
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/01-cadastro/spec.md, case/01-cadastro/plan.md, templates/tests.md e tests/helpers.js.
Escreva tests/01.test.js seguindo templates/tests.md: um test() por cenário de aceite da spec, na ordem,
com o nome "C1: <título>", usando as rotas e os códigos de status do plano e as mensagens exatas da spec.
Não leia server.js nem public/ para escrever os testes.
Se tests/01.test.js já existir, não o reescreva: só rode npm test.
Rode npm test. Se algum teste falhar, corrija server.js ou public/app.js (nunca a spec nem o teste) e rode npm test de novo.
Responda só com uma linha por cenário (C1 PASSA / C2 FALHA) e a linha "Arquivos criados/alterados: ...".
```
Depois: no terminal, `npm test` tem que terminar com `fail 0`. Se mexeu em código, **reinicie o servidor** (receita no topo deste arquivo).

**Checkpoint:** "cadastrei, o duplicado foi recusado e npm test deu fail 0".

---

## Incremento 2 — Vagas  (`case/02-vagas/`)

> **Só comece aqui depois que o incremento 1 estiver rodando na tela.**
> Leia o "Incremento 2" em `case/briefing.md`. Escreva a spec à mão (copie `templates/spec.md` para
> `case/02-vagas/spec.md`) **ou** use o P1. Nos dois casos, releia a spec com as 3 perguntas abaixo antes do P2.

### P1 · Spec (opcional)
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md, templates/spec.md, case/01-cadastro/spec.md e o "Incremento 2" de case/briefing.md.
Escreva o arquivo case/02-vagas/spec.md seguindo exatamente o template.
Se case/02-vagas/spec.md já existir, não escreva nada e me avise.
Continue a numeração das regras de onde a spec 01 parou. Não repita regras que já existem nela.
Só as ambiguidades do incremento 2: cada uma vira uma linha em "Dúvidas resolvidas", com a decisão mais simples.
Inclua um último cenário: "todos os cenários do incremento 1 continuam valendo".
Linguagem de negócio: sem endpoints, campos ou tecnologia. Máximo 60 linhas.
Crie o arquivo só com o conteúdo gerado.
```
**Autorrevisão da spec (3 perguntas):** tem ambiguidade que o agente vai resolver sozinho? Tem regra sem cenário?
Tem tecnologia onde deveria ter linguagem de negócio? Sua spec diz quantas vagas?

### P2 · Plano
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md e case/02-vagas/spec.md.
Escreva case/02-vagas/plan.md seguindo templates/plan.md.
Se case/02-vagas/plan.md já existir, não escreva nada e me avise.
Não implemente nada. Não contradiga a spec nem a constituição.
Se a spec for ambígua, escolha a opção mais simples e registre em "Dúvidas resolvidas".
Máximo 40 linhas. Crie o arquivo só com o conteúdo gerado.
```

### P3 · Tarefas
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/02-vagas/spec.md e case/02-vagas/plan.md.
Escreva case/02-vagas/tasks.md seguindo templates/tasks.md: no máximo 20 tarefas,
cada uma pequena, citando a regra (R?) que satisfaz e como verificar.
A última tarefa é rodar todos os cenários de aceite.
Se case/02-vagas/tasks.md já existir, não escreva nada e me avise.
Crie o arquivo só com o conteúdo gerado.
```

### P4 · Implementar
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md, DESIGN.md, case/02-vagas/spec.md, case/02-vagas/plan.md e case/02-vagas/tasks.md.
Implemente todas as tarefas em server.js, public/index.html e public/app.js,
mantendo o que já existe do incremento 1. Respeite a constituição.
Na tela, copie os blocos prontos de DESIGN.md para dentro de <main id="app"> em public/index.html,
mantendo o cabeçalho, o banner e o rodapé. Não escreva CSS, nem <style>, nem style="".
Marque as tarefas concluídas em tasks.md. Responda só com os arquivos alterados, sem explicações.
```
Depois: **reinicie o servidor** (receita no topo deste arquivo), teste na tela e siga para o **P5**.

### P5 · Testar (sempre: um teste por cenário de aceite)
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/02-vagas/spec.md, case/02-vagas/plan.md, templates/tests.md e tests/helpers.js.
Escreva tests/02.test.js seguindo templates/tests.md: um test() por cenário de aceite da spec, na ordem,
com o nome "C1: <título>", usando as rotas e os códigos de status do plano e as mensagens exatas da spec.
Não leia server.js nem public/ para escrever os testes.
O cenário "todos os cenários do incremento 1 continuam valendo" não vira test(): npm test já roda os arquivos de teste anteriores.
Se tests/02.test.js já existir, não o reescreva: só rode npm test.
Rode npm test. Se algum teste falhar, corrija server.js ou public/app.js (nunca a spec nem o teste) e rode npm test de novo.
Responda só com uma linha por cenário (C1 PASSA / C2 FALHA) e a linha "Arquivos criados/alterados: ...".
```
Depois: no terminal, `npm test` tem que terminar com `fail 0`. Se mexeu em código, **reinicie o servidor** (receita no topo deste arquivo).

**Checkpoint:** "a lista de espera promoveu certo e npm test deu fail 0".

---

## Incremento 3 — Check-in  (`case/03-checkin/`)  — bônus

> **Só comece aqui depois que o incremento 2 estiver rodando na tela.**
> Ambiguidade a caçar no briefing: marcar a chegada duas vezes é erro ou não faz diferença?

### P1 · Spec (opcional)
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md, templates/spec.md, case/02-vagas/spec.md e o "Incremento 3" de case/briefing.md.
Escreva o arquivo case/03-checkin/spec.md seguindo exatamente o template.
Se case/03-checkin/spec.md já existir, não escreva nada e me avise.
Continue a numeração das regras de onde a spec 02 parou. Não repita regras que já existem.
Só as ambiguidades do incremento 3: cada uma vira uma linha em "Dúvidas resolvidas", com a decisão mais simples.
Inclua um último cenário: "todos os cenários dos incrementos 1 e 2 continuam valendo".
Linguagem de negócio: sem endpoints, campos ou tecnologia. Máximo 60 linhas.
Crie o arquivo só com o conteúdo gerado.
```

### P2 · Plano
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md e case/03-checkin/spec.md.
Escreva case/03-checkin/plan.md seguindo templates/plan.md.
Se case/03-checkin/plan.md já existir, não escreva nada e me avise.
Não implemente nada. Não contradiga a spec nem a constituição.
Se a spec for ambígua, escolha a opção mais simples e registre em "Dúvidas resolvidas".
Máximo 40 linhas. Crie o arquivo só com o conteúdo gerado.
```

### P3 · Tarefas
```
Leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/03-checkin/spec.md e case/03-checkin/plan.md.
Escreva case/03-checkin/tasks.md seguindo templates/tasks.md: no máximo 20 tarefas,
cada uma pequena, citando a regra (R?) que satisfaz e como verificar.
A última tarefa é rodar todos os cenários de aceite.
Se case/03-checkin/tasks.md já existir, não escreva nada e me avise.
Crie o arquivo só com o conteúdo gerado.
```

### P4 · Implementar
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia CONSTITUTION.md, DESIGN.md, case/03-checkin/spec.md, case/03-checkin/plan.md e case/03-checkin/tasks.md.
Implemente todas as tarefas em server.js, public/index.html e public/app.js,
mantendo o que já existe dos incrementos 1 e 2. Respeite a constituição.
Na tela, copie os blocos prontos de DESIGN.md para dentro de <main id="app"> em public/index.html,
mantendo o cabeçalho, o banner e o rodapé. Não escreva CSS, nem <style>, nem style="".
Marque as tarefas concluídas em tasks.md. Responda só com os arquivos alterados, sem explicações.
```
Depois: **reinicie o servidor** (receita no topo deste arquivo), teste na tela e siga para o **P5**.

### P5 · Testar (sempre: um teste por cenário de aceite)
```
Execute comandos de teste, leia e escreva os arquivos a partir da pasta /oficina-sdd/kit-sdd.
Não use skills, ferramentas extras, MCP nem busca na web. Leia só os arquivos citados aqui.
Leia case/03-checkin/spec.md, case/03-checkin/plan.md, templates/tests.md e tests/helpers.js.
Escreva tests/03.test.js seguindo templates/tests.md: um test() por cenário de aceite da spec, na ordem,
com o nome "C1: <título>", usando as rotas e os códigos de status do plano e as mensagens exatas da spec.
Não leia server.js nem public/ para escrever os testes.
O cenário "todos os cenários dos incrementos 1 e 2 continuam valendo" não vira test(): npm test já roda os arquivos de teste anteriores.
Se tests/03.test.js já existir, não o reescreva: só rode npm test.
Rode npm test. Se algum teste falhar, corrija server.js ou public/app.js (nunca a spec nem o teste) e rode npm test de novo.
Responda só com uma linha por cenário (C1 PASSA / C2 FALHA) e a linha "Arquivos criados/alterados: ...".
```
Depois: no terminal, `npm test` tem que terminar com `fail 0`. Se mexeu em código, **reinicie o servidor** (receita no topo deste arquivo).

---

## Sobre os testes

Todo incremento termina com `tests/0N.test.js`: **um teste por cenário de aceite**, gerado pelo P5 a partir da spec e do plano,
nunca do código. `tests/helpers.js` já vem no kit (não edite). `npm test` roda todos os incrementos juntos: é a prova de que
o incremento novo não quebrou os anteriores. Teste vermelho = código errado: o agente corrige o código, nunca o teste.

---

## Economia de tokens: sete regras de bolso
1. Um prompt por fase. Sem "oi", sem conversa, sem pedir explicação.
2. Contexto mínimo: só a constituição e os artefatos do incremento atual.
   Nunca deixe o agente usar skills, slash commands, MCP, busca na web ou indexar a pasta: cada um desses enche a janela de contexto e gasta cota.
3. Arquivos curtos: spec ≤ 60 linhas, plano ≤ 40, tarefas ≤ 20 itens.
4. Saída só em arquivos: "não explique, só escreva".
5. Se travar, corrija a spec e rode o prompt de novo. Não discuta com o agente.
6. Use o modelo mais barato que o agente oferecer; guarde o caro para o P4.
