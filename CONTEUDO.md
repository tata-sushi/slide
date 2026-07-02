# Padrão dos slides de conteúdo — Apresentação

Referência visual dos **slides claros** (2 a 8) de `apresentacao.html`.
Use este documento como parâmetro para novos slides intermediários. A capa
inicial e a capa final estão documentadas em [`CAPA.md`](CAPA.md).

---

## Fundo

- Cor: `#FFFFFF` (branco).
- **Barra lateral esquerda:** `border-left: 10px solid #35383F` (variável
  `--carbon`) — acento vertical fixo em todos os slides claros (~meio
  centímetro).

## Alinhamento do conteúdo

- Todo o conteúdo (eyebrow + heading + lista/texto) **começa ancorado no
  topo-esquerdo** — mesmo ponto para todos os slides, independente da
  quantidade de conteúdo.
- Container: `.slide-light .slide-inner`
  - `display: flex`, `flex-direction: column`
  - `justify-content: flex-start`
  - `align-items: flex-start`
  - `text-align: left`
  - `padding: 6% 8%`

## Fontes

- **Eyebrow e sub-notas:** DM Mono (pesos 300, 400, 500).
- **Heading e corpo:** DM Sans (pesos 400, 500, 600, 700).

## Eyebrow (categoria / seção)

Texto pequeno em caixa alta, acima do heading — identifica a seção
("Tópico 03", "Seção 01", etc.).

- Fonte: **DM Mono 500**.
- Tamanho: `clamp(9px, 0.9vw, 11px)`.
- Letter-spacing: `0.28em`.
- Transform: `uppercase`.
- Cor: `#999999` (variável `--t3`).
- Margem abaixo: `margin-bottom: 2.5%`.

## Heading (título do slide)

- Fonte: **DM Sans 700**.
- Tamanho: `clamp(26px, 4.48vw, 58px)`.
- Line-height: `1`.
- Letter-spacing: `-1px`.
- Cor: `#111111` (variável `--t1`).
- Margem abaixo: `margin-bottom: 3%`.
- **Sem destaque em citric** — se houver `<span class="accent">` no HTML,
  visualmente ele fica igual ao resto (CSS neutralizado).

## Lista de bullets (`.slide-list`)

- Fonte: **DM Sans 400** (herda `color: var(--t1)`).
- Tamanho: `clamp(13px, 1.5vw, 20px)`.
- Line-height: `1.4`.
- Largura máxima: `92%`.
- Cada `<li>` tem `padding: 0.55em 0 0.55em 1.5em` e uma linha divisória
  superior (`border-top: 1px solid var(--border)`), exceto o primeiro item.
- **Marcador:** círculo carbon absoluto na esquerda.
  - `width/height: 0.44em`
  - `background: var(--carbon)`
  - `border-radius: 50%`
  - `top: 1em; left: 0`

### Sub-notas (dentro do bullet)

Comentário curto, discreto, abaixo do texto do item.

```html
<li>Devolutiva de testes domingo <span class="note">Extras Cinthia</span></li>
```

- Fonte: **DM Mono 500**.
- Tamanho: `0.68em` (relativo ao próprio bullet).
- Letter-spacing: `0.14em`.
- Transform: `uppercase`.
- Cor: `#999999` (variável `--t3`).

### Variante duas colunas

Aplica `.two-col` ao `<ul>` (usado, por exemplo, na Pauta do dia):

- CSS columns 2, `column-gap: 48px`.
- Cada `<li>` recebe `break-inside: avoid`.

## Texto de parágrafo (opcional, `.slide-text`)

Alternativa à lista para slides mais dissertativos.

- Fonte: **DM Sans 400**.
- Tamanho: `clamp(14px, 1.6vw, 20px)`.
- Line-height: `1.5`.
- Cor: `#555555` (variável `--t2`).
- Largura máxima: `80%`.

## Numeração do slide (`.slide-num`)

Posicionada absoluta no canto inferior direito.

- Fonte: **DM Mono 500**.
- Tamanho: `clamp(9px, 0.9vw, 11px)`.
- Letter-spacing: `0.2em`.
- Cor: `#999999` (variável `--t3`).
- Posição: `right: 3%; bottom: 3%`.

---

## Estrutura HTML (modelo)

### Slide com lista simples

```html
<section class="slide slide-light" aria-label="Slide N · Título">
  <div class="slide-inner">
    <p class="slide-eyebrow">Tópico 01</p>
    <h2 class="slide-heading">Título do slide</h2>
    <ul class="slide-list">
      <li>Item 1</li>
      <li>Item 2 <span class="note">Nota curta</span></li>
      <li>Item 3</li>
    </ul>
  </div>
  <div class="slide-num">02</div>
</section>
```

### Slide com lista em duas colunas

Troque `class="slide-list"` por `class="slide-list two-col"`.

### Slide com parágrafo (sem lista)

```html
<section class="slide slide-light" aria-label="Slide N · Título">
  <div class="slide-inner">
    <p class="slide-eyebrow">Seção 01</p>
    <h2 class="slide-heading">Título</h2>
    <p class="slide-text">Corpo do slide em prosa curta.</p>
  </div>
  <div class="slide-num">03</div>
</section>
```

---

## CSS consolidado (referência)

```css
/* Slide claro */
.slide-light {
  background: #FFFFFF;
  color: #111111;
  border-left: 10px solid #35383F;
}
.slide-light .slide-inner {
  align-items: flex-start;
  justify-content: flex-start;
  text-align: left;
}

/* Eyebrow */
.slide-eyebrow {
  font-family: "DM Mono", monospace;
  font-size: clamp(9px, 0.9vw, 11px);
  font-weight: 500;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: #999999;
  margin-bottom: 2.5%;
}

/* Heading */
.slide-heading {
  font-family: "DM Sans", sans-serif;
  font-size: clamp(26px, 4.48vw, 58px);
  font-weight: 700;
  line-height: 1;
  letter-spacing: -1px;
  color: #111111;
  margin-bottom: 3%;
}
.slide-heading .accent { color: inherit; background: none; padding: 0; border-radius: 0; }

/* Lista */
.slide-list {
  list-style: none;
  padding: 0;
  margin: 0;
  width: 100%;
  max-width: 92%;
  font-family: "DM Sans", sans-serif;
  font-size: clamp(13px, 1.5vw, 20px);
  line-height: 1.4;
  color: #111111;
}
.slide-list li {
  position: relative;
  padding: 0.55em 0 0.55em 1.5em;
  border-top: 1px solid #E2E2E2;
}
.slide-list li:first-child { border-top: none; }
.slide-list li::before {
  content: "";
  position: absolute;
  left: 0;
  top: 1em;
  width: 0.44em;
  height: 0.44em;
  background: #35383F;
  border-radius: 50%;
}
.slide-list li .note {
  display: block;
  font-family: "DM Mono", monospace;
  font-size: 0.68em;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: #999999;
  margin-top: 0.2em;
}
.slide-list.two-col { columns: 2; column-gap: 48px; }
.slide-list.two-col li { break-inside: avoid; }

/* Parágrafo (variação sem lista) */
.slide-text {
  font-size: clamp(14px, 1.6vw, 20px);
  line-height: 1.5;
  color: #555555;
  max-width: 80%;
}

/* Numeração */
.slide-num {
  position: absolute;
  right: 3%;
  bottom: 3%;
  font-family: "DM Mono", monospace;
  font-size: clamp(9px, 0.9vw, 11px);
  font-weight: 500;
  letter-spacing: 0.2em;
  color: #999999;
}
```

---

## Slide de introdução (limpo, sem barra)

Variação usada, por exemplo, no slide 2 — entre a capa e a pauta. Serve
para uma abertura curta com texto centralizado e/ou uma imagem de
referência.

- Classe da `<section>`: `.slide-intro` (em vez de `.slide-light`).
- **Sem** barra carbon à esquerda.
- **Sem** eyebrow, heading, lista ou numeração.
- Conteúdo centralizado horizontal e verticalmente.
- Imagem opcional (`.intro-image`) e texto (`.intro-text`) empilhados
  no centro.

```html
<section class="slide slide-intro" aria-label="Slide 2 · Introdução">
  <div class="slide-inner">
    <img class="intro-image" alt="…" src="…">
    <p class="intro-text">Texto introdutório aqui.</p>
  </div>
</section>
```

CSS envolvido:

```css
.slide-intro { background: #FFFFFF; color: #111111; }
.slide-intro .slide-inner {
  align-items: center;
  justify-content: center;
  text-align: center;
  gap: 4%;
}
.intro-image { max-width: 38%; max-height: 44%; object-fit: contain; }
.intro-text {
  font-family: "DM Sans", sans-serif;
  font-size: clamp(16px, 2vw, 28px);
  font-weight: 500;
  line-height: 1.5;
  color: #111111;
  max-width: 70%;
}
```

## Como adicionar um novo slide de conteúdo

1. Duplicar um `<section class="slide slide-light">` existente.
2. Atualizar o número em `aria-label` e no `<div class="slide-num">`.
3. Trocar eyebrow, heading e itens da lista (ou parágrafo).
4. Escolher variante: lista simples, lista em duas colunas ou parágrafo.
5. Não é preciso mexer em nenhum CSS — os estilos deste documento se
   aplicam automaticamente. O total de slides na navegação é detectado por
   JS.

---

## Ferramentas de animação (opcionais, opt-in por slide)

### 1. Reveal — revelar itens progressivamente

Use quando quiser controlar a exposição dos bullets ao vivo. Adicione a
classe **`reveal-list`** ao `<ul>`. Os itens começam ocultos e cada
`→` / `PgDn` / `Espaço` revela o próximo; `←` / `PgUp` esconde o último.
Quando todos estão visíveis, o próximo `→` avança para o próximo slide
(inclusive na barra inferior).

```html
<ul class="slide-list reveal-list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

Combina com `two-col`:

```html
<ul class="slide-list two-col reveal-list">...</ul>
```

O estado de revelação é lembrado por slide: se sair e voltar, retoma de
onde estava.

### 2. Count-up — número animado do 0 até o alvo

Use em números grandes/impactantes. Envolva o número em um `<span>` (ou
qualquer inline) com a classe **`count-up`** e um `data-target`. Quando o
slide fica ativo, o número anima de `0` até o alvo.

```html
<h2 class="slide-heading">
  <span class="count-up" data-target="120" data-suffix="%">0</span> de eficiência
</h2>
```

Atributos suportados:

| Atributo | Padrão | Descrição |
| --- | --- | --- |
| `data-target` | `0` | Valor final. Aceita decimais. |
| `data-duration` | `1200` | Duração da animação em ms. |
| `data-decimals` | `0` | Casas decimais no resultado. |
| `data-prefix` | `""` | Texto antes do número (ex.: `R$ `). |
| `data-suffix` | `""` | Texto depois (ex.: `%`, `h`). |

Formatação: sem decimais usa separador de milhar `pt-BR`
(`1.250`); com decimais usa vírgula (`3,4`).

Exemplos:

```html
<span class="count-up" data-target="1250">0</span>
<!-- → 1.250 -->

<span class="count-up" data-target="98.5" data-decimals="1" data-suffix="%">0</span>
<!-- → 98,5% -->

<span class="count-up" data-target="4200" data-prefix="R$ ">0</span>
<!-- → R$ 4.200 -->
```
