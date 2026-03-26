---
permalink: /network/7
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 7 – Neighborhood Delivery</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#065f46;color:#fff;border-color:#34d399;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#065f4622;border:1px solid #065f46;border-radius:20px;padding:3px 12px;font-size:11px;color:#34d399;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:6px;}
  #msg-bar{font-size:12px;background:#1f2937;padding:6px 10px;border-radius:6px;margin-bottom:8px;color:#e2e8f0;min-height:28px;}
  #canvas-wrap{position:relative;width:100%;max-width:680px;height:460px;margin:0 auto;border-radius:12px;border:2px solid #1f2937;overflow:hidden;}
  canvas{display:block;width:100%;height:100%;}
  #toast{display:none;position:absolute;top:12px;left:50%;transform:translateX(-50%);background:#052e16;border:2px solid #4ade80;border-radius:10px;padding:8px 16px;font-size:12px;color:#4ade80;font-weight:700;z-index:20;white-space:nowrap;box-shadow:0 4px 20px #4ade8044;}
  #status-row{margin-top:8px;display:flex;gap:6px;flex-wrap:wrap;}
  .si{font-size:10px;color:#6b7280;}
  .si.done{color:#4ade80;}
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
    <a href="level1.html">L1</a><a href="level2.html">L2</a><a href="level3.html">L3</a>
    <a href="level4.html">L4</a><a href="level5.html">L5</a><a href="level6.html">L6</a>
    <a href="level7.html" class="active">L7</a>
  </div>
  <a href="index.html" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 7 / TCP-IP: Application (HTTP, DNS, HTTPS)</div>
    <h2>🚗 Level 7 — Neighborhood Delivery!</h2>
    <p class="flavor"><b>WASD</b> to drive on roads. <b>E</b> near 📮 to pick up. <b>E</b> near 🏠 to deliver.</p>
    <div id="msg-bar">Drive with WASD! Press E near 📮 to pick up, press E near 🏠 to deliver!</div>
    <div id="canvas-wrap">
      <canvas id="gc" width="680" height="460"></canvas>
      <div id="toast"></div>
    </div>
    <div id="status-row"></div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>DNS resolves flask.opencodingsociety.com → 3.233.212.71 first.</li>
        <li>Nginx :443 (public) proxies to Flask :8587 (private).</li>
        <li>HTTP GET /api/users → SQL SELECT → JSON → HTTPS back to GitHub Pages.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🏆</div>
      <h3>Full HTTP cycle complete! Network Stack mastered!</h3>
      <a href="index.html"><button class="btn">🔄 Play Again</button></a>
    </div>
  </div>
</div>
<script>
const W=680,H=460,SPEED=2.5,CAR_W=28,CAR_H=18;
const canvas=document.getElementById('gc');
const ctx=canvas.getContext('2d');

const roads=[
  {x:0,  y:185,w:W,  h:70},
  {x:0,  y:50, w:W,  h:70},
  {x:0,  y:350,w:W,  h:70},
  {x:90, y:0,  w:70, h:H },
  {x:305,y:0,  w:70, h:H },
  {x:520,y:0,  w:70, h:H },
];

const houses=[
  {id:"dns",  x:190,y:130,label:"🔍 DNS",      sub:"8.8.8.8 :53",       color:"#a78bfa",msg:"DNS resolved flask.opencodingsociety.com → 3.233.212.71!"},
  {id:"nginx",x:400,y:130,label:"⚡ Nginx",    sub:"3.233.212.71 :443",  color:"#f59e0b",msg:"Nginx received HTTPS, proxied to Flask :8587!"},
  {id:"flask",x:400,y:290,label:"🐍 Flask",    sub:"localhost :8587",    color:"#4ade80",msg:"Flask queried SQL → JSON response!"},
  {id:"db",   x:190,y:290,label:"🗄️ SQL DB",  sub:"10.0.0.5 (private)", color:"#60a5fa",msg:"Database returned user records to Flask!"},
  {id:"cdn",  x:610,y:290,label:"🌐 CDN",      sub:"151.101.x.x",        color:"#f87171",msg:"CDN cached the response for next time!"},
  {id:"pages",x:610,y:130,label:"📄 GitHub",   sub:"185.199.x.x",        color:"#e2e8f0",msg:"GitHub Pages served the frontend to the browser!"},
];
const ORDER=["dns","nginx","flask","db","cdn","pages"];
const PO={x:125,y:207};

let car={x:PO.x,y:PO.y};
let dir="right";
let hasPkg=false;
let delivered=[];
let nearPO=false;
let nearHouse=null;
const keys={};

function isOnRoad(x,y){
  return roads.some(r=>x+CAR_W>r.x+4&&x<r.x+r.w-4&&y+CAR_H>r.y+4&&y<r.y+r.h-4);
}
function nextTarget(){ return ORDER[delivered.length]||null; }

function setMsg(t){ document.getElementById('msg-bar').textContent=t; }

function showToast(t){
  const el=document.getElementById('toast');
  el.textContent='✅ '+t; el.style.display='block';
  setTimeout(()=>el.style.display='none',2500);
}

function updateStatus(){
  const row=document.getElementById('status-row');
  row.innerHTML=ORDER.map((id,i)=>{
    const h=houses.find(h=>h.id===id);
    const done=delivered.includes(id);
    return `<div class="si ${done?'done':''}">${done?'✅':'⬜'} ${i+1}. ${h.label.replace(/[🔍⚡🐍🗄️🌐📄]/gu,'').trim()}</div>`;
  }).join('');
}

document.addEventListener('keydown',e=>{
  keys[e.key.toLowerCase()]=true;
  if(e.key==='e'||e.key==='E'){
    if(!hasPkg&&nearPO&&delivered.length<ORDER.length){
      hasPkg=true;
      const tgt=houses.find(h=>h.id===nextTarget());
      setMsg(`📦 Picked up! Drive to ${tgt?.label} (${tgt?.sub}) and press E to deliver.`);
      return;
    }
    if(hasPkg&&nearHouse&&nearHouse.id===nextTarget()){
      delivered.push(nearHouse.id);
      const msg=nearHouse.msg;
      hasPkg=false;
      nearHouse=null;
      showToast(msg);
      updateStatus();
      if(delivered.length>=ORDER.length){
        setMsg('🎉 All packages delivered! HTTP request cycle complete!');
        document.getElementById('win-banner').classList.add('show');
      } else {
        const nxt=nextTarget();
        const nxtH=houses.find(h=>h.id===nxt);
        setMsg(`✅ Delivered! Return to 📮 Post Office for next package → ${nxtH?.label}`);
      }
    }
  }
});
document.addEventListener('keyup',e=>keys[e.key.toLowerCase()]=false);

function gameLoop(){
  let {x,y}=car;
  let nx=x,ny=y,newDir=dir,moved=false;
  if(keys['a']||keys['arrowleft']) {nx-=SPEED;newDir='left'; moved=true;}
  if(keys['d']||keys['arrowright']){nx+=SPEED;newDir='right';moved=true;}
  if(keys['w']||keys['arrowup'])   {ny-=SPEED;newDir='up';   moved=true;}
  if(keys['s']||keys['arrowdown']) {ny+=SPEED;newDir='down'; moved=true;}
  nx=Math.max(0,Math.min(W-CAR_W,nx));
  ny=Math.max(0,Math.min(H-CAR_H,ny));
  if(!isOnRoad(nx,ny)){nx=x;ny=y;}
  car={x:nx,y:ny};
  if(moved) dir=newDir;

  nearPO=Math.hypot(nx-PO.x,ny-PO.y)<55;
  const tgt=nextTarget();
  const tgtH=hasPkg&&tgt?houses.find(h=>h.id===tgt):null;
  nearHouse=tgtH&&Math.hypot(nx-tgtH.x,ny-tgtH.y)<72?tgtH:null;

  draw();
  requestAnimationFrame(gameLoop);
}

function draw(){
  // Grass
  ctx.fillStyle='#166534'; ctx.fillRect(0,0,W,H);
  // Grass tufts
  for(let i=0;i<30;i++){
    ctx.fillStyle='#15803d';
    ctx.globalAlpha=.5;
    ctx.beginPath();
    ctx.ellipse((i*73+11)%W,(i*47+7)%H,3,2,0,0,Math.PI*2);
    ctx.fill();
  }
  ctx.globalAlpha=1;

  // Roads
  roads.forEach(r=>{
    ctx.fillStyle='#374151'; ctx.fillRect(r.x,r.y,r.w,r.h);
  });

  // Road markings
  roads.filter(r=>r.w>r.h).forEach(r=>{
    for(let j=0;j<Math.ceil(r.w/56);j++){
      ctx.fillStyle='#fbbf24'; ctx.globalAlpha=.6;
      ctx.fillRect(r.x+j*56+8,r.y+r.h/2-2,32,4);
    }
  });
  roads.filter(r=>r.h>r.w).forEach(r=>{
    for(let j=0;j<Math.ceil(r.h/56);j++){
      ctx.fillStyle='#fbbf24'; ctx.globalAlpha=.6;
      ctx.fillRect(r.x+r.w/2-2,r.y+j*56+8,4,32);
    }
  });
  ctx.globalAlpha=1;

  // Intersections
  [[90,50],[305,50],[520,50],[90,185],[305,185],[520,185],[90,350],[305,350],[520,350]].forEach(([x,y])=>{
    ctx.fillStyle='#4b5563'; ctx.fillRect(x,y,70,70);
  });

  // Houses
  houses.forEach(h=>{
    const isDone=delivered.includes(h.id);
    const isNear=nearHouse?.id===h.id;
    const isNext=nextTarget()===h.id&&hasPkg;
    ctx.font='32px serif'; ctx.textAlign='center';
    ctx.fillText('🏠',h.x,h.y-10);
    ctx.fillStyle=isDone?'#052e16':'#0f172a';
    roundRect(ctx,h.x-32,h.y,70,36,6);
    ctx.fill();
    ctx.strokeStyle=isDone?'#4ade80':isNear?'#fbbf24':isNext?'#fbbf24':h.color;
    ctx.lineWidth=2; ctx.stroke();
    ctx.fillStyle=isDone?'#4ade80':isNear?'#fbbf24':h.color;
    ctx.font='bold 9px Share Tech Mono,monospace';
    ctx.textAlign='center';
    ctx.fillText((isDone?'✅ ':isNext?'🎯 ':'')+h.label,h.x,h.y+13);
    ctx.fillStyle='#6b7280'; ctx.font='8px Share Tech Mono,monospace';
    ctx.fillText(h.sub,h.x,h.y+25);
    if(isNear){
      ctx.fillStyle='#fbbf24'; ctx.font='bold 9px Share Tech Mono,monospace';
      ctx.fillText('Press E!',h.x,h.y-42);
    }
  });

  // Post Office
  ctx.font='24px serif'; ctx.textAlign='center';
  ctx.fillText('📮',PO.x,PO.y-20);
  ctx.fillStyle='#1f2937';
  roundRect(ctx,PO.x-36,PO.y-14,72,28,6); ctx.fill();
  ctx.strokeStyle='#e2e8f0'; ctx.lineWidth=2; ctx.stroke();
  ctx.fillStyle='#e2e8f0'; ctx.font='bold 9px Share Tech Mono,monospace'; ctx.textAlign='center';
  ctx.fillText('Post Office',PO.x,PO.y+2);
  if(nearPO&&!hasPkg&&delivered.length<ORDER.length){
    ctx.fillStyle='#fbbf24'; ctx.font='bold 9px Share Tech Mono,monospace';
    ctx.fillText('Press E!',PO.x,PO.y-38);
  }

  // Car
  ctx.save();
  ctx.translate(car.x+CAR_W/2,car.y+CAR_H/2);
  if(dir==='left') ctx.scale(-1,1);
  else if(dir==='up') ctx.rotate(-Math.PI/2);
  else if(dir==='down') ctx.rotate(Math.PI/2);
  ctx.font='24px serif'; ctx.textAlign='center';
  ctx.fillText('🚗',0,8);
  ctx.restore();
  if(hasPkg){
    ctx.font='16px serif';
    ctx.fillText('📦',car.x+CAR_W/2,car.y-8);
  }

  // Progress overlay bottom
  const tgt=nextTarget();
  if(tgt){
    const h=houses.find(h=>h.id===tgt);
    ctx.fillStyle='#0f172a88'; ctx.fillRect(0,H-28,W,28);
    ctx.fillStyle='#60a5fa'; ctx.font='10px Share Tech Mono,monospace'; ctx.textAlign='left';
    ctx.fillText(`📍 Next: ${h?.label} (${h?.sub})`,8,H-10);
  }
}

function roundRect(ctx,x,y,w,h,r){
  ctx.beginPath();
  ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y); ctx.arcTo(x+w,y,x+w,y+r,r);
  ctx.lineTo(x+w,y+h-r); ctx.arcTo(x+w,y+h,x+w-r,y+h,r);
  ctx.lineTo(x+r,y+h); ctx.arcTo(x,y+h,x,y+h-r,r);
  ctx.lineTo(x,y+r); ctx.arcTo(x,y,x+r,y,r); ctx.closePath();
}

updateStatus();
requestAnimationFrame(gameLoop);
</script>
</body>
</html>