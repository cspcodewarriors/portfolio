---
permalink: /network/4
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 4 – Slice at the MTU</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#7c3aed;color:#fff;border-color:#a78bfa;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#7c3aed22;border:1px solid #7c3aed;border-radius:20px;padding:3px 12px;font-size:11px;color:#a78bfa;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:12px;}
  #game-wrap{max-width:580px;margin:0 auto;}
  #bar-container{position:relative;margin-top:48px;margin-bottom:24px;}
  #bar{display:flex;height:52px;border-radius:8px;overflow:hidden;border:2px solid #374151;}
  .seg{display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:#111;}
  #knife-wrap{position:absolute;top:-36px;pointer-events:none;transition:none;}
  .knife-emoji{font-size:28px;transform:rotate(180deg);display:block;text-align:center;}
  .knife-line{width:3px;height:88px;margin:0 auto;border-radius:2px;}
  .knife-pos{position:absolute;bottom:-22px;font-size:10px;color:#9ca3af;text-align:center;width:44px;left:-20px;}
  .cut-mark{position:absolute;top:-8px;width:3px;height:72px;background:#f87171;border-radius:2px;z-index:3;}
  #pause-msg{background:#1e1b4b;border:1px solid #7c3aed;border-radius:8px;padding:10px;margin:8px 0;font-size:12px;color:#c4b5fd;text-align:center;min-height:38px;}
  #chop-btn{display:block;margin:16px auto 0;background:#3b82f6;color:#fff;border:none;border-radius:8px;padding:10px 32px;cursor:pointer;font-weight:700;font-size:16px;font-family:'Share Tech Mono',monospace;}
  #chop-btn:disabled{opacity:.5;cursor:default;}
  #segments-title{color:#9ca3af;font-size:12px;margin:16px 0 6px;}
  #segments{display:flex;gap:8px;flex-wrap:wrap;}
  .seg-card{background:#1f2937;border-radius:6px;padding:6px 10px;font-size:10px;}
  .seg-card .sc-title{font-weight:700;margin-bottom:2px;}
  .seg-card .sc-row{color:#94a3b8;}
  .seg-card .sc-total{color:#fff;font-weight:700;border-top:1px solid #374151;margin-top:4px;padding-top:4px;}
  .facts{background:#0f172a;border:1px solid #1e3a5f;border-radius:8px;padding:10px;margin-top:16px;}
  .facts summary{cursor:pointer;color:#60a5fa;font-weight:700;font-size:13px;}
  .facts ul{margin:8px 0 0;padding-left:18px;}
  .facts li{color:#94a3b8;font-size:12px;margin-bottom:4px;}
  .win{background:linear-gradient(135deg,#052e16,#14532d);border:2px solid #4ade80;border-radius:12px;padding:16px;margin-top:16px;text-align:center;display:none;}
  .win.show{display:block;}
  .win h3{color:#4ade80;font-size:16px;margin:8px 0;}
  .btn{background:#4ade80;color:#052e16;border:none;border-radius:8px;padding:10px 28px;cursor:pointer;font-weight:700;font-size:14px;font-family:'Share Tech Mono',monospace;}
</style>
</head>
<body>
<div class="header">
  <span class="logo">📬 Network Escape Room</span>
  <div class="nav-links">
    <a href="/portfolio/network/1">L1</a><a href="/portfolio/network/2">L2</a><a href="/portfolio/network/3">L3</a>
    <a href="/portfolio/network/4" class="active">L4</a>
    <a href="/portfolio/network/5">L5</a><a href="/portfolio/network/6">L6</a><a href="/portfolio/network/7">L7</a>
  </div>
  <a href="/portfolio/network/home" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 4 / TCP-IP: Transport</div>
    <h2>🔪 Level 4 — Slice at the MTU!</h2>
    <p class="flavor">Press <b>SPACE</b> or CHOP when the knife hits a color boundary (= 1460B). MTU = 1500B, TCP payload = 1460B.</p>
    <div id="game-wrap">
      <div id="bar-container">
        <div id="bar">
          <div class="seg" id="seg0" style="flex:1460;background:#60a5fa;">1460B</div>
          <div class="seg" id="seg1" style="flex:1460;background:#a78bfa;">1460B</div>
          <div class="seg" id="seg2" style="flex:1420;background:#4ade80;">1420B</div>
        </div>
        <div id="knife-wrap" style="left:0px">
          <span class="knife-emoji">🔪</span>
          <div class="knife-line" id="knife-line" style="background:#fff;"></div>
          <div class="knife-pos" id="knife-pos">0B</div>
        </div>
      </div>
      <div id="pause-msg"></div>
      <button id="chop-btn" onclick="chop()">✂️ CHOP! (or Space)</button>
      <div id="segments-title" style="display:none">Segments produced:</div>
      <div id="segments"></div>
    </div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>MTU = 1500B max. TCP payload = 1500 - 20 (IP) - 20 (TCP) = 1460B.</li>
        <li>TCP sequence numbers let the receiver reassemble in order.</li>
        <li>Nginx on AWS EC2 reassembles all segments into the full HTTP request.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3 id="win-msg">Sliced! TCP segmentation done!</h3>
      <a href="/portfolio/network/5"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const TOTAL=4340, BAR_W=560;
const CUT_POINTS=[1460,2920];
const SEGS=[
  {start:0,   end:1460,color:"#60a5fa"},
  {start:1460,end:2920,color:"#a78bfa"},
  {start:2920,end:4340,color:"#4ade80"},
];

let kx=0, dir=1, paused=false, done=false;
const cuts=[];
let raf;

const barContainer=document.getElementById('bar-container');
const knifeWrap=document.getElementById('knife-wrap');
const knifeLine=document.getElementById('knife-line');
const knifePos=document.getElementById('knife-pos');
const pauseMsg=document.getElementById('pause-msg');
const chopBtn=document.getElementById('chop-btn');

function gameLoop(){
  if(!paused){
    kx+=dir*2.2;
    if(kx>=BAR_W){kx=BAR_W;dir=-1;}
    if(kx<=0){kx=0;dir=1;}
    knifeWrap.style.left=kx+'px';
    knifeLine.style.background=paused?'#4ade80':'#fff';
    knifePos.textContent=Math.round((kx/BAR_W)*TOTAL)+'B';
  }
  if(!done) raf=requestAnimationFrame(gameLoop);
}

function chop(){
  if(paused||done) return;
  let closest=null, minD=Infinity;
  CUT_POINTS.forEach(cp=>{
    if(cuts.includes(cp)) return;
    const cpX=(cp/TOTAL)*BAR_W;
    const d=Math.abs(kx-cpX);
    if(d<minD){minD=d;closest=cp;}
  });
  if(closest!==null && minD<50){
    paused=true; chopBtn.disabled=true;
    cuts.push(closest);
    addCutMark(closest);
    const payload=closest<=1460?closest:closest-1460;
    pauseMsg.textContent=`✂️ Cut at ${closest}B! Payload: ${payload}B + 20B TCP + 20B IP headers.`;
    knifeLine.style.background='#4ade80';
    renderSegments();
    setTimeout(()=>{
      paused=false; chopBtn.disabled=false; pauseMsg.textContent='';
      knifeLine.style.background='#fff';
      if(cuts.length===CUT_POINTS.length){
        done=true; chopBtn.disabled=true;
        document.getElementById('win-msg').textContent=`Sliced into ${cuts.length+1} segments! TCP segmentation done!`;
        document.getElementById('win-banner').classList.add('show');
        cancelAnimationFrame(raf);
      }
    },2400);
  } else {
    pauseMsg.textContent='⚠️ Not a boundary! Look for the color change.';
    knifeWrap.style.transform='translateX(-6px)';
    setTimeout(()=>{pauseMsg.textContent='';knifeWrap.style.transform='';},1000);
  }
}

function addCutMark(cp){
  const cm=document.createElement('div');
  cm.className='cut-mark';
  cm.style.left=(cp/TOTAL)*BAR_W+'px';
  barContainer.appendChild(cm);
}

function renderSegments(){
  document.getElementById('segments-title').style.display='block';
  const segsEl=document.getElementById('segments');
  segsEl.innerHTML='';
  const points=[0,...cuts,TOTAL];
  points.forEach((start,i)=>{
    if(i>=points.length-1) return;
    const end=points[i+1];
    const payload=end-start;
    const sg=SEGS.find(s=>start<s.end&&start>=s.start)||(SEGS[SEGS.length-1]);
    const div=document.createElement('div');
    div.className='seg-card';
    div.style.border=`2px solid ${sg.color}`;
    div.innerHTML=`<div class="sc-title" style="color:${sg.color}">Seg #${i+1}</div><div class="sc-row">Payload: ${payload}B</div><div class="sc-row" style="color:#60a5fa">+TCP+IP: 40B</div><div class="sc-total">= ${payload+40}B</div>`;
    segsEl.appendChild(div);
  });
}

document.addEventListener('keydown',e=>{
  if(e.code==='Space'){e.preventDefault();chop();}
});

requestAnimationFrame(gameLoop);
</script>
</body>
</html>