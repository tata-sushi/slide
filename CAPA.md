# Padrão da capa — Apresentação

Referência visual do slide 1 (capa) de `apresentacao.html`. Use este documento
como parâmetro para todos os novos temas de capa (título, subtítulo e cores
podem variar; o resto se mantém).

---

## Fundo

- Cor da capa inicial: `#35383F` (variável `--carbon`).
- Cor da capa final (slide 9 · encerramento): `#000000` (variante `.is-dark`).

## Fontes

Ambas do Google Fonts, já pré-carregadas no `<head>`.

- **Título:** DM Sans (pesos 400, 500, 600, 700).
- **Subtítulo & labels em caixa alta:** DM Mono (pesos 300, 400, 500).

## Logo

- Base64 embutido no HTML (PNG original 1414×2000, ícone + wordmark).
- Exibe **só o ícone** (hexágono). Wordmark "TATÁ SUSHI" é recortado.
  - `aspect-ratio: 1414 / 1250`
  - `object-fit: cover`
  - `object-position: top center`
- **Tamanho:** `width: 12.67%` do slide, `max-width: 104px`.
- **Espaço abaixo (gap até o título):** `margin-bottom: 4%`.

## Título

- Fonte: **DM Sans 700**.
- Cor: `#CFFF00` (variável `--citric`).
- Tamanho: `clamp(24px, 4.54vw, 65px)`.
- Line-height: `0.9`.
- Letter-spacing: `0.03em`.

## Alinhamento

- **Logo + título formam um único grupo**, centralizado horizontal e
  verticalmente no slide via `.slide-inner` (flex column com
  `justify-content: center` e `align-items: center`).
- O **subtítulo é posicionado absolutamente abaixo do título**
  (`.cover-title-wrap` recebe `position: relative` e o subtítulo usa
  `position: absolute; top: 100%`). Assim ele NÃO afeta o cálculo de
  centro do grupo logo + título.

## Subtítulo

- Fonte: **DM Mono 400**.
- Cor: `rgba(255, 255, 255, .42)` (~42% de branco).
- Tamanho: `clamp(9px, 1vw, 12px)`.
- Letter-spacing: `0.32em`.
- Transform: `uppercase`.
- Gap até o título: `padding-top: 1.1em` (relativo ao próprio subtítulo).
- Posição: absoluto, `top: 100%` do wrapper do título, centralizado com
  `left: 50%; transform: translateX(-50%)`.

## Estrutura HTML

```html
<section class="slide slide-cover is-active" aria-label="Slide 1 · Capa">
  <div class="slide-inner">
    <img src="data:image/png;base64,..." alt="TATÁ SUSHI" class="cover-logo">
    <div class="cover-title-wrap">
      <h1 class="cover-title">Reunião de líderes</h1>
      <p class="cover-subtitle">Um novo começo</p>
    </div>
  </div>
</section>
```

## Capa final (slide 9)

Padrão mais enxuto que a capa inicial:

- **Fundo:** preto sólido `#000000` (`.slide-cover.is-dark`).
- **Único elemento:** logo **inteiro** (ícone + wordmark "TATÁ SUSHI"),
  centralizado horizontal e verticalmente.
- **Sem título, subtítulo, rodapé ou numeração.**
- Classe do logo: `.cover-logo-full` — não usa recorte por `aspect-ratio`
  (usa a proporção natural 1414 × 2000 do PNG), com `object-fit: contain`.
- **Tamanho:** `width: 22%` do slide, `max-width: 220px`.
- O `src` é copiado em runtime do logo da capa inicial (via JS), então há
  apenas uma cópia do base64 no HTML — mas as duas imagens são independentes
  em CSS (`.cover-logo` × `.cover-logo-full`).

Estrutura HTML da capa final:

```html
<section class="slide slide-cover is-dark" aria-label="Slide 9 · Encerramento">
  <div class="slide-inner">
    <img alt="TATÁ SUSHI" class="cover-logo-full" id="closingLogo">
  </div>
</section>
```

## Como trocar o tema

1. **Título** — edite o texto do `<h1 class="cover-title">`.
2. **Subtítulo** — edite o texto do `<p class="cover-subtitle">`.
3. **Cor do fundo** — troque `--carbon` ou adicione uma variante (ex.: para o
   encerramento existe a classe `.slide-cover.is-dark` com `background: #000`).
4. **Cor do título** — mantenha `--citric` para permanecer no sistema, ou crie
   uma variante temática.
5. **Tudo o mais permanece igual** (logo, fontes, tamanhos, alinhamento).

## CSS consolidado (referência)

```css
/* Fundo */
.slide-cover           { background: #35383F; color: #FFFFFF; }
.slide-cover.is-dark   { background: #000000; }

/* Container centralizando o grupo logo + título */
.slide-inner {
  position: absolute; inset: 0;
  padding: 6% 8%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

/* Logo — só o ícone (capa inicial) */
.cover-logo {
  width: 12.67%;
  max-width: 104px;
  aspect-ratio: 1414 / 1250;
  height: auto;
  object-fit: cover;
  object-position: top center;
  margin-bottom: 4%;
}

/* Logo — inteiro (capa final, slide 9) */
.cover-logo-full {
  width: 22%;
  max-width: 220px;
  height: auto;
  object-fit: contain;
}

/* Título */
.cover-title-wrap { position: relative; text-align: center; }
.cover-title {
  font-family: "DM Sans", sans-serif;
  font-size: clamp(24px, 4.54vw, 65px);
  font-weight: 700;
  line-height: 0.9;
  letter-spacing: 0.03em;
  color: #CFFF00;
  margin: 0;
}

/* Subtítulo — absoluto abaixo do título (não afeta o centro do grupo) */
.cover-subtitle {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  margin: 0;
  padding-top: 1.1em;
  font-family: "DM Mono", monospace;
  font-size: clamp(9px, 1vw, 12px);
  font-weight: 400;
  letter-spacing: 0.32em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.42);
  white-space: nowrap;
  line-height: 1;
}
```
