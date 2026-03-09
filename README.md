<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>CASE FILE: CLASSIFIED</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0d0d0a;--panel:#1a1a14;--border:#8a7a3a;--border2:#c8b060;
  --amber:#e8a020;--yellow:#d4a820;--red:#c02020;--green:#40a040;
  --cream:#c8c090;--stamp:#8b1a1a;--paper:#1e1c12;--folder:#6a4e22;--pixel:4px;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Press Start 2P',monospace;background-color:var(--bg);min-height:100vh;overflow-x:hidden;position:relative;cursor:default;image-rendering:pixelated;}
body::after{content:'';position:fixed;top:0;left:0;width:100%;height:100%;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.13) 2px,rgba(0,0,0,0.13) 3px);pointer-events:none;z-index:9999;}
.dust{position:fixed;width:2px;height:2px;background:#c8a030;opacity:0;pointer-events:none;z-index:2;animation:dustFloat linear infinite;}
@keyframes dustFloat{0%{transform:translateY(105vh);opacity:0}8%{opacity:0.4}92%{opacity:0.15}100%{transform:translateY(-5vh) translateX(12px);opacity:0}}
.page{display:none;position:relative;z-index:10;min-height:100vh;padding:24px 16px 52px;flex-direction:column;align-items:center;justify-content:center;}
.page.active{display:flex;}
.pixel-panel{background:var(--paper);border:var(--pixel) solid var(--border);box-shadow:0 0 0 var(--pixel) #000,5px 5px 0 #000,0 0 24px rgba(200,160,40,0.08);padding:24px 20px;width:100%;max-width:360px;position:relative;}
.pixel-panel::before{content:'&#9642;';position:absolute;top:6px;left:8px;color:var(--border2);font-size:8px;}
.pixel-panel::after{content:'&#9642;';position:absolute;bottom:6px;right:8px;color:var(--border2);font-size:8px;}
.title-bar{background:var(--folder);margin:-24px -20px 20px;padding:10px 14px;display:flex;align-items:center;justify-content:space-between;border-bottom:var(--pixel) solid var(--border2);}
.title-bar-text{color:var(--cream);font-size:6px;letter-spacing:1px;text-shadow:1px 1px 0 #000;}
.title-bar-dots{display:flex;gap:5px;}
.dot{width:10px;height:10px;border:2px solid rgba(0,0,0,0.5);}
.dot.r{background:#6a1010;}.dot.y{background:var(--yellow);}.dot.g{background:var(--green);}
.sprite-wrap{display:flex;justify-content:center;margin-bottom:8px;}
.pixel-sprite{image-rendering:pixelated;animation:sway 3s ease-in-out infinite;display:block;margin:0 auto;filter:drop-shadow(0 4px 14px rgba(200,160,32,0.3));}
@keyframes sway{0%,100%{transform:translateY(0px)}50%{transform:translateY(-6px)}}
.dialogue-box{background:#0a0a06;border:var(--pixel) solid var(--border);padding:14px;margin-bottom:18px;position:relative;min-height:86px;}
.dialogue-box::before{content:'&#9660;';position:absolute;bottom:6px;right:10px;color:var(--amber);font-size:7px;animation:blink 0.9s step-end infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
.dialogue-name{color:var(--amber);font-size:6px;margin-bottom:10px;letter-spacing:1px;}
.dialogue-text{color:var(--cream);font-size:7px;line-height:2.2;}
.typewriter{display:inline;border-right:2px solid var(--amber);animation:cur 0.7s step-end infinite;white-space:pre-wrap;word-break:break-word;}
@keyframes cur{0%,100%{border-color:var(--amber)}50%{border-color:transparent}}
.pixel-btn{font-family:'Press Start 2P',monospace;font-size:7px;background:var(--folder);color:var(--cream);border:none;padding:14px 20px;cursor:pointer;width:100%;text-align:center;letter-spacing:1px;box-shadow:4px 4px 0 #000;transition:transform 0.08s,box-shadow 0.08s;display:block;}
.pixel-btn:hover{background:#8a6830;transform:translate(-2px,-2px);box-shadow:6px 6px 0 #000;}
.pixel-btn:active{transform:translate(2px,2px);box-shadow:2px 2px 0 #000;}
.pixel-btn.red-btn{background:var(--stamp);color:#ffcccc;}
.pixel-btn.red-btn:hover{background:#a02020;}
.game-header{text-align:center;margin-bottom:6px;color:var(--amber);font-size:8px;text-shadow:2px 2px 0 #000,0 0 14px rgba(232,160,32,0.4);letter-spacing:2px;animation:flicker 5s ease-in-out infinite;}
@keyframes flicker{0%,93%,96%,99%,100%{opacity:1}94%,97%{opacity:0.3}}
.sub-header{text-align:center;color:var(--cream);font-size:6px;margin-bottom:6px;letter-spacing:2px;opacity:0.6;}
.stamp{display:inline-block;border:3px solid var(--stamp);color:var(--stamp);font-size:7px;padding:4px 10px;letter-spacing:3px;transform:rotate(-7deg);box-shadow:2px 2px 0 rgba(139,26,26,0.3);margin-bottom:12px;animation:sp 3.5s ease-in-out infinite;}
@keyframes sp{0%,100%{opacity:1}50%{opacity:0.65}}
.case-badge{text-align:center;color:var(--border2);font-size:5px;letter-spacing:2px;margin-bottom:10px;opacity:0.55;}
.boxes-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;width:100%;max-width:360px;margin-bottom:14px;}
.gift-box{background:var(--paper);border:var(--pixel) solid var(--border);padding:16px 10px 14px;display:flex;flex-direction:column;align-items:center;justify-content:center;cursor:pointer;transition:transform 0.08s,box-shadow 0.08s;box-shadow:4px 4px 0 #000;min-height:120px;position:relative;-webkit-tap-highlight-color:transparent;overflow:hidden;}
.gift-box::before{content:'';position:absolute;top:0;left:0;right:0;height:5px;background:var(--folder);}
.gift-box:hover{transform:translate(-2px,-2px);box-shadow:6px 6px 0 #000;border-color:var(--amber);}
.gift-box:active{transform:translate(2px,2px);box-shadow:2px 2px 0 #000;}
.gift-box.opened{cursor:default;border-color:var(--red);pointer-events:none;}
.gift-box.opened::before{background:var(--stamp);}
.gift-box.shake{animation:shk 0.3s steps(2) forwards;}
@keyframes shk{0%{transform:translate(0,0)}25%{transform:translate(-4px,0)}50%{transform:translate(4px,-3px)}75%{transform:translate(-3px,3px)}100%{transform:translate(0,0)}}
.box-num{position:absolute;top:8px;right:8px;color:var(--border2);font-size:5px;letter-spacing:1px;}
.box-icon{font-size:30px;margin-bottom:8px;display:block;filter:sepia(0.7) brightness(0.8);}
.box-label{color:var(--cream);font-size:5px;text-align:center;line-height:2;opacity:0.7;}
.box-reveal{color:var(--amber);font-size:5px;text-align:center;line-height:1.9;text-shadow:0 0 6px rgba(232,160,32,0.6);}
.box-reveal-icon{font-size:24px;margin-bottom:6px;animation:pop 0.2s steps(3) forwards;}
@keyframes pop{0%{transform:scale(0)}60%{transform:scale(1.2)}100%{transform:scale(1)}}
.result-header{text-align:center;color:var(--amber);font-size:8px;letter-spacing:2px;margin-bottom:12px;text-shadow:2px 2px 0 #000;animation:flicker 3s ease-in-out infinite;}
.result-score{text-align:center;color:var(--cream);font-size:5px;margin-bottom:16px;letter-spacing:1px;opacity:0.65;}
.result-icon{font-size:46px;display:block;text-align:center;margin-bottom:10px;animation:pop 0.3s steps(3) forwards;filter:sepia(0.4);}
.result-name{color:var(--amber);font-size:10px;text-align:center;margin-bottom:8px;text-shadow:2px 2px 0 #000,0 0 14px rgba(212,168,32,0.5);letter-spacing:2px;line-height:1.7;}
.result-msg{color:var(--cream);font-size:6px;text-align:center;line-height:2.4;margin-bottom:18px;opacity:0.85;}
.bar-wrap{margin-bottom:16px;}
.bar-label{color:var(--cream);font-size:5px;margin-bottom:6px;letter-spacing:1px;opacity:0.7;}
.bar{height:12px;background:#080806;border:3px solid var(--border);overflow:hidden;}
.bar-fill{height:100%;background:var(--amber);width:0%;animation:fill 1.2s steps(18) 0.3s forwards;box-shadow:inset 0 2px 0 rgba(255,255,255,0.15);}
@keyframes fill{to{width:100%;}}
.divider{height:var(--pixel);background:repeating-linear-gradient(90deg,var(--border) 0,var(--border) 6px,transparent 6px,transparent 10px);margin:14px 0;}
.top-bar{position:fixed;top:0;left:0;right:0;background:#120e02;border-bottom:2px solid var(--border);padding:5px 0;z-index:100;overflow:hidden;}
.mq{color:var(--amber);font-size:5px;white-space:nowrap;display:inline-block;animation:mq 22s linear infinite;letter-spacing:2px;opacity:0.75;}
@keyframes mq{0%{transform:translateX(100vw)}100%{transform:translateX(-100%)}}
.mt16{margin-top:16px;}
@keyframes flash{0%{opacity:0}20%{opacity:0.55}100%{opacity:0}}
.flash{position:fixed;top:0;left:0;width:100%;height:100%;background:#c8a020;z-index:998;pointer-events:none;opacity:0;}
.flash.go{animation:flash 0.35s ease-out forwards;}
#cc{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:500;image-rendering:pixelated;}
.room{position:fixed;bottom:0;left:0;right:0;z-index:1;pointer-events:none;}
</style>
</head>
<body>

<div class="top-bar">
  <span class="mq">&#9632; CLASSIFIED &#9632; CASE #4471-B &#9632; AUTHORIZED EYES ONLY &#9632; AGENT: ANH DUONG &#9632; CLEARANCE LEVEL 5 &#9632; NO COPIES PERMITTED &#9632;</span>
</div>

<!-- pixel office room -->
<svg class="room" viewBox="0 0 375 160" preserveAspectRatio="xMidYMax meet" xmlns="http://www.w3.org/2000/svg" style="image-rendering:pixelated;height:160px;">
  <rect x="0" y="118" width="375" height="42" fill="#0e0d07"/>
  <rect x="0" y="118" width="375" height="2" fill="#1c1a0e"/>
  <rect x="70" y="118" width="2" height="42" fill="#131108"/>
  <rect x="155" y="118" width="2" height="42" fill="#131108"/>
  <rect x="230" y="118" width="2" height="42" fill="#131108"/>
  <rect x="310" y="118" width="2" height="42" fill="#131108"/>
  <!-- left desk -->
  <rect x="0" y="90" width="90" height="30" fill="#28200a"/>
  <rect x="0" y="86" width="90" height="6" fill="#38300e"/>
  <rect x="6" y="118" width="14" height="42" fill="#1a1408"/>
  <rect x="68" y="118" width="14" height="42" fill="#1a1408"/>
  <!-- folders left -->
  <rect x="8" y="76" width="18" height="14" fill="#6a4e22"/><rect x="8" y="74" width="18" height="4" fill="#8a6830"/>
  <rect x="28" y="78" width="16" height="12" fill="#5a3e18"/><rect x="28" y="76" width="16" height="4" fill="#7a5828"/>
  <rect x="46" y="76" width="18" height="14" fill="#7a1818"/><rect x="46" y="74" width="18" height="4" fill="#9a2828"/>
  <!-- lamp left -->
  <rect x="62" y="68" width="4" height="20" fill="#383018"/>
  <rect x="54" y="62" width="20" height="7" fill="#c09828" opacity="0.9"/>
  <rect x="50" y="68" width="28" height="4" fill="#d0b040" opacity="0.5"/>
  <!-- right desk -->
  <rect x="285" y="90" width="90" height="30" fill="#28200a"/>
  <rect x="285" y="86" width="90" height="6" fill="#38300e"/>
  <rect x="291" y="118" width="14" height="42" fill="#1a1408"/>
  <rect x="358" y="118" width="14" height="42" fill="#1a1408"/>
  <!-- folders right -->
  <rect x="293" y="76" width="18" height="14" fill="#6a4e22"/><rect x="293" y="74" width="18" height="4" fill="#8a6830"/>
  <rect x="313" y="78" width="16" height="12" fill="#7a1818"/><rect x="313" y="76" width="16" height="4" fill="#9a2828"/>
  <rect x="331" y="76" width="18" height="14" fill="#5a3e18"/><rect x="331" y="74" width="18" height="4" fill="#7a5828"/>
  <!-- cork board center -->
  <rect x="112" y="0" width="152" height="84" fill="#382a14"/>
  <rect x="110" y="0" width="156" height="5" fill="#5a4222"/>
  <rect x="110" y="79" width="156" height="5" fill="#5a4222"/>
  <!-- pinned notes -->
  <rect x="120" y="8" width="32" height="22" fill="#c0b882" opacity="0.85" transform="rotate(-2 120 8)"/>
  <rect x="132" y="6" width="4" height="4" fill="#b02020" opacity="0.9"/>
  <rect x="160" y="10" width="28" height="20" fill="#b8b07a" opacity="0.8" transform="rotate(3 160 10)"/>
  <rect x="170" y="8" width="4" height="4" fill="#b02020" opacity="0.9"/>
  <rect x="196" y="6" width="30" height="20" fill="#c0b882" opacity="0.75" transform="rotate(-3 196 6)"/>
  <rect x="208" y="4" width="4" height="4" fill="#4040a0" opacity="0.9"/>
  <rect x="122" y="38" width="24" height="34" fill="#b8b07a" opacity="0.7" transform="rotate(-2 122 38)"/>
  <rect x="130" y="36" width="4" height="4" fill="#b02020" opacity="0.9"/>
  <rect x="194" y="38" width="32" height="24" fill="#c0b882" opacity="0.75" transform="rotate(4 194 38)"/>
  <rect x="206" y="36" width="4" height="4" fill="#b02020" opacity="0.9"/>
  <!-- red string -->
  <line x1="134" y1="8" x2="172" y2="12" stroke="#c02020" stroke-width="1.2" opacity="0.6"/>
  <line x1="172" y1="12" x2="210" y2="8" stroke="#c02020" stroke-width="1.2" opacity="0.6"/>
  <line x1="132" y1="40" x2="208" y2="40" stroke="#c02020" stroke-width="1.2" opacity="0.5"/>
  <line x1="134" y1="10" x2="132" y2="40" stroke="#c02020" stroke-width="1" opacity="0.4"/>
  <!-- rainy window left -->
  <rect x="0" y="6" width="102" height="78" fill="#0a1318" opacity="0.85"/>
  <rect x="0" y="6" width="102" height="78" fill="none" stroke="#38280c" stroke-width="4"/>
  <rect x="50" y="6" width="3" height="78" fill="#38280c"/>
  <rect x="0" y="44" width="102" height="3" fill="#38280c"/>
  <rect x="14" y="12" width="2" height="10" fill="#1c3050" opacity="0.38"/>
  <rect x="30" y="18" width="2" height="12" fill="#1c3050" opacity="0.3"/>
  <rect x="66" y="10" width="2" height="14" fill="#1c3050" opacity="0.38"/>
  <rect x="82" y="28" width="2" height="10" fill="#1c3050" opacity="0.3"/>
  <!-- filing cabinet right -->
  <rect x="330" y="20" width="45" height="98" fill="#1c1a10"/>
  <rect x="330" y="20" width="45" height="5" fill="#28261a"/>
  <rect x="330" y="52" width="45" height="3" fill="#28261a"/>
  <rect x="330" y="80" width="45" height="3" fill="#28261a"/>
  <rect x="346" y="38" width="12" height="4" fill="#484020"/>
  <rect x="346" y="64" width="12" height="4" fill="#484020"/>
  <rect x="346" y="90" width="12" height="4" fill="#484020"/>
</svg>

<div class="flash" id="fl"></div>
<canvas id="cc"></canvas>

<!-- PAGE 1: INTRO -->
<div class="page active" id="page-intro" style="padding-top:58px;">
  <div class="game-header">&#9632; CASE #4471-B &#9632;</div>
  <div class="sub-header">&#8212; DETECTIVE BUREAU &#8212;</div>
  <div class="case-badge">EYES ONLY // LEVEL 5 CLEARANCE</div>
  <div style="text-align:center;margin-bottom:14px;"><span class="stamp">CLASSIFIED</span></div>

  <!-- SIMPLE FEMALE DETECTIVE SPRITE -->
  <div class="sprite-wrap">
    <svg class="pixel-sprite" width="96" height="108" viewBox="0 0 48 54" fill="none" xmlns="http://www.w3.org/2000/svg" style="image-rendering:pixelated;width:96px;height:108px;">
      <!-- HAIR back (red bob) -->
      <rect x="10" y="10" width="3"  height="18" fill="#8a0c0c"/>
      <rect x="35" y="10" width="3"  height="18" fill="#8a0c0c"/>
      <!-- FEDORA brim -->
      <rect x="5"  y="9"  width="38" height="3"  fill="#161208"/>
      <rect x="3"  y="10" width="42" height="2"  fill="#161208"/>
      <!-- crown -->
      <rect x="12" y="3"  width="24" height="8"  fill="#1e1a08"/>
      <rect x="10" y="4"  width="28" height="7"  fill="#1e1a08"/>
      <!-- hat band amber -->
      <rect x="12" y="9"  width="20" height="2"  fill="#b88010"/>
      <!-- small bow right -->
      <rect x="32" y="8"  width="6"  height="4"  fill="#c89018"/>
      <rect x="34" y="7"  width="4"  height="6"  fill="#e8c040"/>
      <!-- dent top -->
      <rect x="20" y="3"  width="8"  height="2"  fill="#161208"/>
      <!-- HAIR colour on top/bangs -->
      <rect x="10" y="3"  width="28" height="8"  fill="#ae1010"/>
      <rect x="12" y="10" width="6"  height="4"  fill="#ae1010"/>
      <rect x="30" y="10" width="6"  height="4"  fill="#ae1010"/>
      <!-- HEAD -->
      <rect x="12" y="11" width="24" height="16" fill="#ecc07a"/>
      <rect x="10" y="13" width="2"  height="12" fill="#ecc07a"/>
      <rect x="36" y="13" width="2"  height="12" fill="#ecc07a"/>
      <!-- EYES simple (2 rects each) -->
      <rect x="14" y="17" width="7"  height="4"  fill="#fff"/>
      <rect x="15" y="18" width="5"  height="3"  fill="#080808"/>
      <rect x="15" y="18" width="2"  height="1"  fill="#fff" opacity="0.5"/>
      <!-- lashes top left -->
      <rect x="14" y="15" width="7"  height="2"  fill="#080808"/>
      <rect x="27" y="17" width="7"  height="4"  fill="#fff"/>
      <rect x="28" y="18" width="5"  height="3"  fill="#080808"/>
      <rect x="28" y="18" width="2"  height="1"  fill="#fff" opacity="0.5"/>
      <!-- lashes top right -->
      <rect x="27" y="15" width="7"  height="2"  fill="#080808"/>
      <!-- BLUSH simple -->
      <rect x="10" y="21" width="5"  height="3"  fill="#f0a080" opacity="0.4"/>
      <rect x="33" y="21" width="5"  height="3"  fill="#f0a080" opacity="0.4"/>
      <!-- MOUTH red lip -->
      <rect x="18" y="24" width="12" height="2"  fill="#a01414"/>
      <!-- NECK -->
      <rect x="20" y="27" width="8"  height="4"  fill="#ecc07a"/>
      <!-- TRENCH COAT body (simple block) -->
      <rect x="10" y="30" width="28" height="18" fill="#38280e"/>
      <rect x="7"  y="34" width="34" height="14" fill="#38280e"/>
      <!-- lapels simple V -->
      <rect x="18" y="30" width="6"  height="8"  fill="#48381a"/>
      <rect x="24" y="30" width="6"  height="8"  fill="#48381a"/>
      <rect x="20" y="30" width="4"  height="5"  fill="#38280e"/>
      <rect x="24" y="30" width="4"  height="5"  fill="#38280e"/>
      <!-- belt -->
      <rect x="12" y="42" width="24" height="3"  fill="#281c06"/>
      <rect x="21" y="41" width="6"  height="5"  fill="#48381a"/>
      <rect x="22" y="42" width="4"  height="3"  fill="#c0880c"/>
      <!-- coat flare (A-line) -->
      <rect x="5"  y="46" width="38" height="4"  fill="#30200a"/>
      <rect x="3"  y="49" width="42" height="3"  fill="#2a1c08"/>
      <!-- LEFT ARM — magnifying glass (simple) -->
      <rect x="4"  y="31" width="7"  height="14" fill="#38280e"/>
      <rect x="2"  y="43" width="8"  height="6"  fill="#ecc07a"/>
      <!-- handle -->
      <rect x="0"  y="47" width="5"  height="7"  fill="#886028"/>
      <!-- mag frame (simple box) -->
      <rect x="1"  y="31" width="8"  height="2"  fill="#c0900c"/>
      <rect x="1"  y="41" width="8"  height="2"  fill="#c0900c"/>
      <rect x="1"  y="31" width="2"  height="12" fill="#c0900c"/>
      <rect x="7"  y="31" width="2"  height="12" fill="#c0900c"/>
      <!-- lens -->
      <rect x="3"  y="33" width="4"  height="8"  fill="#182030" opacity="0.7"/>
      <rect x="3"  y="33" width="2"  height="2"  fill="#fff" opacity="0.25"/>
      <!-- RIGHT ARM — raised, finger heart -->
      <rect x="37" y="28" width="7"  height="12" fill="#38280e"/>
      <rect x="37" y="38" width="7"  height="6"  fill="#ecc07a"/>
      <rect x="37" y="26" width="7"  height="10" fill="#ecc07a"/>
      <!-- index up -->
      <rect x="37" y="20" width="3"  height="8"  fill="#ecc07a"/>
      <!-- thumb -->
      <rect x="41" y="21" width="3"  height="7"  fill="#ecc07a"/>
      <!-- heart pixels -->
      <rect x="38" y="20" width="2"  height="2"  fill="#b81010"/>
      <rect x="42" y="20" width="2"  height="2"  fill="#b81010"/>
      <rect x="37" y="21" width="7"  height="2"  fill="#b81010"/>
      <rect x="38" y="23" width="5"  height="2"  fill="#b81010"/>
      <rect x="39" y="25" width="3"  height="1"  fill="#b81010"/>
      <rect x="40" y="26" width="2"  height="1"  fill="#b81010"/>
      <rect x="38" y="21" width="2"  height="1"  fill="#e85070"/>
      <!-- LEGS -->
      <rect x="16" y="51" width="6"  height="3"  fill="#281e14"/>
      <rect x="26" y="51" width="6"  height="3"  fill="#281e14"/>
      <!-- SHOES simple block + heel -->
      <rect x="13" y="52" width="10" height="2"  fill="#0e0a04"/>
      <rect x="25" y="52" width="10" height="2"  fill="#0e0a04"/>
      <rect x="19" y="53" width="4"  height="2"  fill="#0e0a04"/>
      <rect x="31" y="53" width="4"  height="2"  fill="#0e0a04"/>
      <!-- sparkle left -->
      <rect x="0"  y="15" width="2"  height="2"  fill="#d4a820"/>
      <rect x="1"  y="13" width="1"  height="6"  fill="#d4a820" opacity="0.5"/>
      <!-- sparkle right -->
      <rect x="45" y="10" width="2"  height="2"  fill="#d4a820"/>
      <rect x="46" y="8"  width="1"  height="6"  fill="#d4a820" opacity="0.5"/>
      <!-- heart sparkle near hand -->
      <rect x="44" y="18" width="2"  height="2"  fill="#b81010" opacity="0.7"/>
    </svg>
  </div>

  <div class="pixel-panel">
    <div class="title-bar">
      <span class="title-bar-text">DET. ANGIE // ON DUTY</span>
      <div class="title-bar-dots"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div></div>
    </div>
    <div class="dialogue-box">
      <div class="dialogue-name">&#9654; DET. ANGIE:</div>
      <div class="dialogue-text" id="introText"></div>
    </div>
    <div class="divider"></div>
    <button class="pixel-btn" id="continueBtn" onclick="goToBoxes()" style="display:none">&#9654; EXAMINE DOSSIERS</button>
  </div>
</div>

<!-- PAGE 2: FILE SELECTION -->
<div class="page" id="page-boxes" style="padding-top:58px;">
  <div class="game-header">&#9632; OPEN A DOSSIER &#9632;</div>
  <div class="sub-header">&#8212; 4 SEALED CASE FILES &#8212;</div>
  <div style="text-align:center;margin-bottom:14px;"><span class="stamp">DO NOT OPEN</span></div>

  <div class="boxes-grid" id="boxesGrid">
    <div class="gift-box" id="box-0" onclick="openBox(0)"><span class="box-num">FILE 01</span><span class="box-icon">&#128193;</span><div class="box-label">SEALED<br>DOSSIER<br>&#9608;&#9608;&#9608;</div></div>
    <div class="gift-box" id="box-1" onclick="openBox(1)"><span class="box-num">FILE 02</span><span class="box-icon">&#128194;</span><div class="box-label">SEALED<br>DOSSIER<br>&#9608;&#9608;&#9608;</div></div>
    <div class="gift-box" id="box-2" onclick="openBox(2)"><span class="box-num">FILE 03</span><span class="box-icon">&#128193;</span><div class="box-label">SEALED<br>DOSSIER<br>&#9608;&#9608;&#9608;</div></div>
    <div class="gift-box" id="box-3" onclick="openBox(3)"><span class="box-num">FILE 04</span><span class="box-icon">&#128194;</span><div class="box-label">SEALED<br>DOSSIER<br>&#9608;&#9608;&#9608;</div></div>
  </div>

  <div class="pixel-panel" style="max-width:360px">
    <div class="title-bar">
      <span class="title-bar-text">FIELD NOTES</span>
      <div class="title-bar-dots"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div></div>
    </div>
    <div style="color:var(--cream);font-size:6px;line-height:2.4;text-align:center;opacity:0.8;">FOLLOW YOUR GUT.<br>TAP A FILE TO<br>CRACK IT OPEN.</div>
  </div>
</div>

<!-- PAGE 3: RESULT -->
<div class="page" id="page-result" style="padding-top:58px;">
  <div class="result-header">&#9632; LEAD CONFIRMED &#9632;</div>
  <div class="result-score" id="resultScore">INTEL SCORE: &#9608;&#9608;&#9608;&#9608; PTS</div>

  <div class="pixel-panel">
    <div class="title-bar">
      <span class="title-bar-text">MISSION ISSUED</span>
      <div class="title-bar-dots"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div></div>
    </div>
    <span class="result-icon" id="resultEmoji">&#128269;</span>
    <div style="color:var(--cream);font-size:5px;text-align:center;margin-bottom:6px;letter-spacing:2px;opacity:0.65;">YOUR NEXT MOVE:</div>
    <div class="result-name" id="resultName">???</div>
    <div class="divider"></div>
    <div class="bar-wrap">
      <div class="bar-label">OPERATIVE READINESS:</div>
      <div class="bar"><div class="bar-fill" id="barFill"></div></div>
    </div>
    <div class="result-msg" id="resultMsg">DECODING...</div>
    <div class="divider"></div>
    <div style="text-align:center;margin-bottom:14px;"><span class="stamp">CASE CLOSED</span></div>
    <button class="pixel-btn red-btn mt16" onclick="resetGame()">&#8635; PULL A NEW FILE</button>
  </div>
</div>

<script>
const activities=[
  {name:"CRIME SCENARIO",  emoji:"&#128269;",msg:"SCENE OF THE CRIME.\nREAD THE CLUES.\nDON'T BLINK."},
  {name:"UNLOCK BOARD GAME",emoji:"&#128221;",msg:"LOCKED BOX.\nCODE UNKNOWN.\nCRACK IT."},
  {name:"ADMIN STUFF\nWORKDATE",emoji:"&#128203;",msg:"PAPERWORK.\nDUE DATES.\nCLEAR THE BACKLOG."},
  {name:"MOVIE DATE\n(TBD)",        emoji:"&#127916;",msg:"LIGHTS DOWN.\nTITLE UNKNOWN.\nPICK THE FILM."}
];

let shuffled=[];

// dust
(function(){for(let i=0;i<16;i++){const d=document.createElement('div');d.className='dust';d.style.left=Math.random()*100+'%';d.style.animationDuration=(12+Math.random()*14)+'s';d.style.animationDelay=(Math.random()*16)+'s';d.style.width=d.style.height=(Math.random()>.6?'3px':'2px');document.body.appendChild(d);}})();

function typewrite(el,text,speed,cb){
  el.innerHTML='';let i=0;
  const span=document.createElement('span');span.className='typewriter';el.appendChild(span);
  const iv=setInterval(()=>{if(i<text.length){span.textContent+=text[i++];}else{clearInterval(iv);span.classList.remove('typewriter');if(cb)cb();}},speed);
}

const introMsg="Got a hunch,\npartner?\n\nSomething's\nafoot tonight.\n\nPick a file.\nLet's move.";

window.addEventListener('load',()=>{
  typewrite(document.getElementById('introText'),introMsg,46,()=>{
    document.getElementById('continueBtn').style.display='block';
  });
});

function shuffle(a){const r=[...a];for(let i=r.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[r[i],r[j]]=[r[j],r[i]];}return r;}

function goToBoxes(){
  shuffled=shuffle(activities);
  for(let i=0;i<4;i++){
    const b=document.getElementById('box-'+i);
    b.className='gift-box';b.onclick=()=>openBox(i);
    b.innerHTML=`<span class="box-num">FILE 0${i+1}</span><span class="box-icon">${i%2===0?'&#128193;':'&#128194;'}</span><div class="box-label">SEALED<br>DOSSIER<br>&#9608;&#9608;&#9608;</div>`;
  }
  showPage('page-boxes');
}

function flash(){const f=document.getElementById('fl');f.classList.remove('go');void f.offsetWidth;f.classList.add('go');}

function openBox(index){
  const box=document.getElementById('box-'+index);
  if(box.classList.contains('opened'))return;
  box.classList.add('shake');
  setTimeout(()=>{
    box.classList.remove('shake');box.classList.add('opened');box.onclick=null;
    const act=shuffled[index];flash();
    box.innerHTML=`<span class="box-num">FILE 0${index+1}</span><div class="box-reveal-icon">${act.emoji}</div><div class="box-reveal">${act.name.replace(/\n/g,'<br>')}</div>`;
    setTimeout(()=>showResult(act),650);
  },320);
}

function showResult(act){
  document.getElementById('resultEmoji').innerHTML=act.emoji;
  document.getElementById('resultName').innerHTML=act.name.replace(/\n/g,'<br>');
  document.getElementById('resultMsg').innerHTML=act.msg.replace(/\n/g,'<br>');
  document.getElementById('resultScore').textContent='INTEL SCORE: '+(Math.floor(Math.random()*9000)+1000)+' PTS';
  const bf=document.getElementById('barFill');bf.style.animation='none';void bf.offsetWidth;bf.style.animation='';
  showPage('page-result');launchConfetti();
}

function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');window.scrollTo(0,0);
}

function resetGame(){
  showPage('page-intro');
  document.getElementById('continueBtn').style.display='none';
  typewrite(document.getElementById('introText'),introMsg,46,()=>{document.getElementById('continueBtn').style.display='block';});
}

// confetti
const cv=document.getElementById('cc'),ctx=cv.getContext('2d');
let pp=[],aid;
const cols=['#d4a820','#8b1a1a','#c8c090','#3a6a3a','#c0b870','#a07030','#e8d080'];
function launchConfetti(){
  cv.width=window.innerWidth;cv.height=window.innerHeight;pp=[];
  for(let i=0;i<50;i++)pp.push({x:Math.random()*cv.width,y:-10,w:5+Math.random()*9,h:3+Math.random()*7,color:cols[Math.floor(Math.random()*cols.length)],vx:(Math.random()-.5)*5,vy:2+Math.random()*4,rot:Math.random()*360,rv:(Math.random()-.5)*6});
  cancelAnimationFrame(aid);draw();
  setTimeout(()=>{cancelAnimationFrame(aid);ctx.clearRect(0,0,cv.width,cv.height);},3500);
}
function draw(){
  ctx.clearRect(0,0,cv.width,cv.height);let alive=false;
  pp.forEach(p=>{if(p.y>cv.height+20)return;alive=true;p.x+=p.vx;p.y+=p.vy;p.vy+=0.1;p.rot+=p.rv;ctx.save();ctx.globalAlpha=0.8;ctx.translate(Math.round(p.x),Math.round(p.y));ctx.rotate(p.rot*Math.PI/180);ctx.fillStyle=p.color;ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h);ctx.restore();});
  ctx.globalAlpha=1;if(alive)aid=requestAnimationFrame(draw);
}
</script>
</body>
</html>
