---
permalink: /network/home
---

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Network Stack Escape Room</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:#0a0f1e;min-height:100vh;font-family:'Share Tech Mono',monospace;color:#e2e8f0;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px;}
  h1{font-family:'Orbitron',sans-serif;font-size:clamp(20px,4vw,32px);color:#fff;text-align:center;letter-spacing:2px;margin-bottom:8px;}
  .sub{color:#94a3b8;text-align:center;max-width:500px;font-size:13px;line-height:1.7;margin-bottom:28px;}
  .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:14px;max-width:700px;width:100%;margin-bottom:28px;}
  .card{background:#111827;border:2px solid #1f2937;border-radius:12px;padding:18px 16px;cursor:pointer;transition:all .2s;text-decoration:none;display:block;}
  .card:hover{border-color:#3b82f6;transform:translateY(-2px);box-shadow:0 8px 24px #3b82f633;}
  .card .icon{font-size:32px;margin-bottom:8px;}
  .card .lnum{font-family:'Orbitron',sans-serif;font-size:10px;color:#3b82f6;letter-spacing:2px;margin-bottom:4px;}
  .card .lname{color:#fff;font-size:13px;font-weight:700;}
  .card .layer{color:#6b7280;font-size:10px;margin-top:3px;}
  .start{background:#3b82f6;color:#fff;border:none;border-radius:10px;padding:14px 44px;cursor:pointer;font-family:'Orbitron',sans-serif;font-size:15px;letter-spacing:1px;font-weight:700;}
  .start:hover{background:#2563eb;}
  .tag{display:inline-block;background:#1e3a5f;border:1px solid #3b82f6;border-radius:20px;padding:2px 12px;font-size:10px;color:#60a5fa;margin-bottom:18px;letter-spacing:1px;}
</style>
</head>
<body>
<div class="tag">📡 OSI 7-LAYER GAME</div>
<h1>NETWORK STACK<br/>ESCAPE ROOM</h1>
<p class="sub">Help <strong style="color:#fbbf24">Mailman Max</strong> deliver packets from <strong style="color:#60a5fa">GitHub Pages</strong> to <strong style="color:#4ade80">AWS EC2 Flask</strong> through all 7 OSI layers!</p>
<div class="grid">
  <a class="card" href="/portfolio/network/1"><div class="icon">🔌</div><div class="lnum">LEVEL 1</div><div class="lname">Wire the Network</div><div class="layer">OSI Layer 1 · Physical</div></a>
  <a class="card" href="/portfolio/network/2"><div class="icon">📦</div><div class="lnum">LEVEL 2</div><div class="lname">Build the Frame</div><div class="layer">OSI Layer 2 · Data Link</div></a>
  <a class="card" href="/portfolio/network/3"><div class="icon">🏬</div><div class="lnum">LEVEL 3</div><div class="lname">Route the Packets</div><div class="layer">OSI Layer 3 · Network</div></a>
  <a class="card" href="/portfolio/network/4"><div class="icon">🔪</div><div class="lnum">LEVEL 4</div><div class="lname">Slice at the MTU</div><div class="layer">OSI Layer 4 · Transport</div></a>
  <a class="card" href="/portfolio/network/5"><div class="icon">📡</div><div class="lnum">LEVEL 5</div><div class="lname">TCP Handshake</div><div class="layer">OSI Layer 5 · Session</div></a>
  <a class="card" href="/portfolio/network/6"><div class="icon">🎁</div><div class="lnum">LEVEL 6</div><div class="lname">Wrap with TLS</div><div class="layer">OSI Layer 6 · Presentation</div></a>
  <a class="card" href="/portfolio/network/7"><div class="icon">🚗</div><div class="lnum">LEVEL 7</div><div class="lname">Neighborhood Delivery</div><div class="layer">OSI Layer 7 · Application</div></a>
</div>
<a href="/portfolio/network/1"><button class="start">🚚 START DELIVERING</button></a>
</body>
</html>