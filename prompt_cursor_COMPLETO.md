# PROMPT COMPLETO — Site de Apresentação Fruttino Andino
# Nível: Produção Profissional | Stack: HTML + CSS + JS Vanilla (zero frameworks)

---

## ⚠️ LEIA ANTES DE COMEÇAR — REGRAS ABSOLUTAS

1. **Zero frameworks.** Nenhum Bootstrap, Tailwind, React, Vue, jQuery. Apenas HTML5, CSS3 e JavaScript ES6+ puro.
2. **Um único arquivo `index.html`** com `<style>` interno e `<script>` no final do body. Nada de arquivos separados.
3. **Todas as imagens** estão na pasta `./imagens_extraidas/` relativa ao `index.html`. Nunca use caminhos absolutos.
4. **Google Fonts** carregado via `<link>` no `<head>` — as únicas dependências externas permitidas.
5. O site deve abrir perfeitamente em `file:///` (sem servidor local). Isso significa zero fetch de APIs, zero módulos ES6 com import/export.
6. Compatível com Google Chrome versão atual. Priorize Chrome pois é onde será apresentado.
7. **Não use `vh` em elementos críticos do hero** — use `min-height: 100dvh` para evitar bug de altura em telas com barra do navegador.
8. Toda animação deve usar `will-change: transform` para garantir 60fps.
9. **Código limpo e comentado** — cada seção do CSS e JS deve ter um comentário `/* === NOME DA SEÇÃO === */`.

---

## FONTES — Google Fonts

Cole exatamente este `<link>` no `<head>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

- **`Playfair Display 700/900`** → todos os títulos de seção, nome da marca, headings H1/H2
- **`Montserrat 300/400/500/600`** → subtítulos, corpo de texto, labels, botões, nav links

---

## PALETA DE CORES — VALORES EXATOS (extraídos da imagem_09.jpeg)

```css
:root {
  /* Cores da marca Fruttino Andino */
  --magui:          #4a6c8a;   /* Morado Magui — azul-acinzentado escuro */
  --morango:        #e8736e;   /* Rosa Morango — coral-rosado quente */
  --chirimoia:      #d4b84a;   /* Amarelo Chirimoia — mostarda dourada */
  --crema:          #f0ddd8;   /* Crema Etiqueta — bege rosado suave */
  --negro:          #1a1a1a;   /* Negro Montaña — quase preto */
  --verde:          #4a7c3f;   /* Verde Andino — extraído do logo */
  --branco:         #ffffff;
  --cinza-claro:    #f8f6f3;   /* fundo de seções neutras */

  /* Cores por sabor de produto */
  --cor-chirimoya:  #f5f0d0;   /* amarelo creme muito suave */
  --cor-morango:    #fce8e8;   /* rosa bebê */
  --cor-maqui:      #ede0f0;   /* lilás suave */
  --cor-manzana:    #e8f5e8;   /* verde menta suave */

  /* Gradientes usados no site */
  --grad-hero:      linear-gradient(to bottom, rgba(0,0,0,0.15) 0%, rgba(0,0,0,0.45) 100%);
  --grad-verde:     linear-gradient(135deg, #4a7c3f 0%, #2d5a25 100%);
  --grad-crema:     linear-gradient(180deg, #f8f6f3 0%, #f0ddd8 100%);

  /* Sombras */
  --sombra-card:    0 8px 32px rgba(0,0,0,0.12);
  --sombra-hover:   0 20px 60px rgba(0,0,0,0.22);
  --sombra-nav:     0 2px 20px rgba(0,0,0,0.10);

  /* Bordas */
  --radius-card:    20px;
  --radius-btn:     50px;
  --radius-img:     16px;

  /* Transições */
  --transition:     all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
}
```

---

## CSS BASE GLOBAL

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  font-size: 16px;
}

body {
  font-family: 'Montserrat', sans-serif;
  background-color: var(--branco);
  color: var(--negro);
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}

img {
  max-width: 100%;
  display: block;
}

section {
  position: relative;
  overflow: hidden;
}

/* Classe utilitária de container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
}

/* Scroll reveal — estado inicial (invisível, deslocado para baixo) */
.reveal {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.7s ease, transform 0.7s ease;
  will-change: transform, opacity;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
.reveal.delay-1 { transition-delay: 0.1s; }
.reveal.delay-2 { transition-delay: 0.2s; }
.reveal.delay-3 { transition-delay: 0.3s; }
.reveal.delay-4 { transition-delay: 0.4s; }
```

---

## SEÇÃO 1 — NAVBAR

**Comportamento:** Começa absolutamente posicionada sobre o hero (transparente). Após 80px de scroll, adiciona a classe `.scrolled` via JavaScript que muda o fundo.

**HTML exato:**
```html
<nav id="navbar">
  <div class="nav-inner">
    <a href="#hero" class="nav-logo">
      <!-- SVG inline de montanha simples -->
      <svg width="32" height="20" viewBox="0 0 32 20" fill="none">
        <path d="M0 20 L8 6 L13 13 L18 4 L24 13 L27 9 L32 20Z" fill="#4a7c3f"/>
      </svg>
      <span>FRUTTINO <strong>ANDINO</strong></span>
    </a>
    <button class="nav-hamburger" id="hamburger" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links" id="navLinks">
      <li><a href="#sobre">Nossa História</a></li>
      <li><a href="#produtos">Sabores</a></li>
      <li><a href="#galeria">Momentos</a></li>
      <li><a href="#canais">Onde Encontrar</a></li>
      <li><a href="#produtos" class="nav-cta">Conheça os Sabores</a></li>
    </ul>
  </div>
</nav>
```

**CSS exato:**
```css
/* === NAVBAR === */
#navbar {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 1000;
  padding: 20px 0;
  transition: var(--transition);
}

#navbar.scrolled {
  background: rgba(255,255,255,0.95);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  box-shadow: var(--sombra-nav);
  padding: 14px 0;
}

.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  font-family: 'Playfair Display', serif;
  font-size: 1.1rem;
  color: var(--branco);
  letter-spacing: 1px;
  transition: var(--transition);
}
#navbar.scrolled .nav-logo { color: var(--negro); }
#navbar.scrolled .nav-logo svg path { fill: var(--verde); }
.nav-logo:not(.scrolled *) svg path { fill: var(--branco); }

.nav-links {
  display: flex;
  align-items: center;
  gap: 36px;
  list-style: none;
}

.nav-links a {
  text-decoration: none;
  font-size: 0.82rem;
  font-weight: 600;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: rgba(255,255,255,0.9);
  transition: var(--transition);
  position: relative;
}

/* underline animado nos links */
.nav-links a:not(.nav-cta)::after {
  content: '';
  position: absolute;
  bottom: -4px; left: 0;
  width: 0; height: 2px;
  background: var(--morango);
  transition: width 0.3s ease;
}
.nav-links a:not(.nav-cta):hover::after { width: 100%; }

#navbar.scrolled .nav-links a { color: var(--negro); }

.nav-cta {
  background: var(--morango) !important;
  color: var(--branco) !important;
  padding: 10px 22px;
  border-radius: var(--radius-btn);
  font-size: 0.78rem !important;
  letter-spacing: 1px;
  transition: var(--transition) !important;
}
.nav-cta:hover {
  background: var(--verde) !important;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(74,124,63,0.4);
}
.nav-cta::after { display: none !important; }

/* Hambúrguer — só aparece em mobile */
.nav-hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}
.nav-hamburger span {
  display: block;
  width: 26px; height: 2px;
  background: var(--branco);
  border-radius: 2px;
  transition: var(--transition);
}
#navbar.scrolled .nav-hamburger span { background: var(--negro); }
```

**JS para navbar:**
```javascript
// === NAVBAR SCROLL BEHAVIOR ===
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 80);
});

// === HAMBURGER MENU ===
const hamburger = document.getElementById('hamburger');
const navLinks = document.getElementById('navLinks');
hamburger.addEventListener('click', () => {
  navLinks.classList.toggle('open');
  hamburger.classList.toggle('active');
});
// Fechar ao clicar em link
navLinks.querySelectorAll('a').forEach(link => {
  link.addEventListener('click', () => {
    navLinks.classList.remove('open');
    hamburger.classList.remove('active');
  });
});
```

---

## SEÇÃO 2 — HERO (100dvh, tela cheia)

**Imagem de fundo:** `./imagens_extraidas/imagem_01.png`  
**Layout:** fullscreen com overlay gradiente. Conteúdo centralizado verticalmente.  
**Elementos internos (de cima para baixo):**
1. Badge pequeno animado: `✦ Vinho Chileno com Frutas Naturais ✦`
2. Título principal H1 com efeito typewriter letra por letra
3. Subtítulo fade-in com delay
4. Dois botões lado a lado
5. Seta bounce no rodapé
6. 20 partículas "bolhas" geradas por JS subindo em loop infinito

**HTML exato:**
```html
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-overlay"></div>
  <div class="hero-bubbles" id="heroBubbles"></div>

  <div class="hero-content">
    <div class="hero-badge">✦ Vinho Chileno com Frutas Naturais ✦</div>
    <h1 class="hero-title" id="heroTitle"></h1>
    <p class="hero-sub">Do coração dos Andes para o seu momento perfeito</p>
    <div class="hero-btns">
      <a href="#produtos" class="btn btn-primary">Descobrir os Sabores</a>
      <a href="#sobre" class="btn btn-outline">Nossa História</a>
    </div>
  </div>

  <a href="#sobre" class="hero-arrow" aria-label="Rolar para baixo">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
      <path d="M12 5v14M5 12l7 7 7-7" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </a>
</section>
```

**CSS exato:**
```css
/* === HERO === */
#hero {
  min-height: 100dvh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background-image: url('./imagens_extraidas/imagem_01.png');
  background-size: cover;
  background-position: center 30%;
  background-repeat: no-repeat;
  transform: scale(1.05); /* ligeiramente maior para o parallax */
  transition: transform 0.1s linear;
  will-change: transform;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(0,0,0,0.20) 0%,
    rgba(0,0,0,0.10) 30%,
    rgba(0,0,0,0.50) 100%
  );
}

.hero-bubbles {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

/* Cada bolha gerada por JS */
.bubble {
  position: absolute;
  bottom: -20px;
  border-radius: 50%;
  background: rgba(255,255,255,0.25);
  animation: bubbleRise linear infinite;
  will-change: transform, opacity;
}

@keyframes bubbleRise {
  0%   { transform: translateY(0) translateX(0); opacity: 0.8; }
  50%  { transform: translateY(-40vh) translateX(15px); opacity: 0.4; }
  100% { transform: translateY(-100vh) translateX(-10px); opacity: 0; }
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 780px;
  padding: 0 24px;
}

.hero-badge {
  display: inline-block;
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255,255,255,0.3);
  color: rgba(255,255,255,0.95);
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 3px;
  text-transform: uppercase;
  padding: 8px 20px;
  border-radius: 50px;
  margin-bottom: 28px;
  animation: fadeInDown 0.8s ease forwards;
}

@keyframes fadeInDown {
  from { opacity: 0; transform: translateY(-20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(3rem, 8vw, 6.5rem);
  font-weight: 900;
  color: var(--branco);
  line-height: 1.05;
  letter-spacing: -1px;
  margin-bottom: 20px;
  min-height: 1.2em; /* evita salto de layout durante typewriter */
}

/* O cursor piscante do typewriter */
.hero-title::after {
  content: '|';
  animation: blink 0.8s step-end infinite;
  color: var(--morango);
  font-weight: 300;
}
.hero-title.done::after { display: none; }

@keyframes blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0; }
}

.hero-sub {
  font-size: clamp(0.95rem, 2vw, 1.2rem);
  font-weight: 300;
  color: rgba(255,255,255,0.88);
  letter-spacing: 1px;
  margin-bottom: 44px;
  opacity: 0;
  animation: fadeIn 1s ease 2.5s forwards; /* delay para começar após typewriter */
}

@keyframes fadeIn {
  to { opacity: 1; }
}

.hero-btns {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
  opacity: 0;
  animation: fadeIn 1s ease 3s forwards;
}

/* Botões reutilizáveis */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 15px 36px;
  border-radius: var(--radius-btn);
  font-family: 'Montserrat', sans-serif;
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  text-decoration: none;
  cursor: pointer;
  border: 2px solid transparent;
  transition: var(--transition);
  will-change: transform;
}

.btn-primary {
  background: var(--morango);
  color: var(--branco);
  box-shadow: 0 4px 20px rgba(232,115,110,0.45);
}
.btn-primary:hover {
  background: var(--verde);
  box-shadow: 0 8px 30px rgba(74,124,63,0.5);
  transform: translateY(-3px);
}

.btn-outline {
  background: transparent;
  color: var(--branco);
  border-color: rgba(255,255,255,0.6);
}
.btn-outline:hover {
  background: rgba(255,255,255,0.15);
  border-color: var(--branco);
  transform: translateY(-3px);
}

/* Seta de scroll bounce */
.hero-arrow {
  position: absolute;
  bottom: 36px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  animation: bounce 2s ease infinite;
  opacity: 0;
  animation: bounce 2s ease 3.5s infinite, fadeIn 1s ease 3.5s forwards;
  display: flex;
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(10px); }
}
```

**JS para hero (typewriter + bolhas + parallax):**
```javascript
// === HERO TYPEWRITER ===
const heroTitle = document.getElementById('heroTitle');
const text = 'O Sabor\nDos Andes';
let i = 0;
function typeWriter() {
  if (i < text.length) {
    if (text[i] === '\n') {
      heroTitle.innerHTML += '<br>';
    } else {
      heroTitle.innerHTML += text[i];
    }
    i++;
    setTimeout(typeWriter, i < 3 ? 120 : 80);
  } else {
    heroTitle.classList.add('done');
  }
}
window.addEventListener('load', () => setTimeout(typeWriter, 400));

// === HERO PARALLAX ===
const heroBg = document.querySelector('.hero-bg');
window.addEventListener('scroll', () => {
  if (window.scrollY < window.innerHeight) {
    heroBg.style.transform = `scale(1.05) translateY(${window.scrollY * 0.25}px)`;
  }
}, { passive: true });

// === HERO BUBBLES ===
const bubblesContainer = document.getElementById('heroBubbles');
function createBubble() {
  const b = document.createElement('div');
  b.classList.add('bubble');
  const size = Math.random() * 12 + 4; // 4px a 16px
  b.style.cssText = `
    width: ${size}px;
    height: ${size}px;
    left: ${Math.random() * 100}%;
    animation-duration: ${Math.random() * 8 + 6}s;
    animation-delay: ${Math.random() * 5}s;
  `;
  bubblesContainer.appendChild(b);
}
for (let j = 0; j < 22; j++) createBubble();
```

---

## SEÇÃO 3 — SOBRE A MARCA

**Imagem de fundo:** `./imagens_extraidas/imagem_02.png` (montanhas aquarela azuis)  
**Efeito:** parallax com `background-attachment: fixed`  
**Layout:** card branco centralizado flutuando sobre a imagem

**HTML:**
```html
<section id="sobre">
  <div class="sobre-bg"></div>
  <div class="container">
    <div class="sobre-card reveal">
      <div class="sobre-label">Nossa História</div>
      <h2>Nascido nas Montanhas,<br>Feito para o Verão</h2>
      <p>O <strong>Fruttino Andino</strong> é um vinho leve e efervescente, produzido no Chile com frutas nativas colhidas nas regiões andinas mais ricas do país. Cada garrafa de 275ml carrega a pureza das montanhas nevadas, a frescura do vento patagônico e o sabor autêntico da terra chilena.</p>
      <p>Com apenas 7% de teor alcoólico, é o companheiro perfeito para momentos ao ar livre, praias, festivais e celebrações com amigos.</p>
      <div class="sobre-stats">
        <div class="stat reveal delay-1">
          <div class="stat-icon">🍷</div>
          <div class="stat-num">100%</div>
          <div class="stat-label">Vinho Chileno<br>Autêntico</div>
        </div>
        <div class="stat reveal delay-2">
          <div class="stat-icon">🌿</div>
          <div class="stat-num">4</div>
          <div class="stat-label">Sabores com<br>Frutas Naturais</div>
        </div>
        <div class="stat reveal delay-3">
          <div class="stat-icon">✨</div>
          <div class="stat-num">7%</div>
          <div class="stat-label">Vol · Leve e<br>Refrescante</div>
        </div>
        <div class="stat reveal delay-4">
          <div class="stat-icon">📦</div>
          <div class="stat-num">275ml</div>
          <div class="stat-label">Formato Prático<br>Individual</div>
        </div>
      </div>
    </div>
  </div>
</section>
```

**CSS:**
```css
/* === SOBRE === */
#sobre {
  padding: 140px 0;
  position: relative;
}

.sobre-bg {
  position: absolute;
  inset: 0;
  background-image: url('./imagens_extraidas/imagem_02.png');
  background-size: cover;
  background-position: center bottom;
  background-attachment: fixed;
  opacity: 0.6;
}

#sobre::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(255,255,255,0.5);
}

.sobre-card {
  position: relative;
  z-index: 1;
  background: rgba(255,255,255,0.92);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-radius: var(--radius-card);
  padding: 64px 72px;
  max-width: 860px;
  margin: 0 auto;
  box-shadow: var(--sombra-card);
  border: 1px solid rgba(255,255,255,0.8);
}

.sobre-label {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--morango);
  margin-bottom: 16px;
}

.sobre-card h2 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  color: var(--negro);
  line-height: 1.2;
  margin-bottom: 28px;
}

.sobre-card p {
  font-size: 1.02rem;
  font-weight: 400;
  color: #444;
  line-height: 1.8;
  margin-bottom: 16px;
}

.sobre-stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  margin-top: 48px;
  padding-top: 40px;
  border-top: 1px solid rgba(0,0,0,0.08);
}

.stat {
  text-align: center;
}

.stat-icon {
  font-size: 2rem;
  margin-bottom: 12px;
}

.stat-num {
  font-family: 'Playfair Display', serif;
  font-size: 2rem;
  font-weight: 900;
  color: var(--verde);
  line-height: 1;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 0.78rem;
  font-weight: 600;
  color: #666;
  line-height: 1.4;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
```

---

## SEÇÃO 4 — PRODUTOS (4 SABORES)

**Layout:** grid 2×2 em desktop, 1 coluna em mobile  
**Interação:** card com efeito flip 3D real no hover (perspectiva CSS + rotateY)  
**Imagem:** `imagem_04.png` (garrafa Chirimoya) usada em todos os cards — cada um tem um filtro CSS `hue-rotate` diferente para dar cor ao líquido da garrafa visualmente

**Os 4 sabores (dados exatos do slide):**
```
1. Chirimoya de Quillota — Vinho Branco — fruta: Chirimoya — cor: amarelo creme
2. Morango do Maipo    — Vinho Rosé   — fruta: Morango    — cor: rosa suave  
3. Maqui Patagônico    — Vinho Tinto  — fruta: Maqui      — cor: lilás suave
4. Manzana de Quillota — Vinho Branco — fruta: Maçã Verde  — cor: verde menta
```

**HTML:**
```html
<section id="produtos">
  <div class="container">
    <div class="section-header reveal">
      <span class="section-label">Nossa Linha</span>
      <h2>Quatro Sabores,<br>Infinitas Memórias</h2>
      <p>Cada garrafa é uma experiência única, inspirada nas frutas mais especiais dos vales andinos chilenos.</p>
    </div>

    <div class="produtos-grid">

      <!-- Card 1: Chirimoya -->
      <div class="produto-card reveal delay-1" data-flavor="chirimoya">
        <div class="card-inner">
          <div class="card-front" style="background: var(--cor-chirimoya);">
            <div class="card-fruit-emoji">🍈</div>
            <img src="./imagens_extraidas/imagem_04.png" alt="Chirimoya de Quillota" class="card-bottle">
            <div class="card-front-info">
              <h3>Chirimoya<br><span>de Quillota</span></h3>
              <div class="card-tag">Vinho Branco · 7% vol</div>
            </div>
          </div>
          <div class="card-back" style="background: var(--chirimoia);">
            <div class="card-back-emoji">🍈</div>
            <h3>Chirimoya<br>de Quillota</h3>
            <div class="card-divider"></div>
            <p>Notas frescas e cremosas da chirimoya nativa de Quillota, com final suave e floral. Servir gelado entre 4–6°C.</p>
            <ul>
              <li>🍾 Vinho Branco com Fruta Natural</li>
              <li>📍 Vale de Quillota, Chile</li>
              <li>🌡️ 7% vol · 275ml</li>
            </ul>
            <a href="#" class="btn btn-back">Saiba Mais</a>
          </div>
        </div>
      </div>

      <!-- Card 2: Morango -->
      <div class="produto-card reveal delay-2" data-flavor="morango">
        <div class="card-inner">
          <div class="card-front" style="background: var(--cor-morango);">
            <div class="card-fruit-emoji">🍓</div>
            <img src="./imagens_extraidas/imagem_04.png" alt="Morango do Maipo" class="card-bottle" style="filter: hue-rotate(320deg) saturate(1.4);">
            <div class="card-front-info">
              <h3>Morango<br><span>do Maipo</span></h3>
              <div class="card-tag">Vinho Rosé · 7% vol</div>
            </div>
          </div>
          <div class="card-back" style="background: var(--morango);">
            <div class="card-back-emoji">🍓</div>
            <h3>Morango<br>do Maipo</h3>
            <div class="card-divider"></div>
            <p>Morangos frescos colhidos no Vale do Maipo transformados em um rosé leve, com aroma intenso e sabor vibrante.</p>
            <ul>
              <li>🍾 Vinho Rosé com Fruta Natural</li>
              <li>📍 Vale do Maipo, Chile</li>
              <li>🌡️ 7% vol · 275ml</li>
            </ul>
            <a href="#" class="btn btn-back">Saiba Mais</a>
          </div>
        </div>
      </div>

      <!-- Card 3: Maqui -->
      <div class="produto-card reveal delay-3" data-flavor="maqui">
        <div class="card-inner">
          <div class="card-front" style="background: var(--cor-maqui);">
            <div class="card-fruit-emoji">🫐</div>
            <img src="./imagens_extraidas/imagem_04.png" alt="Maqui Patagônico" class="card-bottle" style="filter: hue-rotate(220deg) saturate(1.6) brightness(0.85);">
            <div class="card-front-info">
              <h3>Maqui<br><span>Patagônico</span></h3>
              <div class="card-tag">Vinho Tinto · 7% vol</div>
            </div>
          </div>
          <div class="card-back" style="background: var(--magui);">
            <div class="card-back-emoji">🫐</div>
            <h3>Maqui<br>Patagônico</h3>
            <div class="card-divider"></div>
            <p>O maqui, superfruita patagônica rica em antioxidantes, dá origem a um tinto leve com cor intensa e sabor silvestre único.</p>
            <ul>
              <li>🍾 Vinho Tinto com Fruta Natural</li>
              <li>📍 Patagônia Chilena</li>
              <li>🌡️ 7% vol · 275ml</li>
            </ul>
            <a href="#" class="btn btn-back">Saiba Mais</a>
          </div>
        </div>
      </div>

      <!-- Card 4: Manzana -->
      <div class="produto-card reveal delay-4" data-flavor="manzana">
        <div class="card-inner">
          <div class="card-front" style="background: var(--cor-manzana);">
            <div class="card-fruit-emoji">🍏</div>
            <img src="./imagens_extraidas/imagem_04.png" alt="Manzana de Quillota" class="card-bottle" style="filter: hue-rotate(80deg) saturate(0.8) brightness(1.1);">
            <div class="card-front-info">
              <h3>Manzana<br><span>de Quillota</span></h3>
              <div class="card-tag">Vinho Branco · 7% vol</div>
            </div>
          </div>
          <div class="card-back" style="background: var(--verde);">
            <div class="card-back-emoji">🍏</div>
            <h3>Manzana<br>de Quillota</h3>
            <div class="card-divider"></div>
            <p>A maçã verde crocante de Quillota transforma-se em um vinho branco refrescante, com acidez equilibrada e aroma de pomar andino.</p>
            <ul>
              <li>🍾 Vinho Branco com Fruta Natural</li>
              <li>📍 Vale de Quillota, Chile</li>
              <li>🌡️ 7% vol · 275ml</li>
            </ul>
            <a href="#" class="btn btn-back">Saiba Mais</a>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

**CSS:**
```css
/* === PRODUTOS === */
#produtos {
  padding: 120px 0;
  background: var(--cinza-claro);
}

.section-header {
  text-align: center;
  margin-bottom: 72px;
}

.section-label {
  display: inline-block;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--morango);
  margin-bottom: 16px;
}

.section-header h2 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.2rem, 4.5vw, 3.4rem);
  font-weight: 700;
  color: var(--negro);
  line-height: 1.15;
  margin-bottom: 20px;
}

.section-header p {
  font-size: 1.05rem;
  color: #666;
  max-width: 540px;
  margin: 0 auto;
  line-height: 1.7;
}

/* Grid de produtos */
.produtos-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 28px;
  max-width: 900px;
  margin: 0 auto;
}

/* Flip card */
.produto-card {
  height: 500px;
  perspective: 1200px;
  cursor: pointer;
}

.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 0.7s cubic-bezier(0.4, 0.2, 0.2, 1);
  will-change: transform;
}

.produto-card:hover .card-inner {
  transform: rotateY(180deg);
}

.card-front,
.card-back {
  position: absolute;
  inset: 0;
  border-radius: var(--radius-card);
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  padding: 32px;
}

.card-front {
  position: relative;
}

.card-fruit-emoji {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 2.5rem;
  opacity: 0.5;
}

.card-bottle {
  width: 55%;
  max-height: 320px;
  object-fit: contain;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -52%);
  filter: drop-shadow(0 20px 40px rgba(0,0,0,0.18));
  transition: transform 0.4s ease;
  will-change: transform;
}
.produto-card:hover .card-bottle {
  transform: translate(-50%, -56%) scale(1.04);
}

.card-front-info {
  position: relative;
  text-align: center;
  z-index: 1;
}

.card-front-info h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.6rem;
  font-weight: 700;
  color: var(--negro);
  line-height: 1.1;
  margin-bottom: 8px;
}
.card-front-info h3 span {
  font-size: 1.1rem;
  font-weight: 400;
  font-style: italic;
}

.card-tag {
  display: inline-block;
  background: rgba(0,0,0,0.08);
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 4px 14px;
  border-radius: 50px;
  color: var(--negro);
}

/* Verso do card */
.card-back {
  transform: rotateY(180deg);
  justify-content: center;
  text-align: center;
  color: var(--branco);
  gap: 16px;
}

.card-back-emoji {
  font-size: 3rem;
}

.card-back h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.8rem;
  font-weight: 700;
  line-height: 1.1;
  color: var(--branco);
}

.card-divider {
  width: 40px;
  height: 2px;
  background: rgba(255,255,255,0.5);
  margin: 0 auto;
}

.card-back p {
  font-size: 0.9rem;
  line-height: 1.7;
  color: rgba(255,255,255,0.9);
  max-width: 260px;
}

.card-back ul {
  list-style: none;
  text-align: left;
  width: 100%;
}

.card-back ul li {
  font-size: 0.82rem;
  font-weight: 500;
  color: rgba(255,255,255,0.85);
  padding: 5px 0;
  border-bottom: 1px solid rgba(255,255,255,0.15);
}

.btn-back {
  background: rgba(255,255,255,0.2);
  color: var(--branco);
  border: 2px solid rgba(255,255,255,0.5);
  padding: 10px 28px;
  border-radius: var(--radius-btn);
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  text-decoration: none;
  transition: var(--transition);
  margin-top: 8px;
}
.btn-back:hover {
  background: rgba(255,255,255,0.35);
}
```

---

## SEÇÃO 5 — GALERIA LIFESTYLE

**Imagens usadas:**
- `imagem_05.png` — amigos na praia (caption: "Momentos com Amigos")
- `imagem_06.png` — garrafas na praia com montanhas (caption: "Natureza e Sabor")
- `imagem_08.png` — garrafas no topo da montanha (caption: "Da Montanha para Você")

**Fundo:** `imagem_03.png` (praia desfocada) com overlay verde-andino 45%

**HTML:**
```html
<section id="galeria">
  <div class="galeria-bg"></div>
  <div class="galeria-overlay"></div>
  <div class="container">
    <div class="section-header reveal" style="color: white;">
      <span class="section-label" style="color: rgba(255,255,255,0.7);">Estilo de Vida</span>
      <h2 style="color: white;">Para Cada<br>Momento Especial</h2>
    </div>
    <div class="galeria-grid">
      <div class="galeria-item reveal delay-1">
        <div class="galeria-img-wrap">
          <img src="./imagens_extraidas/imagem_05.png" alt="Amigos celebrando com Fruttino Andino">
          <div class="galeria-caption">Momentos com Amigos</div>
        </div>
      </div>
      <div class="galeria-item reveal delay-2">
        <div class="galeria-img-wrap">
          <img src="./imagens_extraidas/imagem_06.png" alt="Fruttino Andino na praia com montanhas">
          <div class="galeria-caption">Natureza e Sabor</div>
        </div>
      </div>
      <div class="galeria-item reveal delay-3">
        <div class="galeria-img-wrap">
          <img src="./imagens_extraidas/imagem_08.png" alt="Fruttino Andino no alto da montanha">
          <div class="galeria-caption">Da Montanha para Você</div>
        </div>
      </div>
    </div>
  </div>
</section>
```

**CSS:**
```css
/* === GALERIA === */
#galeria {
  padding: 120px 0;
  position: relative;
}

.galeria-bg {
  position: absolute;
  inset: 0;
  background-image: url('./imagens_extraidas/imagem_03.png');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

.galeria-overlay {
  position: absolute;
  inset: 0;
  background: rgba(26, 60, 22, 0.72);
}

#galeria .container { position: relative; z-index: 1; }
#galeria .section-header { margin-bottom: 56px; }

.galeria-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.galeria-img-wrap {
  border-radius: var(--radius-img);
  overflow: hidden;
  position: relative;
  box-shadow: var(--sombra-card);
  aspect-ratio: 3/4;
}

.galeria-img-wrap img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  will-change: transform;
}

.galeria-img-wrap:hover img {
  transform: scale(1.08);
}

.galeria-caption {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  padding: 28px 20px 20px;
  background: linear-gradient(transparent, rgba(0,0,0,0.75));
  color: var(--branco);
  font-size: 0.88rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  transform: translateY(4px);
  transition: var(--transition);
}

.galeria-img-wrap:hover .galeria-caption {
  transform: translateY(0);
}
```

---

## SEÇÃO 6 — IMPACTO VISUAL (garrafa em círculo girando)

**Imagem:** `imagem_10.png` (foto aérea das garrafas em círculo na areia)  
**Efeito:** rotação lenta e contínua + texto ao lado  
**Layout:** dois blocos lado a lado — imagem à esquerda rotacionando, texto à direita

**HTML:**
```html
<section id="impacto">
  <div class="container">
    <div class="impacto-grid">
      <div class="impacto-img-wrap reveal">
        <div class="impacto-ring"></div>
        <img src="./imagens_extraidas/imagem_10.png" alt="Linha completa Fruttino Andino" class="impacto-img">
      </div>
      <div class="impacto-texto reveal delay-2">
        <span class="section-label">Linha Completa</span>
        <h2>Uma Família de<br>Sabores Andinos</h2>
        <p>Do branco ao tinto, do doce ao seco, a linha Fruttino Andino celebra a diversidade das frutas que crescem nos vales e montanhas do Chile. Cada variação é uma viagem sensorial pelos terrenos mais fascinantes da América do Sul.</p>
        <p>Produzidos com controle rigoroso de qualidade, nossos vinhos combinam tradição vitivinícola chilena com inovação na escolha das frutas.</p>
        <div class="impacto-badges">
          <div class="badge-item">🏔️ Origem Andina Certificada</div>
          <div class="badge-item">🍃 Sem Corantes Artificiais</div>
          <div class="badge-item">❄️ Servir Bem Gelado</div>
        </div>
      </div>
    </div>
  </div>
</section>
```

**CSS:**
```css
/* === IMPACTO === */
#impacto {
  padding: 120px 0;
  background: var(--branco);
  overflow: visible;
}

.impacto-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.impacto-img-wrap {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Anel decorativo girando atrás da imagem */
.impacto-ring {
  position: absolute;
  width: 105%;
  height: 105%;
  border-radius: 50%;
  border: 2px dashed rgba(74,124,63,0.25);
  animation: ringRotate 30s linear infinite;
  will-change: transform;
}

@keyframes ringRotate {
  to { transform: rotate(360deg); }
}

.impacto-img {
  width: 100%;
  border-radius: 50%;
  box-shadow: 0 30px 80px rgba(0,0,0,0.15);
  animation: slowRotate 60s linear infinite;
  will-change: transform;
}

@keyframes slowRotate {
  to { transform: rotate(360deg); }
}

.impacto-texto h2 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2rem, 3.5vw, 2.8rem);
  font-weight: 700;
  color: var(--negro);
  line-height: 1.15;
  margin: 12px 0 24px;
}

.impacto-texto p {
  font-size: 1rem;
  color: #555;
  line-height: 1.8;
  margin-bottom: 16px;
}

.impacto-badges {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 32px;
}

.badge-item {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--verde);
  padding: 12px 20px;
  background: rgba(74,124,63,0.07);
  border-radius: 12px;
  border-left: 3px solid var(--verde);
}
```

---

## SEÇÃO 7 — CANAIS DE VENDA

**Layout:** 3 cards lado a lado com countup animation nos percentuais  
**Dados exatos do slide (imagem_07.png):**
- Canal Moderno: 60% — "Góndola fria, seção importados"
- HORECA: 25% — "Quiosques de praia, bares, eventos. Consumo imediato bem gelado."
- E-Commerce +: 15% — "Mercado Livre, Zé Delivery, Rappi, Instagram Shop"

**HTML:**
```html
<section id="canais">
  <div class="container">
    <div class="section-header reveal">
      <span class="section-label">Distribuição</span>
      <h2>Onde Encontrar<br>Fruttino Andino</h2>
    </div>
    <div class="canais-grid">
      <div class="canal-card reveal delay-1" data-target="60" data-color="#4a6c8a">
        <div class="canal-icon" style="background: linear-gradient(135deg, #4a6c8a, #2d4a6a);">
          <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5">
            <path d="M6 2L3 6v14a2 2 0 002 2h14a2 2 0 002-2V6l-3-4z"/>
            <line x1="3" y1="6" x2="21" y2="6"/>
            <path d="M16 10a4 4 0 01-8 0"/>
          </svg>
        </div>
        <div class="canal-percent" data-count="60">0<span>%</span></div>
        <h3>Canal Moderno</h3>
        <p>Góndola fria e seção de importados em supermercados e lojas especializadas.</p>
        <div class="canal-bar"><div class="canal-bar-fill" style="width: 0%; background: #4a6c8a;" data-width="60"></div></div>
      </div>

      <div class="canal-card reveal delay-2" data-target="25" data-color="#e8736e">
        <div class="canal-icon" style="background: linear-gradient(135deg, #e8736e, #c94f4a);">
          <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5">
            <circle cx="12" cy="12" r="4"/>
            <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41"/>
          </svg>
        </div>
        <div class="canal-percent" data-count="25">0<span>%</span></div>
        <h3>HORECA</h3>
        <p>Quiosques de praia, bares e eventos. Consumo imediato bem gelado ao ar livre.</p>
        <div class="canal-bar"><div class="canal-bar-fill" style="width: 0%; background: #e8736e;" data-width="25"></div></div>
      </div>

      <div class="canal-card reveal delay-3" data-target="15" data-color="#4a7c3f">
        <div class="canal-icon" style="background: linear-gradient(135deg, #4a7c3f, #2d5a25);">
          <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5">
            <rect x="5" y="2" width="14" height="20" rx="2" ry="2"/>
            <line x1="12" y1="18" x2="12.01" y2="18"/>
          </svg>
        </div>
        <div class="canal-percent" data-count="15">0<span>%</span></div>
        <h3>E-Commerce +</h3>
        <p>Mercado Livre, Zé Delivery, Rappi e Instagram Shop. Entrega rápida na sua porta.</p>
        <div class="canal-bar"><div class="canal-bar-fill" style="width: 0%; background: #4a7c3f;" data-width="15"></div></div>
      </div>
    </div>
  </div>
</section>
```

**CSS:**
```css
/* === CANAIS === */
#canais {
  padding: 120px 0;
  background: var(--grad-crema);
}

.canais-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 28px;
  margin-top: 16px;
}

.canal-card {
  background: var(--branco);
  border-radius: var(--radius-card);
  padding: 44px 36px;
  box-shadow: var(--sombra-card);
  text-align: center;
  transition: var(--transition);
  will-change: transform;
}

.canal-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--sombra-hover);
}

.canal-icon {
  width: 72px;
  height: 72px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 24px;
  box-shadow: 0 8px 24px rgba(0,0,0,0.18);
}

.canal-percent {
  font-family: 'Playfair Display', serif;
  font-size: 5rem;
  font-weight: 900;
  line-height: 1;
  color: var(--negro);
  margin-bottom: 12px;
}
.canal-percent span {
  font-size: 2.5rem;
  font-weight: 700;
}

.canal-card h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--negro);
  margin-bottom: 12px;
}

.canal-card p {
  font-size: 0.9rem;
  color: #666;
  line-height: 1.7;
  margin-bottom: 24px;
}

.canal-bar {
  height: 6px;
  background: rgba(0,0,0,0.08);
  border-radius: 3px;
  overflow: hidden;
}

.canal-bar-fill {
  height: 100%;
  border-radius: 3px;
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  will-change: width;
}
```

**JS para countup e barra (via IntersectionObserver):**
```javascript
// === CANAIS COUNTUP + BARRA ===
const canaisObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (!entry.isIntersecting) return;
    const card = entry.target;
    const target = parseInt(card.dataset.target);
    const numEl = card.querySelector('.canal-percent');
    const barFill = card.querySelector('.canal-bar-fill');

    // Countup
    let count = 0;
    const step = Math.ceil(target / 40);
    const timer = setInterval(() => {
      count = Math.min(count + step, target);
      numEl.innerHTML = count + '<span>%</span>';
      if (count >= target) clearInterval(timer);
    }, 40);

    // Barra
    setTimeout(() => {
      barFill.style.width = barFill.dataset.width + '%';
    }, 100);

    canaisObserver.unobserve(card);
  });
}, { threshold: 0.4 });

document.querySelectorAll('.canal-card').forEach(card => canaisObserver.observe(card));
```

---

## SEÇÃO 8 — FOOTER

**HTML:**
```html
<footer id="footer">
  <div class="footer-inner">
    <div class="footer-logo">
      <svg width="48" height="30" viewBox="0 0 48 30" fill="none">
        <path d="M0 30 L12 9 L19.5 19.5 L27 6 L36 19.5 L40.5 13.5 L48 30Z" fill="#4a7c3f" opacity="0.8"/>
      </svg>
      <div>
        <div class="footer-brand">FRUTTINO ANDINO</div>
        <div class="footer-tagline">Vinho Chileno com Frutas Naturais</div>
      </div>
    </div>
    <div class="footer-divider"></div>
    <div class="footer-sabores">
      <span>Chirimoya de Quillota</span>
      <span>·</span>
      <span>Morango do Maipo</span>
      <span>·</span>
      <span>Maqui Patagônico</span>
      <span>·</span>
      <span>Manzana de Quillota</span>
    </div>
    <div class="footer-divider"></div>
    <div class="footer-aviso">🍷 Beba com moderação. Proibido para menores de 18 anos.</div>
    <div class="footer-copy">© 2025 Fruttino Andino · Produzido no Chile · Todos os direitos reservados</div>
  </div>
</footer>
```

**CSS:**
```css
/* === FOOTER === */
#footer {
  background: var(--negro);
  padding: 64px 40px 40px;
  text-align: center;
}

.footer-inner {
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 28px;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 16px;
}

.footer-brand {
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--branco);
  letter-spacing: 3px;
}

.footer-tagline {
  font-size: 0.78rem;
  color: rgba(255,255,255,0.5);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-top: 4px;
}

.footer-divider {
  width: 60px;
  height: 1px;
  background: rgba(255,255,255,0.15);
}

.footer-sabores {
  display: flex;
  gap: 12px;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
  font-size: 0.82rem;
  color: rgba(255,255,255,0.55);
  font-style: italic;
}

.footer-aviso {
  font-size: 0.8rem;
  color: rgba(255,255,255,0.4);
  letter-spacing: 0.5px;
}

.footer-copy {
  font-size: 0.72rem;
  color: rgba(255,255,255,0.25);
  letter-spacing: 1px;
}
```

---

## JS GLOBAL — SCROLL REVEAL (IntersectionObserver)

```javascript
// === SCROLL REVEAL ===
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      revealObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.15, rootMargin: '0px 0px -60px 0px' });

document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));
```

---

## RESPONSIVIDADE MOBILE (max-width: 768px)

```css
@media (max-width: 768px) {
  .container { padding: 0 20px; }

  /* Navbar mobile */
  .nav-hamburger { display: flex; }
  .nav-links {
    position: fixed;
    top: 0; right: -100%;
    width: 80vw;
    height: 100vh;
    background: rgba(255,255,255,0.98);
    backdrop-filter: blur(16px);
    flex-direction: column;
    justify-content: center;
    gap: 32px;
    padding: 40px;
    transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: -10px 0 40px rgba(0,0,0,0.12);
  }
  .nav-links.open { right: 0; }
  .nav-links a { color: var(--negro) !important; font-size: 1rem !important; }

  /* Hambúrguer ativo (X) */
  .nav-hamburger.active span:nth-child(1) { transform: rotate(45deg) translate(5px, 5px); }
  .nav-hamburger.active span:nth-child(2) { opacity: 0; }
  .nav-hamburger.active span:nth-child(3) { transform: rotate(-45deg) translate(5px, -5px); }

  /* Hero */
  .hero-title { font-size: clamp(2.4rem, 10vw, 3.5rem); }
  .hero-btns { flex-direction: column; align-items: center; }

  /* Sobre */
  .sobre-card { padding: 36px 28px; }
  .sobre-stats { grid-template-columns: repeat(2, 1fr); }

  /* Produtos */
  .produtos-grid { grid-template-columns: 1fr; max-width: 420px; }
  .produto-card { height: 460px; }

  /* Galeria — scroll horizontal */
  .galeria-grid {
    grid-template-columns: repeat(3, 80vw);
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    -webkit-overflow-scrolling: touch;
    padding-bottom: 16px;
  }
  .galeria-item { scroll-snap-align: center; }

  /* Impacto */
  .impacto-grid { grid-template-columns: 1fr; gap: 40px; }
  .impacto-img { max-width: 300px; margin: 0 auto; }

  /* Canais */
  .canais-grid { grid-template-columns: 1fr; max-width: 400px; margin: 0 auto; }
  .canal-percent { font-size: 4rem; }

  /* Geral */
  #sobre, #produtos, #galeria, #impacto, #canais { padding: 80px 0; }
  .section-header { margin-bottom: 40px; }
}
```

---

## CHECKLIST FINAL — ANTES DE ENTREGAR

Verifique cada item antes de dizer que terminou:

- [ ] Hero: typewriter funciona, bolhas sobem, parallax suave ao scrollar
- [ ] Navbar: transparente no topo, branca após scroll, hambúrguer funciona no mobile
- [ ] Cards de produto: flip 3D funciona no hover, frente e verso sem bug de espelhamento
- [ ] Scroll reveal: todas as `.reveal` aparecem suavemente ao entrar na viewport
- [ ] Canais: números contam de 0 até o valor, barra preenche ao revelar
- [ ] Garrafa circular: está girando lentamente de forma contínua
- [ ] Footer: aparece completo, sem texto cortado
- [ ] Sem erros no console do Chrome (F12)
- [ ] Site abre corretamente com `file:///` (duplo clique no index.html)
- [ ] Em tela 1440px: nenhum elemento estoura para fora do container
- [ ] Em tela 375px (iPhone): todo conteúdo legível, hambúrguer funciona
- [ ] Imagens carregam (paths `./imagens_extraidas/imagem_0X.png` corretos)
- [ ] Google Fonts carregadas (precisa de conexão com internet)
