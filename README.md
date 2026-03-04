<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Blind Box Restaurant Picker</title>
  <style>
    :root{
      --bg1:#fff0f7;
      --bg2:#ffe3f1;
      --pink:#ff4fa3;
      --pink2:#ff86c6;
      --hot:#ff2b8a;
      --ink:#4a2a3a;
      --card:#ffffffcc;
      --shadow: 0 14px 30px rgba(255, 79, 163, .18);
      --shadow2: 0 10px 20px rgba(74, 42, 58, .10);
      --radius: 22px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      color:var(--ink);
      background: radial-gradient(1200px 700px at 20% 0%, var(--bg2), transparent 60%),
                  radial-gradient(900px 600px at 90% 30%, #ffe9f6, transparent 55%),
                  linear-gradient(180deg, var(--bg1), #ffffff);
      min-height:100dvh;
      overflow-x:hidden;
    }

    .blob{
      position:fixed;
      width:220px; height:220px;
      background: radial-gradient(circle at 30% 30%, #ffd2ea, #ff9bd1);
      opacity:.35;
      border-radius: 60% 40% 55% 45% / 50% 55% 45% 50%;
      animation: float 10s ease-in-out infinite;
      z-index:-1;
    }
    .blob.b1{left:-70px; top:80px; animation-duration: 12s;}
    .blob.b2{right:-90px; top:240px; width:260px; height:260px; opacity:.25; animation-duration: 14s;}
    .blob.b3{left:30px; bottom:-120px; width:300px; height:300px; opacity:.18; animation-duration: 16s;}
    @keyframes float{
      0%,100%{ transform: translate(0,0) rotate(0deg);}
      50%{ transform: translate(16px,-18px) rotate(6deg);}
    }

    .wrap{ max-width: 430px; margin: 0 auto; padding: 18px 16px 26px; }

    .topbar{ display:flex; align-items:center; justify-content:space-between; margin-top: 6px; }
    .chip{
      display:inline-flex; align-items:center; gap:8px;
      padding: 10px 12px;
      border-radius: 999px;
      background: #ffffffaa;
      box-shadow: var(--shadow2);
      border: 1px solid #ffd2ea;
      font-weight: 800;
      letter-spacing:.2px;
      font-size: 13px;
    }
    .dot{
      width:10px; height:10px; border-radius:999px;
      background: var(--pink);
      box-shadow: 0 0 0 4px rgba(255,79,163,.15);
    }

    .card{
      background: var(--card);
      border: 1px solid #ffd2ea;
      border-radius: var(--radius);
      padding: 16px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
    }

    .title{ font-size: 22px; line-height: 1.15; margin: 0 0 10px; letter-spacing: .2px; }
    .sub{ margin:0; opacity:.86; line-height:1.35; font-size: 14px; }

    .btn{
      width:100%;
      border:none;
      padding: 14px 16px;
      border-radius: 16px;
      font-weight: 900;
      font-size: 16px;
      color: white;
      background: linear-gradient(135deg, var(--pink), var(--hot));
      box-shadow: 0 14px 28px rgba(255,43,138,.25);
      cursor:pointer;
      transform: translateY(0);
      transition: transform .08s ease, filter .12s ease;
    }
    .btn:active{ transform: translateY(2px); filter: brightness(.98); }

    .btn.secondary{ background: linear-gradient(135deg, #ff9bd1, #ff65b2); }
    .btn.ghost{
      background: #fff;
      color: var(--hot);
      border: 2px solid #ffd2ea;
      box-shadow: var(--shadow2);
    }

    .page{ display:none; }
    .page.active{ display:block; }

    /* ===== Cute Cat Nurse Mascot (CSS-only, original) ===== */
    .mascot{ margin: 12px auto 16px; width: 200px; height: 200px; position: relative; }
    .hat{
      position:absolute;
      left: 52px; top: 0px;
      width: 96px; height: 62px;
      background: #fff;
      border-radius: 18px 18px 22px 22px;
      border: 2px solid #ffd2ea;
      box-shadow: var(--shadow2);
      z-index: 3;
    }
    .hat:before{
      content:"";
      position:absolute; left: 14px; right: 14px; bottom:-12px;
      height: 24px;
      background: #fff;
      border-radius: 999px;
      border: 2px solid #ffd2ea;
    }
    .plus{
      position:absolute; left: 50%; top: 18px;
      width: 28px; height: 28px;
      transform: translateX(-50%);
      border-radius: 10px;
      background: #ffe3f1;
      border: 2px solid #ffd2ea;
      display:grid; place-items:center;
    }
    .plus i{
      display:block;
      width: 16px; height: 4px;
      background: var(--pink);
      border-radius: 999px;
      position:relative;
    }
    .plus i:after{
      content:"";
      position:absolute; left: 6px; top:-6px;
      width: 4px; height: 16px;
      background: var(--pink);
      border-radius: 999px;
    }

    .head{
      position:absolute;
      left: 24px; top: 36px;
      width: 152px; height: 148px;
      background: linear-gradient(180deg, #ffd4eb, #ffb7dc);
      border-radius: 48% 52% 52% 48% / 55% 55% 45% 45%;
      border: 2px solid #ffb0d8;
      box-shadow: 0 12px 24px rgba(255,79,163,.18);
      z-index: 2;
    }
    .ear{
      position:absolute;
      width: 46px; height: 46px;
      background: linear-gradient(180deg, #ffd4eb, #ffb7dc);
      border: 2px solid #ffb0d8;
      border-radius: 10px 46px 10px 46px;
      transform: rotate(10deg);
      z-index: 1;
    }
    .ear.l{ left: 22px; top: 40px; transform: rotate(-18deg); }
    .ear.r{ right: 22px; top: 40px; transform: rotate(18deg) scaleX(-1); }
    .ear:after{
      content:"";
      position:absolute; inset: 10px 12px 10px 12px;
      background: rgba(255,79,163,.22);
      border-radius: 10px 46px 10px 46px;
      filter: blur(.2px);
    }

    .eye{
      position:absolute;
      top: 72px;
      width: 18px; height: 18px;
      background: #3b2431;
      border-radius: 999px;
      box-shadow: inset 0 -3px 0 rgba(255,255,255,.18);
    }
    .eye.l{ left: 54px; }
    .eye.r{ right: 54px; }

    .cheek{
      position:absolute; top: 94px;
      width: 24px; height: 14px;
      background: rgba(255,79,163,.25);
      border-radius: 999px;
    }
    .cheek.l{ left: 32px; }
    .cheek.r{ right: 32px; }

    .nose{
      position:absolute; left:50%; top: 92px;
      width: 14px; height: 10px;
      transform: translateX(-50%);
      background: rgba(59,36,49,.95);
      border-radius: 8px 8px 10px 10px;
    }
    .mouth{
      position:absolute; left:50%; top: 104px;
      width: 40px; height: 22px;
      transform: translateX(-50%);
      border-bottom: 4px solid rgba(59,36,49,.9);
      border-radius: 0 0 40px 40px;
      opacity:.9;
    }
    .whisker{
      position:absolute; top: 104px;
      width: 34px; height: 2px;
      background: rgba(59,36,49,.35);
      border-radius: 999px;
    }
    .whisker.l1{ left: 12px; transform: rotate(8deg); }
    .whisker.l2{ left: 12px; top: 112px; transform: rotate(-8deg); }
    .whisker.r1{ right: 12px; transform: rotate(-8deg); }
    .whisker.r2{ right: 12px; top: 112px; transform: rotate(8deg); }

    .mask{
      position:absolute; left:50%; top: 86px;
      width: 112px; height: 58px;
      transform: translateX(-50%);
      background: rgba(255,255,255,.82);
      border: 2px solid #ffd2ea;
      border-radius: 18px;
      box-shadow: var(--shadow2);
      display:flex; align-items:center; justify-content:center;
      gap:8px;
      z-index: 3;
    }
    .mask span{ width: 10px; height: 10px; border-radius: 999px; background: rgba(255,79,163,.35); }
    .mask .strap{
      position:absolute;
      top: 20px;
      width: 36px; height: 10px;
      background: rgba(255,255,255,.8);
      border: 2px solid #ffd2ea;
      border-radius: 999px;
    }
    .mask .strap.left{ left: -22px; }
    .mask .strap.right{ right: -22px; }

    .grid{
      display:grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 14px;
      margin-top: 14px;
    }
    .box{
      position:relative;
      border-radius: 20px;
      padding: 14px 12px 12px;
      background: #fff;
      border: 2px solid #ffd2ea;
      box-shadow: var(--shadow2);
      min-height: 150px;
      cursor:pointer;
      user-select:none;
      overflow:hidden;
      transition: transform .12s ease, box-shadow .12s ease;
    }
    .box:active{ transform: scale(.99); }
    .box.locked{ cursor: default; opacity: .75; }
    .box.revealed{
      border-color: rgba(255,79,163,.45);
      box-shadow: 0 16px 34px rgba(255,79,163,.22);
    }
    .box .ribbon{
      position:absolute;
      left:-30px; top: 18px;
      width: 160px; height: 26px;
      background: linear-gradient(135deg, #ff8cc7, #ff3f9b);
      transform: rotate(-14deg);
      border-radius: 999px;
      opacity:.95;
    }
    .box .tag{
      position:absolute;
      right: 10px; top: 10px;
      padding: 6px 10px;
      border-radius: 999px;
      font-weight: 900;
      font-size: 12px;
      color: #fff;
      background: rgba(255,79,163,.9);
      box-shadow: 0 10px 18px rgba(255,79,163,.22);
    }
    .present{
      width: 88px; height: 78px;
      margin: 26px auto 10px;
      position: relative;
    }
    .present .p1{
      position:absolute; inset: 14px 6px 0 6px;
      background: linear-gradient(180deg, #ffd2ea, #ff94c9);
      border-radius: 16px;
      border: 2px solid #ffb0d8;
      box-shadow: 0 10px 18px rgba(255,79,163,.18);
    }
    .present .p2{
      position:absolute; left: 50%; top: 16px;
      width: 14px; height: 62px;
      transform: translateX(-50%);
      background: linear-gradient(180deg, #ff4fa3, #ff2b8a);
      border-radius: 999px;
    }
    .present .bow{
      position:absolute; left:50%; top: 0px;
      width: 64px; height: 34px;
      transform: translateX(-50%);
      display:flex; gap:8px; justify-content:center;
    }
    .present .bow:before, .present .bow:after{
      content:"";
      width: 30px; height: 24px;
      background: linear-gradient(180deg, #ff8cc7, #ff3f9b);
      border-radius: 18px 18px 18px 6px;
      border: 2px solid #ff5fb0;
      transform: rotate(10deg);
    }
    .present .bow:after{
      border-radius: 18px 18px 6px 18px;
      transform: rotate(-10deg);
    }

    .hint{ font-size: 13px; opacity:.82; margin: 8px 0 0; text-align:center; }
    .revealText{ margin: 10px 0 2px; text-align:center; font-weight: 1000; font-size: 16px; letter-spacing:.2px; }
    .muted{ opacity:.72; font-size: 12px; text-align:center; margin:0; }

    .overlay{
      position:fixed; inset:0;
      background: rgba(34, 12, 22, .35);
      display:none;
      align-items:flex-end;
      justify-content:center;
      padding: 14px 14px 18px;
      z-index: 50;
    }
    .overlay.show{ display:flex; }
    .sheet{
      width:min(430px, 100%);
      background: #fff;
      border-radius: 24px;
      border: 2px solid #ffd2ea;
      box-shadow: 0 30px 70px rgba(34,12,22,.25);
      overflow:hidden;
      transform: translateY(8px);
      animation: up .18s ease-out forwards;
    }
    @keyframes up{ to{ transform: translateY(0); } }
    .sheetHeader{
      padding: 14px 16px;
      background: linear-gradient(135deg, #ffe3f1, #fff);
      border-bottom: 1px solid #ffe3f1;
      display:flex; align-items:center; justify-content:space-between;
      gap: 12px;
    }
    .pill{
      display:inline-flex; align-items:center; gap:8px;
      padding: 8px 12px;
      border-radius: 999px;
      background: #fff;
      border: 2px solid #ffd2ea;
      font-weight: 900;
      color: var(--hot);
    }
    .sheetBody{ padding: 14px 16px 16px; }
    .bigPick{ font-size: 22px; font-weight: 1000; margin: 2px 0 6px; letter-spacing: .2px; }
    .smallPick{ margin:0; opacity:.82; }
    .sheetBtns{ display:flex; gap: 10px; padding: 0 16px 16px; }

    canvas#confetti{ position:fixed; inset:0; pointer-events:none; z-index: 60; }

    footer{ margin-top: 14px; text-align:center; font-size: 12px; opacity:.7; }
  </style>
</head>
<body>
  <div class="blob b1"></div>
  <div class="blob b2"></div>
  <div class="blob b3"></div>

  <canvas id="confetti"></canvas>

  <div class="wrap">
    <!-- INTRO PAGE -->
    <section id="pageIntro" class="page active">
      <div class="topbar">
        <div class="chip"><span class="dot"></span> Pink Nurse Cat Mode</div>
        <div class="chip">🐾🎁</div>
      </div>

      <div class="mascot" aria-hidden="true">
        <div class="ear l"></div>
        <div class="ear r"></div>

        <div class="hat"><div class="plus"><i></i></div></div>

        <div class="head">
          <div class="eye l"></div>
          <div class="eye r"></div>
          <div class="cheek l"></div>
          <div class="cheek r"></div>
          <div class="nose"></div>
          <div class="mouth" style="opacity:.35"></div>

          <div class="whisker l1"></div>
          <div class="whisker l2"></div>
          <div class="whisker r1"></div>
          <div class="whisker r2"></div>

          <div class="mask">
            <div class="strap left"></div>
            <div class="strap right"></div>
            <span></span><span></span><span></span>
          </div>
        </div>
      </div>

      <div class="card">
        <h1 class="title">Hello, patient Dương — tap Continue to pick a restaurant</h1>
        <p class="sub">
          Your nurse cat brings 4 mystery gift boxes. Tap one to reveal your meal spot — no take-backs 😼🩷
        </p>
        <div style="height:14px"></div>
        <button id="btnContinue" class="btn">Continue</button>
        <div style="height:10px"></div>
        <button id="btnDemo" class="btn ghost" type="button">Little wiggle</button>
      </div>

      <footer>Tip: Open on mobile for the cutest layout ✨</footer>
    </section>

    <!-- BOX PAGE -->
    <section id="pageBoxes" class="page">
      <div class="topbar">
        <div class="chip"><span class="dot"></span> Pick 1 mystery box</div>
        <button id="btnResetTop" class="chip" style="border:none; cursor:pointer;">🔄 Reset</button>
      </div>

      <div class="card">
        <h2 class="title" style="margin-bottom:8px;">4 Blind Boxes</h2>
        <p class="sub">Tap <b>one</b> box to lock in today’s restaurant.</p>

        <div class="grid" id="grid"></div>

        <p class="hint" id="hint">Pick any box 👇</p>
      </div>

      <footer>Built with extra pink energy 🩷</footer>
    </section>
  </div>

  <!-- RESULT SHEET -->
  <div id="overlay" class="overlay" role="dialog" aria-modal="true" aria-label="Result">
    <div class="sheet">
      <div class="sheetHeader">
        <div class="pill">✅ Result</div>
        <button id="btnClose" class="chip" style="border:none; cursor:pointer;">✕</button>
      </div>
      <div class="sheetBody">
        <div class="bigPick" id="pickedName">—</div>
        <p class="smallPick" id="pickedMsg">Patient Dương, let’s go eat! 🍽️</p>
      </div>
      <div class="sheetBtns">
        <button id="btnAgain" class="btn secondary">Play again</button>
        <button id="btnOk" class="btn">OK, let’s go</button>
      </div>
    </div>
  </div>

  <script>
    const restaurants = ["Ottugi", "Chosim", "Lẩu Wulao", "Sumo"];

    const pageIntro = document.getElementById("pageIntro");
    const pageBoxes = document.getElementById("pageBoxes");
    const btnContinue = document.getElementById("btnContinue");
    const btnResetTop = document.getElementById("btnResetTop");
    const btnDemo = document.getElementById("btnDemo");

    const grid = document.getElementById("grid");
    const hint = document.getElementById("hint");

    const overlay = document.getElementById("overlay");
    const pickedName = document.getElementById("pickedName");
    const pickedMsg = document.getElementById("pickedMsg");
    const btnClose = document.getElementById("btnClose");
    const btnAgain = document.getElementById("btnAgain");
    const btnOk = document.getElementById("btnOk");

    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    let confettiTimer = null;

    let shuffled = [];
    let revealed = false;

    function shuffle(arr){
      const a = arr.slice();
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }

    function showPage(which){
      pageIntro.classList.remove("active");
      pageBoxes.classList.remove("active");
      which.classList.add("active");
      window.scrollTo({top:0, behavior:"smooth"});
    }

    function buildBoxes(){
      grid.innerHTML = "";
      shuffled = shuffle(restaurants);
      revealed = false;
      hint.textContent = "Pick any box 👇";

      shuffled.forEach((name, idx) => {
        const box = document.createElement("div");
        box.className = "box";
        box.setAttribute("role", "button");
        box.setAttribute("tabindex", "0");
        box.setAttribute("aria-label", "Mystery box " + (idx+1));

        box.innerHTML = `
          <div class="ribbon"></div>
          <div class="tag">BOX ${idx+1}</div>
          <div class="present" aria-hidden="true">
            <div class="bow"></div>
            <div class="p1"></div>
            <div class="p2"></div>
          </div>
          <div class="revealText">Mystery</div>
          <p class="muted">Tap to open</p>
        `;

        const open = () => {
          if (revealed) return;
          revealed = true;

          [...grid.children].forEach(el => el.classList.add("locked"));
          box.classList.remove("locked");
          box.classList.add("revealed");

          box.querySelector(".revealText").textContent = name;
          box.querySelector(".muted").textContent = "Opened ✅";

          hint.textContent = "Locked in! 🎉";

          openResult(name);
          burstConfetti();
        };

        box.addEventListener("click", open);
        box.addEventListener("keydown", (e) => {
          if (e.key === "Enter" || e.key === " ") {
            e.preventDefault();
            open();
          }
        });

        grid.appendChild(box);
      });
    }

    function openResult(name){
      pickedName.textContent = name;
      pickedMsg.textContent = `Patient Dương — today we’re going to "${name}" 🩷`;
      overlay.classList.add("show");
    }

    function closeResult(){ overlay.classList.remove("show"); }

    function resetAll(){
      closeResult();
      buildBoxes();
    }

    function resizeCanvas(){
      canvas.width = window.innerWidth * devicePixelRatio;
      canvas.height = window.innerHeight * devicePixelRatio;
      canvas.style.width = window.innerWidth + "px";
      canvas.style.height = window.innerHeight + "px";
      ctx.setTransform(devicePixelRatio, 0, 0, devicePixelRatio, 0, 0);
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    function burstConfetti(){
      const pieces = [];
      const W = window.innerWidth, H = window.innerHeight;
      const count = 140;

      for(let i=0;i<count;i++){
        pieces.push({
          x: W/2 + (Math.random()*120-60),
          y: H*0.22 + (Math.random()*60-30),
          vx: (Math.random()*6-3),
          vy: (Math.random()*-6-2),
          g: 0.18 + Math.random()*0.10,
          r: 2 + Math.random()*4,
          a: 1,
          rot: Math.random()*Math.PI,
          vr: (Math.random()*0.2-0.1),
          c: ["#ff4fa3","#ff86c6","#ffd2ea","#ff2b8a","#ff9bd1"][Math.floor(Math.random()*5)]
        });
      }

      let t = 0;
      if (confettiTimer) cancelAnimationFrame(confettiTimer);

      const tick = () => {
        t++;
        ctx.clearRect(0,0,window.innerWidth, window.innerHeight);

        for(const p of pieces){
          p.x += p.vx;
          p.y += p.vy;
          p.vy += p.g;
          p.rot += p.vr;
          p.a *= 0.992;

          ctx.save();
          ctx.globalAlpha = Math.max(0, Math.min(1, p.a));
          ctx.translate(p.x, p.y);
          ctx.rotate(p.rot);
          ctx.fillStyle = p.c;
          ctx.fillRect(-p.r, -p.r, p.r*2.2, p.r*1.6);
          ctx.restore();
        }

        if (t < 170){
          confettiTimer = requestAnimationFrame(tick);
        } else {
          ctx.clearRect(0,0,window.innerWidth, window.innerHeight);
        }
      };
      tick();
    }

    btnContinue.addEventListener("click", () => {
      showPage(pageBoxes);
      buildBoxes();
    });

    btnResetTop.addEventListener("click", resetAll);

    document.getElementById("btnClose").addEventListener("click", closeResult);
    document.getElementById("btnOk").addEventListener("click", closeResult);
    document.getElementById("btnAgain").addEventListener("click", resetAll);

    overlay.addEventListener("click", (e) => { if (e.target === overlay) closeResult(); });

    btnDemo.addEventListener("click", () => {
      const card = pageIntro.querySelector(".card");
      card.animate([
        { transform: "translateX(0)" },
        { transform: "translateX(-6px)" },
        { transform: "translateX(6px)" },
        { transform: "translateX(-4px)" },
        { transform: "translateX(4px)" },
        { transform: "translateX(0)" },
      ], { duration: 420, easing: "ease-out" });
    });
  </script>
</body>
</html># blindbox
