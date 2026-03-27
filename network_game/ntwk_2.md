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

  #ner-app * { box-sizing: border-box !important; margin: 0 !important; padding: 0 !important; float: none !important; }
  #ner-app { font-family: 'Share Tech Mono', monospace !important; color: #e2e8f0 !important; padding: 16px !important; display: block !important; width: 100% !important; position: relative !important; }

  #ner-app .ner-header { background:#0f172a !important; border-bottom:1px solid #1e293b !important; padding:10px 16px !important; display:flex !important; align-items:center !important; gap:10px !important; flex-wrap:wrap !important; margin-bottom:16px !important; border-radius:8px !important; }
  #ner-app .ner-logo { font-family:'Orbitron',sans-serif !important; font-size:13px !important; color:#fff !important; font-weight:700 !important; }
  #ner-app .ner-nav { display:flex !important; gap:6px !important; flex-wrap:wrap !important; }
  #ner-app .ner-nav a { padding:3px 10px !important; border-radius:12px !important; font-size:11px !important; text-decoration:none !important; color:#6b7280 !important; background:#1f2937 !important; border:1px solid transparent !important; display:inline-block !important; }
  #ner-app .ner-nav a.active { background:#3b82f6 !important; color:#fff !important; border-color:#60a5fa !important; }
  #ner-app .ner-home { margin-left:auto !important; background:transparent !important; border:1px solid #374151 !important; color:#9ca3af !important; padding:3px 10px !important; border-radius:6px !important; cursor:pointer !important; font-size:11px !important; text-decoration:none !important; }

  #ner-app .ner-wrapper { max-width:760px !important; margin:0 auto !important; display:block !important; }
  #ner-app .ner-badge { display:inline-block !important; background:#d9770622 !important; border:1px solid #d97706 !important; border-radius:20px !important; padding:3px 12px !important; font-size:11px !important; color:#d97706 !important; font-weight:700 !important; margin-bottom:8px !important; }
  #ner-app .ner-card { background:#111827 !important; border-radius:12px !important; padding:20px !important; border:1px solid #1f2937 !important; display:block !important; }
  #ner-app .ner-card h2 { color:#fff !important; font-family:'Orbitron',sans-serif !important; font-size:18px !important; font-weight:800 !important; margin:8px 0 !important; display:block !important; }
  #ner-app .ner-flavor { color:#94a3b8 !important; font-size:13px !important; margin-bottom:16px !important; display:block !important; }

  #ner-app .ner-layout {
    display: grid !important;
    grid-template-columns: 180px 1fr !important;
    gap: 20px !important;
    align-items: start !important;
    width: 100% !important;
  }
  @media(max-width:560px){
    #ner-app .ner-layout { grid-template-columns: 1fr !important; }
  }

  #ner-app .ner-sidebar { display:block !important; width:100% !important; min-width:0 !important; overflow:visible !important; }
  #ner-app .ner-main { display:block !important; width:100% !important; min-width:0 !important; overflow:visible !important; }

  #ner-app .inbox-title { color:#60a5fa !important; font-weight:700 !important; font-size:12px !important; margin-bottom:8px !important; display:block !important; }
  #ner-app .packet-card { background:#1e3a5f !important; border:2px dashed #3b82f6 !important; border-radius:10px !important; padding:12px !important; cursor:grab !important; font-size:11px !important; line-height:1.7 !important; user-select:none !important; display:block !important; width:100% !important; position:static !important; }
  #ner-app .picon { font-size:28px !important; text-align:center !important; display:block !important; }
  #ner-app .ptitle { color:#60a5fa !important; font-weight:700 !important; display:block !important; }
  #ner-app .pmeta { color:#94a3b8 !important; display:block !important; }
  #ner-app .phint { color:#fbbf24 !important; margin-top:4px !important; display:block !important; }
  #ner-app .packet-done { background:#052e16 !important; border:2px solid #4ade80 !important; border-radius:10px !important; padding:12px !important; font-size:11px !important; color:#4ade80 !important; text-align:center !important; display:block !important; }

  #ner-app .size-box { margin-top:16px !important; background:#0f172a !important; border-radius:8px !important; padding:10px !important; font-size:11px !important; display:block !important; }
  #ner-app .size-title { color:#fbbf24 !important; font-weight:700 !important; margin-bottom:4px !important; display:block !important; }
  #ner-app .size-row { color:#94a3b8 !important; margin-bottom:2px !important; display:block !important; }
  #ner-app .size-total { color:#fff !important; font-weight:700 !important; border-top:1px solid #1f2937 !important; margin-top:4px !important; padding-top:4px !important; display:block !important; }
  #ner-app .bar-bg { height:6px !important; background:#1f2937 !important; border-radius:3px !important; margin-top:6px !important; overflow:hidden !important; display:block !important; }
  #ner-app .bar-fill { height:100% !important; background:linear-gradient(90deg,#3b82f6,#4ade80) !important; border-radius:3px !important; transition:width .4s !important; display:block !important; }

  #ner-app .field-title { color:#f59e0b !important; font-weight:700 !important; font-size:12px !important; margin-bottom:8px !important; display:block !important; }
  #ner-app .ner-field { margin-bottom:10px !important; background:#0f172a !important; border-radius:8px !important; padding:10px !important; border:2px solid #374151 !important; transition:border-color .3s !important; display:block !important; }
  #ner-app .ner-field.valid { border-color:#4ade80 !important; }
  #ner-app .ner-field.invalid { border-color:#f87171 !important; }
  #ner-app .field-header { display:flex !important; justify-content:space-between !important; margin-bottom:4px !important; align-items:center !important; }
  #ner-app .field-label { font-weight:700 !important; font-size:12px !important; }
  #ner-app .field-size { color:#6b7280 !important; font-size:10px !important; }
  #ner-app .field-row { display:flex !important; gap:6px !important; align-items:center !important; }
  #ner-app .field-row input { flex:1 !important; background:#111827 !important; border:1px solid #374151 !important; border-radius:6px !important; padding:6px 10px !important; color:#e2e8f0 !important; font-size:12px !important; font-family:'Share Tech Mono',monospace !important; outline:none !important; min-width:0 !important; }
  #ner-app .hint-btn { background:#374151 !important; border:none !important; border-radius:6px !important; padding:4px 10px !important; color:#e2e8f0 !important; cursor:pointer !important; font-size:11px !important; flex-shrink:0 !important; white-space:nowrap !important; }
  #ner-app .hint-btn:hover { background:#4b5563 !important; }
  #ner-app .drop-zone { background:#111827 !important; border:2px dashed #374151 !important; border-radius:6px !important; padding:10px !important; text-align:center !important; font-size:11px !important; color:#6b7280 !important; margin-top:4px !important; transition:all .2s !important; display:block !important; }
  #ner-app .drop-zone.drag-over { background:#1e3a5f !important; border-color:#60a5fa !important; }
  #ner-app .drop-zone.loaded { background:#052e16 !important; border-color:#4ade80 !important; color:#4ade80 !important; }
  #ner-app .crc-row { display:flex !important; gap:8px !important; align-items:center !important; margin-top:4px !important; }
  #ner-app .crc-val { flex:1 !important; background:#111827 !important; border-radius:6px !important; padding:8px 10px !important; font-size:11px !important; font-family:'Share Tech Mono',monospace !important; color:#4b5563 !important; }
  #ner-app .crc-val.ready { color:#f87171 !important; }
  #ner-app .seal-btn { background:#374151 !important; border:none !important; border-radius:6px !important; padding:6px 12px !important; color:#e2e8f0 !important; cursor:pointer !important; font-size:11px !important; font-family:'Share Tech Mono',monospace !important; flex-shrink:0 !important; white-space:nowrap !important; }
  #ner-app .seal-btn.active { background:#f87171 !important; color:#fff !important; }

  #ner-app .ner-facts { background:#0f172a !important; border:1px solid #1e3a5f !important; border-radius:8px !important; padding:10px !important; margin-top:16px !important; display:block !important; }
  #ner-app .ner-facts summary { cursor:pointer !important; color:#60a5fa !important; font-weight:700 !important; font-size:13px !important; display:list-item !important; padding:0 !important; margin:0 !important; }
  #ner-app .ner-facts ul { margin:8px 0 0 !important; padding-left:18px !important; display:block !important; }
  #ner-app .ner-facts li { color:#94a3b8 !important; font-size:12px !important; margin-bottom:4px !important; display:list-item !important; }

  #ner-app .ner-win { background:linear-gradient(135deg,#052e16,#14532d) !important; border:2px solid #4ade80 !important; border-radius:12px !important; padding:16px !important; margin-top:16px !important; text-align:center !important; display:none !important; }
  #ner-app .ner-win.show { display:block !important; }
  #ner-app .ner-win h3 { color:#4ade80 !important; font-size:16px !important; margin:8px 0 !important; }
  #ner-app .ner-btn { background:#4ade80 !important; color:#052e16 !important; border:none !important; border-radius:8px !important; padding:10px 28px !important; cursor:pointer !important; font-weight:700 !important; font-size:14px !important; font-family:'Share Tech Mono',monospace !important; }
</style>
</head>
<body>
<div id="ner-app">
  <div class="ner-header">
    <span class="ner-logo">📬 Network Escape Room</span>
    <div class="ner-nav">
      <a href="/portfolio/network/1">L1</a>
      <a href="/portfolio/network/2" class="active">L2</a>
      <a href="/portfolio/network/3">L3</a>
      <a href="/portfolio/network/4">L4</a>
      <a href="/portfolio/network/5">L5</a>
      <a href="/portfolio/network/6">L6</a>
      <a href="/portfolio/network/7">L7</a>
    </div>
    <a href="/portfolio/network/home" class="ner-home">🏠</a>
  </div>

  <div class="ner-wrapper">
    <div class="ner-card">
      <div class="ner-badge">OSI Layer 2 / TCP-IP: Network Access</div>
      <h2>📦 Level 2 — Build the Ethernet Frame</h2>
      <p class="ner-flavor">Type the correct values, drag the IP packet into the payload slot, then compute the CRC to seal the frame!</p>

      <div class="ner-layout">
        <!-- SIDEBAR -->
        <div class="ner-sidebar">
          <div class="inbox-title">📥 Inbox — IP Packet</div>
          <div id="packet-src" class="packet-card" draggable="true"
               ondragstart="event.dataTransfer.setData('text','packet')">
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

        <!-- MAIN -->
        <div class="ner-main">
          <div class="field-title">🖊️ Ethernet Frame Fields</div>

          <div class="ner-field" id="f-dstMac">
            <div class="field-header">
              <span class="field-label" style="color:#f59e0b">Dst MAC <span class="field-size">(6B)</span></span>
              <span id="ok-dstMac"></span>
            </div>
            <div class="field-row">
              <input id="inp-dstMac" placeholder="AA:BB:CC:DD:EE:FF" oninput="checkField('dstMac',this.value)"/>
              <button class="hint-btn" onclick="autofill('dstMac')">💡</button>
            </div>
          </div>

          <div class="ner-field" id="f-srcMac">
            <div class="field-header">
              <span class="field-label" style="color:#f59e0b">Src MAC <span class="field-size">(6B)</span></span>
              <span id="ok-srcMac"></span>
            </div>
            <div class="field-row">
              <input id="inp-srcMac" placeholder="11:22:33:44:55:66" oninput="checkField('srcMac',this.value)"/>
              <button class="hint-btn" onclick="autofill('srcMac')">💡</button>
            </div>
          </div>

          <div class="ner-field" id="f-ethertype">
            <div class="field-header">
              <span class="field-label" style="color:#60a5fa">EtherType <span class="field-size">(2B)</span></span>
              <span id="ok-ethertype"></span>
            </div>
            <div class="field-row">
              <input id="inp-ethertype" placeholder="0x0800" oninput="checkField('ethertype',this.value)"/>
              <button class="hint-btn" onclick="autofill('ethertype')">💡</button>
            </div>
          </div>

          <div class="ner-field" id="f-payload">
            <span class="field-label" style="color:#4ade80">IP Payload <span class="field-size">(≤1500B)</span></span>
            <div class="drop-zone" id="drop-zone"
                 ondragover="event.preventDefault();this.classList.add('drag-over')"
                 ondragleave="this.classList.remove('drag-over')"
                 ondrop="dropPacket(event)">⬇ Drop IP packet here</div>
          </div>

          <div class="ner-field" id="f-crc">
            <span class="field-label" style="color:#f87171">CRC/FCS <span class="field-size">(4B)</span></span>
            <div class="crc-row">
              <div class="crc-val" id="crc-val">[ Complete fields above first ]</div>
              <button class="seal-btn" id="seal-btn" onclick="computeCrc()">🔒 Seal</button>
            </div>
          </div>
        </div>
      </div>

      <details class="ner-facts">
        <summary>📚 Network Facts ▼</summary>
        <ul>
          <li>Ethernet frame = 14B header + payload (≤1500B) + 4B CRC = 1518B max.</li>
          <li>CRC detects bit errors in transit — like a tamper-proof seal.</li>
          <li>EtherType 0x0800 = IPv4. 0x86DD = IPv6. 0x0806 = ARP.</li>
        </ul>
      </details>

      <div class="ner-win" id="win-banner">
        <div style="font-size:28px">🎉</div>
        <h3>Frame built and sealed! Ready for transmission!</h3>
        <a href="/portfolio/network/3"><button class="ner-btn">Next Level →</button></a>
      </div>
    </div>
  </div>
</div>

<script>
const FIELDS = {
  dstMac:    { answer:"AA:BB:CC:DD:EE:FF", validate: v => /^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$/.test(v.trim()) },
  srcMac:    { answer:"11:22:33:44:55:66", validate: v => /^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$/.test(v.trim()) },
  ethertype: { answer:"0x0800",            validate: v => v.trim() === "0x0800" },
};
const state = { dstMac:false, srcMac:false, ethertype:false, payload:false, crc:false };

function checkField(id, val) {
  const f = FIELDS[id];
  const el = document.getElementById('f-'+id);
  const ok = document.getElementById('ok-'+id);
  if (f.validate(val)) {
    el.classList.add('valid'); el.classList.remove('invalid');
    ok.textContent = '✓'; ok.style.color = '#4ade80';
    state[id] = true;
  } else {
    el.classList.remove('valid');
    if (val.length > 0) { el.classList.add('invalid'); ok.textContent = ''; }
    else { el.classList.remove('invalid'); ok.textContent = ''; }
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
  const src = document.getElementById('packet-src');
  src.style.display = 'none';
  const pd = document.createElement('div');
  pd.className = 'packet-done';
  pd.textContent = '✅ In frame!';
  src.parentNode.insertBefore(pd, src);
  state.payload = true;
  updateSize();
}

function computeCrc() {
  if (!state.dstMac || !state.srcMac || !state.ethertype || !state.payload) {
    const f = document.getElementById('f-crc');
    f.style.borderColor = '#f87171';
    setTimeout(() => { f.style.borderColor = '#374151'; }, 800);
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
  document.getElementById('sz-bar').style.width = `${Math.min(100, (total/1518)*100)}%`;
}
</script>
</body>
</html>