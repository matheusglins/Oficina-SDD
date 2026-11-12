# Design kit — receita da tela

A identidade visual da **Pitang** (cores, fontes e layout de pitang.com) já está pronta em `public/styles.css`, com as fontes em `public/fonts/` (funciona sem internet).
**O agente não escreve CSS.** Ele copia os blocos abaixo e troca só os textos e os `id`.
Todos os componentes aparecem renderizados em `http://localhost:3000/components.html`.

## 5 regras
1. `public/index.html` já tem o esqueleto: cabeçalho (`.bd-header`) + banner com o título (`.bd-hero`) + `<main class="bd-content" id="app">` + rodapé (`.bd-footer`). **Não apague nem mude** o cabeçalho, o banner e o rodapé. Todo conteúdo novo entra **dentro de `#app`**.
2. Todo bloco de conteúdo fica dentro de um `<div class="bd-card">`. O título da seção (`<h2 class="bd-section__title">`) fica **fora** do cartão.
3. Proibido: tag `<style>`, atributo `style=""` (exceto os que já estão nos blocos abaixo), arquivo `.css` novo, cores ou fontes no HTML.
4. Botões e inputs **sempre** com as classes do kit: `bd-btn bd-btn--primary`, `bd-input`, etc. Um `<button>` ou `<input>` sem classe está errado.
5. Faltou componente? Combine os existentes. Não invente classe nova.

## Bloco A — tela de cadastro (incremento 1): cole dentro de `#app`
```html
<section class="bd-section">
  <h2 class="bd-section__title">Nova inscrição</h2>
  <div class="bd-card">
    <form class="bd-form bd-form--inline" id="form">
      <div class="bd-field">
        <label class="bd-field__label" for="name">Nome</label>
        <input class="bd-input" id="name" name="name" placeholder="Ex.: Ana Lima" autocomplete="off" required>
      </div>
      <div class="bd-field">
        <label class="bd-field__label" for="email">E-mail</label>
        <input class="bd-input" id="email" name="email" placeholder="ana@mail.com" autocomplete="off" required>
      </div>
      <button class="bd-btn bd-btn--primary" type="submit">Inscrever</button>
    </form>
    <p class="bd-alert bd-alert--error" id="message" role="alert" style="margin:20px 0 0"></p>
  </div>
</section>

<section class="bd-section">
  <h2 class="bd-section__title" id="list-title">Inscritos <span class="bd-count">0</span></h2>
  <div class="bd-card">
    <ul class="bd-list" id="list"></ul>
  </div>
</section>
```
- `#message` vazio fica invisível. Para mostrar erro: `message.textContent = data.error`. Para limpar: `message.textContent = ''`.

## Bloco B — um item da lista (gerado pelo `app.js`)
HTML que cada `<li>` deve ter (texto visível: "Ana Lima — ana@mail.com"):
```html
<li class="bd-list__item">
  <span class="bd-avatar">AL</span>
  <div class="bd-list__body bd-list__body--inline"><strong>Ana Lima</strong><span>— ana@mail.com</span></div>
  <span class="bd-badge bd-badge--info">Confirmado</span>
  <div class="bd-list__actions">
    <button class="bd-btn bd-btn--sm bd-btn--success" type="button">Check-in</button>
    <button class="bd-btn bd-btn--sm bd-btn--danger" type="button">Cancelar</button>
  </div>
</li>
```
Função JS pronta para gerar esse item (copie para `public/app.js` e adapte os botões ao incremento):
```js
function el(tag, className, text) {
  const node = document.createElement(tag);
  if (className) node.className = className;
  if (text !== undefined) node.textContent = text;
  return node;
}
function initials(name) {
  return name.trim().split(/\s+/).slice(0, 2).map((w) => w[0]).join('').toUpperCase();
}
function renderItem(p) {
  const li = el('li', 'bd-list__item');
  li.appendChild(el('span', 'bd-avatar', initials(p.name)));
  const body = el('div', 'bd-list__body bd-list__body--inline');
  body.appendChild(el('strong', '', p.name));
  body.appendChild(el('span', '', `— ${p.email}`));
  li.appendChild(body);
  const actions = el('div', 'bd-list__actions');
  // Exemplo de botão de ação (só nos incrementos que pedem):
  // const btn = el('button', 'bd-btn bd-btn--sm bd-btn--danger', 'Cancelar'); btn.type = 'button';
  // btn.addEventListener('click', () => cancelParticipant(p.id)); actions.appendChild(btn);
  li.appendChild(actions);
  return li;
}
```
Lista vazia: `list.replaceChildren(el('li', 'bd-list__empty', 'Ninguém inscrito ainda.'))`.
Contagem no título: `title.replaceChildren('Inscritos ', el('span', 'bd-count', String(items.length)))`.

## Bloco C — dois grupos lado a lado (ex.: confirmados e lista de espera)
```html
<div class="bd-grid bd-grid--2">
  <section class="bd-section">
    <h2 class="bd-section__title" id="confirmed-title">Confirmados <span class="bd-count">0</span></h2>
    <div class="bd-card"><ul class="bd-list" id="confirmed"></ul></div>
  </section>
  <section class="bd-section">
    <h2 class="bd-section__title" id="waitlist-title">Lista de espera <span class="bd-count">0</span></h2>
    <div class="bd-card"><ul class="bd-list" id="waitlist"></ul></div>
  </section>
</div>
```

## Bloco D — contagens em destaque (ex.: presentes, ausentes, em espera): cole no topo de `#app`
```html
<div class="bd-stats" id="summary">
  <div class="bd-card bd-stat">
    <span class="bd-stat__icon bd-stat__icon--green"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg></span>
    <div><div class="bd-stat__label">Presentes</div><div class="bd-stat__value" id="stat-present">0</div></div>
  </div>
  <div class="bd-card bd-stat">
    <span class="bd-stat__icon bd-stat__icon--red"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg></span>
    <div><div class="bd-stat__label">Ausentes</div><div class="bd-stat__value" id="stat-absent">0</div></div>
  </div>
  <div class="bd-card bd-stat">
    <span class="bd-stat__icon bd-stat__icon--yellow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/></svg></span>
    <div><div class="bd-stat__label">Em espera</div><div class="bd-stat__value" id="stat-waitlist">0</div></div>
  </div>
</div>
```
Atualizar: `document.getElementById('stat-present').textContent = presentes;`

## Tabela de escolha: "preciso de X" → "uso Y"
| Preciso de... | Use exatamente |
|---|---|
| Botão principal (enviar formulário) | `<button class="bd-btn bd-btn--primary" type="submit">` |
| Botão de cancelar / remover (em lista) | `<button class="bd-btn bd-btn--sm bd-btn--danger" type="button">Cancelar</button>` |
| Botão de check-in / confirmar (em lista) | `<button class="bd-btn bd-btn--sm bd-btn--success" type="button">Check-in</button>` |
| Botão neutro secundário | `<button class="bd-btn bd-btn--outline" type="button">` |
| Status "Confirmado" | `<span class="bd-badge bd-badge--info">Confirmado</span>` |
| Status "Em espera" | `<span class="bd-badge bd-badge--warning">Em espera</span>` |
| Status "Presente" | `<span class="bd-badge bd-badge--success">Presente</span>` |
| Status "Ausente" | `<span class="bd-badge bd-badge--neutral">Ausente</span>` |
| Mensagem de erro da API | `<p class="bd-alert bd-alert--error" id="message" role="alert"></p>` |
| Mensagem de sucesso | `<p class="bd-alert bd-alert--success" role="status">` |
| Contagem ao lado de um título | `<span class="bd-count">3</span>` |
| Tabela com colunas | `<div class="bd-table-wrap"><table class="bd-table">` (`<td class="is-muted">` para e-mail) |
| Abas para alternar grupos | `<div class="bd-tabs"><button class="bd-tab is-active" type="button">` |
| Barra de ocupação de vagas | `<div class="bd-progress"><div class="bd-progress__bar" style="width:75%"></div></div>` |
| Lista sem itens | `<li class="bd-list__empty">Ninguém inscrito ainda.</li>` |

## Tokens (só referência; não repita valores no HTML)
Títulos Montserrat, texto Inter · fundo branco · cartão branco com borda `#E6E6E6`, raio 24px · primário (vermelho Pitang) `#ED1C24` · laranja `#FF8000` · texto `#2D2D2D` · secundário `#777777` · sucesso `#00C392` · alerta `#F6B700`. Só as cores do site da Pitang: nada de azul.
