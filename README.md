<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ACCESS TERMINAL v2.3</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap');
  :root{--green:#00ff41;--darkgreen:#003b00;--amber:#ffb000;--red:#ff0033;--cyan:#00ffff;--bg:#000300}
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
  #terminal-wrap{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);z-index:10;width:min(560px,94vw)}
  .win95-bar{background:linear-gradient(90deg,#000080 0%,#1084d0 60%,#000080 100%);padding:4px 8px;display:flex;align-items:center;justify-content:space-between;border-top:2px solid #fff;border-left:2px solid #fff;border-right:2px solid #888;font-family:'VT323',monospace;font-size:18px;color:#fff;user-select:none}
  .win95-bar-title{display:flex;align-items:center;gap:8px}
  .win95-btns{display:flex;gap:3px}
  .win95-btn{width:18px;height:16px;background:#c0c0c0;border-top:2px solid #fff;border-left:2px solid #fff;border-right:2px solid #555;border-bottom:2px solid #555;font-size:11px;color:#000;display:flex;align-items:center;justify-content:center;cursor:pointer;font-weight:bold;font-family:'VT323',monospace}
  .terminal-body{background:rgba(0,3,0,.96);border-left:2px solid #00ff41;border-right:2px solid #00ff41;border-bottom:2px solid #00ff41;padding:24px;box-shadow:0 0 40px #00ff4133,inset 0 0 60px #00110033}
  .terminal-header{font-family:'VT323',monospace;font-size:13px;color:#00ff4188;margin-bottom:16px;line-height:1.5}
  .ascii-logo{font-family:'VT323',monospace;font-size:clamp(9px,2vw,13px);color:var(--green);text-shadow:0 0 8px var(--green);white-space:pre;line-height:1.1;margin-bottom:18px;animation:logo-flicker 8s ease-in-out infinite}
  @keyframes logo-flicker{0%,100%{opacity:1}92%{opacity:1}93%{opacity:.4}94%{opacity:1}97%{opacity:1}98%{opacity:.3}99%{opacity:1}}
  .prompt-line{display:flex;align-items:center;gap:10px;margin-top:20px}
  .prompt-symbol{font-family:'VT323',monospace;font-size:22px;color:var(--green);text-shadow:0 0 8px var(--green);white-space:nowrap}
  #password-input{flex:1;background:transparent;border:none;border-bottom:2px solid var(--green);color:var(--green);font-family:'Share Tech Mono',monospace;font-size:20px;outline:none;caret-color:var(--green);text-shadow:0 0 8px var(--green);letter-spacing:6px;padding:4px 0}
  #password-input::placeholder{color:#00ff4133;letter-spacing:2px}
  #status-line{margin-top:14px;font-family:'VT323',monospace;font-size:18px;min-height:24px;transition:all .3s}
  .status-error{color:var(--red);text-shadow:0 0 8px var(--red);animation:shake .4s ease}
  .status-ok{color:var(--green);text-shadow:0 0 12px var(--green)}
  .status-wait{color:var(--amber);text-shadow:0 0 8px var(--amber)}
  @keyframes shake{0%,100%{transform:translateX(0)}20%{transform:translateX(-8px)}40%{transform:translateX(8px)}60%{transform:translateX(-6px)}80%{transform:translateX(6px)}}
  #glitch-overlay{display:none;position:fixed;top:0;left:0;width:100%;height:100%;z-index:20;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(255,0,51,.08) 0px,rgba(255,0,51,.08) 1px,transparent 1px,transparent 4px);animation:glitch-flash .4s steps(2) forwards}
  @keyframes glitch-flash{0%{opacity:1;transform:skewX(0)}25%{opacity:.8;transform:skewX(-2deg) translateX(4px)}50%{opacity:1;transform:skewX(1deg) translateX(-3px)}75%{opacity:.6;transform:skewX(-1deg)}100%{opacity:0}}
  #reveal-panel{display:none;animation:reveal-enter 1s ease forwards}
  @keyframes reveal-enter{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
  .reveal-separator{color:var(--green);font-family:'VT323',monospace;font-size:14px;letter-spacing:2px;margin:14px 0;text-shadow:0 0 6px var(--green);overflow:hidden;white-space:nowrap;animation:expand-line .8s ease forwards}
  @keyframes expand-line{from{max-width:0}to{max-width:100%}}
  .location-box{border:1px solid var(--green);padding:16px;margin-top:10px;position:relative;background:rgba(0,255,65,.04);box-shadow:0 0 20px #00ff4122,inset 0 0 20px #00ff4108}
  .location-box::before{content:'[ DECRYPTED ]';position:absolute;top:-10px;left:14px;background:var(--bg);padding:0 8px;font-family:'VT323',monospace;font-size:14px;color:var(--cyan);text-shadow:0 0 8px var(--cyan)}
  .location-label{font-family:'VT323',monospace;font-size:13px;color:#00ff4177;margin-bottom:6px;letter-spacing:3px}
  .location-value{font-family:'VT323',monospace;font-size:clamp(20px,4vw,30px);color:#fff;text-shadow:0 0 12px var(--cyan),0 0 24px var(--cyan);letter-spacing:2px;animation:location-pulse 2s ease-in-out infinite}
  @keyframes location-pulse{0%,100%{text-shadow:0 0 12px var(--cyan),0 0 24px var(--cyan)}50%{text-shadow:0 0 20px var(--cyan),0 0 50px var(--cyan),0 0 80px #fff}}
  .location-coords{font-family:'Share Tech Mono',monospace;font-size:12px;color:#00ff4177;margin-top:8px}
  .side-scroll{position:fixed;writing-mode:vertical-rl;font-family:'Share Tech Mono',monospace;font-size:10px;color:#00ff4133;z-index:3;pointer-events:none;white-space:nowrap;animation:scroll-down linear 20s infinite;top:-100%}
  .side-left{left:18px;animation-delay:0s}.side-right{right:18px;animation-delay:-10s}
  @keyframes scroll-down{from{top:-50%}to{top:130%}}
  .hex-overlay{position:fixed;top:0;left:0;width:100%;height:100%;z-index:1;pointer-events:none;opacity:.06;background-image:radial-gradient(circle,#00ff41 1px,transparent 1px);background-size:30px 30px}
  .boot-line{font-family:'Share Tech Mono',monospace;font-size:11px;color:#00ff4177;margin-bottom:2px}
  #attempt-counter{position:fixed;top:14px;right:14px;font-family:'VT323',monospace;font-size:14px;color:var(--amber);z-index:20;text-align:right;text-shadow:0 0 8px var(--amber)}
  #status-bar{position:fixed;bottom:0;left:0;right:0;background:linear-gradient(90deg,#000080,#1084d0 50%,#000080);padding:3px 12px;font-family:'VT323',monospace;font-size:15px;color:#fff;display:flex;justify-content:space-between;z-index:15;border-top:2px solid #fff}
  #pacman-bar{position:fixed;bottom:30px;left:0;z-index:4;pointer-events:none;display:flex;align-items:center;animation:pacman-run 12s linear infinite}
  @keyframes pacman-run{from{left:-80px}to{left:110vw}}
  .pacman-sprite{font-size:26px;animation:chomp .3s steps(2) infinite;filter:drop-shadow(0 0 6px #ffb000)}
  @keyframes chomp{50%{transform:scaleX(.6)}}
  .pellet-trail{display:flex;gap:18px;margin-left:6px}
  .pellet{width:6px;height:6px;background:#ffb000;border-radius:50%;box-shadow:0 0 6px #ffb000}
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
<div class="ghost">👻</div><div class="ghost">👻</div><div class="ghost">👻</div><div class="ghost">👻</div>
<div class="pac-dots" id="pac-dots"></div>
<div id="pacman-bar"><div class="pacman-sprite">ᗧ</div><div class="pellet-trail"><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div><div class="pellet"></div></div></div>
<div class="corner corner-tl" id="corner-tl"></div>
<div class="corner corner-tr" id="corner-tr"></div>
<div class="corner corner-bl" id="corner-bl"></div>
<div class="corner corner-br" id="corner-br"></div>
<div id="attempt-counter">ATTEMPTS: 0 / ∞</div>
<div id="terminal-wrap">
  <div class="win95-bar">
    <div class="win95-bar-title"><span>🔒</span><span>SECURE TERMINAL v2.3 — RESTRICTED ACCESS</span></div>
    <div class="win95-btns"><div class="win95-btn">_</div><div class="win95-btn">□</div><div class="win95-btn">✕</div></div>
  </div>
  <div class="terminal-body">
    <div class="ascii-logo"> ██████╗  █████╗  ██████╗    ███╗   ███╗ █████╗ ███╗
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
        <div class="location-value" id="location-text">YOUR LOCATION HERE</div>
        <div class="location-coords">48°51′24″N  2°21′08″E</div>
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
// ══ 🔧 EDIT THESE TWO ══
const SECRET_PASSWORD = "PACMAN";
const LOCATION_DISPLAY = "YOUR LOCATION HERE";
// ════════════════════════
let attempts = 0;
function updateClock(){const n=new Date();document.getElementById('sb-right').textContent=n.toLocaleTimeString('en-GB')+'  '+n.toLocaleDateString('en-GB')}
setInterval(updateClock,1000);updateClock();
(function(){
const canvas=document.getElementById('matrix-canvas');
const ctx=canvas.getContext('2d');
const chars='アイウエオカキクケコサシスセソタチツテトABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+-=[]{}|;<>?/\~`';
let cols,drops;
function resize(){canvas.width=window.innerWidth;canvas.height=window.innerHeight;cols=Math.floor(canvas.width/16);drops=Array(cols).fill(1)}
window.addEventListener('resize',resize);resize();
function draw(){
ctx.fillStyle='rgba(0,3,0,0.055)';ctx.fillRect(0,0,canvas.width,canvas.height);
ctx.font='14px "Share Tech Mono"';
for(let i=0;i<drops.length;i++){
const ch=chars[Math.floor(Math.random()chars.length)];
ctx.fillStyle=drops[i]%3===0?'#ffffff':'#00ff41';
ctx.fillText(ch,i16,drops[i]*14);
if(drops[i]*14>canvas.height&&Math.random()>.975)drops[i]=0;
drops[i]++;
}
}
setInterval(draw,40);
})();
document.getElementById('ring1').textContent='10110100111001010110110010011101001010110101001101010011001011010101001 '.repeat(8);
document.getElementById('ring2').textContent='ACCESS_DENIED::FIREWALL_ACTIVE::TRACE_ROUTE::PACKET_LOSS::ENCRYPTED:: '.repeat(6);
document.getElementById('ring3').textContent='ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ···ᗧ··· '.repeat(5);
const code='function decrypt(key){const h=[];for(let i=0;i<key.length;i++){h.push(key.charCodeAt(i).toString(16));}return h.join(":");} // WARNING: UNAUTHORIZED ACCESS IS PROHIBITED // 0xDEADBEEF 0xCAFEBABE // chmod 700 /root/secret.dat // gpg --decrypt --armor payload.asc // ssh -i id_rsa ghost@192.168.1.1 // openssl enc -aes-256-cbc -d -in secret.bin // ';
document.getElementById('side-left').textContent=code.repeat(3);
document.getElementById('side-right').textContent=code.split('').reverse().join('').repeat(3);
(function(){const c=document.getElementById('pac-dots');for(let i=0;i<40;i++){const d=document.createElement('div');d.className='dot';d.style.left=Math.random()*96+'%';d.style.top=Math.random()*90+'%';d.style.animationDelay=(Math.random()*3)+'s';d.style.animationDuration=(1.5+Math.random()*2)+'s';if(Math.random()>.7){d.style.width=d.style.height='10px';d.style.boxShadow='0 0 10px #ffb000,0 0 20px #ffb00066';}c.appendChild(d);}})();
function cycle(id,arr){let i=0;document.getElementById(id).textContent=arr[0];setInterval(()=>{document.getElementById(id).textContent=arr[i%arr.length];i++;},2200)}
cycle('corner-tl',['[SYS:ACTIVE]','[NODE:03]','[PING:12ms]','[CPU:07%]']);
cycle('corner-tr',['[ENCRYPT:ON]','[AES-256]','[KEY:????]','[AUTH:PEND]']);
cycle('corner-bl',['[MEM:128K]','[SWAP:ON]','[FS:EXT4]','[MOUNT:OK]']);
cycle('corner-br',['[NET:UP]','[PKTS:2049]','[ERR:0]','[SYNC:OK]']);
(function(){
const lines=['> Initializing PAC-MAN OS kernel 3.14...','> Loading ghost subsystem... [OK]','> Mounting /dev/maze... [OK]','> Decryption module v7.3 ready.','> WARNING: Unauthorized access will be logged.','> Enter passkey to decrypt payload ▌'];
const el=document.getElementById('boot-log');let i=0;
function addLine(){if(i>=lines.length)return;const div=document.createElement('div');div.className='boot-line';div.textContent='';el.appendChild(div);let j=0;const txt=lines[i];const t=setInterval(()=>{div.textContent=txt.slice(0,++j);if(j>=txt.length){clearInterval(t);i++;setTimeout(addLine,300);}},28);}
setTimeout(addLine,600);
})();
const input=document.getElementById('password-input');
const status=document.getElementById('status-line');
const glitch=document.getElementById('glitch-overlay');
const counter=document.getElementById('attempt-counter');
function triggerGlitch(){glitch.style.display='block';setTimeout(()=>{glitch.style.display='none';},450)}
function showStatus(msg,type){status.textContent=msg;status.className='status-'+type}
function revealLocation(){
document.getElementById('input-section').style.display='none';
const panel=document.getElementById('reveal-panel');panel.style.display='block';
const sep=document.getElementById('sep-line');let s='';let i2=0;
const t=setInterval(()=>{s+='═';sep.textContent=s;if(++i2>=58)clearInterval(t);},18);
const locEl=document.getElementById('location-text');
locEl.textContent='';let k=0;
setTimeout(()=>{const t2=setInterval(()=>{locEl.textContent+=LOCATION_DISPLAY[k];if(++k>=LOCATION_DISPLAY.length)clearInterval(t2);},60);},900);
document.getElementById('sb-left').textContent='🟡 DECRYPTED — ACCESS GRANTED';
}
input.addEventListener('keydown',function(e){
if(e.key!=='Enter')return;
const val=input.value.trim();if(!val)return;
attempts++;counter.textContent='ATTEMPTS: '+attempts+' / ∞';
if(val.toUpperCase()===SECRET_PASSWORD.toUpperCase()){
showStatus('> ACCESS GRANTED — DECRYPTING PAYLOAD...','ok');
input.disabled=true;setTimeout(revealLocation,1400);
} else {
triggerGlitch();
showStatus('> ACCESS DENIED — WRONG PASSKEY ['+val.toUpperCase()+']','error');
setTimeout(()=>{showStatus('> RE-ENTER PASSKEY ▌','wait');input.value='';},900);
}
});
setTimeout(()=>input.focus(),2000);
</script>
</body>
</html>
