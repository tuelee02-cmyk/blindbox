<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dinnemon - Master Duong</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Nunito:wght@400;700;900&display=swap');
:root { --gold:#FFD700; --dark:#0d0820; }
*{margin:0;padding:0;box-sizing:border-box;}
body {
  min-height:100vh; background:var(--dark);
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  font-family:'Nunito',sans-serif; overflow:hidden;
  background-image:
    radial-gradient(ellipse 80% 60% at 50% 0%,#2a0a5e44 0%,transparent 70%),
    repeating-linear-gradient(0deg,transparent,transparent 40px,rgba(255,255,255,.015) 40px,rgba(255,255,255,.015) 41px),
    repeating-linear-gradient(90deg,transparent,transparent 40px,rgba(255,255,255,.015) 40px,rgba(255,255,255,.015) 41px);
}
.stars{position:fixed;inset:0;pointer-events:none;}
.star{position:absolute;border-radius:50%;background:white;opacity:0;animation:twinkle var(--d) var(--dl) infinite;}
@keyframes twinkle{0%,100%{opacity:0;transform:scale(0)}50%{opacity:.9;transform:scale(1)}}
h1{font-family:'Bangers',cursive;font-size:2.4rem;letter-spacing:4px;color:var(--gold);
   text-shadow:0 0 30px #FFD70099,3px 3px 0 #550088;margin-bottom:6px;z-index:10;text-align:center;}
.subtitle{color:#8877aa;font-size:.8rem;margin-bottom:32px;z-index:10;letter-spacing:2px;text-transform:uppercase;}
.scene{perspective:1200px;z-index:10;position:relative;}
.pack-wrapper{position:relative;width:300px;height:440px;cursor:grab;user-select:none;}
.pack{position:absolute;inset:0;border-radius:16px;overflow:hidden;box-shadow:0 30px 80px #7700aa66,0 0 0 1.5px #ffffff33;}
.pack-svg{position:absolute;inset:0;width:100%;height:100%;}
.pack-sheen{position:absolute;inset:0;background:linear-gradient(115deg,transparent 20%,rgba(255,255,255,.3) 50%,transparent 80%);
  transform:translateX(-120%);animation:sheen 3.5s ease-in-out infinite;pointer-events:none;border-radius:16px;}
@keyframes sheen{0%{transform:translateX(-120%)}45%,100%{transform:translateX(220%)}}
.tear-line{position:absolute;top:27%;left:0;right:0;height:2px;
  background:repeating-linear-gradient(90deg,rgba(255,255,255,.7) 0 8px,transparent 8px 16px);
  pointer-events:none;z-index:5;}
.tear-hint{position:absolute;top:calc(27% - 22px);width:100%;text-align:center;font-size:.6rem;
  color:rgba(255,255,255,.8);letter-spacing:3px;text-transform:uppercase;pointer-events:none;z-index:6;
  animation:pulse 1.5s ease-in-out infinite;}
@keyframes pulse{0%,100%{opacity:.4}50%{opacity:1}}
.pack-top{position:absolute;top:0;left:0;right:0;height:27%;border-radius:16px 16px 0 0;overflow:hidden;transform-origin:top center;z-index:20;cursor:grab;}
.pack-top-svg{width:100%;height:100%;display:block;}

/* CARD */
.card-reveal{position:absolute;inset:0;border-radius:16px;opacity:0;pointer-events:none;
  transform:scale(.9) rotateY(15deg);transition:opacity .6s ease,transform .6s cubic-bezier(.17,.67,.3,1.3);}
.card-reveal.visible{opacity:1;transform:scale(1) rotateY(0deg);pointer-events:all;}
.card-outer{position:absolute;inset:0;border-radius:16px;padding:8px;display:flex;flex-direction:column;}
.card-outer::before{content:'';position:absolute;inset:0;border-radius:16px;
  background:conic-gradient(from var(--ha,0deg),#ff000055,#ff880055,#ffff0055,#00ff0055,#00ffff55,#0066ff55,#aa00ff55,#ff000055);
  opacity:0;transition:opacity .3s;pointer-events:none;z-index:50;mix-blend-mode:screen;}
.card-outer:hover::before{opacity:.6;animation:holoSpin 4s linear infinite;}
@keyframes holoSpin{to{--ha:360deg;}}
@property --ha{syntax:'<angle>';initial-value:0deg;inherits:false;}
.card-inner-wrap{flex:1;border-radius:10px;padding:10px 10px 8px;position:relative;overflow:hidden;display:flex;flex-direction:column;gap:5px;}
.card-inner-wrap.fire{background:linear-gradient(170deg,#FF6B1A 0%,#FFC200 40%,#FF3300 70%,#FF6B1A 100%);box-shadow:inset 0 0 30px rgba(0,0,0,.3);}
.card-inner-wrap.water{background:linear-gradient(170deg,#1a6eff 0%,#00d4ff 40%,#1a3dcc 70%,#003399 100%);box-shadow:inset 0 0 30px rgba(0,0,0,.3);}
.card-inner-wrap.grass{background:linear-gradient(170deg,#1db954 0%,#b5ff2e 40%,#007733 70%,#1db954 100%);box-shadow:inset 0 0 30px rgba(0,0,0,.3);}
.card-pattern{position:absolute;inset:0;opacity:.12;pointer-events:none;}
.card-inner-wrap::after{content:'';position:absolute;inset:4px;border-radius:7px;border:2px solid rgba(255,255,255,.45);pointer-events:none;z-index:5;}
.card-header{display:flex;align-items:flex-start;justify-content:space-between;z-index:6;padding:0 4px;}
.card-name-block{display:flex;flex-direction:column;}
.card-name{font-family:'Bangers',cursive;font-size:1.4rem;color:white;line-height:1.05;text-shadow:1px 1px 0 rgba(0,0,0,.5);letter-spacing:1px;}
.card-stage{font-size:.5rem;font-weight:900;letter-spacing:2px;color:rgba(255,255,255,.8);text-transform:uppercase;}
.card-hp-block{text-align:right;}
.card-hp{font-family:'Bangers',cursive;font-size:1.5rem;color:white;text-shadow:1px 1px 0 rgba(0,0,0,.5);}
.hp-label{font-size:.5rem;font-weight:900;color:rgba(255,255,255,.7);letter-spacing:1px;}
.card-art-frame{border:3px solid rgba(255,255,255,.5);border-radius:6px;background:rgba(0,0,0,.2);overflow:hidden;position:relative;z-index:6;height:148px;flex-shrink:0;}
.card-art-frame svg{width:100%;height:100%;display:block;}
.art-type-strip{position:absolute;bottom:0;left:0;right:0;background:rgba(0,0,0,.45);font-size:.5rem;font-weight:900;letter-spacing:2px;color:rgba(255,255,255,.9);text-align:center;padding:2px 0;text-transform:uppercase;}
.card-flavor-box{border:1.5px solid rgba(255,255,255,.3);border-radius:5px;background:rgba(0,0,0,.2);padding:5px 8px;font-size:.56rem;font-style:italic;color:rgba(255,255,255,.9);line-height:1.45;z-index:6;flex-shrink:0;}
.card-attacks{z-index:6;display:flex;flex-direction:column;gap:3px;}
.attack{background:rgba(0,0,0,.25);border-radius:5px;padding:5px 8px;display:flex;align-items:center;gap:6px;border:1px solid rgba(255,255,255,.2);}
.attack-energy{display:flex;gap:2px;flex-shrink:0;}
.energy{width:16px;height:16px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:.55rem;font-weight:900;border:1.5px solid rgba(255,255,255,.5);flex-shrink:0;}
.energy.fire{background:radial-gradient(#FF8C00,#FF3300);color:white;}
.energy.water{background:radial-gradient(#00BFFF,#0044FF);color:white;}
.energy.grass{background:radial-gradient(#7FFF00,#228B22);color:white;}
.energy.colorless{background:radial-gradient(#DDD,#999);color:#333;}
.attack-name{flex:1;font-weight:900;font-size:.68rem;color:white;line-height:1.2;}
.attack-desc{font-size:.52rem;color:rgba(255,255,255,.7);font-style:italic;}
.attack-dmg{font-family:'Bangers',cursive;font-size:1.3rem;color:white;text-shadow:1px 1px 0 rgba(0,0,0,.5);flex-shrink:0;}
.card-footer{display:flex;justify-content:space-between;align-items:center;padding:0 4px;z-index:6;margin-top:auto;}
.card-weakness{font-size:.5rem;color:rgba(255,255,255,.7);}
.card-weakness span{font-weight:900;}
.card-number{font-size:.5rem;color:rgba(255,255,255,.6);font-style:italic;}
.card-rarity{font-size:.9rem;}
.card-holo{position:absolute;inset:0;border-radius:10px;background:linear-gradient(115deg,transparent 30%,rgba(255,255,255,.18) 50%,transparent 70%);pointer-events:none;z-index:10;transform:translateX(-100%);animation:cardSheen 4s ease-in-out infinite;}
@keyframes cardSheen{0%{transform:translateX(-100%)}40%,100%{transform:translateX(200%)}}
.reset-btn{margin-top:24px;z-index:10;background:none;border:2px solid var(--gold);color:var(--gold);font-family:'Bangers',cursive;font-size:1.1rem;letter-spacing:3px;padding:10px 32px;border-radius:50px;cursor:pointer;opacity:0;transform:translateY(8px);transition:opacity .4s,transform .4s,background .2s;pointer-events:none;text-shadow:0 0 10px #FFD70066;box-shadow:0 0 20px #FFD70033;}
.reset-btn:hover{background:rgba(255,215,0,.12);}
.reset-btn.show{opacity:1;transform:translateY(0);pointer-events:all;}
.conf{position:fixed;width:8px;height:8px;border-radius:2px;opacity:0;pointer-events:none;z-index:999;}
</style>
</head>
<body>
<div class="stars" id="stars"></div>
<h1>⚡ DINNEMON ⚡</h1>
<p class="subtitle">Master Duong — your dinner awaits. Choose your fate.</p>
<div class="scene">
<div class="pack-wrapper" id="packWrapper">

  <!-- CARD behind pack -->
  <div class="card-reveal" id="cardReveal">
    <div class="card-outer" id="cardOuter">
      <div class="card-inner-wrap" id="cardInnerWrap">
        <svg class="card-pattern" id="cardPattern" xmlns="http://www.w3.org/2000/svg"></svg>
        <div class="card-holo"></div>
        <div class="card-header">
          <div class="card-name-block">
            <span class="card-stage" id="cStage">BASIC</span>
            <span class="card-name" id="cName">???</span>
          </div>
          <div class="card-hp-block">
            <div class="hp-label">HP</div>
            <div class="card-hp" id="cHP">90</div>
          </div>
        </div>
        <div class="card-art-frame" id="artFrame">
          <svg id="cardArtSVG" viewBox="0 0 260 148" xmlns="http://www.w3.org/2000/svg"></svg>
          <div class="art-type-strip" id="artStrip">RESTAURANT POKEMON</div>
        </div>
        <div class="card-flavor-box" id="cFlavor">...</div>
        <div class="card-attacks" id="cAttacks"></div>
        <div class="card-footer">
          <div class="card-weakness" id="cWeakness">WEAKNESS: <span>—</span></div>
          <div class="card-number" id="cNumber">No. 001</div>
          <div class="card-rarity" id="cRarity">★</div>
        </div>
      </div>
    </div>
  </div>

  <!-- PACK -->
  <div class="pack" id="pack">
    <svg class="pack-svg" viewBox="0 0 300 440" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="packGrad" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#8800FF"/>
          <stop offset="30%" stop-color="#3300CC"/>
          <stop offset="55%" stop-color="#0055FF"/>
          <stop offset="80%" stop-color="#00AAFF"/>
          <stop offset="100%" stop-color="#FF00AA"/>
        </linearGradient>
        <linearGradient id="packOvl" x1="100%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="#FF006699"/>
          <stop offset="50%" stop-color="#7700AA55"/>
          <stop offset="100%" stop-color="#0044FF99"/>
        </linearGradient>
        <pattern id="pDiag" patternUnits="userSpaceOnUse" width="20" height="20" patternTransform="rotate(45)">
          <line x1="0" y1="0" x2="0" y2="20" stroke="rgba(255,255,255,0.06)" stroke-width="8"/>
        </pattern>
        <pattern id="pDots" patternUnits="userSpaceOnUse" width="12" height="12">
          <circle cx="6" cy="6" r="1.5" fill="rgba(255,255,255,0.07)"/>
        </pattern>
        <filter id="glow"><feGaussianBlur stdDeviation="3" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
        <filter id="softglow"><feGaussianBlur stdDeviation="6" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
      </defs>

      <!-- Base -->
      <rect width="300" height="440" rx="16" fill="url(#packGrad)"/>
      <rect width="300" height="440" rx="16" fill="url(#packOvl)"/>
      <rect width="300" height="440" rx="16" fill="url(#pDiag)"/>
      <rect width="300" height="440" rx="16" fill="url(#pDots)"/>

      <!-- Borders -->
      <rect x="6" y="6" width="288" height="428" rx="12" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="2"/>
      <rect x="11" y="11" width="278" height="418" rx="9" fill="none" stroke="rgba(255,255,255,0.1)" stroke-width="1"/>

      <!-- Glow blobs -->
      <ellipse cx="150" cy="220" rx="130" ry="170" fill="rgba(180,0,255,0.12)"/>
      <ellipse cx="50" cy="80" rx="90" ry="70" fill="rgba(0,100,255,0.18)"/>
      <ellipse cx="250" cy="370" rx="90" ry="70" fill="rgba(255,0,100,0.12)"/>

      <!-- === POKEBALL === -->
      <g transform="translate(150,260)" filter="url(#softglow)">
        <circle cx="0" cy="0" r="85" fill="none" stroke="rgba(255,255,255,0.06)" stroke-width="18"/>
        <circle cx="0" cy="0" r="72" fill="rgba(0,0,0,0.28)" stroke="rgba(255,255,255,0.18)" stroke-width="2.5"/>
        <!-- Red top -->
        <path d="M-72,0 A72,72 0 0,1 72,0 Z" fill="rgba(210,30,30,0.55)"/>
        <!-- White bottom -->
        <path d="M-72,0 A72,72 0 0,0 72,0 Z" fill="rgba(255,255,255,0.12)"/>
        <!-- Band -->
        <line x1="-72" y1="0" x2="72" y2="0" stroke="rgba(255,255,255,0.35)" stroke-width="6"/>
        <!-- Center button outer ring -->
        <circle cx="0" cy="0" r="17" fill="rgba(0,0,0,0.45)" stroke="rgba(255,255,255,0.45)" stroke-width="3.5"/>
        <!-- Center button inner -->
        <circle cx="0" cy="0" r="11" fill="rgba(200,200,200,0.15)" stroke="rgba(255,255,255,0.55)" stroke-width="2"/>
        <!-- Shine -->
        <circle cx="-4" cy="-4" r="4" fill="rgba(255,255,255,0.55)"/>
      </g>

      <!-- Decorative corner ornaments -->
      <!-- TL -->
      <g transform="translate(24,24)" fill="none" stroke="rgba(255,255,255,.3)" stroke-width="1.5">
        <path d="M0,20 L0,0 L20,0"/>
        <path d="M4,16 L4,4 L16,4"/>
        <circle cx="4" cy="4" r="2" fill="rgba(255,255,255,.4)"/>
      </g>
      <!-- TR -->
      <g transform="translate(276,24)" fill="none" stroke="rgba(255,255,255,.3)" stroke-width="1.5">
        <path d="M0,0 L20,0 L20,20"/>
        <path d="M4,4 L16,4 L16,16"/>
        <circle cx="16" cy="4" r="2" fill="rgba(255,255,255,.4)"/>
      </g>
      <!-- BL -->
      <g transform="translate(24,416)" fill="none" stroke="rgba(255,255,255,.3)" stroke-width="1.5">
        <path d="M0,0 L0,20 L20,20"/>
        <path d="M4,4 L4,16 L16,16"/>
        <circle cx="4" cy="16" r="2" fill="rgba(255,255,255,.4)"/>
      </g>
      <!-- BR -->
      <g transform="translate(276,416)" fill="none" stroke="rgba(255,255,255,.3)" stroke-width="1.5">
        <path d="M20,0 L20,20 L0,20"/>
        <path d="M16,4 L16,16 L4,16"/>
        <circle cx="16" cy="16" r="2" fill="rgba(255,255,255,.4)"/>
      </g>

      <!-- Energy symbols -->
      <g opacity=".4">
        <circle cx="38" cy="158" r="15" fill="#FF6600" stroke="rgba(255,255,255,.3)" stroke-width="1.5"/>
        <text x="38" y="163" text-anchor="middle" font-size="14">🔥</text>
        <circle cx="262" cy="158" r="15" fill="#0055FF" stroke="rgba(255,255,255,.3)" stroke-width="1.5"/>
        <text x="262" y="163" text-anchor="middle" font-size="14">💧</text>
        <circle cx="38" cy="320" r="15" fill="#00AA33" stroke="rgba(255,255,255,.3)" stroke-width="1.5"/>
        <text x="38" y="325" text-anchor="middle" font-size="14">🌿</text>
        <circle cx="262" cy="320" r="15" fill="#CC00AA" stroke="rgba(255,255,255,.3)" stroke-width="1.5"/>
        <text x="262" y="325" text-anchor="middle" font-size="14">✨</text>
      </g>

      <!-- Star sparkles -->
      <g fill="rgba(255,255,255,.55)" filter="url(#glow)">
        <polygon points="28,55 30.5,47.5 33,55 40.5,55 35,59.5 37,67 30.5,62.5 24,67 26,59.5 20.5,55" transform="scale(.75)"/>
        <polygon points="275,65 277,59 279,65 285,65 281,69 282.5,75.5 277,71.5 271.5,75.5 273,69 269,65" transform="scale(.7)"/>
        <polygon points="42,390 44,384 46,390 52,390 48,394 49.5,400 44,396 38.5,400 40,394 36,390" transform="scale(.6)"/>
        <polygon points="258,378 260,372 262,378 268,378 264,382 265.5,388 260,384 254.5,388 256,382 252,378" transform="scale(.6)"/>
      </g>

      <!-- Title badge -->
      <g transform="translate(150,96)">
        <rect x="-95" y="-26" width="190" height="52" rx="9" fill="rgba(0,0,0,0.45)" stroke="rgba(255,255,255,.3)" stroke-width="1.5"/>
        <rect x="-93" y="-24" width="186" height="48" rx="7" fill="none" stroke="rgba(255,255,255,.1)" stroke-width="1"/>
        <text x="0" y="-7" text-anchor="middle" font-family="Bangers,cursive" font-size="24" fill="white" letter-spacing="3">DINNEMON</text>
        <text x="0" y="13" text-anchor="middle" font-family="sans-serif" font-size="8" fill="rgba(255,255,255,.65)" letter-spacing="4">COLLECTOR SERIES</text>
      </g>

      <!-- Big ??? -->
      <text x="150" y="278" text-anchor="middle" font-family="Bangers,cursive" font-size="82" fill="rgba(255,255,255,0.1)" letter-spacing="-4">???</text>

      <!-- Bottom label -->
      <g transform="translate(150,406)">
        <rect x="-72" y="-14" width="144" height="24" rx="6" fill="rgba(0,0,0,.4)" stroke="rgba(255,255,255,.2)" stroke-width="1"/>
        <text x="0" y="4" text-anchor="middle" font-family="sans-serif" font-size="7.5" fill="rgba(255,255,255,.55)" letter-spacing="2">HANOI RESTAURANT SERIES</text>
      </g>
    </svg>
    <div class="pack-sheen"></div>
    <div class="tear-line"></div>
    <div class="tear-hint">↑ DRAG UP TO TEAR ↑</div>
  </div>

  <!-- TOP FLAP -->
  <div class="pack-top" id="packTop">
    <svg class="pack-top-svg" viewBox="0 0 300 119" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="tG" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#9900DD"/>
          <stop offset="50%" stop-color="#4400FF"/>
          <stop offset="100%" stop-color="#0066FF"/>
        </linearGradient>
        <pattern id="tDiag" patternUnits="userSpaceOnUse" width="20" height="20" patternTransform="rotate(45)">
          <line x1="0" y1="0" x2="0" y2="20" stroke="rgba(255,255,255,0.07)" stroke-width="8"/>
        </pattern>
      </defs>
      <rect width="300" height="119" rx="16" fill="url(#tG)"/>
      <rect width="300" height="119" rx="16" fill="url(#tDiag)"/>
      <rect x="0" y="100" width="300" height="19" fill="url(#tG)"/>
      <rect x="0" y="100" width="300" height="19" fill="url(#tDiag)"/>
      <!-- Stars on flap -->
      <polygon points="22,18 25,10 28,18 36,18 30,23 32,31 25,26 18,31 20,23 14,18" fill="rgba(255,255,255,.4)"/>
      <polygon points="278,18 281,10 284,18 292,18 286,23 288,31 281,26 274,31 276,23 270,18" fill="rgba(255,255,255,.4)"/>
      <polygon points="150,8 152,3 154,8 159,8 155,11 156.5,16 152,13 147.5,16 149,11 145,8" fill="rgba(255,255,255,.5)"/>
      <!-- Center badge -->
      <rect x="88" y="28" width="124" height="48" rx="8" fill="rgba(0,0,0,.38)" stroke="rgba(255,255,255,.28)" stroke-width="1.5"/>
      <text x="150" y="50" text-anchor="middle" font-family="Bangers,cursive" font-size="20" fill="white" letter-spacing="2">DINNEMON</text>
      <text x="150" y="67" text-anchor="middle" font-family="sans-serif" font-size="7" fill="rgba(255,255,255,.7)" letter-spacing="3">DRAG UP TO TEAR</text>
      <!-- Torn bottom edge -->
      <path d="M0,106 L0,119 L10,112 L20,119 L32,110 L44,119 L56,111 L68,118 L80,110 L92,119 L104,109 L116,118 L128,112 L140,119 L152,108 L164,118 L176,112 L188,119 L200,109 L212,118 L224,111 L236,119 L248,110 L260,119 L272,111 L284,119 L294,112 L300,119 L300,106 Z"
        fill="#4400FF" opacity=".95"/>
    </svg>
  </div>

</div>
</div>
<button class="reset-btn" id="resetBtn" onclick="resetPack()">↺ DRAW AGAIN</button>

<script>
const restaurants = [
  {
    name:"POP QUIZ Irish Beer", stage:"LEGENDARY PUB",
    type:"fire", typeName:"FIRE", hp:110, number:"No. 047",
    flavor:"When the trivia night begins, all challengers tremble. Its golden pints are said to grant +10 INT for the duration of the quiz.",
    weakness:"Water x2",
    attacks:[
      {energies:["fire"],name:"Pint of the Day",desc:"Restore 20HP to self",dmg:"40"},
      {energies:["fire","fire","colorless"],name:"Quiz Master's Fury",desc:"Flip a coin; if heads, opponent is confused",dmg:"90"},
    ],
    rarity:"★★★★",
    art: drawIrishPub
  },
  {
    name:"BAO WOW", stage:"STAGE 1",
    type:"water", typeName:"WATER", hp:90, number:"No. 023",
    flavor:"Pillowy-soft bao buns that have evolved beyond mere sustenance. Opponents often forget what they were doing mid-bite.",
    weakness:"Lightning x2",
    attacks:[
      {energies:["water"],name:"Steamed Surprise",desc:"",dmg:"30"},
      {energies:["water","water"],name:"Bao Blast",desc:"Discard 1 water energy; does 30 more damage",dmg:"70"},
    ],
    rarity:"★★★",
    art: drawBaoWow
  },
  {
    name:"COM NHA VIET NAM", stage:"BASIC",
    type:"grass", typeName:"GRASS", hp:100, number:"No. 001",
    flavor:"A timeless force of nature. Its Pho Power heals the soul, and its rice plates contain memories of home.",
    weakness:"Fire x2",
    attacks:[
      {energies:["grass"],name:"Pho Power",desc:"Heal 20 damage from this Pokemon",dmg:"35"},
      {energies:["grass","grass","colorless"],name:"Com Tam Crush",desc:"",dmg:"80"},
    ],
    rarity:"★★★",
    art: drawComNha
  },
];

function drawIrishPub(svg){
  svg.innerHTML=`
  <defs>
    <linearGradient id="skyG" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0d0520"/><stop offset="100%" stop-color="#3d1200"/>
    </linearGradient>
    <radialGradient id="beerG" cx="50%" cy="50%" r="50%">
      <stop offset="0%" stop-color="#FFD700" stop-opacity=".5"/><stop offset="100%" stop-color="#FF8800" stop-opacity="0"/>
    </radialGradient>
  </defs>
  <rect width="260" height="148" fill="url(#skyG)"/>
  <ellipse cx="130" cy="80" rx="70" ry="55" fill="url(#beerG)"/>
  <!-- Floor -->
  <rect x="0" y="112" width="260" height="36" fill="#2a0d00"/>
  <rect x="0" y="110" width="260" height="5" fill="#4a1a00"/>
  ${[114,121,128,135,142].map(y=>`<rect x="0" y="${y}" width="260" height="3" fill="rgba(100,40,0,.4)"/>`).join('')}
  <!-- Back shelf -->
  <rect x="8" y="34" width="244" height="5" fill="#5a2800"/>
  <!-- Bottles -->
  ${[22,44,66,88,110,132,154,176,198,220].map((x,i)=>`
    <rect x="${x}" y="${18+(i%4)*3}" width="13" height="19" rx="2" fill="${['#1a4a00','#8B0000','#8B6914','#003366','#4a1a00','#006633','#660033','#1a1a44','#004444','#441a00'][i]}" opacity=".85"/>
    <rect x="${x+1}" y="${18+(i%4)*3}" width="11" height="7" rx="1" fill="rgba(255,255,255,.18)"/>
    <rect x="${x+4}" y="${18+(i%4)*3+7}" width="5" height="8" rx="1" fill="rgba(255,255,255,.06)"/>
  `).join('')}
  <!-- Pint glow -->
  <ellipse cx="130" cy="88" rx="42" ry="32" fill="rgba(255,200,0,.18)"/>
  <!-- Pint glass -->
  <g transform="translate(108,58)">
    <path d="M8,0 L4,52 L40,52 L36,0 Z" fill="rgba(255,215,0,.8)" stroke="rgba(255,255,255,.35)" stroke-width="1.5"/>
    <path d="M9,4 L5,52 L39,52 L35,4 Z" fill="#F5A623" opacity=".9"/>
    <ellipse cx="22" cy="4" rx="14" ry="7" fill="rgba(255,255,255,.95)"/>
    <ellipse cx="14" cy="2" rx="6" ry="5" fill="rgba(255,255,255,.8)"/>
    <ellipse cx="30" cy="3" rx="5" ry="4" fill="rgba(255,255,255,.75)"/>
    <circle cx="13" cy="24" r="2" fill="rgba(255,255,255,.35)"/>
    <circle cx="29" cy="37" r="1.5" fill="rgba(255,255,255,.3)"/>
    <path d="M10,7 L8,48" stroke="rgba(255,255,255,.3)" stroke-width="3" stroke-linecap="round"/>
    <path d="M36,14 Q50,14 50,24 Q50,34 36,34" fill="none" stroke="rgba(255,255,255,.25)" stroke-width="4"/>
  </g>
  <!-- Shamrocks -->
  ${[[20,92,.55],[196,64,.5],[240,100,.45]].map(([x,y,s])=>`
  <g transform="translate(${x},${y}) scale(${s})" opacity=".65">
    <ellipse cx="0" cy="-9" rx="7" ry="9" fill="#00cc44"/>
    <ellipse cx="-8" cy="0" rx="7" ry="9" fill="#00cc44" transform="rotate(-35)"/>
    <ellipse cx="8" cy="0" rx="7" ry="9" fill="#00cc44" transform="rotate(35)"/>
    <line x1="0" y1="0" x2="0" y2="16" stroke="#009933" stroke-width="2.5"/>
  </g>`).join('')}
  <!-- Harp silhouette left -->
  <g transform="translate(22,50)" opacity=".3" fill="none" stroke="rgba(255,215,0,.6)" stroke-width="1.5">
    <path d="M0,50 Q-5,20 8,0 Q20,0 20,50 Z"/>
    <path d="M0,50 L20,50"/>
    ${[8,16,22,27,31,34,36].map((y,i)=>`<line x1="${2+i*.5}" y1="${y}" x2="${18-i*.5}" y2="${y}"/>`).join('')}
  </g>
  <!-- Stars -->
  <circle cx="200" cy="18" r="1.5" fill="rgba(255,255,255,.7)"/>
  <circle cx="52" cy="14" r="1" fill="rgba(255,255,255,.5)"/>
  <circle cx="220" cy="46" r="1" fill="rgba(255,255,255,.6)"/>
  <circle cx="170" cy="22" r="1" fill="rgba(255,255,255,.4)"/>`;
}

function drawBaoWow(svg){
  svg.innerHTML=`
  <defs>
    <linearGradient id="bg2" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#001440"/><stop offset="100%" stop-color="#002255"/>
    </linearGradient>
    <radialGradient id="stG" cx="50%" cy="40%" r="50%">
      <stop offset="0%" stop-color="#00ffff" stop-opacity=".12"/><stop offset="100%" stop-color="transparent"/>
    </radialGradient>
  </defs>
  <rect width="260" height="148" fill="url(#bg2)"/>
  <rect width="260" height="148" fill="url(#stG)"/>
  <!-- Asian pattern border -->
  ${Array.from({length:13},(_,i)=>`<rect x="${i*20}" y="0" width="20" height="8" fill="none" stroke="rgba(255,200,0,.2)" stroke-width=".8"/>
  <rect x="${i*20+4}" y="2" width="12" height="4" rx="1" fill="rgba(255,200,0,.08)"/>`).join('')}
  ${Array.from({length:13},(_,i)=>`<rect x="${i*20}" y="140" width="20" height="8" fill="none" stroke="rgba(255,200,0,.2)" stroke-width=".8"/>
  <rect x="${i*20+4}" y="142" width="12" height="4" rx="1" fill="rgba(255,200,0,.08)"/>`).join('')}
  <!-- Bamboo steamer -->
  <g transform="translate(130,78)">
    <!-- Bottom -->
    <ellipse cx="0" cy="32" rx="60" ry="14" fill="#7B5A0A" stroke="#4a3000" stroke-width="2"/>
    <rect x="-60" y="18" width="120" height="16" rx="3" fill="#9B7A1A" stroke="#4a3000" stroke-width="1.5"/>
    ${[-40,-20,0,20,40].map(x=>`<line x1="${x}" y1="18" x2="${x}" y2="34" stroke="rgba(0,0,0,.2)" stroke-width="1.5"/>`).join('')}
    <ellipse cx="0" cy="18" rx="60" ry="8" fill="#8B6A10" stroke="#4a3000" stroke-width="2"/>
    <!-- Middle -->
    <rect x="-58" y="-8" width="116" height="28" rx="3" fill="#A88020" stroke="#4a3000" stroke-width="1.5"/>
    ${[-40,-20,0,20,40].map(x=>`<line x1="${x}" y1="-8" x2="${x}" y2="20" stroke="rgba(0,0,0,.15)" stroke-width="1.5"/>`).join('')}
    <ellipse cx="0" cy="-8" rx="58" ry="8" fill="#987010" stroke="#4a3000" stroke-width="2"/>
    <!-- Lid body -->
    <path d="M-58,-8 Q-58,-32 0,-36 Q58,-32 58,-8" fill="#C8960C" stroke="#4a3000" stroke-width="1.5"/>
    <!-- Lid stripes -->
    ${[-40,-20,0,20,40].map(x=>`<line x1="${x}" y1="${-8+Math.abs(x)*0.18}" x2="${x}" y2="-34" stroke="rgba(0,0,0,.12)" stroke-width="1.5"/>`).join('')}
    <!-- Knob -->
    <ellipse cx="0" cy="-34" rx="11" ry="6" fill="#B88A00" stroke="#4a3000" stroke-width="1.5"/>
    <ellipse cx="0" cy="-37" rx="7" ry="3.5" fill="#D4A800"/>
    <!-- Visible bao buns in gap -->
    <ellipse cx="-18" cy="-5" rx="14" ry="9" fill="rgba(255,255,255,.92)" stroke="rgba(200,200,200,.4)" stroke-width="1"/>
    <ellipse cx="18" cy="-5" rx="14" ry="9" fill="rgba(255,255,255,.9)" stroke="rgba(200,200,200,.4)" stroke-width="1"/>
    <path d="M-24,-5 Q-18,-11 -12,-5" fill="none" stroke="rgba(180,180,180,.4)" stroke-width="1"/>
    <path d="M12,-5 Q18,-11 24,-5" fill="none" stroke="rgba(180,180,180,.4)" stroke-width="1"/>
    <!-- Steam -->
    <path d="M-20,-38 Q-14,-54 -19,-68" fill="none" stroke="rgba(255,255,255,.4)" stroke-width="3" stroke-linecap="round"/>
    <path d="M0,-39 Q6,-56 0,-72" fill="none" stroke="rgba(255,255,255,.35)" stroke-width="3" stroke-linecap="round"/>
    <path d="M20,-38 Q14,-54 19,-68" fill="none" stroke="rgba(255,255,255,.4)" stroke-width="3" stroke-linecap="round"/>
    <path d="M-10,-40 Q-7,-60 -11,-74" fill="none" stroke="rgba(255,255,255,.2)" stroke-width="2" stroke-linecap="round"/>
    <path d="M10,-40 Q7,-60 11,-74" fill="none" stroke="rgba(255,255,255,.2)" stroke-width="2" stroke-linecap="round"/>
  </g>
  <!-- Water drops -->
  ${[[38,32],[218,32],[30,74],[230,74],[55,112],[205,112]].map(([x,y])=>`
    <ellipse cx="${x}" cy="${y}" rx="5" ry="7" fill="rgba(0,170,255,.25)" stroke="rgba(100,220,255,.5)" stroke-width="1"/>`).join('')}
  <!-- Stars -->
  <circle cx="44" cy="20" r="1.5" fill="rgba(255,255,255,.7)"/>
  <circle cx="216" cy="20" r="1.5" fill="rgba(255,255,255,.7)"/>`;
}

function drawComNha(svg){
  svg.innerHTML=`
  <defs>
    <linearGradient id="bg3" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#081800"/><stop offset="100%" stop-color="#143000"/>
    </linearGradient>
    <radialGradient id="bwlG" cx="50%" cy="65%" r="50%">
      <stop offset="0%" stop-color="#88ff44" stop-opacity=".18"/><stop offset="100%" stop-color="transparent"/>
    </radialGradient>
  </defs>
  <rect width="260" height="148" fill="url(#bg3)"/>
  <rect width="260" height="148" fill="url(#bwlG)"/>
  <!-- Hills / rice paddies -->
  <ellipse cx="130" cy="140" rx="170" ry="70" fill="#1a3d00" opacity=".8"/>
  <ellipse cx="30" cy="128" rx="90" ry="50" fill="#1e4800" opacity=".6"/>
  <ellipse cx="230" cy="122" rx="90" ry="50" fill="#1e4800" opacity=".6"/>
  <!-- Rice paddy lines -->
  ${[0,1,2,3].map(i=>`
    <path d="M${10+i*12},148 Q${28+i*12},108 ${46+i*12},148" fill="none" stroke="rgba(100,200,0,.25)" stroke-width="1.5"/>
    <path d="M${130+i*12},148 Q${148+i*12},105 ${166+i*12},148" fill="none" stroke="rgba(100,200,0,.25)" stroke-width="1.5"/>
  `).join('')}
  <!-- Moon -->
  <circle cx="210" cy="22" r="14" fill="rgba(255,240,180,.15)" stroke="rgba(255,240,180,.25)" stroke-width="1"/>
  <circle cx="216" cy="19" r="11" fill="#143000"/>
  <!-- Stars sky -->
  <circle cx="30" cy="14" r="1.5" fill="rgba(255,255,255,.8)"/>
  <circle cx="70" cy="8" r="1" fill="rgba(255,255,255,.6)"/>
  <circle cx="140" cy="10" r="1.5" fill="rgba(255,255,255,.7)"/>
  <circle cx="80" cy="22" r="1" fill="rgba(255,255,255,.5)"/>
  <circle cx="165" cy="16" r="1" fill="rgba(255,255,255,.5)"/>
  <!-- Pho bowl -->
  <g transform="translate(130,84)">
    <!-- Shadow -->
    <ellipse cx="0" cy="45" rx="58" ry="10" fill="rgba(0,0,0,.4)"/>
    <!-- Bowl outer -->
    <path d="M-58,0 Q-58,46 0,52 Q58,46 58,0 Z" fill="#cc3300"/>
    <path d="M-58,0 Q-58,46 0,52 Q58,46 58,0 Z" fill="none" stroke="rgba(255,200,0,.55)" stroke-width="2"/>
    <!-- Decorative band -->
    <path d="M-56,9 Q-56,13 0,15 Q56,13 56,9" fill="none" stroke="rgba(255,200,0,.5)" stroke-width="1.5"/>
    ${[-32,-14,0,14,32].map(x=>`<text x="${x}" y="33" text-anchor="middle" font-size="7" fill="rgba(255,200,0,.45)">✦</text>`).join('')}
    <!-- Broth -->
    <ellipse cx="0" cy="0" rx="58" ry="12" fill="#7B3A12"/>
    <ellipse cx="0" cy="0" rx="55" ry="10" fill="#9B4A18"/>
    <ellipse cx="-12" cy="-2" rx="22" ry="5" fill="rgba(255,140,0,.2)"/>
    <!-- Noodles -->
    <path d="M-38,-2 Q-22,10 -6,1 Q10,-8 26,1 Q42,9 50,3" fill="none" stroke="rgba(255,235,190,.7)" stroke-width="3.5" stroke-linecap="round"/>
    <path d="M-42,3 Q-26,-7 -10,3 Q6,12 22,3 Q38,-6 48,2" fill="none" stroke="rgba(255,235,190,.5)" stroke-width="2" stroke-linecap="round"/>
    <!-- Herbs -->
    <ellipse cx="-22" cy="-3" rx="9" ry="5" fill="rgba(0,190,0,.7)" transform="rotate(-22,-22,-3)"/>
    <ellipse cx="24" cy="4" rx="8" ry="4.5" fill="rgba(0,190,0,.65)" transform="rotate(18,24,4)"/>
    <!-- Chilli slices -->
    <ellipse cx="8" cy="-5" rx="4" ry="2.5" fill="rgba(220,20,20,.7)" transform="rotate(-15,8,-5)"/>
    <!-- Chopsticks -->
    <line x1="-8" y1="-20" x2="8" y2="15" stroke="#8B6914" stroke-width="3" stroke-linecap="round"/>
    <line x1="4" y1="-20" x2="18" y2="15" stroke="#A07820" stroke-width="3" stroke-linecap="round"/>
    <!-- Steam wisps -->
    <path d="M-14,-15 Q-8,-32 -13,-46" fill="none" stroke="rgba(255,255,255,.28)" stroke-width="2.5" stroke-linecap="round"/>
    <path d="M0,-14 Q6,-34 0,-48" fill="none" stroke="rgba(255,255,255,.23)" stroke-width="2.5" stroke-linecap="round"/>
    <path d="M14,-15 Q8,-32 13,-46" fill="none" stroke="rgba(255,255,255,.28)" stroke-width="2.5" stroke-linecap="round"/>
  </g>
  <!-- Lotus flowers -->
  ${[[24,108,.48],[234,98,.45]].map(([x,y,s])=>`
  <g transform="translate(${x},${y}) scale(${s})" opacity=".75">
    ${[0,72,144,216,288].map(a=>`<ellipse cx="0" cy="-13" rx="8" ry="12" fill="${a%144===0?'#ff88bb':'#ffaad4'}" transform="rotate(${a})"/>`).join('')}
    <circle cx="0" cy="0" r="7" fill="#FFD700"/>
    <circle cx="0" cy="0" r="4" fill="#FF8C00"/>
  </g>`).join('')}`;
}

const typeGrads = {
  fire:   ['#FF9500','#FF4500','#FF6B1A','#FF3300'],
  water:  ['#1a78ff','#0044cc','#00d4ff','#0033aa'],
  grass:  ['#22cc55','#008833','#aaff22','#005522'],
};
const typePatterns = {
  fire:`<defs><pattern id="fp" patternUnits="userSpaceOnUse" width="28" height="28"><path d="M14,26 Q7,18 11,10 Q14,4 14,1 Q17,7 15,13 Q19,9 18,15 Q21,11 19,17 Q22,14 21,21 Q18,26 14,26Z" fill="rgba(255,100,0,.18)" stroke="rgba(255,150,0,.1)" stroke-width=".5"/></pattern></defs><rect width="100%" height="100%" fill="url(#fp)"/>`,
  water:`<defs><pattern id="wp" patternUnits="userSpaceOnUse" width="24" height="24"><circle cx="12" cy="12" r="8" fill="none" stroke="rgba(100,200,255,.15)" stroke-width="1.5"/><circle cx="12" cy="12" r="4" fill="rgba(100,200,255,.07)"/></pattern></defs><rect width="100%" height="100%" fill="url(#wp)"/>`,
  grass:`<defs><pattern id="gp" patternUnits="userSpaceOnUse" width="18" height="18"><line x1="9" y1="18" x2="9" y2="9" stroke="rgba(100,255,100,.22)" stroke-width="1.5"/><line x1="9" y1="9" x2="3" y2="3" stroke="rgba(100,255,100,.15)" stroke-width="1"/><line x1="9" y1="9" x2="15" y2="3" stroke="rgba(100,255,100,.15)" stroke-width="1"/><line x1="9" y1="12" x2="4" y2="8" stroke="rgba(100,255,100,.1)" stroke-width="1"/><line x1="9" y1="12" x2="14" y2="8" stroke="rgba(100,255,100,.1)" stroke-width="1"/></pattern></defs><rect width="100%" height="100%" fill="url(#gp)"/>`,
};

let torn=false,tearProg=0,isDrag=false,startY=0;
const packTop=document.getElementById('packTop');
const pack=document.getElementById('pack');
const cardReveal=document.getElementById('cardReveal');
const resetBtn=document.getElementById('resetBtn');

function renderCard(r){
  document.getElementById('cStage').textContent=r.stage;
  document.getElementById('cName').textContent=r.name;
  document.getElementById('cHP').textContent=r.hp+' HP';
  document.getElementById('cFlavor').textContent='"'+r.flavor+'"';
  document.getElementById('cWeakness').innerHTML='WEAKNESS: <span>'+r.weakness+'</span>';
  document.getElementById('cNumber').textContent=r.number;
  document.getElementById('cRarity').textContent=r.rarity;
  const wrap=document.getElementById('cardInnerWrap');
  wrap.className='card-inner-wrap '+r.type;
  const outer=document.getElementById('cardOuter');
  const g=typeGrads[r.type];
  outer.style.background=`linear-gradient(145deg,${g[0]},${g[1]},${g[2]},${g[3]})`;
  document.getElementById('cardPattern').innerHTML=typePatterns[r.type]||'';
  r.art(document.getElementById('cardArtSVG'));
  document.getElementById('artStrip').textContent=r.typeName+' POKEMON';
  const energyIcon={fire:'🔥',water:'💧',grass:'🍃',colorless:'⬡'};
  document.getElementById('cAttacks').innerHTML=r.attacks.map(a=>`
    <div class="attack">
      <div class="attack-energy">${a.energies.map(e=>`<div class="energy ${e}">${energyIcon[e]||'⬡'}</div>`).join('')}</div>
      <div><div class="attack-name">${a.name}</div>${a.desc?`<div class="attack-desc">${a.desc}</div>`:''}</div>
      <div class="attack-dmg">${a.dmg}</div>
    </div>`).join('');
}

function onDown(e){
  if(torn)return; isDrag=true;
  startY=e.clientY??e.touches?.[0]?.clientY;
  e.preventDefault();
}
function onMove(e){
  if(!isDrag||torn)return;
  const cy=e.clientY??e.touches?.[0]?.clientY;
  tearProg=Math.max(0,Math.min(1,(startY-cy)/90));
  const tx=Math.sin(tearProg*12)*tearProg*6;
  packTop.style.transform=`rotate(${tearProg*-42}deg) translateX(${tx}px) translateY(${-tearProg*38}px)`;
  packTop.style.opacity=String(1-tearProg*.65);
  if(tearProg>0.72)completeTear();
}
function onUp(){
  if(!isDrag)return; isDrag=false;
  if(!torn&&tearProg<0.72){
    packTop.style.transition='transform .35s ease,opacity .35s ease';
    packTop.style.transform=''; packTop.style.opacity='';
    setTimeout(()=>{packTop.style.transition='';tearProg=0;},360);
  }
}
function completeTear(){
  if(torn)return; torn=true;
  const r=restaurants[Math.floor(Math.random()*restaurants.length)];
  renderCard(r);
  packTop.style.transition='transform .55s cubic-bezier(.4,0,.2,1),opacity .55s ease';
  packTop.style.transform=`rotate(${-30-Math.random()*25}deg) translateY(-260px) translateX(${Math.random()*110-55}px)`;
  packTop.style.opacity='0';
  setTimeout(()=>{pack.style.transition='opacity .4s ease';pack.style.opacity='0';},180);
  setTimeout(()=>{cardReveal.classList.add('visible');burst();confetti();resetBtn.classList.add('show');},380);
}
function burst(){
  const syms=['⭐','✨','💫','🌟','🎴','🍽️','❇️'];
  const w=document.getElementById('packWrapper');
  for(let i=0;i<24;i++){
    const el=document.createElement('div');
    el.textContent=syms[Math.floor(Math.random()*syms.length)];
    const dx=(Math.random()-.5)*300,dy=(Math.random()-.5)*300;
    el.style.cssText=`position:absolute;left:50%;top:50%;font-size:${10+Math.random()*18}px;pointer-events:none;z-index:200;animation:bOut .9s ease forwards;--dx:${dx}px;--dy:${dy}px;`;
    w.appendChild(el); setTimeout(()=>el.remove(),1000);
  }
  if(!document.getElementById('bOutKf')){
    const s=document.createElement('style');s.id='bOutKf';
    s.textContent='@keyframes bOut{0%{transform:translate(-50%,-50%) scale(0);opacity:1}100%{transform:translate(calc(-50% + var(--dx)),calc(-50% + var(--dy))) scale(1.2);opacity:0}}';
    document.head.appendChild(s);
  }
}
function confetti(){
  const cols=['#FFD700','#FF6B6B','#4ECDC4','#7700AA','#FF00AA','#00FF88','#FF8800'];
  for(let i=0;i<55;i++){
    const el=document.createElement('div');el.className='conf';
    el.style.cssText=`background:${cols[Math.floor(Math.random()*cols.length)]};left:${15+Math.random()*70}%;top:-15px;transform:rotate(${Math.random()*360}deg);animation:cFall ${1.2+Math.random()*1.8}s ease ${Math.random()*.5}s forwards;`;
    document.body.appendChild(el);setTimeout(()=>el.remove(),3500);
  }
  if(!document.getElementById('cFallKf')){
    const s=document.createElement('style');s.id='cFallKf';
    s.textContent='@keyframes cFall{0%{opacity:1;transform:translateY(0) rotate(0deg)}100%{opacity:0;transform:translateY(100vh) rotate(540deg)}}';
    document.head.appendChild(s);
  }
}
function resetPack(){
  torn=false;tearProg=0;
  packTop.style.transition='none';packTop.style.transform='';packTop.style.opacity='';
  pack.style.transition='none';pack.style.opacity='';
  cardReveal.classList.remove('visible');resetBtn.classList.remove('show');
  requestAnimationFrame(()=>{packTop.style.transition='';pack.style.transition='';});
}

packTop.addEventListener('mousedown',onDown);
packTop.addEventListener('touchstart',onDown,{passive:false});
window.addEventListener('mousemove',onMove);
window.addEventListener('touchmove',e=>{if(isDrag){e.preventDefault();onMove({clientY:e.touches[0].clientY});}},{passive:false});
window.addEventListener('mouseup',onUp);
window.addEventListener('touchend',onUp);

const starsEl=document.getElementById('stars');
for(let i=0;i<80;i++){
  const s=document.createElement('div');s.className='star';
  const sz=Math.random()*2+1;
  s.style.cssText=`width:${sz}px;height:${sz}px;left:${Math.random()*100}%;top:${Math.random()*100}%;--d:${2+Math.random()*5}s;--dl:${Math.random()*5}s;`;
  starsEl.appendChild(s);
}
</script>
</body>
</html>
