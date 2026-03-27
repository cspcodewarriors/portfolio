---
permalink: /network/5
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Level 5 – TCP Handshake Arcade</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;padding:16px;}
  .header{background:#0f172a;border-bottom:1px solid #1e293b;padding:10px 16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:16px;border-radius:8px;}
  .header .logo{font-family:'Orbitron',sans-serif;font-size:13px;color:#fff;font-weight:700;}
  .nav-links{display:flex;gap:6px;flex-wrap:wrap;}
  .nav-links a{padding:3px 10px;border-radius:12px;font-size:11px;text-decoration:none;color:#6b7280;background:#1f2937;border:1px solid transparent;}
  .nav-links a.active{background:#0891b2;color:#fff;border-color:#67e8f9;}
  .home-btn{margin-left:auto;background:transparent;border:1px solid #374151;color:#9ca3af;padding:3px 10px;border-radius:6px;cursor:pointer;font-size:11px;text-decoration:none;}
  .wrapper{max-width:760px;margin:0 auto;}
  .osi-badge{display:inline-block;background:#0891b222;border:1px solid #0891b2;border-radius:20px;padding:3px 12px;font-size:11px;color:#67e8f9;font-weight:700;margin-bottom:8px;}
  .card{background:#111827;border-radius:12px;padding:20px;border:1px solid #1f2937;}
  h2{color:#fff;font-family:'Orbitron',sans-serif;font-size:18px;font-weight:800;margin:8px 0;}
  .flavor{color:#94a3b8;font-size:13px;margin-bottom:12px;}
  #arena{position:relative;background:#0f172a;border-radius:12px;height:340px;max-width:640px;margin:0 auto;border:1px solid #1f2937;overflow:hidden;}
  #arena svg{position:absolute;inset:0;width:100%;height:100%;pointer-events:none;}
  .actor{position:absolute;top:8px;text-align:center;width:90px;}
  .actor .emoji{font-size:28px;}
  .actor .name{font-size:10px;font-weight:700;line-height:1.3;}
  .timeline{position:absolute;top:50px;width:2px;height:270px;background:#1e293b;}
  .flying-pkt{position:absolute;border-radius:8px;padding:3px 8px;font-size:10px;font-weight:700;z-index:5;white-space:nowrap;pointer-events:none;}
  .internal-label{position:absolute;font-size:10px;font-weight:700;}
  #send-area{position:absolute;bottom:10px;left:50%;transform:translateX(-50%);text-align:center;}
  #step-info{font-size:10px;color:#6b7280;margin-bottom:4px;max-width:300px;}
  #send-btn{background:#3b82f6;color:#fff;border:none;border-radius:8px;padding:7px 20px;cursor:pointer;font-weight:700;font-size:13px;font-family:'Share Tech Mono',monospace;}
  #send-btn:disabled{opacity:.5;cursor:default;}
  #quiz-overlay{position:absolute;inset:0;background:#0a0f1eee;display:flex;align-items:center;justify-content:center;z-index:20;padding:16px;}
  #quiz-box{background:#1e293b;border-radius:12px;padding:18px;max-width:360px;width:100%;border:2px solid #334155;}
  #quiz-title{color:#fbbf24;font-weight:700;font-size:13px;margin-bottom:10px;}
  #quiz-q{color:#e2e8f0;font-size:13px;margin-bottom:12px;}
  #quiz-opts{display:flex;flex-direction:column;gap:6px;}
  .quiz-opt{background:#111827;border:2px solid #374151;border-radius:8px;padding:8px 12px;color:#e2e8f0;font-size:12px;cursor:pointer;text-align:left;transition:all .2s;font-family:'Share Tech Mono',monospace;}
  .quiz-opt.correct{background:#052e16;border-color:#4ade80;color:#4ade80;}
  .quiz-opt.wrong{background:#450a0a;border-color:#f87171;color:#f87171;}
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
    <a href="/portfolio/network/1">L1</a><a href="/portfolio/network/2">L2</a><a href="/portfolio/network/3">L3</a><a href="/portfolio/network/4">L4</a>
    <a href="/portfolio/network/5" class="active">L5</a>
    <a href="/portfolio/network/6">L6</a><a href="/portfolio/network/7">L7</a>
  </div>
  <a href="/portfolio/network/home" class="home-btn">🏠</a>
</div>
<div class="wrapper">
  <div class="card">
    <div class="osi-badge">OSI Layer 5 · Session (+ L4 Transport) | TCP/IP Layer 3: Transport</div>
    <h2>📡 Level 5 — TCP Handshake Arcade!</h2>
    <p class="flavor">Click <b>SEND</b> to fire each packet, then answer the quiz before the next one flies! OSI has a separate "Session" layer (L5); TCP/IP folds session management directly into the Transport layer.</p>
    <div id="arena">
      <div class="actor" style="left:36px" id="actor-client">
        <div class="emoji">💻</div>
        <div class="name" style="color:#60a5fa">GitHub Pages<br/>185.199.x.x</div>
      </div>
      <div class="actor" style="left:476px" id="actor-server">
        <div class="emoji">☁️</div>
        <div class="name" style="color:#4ade80">AWS EC2 Nginx<br/>3.233.212.71</div>
      </div>
      <div class="timeline" style="left:80px"></div>
      <div class="timeline" style="left:520px"></div>
      <svg id="arrows-svg"></svg>
      <div id="internal-labels"></div>
      <div id="flying-pkt" class="flying-pkt" style="display:none"></div>
      <div id="quiz-overlay" style="display:none">
        <div id="quiz-box">
          <div id="quiz-title">🎯 Quick Check!</div>
          <div id="quiz-q"></div>
          <div id="quiz-opts"></div>
        </div>
      </div>
      <div id="send-area">
        <div id="step-info"></div>
        <button id="send-btn" onclick="sendPacket()">📡 Send</button>
      </div>
    </div>
    <details class="facts">
      <summary>📚 Network Facts ▼</summary>
      <ul>
        <li>TCP 3-way handshake: SYN → SYN-ACK → ACK before any data flows. This is OSI L5 (Session) behavior implemented inside TCP, which lives at OSI L4 / TCP/IP L3.</li>
        <li><b>OSI vs TCP/IP:</b> OSI defines a dedicated Session layer (L5) for connection management. TCP/IP has no separate session layer — TCP itself handles session setup and teardown, collapsing OSI L4+L5 into one Transport layer.</li>
        <li>Nginx :443 handles the TLS session and TCP connection; it proxies the decrypted request internally to Flask :8587 over a new local TCP session.</li>
        <li><b>Deployment angle:</b> Every <code>fetch()</code> call from GitHub Pages triggers a full TCP handshake to your EC2 instance. HTTP/2 and HTTP/3 reduce overhead by multiplexing many requests over a single TCP (or QUIC) session — an important deployment optimization for API-heavy frontends.</li>
      </ul>
    </details>
    <div class="win" id="win-banner">
      <div style="font-size:28px">🎉</div>
      <h3>TCP session mastered!</h3>
      <a href="/portfolio/network/6"><button class="btn">Next Level →</button></a>
    </div>
  </div>
</div>
<script>
const CLIENT_X=80, SERVER_X=520;
const steps=[
  {id:"syn",    from:"client",to:"server",label:"SYN",                 color:"#60a5fa",info:"Client: 'Hey AWS, I want to connect! Seq=1000'"},
  {id:"synack", from:"server",to:"client",label:"SYN-ACK",             color:"#4ade80",info:"AWS: 'Got it! Ack=1001, my Seq=5000'"},
  {id:"ack",    from:"client",to:"server",label:"ACK",                 color:"#f59e0b",info:"Client: 'Ack=5001. Connection open!'"},
  {id:"get",    from:"client",to:"server",label:"HTTP GET /api/users", color:"#a78bfa",info:"fetch() sends to flask.opencodingsociety.com"},
  {id:"nginx",  from:"server",to:"server",label:"Nginx → Flask :8587", color:"#fbbf24",info:"Nginx strips TLS, proxies to localhost:8587"},
  {id:"flask",  from:"server",to:"server",label:"Flask → SQL DB",      color:"#f97316",info:"SELECT * FROM users → JSON"},
  {id:"resp",   from:"server",to:"client",label:"200 OK + JSON",       color:"#f87171",info:"Response wrapped in HTTPS, sent to browser"},
  {id:"fin",    from:"client",to:"server",label:"FIN + ACK",           color:"#6b7280",info:"Both sides close the TCP connection"},
];
const quizzes={
  syn:    {q:"Why does TCP send SYN first?",            opts:["Say hello to DNS","Initiate connection with sequence number","Encrypt with TLS","Query SQL database"],correct:1},
  synack: {q:"What does ACK=1001 mean?",               opts:["Send 1001 bytes","Expecting seq 1001 next","Port 1001 open","1001 packets sent"],correct:1},
  ack:    {q:"After 3-way handshake, connection is...",opts:["Encrypted","Established & reliable","Closed","Pending"],correct:1},
  get:    {q:"Which port does HTTPS use?",             opts:["8080","8587","443","80"],correct:2},
  nginx:  {q:"What port does Flask run on internally?",opts:["443","80","8080","8587"],correct:3},
  flask:  {q:"GET /api/users maps to which SQL op?",   opts:["INSERT","UPDATE","SELECT (Read)","DELETE"],correct:2},
  resp:   {q:"HTTP 200 means...",                      opts:["Not Found","Server Error","OK - Success","Redirect"],correct:2},
  fin:    {q:"What closes a TCP connection?",          opts:["RST only","FIN + ACK exchange","DNS query","HTTP DELETE"],correct:1},
};

let phase=0;
let arrows=[];
let flying=false;
let quizActive=false;
const svg=document.getElementById('arrows-svg');
const internalLabels=document.getElementById('internal-labels');
const flyEl=document.getElementById('flying-pkt');
const sendArea=document.getElementById('send-area');
const sendBtn=document.getElementById('send-btn');
const quizOverlay=document.getElementById('quiz-overlay');

function updateSendArea(){
  if(phase>=steps.length){sendArea.style.display='none';return;}
  const st=steps[phase];
  document.getElementById('step-info').textContent=st.info;
  sendBtn.textContent=`📡 Send: ${st.label}`;
  sendBtn.style.background=st.color;
  sendBtn.style.color=st.color==='#f59e0b'||st.color==='#fbbf24'?'#111':'#fff';
}

function sendPacket(){
  if(flying||quizActive||phase>=steps.length) return;
  const step=steps[phase];
  if(step.from===step.to){
    // internal
    addInternalArrow(step,phase);
    phase++;
    showQuiz(step.id);
    return;
  }
  flying=true;
  sendBtn.disabled=true;
  const fromX=step.from==='client'?CLIENT_X:SERVER_X;
  const toX=step.to==='client'?CLIENT_X:SERVER_X;
  const y=80+phase*28;
  flyEl.style.display='block';
  flyEl.style.background=step.color;
  flyEl.style.color=(step.color==='#f59e0b'||step.color==='#fbbf24')?'#111':'#111';
  flyEl.textContent='📦 '+step.label;
  flyEl.style.top=(y-14)+'px';
  let prog=0;
  const anim=()=>{
    prog=Math.min(1,prog+0.03);
    const cx=fromX+(toX-fromX)*prog;
    flyEl.style.left=(cx-28)+'px';
    if(prog<1){requestAnimationFrame(anim);}
    else{
      flyEl.style.display='none';
      addArrow(fromX,toX,y,step,arrows.length);
      arrows.push({...step,fromX,toX,y});
      flying=false; sendBtn.disabled=false;
      phase++;
      showQuiz(step.id);
    }
  };
  requestAnimationFrame(anim);
}

function addArrow(fx,tx,y,step,idx){
  const markerId='arr'+idx;
  const marker=document.createElementNS('http://www.w3.org/2000/svg','marker');
  marker.setAttribute('id',markerId); marker.setAttribute('markerWidth','6');
  marker.setAttribute('markerHeight','6'); marker.setAttribute('refX','5');
  marker.setAttribute('refY','3'); marker.setAttribute('orient','auto');
  const path=document.createElementNS('http://www.w3.org/2000/svg','path');
  path.setAttribute('d','M0,0 L6,3 L0,6 Z'); path.setAttribute('fill',step.color);
  marker.appendChild(path);
  let defs=svg.querySelector('defs');
  if(!defs){defs=document.createElementNS('http://www.w3.org/2000/svg','defs');svg.appendChild(defs);}
  defs.appendChild(marker);
  const line=document.createElementNS('http://www.w3.org/2000/svg','line');
  line.setAttribute('x1',fx); line.setAttribute('y1',y);
  line.setAttribute('x2',tx); line.setAttribute('y2',y);
  line.setAttribute('stroke',step.color); line.setAttribute('stroke-width','2');
  line.setAttribute('marker-end','url(#'+markerId+')');
  svg.appendChild(line);
  const text=document.createElementNS('http://www.w3.org/2000/svg','text');
  text.setAttribute('x',(fx+tx)/2); text.setAttribute('y',y-6);
  text.setAttribute('text-anchor','middle'); text.setAttribute('font-size','10');
  text.setAttribute('fill',step.color); text.setAttribute('font-weight','700');
  text.textContent=step.label;
  svg.appendChild(text);
}

function addInternalArrow(step,idx){
  const div=document.createElement('div');
  div.className='internal-label';
  div.style.left=(SERVER_X-110)+'px';
  div.style.top=(68+idx*28)+'px';
  div.style.color=step.color;
  div.style.fontWeight='700';
  div.textContent='⚙️ '+step.label;
  internalLabels.appendChild(div);
}

function showQuiz(stepId){
  quizActive=true;
  sendArea.style.display='none';
  const qz=quizzes[stepId];
  document.getElementById('quiz-q').textContent=qz.q;
  const opts=document.getElementById('quiz-opts');
  opts.innerHTML='';
  qz.opts.forEach((opt,i)=>{
    const btn=document.createElement('button');
    btn.className='quiz-opt';
    btn.textContent=opt;
    btn.onclick=()=>answerQuiz(i,qz.correct,btn,opts);
    opts.appendChild(btn);
  });
  quizOverlay.style.display='flex';
}

function answerQuiz(chosen,correct,btn,opts){
  [...opts.children].forEach((b,i)=>{
    b.onclick=null;
    if(i===correct) b.classList.add('correct');
    else if(i===chosen) b.classList.add('wrong');
  });
  setTimeout(()=>{
    quizOverlay.style.display='none';
    quizActive=false;
    if(phase>=steps.length){
      sendArea.style.display='none';
      document.getElementById('win-banner').classList.add('show');
    } else {
      sendArea.style.display='block';
      updateSendArea();
    }
  }, chosen===correct?700:1400);
}

updateSendArea();
</script>
</body>
</html>