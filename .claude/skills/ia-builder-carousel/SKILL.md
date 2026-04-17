---
name: ia-builder-carousel
description: Gera carrosséis HTML no design system IA Builder (tema HUD dark/cyan, slides 1080x1080 para Instagram). Use quando o usuário pedir carrossel, slides, post Instagram, criativo ou peça visual no estilo IA Builder.
---

# IA Builder — Carousel Design System

Gera carrosséis HTML exportáveis em 1080×1080 px usando o design system da marca **IA Builder** (tema HUD futurista, fundo dark, acentos cyan e laranja).

## Quando usar

- Pedido explícito: "faz um carrossel", "slides pro Instagram", "criativo IA Builder", "peça em HUD".
- Qualquer peça visual da marca IA Builder (lançamentos, captação, anúncios de turma, conteúdo educativo).

## Output esperado

Um único arquivo `.html` auto-contido com N seções `<section class="slide">`, cada uma em `1080×1080 px`, pronto para capturar tela / imprimir como PDF / exportar com "Full Page Screen Capture".

---

## Design Tokens

### Paleta

| Token | Hex | Uso |
|---|---|---|
| `--bg-body` | `#25252d` | Fundo da página (fora dos slides) |
| `--bg-slide` | `#0e0e13` | Fundo de cada slide |
| `--bg-panel` | `#19191f` | Painel de nota / cards secundários |
| `--bg-mini-glass` | `rgba(31, 31, 38, 0.85)` | Mini-cards (grade 2×2) |
| `--bg-glass` | `rgba(19, 19, 25, 0.65)` | Glassmorphism principal |
| `--text-primary` | `#f9f5fd` | Texto principal |
| `--text-muted` | `#acaab1` | Texto secundário |
| `--accent-cyan` | `#8ff5ff` | Cor de destaque / HUD |
| `--accent-purple` | `#c47fff` | Variante de chip / raridade |
| `--border-soft` | `#48474d` | Bordas neutras |
| `--cta-gradient` | `linear-gradient(135deg, #ff9f43 0%, #ff7a1a 56%, #f25c05 100%)` | Botão CTA |

### Tipografia

- **Display:** `Space Grotesk` (400, 500, 600, 700) — headlines, brand, chips.
- **Texto:** `Inter` (400, 500, 600, 700) — body, subtítulos, listas.
- **Import via Google Fonts:**
  ```html
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  ```

### Escala de fontes

| Classe | Tamanho | Uso |
|---|---|---|
| `.headline--xl` | `76px` / letter-spacing -0.02em | Slide de capa |
| `.headline--lg` | `62px` | Títulos fortes |
| `.headline--md` | `52px` | Títulos internos |
| `.sub` | `26px` / line-height 1.45 | Subtítulo padrão |
| `.sub--sm` | `22px` | Subtítulo compacto |
| `.bullet-list li` | `24px` / line-height 1.4 | Listas |
| `.chip` | `11px` / letter-spacing 0.12em uppercase | Tags |
| `.hud-label` | `9px` / letter-spacing 0.22em uppercase | Label topo HUD |
| `.brand` | `15px` / letter-spacing 0.2em uppercase | "IA BUILDER" no footer |
| `.slide-index` | `13px` / letter-spacing 0.18em | "01 / 08" |
| `.cta-btn` | `22px` / letter-spacing 0.06em uppercase | Botão CTA |

### Efeitos / Glow

- Text shadow headline: `0 0 18px rgba(143, 245, 255, 0.35)`
- Bullet glow: `0 0 12px rgba(143, 245, 255, 0.6)`
- CTA shadow: `0 10px 34px rgba(255, 122, 26, 0.28)`
- Glass backdrop-filter: `blur(20px)`

### Dimensões

- Slide: `1080×1080 px` (fixo — feed Instagram quadrado).
- Padding interno: `56px 72px 48px`.
- Border-radius: `2px` (chips), `4px` (todo o resto). **Não arredondar mais que isso** — o design é anguloso.
- Gap entre slides na visualização: `48px`.

---

## Componentes

### 1. Estrutura base do slide

```html
<section class="slide" aria-label="Slide N de TOTAL">
  <div class="slide__bg"></div>           <!-- grid cyan sutil -->
  <div class="slide__vignette"></div>     <!-- vinheta radial -->
  <span class="hud-corner hud-corner--tl"></span>
  <span class="hud-corner hud-corner--tr"></span>
  <span class="hud-corner hud-corner--bl"></span>
  <span class="hud-corner hud-corner--br"></span>
  <div class="slide__inner">
    <div class="hud-label">
      <span class="hud-label__line"></span>
      CATEGORIA // SUBTÍTULO
      <span class="hud-label__line"></span>
    </div>
    <div class="slide__body">
      <!-- conteúdo centralizado -->
    </div>
    <footer class="slide-footer">
      <span class="brand">IA BUILDER</span>
      <span class="slide-index">0N / 0T</span>
    </footer>
  </div>
</section>
```

### 2. HUD corners
4 cantos em L com borda 2px cyan (`rgba(143, 245, 255, 0.45)`), 28×28 px, offset 36px das bordas.

### 3. Grid background
Linhas cyan a 4% de opacidade, cell 60×60px, sobre fundo `#0e0e13`.

### 4. Vinheta
`radial-gradient(ellipse 85% 75% at 50% 50%, transparent 0%, rgba(14, 14, 19, 0.88) 100%)` — escurece as bordas para puxar o olhar ao centro.

### 5. HUD label (topo)
`CATEGORIA // DETALHE` em cyan, 9px, com linhas horizontais cyan dos dois lados (`width: 32px; height: 1px`).

### 6. Headline
Espaço Grotesk 700, cor `#f9f5fd`, com glow cyan. Use `<span class="headline--accent">` para destacar parte em cyan.

### 7. Glass card
Container translúcido com blur — usado para conter listas ou textos de apoio.
```html
<div class="glass">...</div>
```

### 8. Bullet list
Lista com marcador quadrado cyan de 8×8px com glow. Texto em cinza, com `<strong>` em branco.

### 9. Chip
Tag retangular (border-radius 2px) cyan. Variante `chip--purple` para raridade.

### 10. Mini-glass (grid 2×2)
Cards compactos com título cyan pequeno em cima e descrição cinza embaixo.
```html
<div class="two-col">
  <div class="mini-glass"><strong>Título</strong>Descrição curta</div>
  ...
</div>
```

### 11. CTA button
Botão laranja com gradiente, uppercase, usado apenas no último slide.

### 12. Footer
`IA BUILDER` à esquerda + `0N / 0T` à direita, separados por `56px`, com borda superior cyan muito sutil.

---

## Boilerplate completo (copiar e adaptar)

Quando gerar um novo carrossel, comece deste esqueleto, substitua o conteúdo e ajuste o número de slides. **Nunca altere os tokens ou o CSS** sem pedido explícito.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>IA Builder — {{TÍTULO DO CARROSSEL}}</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: #25252d; color: #f9f5fd; font-family: 'Inter', sans-serif; padding: 48px 24px 80px; }
    .doc-note { max-width: 1080px; margin: 0 auto 32px; font-size: 14px; color: #acaab1; line-height: 1.5; padding: 16px 20px; background: #19191f; border: 1px solid #48474d; border-radius: 4px; }
    .slides { display: flex; flex-direction: column; align-items: center; gap: 48px; }
    .slide { width: 1080px; height: 1080px; position: relative; background: #0e0e13; overflow: hidden; flex-shrink: 0; }
    .slide__bg { position: absolute; inset: 0; background-image: linear-gradient(rgba(143, 245, 255, 0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(143, 245, 255, 0.04) 1px, transparent 1px); background-size: 60px 60px; }
    .slide__vignette { position: absolute; inset: 0; pointer-events: none; background: radial-gradient(ellipse 85% 75% at 50% 50%, transparent 0%, rgba(14, 14, 19, 0.88) 100%); }
    .slide__inner { position: relative; z-index: 1; height: 100%; padding: 56px 72px 48px; display: flex; flex-direction: column; justify-content: flex-start; align-items: stretch; }
    .slide__body { flex: 1; min-height: 0; display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; width: 100%; }
    .hud-corner { position: absolute; width: 28px; height: 28px; border-color: rgba(143, 245, 255, 0.45); z-index: 2; pointer-events: none; }
    .hud-corner--tl { top: 36px; left: 36px; border-top: 2px solid; border-left: 2px solid; }
    .hud-corner--tr { top: 36px; right: 36px; border-top: 2px solid; border-right: 2px solid; }
    .hud-corner--bl { bottom: 36px; left: 36px; border-bottom: 2px solid; border-left: 2px solid; }
    .hud-corner--br { bottom: 36px; right: 36px; border-bottom: 2px solid; border-right: 2px solid; }
    .hud-label { font-size: 9px; font-weight: 700; letter-spacing: 0.22em; text-transform: uppercase; color: #8ff5ff; opacity: 0.75; display: flex; align-items: center; justify-content: center; gap: 10px; margin-bottom: 0; width: 100%; flex-shrink: 0; }
    .hud-label__line { display: block; width: 32px; height: 1px; background: #8ff5ff; opacity: 0.55; }
    .headline { font-family: 'Space Grotesk', sans-serif; font-weight: 700; line-height: 1.05; color: #f9f5fd; text-shadow: 0 0 18px rgba(143, 245, 255, 0.35); text-align: center; max-width: 920px; }
    .headline--xl { font-size: 76px; letter-spacing: -0.02em; }
    .headline--lg { font-size: 62px; letter-spacing: -0.02em; }
    .headline--md { font-size: 52px; letter-spacing: -0.02em; }
    .headline--accent { color: #8ff5ff; }
    .sub { margin-top: 24px; font-size: 26px; line-height: 1.45; color: rgba(249, 245, 253, 0.72); font-weight: 400; max-width: 900px; margin-left: auto; margin-right: auto; text-align: center; }
    .sub--sm { font-size: 22px; }
    .chip-row { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 28px; justify-content: center; width: 100%; }
    .chip { background: rgba(143, 245, 255, 0.08); border: 1px solid rgba(143, 245, 255, 0.22); color: #8ff5ff; font-size: 11px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; border-radius: 2px; padding: 6px 12px; }
    .chip--purple { background: rgba(196, 127, 255, 0.1); border-color: rgba(196, 127, 255, 0.35); color: #c47fff; }
    .glass { margin-top: 32px; background: rgba(19, 19, 25, 0.65); backdrop-filter: blur(20px); border: 1px solid rgba(143, 245, 255, 0.12); border-radius: 4px; padding: 28px 32px; width: 100%; max-width: 920px; margin-left: auto; margin-right: auto; text-align: center; }
    .bullet-list { list-style: none; }
    .bullet-list li { display: flex; align-items: flex-start; justify-content: center; gap: 16px; font-size: 24px; line-height: 1.4; color: #acaab1; margin-bottom: 18px; }
    .bullet-list li > span:last-child { text-align: center; max-width: 780px; }
    .bullet-list li:last-child { margin-bottom: 0; }
    .bullet-list__mark { flex-shrink: 0; width: 8px; height: 8px; margin-top: 11px; background: #8ff5ff; box-shadow: 0 0 12px rgba(143, 245, 255, 0.6); border-radius: 1px; }
    .bullet-list strong { color: #f9f5fd; font-weight: 600; }
    .slide-footer { display: flex; align-items: center; justify-content: center; gap: 56px; padding-top: 24px; border-top: 1px solid rgba(143, 245, 255, 0.08); width: 100%; flex-shrink: 0; }
    .brand { font-family: 'Space Grotesk', sans-serif; font-weight: 700; font-size: 15px; letter-spacing: 0.2em; text-transform: uppercase; color: #8ff5ff; }
    .slide-index { font-family: 'Space Grotesk', sans-serif; font-size: 13px; font-weight: 600; letter-spacing: 0.18em; color: rgba(172, 170, 177, 0.65); }
    .cta-btn { display: inline-flex; align-items: center; justify-content: center; margin-top: 32px; padding: 22px 40px; font-family: 'Space Grotesk', sans-serif; font-weight: 700; font-size: 22px; letter-spacing: 0.06em; text-transform: uppercase; color: #fff; background: linear-gradient(135deg, #ff9f43 0%, #ff7a1a 56%, #f25c05 100%); border: none; border-radius: 4px; box-shadow: 0 10px 34px rgba(255, 122, 26, 0.28); }
    .cta-hint { margin-top: 16px; font-size: 18px; color: rgba(172, 170, 177, 0.9); text-align: center; }
    .cta-block { display: flex; flex-direction: column; align-items: center; width: 100%; max-width: 920px; }
    .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 28px; width: 100%; max-width: 880px; margin-left: auto; margin-right: auto; }
    .mini-glass { background: rgba(31, 31, 38, 0.85); border: 1px solid rgba(143, 245, 255, 0.1); border-radius: 4px; padding: 20px 22px; font-size: 20px; color: #acaab1; line-height: 1.35; text-align: center; }
    .mini-glass strong { display: block; font-family: 'Space Grotesk', sans-serif; color: #8ff5ff; font-size: 15px; letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 8px; text-align: center; }
    @media print { body { background: #fff; padding: 0; } .doc-note { display: none; } .slides { gap: 0; } .slide { page-break-after: always; margin: 0; } }
  </style>
</head>
<body>
  <p class="doc-note"><strong>Uso:</strong> cada bloco mede <strong>1080×1080 px</strong> (feed Instagram). Abra no navegador, zoom 100% e exporte cada slide.</p>
  <div class="slides">
    <!-- SLIDES AQUI -->
  </div>
</body>
</html>
```

---

## Padrões de conteúdo por tipo de slide

### Capa (Slide 1)
- `headline--xl` com segunda linha em `headline--accent`.
- `sub` curto (~1-2 linhas) com promessa.
- `chip-row` com 2 chips (um cyan + um roxo opcional).

### Promessa / Mensagem forte (Slide 2)
- `headline--lg` + linha `headline--md headline--accent` como extensão.
- `sub` que conecta à dor/benefício.

### Dados / Mercado (Slide 3)
- `headline--md` com accent na segunda linha.
- `.glass` com `.bullet-list` de 3 itens — números em `<strong>`.

### Formato / Features (Slide 4)
- Igual Slide 3, mas itens descrevem entregas (duração, projetos, temas).

### Perfil / Para quem é (Slide 5)
- `two-col` com 4 `mini-glass`.
- `sub--sm` ao final resumindo.

### Autoridade / Time (Slide 6)
- `headline--md` com uma palavra em accent.
- `sub` de credenciamento + `.glass` com `.bullet-list` de nomes (`<strong>Nome</strong> — especialidade`).

### Oferta / Bolsas (Slide 7)
- `headline--lg` com accent no valor/oferta.
- `sub` com regras/valores.
- `.glass` com detalhe do processo.
- `chip-row` de reforço.

### CTA (último slide)
- `headline--md` com accent em "formulário" ou ação.
- `sub` com chamada final.
- `.cta-block` com `.cta-btn` + `.cta-hint` (link/instrução).

---

## Regras de escrita

- **Título curto**, quebrado em 2 linhas com `<br />` quando precisa respirar.
- **Use `<span class="headline--accent">`** para destacar 1 palavra/frase por slide — nunca mais.
- **`<strong>` dentro de `sub` e `bullet-list`** fica branco (`#f9f5fd`) — use para números, nomes, entregas.
- **Tom:** direto, assertivo, verbos no imperativo ou afirmações fortes. Nunca "talvez", "pode ser".
- **Chips:** sempre uppercase, 1-3 palavras.
- **HUD label:** `CATEGORIA // SUBTÍTULO` em uppercase. Exemplos do projeto base: `LANÇAMENTO // PÓS-GRADUAÇÃO`, `MERCADO // DADOS`, `DOCÊNCIA // MERCADO`, `CTA // PRÓXIMO PASSO`.

---

## Checklist antes de entregar

- [ ] Nome do arquivo: `instagram-carousel-{{tema}}.html`.
- [ ] Todos os slides têm os 4 `hud-corner`.
- [ ] Todos têm `slide__bg` + `slide__vignette`.
- [ ] Footer em todos com `brand` + `slide-index` correto (`0N / 0T`).
- [ ] Índice bate com número total (ex.: 8 slides → todos terminam em `/ 08`).
- [ ] Só 1 `headline--accent` por slide (ou no máximo 2 linhas consecutivas).
- [ ] CTA aparece só no último slide.
- [ ] Nenhum token de cor ou valor de CSS foi alterado em relação ao boilerplate.
- [ ] `@media print` presente para exportação PDF.

---

## Referência

Projeto base: `/Users/weslleyhenrique/Downloads/Projetos/apresentacao pos/instagram-carousel-turma-cofundadores.html` — carrossel de 8 slides para lançamento da Turma Co-Fundadores.
