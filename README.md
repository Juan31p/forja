[index (1).html](https://github.com/user-attachments/files/29640142/index.1.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FORJA — Carta Digital</title>
<meta name="description" content="FORJA. Cortes al barril, shawarmas y nachos. Sin adornos, solo sabor.">

<!-- ============================================================
     FORJA — CARTA DIGITAL
     ------------------------------------------------------------
     GUÍA RÁPIDA DE EDICIÓN
     1) PRECIOS: buscar "$ __.___" y reemplazar por el valor real.
     2) LOGO REAL: buscar la sección "LOGO" en el HERO y reemplazar
        el bloque <div class="mark">…</div> por:
        <img src="logo-forja.png" alt="FORJA" class="logo-img">
     3) TEXTOS: todos los textos están en español, directamente en
        el HTML, buscables y editables sin tocar el CSS/JS.
     4) COLORES: variables centralizadas en :root (arriba del CSS).
     5) PRODUCTOS: cada tarjeta es un bloque <article class="dish">,
        se puede copiar/pegar para añadir más productos.
     ============================================================ -->

<style>
  /* =========================================================
     1. TOKENS DE MARCA
  ========================================================= */
  :root{
    --black:      #0D0D0D;
    --graphite:   #1A1A1A;
    --graphite-2: #151515;
    --steel:      #B6B6B6;
    --steel-dim:  #7A7A7A;
    --white:      #F5F5F4;
    --red:        #FF3B00;
    --red-dim:    rgba(255,59,0,.16);
    --red-line:   rgba(255,59,0,.35);

    --font-display: 'Rajdhani', 'Arial Narrow', sans-serif;
    --font-body:    'Inter', -apple-system, sans-serif;

    --cut: 22px;               /* tamaño del corte angular de firma */
    --border: 1px solid rgba(182,182,182,.14);
    --ease: cubic-bezier(.22,.61,.36,1);
  }

  *{ margin:0; padding:0; box-sizing:border-box; }

  html{ scroll-behavior:smooth; }

  body{
    background:var(--black);
    color:var(--white);
    font-family:var(--font-body);
    font-weight:400;
    line-height:1.6;
    overflow-x:hidden;
    -webkit-font-smoothing:antialiased;
  }

  /* Textura de fondo discreta: ruido + veta metálica sutil */
  body::before{
    content:"";
    position:fixed; inset:0;
    z-index:0;
    pointer-events:none;
    background-image:
      radial-gradient(1200px 700px at 15% -10%, rgba(255,59,0,.05), transparent 60%),
      radial-gradient(900px 600px at 110% 20%, rgba(182,182,182,.04), transparent 55%),
      repeating-linear-gradient(115deg, rgba(255,255,255,.012) 0px, rgba(255,255,255,.012) 1px, transparent 1px, transparent 3px);
    opacity:.9;
  }

  h1,h2,h3,h4{
    font-family:var(--font-display);
    font-weight:600;
    letter-spacing:.04em;
    text-transform:uppercase;
    color:var(--white);
  }

  a{ color:inherit; text-decoration:none; }
  ul{ list-style:none; }
  img{ max-width:100%; display:block; }

  .wrap{
    max-width:1180px;
    margin:0 auto;
    padding:0 clamp(20px,5vw,64px);
    position:relative;
    z-index:1;
  }

  .eyebrow{
    display:inline-flex;
    align-items:center;
    gap:10px;
    font-family:var(--font-display);
    font-size:.78rem;
    letter-spacing:.35em;
    text-transform:uppercase;
    color:var(--red);
  }
  .eyebrow::before{
    content:"";
    width:18px; height:1px;
    background:var(--red);
    display:inline-block;
  }

  /* corte angular de firma — esquina superior derecha cortada */
  .cut{
    clip-path: polygon(0 0, calc(100% - var(--cut)) 0, 100% var(--cut), 100% 100%, 0 100%);
  }
  .cut-inv{
    clip-path: polygon(var(--cut) 0, 100% 0, 100% 100%, 0 100%, 0 var(--cut));
  }

  /* =========================================================
     2. NAV
  ========================================================= */
  .nav{
    position:fixed;
    top:0; left:0; right:0;
    z-index:50;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:18px clamp(20px,5vw,64px);
    background:rgba(13,13,13,.72);
    backdrop-filter:blur(14px);
    -webkit-backdrop-filter:blur(14px);
    border-bottom:1px solid rgba(182,182,182,.08);
    transform:translateY(-110%);
    transition:transform .5s var(--ease);
  }
  .nav.show{ transform:translateY(0); }

  .nav-brand{
    display:flex; align-items:center; gap:10px;
    font-family:var(--font-display);
    font-size:1.05rem;
    letter-spacing:.28em;
  }
  .nav-brand .mark-mini{ width:16px; height:20px; }
  .nav-links{
    display:flex; gap:clamp(14px,3vw,34px);
    font-family:var(--font-display);
    font-size:.8rem;
    letter-spacing:.16em;
    text-transform:uppercase;
  }
  .nav-links a{
    color:var(--steel);
    position:relative;
    padding-bottom:4px;
    transition:color .3s var(--ease);
  }
  .nav-links a::after{
    content:"";
    position:absolute; left:0; bottom:0;
    width:0; height:1px;
    background:var(--red);
    transition:width .3s var(--ease);
  }
  .nav-links a:hover{ color:var(--white); }
  .nav-links a:hover::after{ width:100%; }
  .nav-links li.active-hide{ display:none; }
  @media (max-width:640px){ .nav-links{ display:none; } }

  /* =========================================================
     3. HERO
  ========================================================= */
  .hero{
    min-height:100svh;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    text-align:center;
    position:relative;
    padding:120px 24px 80px;
  }

  /* LOGO — reemplazar este bloque por <img> si tienes el archivo real */
  .mark{
    width:min(120px, 26vw);
    height:auto;
    margin:0 auto 28px;
    opacity:0;
    animation:reveal 1.1s var(--ease) .2s forwards;
  }
  .mark svg{ width:100%; height:auto; display:block; }

  .brand-name{
    font-size:clamp(2.6rem, 9vw, 5.2rem);
    letter-spacing:.34em;
    padding-left:.34em; /* compensa el letter-spacing final */
    line-height:1;
    opacity:0;
    animation:reveal 1.1s var(--ease) .45s forwards;
  }

  .brand-line{
    width:64px; height:2px;
    background:var(--red);
    margin:26px auto;
    opacity:0;
    animation:reveal 1s var(--ease) .7s forwards;
  }

  .hero-question{
    font-family:var(--font-display);
    font-weight:500;
    font-size:clamp(1.2rem, 3.4vw, 1.9rem);
    letter-spacing:.03em;
    text-transform:none;
    color:var(--steel);
    max-width:560px;
    opacity:0;
    animation:reveal 1s var(--ease) .95s forwards;
  }
  .hero-question em{
    font-style:normal;
    color:var(--white);
    border-bottom:1px solid var(--red-line);
  }

  .scroll-cue{
    position:absolute;
    bottom:38px; left:50%;
    transform:translateX(-50%);
    display:flex; flex-direction:column; align-items:center; gap:10px;
    opacity:0;
    animation:reveal .8s var(--ease) 1.4s forwards, floaty 2.6s ease-in-out 2.2s infinite;
  }
  .scroll-cue span{
    font-family:var(--font-display);
    font-size:.7rem;
    letter-spacing:.3em;
    color:var(--steel-dim);
  }
  .scroll-cue .line{ width:1px; height:34px; background:linear-gradient(var(--steel-dim), transparent); }

  @keyframes reveal{
    from{ opacity:0; transform:translateY(16px); }
    to{ opacity:1; transform:translateY(0); }
  }
  @keyframes floaty{
    0%,100%{ transform:translate(-50%,0); }
    50%{ transform:translate(-50%,6px); }
  }

  /* =========================================================
     4. SECCIÓN GENÉRICA / TÍTULOS
  ========================================================= */
  section{ position:relative; z-index:1; padding:110px 0; }
  .section-head{
    max-width:640px;
    margin-bottom:56px;
  }
  .section-head h2{
    font-size:clamp(2rem, 5vw, 3.2rem);
    margin-top:14px;
    letter-spacing:.05em;
  }
  .section-head p{
    margin-top:16px;
    color:var(--steel);
    font-size:1.02rem;
    max-width:480px;
  }

  .reveal-up{
    opacity:0;
    transform:translateY(28px);
    transition:opacity .8s var(--ease), transform .8s var(--ease);
  }
  .reveal-up.in{ opacity:1; transform:translateY(0); }

  /* =========================================================
     5. CATEGORÍAS (hero cards)
  ========================================================= */
  .categories{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:20px;
  }
  @media (max-width:860px){ .categories{ grid-template-columns:1fr; } }

  .cat-card{
    background:linear-gradient(160deg, var(--graphite) 0%, var(--graphite-2) 100%);
    border:var(--border);
    padding:38px 30px 32px;
    position:relative;
    transition:transform .45s var(--ease), border-color .45s var(--ease), box-shadow .45s var(--ease);
    display:flex; flex-direction:column; gap:18px;
  }
  .cat-card::before{
    content:"";
    position:absolute; inset:0;
    background:linear-gradient(160deg, var(--red-dim), transparent 55%);
    opacity:0;
    transition:opacity .45s var(--ease);
    pointer-events:none;
  }
  .cat-card:hover{
    transform:translateY(-6px);
    border-color:var(--red-line);
    box-shadow:0 24px 46px -22px rgba(0,0,0,.7);
  }
  .cat-card:hover::before{ opacity:1; }

  .cat-index{
    font-family:var(--font-display);
    font-size:.75rem;
    letter-spacing:.3em;
    color:var(--red);
  }
  .cat-card h3{
    font-size:1.6rem;
    letter-spacing:.08em;
  }
  .cat-card p{
    color:var(--steel);
    font-size:.92rem;
    flex-grow:1;
  }

  .btn{
    font-family:var(--font-display);
    font-size:.78rem;
    letter-spacing:.22em;
    text-transform:uppercase;
    color:var(--white);
    background:transparent;
    border:1px solid rgba(182,182,182,.3);
    padding:13px 22px;
    display:inline-flex;
    align-items:center;
    justify-content:center;
    gap:10px;
    cursor:pointer;
    transition:border-color .35s var(--ease), color .35s var(--ease), background .35s var(--ease);
    width:fit-content;
  }
  .btn:hover{
    border-color:var(--red);
    color:var(--red);
  }
  .btn::after{ content:"→"; transition:transform .35s var(--ease); }
  .btn:hover::after{ transform:translateX(4px); }

  .btn-ghost{
    border-color:transparent;
    color:var(--steel);
    padding:13px 0;
  }
  .btn-ghost:hover{ color:var(--red); }

  /* =========================================================
     6. PRODUCTOS
  ========================================================= */
  .dishes{
    display:grid;
    grid-template-columns:repeat(auto-fit, minmax(300px, 1fr));
    gap:22px;
  }

  .dish{
    background:var(--graphite);
    border:var(--border);
    padding:32px 28px;
    position:relative;
    overflow:hidden;
    transition:border-color .4s var(--ease), transform .4s var(--ease);
  }
  .dish::after{
    content:"";
    position:absolute;
    top:0; right:0;
    width:44px; height:44px;
    background:linear-gradient(135deg, transparent 49%, rgba(255,59,0,.5) 50%, transparent 51%);
    opacity:0;
    transition:opacity .4s var(--ease);
  }
  .dish:hover{
    border-color:var(--red-line);
    transform:translateY(-4px);
  }
  .dish:hover::after{ opacity:1; }

  .dish-head{
    display:flex;
    justify-content:space-between;
    align-items:baseline;
    gap:14px;
    margin-bottom:8px;
  }
  .dish-head h4{
    font-size:1.32rem;
    letter-spacing:.04em;
  }
  .dish-price{
    font-family:var(--font-display);
    font-size:1.05rem;
    color:var(--red);
    white-space:nowrap;
  }
  .dish-portion{
    font-size:.78rem;
    color:var(--steel-dim);
    letter-spacing:.08em;
    text-transform:uppercase;
    margin-bottom:16px;
  }
  .dish-includes{
    font-size:.68rem;
    letter-spacing:.18em;
    text-transform:uppercase;
    color:var(--red);
    margin-bottom:10px;
  }
  .dish-list{
    display:flex; flex-wrap:wrap;
    gap:8px 10px;
  }
  .dish-list li{
    font-size:.86rem;
    color:var(--steel);
    position:relative;
    padding-left:14px;
  }
  .dish-list li::before{
    content:"";
    position:absolute; left:0; top:9px;
    width:5px; height:1px;
    background:var(--steel-dim);
  }

  .dish-desc{
    color:var(--steel);
    font-size:.92rem;
    margin-bottom:14px;
  }

  /* =========================================================
     7. SALSAS — bloque especial
  ========================================================= */
  .sauces{
    background:radial-gradient(900px 400px at 20% 0%, rgba(255,59,0,.08), transparent 60%), var(--graphite-2);
    border:var(--border);
    padding:clamp(40px,6vw,72px);
    position:relative;
  }
  .sauces .section-head{ margin-bottom:44px; }
  .sauces-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:40px;
  }
  @media (max-width:700px){ .sauces-grid{ grid-template-columns:1fr; } }

  .sauce-group h4{
    font-size:.82rem;
    letter-spacing:.22em;
    color:var(--red);
    margin-bottom:20px;
    padding-bottom:12px;
    border-bottom:1px solid rgba(182,182,182,.14);
  }
  .sauce-group ul li{
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:14px 0;
    border-bottom:1px solid rgba(182,182,182,.08);
    font-size:1.02rem;
    color:var(--white);
    letter-spacing:.02em;
  }
  .sauce-group ul li span{
    font-size:.72rem;
    color:var(--steel-dim);
    letter-spacing:.14em;
    text-transform:uppercase;
  }
  .sauce-group ul li:last-child{ border-bottom:none; }

  /* =========================================================
     8. FOOTER
  ========================================================= */
  footer{
    padding:70px 0 50px;
    text-align:center;
    border-top:1px solid rgba(182,182,182,.08);
  }
  .footer-mark{ width:44px; margin:0 auto 18px; opacity:.85; }
  footer .brand-name{
    font-size:1.15rem;
    letter-spacing:.32em;
    padding-left:.32em;
    animation:none;
    opacity:1;
    margin-bottom:22px;
  }
  footer p{
    color:var(--steel-dim);
    font-size:.78rem;
    letter-spacing:.06em;
    margin-bottom:26px;
  }

  /* =========================================================
     9. UTILIDADES
  ========================================================= */
  .divider{
    height:1px;
    background:linear-gradient(90deg, transparent, rgba(182,182,182,.2), transparent);
    margin:110px 0;
  }

  @media (prefers-reduced-motion: reduce){
    *{ animation-duration:.01ms !important; animation-iteration-count:1 !important; transition-duration:.01ms !important; scroll-behavior:auto !important; }
  }

  :focus-visible{
    outline:1px solid var(--red);
    outline-offset:3px;
  }
</style>
</head>
<body>

<!-- ============================================================
     GOOGLE FONTS
     ============================================================ -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">

<!-- ============================================================
     NAV FIJA
     ============================================================ -->
<nav class="nav" id="mainNav">
  <a href="#top" class="nav-brand">
    <svg class="mark-mini" viewBox="0 0 100 130" xmlns="http://www.w3.org/2000/svg">
      <polygon points="10,0 100,0 78,26 34,26 34,54 68,54 50,78 34,78 34,130 10,130" fill="#F5F5F4"/>
    </svg>
    FORJA
  </a>
  <ul class="nav-links">
    <li><a href="#picadas">Picadas</a></li>
    <li><a href="#shawarmas">Shawarmas</a></li>
    <li><a href="#nachos">Nachos</a></li>
    <li><a href="#salsas">Salsas</a></li>
  </ul>
</nav>

<!-- ============================================================
     HERO
     ============================================================ -->
<header class="hero" id="top">
  <div class="wrap" style="display:flex;flex-direction:column;align-items:center;">

    <!-- LOGO: sustituir por <img src="logo-forja.png" alt="FORJA" class="mark"> si se dispone del archivo real -->
    <div class="mark">
      <svg viewBox="0 0 100 130" xmlns="http://www.w3.org/2000/svg">
        <polygon points="10,0 100,0 78,26 34,26 34,54 68,54 50,78 34,78 34,130 10,130"
                 fill="none" stroke="#FF3B00" stroke-width="2.5"/>
      </svg>
    </div>

    <h1 class="brand-name">FORJA</h1>
    <div class="brand-line"></div>

    <p class="hero-question">¿Con qué quieres <em>matar el hambre</em>?</p>
  </div>

  <div class="scroll-cue">
    <span>DESLIZA</span>
    <div class="line"></div>
  </div>
</header>

<!-- ============================================================
     SELECTOR DE CATEGORÍAS
     ============================================================ -->
<section id="categorias">
  <div class="wrap">
    <div class="section-head reveal-up">
      <span class="eyebrow">La Selección</span>
      <h2>Elige tu categoría</h2>
    </div>

    <div class="categories">

      <article class="cat-card reveal-up">
        <span class="cat-index">01</span>
        <h3>Picadas</h3>
        <p>Cortes al barril y acompañamientos clásicos, servidos para compartir.</p>
        <a href="#picadas" class="btn">Ver picadas</a>
      </article>

      <article class="cat-card reveal-up">
        <span class="cat-index">02</span>
        <h3>Shawarmas</h3>
        <p>Enrollados con vegetales frescos, queso y carne a elección.</p>
        <a href="#shawarmas" class="btn">Ver shawarmas</a>
      </article>

      <article class="cat-card reveal-up">
        <span class="cat-index">03</span>
        <h3>Nachos</h3>
        <p>Crujientes, cremosos y cargados con el sello de la casa.</p>
        <a href="#nachos" class="btn">Ver nachos</a>
      </article>

    </div>
  </div>
</section>

<div class="wrap"><div class="divider"></div></div>

<!-- ============================================================
     SECCIÓN 1 — PICADAS
     ============================================================ -->
<section id="picadas">
  <div class="wrap">
    <div class="section-head reveal-up">
      <span class="eyebrow">Sección 01</span>
      <h2>Picadas</h2>
      <p>Cortes al barril, acompañamientos clásicos.</p>
    </div>

    <div class="dishes">

      <article class="dish reveal-up">
        <div class="dish-head">
          <h4>La Breve</h4>
          <span class="dish-price">$ __.___</span>
        </div>
        <p class="dish-portion">Porción para 1 a 2 personas</p>
        <p class="dish-includes">Incluye</p>
        <ul class="dish-list">
          <li>Chorizo</li><li>Chicharrón</li>
          <li>Papa</li><li>Yuca</li><li>Bondiola</li>
        </ul>
      </article>

      <article class="dish reveal-up">
        <div class="dish-head">
          <h4>La Pesada</h4>
          <span class="dish-price">$ __.___</span>
        </div>
        <p class="dish-portion">Porción para 3 a 4 personas</p>
        <p class="dish-includes">Incluye</p>
        <ul class="dish-list">
          <li>Chorizo</li><li>Chicharrón</li>
          <li>Papa</li><li>Yuca</li><li>Bondiola</li>
        </ul>
      </article>

      <article class="dish reveal-up">
        <div class="dish-head">
          <h4>La Brutal</h4>
          <span class="dish-price">$ __.___</span>
        </div>
        <p class="dish-portion">Porción para 5 o más personas</p>
        <p class="dish-includes">Incluye</p>
        <ul class="dish-list">
          <li>Chorizo</li><li>Chicharrón</li>
          <li>Papa</li><li>Yuca</li><li>Bondiola</li>
        </ul>
      </article>

    </div>
  </div>
</section>

<div class="wrap"><div class="divider"></div></div>

<!-- ============================================================
     SECCIÓN 2 — SHAWARMAS
     ============================================================ -->
<section id="shawarmas">
  <div class="wrap">
    <div class="section-head reveal-up">
      <span class="eyebrow">Sección 02</span>
      <h2>Shawarmas</h2>
      <p>Enrollados con vegetales frescos, queso y carne a elección.</p>
    </div>

    <div class="dishes">
      <article class="dish reveal-up">
        <div class="dish-head">
          <h4>Shawarma FORJA</h4>
          <span class="dish-price">$ 25.000</span>
        </div>
        <p class="dish-desc">Carne de res o cerdo a elección, envuelta a la manera de la casa.</p>
        <p class="dish-includes">Incluye</p>
        <ul class="dish-list">
          <li>Lechuga</li><li>Tomate</li><li>Cebolla</li>
          <li>Queso</li><li>Carne de res o cerdo a elección</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<div class="wrap"><div class="divider"></div></div>

<!-- ============================================================
     SECCIÓN 3 — NACHOS
     ============================================================ -->
<section id="nachos">
  <div class="wrap">
    <div class="section-head reveal-up">
      <span class="eyebrow">Sección 03</span>
      <h2>Nachos</h2>
      <p>Crujientes, cremosos y cargados con el sello de la casa.</p>
    </div>

    <div class="dishes">
      <article class="dish reveal-up">
        <div class="dish-head">
          <h4>Nachos FORJA</h4>
          <span class="dish-price">$ __.___</span>
        </div>
        <p class="dish-includes">Incluye</p>
        <ul class="dish-list">
          <li>Nachos</li><li>Guacamole</li><li>Pico de gallo</li>
          <li>Queso crema</li><li>Yuquitas fritas</li><li>Carne de cerdo desmenuzada</li>
        </ul>
      </article>
    </div>
  </div>
</section>

<div class="wrap"><div class="divider"></div></div>

<!-- ============================================================
     SALSAS — BLOQUE ESPECIAL
     ============================================================ -->
<section id="salsas">
  <div class="wrap">
    <div class="sauces reveal-up">
      <div class="section-head">
        <span class="eyebrow">Complemento</span>
        <h2>Salsas</h2>
        <p>Finaliza tu elección con el golpe exacto de sabor.</p>
      </div>

      <div class="sauces-grid">
        <div class="sauce-group">
          <h4>Salsas de la casa</h4>
          <ul>
            <li>Tocineta <span>Casa</span></li>
            <li>Maní <span>Casa</span></li>
            <li>Wasakaka <span>Casa</span></li>
          </ul>
        </div>
        <div class="sauce-group">
          <h4>Salsas clásicas</h4>
          <ul>
            <li>Tomate <span>Clásica</span></li>
            <li>Barbacoa <span>Clásica</span></li>
            <li>Rosada <span>Clásica</span></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ============================================================
     FOOTER
     ============================================================ -->
<footer>
  <div class="wrap" style="display:flex;flex-direction:column;align-items:center;">
    <svg class="footer-mark" viewBox="0 0 100 130" xmlns="http://www.w3.org/2000/svg">
      <polygon points="10,0 100,0 78,26 34,26 34,54 68,54 50,78 34,78 34,130 10,130" fill="#B6B6B6"/>
    </svg>
    <h3 class="brand-name">FORJA</h3>
    <p>COCINA AL BARRIL — HECHO CON PRECISIÓN</p>
    <a href="#top" class="btn btn-ghost">Volver</a>
  </div>
</footer>

<!-- ============================================================
     JS — reveals, nav y smooth scroll
     ============================================================ -->
<script>
  // Nav: aparece tras superar la altura del hero
  const nav = document.getElementById('mainNav');
  const hero = document.getElementById('top');
  const navObserver = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      nav.classList.toggle('show', !entry.isIntersecting);
    });
  }, { threshold: 0.15 });
  navObserver.observe(hero);

  // Reveal on scroll
  const revealEls = document.querySelectorAll('.reveal-up');
  const revealObserver = new IntersectionObserver((entries)=>{
    entries.forEach((entry, i)=>{
      if(entry.isIntersecting){
        setTimeout(()=> entry.target.classList.add('in'), i * 70);
        revealObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.15, rootMargin: '0px 0px -60px 0px' });
  revealEls.forEach(el => revealObserver.observe(el));
</script>

</body>
</html>
