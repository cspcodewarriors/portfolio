---
permalink: /network/1
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 1 – Wire the Network</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#3b82f6;color:#fff;border-color:#60a5fa;}
  .nav-links a.done{background:#052e16;color:#4ade80;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#6b728022;border:1px solid #6b7280;border-radius:20px;padding:3px 12px;font-size:11px;color:#6b7280;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:12px;}
  #game-area{position:relative;user-select:none;}
  svg#wires{position:absolute;top:0;left:0;width:100%;height:300px;pointer-events:none;z-index:2;}
  .columns{display:flex;justify-content:space-between;align-items:center;height:300px;}
  .col-ports{display:flex;flex-direction:column;gap:18px;padding:0 8px;}
  .col-labels{display:flex;flex-direction:column;gap:18px;}
  .port{width:36px;height:36px;border-radius:50%;cursor:crosshair;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;color:#111;position:relative;z-index:3;transition:transform .15s;}
  .port:hover{transform:scale(1.15);}
  .port.done-port{cursor:default;background:#052e16!important;color:#4ade80;}
  .label-text{font-size:12px;font-weight:700;}
  .middle{flex:1;text-align:center;color:#4b5563;font-size:12px;}
  .middle .icon{font-size:32px;margin-bottom:4px;}
  .facts{background:#0f172a;border:1px solid #1e3a5f;border-radius:8px;padding:10px;margin-top:16px;}
  .facts summary{cursor:pointer;color:#60a5fa;font-weight:700;font-size:13px;}
  .facts ul{margin:8px 0 0;padding-left:18px;}
  .facts li{color:#94a3b8;font-size:12px;margin-bottom:4px;}
  .win{background:linear-gradient(135deg,#052e16,#14532d);border:2px solid #4ade80;border-radius:12px;padding:16px;margin-top:16px;text-align:center;display:none;}
  .win.show{display:block;}
  .win h3{color:#4ade80;font-size:16px;margin:8px 0;}
  .btn{background:#4ade80;color:#052e16;border:none;border-radius:8px;padding:10px 28px;cursor:pointer;font-weight:700;font-size:14px;font-family:'Share Tech Mono',monospace;}
  .btn:hover{background:#22c55e;}
</style>
</head>
<body>
<div class="header">
  <span class="logo">📬 Network Escape Room</span>
  <div class="nav-links">
    <a href="/portfolio/network/1" class="active">L1</a>
    <a href="/portfolio/network/2">L2</a><a href="/portfolio/network/3">L3</a><a href="/portfolio/network/4">L4</a>
    <a href="/portfolio/network/5">L5</a><a href="/portfolio/network/6">L6</a><a href="/portfolio/network/7">L7</a>
  </div>
  <a href="/portfolio/network/home" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 1 / TCP-IP: Physical</div>
    <h2>🔌 Level 1 — Wire the Network</h2>
    <p class="flavor">Drag from a colored port to its matching device — like Among Us wiring!</p>
    <div id="game-area">
      <svg id="wires"></svg>
      <div class="columns">
        <div class="col-ports" id="left-ports"></div>
        <div class="col-labels" id="left-labels"></div>
        <div class="middle"><div class="icon">📡</div>Electrical/Optical<br/>0s &amp; 1s</div>
        <div class="col-labels" id="right-labels"></div>
        <div class="col-ports" id="right-ports"></div>
      </div>
    </div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>Physical layer = raw bits as electrical/optical/radio signals.</li>
        <li>Ethernet max frame = 1518 bytes — origin of MTU.</li>
        <li>GitHub Pages uses Wi-Fi; AWS EC2 runs on fiber in the datacenter.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3>All cables connected! Signals are flowing!</h3>
      <a href="/portfolio/network/2"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const cables = [
  {id:"eth",  label:"Ethernet",    color:"#f59e0b"},
  {id:"fib",  label:"Fiber Optic", color:"#06b6d4"},
  {id:"wifi", label:"Wi-Fi",       color:"#a78bfa"},
  {id:"coax", label:"Coaxial",     color:"#f87171"},
];
const rightDefs = [
  {cableId:"eth",  label:"🏠 Router"},
  {cableId:"fib",  label:"☁️ AWS EC2"},
  {cableId:"wifi", label:"💻 GitHub Pages"},
  {cableId:"coax", label:"🌐 ISP Node"},
];
// Shuffle right ports
const shuffled = [...rightDefs].sort(()=>Math.random()-.5);

const connected = {};
const lines = [];
let drawing = null;

const svg = document.getElementById('wires');
const gameArea = document.getElementById('game-area');
const leftPortsEl = document.getElementById('left-ports');
const leftLabels = document.getElementById('left-labels');
const rightLabels = document.getElementById('right-labels');
const rightPortsEl = document.getElementById('right-ports');

const portEls = {};

function buildUI() {
  cables.forEach(c => {
    // Left port
    const p = document.createElement('div');
    p.className = 'port';
    p.id = 'lp_'+c.id;
    p.style.background = c.color;
    p.style.border = `3px solid ${c.color}`;
    p.addEventListener('mousedown', e => startDraw(e, 'lp_'+c.id, c.id));
    leftPortsEl.appendChild(p);
    portEls['lp_'+c.id] = p;
    // Left label
    const lbl = document.createElement('div');
    lbl.className = 'label-text';
    lbl.style.color = c.color;
    lbl.textContent = c.label;
    leftLabels.appendChild(lbl);
  });
  shuffled.forEach(r => {
    const c = cables.find(c=>c.id===r.cableId);
    // Right label
    const lbl = document.createElement('div');
    lbl.className = 'label-text';
    lbl.style.color = c.color;
    lbl.style.textAlign = 'right';
    lbl.textContent = r.label;
    rightLabels.appendChild(lbl);
    // Right port
    const p = document.createElement('div');
    p.className = 'port';
    p.id = 'rp_'+r.cableId;
    p.style.background = '#1f2937';
    p.style.border = `3px solid ${c.color}`;
    p.addEventListener('mouseup', e => onDrop(e, r.cableId));
    rightPortsEl.appendChild(p);
    portEls['rp_'+r.cableId] = p;
  });
}

function getCenter(id) {
  const el = portEls[id];
  const sr = svg.getBoundingClientRect();
  const er = el.getBoundingClientRect();
  return {x: er.left+er.width/2-sr.left, y: er.top+er.height/2-sr.top};
}

function startDraw(e, portId, cableId) {
  if (connected[cableId]) return;
  e.preventDefault();
  const c = cables.find(c=>c.id===cableId);
  const {x,y} = getCenter(portId);
  drawing = {cableId, color:c.color, x1:x, y1:y, x2:x, y2:y, fromId:portId};
  redraw();
}

gameArea.addEventListener('mousemove', e => {
  if (!drawing) return;
  const r = svg.getBoundingClientRect();
  drawing.x2 = e.clientX - r.left;
  drawing.y2 = e.clientY - r.top;
  redraw();
});
gameArea.addEventListener('mouseup', () => { drawing=null; redraw(); });

function onDrop(e, cableId) {
  if (!drawing) return;
  if (cableId === drawing.cableId) {
    const {x,y} = getCenter('rp_'+cableId);
    const {x:x1,y:y1} = getCenter(drawing.fromId);
    lines.push({cableId, color:drawing.color, x1, y1, x2:x, y2:y});
    connected[cableId] = true;
    markDone(cableId);
  }
  drawing = null;
  redraw();
  if (Object.keys(connected).length === cables.length) {
    document.getElementById('win-banner').classList.add('show');
  }
}

function markDone(cableId) {
  const lp = portEls['lp_'+cableId];
  const rp = portEls['rp_'+cableId];
  lp.classList.add('done-port'); lp.style.background='#052e16'; lp.textContent='✓';
  rp.classList.add('done-port'); rp.style.background='#052e16'; rp.textContent='✓';
}

function redraw() {
  svg.innerHTML = '';
  lines.forEach(l => {
    const line = document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1',l.x1); line.setAttribute('y1',l.y1);
    line.setAttribute('x2',l.x2); line.setAttribute('y2',l.y2);
    line.setAttribute('stroke',l.color); line.setAttribute('stroke-width','5');
    line.setAttribute('stroke-linecap','round');
    svg.appendChild(line);
  });
  if (drawing) {
    const line = document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1',drawing.x1); line.setAttribute('y1',drawing.y1);
    line.setAttribute('x2',drawing.x2); line.setAttribute('y2',drawing.y2);
    line.setAttribute('stroke',drawing.color); line.setAttribute('stroke-width','5');
    line.setAttribute('stroke-linecap','round'); line.setAttribute('stroke-dasharray','8 4');
    svg.appendChild(line);
  }
}

buildUI();
</script>
</body>
</html>