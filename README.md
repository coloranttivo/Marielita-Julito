<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>¡Destapa la Fiesta! 80 Años</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --rojo: #E31B23;
    --rojo-oscuro: #7A0E12;
    --crema: #FFF8E7;
    --dorado: #F2B705;
    --negro: #1A1010;
  }
  *{ box-sizing: border-box; margin:0; padding:0; }
  html,body{
    height:100%;
    width:100%;
    overflow-x:hidden;
    background: radial-gradient(ellipse at 50% 20%, var(--rojo-oscuro) 0%, var(--negro) 70%);
    font-family:'Poppins', sans-serif;
    color: var(--crema);
  }
  .stage{
    position:relative;
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    overflow:hidden;
    padding: 30px 12px;
  }

  /* Luces de disco de fondo */
  .disco-light{
    position:absolute;
    border-radius:50%;
    filter: blur(40px);
    opacity:0.35;
    animation: swirl 9s ease-in-out infinite;
    pointer-events:none;
  }
  .l1{ width:280px; height:280px; background:var(--dorado); top:5%; left:8%; animation-delay:0s;}
  .l2{ width:220px; height:220px; background:var(--rojo); bottom:10%; right:10%; animation-delay:2s;}
  .l3{ width:180px; height:180px; background:var(--crema); top:60%; left:20%; animation-delay:4s;}
  @keyframes swirl{
    0%,100%{ transform: translate(0,0) scale(1); }
    50%{ transform: translate(30px,-20px) scale(1.2); }
  }

  /* Siluetas de botella decorativas */
  .bottle-deco{
    position:absolute;
    width:60px;
    opacity:.18;
    filter: drop-shadow(0 0 10px rgba(0,0,0,.4));
    pointer-events:none;
  }
  .bd1{ top:8%; right:6%; transform: rotate(8deg); }
  .bd2{ bottom:6%; left:5%; transform: rotate(-10deg); width:50px; }

  /* ---------- PANTALLA 1: LA TAPA ---------- */
  #tapPrompt{
    position:relative;
    z-index:5;
    text-align:center;
    cursor:pointer;
    user-select:none;
    transition: opacity .6s ease, transform .6s ease;
  }
  #capSvg{
    width:170px;
    height:170px;
    animation: bob 2.4s ease-in-out infinite;
    filter: drop-shadow(0 12px 20px rgba(0,0,0,.55));
  }
  @keyframes bob{
    0%,100%{ transform: translateY(0) rotate(-3deg); }
    50%{ transform: translateY(-12px) rotate(3deg); }
  }
  #tapPrompt p{
    margin-top: 14px;
    font-size: 1rem;
    letter-spacing:.5px;
    opacity:.9;
  }
  #tapPrompt p b{ color: var(--dorado); }
  #tapPrompt .tap-title{
    font-family:'Pacifico', cursive;
    font-size: clamp(1.8rem, 9vw, 2.6rem);
    color: var(--dorado);
    margin-top: 18px;
    text-shadow: 0 4px 14px rgba(0,0,0,.4);
    letter-spacing: 0;
  }
  #tapPrompt .tap-sub{
    font-size: .9rem;
    opacity:.85;
    margin-top: 6px;
  }

  #tapPrompt.hide{
    opacity:0;
    transform: scale(1.3) translateY(-60px);
    pointer-events:none;
  }

  /* Burbujas */
  .bubble{
    position:absolute;
    bottom:-20px;
    background: rgba(255,248,231,.6);
    border-radius:50%;
    animation: rise linear forwards;
    pointer-events:none;
  }
  @keyframes rise{
    to{ transform: translateY(-110vh) translateX(var(--drift,0)); opacity:0; }
  }

  /* Confeti */
  .confetti{
    position:absolute;
    top:-10px;
    width:10px; height:14px;
    opacity:.95;
    animation: fall linear forwards;
    pointer-events:none;
  }
  @keyframes fall{
    to{ transform: translateY(110vh) rotate(720deg); opacity:.2; }
  }

  /* ---------- PANTALLA 2: INVITACION ---------- */
  #invite{
    position:absolute;
    z-index:4;
    width:min(92vw, 460px);
    max-height: 90vh;
    overflow-y:auto;
    text-align:center;
    opacity:0;
    transform: translateY(40px);
    transition: opacity .9s ease .2s, transform .9s ease .2s;
    background: linear-gradient(180deg, rgba(26,16,16,.6), rgba(26,16,16,.9));
    border: 2px solid var(--dorado);
    border-radius: 22px;
    padding: 0 0 24px;
  }
  #invite.show{
    opacity:1;
    transform: translateY(0);
  }
  .ribbon-top, .ribbon-bottom{
    width:100%;
    display:block;
  }
  .ribbon-bottom{ transform: scaleY(-1); }

  .invite-inner{ padding: 6px 26px 0; }

  .eyebrow-line{
    font-size:.85rem;
    letter-spacing:2px;
    color: var(--dorado);
    margin-bottom:6px;
  }
  #invite h1{
    font-family:'Pacifico', cursive;
    font-size: clamp(1.9rem, 8vw, 2.6rem);
    color: var(--crema);
    line-height:1.15;
    margin-bottom:14px;
    text-shadow: 0 4px 14px rgba(0,0,0,.4);
  }

  /* Marco de foto tipo Polaroid con "chapa" de tapa */
  .foto-frame{
    position:relative;
    width: 230px;
    height: 230px;
    margin: 6px auto 16px;
    background: var(--crema);
    padding: 8px 8px 8px;
    border-radius: 8px;
    box-shadow: 0 12px 24px rgba(0,0,0,.4);
    transform: rotate(-3deg);
  }
  .foto-frame .foto-slot{
    width:100%;
    height:100%;
    border: 2px dashed var(--rojo);
    border-radius:4px;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    color: var(--rojo-oscuro);
    font-size:.75rem;
    font-weight:600;
    padding: 6px;
    background: repeating-linear-gradient(45deg, rgba(227,27,35,.05) 0 10px, rgba(227,27,35,.09) 10px 20px);
  }
  .foto-pin{
    position:absolute;
    top:-16px; left:50%;
    transform: translateX(-50%) rotate(8deg);
    width:34px; height:34px;
    background: var(--rojo);
    border-radius:50%;
    box-shadow: 0 4px 8px rgba(0,0,0,.5), inset 0 -3px 0 rgba(0,0,0,.25);
    display:flex; align-items:center; justify-content:center;
  }
  .foto-pin::before{
    content:"";
    position:absolute;
    inset:5px;
    border-radius:50%;
    background: repeating-conic-gradient(var(--rojo) 0deg 15deg, var(--rojo-oscuro) 15deg 30deg);
    opacity:.5;
  }

  .nombres{
    font-size: 1.35rem;
    font-weight:800;
    color: var(--dorado);
    margin: 4px 0 4px;
  }
  .frase{
    font-size:.95rem;
    opacity:.9;
    margin-bottom: 6px;
    line-height:1.5;
  }

  .wave-divider{
    width:70%;
    margin: 14px auto;
    opacity:.8;
  }

  .detalles{
    display:grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px 14px;
    text-align:left;
    margin: 6px 0 6px;
    font-size:.92rem;
  }
  .detalles div{
    background: rgba(255,255,255,.06);
    border-left: 3px solid var(--rojo);
    padding: 8px 10px;
    border-radius: 6px;
  }
  .detalles div b{
    display:block;
    color: var(--dorado);
    font-size:.72rem;
    letter-spacing:.5px;
    margin-bottom:2px;
  }
  .dancers{
    display:flex;
    justify-content:center;
    gap:14px;
    margin: 14px 0 4px;
    font-size: 1.6rem;
  }
  .dancers span{
    display:inline-block;
    animation: baila 1s ease-in-out infinite;
  }
  .dancers span:nth-child(2){ animation-delay:.2s; }
  .dancers span:nth-child(3){ animation-delay:.4s; }
  .dancers span:nth-child(4){ animation-delay:.6s; }
  @keyframes baila{
    0%,100%{ transform: translateY(0) rotate(-6deg); }
    50%{ transform: translateY(-10px) rotate(6deg); }
  }

  .rsvp{
    margin-top: 14px;
    font-size:.85rem;
    opacity:.85;
  }
  .rsvp b{ color: var(--crema); }

  /* Botón de WhatsApp */
  .whatsapp-btn{
    display:inline-flex;
    align-items:center;
    gap:8px;
    margin-top: 12px;
    padding: 12px 22px;
    background: var(--rojo);
    color: var(--crema);
    font-weight:700;
    font-size:.92rem;
    text-decoration:none;
    border-radius: 30px;
    border: 2px solid var(--dorado);
    box-shadow: 0 8px 18px rgba(0,0,0,.4);
    transition: transform .2s ease;
  }
  .whatsapp-btn:active{ transform: scale(.96); }

  @media (prefers-reduced-motion: reduce){
    *{ animation: none !important; transition: none !important; }
  }
</style>
</head>
<body>
<audio id="bgMusic" loop preload="none">
  <source src="TU_CANCION.mp3" type="audio/mpeg">
</audio>

<div class="stage">
  <div class="disco-light l1"></div>
  <div class="disco-light l2"></div>
  <div class="disco-light l3"></div>

  <svg class="bottle-deco bd1" viewBox="0 0 100 260" xmlns="http://www.w3.org/2000/svg">
    <path d="M40 0 h20 v30 c0 8 10 10 10 22 v190 c0 10 -8 18 -18 18 h-4 c-10 0 -18 -8 -18 -18 V52 c0-12 10-14 10-22 Z" fill="#FFF8E7"/>
  </svg>
  <svg class="bottle-deco bd2" viewBox="0 0 100 260" xmlns="http://www.w3.org/2000/svg">
    <path d="M40 0 h20 v30 c0 8 10 10 10 22 v190 c0 10 -8 18 -18 18 h-4 c-10 0 -18 -8 -18 -18 V52 c0-12 10-14 10-22 Z" fill="#FFF8E7"/>
  </svg>

  <div id="tapPrompt">
    <svg id="capSvg" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
      <polygon id="capTeeth" fill="#E31B23" stroke="#7A0E12" stroke-width="2"/>
      <circle cx="100" cy="100" r="70" fill="#E31B23" stroke="#7A0E12" stroke-width="2"/>
      <circle cx="100" cy="100" r="62" fill="none" stroke="#FFF8E7" stroke-width="2" opacity="0.85"/>
      <circle cx="100" cy="100" r="58" fill="none" stroke="#FFF8E7" stroke-width="1" stroke-dasharray="3 5" opacity="0.6"/>
      <text x="100" y="112" text-anchor="middle" font-family="Pacifico, cursive" font-size="30" fill="#FFF8E7" transform="rotate(-8 100 100)">Cola</text>
      <ellipse cx="78" cy="70" rx="22" ry="10" fill="#FFF8E7" opacity="0.18" transform="rotate(-25 78 70)"/>
    </svg>
    <p class="tap-title">Coca-Cola Bailable</p>
    <p class="tap-sub">Toca la tapa para <b>destapar la fiesta</b> 🎉</p>
  </div>

  <div id="invite">
    <svg class="ribbon-top" viewBox="0 0 460 40" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M0 30 C 80 0, 160 40, 230 22 C 300 4, 380 40, 460 14 L460 0 L0 0 Z" fill="#E31B23"/>
    </svg>

    <div class="invite-inner">
      <h1>Coca-Cola Bailable</h1>

      <div class="foto-frame">
        <div class="foto-pin"></div>
        <div class="foto-slot">📷<br>Espacio para<br>su foto</div>
      </div>

      <div class="nombres">[NOMBRE 1] &amp; [NOMBRE 2]</div>
      <div class="frase">celebran 80 años a puro sabor, historias y muchísimo baile. Ven a destaparla con nosotros.</div>

      <svg class="wave-divider" viewBox="0 0 300 20" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q 25 0, 50 10 T 100 10 T 150 10 T 200 10 T 250 10 T 300 10" fill="none" stroke="#F2B705" stroke-width="3" stroke-linecap="round"/>
      </svg>

      <div class="dancers">
        <span>💃</span><span>🕺</span><span>🥤</span><span>🎶</span>
      </div>

      <div class="detalles">
        <div><b>FECHA</b>[DÍA, FECHA]</div>
        <div><b>HORA</b>[HORA DE INICIO]</div>
        <div><b>LUGAR</b>[NOMBRE DEL LUGAR]</div>
        <div><b>DIRECCIÓN</b>[DIRECCIÓN]</div>
      </div>

      <div class="rsvp">Confirma tu asistencia antes del <b>[FECHA LÍMITE]</b></div>
      <a class="whatsapp-btn" href="[LINK_DE_WHATSAPP]" target="_blank" rel="noopener">📲 Confirmar por WhatsApp</a>
    </div>

    <svg class="ribbon-bottom" viewBox="0 0 460 40" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M0 30 C 80 0, 160 40, 230 22 C 300 4, 380 40, 460 14 L460 0 L0 0 Z" fill="#E31B23"/>
    </svg>
  </div>
</div>

<script>
  // Genera los "dientes" de la tapa (corona dentada tipo tapa de gaseosa)
  (function drawCapTeeth(){
    const teeth = 24;
    const cx = 100, cy = 100;
    const outerR = 96, innerR = 82;
    let points = [];
    for(let i=0;i<teeth*2;i++){
      const angle = (Math.PI * 2 * i) / (teeth*2);
      const r = (i % 2 === 0) ? outerR : innerR;
      const x = cx + r * Math.cos(angle);
      const y = cy + r * Math.sin(angle);
      points.push(x.toFixed(1)+','+y.toFixed(1));
    }
    document.getElementById('capTeeth').setAttribute('points', points.join(' '));
  })();

  const tapPrompt = document.getElementById('tapPrompt');
  const invite = document.getElementById('invite');
  const stage = document.querySelector('.stage');
  let opened = false;

  function spawnBubbles(n){
    for(let i=0;i<n;i++){
      const b = document.createElement('div');
      b.className='bubble';
      const size = 6 + Math.random()*14;
      b.style.width = size+'px';
      b.style.height = size+'px';
      b.style.left = (10 + Math.random()*80)+'%';
      b.style.setProperty('--drift', (Math.random()*80-40)+'px');
      b.style.animationDuration = (2.5 + Math.random()*2.5)+'s';
      stage.appendChild(b);
      setTimeout(()=>b.remove(), 5200);
    }
  }

  function spawnConfetti(n){
    const colors = ['#E31B23','#F2B705','#FFF8E7','#7A0E12'];
    for(let i=0;i<n;i++){
      const c = document.createElement('div');
      c.className='confetti';
      c.style.left = Math.random()*100+'%';
      c.style.background = colors[Math.floor(Math.random()*colors.length)];
      c.style.animationDuration = (2 + Math.random()*2)+'s';
      c.style.transform = 'rotate('+(Math.random()*360)+'deg)';
      stage.appendChild(c);
      setTimeout(()=>c.remove(), 4200);
    }
  }

  tapPrompt.addEventListener('click', () => {
    if(opened) return;
    opened = true;
    const bgMusic = document.getElementById('bgMusic');
    bgMusic.volume = 0.6;
    bgMusic.play().catch(()=>{ /* el navegador puede bloquear el autoplay hasta el primer toque, esto ya cuenta como toque */ });
    spawnBubbles(18);
    spawnConfetti(50);
    tapPrompt.classList.add('hide');
    setTimeout(()=>{
      invite.classList.add('show');
    }, 250);
    const bubbleLoop = setInterval(()=>spawnBubbles(4), 1400);
    setTimeout(()=>clearInterval(bubbleLoop), 15000);
  });
</script>
</body>
</html>
