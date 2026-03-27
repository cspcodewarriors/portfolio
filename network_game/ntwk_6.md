---
permalink: /network/6
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 6 – Wrap with TLS</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#0d9488;color:#fff;border-color:#2dd4bf;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#0d948822;border:1px solid #0d9488;border-radius:20px;padding:3px 12px;font-size:11px;color:#2dd4bf;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:16px;}
  .layout{display:flex;gap:24px;flex-wrap:wrap;justify-content:center;align-items:flex-start;margin-top:16px;}
  .box-side{display:flex;flex-direction:column;align-items:center;}
  #box-preview{position:relative;width:200px;height:220px;}
  .box-shadow{position:absolute;left:24px;bottom:8px;width:168px;height:12px;background:#000;border-radius:50%;opacity:.3;}
  #box-body{position:absolute;left:20px;top:40px;width:160px;height:140px;border-radius:6px;border:3px solid #78350f;background:#92400e;display:flex;align-items:center;justify-content:center;transition:all .5s;}
  #box-body.encrypted{background:#1e3a5f;border-color:#3b82f6;}
  #box-content{text-align:center;font-size:10px;padding:8px;}
  #box-lid{display:none;position:absolute;left:14px;top:28px;width:172px;height:20px;background:#a16207;border-radius:4px 4px 0 0;border:2px solid #78350f;z-index:6;}
  #box-wrap-layer{display:none;position:absolute;left:16px;top:36px;width:168px;height:148px;border-radius:8px;z-index:4;pointer-events:none;}
  #box-ribbon-h{display:none;position:absolute;left:16px;right:16px;top:calc(40px + 63px);height:14px;background:linear-gradient(90deg,#f87171,#fca5a5,#f87171);border-radius:2px;z-index:6;box-shadow:0 0 8px #f8717188;}
  #box-ribbon-v{display:none;position:absolute;left:calc(20px + 73px);top:36px;bottom:-4px;width:14px;background:linear-gradient(180deg,#f87171,#fca5a5,#f87171);border-radius:2px;z-index:6;box-shadow:0 0 8px #f8717188;}
  #box-bow{display:none;position:absolute;left:calc(20px + 67px);top:16px;font-size:24px;z-index:7;}
  #box-seal{display:none;position:absolute;right:10px;top:50px;z-index:10;background:#4ade80;border-radius:50%;width:36px;height:36px;display:none;align-items:center;justify-content:center;font-size:16px;border:3px solid #166534;box-shadow:0 0 12px #4ade8088;}
  #box-label{display:none;position:absolute;left:28px;bottom:14px;width:128px;background:#fff;border-radius:4px;padding:3px 6px;font-size:8px;color:#111;z-index:10;border:1px solid #d1d5db;}
  #box-label .lbl-title{font-weight:700;color:#7c3aed;}
  .checklist{margin-top:12px;display:flex;flex-direction:column;gap:4px;font-size:10px;min-width:200px;}
  .check-item{display:flex;align-items:center;gap:6px;color:#4b5563;transition:color .3s;}
  .check-item.done{color:inherit;}
  .ctrl-side{flex:1;min-width:220px;max-width:280px;}
  #step-card{background:#0f172a;border-radius:12px;padding:16px;margin-bottom:14px;transition:border-color .3s;}
  #step-icon{font-size:32px;text-align:center;margin-bottom:8px;}
  #step-title{font-weight:700;font-size:14px;margin-bottom:6px;}
  #step-desc{font-size:12px;margin-bottom:4px;}
  #step-detail{color:#6b7280;font-size:11px;font-style:italic;}
  .progress-bar{height:10px;background:#1f2937;border-radius:5px;margin-bottom:10px;overflow:hidden;}
  .progress-fill{height:100%;border-radius:5px;transition:width .03s;}
  #wrap-btn{width:100%;padding:14px 0;font-size:16px;font-weight:700;border:2px solid currentColor;border-radius:10px;cursor:pointer;transition:all .15s;font-family:'Share Tech Mono',monospace;}
  .done-card{background:#052e16;border:2px solid #4ade80;border-radius:12px;padding:20px;text-align:center;}
  .done-card .big{font-size:40px;margin-bottom:8px;}
  .done-card h3{color:#4ade80;font-size:15px;margin-bottom:8px;}
  .done-card ul{list-style:none;font-size:11px;line-height:1.8;color:#6b7280;}
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
    <a href="/portfolio/network/4">L4</a><a href="/portfolio/network/5">L5</a>
    <a href="/portfolio/network/6" class="active">L6</a>
    <a href="/portfolio/network/7">L7</a>
  </div>
  <a href="/portfolio/network/home" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 6 · Presentation | TCP/IP Layer 4: Application (TLS lives here)</div>
    <h2>🎁 Level 6 — Wrap with TLS!</h2>
    <p class="flavor">Hold the <b>WRAP</b> button to apply each TLS layer around the HTTP package. OSI has a dedicated "Presentation" layer (L6) for encryption/encoding; TCP/IP merges L5+L6+L7 into one Application layer.</p>
    <div class="layout">
      <div class="box-side">
        <div style="font-size:12px;color:#6b7280;margin-bottom:8px;">Package Preview</div>
        <div id="box-preview">
          <div class="box-shadow"></div>
          <div id="box-lid"></div>
          <div id="box-body">
            <div id="box-content">
              <div style="font-size:14px">📄</div>
              <div style="color:#fef3c7;font-weight:700;font-size:9px">HTTP GET /api/users</div>
              <div style="color:#fde68a;font-size:8px">Host: flask.opencodingsociety.com</div>
            </div>
          </div>
          <div id="box-wrap-layer"></div>
          <div id="box-ribbon-h"></div>
          <div id="box-ribbon-v"></div>
          <div id="box-bow"></div>
          <div id="box-seal" style="display:none">🔏</div>
          <div id="box-label" style="display:none"><div class="lbl-title">🏷️ SNI: flask.opencodingsociety.com</div><div>To: 3.233.212.71 :443 | TLS 1.3 ✓</div></div>
        </div>
        <div class="checklist" id="checklist"></div>
      </div>
      <div class="ctrl-side">
        <div id="step-card">
          <div id="step-icon"></div>
          <div id="step-title"></div>
          <div id="step-desc"></div>
          <div id="step-detail"></div>
        </div>
        <div class="progress-bar"><div class="progress-fill" id="prog-fill" style="width:0%"></div></div>
        <button id="wrap-btn">Hold to Wrap</button>
        <div id="done-card" style="display:none" class="done-card">
          <div class="big">🔒🎁</div>
          <h3>HTTPS Package Ready!</h3>
          <ul><li>TLS Record Layer ✓</li><li>AES-256-GCM Encrypted ✓</li><li>HMAC Auth Tag ✓</li><li>Certbot Certified ✓</li><li>SNI Label Attached ✓</li></ul>
        </div>
      </div>
    </div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li><b>OSI Layer 6 (Presentation)</b> handles encryption, encoding, and data format translation. <b>TCP/IP</b> has no separate presentation layer — TLS, encoding, and compression are handled inside the Application layer.</li>
        <li>TLS 1.3 (via Certbot/Let's Encrypt) wraps HTTP into HTTPS on port 443. AES-256-GCM encrypts the payload; HMAC ensures tamper detection.</li>
        <li>Nginx handles TLS termination — it decrypts the HTTPS traffic and passes plaintext HTTP to Flask :8587. Flask never sees TLS.</li>
        <li>SNI (Server Name Indication) lets one IP address host many HTTPS domains — critical for shared cloud hosting.</li>
        <li><b>Deployment angle:</b> Running <code>certbot --nginx</code> on your EC2 instance auto-configures Nginx with a free Let's Encrypt TLS certificate. Without TLS, browsers block API calls from HTTPS pages to HTTP endpoints (mixed-content policy) — so HTTPS is required for any deployed frontend that calls your Flask backend.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3>Package encrypted and certified! HTTPS ready!</h3>
      <a href="/portfolio/network/7"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const STEPS=[
  {id:"body",    label:"Fold the Box Body",        icon:"📦",color:"#f59e0b",desc:"TLS Record Layer — structures data before encryption",          detail:"Like folding cardboard into a box shape before filling it"},
  {id:"encrypt", label:"Apply AES-256 Wrap",       icon:"🎨",color:"#60a5fa",desc:"AES-256-GCM encrypts every byte of the HTTP payload",           detail:"The gift wrap paper — beautiful and impossible to see through"},
  {id:"ribbon",  label:"Tie the HMAC Ribbon",      icon:"🎀",color:"#f87171",desc:"HMAC auth tag proves the package wasn't tampered with",          detail:"If anyone opens the box, the ribbon breaks — tamper detection!"},
  {id:"seal",    label:"Press the Certbot Seal",   icon:"🔏",color:"#4ade80",desc:"Let's Encrypt cert proves sender = flask.opencodingsociety.com",detail:"The wax seal of authenticity — only the real server has this key"},
  {id:"label",   label:"Attach the Address Label", icon:"🏷️",color:"#a78bfa",desc:"TLS SNI header — destination address on the outside",           detail:"Even encrypted packages need a readable address"},
];

let step=0, holding=false, progress=0, completed=[], interval=null, done=false;

const wrapBtn=document.getElementById('wrap-btn');
const progFill=document.getElementById('prog-fill');
const checklist=document.getElementById('checklist');

function buildChecklist(){
  checklist.innerHTML='';
  STEPS.forEach(ws=>{
    const div=document.createElement('div');
    div.className='check-item';
    div.id='check-'+ws.id;
    div.style.color=completed.includes(ws.id)?ws.color:'#4b5563';
    div.innerHTML=`<span>${completed.includes(ws.id)?'✅':'⬜'}</span><span>${ws.icon} ${ws.label}</span>`;
    checklist.appendChild(div);
  });
}

function updateStepCard(){
  if(done) return;
  const cur=STEPS[step];
  document.getElementById('step-icon').textContent=cur.icon;
  document.getElementById('step-title').style.color=cur.color;
  document.getElementById('step-title').textContent=`Step ${step+1}/${STEPS.length}: ${cur.label}`;
  document.getElementById('step-desc').textContent=cur.desc;
  document.getElementById('step-detail').textContent=cur.detail;
  document.getElementById('step-card').style.border=`2px solid ${cur.color}`;
  wrapBtn.style.color=cur.color;
  wrapBtn.style.border=`2px solid ${cur.color}`;
  wrapBtn.style.background='#1f2937';
  wrapBtn.textContent=`Hold to ${cur.label}`;
  progFill.style.background=`linear-gradient(90deg,${cur.color}88,${cur.color})`;
}

function applyStep(id){
  if(id==='body'){
    document.getElementById('box-lid').style.display='block';
  }
  if(id==='encrypt'){
    const b=document.getElementById('box-body');
    b.classList.add('encrypted');
    document.getElementById('box-content').innerHTML='<div style="font-size:20px;margin-bottom:4px">🔒</div><div style="color:#60a5fa;font-weight:700">ENCRYPTED</div><div style="color:#4b5563;font-family:monospace;font-size:9px">AES-256-GCM</div>';
    const wl=document.getElementById('box-wrap-layer');
    wl.style.display='block';
    wl.style.background='linear-gradient(135deg,#1d4ed888,#7c3aed88)';
    wl.style.border='2px solid #60a5fa';
    wl.style.borderRadius='8px';
  }
  if(id==='ribbon'){
    document.getElementById('box-ribbon-h').style.display='block';
    document.getElementById('box-ribbon-v').style.display='block';
    document.getElementById('box-bow').style.display='block';
    document.getElementById('box-bow').textContent='🎀';
  }
  if(id==='seal'){
    const s=document.getElementById('box-seal');
    s.style.display='flex';
  }
  if(id==='label'){
    document.getElementById('box-label').style.display='block';
  }
}

function startHold(){
  if(done||holding) return;
  holding=true;
  const cur=STEPS[step];
  wrapBtn.style.background=cur.color;
  wrapBtn.style.color='#111';
  wrapBtn.textContent=`${cur.icon} Wrapping...`;
  interval=setInterval(()=>{
    progress=Math.min(100,progress+3.5);
    progFill.style.width=progress+'%';
    if(progress>=100){
      clearInterval(interval);
      completed.push(cur.id);
      applyStep(cur.id);
      buildChecklist();
      holding=false; progress=0; progFill.style.width='0%';
      if(step+1>=STEPS.length){
        done=true;
        wrapBtn.style.display='none';
        document.getElementById('step-card').style.display='none';
        document.getElementById('done-card').style.display='block';
        document.getElementById('win-banner').classList.add('show');
      } else {
        step++;
        updateStepCard();
      }
    }
  },30);
}

function stopHold(){
  if(!holding) return;
  clearInterval(interval);
  holding=false; progress=0; progFill.style.width='0%';
  updateStepCard();
}

wrapBtn.addEventListener('mousedown',startHold);
wrapBtn.addEventListener('mouseup',stopHold);
wrapBtn.addEventListener('mouseleave',stopHold);
wrapBtn.addEventListener('touchstart',e=>{e.preventDefault();startHold();});
wrapBtn.addEventListener('touchend',stopHold);

buildChecklist();
updateStepCard();
</script>
</body>
</html>