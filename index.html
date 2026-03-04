<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ACCESS TERMINAL v2.3</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap');
  :root{--green:#00ff41;--amber:#ffb000;--red:#ff0033;--cyan:#00ffff;--bg:#000300}
  *{margin:0;padding:0;box-sizing:border-box}
  body{background:var(--bg);color:var(--green);font-family:'Share Tech Mono',monospace;overflow:hidden;height:100vh;width:100vw;cursor:crosshair}
  #matrix-canvas{position:fixed;top:0;left:0;z-index:0;opacity:.55}
  .orbit-container{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);z-index:1;pointer-events:none}
  .orbit-ring{position:absolute;top:50%;left:50%;transform-origin:center;animation:spin linear infinite;white-space:nowrap;font-family:'VT323',monospace;letter-spacing:3px}
  .ring1{width:700px;height:700px;margin:-350px 0 0 -350px;font-size:11px;color:#00ff4133;animation-duration:40s}
  .ring2{width:550px;height:550px;margin:-275px 0 0 -275px;font-size:10px;color:#00ffff22;animation-duration:28s;animation-direction:reverse}
  .ring3{width:420px;height:420px;margin:-210px 0 0 -210px;font-size:9px;color:#ffb00033;animation-duration:18s}
  @keyframes spin{from{transform:rotate(0deg)}to{transform:rotate(360deg)}}
  #scanlines{position:fixed;top:0;left:0;width:100%;height:100%;z-index:2;pointer-events:none;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,.15) 2px,rgba(0,0,0,.15) 4px)}
  .corner{position:fixed;font-family:'VT323',monospace;font-size:12px;color:#00ff4155;z-index:3;pointer-events:none;animation:blink 3s step-end infinite}
  .corner-tl{top:10px;left:10px}.corner-tr{top:10px;right:10px;text-align:right}.corner-bl{bottom:32px;left:10px}.corner-br{bottom:32px;right:10px;text-align:right}
  @keyframes blink{0%,100%{opacity:1}50%{opacity:.2}}
  .ghost{position:fixed;font-size:22px;z-index:3;pointer-events:none;filter:drop-shadow(0 0 6px currentColor);animation:ghost-wander linear infinite}
  .ghost:nth-child(1){color:#ff0033;top:12%;animation-duration:18s;animation-delay:0s}
  .ghost:nth-child(2){color:#ffb8ff;top:72%;animation-duration:24s;animation-delay:-7s}
  .ghost:nth-child(3){color:#00ffff;top:38%;animation-duration:20s;animation-delay:-12s}
  .ghost:nth-child(4){color:#ffb000;top:85%;animation-duration:15s;animation-delay:-4s}
  @keyframes ghost-wander{0%{left:-5%;transform:scaleX(1)}49%{left:103%;transform:scaleX(1)}50%{left:103%;transform:scaleX(-1)}99%{left:-5%;transform:scaleX(-1)}100%{left:-5%;transform:scaleX(1)}}
  .pac-dots{position:fixed;z-index:3;pointer-events:none;top:0;left:0;width:100%;height:100%}
  .dot{position:absolute;width:5px;height:5px;border-radius:50%;background:#ffb000;box-shadow:0 0 6px #ffb000;animation:dot-pulse 2s ease-in-out infinite}
  @keyframes dot-pulse{0%,100%{transform:scale(1);opacity:.6}50%{transform:scale(1.6);opacity:1}}
  #terminal-wrap{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);z-index:10;width:min(580px,94vw)}
  .win95-bar{background:linear-gradient(90deg,#000080 0%,#1084d0 60%,#000080 100%);padding:5px 8px;display:flex;align-items:center;justify-content:space-between;border-top:2px solid #fff;border-left:2px solid #fff;border-right:2px solid #888;font-family:'VT323',monospace;font-size:18px;color:#fff;user-select:none}
  .win95-bar-title{display:flex;align-items:center;gap:8px}
  .win95-btns{display:flex;gap:3px}
  .win95-btn{width:18px;height:16px;background:#c0c0c0;border-top:2px solid #fff;border-left:2px solid #fff;border-right:2px solid #555;border-bottom:2px solid #555;font-size:11px;color:#000;display:flex;align-items:center;justify-content:center;cursor:pointer;font-weight:bold;font-family:'VT323',monospace}
  .terminal-body{background:rgba(0,3,0,.97);border-left:2px solid #00ff41;border-right:2px solid #00ff41;border-bottom:2px solid #00ff41;padding:24px;box-shadow:0 0 40px #00ff4133,inset 0 0 60px #00110033}
  .ascii-logo{font-family:'VT323',monospace;font-size:clamp(8px,1.8vw,13px);color:var(--green);text-shadow:0 0 8px var(--green);white-space:pre;line-height:1.1;margin-bottom:18px;animation:logo-flicker 8s ease-in-out infinite}
  @keyframes logo-flicker{0%,100%{opacity:1}92%{opacity:1}93%{opacity:.4}94%{opacity:1}97%{opacity:1}98%{opacity:.3}99%{opacity:1}}
  .terminal-header{font-family:'VT323',monospace;font-size:13px;color:#00ff4188;margin-bottom:16px;line-height:1.6}
  .boot-line{font-family:'Share Tech Mono',monospace;font-size:11px;color:#00ff4177;margin-bottom:2px}
  .prompt-line{display:flex;align-items:center;gap:10px;margin-top:20px}
  .prompt-symbol{font-family:'VT323',monospace;font-size:22px;color:var(--green);text-shadow:0 0 8px var(--green);white-space:nowrap}
  #password-input{flex:1;background:transparent;border:none;border-bottom:2px solid var(--green);color:var(--green);font-family:'Share Tech Mono',monospace;font-size:20px;outline:none;caret-color:var(--green);text-shadow:0 0 8px var(--green);letter-spacing:6px;padding:4px 0}
  #password-input::placeholder{color:#00ff4133;letter-spacing:2px}
  #status-line{margin-top:14px;font-family:'VT323',monospace;font-size:18px;min-height:24px}
  .status-error{color:var(--red);text-shadow:0 0 8px var(--red);animation:shake .4s ease}
  .status-ok{color:var(--green);text-shadow:0 0 12px var(--green)}
  .status-wait{color:var(--amber);text-shadow:0 0 8px var(--amber)}
  @keyframes shake{0%,100%{transform:translateX(0)}20%{transform:translateX(-8px)}40%{transform:translateX(8px)}60%{transform:translateX(-6px)}80%{transform:translateX(6px)}}
  #glitch-overlay{display:none;position:fixed;top:0;left:0;width:100%;height:100%;z-index:20;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(255,0,51,.1) 0px,rgba(255,0,51,.1) 1px,transparent 1px,transparent 4px);animation:glitch-flash .45s steps(2) forwards}
  @keyframes glitch-flash{0%{opacity:1;transform:skewX(0)}25%{opacity:.8;transform:skewX(-2deg) translateX(5px)}50%{opacity:1;transform:skewX(1.5deg) translateX(-4px)}75%{opacity:.6;transform:skewX(-1deg)}100%{opacity:0}}
  #reveal-panel{display:none;animation:reveal-enter 1s ease forwards}
  @keyframes reveal-enter{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
  .reveal-separator{color:var(--green);font-family:'VT323',monospace;font-size:14px;letter-spacing:2px;margin:16px 0 10px;text-shadow:0 0 6px var(--green);overflow:hidden;white-space:nowrap}
  .location-box{border:1px solid var(--green);padding:18px;margin-top:6px;position:relative;background:rgba(0,255,65,.04);box-shadow:0 0 24px #00ff4122,inset 0 0 20px #00ff4108}
  .location-box::before{content:'[ DECRYPTED PAYLOAD ]';position:absolute;top:-10px;left:14px;background:var(--bg);padding:0 8px;font-family:'VT323',monospace;font-size:14px;color:var(--cyan);text-shadow:0 0 8px var(--cyan)}
  .location-label{font-family:'VT323',monospace;font-size:13px;color:#00ff4177;margin-bottom:8px;letter-spacing:3px}
  .location-value{font-family:'VT323',monospace;font-size:clamp(22px,4vw,32px);color:#fff;text-shadow:0 0 12px var(--cyan),0 0 24px var(--cyan);letter-spacing:2px;animation:location-pulse 2s ease-in-out infinite;word-break:break-word}
  @keyframes location-pulse{0%,100%{text-shadow:0 0 12px var(--cyan),0 0 24px var(--cyan)}50%{text-shadow:0 0 22px var(--cyan),0 0 55px var(--cyan),0 0 90px #fff}}
  .location-coords{font-family:'Share Tech Mono',monospace;font-size:12px;color:#00ff4166;margin-top:10px}
  .side-scroll{position:fixed;writing-mode:vertical-rl;font-family:'Share Tech Mono',monospace;font-size:10px;color:#00ff4130;z-index:3;pointer-events:none;white-space:nowrap;animation:scroll-down linear 22s infinite}
  .side-left{left:16px;top:-60%;animation-delay:0s}.side-right{right:16px;top:-60%;animation-delay:-11s}
  @keyframes scroll-down{from{top:-60%}to{top:130%}}
  .hex-overlay{position:fixed;top:0;left:0;width:100%;height:100%;z-index:1;pointer-events:none;opacity:.05;background-image:radial-gradient(circle,#00ff41 1px,transparent 1px);background-size:30px 30px}
  #attempt-counter{position:fixed;top:12px;right:12px;font-family:'VT323',monospace;font-size:14px;color:var(--amber);z-index:20;text-shadow:0 0 8px var(--amber)}
  #status-bar{position:fixed;bottom:0;left:0;right:0;background:linear-gradient(90deg,#000080,#1084d0 50%,#000080);padding:3px 12px;font-family:'VT323',monospace;font-size:15px;color:#fff;display:flex;justify-content:space-between;z-index:15;border-top:2px solid #fff}
  #pacman-bar{position:fixed;bottom:28px;left:0;z-index:4;pointer-events:none;display:flex;align-items:center;animation:pacman-run 13s linear infinite}
  @keyframes pacman-run{from{left:-100px}to{left:110vw}}
  .pacman-sprite{font-size:28px;filter:drop-shadow(0 0 8px #ffb000);animation:chomp .25s steps(2) infinite}
  @keyframes chomp{50%{transform:scaleX(.55)}}
  .pellet-trail{display:flex;gap:20px;margin-left:8px}
  .pellet{width:7px;height:7px;background:#ffb000;border-radius:50%;box-shadow:0 0 8px #ffb000}
</style>
</head>
<body>

<canvas id="matrix-canvas"></canvas>
<div id="scanlines"></div>
<div class="hex-overlay"></div>
<div id="glitch-overlay"></div>

<div class="orbit-container">
  <div class="orbit-ring ring1" id="ring1"></div>
  <div class="orbit-ring ring2" id="ring2"></div>
  <div class="orbit-ring ring3" id="ring3"></div>
</div>

<div class="side-scroll side-left" id="side-left"></div>
<div class="side-scroll side-right" id="side-right"></div>

<div class="ghost">👻</div>
<div class="ghost">👻</div>
<div class="ghost">👻</div>
<div class="ghost">👻</div>

<div class="pac-dots" id="pac-dots"></div>

<div id="pacman-bar">
  <div class="pacman-sprite">ᗧ</div>
  <div class="pellet-trail">
    <div class="pellet"></div><div class="pellet"></div><div class="pellet"></div>
    <div class="pellet"></div><div class="pellet"></div><div class="pellet"></div>
    <div class="pellet"></div><div class="pellet"></div><div class="pellet"></div>
  </div>
</div>

<div class="corner corner-tl" id="corner-tl">[SYS:ACTIVE]</div>
<div class="corner corner-tr" id="corner-tr">[ENCRYPT:ON]</div>
<div class="corner corner-bl" id="corner-bl">[MEM:128K]</div>
<div class="corner corner-br" id="corner-br">[NET:UP]</div>

<div id="attempt-counter">ATTEMPTS: 0 / ∞</div>

<div id="terminal-wrap">
  <div class="win95-bar">
    <div class="win95-bar-title">
      <span>🔒</span>
      <span>SECURE TERMINAL v2.3 — RESTRICTED ACCESS</span>
    </div>
    <div class="win95-btns">
      <div class="win95-btn">_</div>
      <div class="win95-btn">□</div>
      <div class="win95-btn">✕</div>
    </div>
  </div>
  <div class="terminal-body">
    <div class="ascii-logo" id="ascii-logo"> ██████╗  █████╗  ██████╗    ███╗   ███╗ █████╗ ███╗
 ██╔══██╗██╔══██╗██╔════╝    ████╗ ████║██╔══██╗████╗
 ██████╔╝███████║██║         ██╔████╔██║███████║██╔██╗
 ██╔═══╝ ██╔══██║██║         ██║╚██╔╝██║██╔══██║██║╚██╗
 ██║     ██║  ██║╚██████╗    ██║ ╚═╝ ██║██║  ██║██║ ╚██╗
 ╚═╝     ╚═╝  ╚═╝ ╚═════╝   ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝</div>
    <div class="terminal-header" id="boot-log"></div>
    <div id="input-section">
      <div class="prompt-line">
        <span class="prompt-symbol">root@PAC-MAN:~#&nbsp;</span>
        <input type="password" id="password-input" placeholder="ENTER PASSKEY..." autocomplete="off" spellcheck="false" maxlength="32"/>
      </div>
      <div id="status-line"></div>
    </div>
    <div id="reveal-panel">
      <div class="reveal-separator" id="sep-line"></div>
      <div class="location-box">
        <div class="location-label">▶ DECRYPTED COORDINATES</div>
        <!-- =============================================  -->
        <!--  The location value is set by JS below        -->
        <!-- =============================================  -->
        <div class="location-value" id="location-text"></div>
        <div class="location-coords" id="location-coords"></div>
      </div>
    </div>
  </div>
</div>

<div id="status-bar">
  <span id="sb-left">🟢 SYSTEM ONLINE</span>
  <span>PAC-MAN OS v95.4 — KERNEL 3.14</span>
  <span id="sb-right"></span>
</div>

<script>
// ╔══════════════════════════════════════════════╗
// ║  🔧 EDIT THESE THREE LINES ONLY              ║
const SECRET_PASSWORD  = "PACMAN";
const LOCATION_TEXT    = "Piazza del Duomo, Milano";
const LOCATION_COORDS  = "45°27′51″N  9°11′17″E";
// ╚══════════════════════════════════════════════╝

let attempts = 0;

// ── Clock ──
function updateClock() {
  const n = new Date();
  document.getElementById('sb-right').textContent =
    n.toLocaleTimeString('en-GB') + '   ' + n.toLocaleDateString('en-GB');
}
setInterval(updateClock, 1000);
updateClock();

// ── Matrix rain ──
(function () {
  const canvas = document.getElementById('matrix-canvas');
  const ctx = canvas.getContext('2d');
  const chars = 'アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+-=[]{}|;<>?/\\~`';
  let cols, drops;
  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    cols = Math.floor(canvas.width / 16);
    drops = Array(cols).fill(1);
  }
  window.addEventListener('resize', resize);
  resize();
  setInterval(function () {
    ctx.fillStyle = 'rgba(0,3,0,0.055)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.font = '14px "Share Tech Mono"';
    for (let i = 0; i < drops.length; i++) {
      const ch = chars[Math.floor(Math.random() * chars.length)];
      ctx.fillStyle = drops[i] % 3 === 0 ? '#ffffff' : '#00ff41';
      ctx.fillText(ch, i * 16, drops[i] * 14);
      if (drops[i] * 14 > canvas.height && Math.random() > 0.975) drops[i] = 0;
      drops[i]++;
    }
  }, 40);
})();

// ── Orbiting rings ──
document.getElementById('ring1').textContent =
  '10110100111001010110110010011101001010110101001101010011001011010101001 '.repeat(8);
document.getElementById('ring2').textContent =
  'ACCESS_DENIED :: FIREWALL_ACTIVE :: TRACE_ROUTE :: PACKET_LOSS :: ENCRYPTED :: GHOST_DETECTED :: '.repeat(5);
document.getElementById('ring3').textContent =
  'ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · ᗧ · · · '.repeat(4);

// ── Side scrolling code ──
const sideCode = 'function decrypt(key){const h=[];for(let i=0;i<key.length;i++){h.push(key.charCodeAt(i).toString(16));}return h.join(":");} // WARNING: UNAUTHORIZED ACCESS IS PROHIBITED AND WILL BE PROSECUTED // 0xDEADBEEF 0xCAFEBABE 0xFACEFEED // chmod 700 /root/secret.dat // sudo gpg --decrypt --armor payload.asc // ssh -i id_rsa ghost@192.168.0.1 // netstat -tulpn | grep LISTEN // iptables -A INPUT -p tcp --dport 22 -j DROP // find / -name "*.key" 2>/dev/null // openssl enc -aes-256-cbc -d -in secret.bin -out plain.txt // ';
document.getElementById('side-left').textContent = sideCode.repeat(3);
document.getElementById('side-right').textContent = sideCode.split('').reverse().join('').repeat(3);

// ── Pac-Man dots ──
(function () {
  const c = document.getElementById('pac-dots');
  for (let i = 0; i < 45; i++) {
    const d = document.createElement('div');
    d.className = 'dot';
    d.style.left = (Math.random() * 96) + '%';
    d.style.top  = (Math.random() * 90) + '%';
    d.style.animationDelay    = (Math.random() * 3) + 's';
    d.style.animationDuration = (1.5 + Math.random() * 2) + 's';
    if (Math.random() > 0.7) {
      d.style.width = d.style.height = '10px';
      d.style.boxShadow = '0 0 10px #ffb000, 0 0 22px #ffb00055';
    }
    c.appendChild(d);
  }
})();

// ── Corner cycling text ──
function cycleTxt(id, arr) {
  let i = 0;
  document.getElementById(id).textContent = arr[0];
  setInterval(function () { document.getElementById(id).textContent = arr[i++ % arr.length]; }, 2400);
}
cycleTxt('corner-tl', ['[SYS:ACTIVE]', '[NODE:03]',   '[PING:12ms]', '[CPU:07%]']);
cycleTxt('corner-tr', ['[ENCRYPT:ON]', '[AES-256]',   '[KEY:????]',  '[AUTH:PEND]']);
cycleTxt('corner-bl', ['[MEM:128K]',   '[SWAP:ON]',   '[FS:EXT4]',   '[MOUNT:OK]']);
cycleTxt('corner-br', ['[NET:UP]',     '[PKTS:2049]', '[ERR:0]',     '[SYNC:OK]']);

// ── Boot log typewriter ──
(function () {
  const lines = [
    '> Initializing PAC-MAN OS kernel 3.14...',
    '> Loading ghost subsystem............. [OK]',
    '> Mounting /dev/maze.................. [OK]',
    '> AES-256 decryption module v7.3...... [READY]',
    '> WARNING: Unauthorized access will be traced.',
    '> Enter passkey to decrypt payload ▌',
  ];
  const el = document.getElementById('boot-log');
  let i = 0;
  function addLine() {
    if (i >= lines.length) return;
    const div = document.createElement('div');
    div.className = 'boot-line';
    div.textContent = '';
    el.appendChild(div);
    let j = 0;
    const txt = lines[i];
    const t = setInterval(function () {
      div.textContent = txt.slice(0, ++j);
      if (j >= txt.length) { clearInterval(t); i++; setTimeout(addLine, 280); }
    }, 26);
  }
  setTimeout(addLine, 500);
})();

// ── Password logic ──
const input   = document.getElementById('password-input');
const statusEl = document.getElementById('status-line');
const glitch  = document.getElementById('glitch-overlay');
const counter = document.getElementById('attempt-counter');

function triggerGlitch() {
  glitch.style.animation = 'none';
  glitch.style.display = 'block';
  void glitch.offsetWidth; // reflow
  glitch.style.animation = 'glitch-flash .45s steps(2) forwards';
  setTimeout(function () { glitch.style.display = 'none'; }, 500);
}

function setStatus(msg, type) {
  statusEl.textContent = msg;
  statusEl.className = 'status-' + type;
}

function revealLocation() {
  document.getElementById('input-section').style.display = 'none';
  const panel = document.getElementById('reveal-panel');
  panel.style.display = 'block';

  // Animate separator line
  const sep = document.getElementById('sep-line');
  let s = ''; let k = 0;
  const t1 = setInterval(function () {
    s += '═'; sep.textContent = s;
    if (++k >= 56) clearInterval(t1);
  }, 16);

  // Typewrite location name
  const locEl = document.getElementById('location-text');
  locEl.textContent = '';
  let j = 0;
  setTimeout(function () {
    const t2 = setInterval(function () {
      locEl.textContent += LOCATION_TEXT[j];
      if (++j >= LOCATION_TEXT.length) clearInterval(t2);
    }, 55);
  }, 850);

  // Show coords after name finishes
  setTimeout(function () {
    document.getElementById('location-coords').textContent = LOCATION_COORDS;
  }, 850 + LOCATION_TEXT.length * 55 + 400);

  document.getElementById('sb-left').textContent = '🟡 DECRYPTED — ACCESS GRANTED';
}

input.addEventListener('keydown', function (e) {
  if (e.key !== 'Enter') return;
  const val = input.value.trim();
  if (!val) return;

  attempts++;
  counter.textContent = 'ATTEMPTS: ' + attempts + ' / ∞';

  if (val.toUpperCase() === SECRET_PASSWORD.toUpperCase()) {
    setStatus('> ACCESS GRANTED — DECRYPTING PAYLOAD...', 'ok');
    input.disabled = true;
    setTimeout(revealLocation, 1400);
  } else {
    triggerGlitch();
    setStatus('> ACCESS DENIED — WRONG PASSKEY [' + val.toUpperCase() + ']', 'error');
    setTimeout(function () {
      setStatus('> RE-ENTER PASSKEY ▌', 'wait');
      input.value = '';
    }, 950);
  }
});

// Auto-focus after boot
setTimeout(function () { input.focus(); }, 2200);
</script>
</body>
</html>
