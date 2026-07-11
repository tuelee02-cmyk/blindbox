<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pack Rip — Hanoi Date Quest</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#0a0e21;
    --well:#141b3d;
    --well-2:#0d1330;
    --tiffany:#0ABAB5;
    --fuchsia:#E0115F;
    --paper:#f4f4f4;
    --dim:#9fb0d8;
    --black:#0a0a12;
    --display: 'Press Start 2P', monospace;
    --body: 'VT323', monospace;
    --mono: 'Press Start 2P', monospace;
    --accent: var(--tiffany);
  }
  *{ box-sizing:border-box; }
  html,body{ height:100%; }
  body{
    margin:0;
    background:
      repeating-linear-gradient(0deg, rgba(255,255,255,0.025) 0px, rgba(255,255,255,0.025) 1px, transparent 1px, transparent 3px),
      radial-gradient(circle at 15% 0%, rgba(10,186,181,0.22), transparent 55%),
      radial-gradient(circle at 85% 100%, rgba(224,17,95,0.16), transparent 55%),
      var(--ink);
    color:var(--paper);
    font-family:var(--body);
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:28px 14px;
    overflow-x:hidden;
  }
  @media (prefers-reduced-motion: reduce){
    *{ animation-duration:0.01ms !important; transition-duration:0.01ms !important; }
  }

  .stage-frame{
    width:100%;
    max-width:460px;
    min-height:700px;
    background:linear-gradient(180deg, var(--well), var(--well-2));
    border:4px solid var(--black);
    box-shadow:8px 8px 0 rgba(0,0,0,0.55), inset 0 0 0 2px rgba(255,255,255,0.06);
    clip-path: polygon(0 14px,14px 14px,14px 0, calc(100% - 14px) 0, calc(100% - 14px) 14px, 100% 14px, 100% calc(100% - 14px), calc(100% - 14px) calc(100% - 14px), calc(100% - 14px) 100%, 14px 100%, 14px calc(100% - 14px), 0 calc(100% - 14px));
    padding:22px 20px 26px;
    position:relative;
    overflow:hidden;
    display:flex;
    flex-direction:column;
  }

  .progress{ display:flex; gap:6px; justify-content:center; margin-bottom:20px; }
  .pip{ flex:1; height:10px; background:var(--black); border:2px solid var(--black); box-shadow: inset 0 0 0 2px rgba(255,255,255,0.08); position:relative; overflow:hidden; }
  .pip::after{ content:''; position:absolute; inset:0; background: repeating-linear-gradient(90deg, var(--accent) 0 4px, #fff 4px 8px); transform:scaleX(0); transform-origin:left; transition:transform .5s steps(6); }
  .pip.done::after{ transform:scaleX(1); }
  .pip.active::after{ transform:scaleX(0.55); }

  .eyebrow{ font-family:var(--mono); font-size:9px; letter-spacing:0.06em; text-transform:uppercase; color:var(--accent); margin:0 0 10px; text-shadow:2px 2px 0 rgba(0,0,0,0.5); }
  h1.stage-title{ font-family:var(--display); font-size:15px; line-height:1.7; margin:0 0 12px; text-shadow:2px 2px 0 rgba(0,0,0,0.6); }
  p.stage-sub{ color:var(--dim); font-size:19px; line-height:1.35; margin:0 0 20px; font-family:var(--body); }

  .stage-body{ flex:1; display:flex; flex-direction:column; align-items:center; justify-content:flex-start; }

  /* ---------- PACK (booster-pack look) ---------- */
  .pack-zone{ position:relative; width:220px; height:356px; margin:6px auto 16px; }

  .pack-stack{ position:absolute; left:50%; bottom:4px; width:184px; height:64px; background:var(--black); border:3px solid var(--black); transform:translateX(-50%) rotate(-4deg); z-index:0; opacity:.5; transition:opacity .3s steps(4); }
  .pack-stack.s2{ transform:translateX(-50%) rotate(4deg); opacity:.3; bottom:0px; }
  .pack-zone.torn .pack-stack{ opacity:0; }

  .pack-face-bg{
    background:
      repeating-linear-gradient(45deg, rgba(255,255,255,0.10) 0 6px, rgba(255,255,255,0) 6px 12px),
      linear-gradient(160deg, var(--fuchsia), var(--ink) 45%, var(--tiffany) 100%);
  }
  .pack{
    position:absolute; top:0; left:0; width:220px; height:330px;
    cursor:pointer; z-index:2;
    border:4px solid var(--black);
    box-shadow:6px 6px 0 rgba(0,0,0,0.5);
    clip-path: polygon(
      0px 10px, 14px 0px, 28px 10px, 42px 0px, 56px 10px, 70px 0px,
      84px 10px, 98px 20px, 112px 26px, 126px 20px, 140px 10px,
      154px 0px, 168px 10px, 182px 0px, 196px 10px, 210px 0px, 220px 10px,
      220px calc(100% - 10px), 210px 100%, 10px 100%, 0px calc(100% - 10px)
    );
  }
  .pack .pack-face-bg{ position:absolute; inset:0; overflow:hidden; display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center; padding:26px 16px 18px; }
  .pack:hover{ filter:brightness(1.08); }
  .pack-shine{ position:absolute; top:-30%; left:0; width:35%; height:160%; background:linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent); transform:translateX(-140%) rotate(18deg); animation:shineSweep 2.4s linear infinite; pointer-events:none; }
  @keyframes shineSweep{ 0%{ transform:translateX(-140%) rotate(18deg);} 100%{ transform:translateX(260%) rotate(18deg);} }
  .pack-brand{ font-family:var(--mono); font-size:6.5px; letter-spacing:.06em; color:var(--paper); opacity:.85; margin-bottom:8px; }
  .pack-rarity{ font-size:11px; letter-spacing:3px; color:var(--tiffany); margin-bottom:10px; text-shadow:1px 1px 0 rgba(0,0,0,0.5); }
  .pack .mark{ font-size:50px; margin-bottom:10px; filter: drop-shadow(3px 3px 0 rgba(0,0,0,0.5)); }
  .pack-name{ font-family:var(--mono); font-size:7.5px; letter-spacing:.04em; color:var(--paper); background:rgba(0,0,0,0.4); border:2px solid rgba(255,255,255,0.35); padding:5px 9px; margin-bottom:14px; }
  .pack .tap{ font-family:var(--mono); font-size:9px; letter-spacing:0.05em; color:var(--black); background:var(--accent); animation:pulse 1.2s steps(2) infinite; border:2px solid var(--black); padding:8px 10px; }
  @keyframes pulse{ 0%,100%{opacity:1;} 50%{opacity:.55;} }
  .seam{ position:absolute; left:50%; top:16px; bottom:16px; width:0; border-left:3px dashed rgba(255,255,255,0.4); transform:translateX(-1.5px); z-index:3; }

  .pack-half{ position:absolute; top:0; width:110px; height:330px; overflow:hidden; border:4px solid var(--black); z-index:2; }
  .pack-half .pack-face-bg{ position:absolute; top:0; width:220px; height:330px; }
  .pack-half.left{ left:0; border-right:none;
    clip-path: polygon(8px 0, 100% 0, 82% 10%, 100% 18%, 82% 26%, 100% 34%, 82% 42%, 100% 50%, 82% 58%, 100% 66%, 82% 74%, 100% 82%, 82% 90%, 100% 100%, 8px 100%, 0 calc(100% - 8px), 0 8px);
  }
  .pack-half.left .pack-face-bg{ left:0; }
  .pack-half.right{ right:0; border-left:none;
    clip-path: polygon(18% 0, calc(100% - 8px) 0, 100% 8px, 100% calc(100% - 8px), calc(100% - 8px) 100%, 18% 100%, 0 90%, 18% 82%, 0 74%, 18% 66%, 0 58%, 18% 50%, 0 42%, 18% 34%, 0 26%, 18% 18%, 0 10%);
  }
  .pack-half.right .pack-face-bg{ right:0; }

  @keyframes rippleLeft{
    0%{ transform:translateX(0) translateY(0) rotate(0deg); opacity:1; }
    18%{ transform:translateX(-8px) translateY(-4px) rotate(-3deg); }
    38%{ transform:translateX(-4px) translateY(3px) rotate(2deg); }
    58%{ transform:translateX(-40px) translateY(-3px) rotate(-4deg); opacity:1; }
    100%{ transform:translateX(-280px) translateY(6px) rotate(-10deg); opacity:0; }
  }
  @keyframes rippleRight{
    0%{ transform:translateX(0) translateY(0) rotate(0deg); opacity:1; }
    18%{ transform:translateX(8px) translateY(4px) rotate(3deg); }
    38%{ transform:translateX(4px) translateY(-3px) rotate(-2deg); }
    58%{ transform:translateX(40px) translateY(3px) rotate(4deg); opacity:1; }
    100%{ transform:translateX(280px) translateY(-6px) rotate(10deg); opacity:0; }
  }
  .pack-zone.torn .pack-half.left{ animation: rippleLeft .75s steps(14) forwards; }
  .pack-zone.torn .pack-half.right{ animation: rippleRight .75s steps(14) forwards; }
  .pack-zone.torn .pack{ opacity:0; transition:opacity .1s; }

  .spark{ position:absolute; width:7px; height:7px; background:var(--tiffany); box-shadow:0 0 0 2px var(--black); pointer-events:none; animation:spark .7s steps(6) forwards; z-index:4; }
  @keyframes spark{ 0%{ transform:translate(0,0) scale(1); opacity:1; } 100%{ transform:translate(var(--sx), var(--sy)) scale(0); opacity:0; } }

  /* ---------- CARDS ---------- */
  .cards-row{ display:flex; gap:14px; flex-wrap:wrap; justify-content:center; margin-top:8px; width:100%; }
  .card{
    width:150px; min-height:210px; padding:14px 12px;
    background:linear-gradient(160deg, rgba(255,255,255,0.09), rgba(255,255,255,0.02));
    border:3px solid var(--black);
    clip-path: polygon(0 8px,8px 8px,8px 0, calc(100% - 8px) 0, calc(100% - 8px) 8px, 100% 8px, 100% calc(100% - 8px), calc(100% - 8px) calc(100% - 8px), calc(100% - 8px) 100%, 8px 100%, 8px calc(100% - 8px), 0 calc(100% - 8px));
    position:relative; cursor:pointer; text-align:left;
    opacity:0; transform:translateY(18px) scale(.85);
    transition:opacity .4s steps(8), transform .4s steps(8), box-shadow .15s ease;
    display:flex; flex-direction:column;
    box-shadow:4px 4px 0 rgba(0,0,0,0.4);
  }
  .card.shown{ opacity:1; transform:translateY(0) scale(1); }
  .card:nth-child(1){ transition-delay:.05s; }
  .card:nth-child(2){ transition-delay:.18s; }
  .card:nth-child(3){ transition-delay:.31s; }
  .card:nth-child(4){ transition-delay:.44s; }
  .card:hover{ transform:translateY(-4px); box-shadow:6px 6px 0 rgba(0,0,0,0.5); }
  .card.picked{ box-shadow:4px 4px 0 var(--accent), 0 0 0 3px var(--black); }
  .card .tag{ font-family:var(--mono); font-size:7.5px; letter-spacing:0.04em; text-transform:uppercase; color:var(--accent); margin-bottom:10px; line-height:1.6; }
  .card .glyph{ font-size:32px; margin-bottom:8px; filter:drop-shadow(2px 2px 0 rgba(0,0,0,0.4)); }
  .card h3{ font-family:var(--display); font-size:11px; margin:0 0 8px; line-height:1.6; }
  .card p{ font-size:16px; color:var(--dim); margin:0; line-height:1.25; flex:1; font-family:var(--body); }

  /* ---------- chain reveal ---------- */
  .chain{ width:100%; margin-top:6px; }
  .chain-item{ display:flex; gap:12px; align-items:flex-start; padding:12px 6px; border-bottom:2px dashed rgba(255,255,255,0.15); opacity:0; transform:translateX(-16px); transition:opacity .4s steps(8), transform .4s steps(8); }
  .chain-item.shown{ opacity:1; transform:translateX(0); }
  .chain-item:last-child{ border-bottom:none; }
  .chain-num{ font-family:var(--mono); font-size:10px; color:var(--black); background:var(--accent); width:26px; height:26px; border:2px solid var(--black); display:flex; align-items:center; justify-content:center; flex:none; margin-top:2px; }
  .chain-item h4{ font-family:var(--display); font-size:11px; margin:0 0 6px; line-height:1.5; }
  .chain-item p{ font-size:16px; color:var(--dim); margin:0; line-height:1.25; font-family:var(--body); }

  .lock-note{
    margin-top:14px; padding:10px 12px;
    border:2px dashed var(--accent);
    background:rgba(255,255,255,0.04);
    font-family:var(--body); font-size:16px; color:var(--paper);
    text-align:center; line-height:1.3;
    opacity:0; transition:opacity .4s steps(8);
  }
  .lock-note.shown{ opacity:1; }

  /* ---------- carousel (stage 3) ---------- */
  .carousel-wrap{ width:100%; }
  .carousel{ display:flex; gap:14px; overflow-x:auto; scroll-snap-type:x mandatory; padding:6px 30px 14px; margin:0 -20px; -webkit-overflow-scrolling:touch; scrollbar-width:none; }
  .carousel::-webkit-scrollbar{ display:none; }
  .drink-card{
    scroll-snap-align:center; flex:none; width:190px; min-height:250px; padding:16px 14px;
    background:linear-gradient(160deg, rgba(255,255,255,0.1), rgba(255,255,255,0.02));
    border:3px solid var(--black);
    clip-path: polygon(0 8px,8px 8px,8px 0, calc(100% - 8px) 0, calc(100% - 8px) 8px, 100% 8px, 100% calc(100% - 8px), calc(100% - 8px) calc(100% - 8px), calc(100% - 8px) 100%, 8px 100%, 8px calc(100% - 8px), 0 calc(100% - 8px));
    box-shadow:4px 4px 0 rgba(0,0,0,0.4);
    display:flex; flex-direction:column;
  }
  .drink-card .glyph{ font-size:34px; margin-bottom:6px; filter:drop-shadow(2px 2px 0 rgba(0,0,0,0.4)); }
  .drink-card .tag{ font-family:var(--mono); font-size:7.5px; letter-spacing:.04em; text-transform:uppercase; color:var(--tiffany); margin-bottom:6px; line-height:1.6; }
  .drink-card h3{ font-family:var(--display); font-size:12px; margin:0 0 6px; line-height:1.6; }
  .drink-card .tagline{ font-size:15px; color:var(--paper); margin:0 0 8px; line-height:1.2; font-family:var(--body); }
  .drink-card ul{ margin:0 0 12px; padding-left:18px; font-size:14.5px; color:var(--dim); line-height:1.3; flex:1; font-family:var(--body); }
  .drink-card button{ margin-top:auto; border:2px solid var(--black); background:var(--accent); color:var(--black); font-family:var(--mono); font-size:8.5px; letter-spacing:.03em; text-transform:uppercase; padding:10px; cursor:pointer; box-shadow:3px 3px 0 rgba(0,0,0,0.5); transition:transform .1s steps(2); }
  .drink-card button:active{ transform:translate(3px,3px); box-shadow:none; }
  .drink-card.picked{ box-shadow:4px 4px 0 var(--accent), 0 0 0 3px var(--black); }
  .dots{ display:flex; gap:6px; justify-content:center; margin-top:2px; }
  .dot{ width:8px; height:8px; background:var(--black); border:2px solid rgba(255,255,255,0.25); }
  .dot.on{ background:var(--accent); border-color:var(--black); }

  /* ---------- recap ---------- */
  .ticket{ width:100%; padding:18px; background:linear-gradient(160deg, rgba(224,17,95,0.18), rgba(255,255,255,0.02)); border:3px solid var(--black); clip-path: polygon(0 10px,10px 10px,10px 0, calc(100% - 10px) 0, calc(100% - 10px) 10px, 100% 10px, 100% calc(100% - 10px), calc(100% - 10px) calc(100% - 10px), calc(100% - 10px) 100%, 10px 100%, 10px calc(100% - 10px), 0 calc(100% - 10px)); box-shadow:5px 5px 0 rgba(0,0,0,0.4); margin-top:4px; }
  .ticket h4{ font-family:var(--mono); font-size:9px; letter-spacing:.05em; text-transform:uppercase; color:var(--fuchsia); margin:0 0 14px; line-height:1.6; }
  .ticket-row{ display:flex; gap:10px; align-items:flex-start; margin-bottom:12px; }
  .ticket-row:last-child{ margin-bottom:0; }
  .ticket-row .n{ font-family:var(--mono); color:var(--fuchsia); font-size:9px; margin-top:2px; }
  .ticket-row div h5{ margin:0 0 3px; font-family:var(--display); font-size:10px; line-height:1.5; }
  .ticket-row div p{ margin:0; font-size:15px; color:var(--dim); font-family:var(--body); line-height:1.25; }

  /* ---------- buttons ---------- */
  .cta{ margin-top:18px; width:100%; background:var(--accent); color:var(--black); border:3px solid var(--black); padding:15px; font-family:var(--display); font-size:10px; letter-spacing:0.04em; cursor:pointer; box-shadow:5px 5px 0 rgba(0,0,0,0.5); transition:transform .1s steps(2), box-shadow .1s steps(2); }
  .cta:hover:not(:disabled){ filter:brightness(1.05); }
  .cta:active:not(:disabled){ transform:translate(4px,4px); box-shadow:1px 1px 0 rgba(0,0,0,0.5); }
  .cta:disabled{ opacity:.35; cursor:not-allowed; }
  .ghost-btn{ margin-top:10px; width:100%; background:transparent; border:3px solid rgba(255,255,255,0.3); color:var(--paper); padding:13px; font-family:var(--body); font-size:17px; cursor:pointer; }

  .fade-enter{ animation:fadeUp .4s steps(8) both; }
  @keyframes fadeUp{ from{ opacity:0; transform:translateY(10px);} to{ opacity:1; transform:translateY(0);} }

  .theme-indoor{ --accent:var(--fuchsia); }
  .theme-outdoor{ --accent:var(--tiffany); }
  .theme-drink{ --accent:var(--fuchsia); }
  .theme-dessert{ --accent:var(--tiffany); }
</style>
</head>
<body>
  <div class="stage-frame" id="frame">
    <div class="progress" id="progress"></div>
    <div id="stageContent" class="fade-enter"></div>
  </div>

<script>
const state = { stage: 1, path: null, food: null, drink: null };

const frame = document.getElementById('frame');
const progressEl = document.getElementById('progress');
const content = document.getElementById('stageContent');

function setProgress(){
  progressEl.innerHTML = '';
  for(let i=1;i<=4;i++){
    const p = document.createElement('div');
    p.className = 'pip' + (i < state.stage ? ' done' : (i === state.stage ? ' active' : ''));
    progressEl.appendChild(p);
  }
}
function setTheme(cls){ frame.className = 'stage-frame ' + cls; }
function mount(html){ content.classList.remove('fade-enter'); void content.offsetWidth; content.innerHTML = html; content.classList.add('fade-enter'); }

function spawnSparks(zone){
  for(let i=0;i<16;i++){
    const s = document.createElement('div');
    s.className = 'spark';
    const angle = Math.random()*Math.PI*2;
    const dist = 60 + Math.random()*80;
    s.style.setProperty('--sx', Math.cos(angle)*dist + 'px');
    s.style.setProperty('--sy', Math.sin(angle)*dist + 'px');
    s.style.left = (103 + Math.random()*14) + 'px';
    s.style.top = (150 + Math.random()*20) + 'px';
    zone.appendChild(s);
    setTimeout(()=> s.remove(), 750);
  }
}

function ripPackBlock(mark, label, rarity){
  rarity = rarity || '★ ★ ★';
  return `
    <div class="pack-zone" id="packZone">
      <div class="pack-stack"></div>
      <div class="pack-stack s2"></div>
      <div class="pack-half left"><div class="pack-face-bg"></div></div>
      <div class="pack-half right"><div class="pack-face-bg"></div></div>
      <div class="pack" id="packBtn">
        <div class="pack-face-bg">
          <div class="pack-shine"></div>
          <div class="pack-brand">◆ HANOI QUEST ◆</div>
          <div class="pack-rarity">${rarity}</div>
          <div class="mark">${mark}</div>
          <div class="pack-name">${label}</div>
          <div class="tap">RIP IT OPEN!</div>
        </div>
      </div>
      <div class="seam"></div>
    </div>`;
}

function wireRip(onTorn){
  const zone = document.getElementById('packZone');
  const btn = document.getElementById('packBtn');
  btn.addEventListener('click', () => {
    if(zone.classList.contains('torn')) return;
    zone.classList.add('torn');
    spawnSparks(zone);
    setTimeout(onTorn, 550);
  }, { once:true });
}

/* ================= STAGE 1 ================= */
function renderStage1(){
  setTheme('');
  setProgress();
  mount(`
    <p class="eyebrow">Stage 01/04</p>
    <h1 class="stage-title">Rip your terrain pack</h1>
    <p class="stage-sub">Two paths inside. Pick one.</p>
    <div class="stage-body">
      ${ripPackBlock('🎴', 'TERRAIN PACK', '★ ★ ★')}
      <div class="cards-row" id="cardsRow">
        <div class="card" data-id="indoor">
          <div class="tag">Cozy Mode</div>
          <div class="glyph">🏠</div>
          <h3>Indoor</h3>
          <p>Fusion food, city stroll.</p>
        </div>
        <div class="card" data-id="outdoor">
          <div class="tag">Beast Mode</div>
          <div class="glyph">🍔</div>
          <h3>Outdoor</h3>
          <p>Burgers, boutiques, games.</p>
        </div>
      </div>
    </div>
  `);

  wireRip(() => { document.querySelectorAll('#cardsRow .card').forEach(c => c.classList.add('shown')); });

  document.getElementById('cardsRow').addEventListener('click', (e) => {
    const card = e.target.closest('.card');
    if(!card || !card.classList.contains('shown')) return;
    document.querySelectorAll('#cardsRow .card').forEach(c => c.classList.remove('picked'));
    card.classList.add('picked');
    state.path = card.dataset.id;
    setTimeout(() => { state.stage = 2; renderStage2(); }, 350);
  });
}

/* ================= STAGE 2 ================= */
function renderStage2(){ if(state.path === 'indoor') renderStage2Indoor(); else renderStage2Outdoor(); }

function renderStage2Indoor(){
  setTheme('theme-indoor');
  setProgress();
  mount(`
    <p class="eyebrow">Stage 02/04</p>
    <h1 class="stage-title">Rip for your first bite</h1>
    <p class="stage-sub">Pick a meal to unlock the route.</p>
    <div class="stage-body">
      ${ripPackBlock('🍽️', 'MEAL PACK', '★ ★ ☆')}
      <div class="cards-row" id="cardsRow">
        <div class="card" data-id="misshanoi">
          <div class="tag">Fusion</div>
          <div class="glyph">🥢</div>
          <h3>Miss Hanoi</h3>
          <p>Vietnamese, remixed.</p>
        </div>
        <div class="card" data-id="pizza4ps">
          <div class="tag">Comfort</div>
          <div class="glyph">🍕</div>
          <h3>Pizza 4P's</h3>
          <p>Hanoi's favorite slice.</p>
        </div>
      </div>
      <div class="chain" id="chain"></div>
    </div>
  `);

  wireRip(() => { document.querySelectorAll('#cardsRow .card').forEach(c => c.classList.add('shown')); });

  document.getElementById('cardsRow').addEventListener('click', (e) => {
    const card = e.target.closest('.card');
    if(!card || !card.classList.contains('shown') || document.querySelector('#cardsRow .card.picked')) return;
    card.classList.add('picked');
    state.food = card.dataset.id === 'misshanoi' ? "Miss Hanoi" : "Pizza 4P's";

    const chain = document.getElementById('chain');
    chain.innerHTML = `
      <div class="chain-item" data-i="1"><div class="chain-num">2</div><div><h4>Hanoi Center</h4><p>Wander. Shop. Repeat.</p></div></div>
      <div class="chain-item" data-i="2"><div class="chain-num">3</div><div><h4>Annam Gourmet</h4><p>Grab your favorites.</p></div></div>
      <div class="lock-note" id="lockNote">⏳ Don't rip Stage 03 until you're at Annam Gourmet.</div>
      <button class="cta" id="toStage3">Stage 03 →</button>
    `;
    document.querySelectorAll('.chain-item').forEach((el, i) => { setTimeout(() => el.classList.add('shown'), 200 + i*180); });
    setTimeout(() => document.getElementById('lockNote').classList.add('shown'), 560);
    document.getElementById('toStage3').addEventListener('click', () => { state.stage = 3; renderStage3(); });
  });
}

function renderStage2Outdoor(){
  setTheme('theme-outdoor');
  setProgress();
  mount(`
    <p class="eyebrow">Stage 02/04</p>
    <h1 class="stage-title">Rip your route</h1>
    <p class="stage-sub">Three stops, no choices.</p>
    <div class="stage-body">
      ${ripPackBlock('🧭', 'ROUTE PACK', '★ ★ ★')}
      <div class="chain" id="chain"></div>
    </div>
  `);

  wireRip(() => {
    const chain = document.getElementById('chain');
    chain.innerHTML = `
      <div class="chain-item" data-i="1"><div class="chain-num">1</div><div><h4>Red's Burger</h4><p>Fuel up first.</p></div></div>
      <div class="chain-item" data-i="2"><div class="chain-num">2</div><div><h4>L'Space</h4><p>Browse and buy.</p></div></div>
      <div class="chain-item" data-i="3"><div class="chain-num">3</div><div><h4>Board game café</h4><p>Wind down, play.</p></div></div>
      <div class="lock-note" id="lockNote">⏳ Don't rip Stage 03 until you're at L'Space.</div>
      <button class="cta" id="toStage3">Stage 03 →</button>
    `;
    document.querySelectorAll('.chain-item').forEach((el, i) => { setTimeout(() => el.classList.add('shown'), 150 + i*180); });
    setTimeout(() => document.getElementById('lockNote').classList.add('shown'), 700);
    document.getElementById('toStage3').addEventListener('click', () => { state.stage = 3; renderStage3(); });
  });
}

/* ================= STAGE 3 ================= */
const DRINKS = [
  { id:'strawberry', tag:'Fruity', glyph:'🍓', name:'Strawberry Fizz', tagline:'Sweet & bubbly.',
    items:['Strawberry juice','Vodka','Lemon juice','Prosecco','Soda'] },
  { id:'vodkatonic', tag:'Classic', glyph:'🥂', name:'Vodka Tonic', tagline:'No fuss.',
    items:['Vodka','Tonic water'] },
  { id:'tequila', tag:'Bold', glyph:'🌵', name:'Tequila', tagline:'No chaser.',
    items:['Tequila, neat or shot'] },
  { id:'wineduo', tag:'Wine', glyph:'🍷', name:'Wine Duo', tagline:'Red or white.',
    items:['White wine','Red wine'] },
];

function renderStage3(){
  setTheme('theme-drink');
  setProgress();
  const cardsHtml = DRINKS.map(d => `
    <div class="drink-card" data-id="${d.id}">
      <div class="tag">${d.tag}</div>
      <div class="glyph">${d.glyph}</div>
      <h3>${d.name}</h3>
      <p class="tagline">${d.tagline}</p>
      <ul>${d.items.map(i => `<li>${i}</li>`).join('')}</ul>
      <button data-pick="${d.id}">Pick me!</button>
    </div>
  `).join('');
  const dotsHtml = DRINKS.map((_,i) => `<div class="dot ${i===0?'on':''}"></div>`).join('');

  mount(`
    <p class="eyebrow">Stage 03/04</p>
    <h1 class="stage-title">Rip the recipe pack</h1>
    <p class="stage-sub">Four drinks. Pick one.</p>
    <div class="stage-body">
      ${ripPackBlock('🍹', 'MIX PACK', '★ ★ ★')}
      <div class="carousel-wrap" id="carouselWrap" style="display:none;">
        <div class="carousel" id="carousel">${cardsHtml}</div>
        <div class="dots" id="dots">${dotsHtml}</div>
      </div>
      <button class="cta" id="toStage4" disabled>Stage 04 →</button>
    </div>
  `);

  wireRip(() => {
    document.getElementById('carouselWrap').style.display = 'block';
    document.querySelectorAll('.drink-card').forEach(c => { c.style.opacity = 0; c.style.transition='opacity .4s steps(6)'; });
    requestAnimationFrame(()=> { document.querySelectorAll('.drink-card').forEach((c,i) => setTimeout(()=> c.style.opacity = 1, i*90)); });
  });

  const carousel = document.getElementById('carousel');
  const dots = () => document.querySelectorAll('#dots .dot');
  carousel.addEventListener('scroll', () => {
    const cards = [...carousel.querySelectorAll('.drink-card')];
    const idx = cards.findIndex(c => Math.abs(c.offsetLeft - carousel.scrollLeft) < c.offsetWidth/2);
    dots().forEach((d,i) => d.classList.toggle('on', i === Math.max(idx,0)));
  });

  carousel.addEventListener('click', (e) => {
    const btn = e.target.closest('button[data-pick]');
    if(!btn) return;
    const drink = DRINKS.find(d => d.id === btn.dataset.pick);
    state.drink = drink.name;
    document.querySelectorAll('.drink-card').forEach(c => c.classList.remove('picked'));
    btn.closest('.drink-card').classList.add('picked');
    document.getElementById('toStage4').disabled = false;
  });

  document.getElementById('toStage4').addEventListener('click', () => { state.stage = 4; renderStage4(); });
}

/* ================= STAGE 4 ================= */
function renderStage4(){
  setTheme('theme-dessert');
  setProgress();
  mount(`
    <p class="eyebrow">Stage 04/04</p>
    <h1 class="stage-title">Rip the dessert pack</h1>
    <p class="stage-sub">Purple means sweet.</p>
    <div class="stage-body">
      ${ripPackBlock('🍮', 'DESSERT PACK', '★ ★ ★')}
      <div id="dessertReveal"></div>
    </div>
  `);

  wireRip(() => {
    const box = document.getElementById('dessertReveal');
    box.innerHTML = `
      <div class="cards-row">
        <div class="card shown" style="width:100%;">
          <div class="tag">Sugar Rush</div>
          <div class="glyph">🔮</div>
          <h3>Dessert Hunt</h3>
          <p>Wander till dessert finds you.</p>
        </div>
      </div>
      <button class="cta" id="toRecap">See my quest →</button>
    `;
    document.getElementById('toRecap').addEventListener('click', renderRecap);
  });
}

/* ================= RECAP ================= */
function renderRecap(){
  const rows = [];
  if(state.path === 'indoor'){
    rows.push({ n:1, h:state.food, p:'Cozy start.' });
    rows.push({ n:2, h:'Hanoi Center', p:'Wander & shop.' });
    rows.push({ n:3, h:'Annam Gourmet', p:'Grab your favorites.' });
  } else {
    rows.push({ n:1, h:"Red's Burger", p:'Burgers first.' });
    rows.push({ n:2, h:"L'Space", p:'Browse & buy.' });
    rows.push({ n:3, h:'Board game café', p:'Wind down.' });
  }
  rows.push({ n:4, h:state.drink, p:"Tonight's drink." });
  rows.push({ n:5, h:'Dessert Hunt', p:'Sweet finish.' });

  mount(`
    <p class="eyebrow">Quest Complete</p>
    <h1 class="stage-title">Your day, assembled</h1>
    <p class="stage-sub">Full route below.</p>
    <div class="stage-body">
      <div class="ticket">
        <h4>${state.path === 'indoor' ? 'Indoor Run' : 'Outdoor Run'}</h4>
        ${rows.map(r => `
          <div class="ticket-row">
            <div class="n">${String(r.n).padStart(2,'0')}</div>
            <div><h5>${r.h}</h5><p>${r.p}</p></div>
          </div>
        `).join('')}
      </div>
      <button class="ghost-btn" id="restart">New pack →</button>
    </div>
  `);
  document.getElementById('progress').innerHTML = '';
  document.getElementById('restart').addEventListener('click', () => {
    state.stage = 1; state.path = null; state.food = null; state.drink = null;
    renderStage1();
  });
}

renderStage1();
</script>
</body>
</html>
