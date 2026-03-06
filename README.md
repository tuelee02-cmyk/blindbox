<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>MISSION: FOOD ▶</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:       #0a0a1a;
    --bg2:      #12122a;
    --panel:    #1a1a3e;
    --border:   #5858f8;
    --border2:  #a0a0ff;
    --yellow:   #f8e800;
    --red:      #e82020;
    --green:    #20e840;
    --cyan:     #20e8f8;
    --white:    #e8e8f8;
    --shadow:   #000080;
    --pink:     #f820a8;
    --orange:   #f89820;
    --pixel: 4px;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Press Start 2P', monospace;
    background-color: var(--bg);
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
    cursor: default;
    image-rendering: pixelated;
  }

  /* Scanline effect */
  body::after {
    content: '';
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 3px,
      rgba(0,0,0,0.08) 3px,
      rgba(0,0,0,0.08) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* Star field bg */
  .starfield {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    overflow: hidden;
  }

  .star {
    position: absolute;
    width: 3px; height: 3px;
    background: white;
    animation: twinkle linear infinite;
    image-rendering: pixelated;
  }

  @keyframes twinkle {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.1; }
  }

  /* Pages */
  .page {
    display: none;
    position: relative;
    z-index: 10;
    min-height: 100vh;
    padding: 24px 16px 48px;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .page.active { display: flex; }

  /* ---- PIXEL PANEL ---- */
  .pixel-panel {
    background: var(--panel);
    border: var(--pixel) solid var(--border);
    box-shadow:
      0 0 0 var(--pixel) var(--shadow),
      inset 0 0 0 var(--pixel) rgba(255,255,255,0.04),
      0 0 40px rgba(88,88,248,0.25);
    padding: 24px 20px;
    width: 100%;
    max-width: 360px;
    position: relative;
  }

  /* Corner decorations */
  .pixel-panel::before,
  .pixel-panel::after {
    content: '■';
    position: absolute;
    color: var(--border2);
    font-size: 10px;
    line-height: 1;
  }
  .pixel-panel::before { top: 6px; left: 8px; }
  .pixel-panel::after  { bottom: 6px; right: 8px; }

  /* ---- TITLE BAR ---- */
  .title-bar {
    background: var(--border);
    margin: -24px -20px 20px;
    padding: 10px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: var(--pixel) solid var(--border2);
  }

  .title-bar-text {
    color: var(--yellow);
    font-size: 8px;
    letter-spacing: 1px;
    text-shadow: 2px 2px 0 #000;
  }

  .title-bar-dots {
    display: flex;
    gap: 5px;
  }

  .dot {
    width: 10px; height: 10px;
    border: 2px solid rgba(255,255,255,0.3);
  }
  .dot.r { background: var(--red); }
  .dot.y { background: var(--yellow); }
  .dot.g { background: var(--green); }

  /* ---- SPRITE ---- */
  .sprite-wrap {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
    position: relative;
  }

  .pixel-sprite {
    image-rendering: pixelated;
    animation: float 1.8s ease-in-out infinite;
    display: block;
    margin: 0 auto;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-8px); }
  }

  /* ---- DIALOGUE BOX ---- */
  .dialogue-box {
    background: #08081c;
    border: var(--pixel) solid var(--border2);
    padding: 16px;
    margin-bottom: 20px;
    position: relative;
    min-height: 80px;
  }

  .dialogue-box::before {
    content: '▼';
    position: absolute;
    bottom: 6px;
    right: 10px;
    color: var(--white);
    font-size: 8px;
    animation: blink 0.8s step-end infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  .dialogue-name {
    color: var(--yellow);
    font-size: 7px;
    margin-bottom: 10px;
    text-shadow: 1px 1px 0 #000;
  }

  .dialogue-text {
    color: var(--white);
    font-size: 8px;
    line-height: 2;
    text-shadow: 1px 1px 0 #000;
  }

  /* Typewriter */
  .typewriter {
    display: inline;
    border-right: 2px solid var(--white);
    animation: cursorBlink 0.7s step-end infinite;
    white-space: pre-wrap;
    word-break: break-word;
  }

  @keyframes cursorBlink {
    0%, 100% { border-color: var(--white); }
    50% { border-color: transparent; }
  }

  /* ---- PIXEL BUTTON ---- */
  .pixel-btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 9px;
    background: var(--yellow);
    color: #000;
    border: none;
    padding: 14px 20px;
    cursor: pointer;
    width: 100%;
    text-align: center;
    letter-spacing: 1px;
    box-shadow: 4px 4px 0 #000, -2px -2px 0 rgba(255,255,255,0.3) inset;
    transition: transform 0.08s, box-shadow 0.08s;
    image-rendering: pixelated;
    display: block;
    text-decoration: none;
  }

  .pixel-btn:hover {
    background: var(--orange);
    transform: translate(-2px, -2px);
    box-shadow: 6px 6px 0 #000, -2px -2px 0 rgba(255,255,255,0.3) inset;
  }

  .pixel-btn:active {
    transform: translate(2px, 2px);
    box-shadow: 2px 2px 0 #000;
  }

  .pixel-btn.cyan {
    background: var(--cyan);
  }
  .pixel-btn.cyan:hover { background: #40ffff; }

  .pixel-btn.green {
    background: var(--green);
  }

  /* ---- HEADER ---- */
  .game-header {
    text-align: center;
    margin-bottom: 20px;
    color: var(--yellow);
    font-size: 10px;
    text-shadow: 3px 3px 0 #000, 0 0 20px rgba(248,232,0,0.5);
    letter-spacing: 2px;
    animation: headerGlow 2s ease-in-out infinite;
  }

  @keyframes headerGlow {
    0%, 100% { text-shadow: 3px 3px 0 #000, 0 0 10px rgba(248,232,0,0.3); }
    50% { text-shadow: 3px 3px 0 #000, 0 0 25px rgba(248,232,0,0.8), 0 0 40px rgba(248,232,0,0.4); }
  }

  .sub-header {
    text-align: center;
    color: var(--cyan);
    font-size: 7px;
    margin-bottom: 4px;
    letter-spacing: 1px;
  }

  .lives-row {
    text-align: center;
    font-size: 11px;
    margin-bottom: 16px;
    color: var(--red);
  }

  /* ---- BOXES GRID ---- */
  .boxes-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    width: 100%;
    max-width: 360px;
    margin-bottom: 16px;
  }

  .gift-box {
    background: var(--panel);
    border: var(--pixel) solid var(--border);
    padding: 18px 10px 14px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.08s, box-shadow 0.08s, border-color 0.1s;
    box-shadow: 4px 4px 0 #000;
    min-height: 120px;
    position: relative;
    -webkit-tap-highlight-color: transparent;
  }

  .gift-box:hover {
    transform: translate(-2px, -2px);
    box-shadow: 6px 6px 0 #000;
    border-color: var(--yellow);
  }

  .gift-box:active {
    transform: translate(2px, 2px);
    box-shadow: 2px 2px 0 #000;
  }

  .gift-box.opened {
    cursor: default;
    border-color: var(--green);
    box-shadow: 4px 4px 0 #000, 0 0 16px rgba(32,232,64,0.3);
    pointer-events: none;
  }

  .gift-box.shake {
    animation: pixelShake 0.35s steps(2) forwards;
  }

  @keyframes pixelShake {
    0%   { transform: translate(0,0); }
    20%  { transform: translate(-4px, 0); }
    40%  { transform: translate(4px, -4px); }
    60%  { transform: translate(-4px, 4px); }
    80%  { transform: translate(4px, 0); }
    100% { transform: translate(0, 0); }
  }

  .box-num {
    position: absolute;
    top: 5px; right: 7px;
    color: var(--border2);
    font-size: 6px;
  }

  .box-icon {
    font-size: 36px;
    margin-bottom: 8px;
    image-rendering: pixelated;
    display: block;
  }

  .box-label {
    color: var(--border2);
    font-size: 6px;
    text-align: center;
    line-height: 1.8;
  }

  .box-reveal {
    color: var(--green);
    font-size: 7px;
    text-align: center;
    line-height: 1.8;
    text-shadow: 0 0 8px rgba(32,232,64,0.8);
  }

  .box-reveal-icon {
    font-size: 28px;
    margin-bottom: 6px;
    animation: popIn 0.2s steps(3) forwards;
  }

  @keyframes popIn {
    0%   { transform: scale(0); }
    60%  { transform: scale(1.3); }
    100% { transform: scale(1); }
  }

  /* ---- RESULT ---- */
  .result-header {
    text-align: center;
    color: var(--yellow);
    font-size: 9px;
    letter-spacing: 2px;
    margin-bottom: 16px;
    text-shadow: 3px 3px 0 #000;
    animation: headerGlow 1.5s ease-in-out infinite;
  }

  .result-score {
    text-align: center;
    color: var(--cyan);
    font-size: 7px;
    margin-bottom: 20px;
    letter-spacing: 1px;
  }

  .result-icon {
    font-size: 56px;
    display: block;
    text-align: center;
    margin-bottom: 12px;
    animation: popIn 0.3s steps(3) forwards;
  }

  .result-name {
    color: var(--yellow);
    font-size: 13px;
    text-align: center;
    margin-bottom: 10px;
    text-shadow: 3px 3px 0 #000, 0 0 20px rgba(248,232,0,0.6);
    letter-spacing: 2px;
  }

  .result-msg {
    color: var(--white);
    font-size: 7px;
    text-align: center;
    line-height: 2.2;
    margin-bottom: 24px;
  }

  .hp-bar-wrap {
    margin-bottom: 20px;
  }

  .hp-label {
    color: var(--white);
    font-size: 6px;
    margin-bottom: 6px;
    letter-spacing: 1px;
  }

  .hp-bar {
    height: 14px;
    background: #0a0a1a;
    border: 3px solid var(--border2);
    overflow: hidden;
  }

  .hp-fill {
    height: 100%;
    background: var(--green);
    width: 0%;
    animation: fillBar 1s steps(20) 0.3s forwards;
    box-shadow: inset 0 3px 0 rgba(255,255,255,0.3);
  }

  @keyframes fillBar {
    to { width: 100%; }
  }

  /* ---- PIXEL CONFETTI ---- */
  #confetti-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 500;
    image-rendering: pixelated;
  }

  /* Blinking SELECT */
  .press-start {
    text-align: center;
    color: var(--white);
    font-size: 7px;
    letter-spacing: 2px;
    animation: blink 1s step-end infinite;
    margin-top: 12px;
  }

  /* Scrolling marquee top bar */
  .top-bar {
    position: fixed;
    top: 0; left: 0; right: 0;
    background: var(--border);
    padding: 5px 0;
    z-index: 100;
    overflow: hidden;
  }

  .marquee-text {
    color: var(--yellow);
    font-size: 6px;
    white-space: nowrap;
    display: inline-block;
    animation: marquee 14s linear infinite;
    letter-spacing: 2px;
  }

  @keyframes marquee {
    0%   { transform: translateX(100vw); }
    100% { transform: translateX(-100%); }
  }

  /* Pixel divider */
  .pixel-divider {
    height: var(--pixel);
    background: repeating-linear-gradient(90deg, var(--border2) 0, var(--border2) 8px, transparent 8px, transparent 12px);
    margin: 16px 0;
  }

  .mt16 { margin-top: 16px; }

  @keyframes screenFlash {
    0% { opacity: 0; }
    30% { opacity: 1; }
    100% { opacity: 0; }
  }

  .flash-overlay {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: white;
    z-index: 998;
    pointer-events: none;
    opacity: 0;
  }

  .flash-overlay.active {
    animation: screenFlash 0.4s ease-out forwards;
  }
</style>
</head>
<body>

<!-- Top scrolling bar -->
<div class="top-bar">
  <span class="marquee-text">★ MISSION: FOOD ★ PLAYER: ANH DUONG ★ OBJECTIVE: CHOOSE A RESTAURANT ★ GOOD LUCK! ★ MISSION: FOOD ★</span>
</div>

<!-- Starfield -->
<div class="starfield" id="starfield"></div>

<!-- Flash overlay -->
<div class="flash-overlay" id="flashOverlay"></div>

<!-- Confetti canvas -->
<canvas id="confetti-canvas"></canvas>

<!-- ===== PAGE 1: INTRO ===== -->
<div class="page active" id="page-intro" style="padding-top:56px;">

  <div class="game-header">★ MISSION: FOOD ★</div>
  <div class="sub-header">— QUEST BOARD —</div>

  <div style="font-size:11px;color:var(--cyan);text-align:center;margin-bottom:16px">
    ♥ ♥ ♥
  </div>

  <!-- Pixel character sprite (chef/guide) -->
  <div class="sprite-wrap">
    <!-- Pixel art guide character made with SVG -->
    <svg class="pixel-sprite" width="112" height="112" viewBox="0 0 56 56" fill="none" xmlns="http://www.w3.org/2000/svg" style="image-rendering:pixelated; width:112px; height:112px;">

      <!-- HAIR BACK -->
      <rect x="10" y="5"  width="3"  height="18" fill="#b01010"/>
      <rect x="43" y="5"  width="3"  height="18" fill="#b01010"/>
      <rect x="10" y="20" width="4"  height="5"  fill="#901000"/>
      <rect x="42" y="20" width="4"  height="5"  fill="#901000"/>

      <!-- HEAD -->
      <rect x="13" y="6"  width="30" height="20" fill="#fdd9b5"/>
      <rect x="11" y="8"  width="2"  height="16" fill="#fdd9b5"/>
      <rect x="43" y="8"  width="2"  height="16" fill="#fdd9b5"/>

      <!-- RED HAIR TOP -->
      <rect x="11" y="2"  width="34" height="6"  fill="#cc1818"/>
      <rect x="9"  y="4"  width="38" height="4"  fill="#cc1818"/>
      <rect x="13" y="1"  width="30" height="2"  fill="#aa1010"/>
      <!-- highlight -->
      <rect x="19" y="2"  width="10" height="2"  fill="#e84040" opacity="0.7"/>

      <!-- BANGS -->
      <rect x="11" y="6"  width="34" height="5"  fill="#cc1818"/>
      <rect x="11" y="11" width="5"  height="3"  fill="#cc1818"/>
      <rect x="17" y="10" width="4"  height="3"  fill="#cc1818"/>
      <rect x="35" y="10" width="4"  height="3"  fill="#cc1818"/>
      <rect x="40" y="11" width="5"  height="3"  fill="#cc1818"/>
      <!-- bob sides -->
      <rect x="11" y="11" width="3"  height="10" fill="#cc1818"/>
      <rect x="42" y="11" width="3"  height="10" fill="#cc1818"/>
      <rect x="11" y="20" width="4"  height="4"  fill="#aa1010"/>
      <rect x="41" y="20" width="4"  height="4"  fill="#aa1010"/>

      <!-- YELLOW FLOWER CLIP -->
      <rect x="37" y="4"  width="5"  height="5"  fill="#f8e000"/>
      <rect x="35" y="6"  width="9"  height="3"  fill="#f8e000"/>
      <rect x="39" y="3"  width="3"  height="7"  fill="#ffffa0"/>
      <rect x="37" y="6"  width="5"  height="3"  fill="#f0a800"/>
      <rect x="39" y="6"  width="2"  height="2"  fill="#ff8000"/>

      <!-- LEFT EYE -->
      <rect x="15" y="15" width="8"  height="6"  fill="#ffffff"/>
      <rect x="16" y="16" width="6"  height="4"  fill="#4848d0"/>
      <rect x="17" y="17" width="4"  height="3"  fill="#101028"/>
      <rect x="17" y="17" width="2"  height="2"  fill="#ffffff"/>
      <rect x="15" y="14" width="3"  height="2"  fill="#101028"/>
      <rect x="20" y="14" width="2"  height="1"  fill="#101028"/>

      <!-- RIGHT EYE -->
      <rect x="33" y="15" width="8"  height="6"  fill="#ffffff"/>
      <rect x="34" y="16" width="6"  height="4"  fill="#4848d0"/>
      <rect x="35" y="17" width="4"  height="3"  fill="#101028"/>
      <rect x="35" y="17" width="2"  height="2"  fill="#ffffff"/>
      <rect x="34" y="14" width="2"  height="1"  fill="#101028"/>
      <rect x="38" y="14" width="3"  height="2"  fill="#101028"/>

      <!-- NOSE -->
      <rect x="27" y="20" width="3"  height="1"  fill="#e8a878" opacity="0.9"/>

      <!-- SMILE -->
      <rect x="21" y="22" width="3"  height="1"  fill="#c06050"/>
      <rect x="32" y="22" width="3"  height="1"  fill="#c06050"/>
      <rect x="23" y="23" width="10" height="1"  fill="#c06050"/>
      <rect x="25" y="22" width="6"  height="1"  fill="#efa090"/>

      <!-- BLUSH -->
      <rect x="12" y="19" width="5"  height="3"  fill="#ffb0a0" opacity="0.55"/>
      <rect x="39" y="19" width="5"  height="3"  fill="#ffb0a0" opacity="0.55"/>

      <!-- NECK -->
      <rect x="23" y="26" width="10" height="3"  fill="#fdd9b5"/>

      <!-- WHITE DRESS BODY -->
      <rect x="14" y="29" width="28" height="16" fill="#f4f4ff"/>
      <rect x="10" y="32" width="36" height="13" fill="#f4f4ff"/>
      <!-- dress flare -->
      <rect x="7"  y="43" width="42" height="5"  fill="#f0f0ff"/>
      <rect x="5"  y="46" width="46" height="3"  fill="#ebebff"/>
      <!-- lace hem -->
      <rect x="5"  y="48" width="46" height="2"  fill="#dcdcff"/>
      <rect x="7"  y="50" width="4"  height="2"  fill="#dcdcff"/>
      <rect x="14" y="50" width="4"  height="2"  fill="#dcdcff"/>
      <rect x="21" y="50" width="4"  height="2"  fill="#dcdcff"/>
      <rect x="28" y="50" width="4"  height="2"  fill="#dcdcff"/>
      <rect x="35" y="50" width="4"  height="2"  fill="#dcdcff"/>
      <rect x="42" y="50" width="4"  height="2"  fill="#dcdcff"/>
      <!-- collar -->
      <rect x="20" y="28" width="16" height="3"  fill="#ffffff"/>
      <rect x="18" y="29" width="20" height="2"  fill="#e8e8ff"/>
      <!-- pink ribbon -->
      <rect x="16" y="37" width="24" height="4"  fill="#f060b0"/>
      <rect x="24" y="34" width="8"  height="8"  fill="#f060b0"/>
      <rect x="26" y="35" width="4"  height="4"  fill="#ff90d0"/>

      <!-- LEFT SLEEVE (normal arm down) -->
      <rect x="8"  y="29" width="6"  height="9"  fill="#f4f4ff"/>
      <rect x="7"  y="36" width="8"  height="2"  fill="#dcdcff"/>
      <!-- left arm (skin) -->
      <rect x="8"  y="38" width="6"  height="8"  fill="#fdd9b5"/>
      <!-- left hand normal -->
      <rect x="8"  y="45" width="6"  height="4"  fill="#fdd9b5"/>
      <rect x="8"  y="44" width="2"  height="2"  fill="#fdd9b5"/>
      <rect x="11" y="44" width="2"  height="2"  fill="#fdd9b5"/>

      <!-- RIGHT ARM RAISED (doing finger heart) -->
      <!-- upper arm going up -->
      <rect x="42" y="22" width="6"  height="10" fill="#fdd9b5"/>
      <!-- white sleeve on upper arm -->
      <rect x="42" y="29" width="6"  height="6"  fill="#f4f4ff"/>
      <rect x="42" y="34" width="6"  height="2"  fill="#dcdcff"/>
      <!-- forearm angled up-right -->
      <rect x="44" y="10" width="5"  height="14" fill="#fdd9b5"/>
      <!-- FINGER HEART HAND -->
      <!-- palm -->
      <rect x="44" y="4"  width="8"  height="8"  fill="#fdd9b5"/>
      <!-- index finger up-left -->
      <rect x="44" y="0"  width="3"  height="6"  fill="#fdd9b5"/>
      <!-- thumb up-right crossing -->
      <rect x="49" y="1"  width="3"  height="5"  fill="#fdd9b5"/>
      <!-- heart shape where tips cross -->
      <rect x="45" y="0"  width="2"  height="2"  fill="#ff3060"/>
      <rect x="49" y="0"  width="2"  height="2"  fill="#ff3060"/>
      <rect x="44" y="1"  width="8"  height="2"  fill="#ff3060"/>
      <rect x="45" y="3"  width="6"  height="2"  fill="#ff3060"/>
      <rect x="46" y="5"  width="4"  height="1"  fill="#ff3060"/>
      <rect x="47" y="6"  width="2"  height="1"  fill="#ff3060"/>
      <!-- heart shine -->
      <rect x="45" y="1"  width="2"  height="1"  fill="#ff90b0"/>

      <!-- LEGS -->
      <rect x="18" y="51" width="8"  height="5"  fill="#fdd9b5"/>
      <rect x="30" y="51" width="8"  height="5"  fill="#fdd9b5"/>

      <!-- SHOES -->
      <rect x="15" y="54" width="13" height="4"  fill="#5a1e00"/>
      <rect x="28" y="54" width="13" height="4"  fill="#5a1e00"/>
      <rect x="18" y="52" width="7"  height="2"  fill="#5a1e00"/>
      <rect x="31" y="52" width="7"  height="2"  fill="#5a1e00"/>
      <rect x="16" y="54" width="4"  height="2"  fill="#8b4020" opacity="0.6"/>
      <rect x="29" y="54" width="4"  height="2"  fill="#8b4020" opacity="0.6"/>

      <!-- SPARKLES -->
      <rect x="1"  y="8"  width="3"  height="3"  fill="#f8e800"/>
      <rect x="0"  y="9"  width="5"  height="1"  fill="#f8e800"/>
      <rect x="1"  y="36" width="3"  height="3"  fill="#a0f820"/>
      <rect x="0"  y="37" width="5"  height="1"  fill="#a0f820"/>
      <!-- extra sparkle near heart -->
      <rect x="39" y="2"  width="3"  height="3"  fill="#f820a8"/>
      <rect x="38" y="3"  width="5"  height="1"  fill="#f820a8"/>
      <rect x="34" y="0"  width="2"  height="2"  fill="#f8e800"/>
      <rect x="33" y="1"  width="4"  height="1"  fill="#f8e800"/>
    </svg>
  </div>

  <div class="pixel-panel">
    <div class="title-bar">
      <span class="title-bar-text">GUIDE ANGIE</span>
      <div class="title-bar-dots">
        <div class="dot r"></div>
        <div class="dot y"></div>
        <div class="dot g"></div>
      </div>
    </div>

    <div class="dialogue-box">
      <div class="dialogue-name">▶ ANGIE:</div>
      <div class="dialogue-text" id="introText"></div>
    </div>

    <div class="pixel-divider"></div>

    <button class="pixel-btn" id="continueBtn" onclick="goToBoxes()" style="display:none">
      ▶ ACCEPT MISSION
    </button>
    <div class="press-start" id="pressStart" style="display:none">▼ PRESS TO CONTINUE</div>
  </div>
</div>

<!-- ===== PAGE 2: BOX SELECTION ===== -->
<div class="page" id="page-boxes" style="padding-top:56px;">

  <div class="game-header">CHOOSE YOUR BOX</div>
  <div class="sub-header">— 4 MYSTERY CHESTS —</div>
  <div style="font-size:11px;color:var(--red);text-align:center;margin-bottom:16px">♥ ♥ ♥</div>

  <div class="boxes-grid" id="boxesGrid">
    <div class="gift-box" id="box-0" onclick="openBox(0)">
      <span class="box-num">BOX 1</span>
      <span class="box-icon">📦</span>
      <div class="box-label">??? <br>MYSTERY<br>CHEST</div>
    </div>
    <div class="gift-box" id="box-1" onclick="openBox(1)">
      <span class="box-num">BOX 2</span>
      <span class="box-icon">🎁</span>
      <div class="box-label">??? <br>MYSTERY<br>CHEST</div>
    </div>
    <div class="gift-box" id="box-2" onclick="openBox(2)">
      <span class="box-num">BOX 3</span>
      <span class="box-icon">📦</span>
      <div class="box-label">??? <br>MYSTERY<br>CHEST</div>
    </div>
    <div class="gift-box" id="box-3" onclick="openBox(3)">
      <span class="box-num">BOX 4</span>
      <span class="box-icon">🎁</span>
      <div class="box-label">??? <br>MYSTERY<br>CHEST</div>
    </div>
  </div>

  <div class="pixel-panel" style="max-width:360px">
    <div class="title-bar">
      <span class="title-bar-text">MISSION BRIEF</span>
      <div class="title-bar-dots">
        <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
      </div>
    </div>
    <div style="color:var(--white);font-size:7px;line-height:2.2;text-align:center;">
      TAP A CHEST TO<br>REVEAL YOUR<br>RESTAURANT DESTINY!
    </div>
  </div>
</div>

<!-- ===== PAGE 3: RESULT ===== -->
<div class="page" id="page-result" style="padding-top:56px;">

  <div class="result-header">★ QUEST COMPLETE! ★</div>
  <div class="result-score" id="resultScore">SCORE: +9999 EXP</div>

  <div class="pixel-panel">
    <div class="title-bar">
      <span class="title-bar-text">MISSION RESULT</span>
      <div class="title-bar-dots">
        <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
      </div>
    </div>

    <span class="result-icon" id="resultEmoji">🍜</span>
    <div style="color:var(--cyan);font-size:7px;text-align:center;margin-bottom:6px;letter-spacing:1px">DESTINATION UNLOCKED:</div>
    <div class="result-name" id="resultName">OTTUGI</div>

    <div class="pixel-divider"></div>

    <div class="hp-bar-wrap">
      <div class="hp-label">HUNGER METER:</div>
      <div class="hp-bar"><div class="hp-fill" id="hpFill"></div></div>
    </div>

    <div class="result-msg" id="resultMsg">YOUR FOOD DESTINY<br>HAS BEEN DECIDED!</div>

    <div class="pixel-divider"></div>

    <button class="pixel-btn cyan mt16" onclick="resetGame()">
      ↺ PLAY AGAIN
    </button>
  </div>

</div>

<script>
const restaurants = [
  { name: "CULTRA TAPROOM",   emoji: "🍝", msg: "FUSION ITALIAN QUEST!\nCRAFT PASTA POWER UP!" },
  { name: "MEDITERRANEO",     emoji: "🫒", msg: "MED CUISINE AWAITS!\n+10 OLIVE OIL BONUS!" },
  { name: "PIZZA 4PS",        emoji: "🍕", msg: "PIZZA DUNGEON!\nFARM TO TABLE POWER UP!" },
  { name: "CHOPS BURGER",     emoji: "🍔", msg: "BURGER BOSS FIGHT!\nSTAMINA FULLY RESTORED!" }
];

let shuffled = [];

// Stars
(function() {
  const sf = document.getElementById('starfield');
  for (let i = 0; i < 60; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    s.style.left = Math.random() * 100 + '%';
    s.style.top  = Math.random() * 100 + '%';
    s.style.animationDuration = (1.5 + Math.random() * 3) + 's';
    s.style.animationDelay = (Math.random() * 3) + 's';
    s.style.width = s.style.height = (Math.random() > 0.7 ? '4px' : '2px');
    s.style.opacity = 0.4 + Math.random() * 0.6;
    sf.appendChild(s);
  }
})();

// Typewriter
function typewrite(el, text, speed, cb) {
  el.innerHTML = '';
  let i = 0;
  const span = document.createElement('span');
  span.className = 'typewriter';
  el.appendChild(span);
  const iv = setInterval(() => {
    if (i < text.length) {
      span.textContent += text[i++];
    } else {
      clearInterval(iv);
      span.classList.remove('typewriter');
      if (cb) cb();
    }
  }, speed);
}

// Intro typewriter
window.addEventListener('load', () => {
  const el = document.getElementById('introText');
  const msg = 'Could you do a\nfavor by letting\nyour intuition\nguide?\n\nMoa moa ~';
  typewrite(el, msg, 42, () => {
    document.getElementById('continueBtn').style.display = 'block';
    document.getElementById('pressStart').style.display = 'none';
  });
});

function shuffle(arr) {
  const a = [...arr];
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

function goToBoxes() {
  shuffled = shuffle(restaurants);
  // Reset boxes
  for (let i = 0; i < 4; i++) {
    const b = document.getElementById('box-' + i);
    b.className = 'gift-box';
    b.onclick = () => openBox(i);
    b.innerHTML = `
      <span class="box-num">BOX ${i+1}</span>
      <span class="box-icon">${i % 2 === 0 ? '📦' : '🎁'}</span>
      <div class="box-label">???<br>MYSTERY<br>CHEST</div>
    `;
  }
  showPage('page-boxes');
}

function flashScreen() {
  const f = document.getElementById('flashOverlay');
  f.classList.remove('active');
  void f.offsetWidth;
  f.classList.add('active');
}

function openBox(index) {
  const box = document.getElementById('box-' + index);
  if (box.classList.contains('opened')) return;

  // Play shake
  box.classList.add('shake');
  setTimeout(() => {
    box.classList.remove('shake');
    box.classList.add('opened');
    box.onclick = null;

    const rest = shuffled[index];
    flashScreen();

    box.innerHTML = `
      <span class="box-num">BOX ${index+1}</span>
      <div class="box-reveal-icon">${rest.emoji}</div>
      <div class="box-reveal">${rest.name}</div>
    `;

    setTimeout(() => showResult(rest), 700);
  }, 350);
}

function showResult(rest) {
  document.getElementById('resultEmoji').textContent = rest.emoji;
  document.getElementById('resultName').textContent = rest.name;
  document.getElementById('resultMsg').innerHTML = rest.msg.replace(/\n/g, '<br>');
  document.getElementById('resultScore').textContent = 'SCORE: +' + (Math.floor(Math.random()*9000)+1000) + ' EXP';

  // Reset HP bar animation
  const hp = document.getElementById('hpFill');
  hp.style.animation = 'none';
  void hp.offsetWidth;
  hp.style.animation = '';

  showPage('page-result');
  launchPixelConfetti();
}

function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0, 0);
}

function resetGame() {
  showPage('page-intro');
  const el = document.getElementById('introText');
  document.getElementById('continueBtn').style.display = 'none';
  document.getElementById('pressStart').style.display = 'none';
  const msg = 'Could you do a\nfavor by letting\nyour intuition\nguide?\n\nMoa moa ~';
  typewrite(el, msg, 42, () => {
    document.getElementById('continueBtn').style.display = 'block';
  });
}

// Pixel confetti
const canvas = document.getElementById('confetti-canvas');
const ctx = canvas.getContext('2d');
let pieces = [], animId;
const colors = ['#f8e800','#e82020','#20e840','#20e8f8','#f820a8','#f89820','#5858f8','#a0a0ff'];

function launchPixelConfetti() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  pieces = [];
  for (let i = 0; i < 80; i++) {
    pieces.push({
      x: Math.random() * canvas.width,
      y: -10,
      size: (Math.random() > 0.5 ? 8 : 6),
      color: colors[Math.floor(Math.random() * colors.length)],
      vx: (Math.random() - 0.5) * 6,
      vy: 2 + Math.random() * 5,
      life: 1
    });
  }
  cancelAnimationFrame(animId);
  drawConfetti();
  setTimeout(() => { cancelAnimationFrame(animId); ctx.clearRect(0,0,canvas.width,canvas.height); }, 3500);
}

function drawConfetti() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  let alive = false;
  pieces.forEach(p => {
    if (p.y > canvas.height + 20) return;
    alive = true;
    p.x += p.vx;
    p.y += p.vy;
    p.vy += 0.12;
    ctx.globalAlpha = Math.max(0, p.life);
    ctx.fillStyle = p.color;
    // Pixel squares
    ctx.fillRect(Math.round(p.x), Math.round(p.y), p.size, p.size);
  });
  ctx.globalAlpha = 1;
  if (alive) animId = requestAnimationFrame(drawConfetti);
}
</script>
</body>
</html>
