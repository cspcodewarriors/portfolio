---
permalink: /network/2/
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 2 – Build the Ethernet Frame</title>
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
  .osi-badge{display:inline-block;background:#d9770622;border:1px solid #d97706;border-radius:20px;padding:3px 12px;font-size:11px;color:#d97706;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:16px;}
  .layout{display:flex;gap:20px;flex-wrap:wrap;justify-content:center;}
  .sidebar{min-width:160px;}
  .main{flex:1;min-width:280px;}
  .inbox-title{color:#60a5fa;font-weight:700;font-size:12px;margin-bottom:8px;}
  .packet-card{background:#1e3a5f;border:2px dashed #3b82f6;border-radius:10px;padding:12px;cursor:grab;font-size:11px;line-height:1.7;user-select:none;}
  .packet-card .picon{font-size:28px;text-align:center;}
  .packet-card .ptitle{color:#60a5fa;font-weight:700;}
  .packet-card .pmeta{color:#94a3b8;}
  .packet-card .phint{color:#fbbf24;margin-top:4px;}
  .packet-done{background:#052e16;border:2px solid #4ade80;border-radius:10px;padding:12px;font-size:11px;color:#4ade80;text-align:center;}
  .size-box{margin-top:16px;background:#0f172a;border-radius:8px;padding:10px;font-size:11px;}
  .size-title{color:#fbbf24;font-weight:700;margin-bottom:4px;}
  .size-row{color:#94a3b8;margin-bottom:2px;}
  .size-total{color:#fff;font-weight:700;border-top:1px solid #1f2937;margin-top:4px;padding-top:4px;}
  .bar-bg{height:6px;background:#1f2937;border-radius:3px;margin-top:6px;overflow:hidden;}
  .bar-fill{height:100%;background:linear-gradient(90deg,#3b82f6,#4ade80);border-radius:3px;transition:width .4s;}
  .field-title{color:#f59e0b;font-weight:700;font-size:12px;margin-bottom:8px;}
  .field{margin-bottom:10px;background:#0f172a;border-radius:8px;padding:10px;border:2px solid #374151;transition:border-color .3s;}
  .field.valid{border-color:#4ade80;}
  .field.invalid{border-color:#f87171;}
  .field-header{display:flex;justify-content:space-between;margin-bottom:4px;}
  .field-label{font-weight:700;font-size:12px;}
  .field-size{color:#6b7280;font-size:10px;}
  .field-row{display:flex;gap:6px;}
  .field input{flex:1;background:#111827;border:1px solid #374151;border-radius:6px;padding:6px 10px;color:#e2e8f0;font-size:12px;font-family:'Share Tech Mono',monospace;outline:none;}
  .hint-btn{background:#374151;border:none;border-radius:6px;padding:4px 10px;color:#e2e8f0;cursor:pointer;font-size:11px;}
  .hint-btn:hover{background:#4b5563;}
  .drop-zone{background:#111827;border:2px dashed #374151;border-radius:6px;padding:10px;text-align:center;font-size:11px;color:#6b7280;margin-top:4px;transition:all .2s;}
  .drop-zone.drag-over{background:#1e3a5f;border-color:#60a5fa;}
  .drop-zone.loaded{background:#052e16;border-color:#4ade80;color:#4ade80;}
  .crc-row{display:flex;gap:8px;align-items:center;margin-top:4px;}
  .crc-val{flex:1;background:#111827;border-radius:6px;padding:8px 10px;font-size:11px;font-family:'Share Tech Mono',monospace;color:#4b5563;}
  .crc-val.ready{color:#f87171;}
  .seal-btn{background:#374151;border:none;border-radius:6px;padding:6px 12px;color:#e2e8f0;cursor:pointer;font-size:11px;font-family:'Share Tech Mono',monospace;}
  .seal-btn.active{background:#f87171;color:#fff;}
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
    <a href="level1.html">L1</a>
    <a href="level2.html" class="active">L2</a>
    <a href="level3.html">L3</a><a href="level4.html">L4</a>
    <a href="level5.html">L5</a><a href="level6.html">L6</a><a href="level7.html">L7</a>
  </div>
  <a href="index.html" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 2 / TCP-IP: Network Access</div>
    <h2>📦 Level 2 — Build the Ethernet Frame</h2>
    <p class="flavor">Type the correct values, drag the IP packet into the payload slot, then compute the CRC to seal the frame!</p>
    <div class="layout">
      <div class="sidebar">
        <div class="inbox-title">📥 Inbox — IP Packet</div>
        <div id="packet-src" class="packet-card" draggable="true">
          <div class="picon">📦</div>
          <div class="ptitle">IP Packet</div>
          <div class="pmeta">Src: 185.199.110.153</div>
          <div class="pmeta">Dst: 3.233.212.71</div>
          <div class="pmeta">Proto: TCP | HTTP GET</div>
          <div class="phint">Drag me →</div>
        </div>
        <div class="size-box">
          <div class="size-title">📊 Frame Size</div>
          <div class="size-row">Header: 14B</div>
          <div class="size-row" id="sz-payload">Payload: 0B</div>
          <div class="size-row" id="sz-crc">CRC: 0B</div>
          <div class="size-total" id="sz-total">Total: 14B / 1518B</div>
          <div class="bar-bg"><div class="bar-fill" id="sz-bar" style="width:0.92%"></div></div>
        </div>
      </div>
      <div class="main">
        <div class="field-title">🖊️ Ethernet Frame Fields</div>
        <div class="field" id="f-dstMac">
          <div class="field-header"><span class="field-label" style="color:#f59e0b">Dst MAC <span class="field-size">(6B)</span></span><span id="ok-dstMac"></span></div>
          <div class="field-row">
            <input id="inp-dstMac" placeholder="AA:BB:CC:DD:EE:FF" oninput="checkField('dstMac',this.value)"/>
            <button class="hint-btn" onclick="autofill('dstMac')">💡</button>
          </div>
        </div>
        <div class="field" id="f-srcMac">
          <div class="field-header"><span class="field-label" style="color:#f59e0b">Src MAC <span class="field-size">(6B)</span></span><span id="ok-srcMac"></span></div>
          <div class="field-row">
            <input id="inp-srcMac" placeholder="11:22:33:44:55:66" oninput="checkField('srcMac',this.value)"/>
            <button class="hint-btn" onclick="autofill('srcMac')">💡</button>
          </div>
        </div>
        <div class="field" id="f-ethertype">
          <div class="field-header"><span class="field-label" style="color:#60a5fa">EtherType <span class="field-size">(2B)</span></span><span id="ok-ethertype"></span></div>
          <div class="field-row">
            <input id="inp-ethertype" placeholder="0x0800" oninput="checkField('ethertype',this.value)"/>
            <button class="hint-btn" onclick="autofill('ethertype')">💡</button>
          </div>
        </div>
        <div class="field" id="f-payload">
          <span class="field-label" style="color:#4ade80">IP Payload <span class="field-size">(≤1500B)</span></span>
          <div class="drop-zone" id="drop-zone" ondragover="event.preventDefault();this.classList.add('drag-over')" ondragleave="this.classList.remove('drag-over')" ondrop="dropPacket(event)">⬇ Drop IP packet here</div>
        </div>
        <div class="field" id="f-crc">
          <span class="field-label" style="color:#f87171">CRC/FCS <span class="field-size">(4B)</span></span>
          <div class="crc-row">
            <div class="crc-val" id="crc-val">[ Complete fields above first ]</div>
            <button class="seal-btn" id="seal-btn" onclick="computeCrc()">🔒 Seal</button>
          </div>
        </div>
      </div>
    </div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>Ethernet frame = 14B header + payload (≤1500B) + 4B CRC = 1518B max.</li>
        <li>CRC detects bit errors in transit — like a tamper-proof seal.</li>
        <li>EtherType 0x0800 = IPv4. 0x86DD = IPv6. 0x0806 = ARP.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3>Frame built and sealed! Ready for transmission!</h3>
      <a href="level3.html"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const FIELDS = {
  dstMac:    {answer:"AA:BB:CC:DD:EE:FF", validate: v=>/^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$/.test(v.trim())},
  srcMac:    {answer:"11:22:33:44:55:66", validate: v=>/^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$/.test(v.trim())},
  ethertype: {answer:"0x0800",            validate: v=>v.trim()==="0x0800"},
};
const state = {dstMac:false, srcMac:false, ethertype:false, payload:false, crc:false};

function checkField(id, val) {
  const f = FIELDS[id];
  const el = document.getElementById('f-'+id);
  const ok = document.getElementById('ok-'+id);
  if (f.validate(val)) {
    el.classList.add('valid'); el.classList.remove('invalid');
    ok.textContent = '✓'; ok.style.color='#4ade80';
    state[id] = true;
  } else {
    el.classList.remove('valid');
    if (val.length > 0) { el.classList.add('invalid'); ok.textContent=''; }
    else { el.classList.remove('invalid'); ok.textContent=''; }
    state[id] = false;
  }
}

function autofill(id) {
  document.getElementById('inp-'+id).value = FIELDS[id].answer;
  checkField(id, FIELDS[id].answer);
}

function dropPacket(e) {
  e.preventDefault();
  const dz = document.getElementById('drop-zone');
  dz.classList.remove('drag-over');
  dz.classList.add('loaded');
  dz.textContent = '✅ IP Packet loaded (1460B)';
  document.getElementById('packet-src').style.display='none';
  const pd = document.createElement('div');
  pd.className='packet-done'; pd.textContent='✅ In frame!';
  document.getElementById('packet-src').parentNode.insertBefore(pd, document.getElementById('packet-src'));
  state.payload = true;
  updateSize();
}

function computeCrc() {
  if (!state.dstMac || !state.srcMac || !state.ethertype || !state.payload) {
    const f = document.getElementById('f-crc');
    f.style.borderColor='#f87171';
    setTimeout(()=>{f.style.borderColor='#374151';},800);
    return;
  }
  document.getElementById('crc-val').classList.add('ready');
  document.getElementById('crc-val').textContent = 'CRC: A3:F2:01:CC ✓';
  document.getElementById('seal-btn').classList.add('active');
  state.crc = true;
  updateSize();
  document.getElementById('win-banner').classList.add('show');
}

function updateSize() {
  const p = state.payload ? 1460 : 0;
  const c = state.crc ? 4 : 0;
  const total = 14 + p + c;
  document.getElementById('sz-payload').textContent = `Payload: ${p}B`;
  document.getElementById('sz-payload').style.color = state.payload ? '#4ade80' : '#94a3b8';
  document.getElementById('sz-crc').textContent = `CRC: ${c}B`;
  document.getElementById('sz-crc').style.color = state.crc ? '#f87171' : '#94a3b8';
  document.getElementById('sz-total').textContent = `Total: ${total}B / 1518B`;
  document.getElementById('sz-bar').style.width = `${Math.min(100,(total/1518)*100)}%`;
}
</script>
</body>
</html>