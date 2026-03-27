---
permalink: /network/3
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 3 – Route the Packets</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#3b82f6;color:#fff;border-color:#60a5fa;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#2563eb22;border:1px solid #2563eb;border-radius:20px;padding:3px 12px;font-size:11px;color:#60a5fa;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:6px;}
  #msg{font-size:12px;color:#9ca3af;margin-bottom:6px;min-height:18px;}
  #msg.wrong{color:#f87171;}
  #canvas-wrap{position:relative;width:100%;max-width:640px;height:380px;margin:0 auto;border-radius:12px;border:1px solid #1f2937;overflow:hidden;}
  canvas{display:block;width:100%;height:100%;}
  .status-row{margin-top:8px;display:flex;gap:8px;flex-wrap:wrap;}
  .status-item{font-size:11px;color:#6b7280;}
  .status-item.done{color:#4ade80;}
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
    <a href="/portfolio/network/1">L1</a><a href="/portfolio/network/2">L2</a>
    <a href="/portfolio/network/3" class="active">L3</a>
    <a href="/portfolio/network/4">L4</a><a href="/portfolio/network/5">L5</a><a href="/portfolio/network/6">L6</a><a href="/portfolio/network/7">L7</a>
  </div>
  <a href="/portfolio/network/home" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 3 / TCP-IP: Network (Internet)</div>
    <h2>🏬 Level 3 — Route the Packets!</h2>
    <p class="flavor"><b>WASD</b> to walk · <b>E</b> to pick up / throw to nearest bin</p>
    <div id="msg">WASD to walk • E to pick up/throw</div>
    <div id="canvas-wrap"><canvas id="gc" width="640" height="380"></canvas></div>
    <div class="status-row" id="status-row"></div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>IP routing decides which network each packet belongs to.</li>
        <li>3.233.212.71 is the real AWS EC2 IP for flask.opencodingsociety.com.</li>
        <li>Private IPs (10.x, 192.168.x) never leave the local network.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3>All packets routed!</h3>
      <a href="/portfolio/network/4"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const W=640,H=380,SPEED=3;
const canvas=document.getElementById('gc');
const ctx=canvas.getContext('2d');

const bins=[
  {id:"web",x:520,y:60, w:100,h:50,label:"🌐 Public Web", color:"#3b82f6",accepts:["github","cdn"]},
  {id:"aws",x:520,y:150,w:100,h:50,label:"☁️ AWS Cloud",  color:"#f59e0b",accepts:["ec2"]},
  {id:"dns",x:520,y:240,w:100,h:50,label:"🔍 DNS",         color:"#a78bfa",accepts:["dns"]},
  {id:"loc",x:520,y:320,w:100,h:50,label:"🏠 Local",       color:"#4ade80",accepts:["isp","db"]},
];
const pkgDefs=[
  {id:"github",label:"185.199.x.x",sub:"GitHub Pages",correct:"web"},
  {id:"ec2",   label:"3.233.212.71",sub:"AWS EC2",     correct:"aws"},
  {id:"dns",   label:"8.8.8.8",     sub:"DNS Server",  correct:"dns"},
  {id:"isp",   label:"192.168.1.1", sub:"Home Router", correct:"loc"},
  {id:"cdn",   label:"151.101.x.x", sub:"CDN Node",    correct:"web"},
  {id:"db",    label:"10.0.0.5",    sub:"SQL DB",       correct:"loc"},
];
const packages=pkgDefs.map((p,i)=>({...p,x:30+(i%2)*60,y:40+i*50}));

let player={x:80,y:200};
let held=null;
let thrown=null; // {id,fromX,fromY,tx,ty,cx,cy,progress}
let delivered=[];
let wrongFlash=false;
const keys={};

function setMsg(t,bad){
  const el=document.getElementById('msg');
  el.textContent=t;
  el.className=bad?'wrong':'';
}

function updateStatus(){
  const row=document.getElementById('status-row');
  row.innerHTML=pkgDefs.map(p=>`<div class="status-item ${delivered.includes(p.id)?'done':''}">${delivered.includes(p.id)?'✅':'⬜'} ${p.sub}</div>`).join('');
}

document.addEventListener('keydown',e=>{
  keys[e.key.toLowerCase()]=true;
  if(e.key==='e'||e.key==='E'){
    if(held){
      // throw to nearest bin
      let closest=null,minD=Infinity;
      bins.forEach(b=>{
        const d=Math.hypot(player.x-(b.x+b.w/2),player.y-(b.y+b.h/2));
        if(d<minD){minD=d;closest=b;}
      });
      if(closest){
        thrown={id:held,fromX:player.x,fromY:player.y,tx:closest.x+closest.w/2,ty:closest.y+closest.h/2,cx:player.x,cy:player.y,progress:0,binId:closest.id};
        held=null;
      }
    } else {
      const near=packages.find(p=>!delivered.includes(p.id)&&p.id!==held&&Math.hypot(p.x-player.x,p.y-player.y)<40);
      if(near){held=near.id;setMsg(`Picked up ${near.sub}! Press E near a bin to throw.`);}
    }
  }
});
document.addEventListener('keyup',e=>{ keys[e.key.toLowerCase()]=false; });

function gameLoop(){
  if(keys['a']||keys['arrowleft']) player.x-=SPEED;
  if(keys['d']||keys['arrowright'])player.x+=SPEED;
  if(keys['w']||keys['arrowup'])   player.y-=SPEED;
  if(keys['s']||keys['arrowdown']) player.y+=SPEED;
  player.x=Math.max(20,Math.min(W-60,player.x));
  player.y=Math.max(20,Math.min(H-20,player.y));

  if(thrown){
    thrown.progress=Math.min(1,thrown.progress+0.04);
    const t=thrown.progress;
    thrown.cx=thrown.fromX+(thrown.tx-thrown.fromX)*t;
    thrown.cy=thrown.fromY+(thrown.ty-thrown.fromY)*t-Math.sin(t*Math.PI)*60;
    if(thrown.progress>=1){
      const pkg=pkgDefs.find(p=>p.id===thrown.id);
      const bin=bins.find(b=>b.id===thrown.binId);
      if(bin.accepts.includes(pkg.id)){
        delivered=[...delivered,thrown.id];
        setMsg(`✅ ${pkg.sub} → ${bin.label}!`);
        updateStatus();
        if(delivered.length===pkgDefs.length){
          setMsg('🎉 All routed!');
          document.getElementById('win-banner').classList.add('show');
        }
      } else {
        setMsg(`❌ Wrong bin for ${pkg.sub}!`,true);
        wrongFlash=true; setTimeout(()=>wrongFlash=false,1000);
      }
      thrown=null;
    }
  }
  draw();
  requestAnimationFrame(gameLoop);
}

function draw(){
  ctx.clearRect(0,0,W,H);
  ctx.fillStyle='#0f172a'; ctx.fillRect(0,0,W,H);

  // Bins
  bins.forEach(b=>{
    ctx.fillStyle=b.color+'22';
    ctx.strokeStyle=b.color;
    ctx.lineWidth=2;
    roundRect(ctx,b.x,b.y,b.w,b.h,8);
    ctx.fill(); ctx.stroke();
    ctx.fillStyle=b.color; ctx.font='bold 10px Share Tech Mono,monospace';
    ctx.textAlign='center';
    ctx.fillText(b.label,b.x+b.w/2,b.y+b.h/2+4);
  });

  // Packages
  packages.forEach(p=>{
    if(delivered.includes(p.id)||p.id===held) return;
    ctx.fillStyle='#1f2937'; ctx.strokeStyle='#4b5563'; ctx.lineWidth=1;
    roundRect(ctx,p.x-24,p.y-20,50,36,6); ctx.fill(); ctx.stroke();
    ctx.fillStyle='#e2e8f0'; ctx.font='14px serif'; ctx.textAlign='center';
    ctx.fillText('📦',p.x,p.y-4);
    ctx.fillStyle='#60a5fa'; ctx.font='8px Share Tech Mono,monospace';
    ctx.fillText(p.label,p.x,p.y+10);
  });

  // Thrown package
  if(thrown){
    ctx.font='20px serif'; ctx.textAlign='center';
    ctx.fillText('📦',thrown.cx,thrown.cy);
  }

  // Player
  ctx.font='28px serif'; ctx.textAlign='center';
  ctx.fillText('🧑‍💼',player.x,player.y+8);
  if(held){
    ctx.font='16px serif';
    ctx.fillText('📦',player.x,player.y-16);
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