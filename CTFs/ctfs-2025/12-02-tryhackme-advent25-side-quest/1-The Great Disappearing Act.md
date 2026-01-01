
Can you help Hopper escape his wrongful imprisonment in HopSec asylum?


## Task 1 - Introduction

### Set up your virtual environment

To successfully complete this room, you'll need to set up your virtual environment. This involves starting both your AttackBox (if you're not using your VPN) and Target Machines, ensuring you're equipped with the necessary tools and access to tackle the challenges ahead.

### Hopper the Court Jester 

**Once upon a time, there was a red-teaming mastermind turned court jester… our story begins with Hopper.** Once feared as the ruthless Head of the Red Team Bunny Battalion, Hopper rose to the rank of Colonel with dizzying speed. The promotion filled him with such exhilaration and such hunger for more that it consumed his every thought. His soldiers mistook his growing twitch for stress and began calling him “Colonel Panic”, but the truth was far more dangerous: the twitch came from his obsession with power, not fear.  
  
In those days, Hopper had already played a crucial, though conveniently forgotten, role in the earliest whispers of the Wareville siege. Buried beneath secrecy and denied by the crown, those first experiments in breaching new digital frontiers were Hopper’s design. But when the King began distancing himself from the truth, Hopper’s contributions were quietly erased from history, and his fall from grace accelerated. We now find Hopper in his prison cell in HopSec Asylum.  
  
This challenge is unlocked by finding the SideQuest key in [Advent of Cyber Day 1](https://tryhackme.com/jr/linuxcli-aoc2025-o1fpqkvxti). If you have been savvy enough to find it, you can unlock the machine by visiting `10.64.128.155:21337` and entering your key. Happy SideQuesting!


### Desbloqueo 

http://10.65.169.88:21337/

```
curl -X POST http://10.64.128.155:21337/unlock \
  -H "Content-Type: application/json" \
  -d '{"k":"now_you_see_me"}' \
  -c cookies.txt \
  -v
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 10.64.128.155:21337...
* Connected to 10.64.128.155 (10.64.128.155) port 21337
> POST /unlock HTTP/1.1
> Host: 10.64.128.155:21337
> User-Agent: curl/8.5.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 22
>
< HTTP/1.1 200 OK
< Server: Werkzeug/3.0.1 Python/3.12.3
< Date: Mon, 01 Dec 2025 21:55:36 GMT
< Content-Type: text/html; charset=utf-8
< Content-Length: 15
< Connection: close
<
* Closing connection
{"status":"ok"}#

```


## Prison Escape Challenge

You now take control of Hopper, with one ultimate goal. Free yourself from this wrongful imprisonment. To do this, you must follow Hopper's 5-step escape plan:

### 1. Unlock Hopper’s Cell

Your escape begins in the Cells and Storage area. Hopper is locked inside, and the door is secured with a digital lock. Your first task is to access the cell controls and unlock his door. Once Hopper is free, you can begin moving toward the lobby.

### 2. Move Through the Lobby

With the cell unlocked, head straight ahead into the lobby. This area connects the different blocks of the facility. Cameras are active, so stay alert. Your objective is to reach the Psych Ward entrance on the east side of the lobby.

### 3. Bypass the Psych Ward Keypad

The Psych Ward is protected by a keypad system. You must identify the correct code or exploit the keypad to continue. Once the keypad is bypassed, you will gain access to the Psych Ward Exit hallway.

### 4. Reach the Main Corridor

From the Psych Ward Exit you can move south and loop around into the Main Corridor. This is the final section of the escape route. The last challenge awaits here, and completing it will open the final exit door.

### 5. Escape the Facility

Solve the final challenge in the Main Corridor and make your way toward the exit marked on the map. Once the door opens, Hopper is free, and the escape is complete.

https://tryhackme.com/room/sq1-aoc2025-FzPnrt2SAu

### nmap
```
nmap -n -Pn -sV --min-rate 9000 -vv -p- 10.65.169.88
Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-01 17:30 CST
	 
Scanned at 2025-12-01 17:30:12 CST for 117s
Not shown: 65524 closed tcp ports (reset)
PORT      STATE SERVICE     REASON         VERSION
22/tcp    open  ssh         syn-ack ttl 62 OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http        syn-ack ttl 62 nginx 1.24.0 (Ubuntu)
8000/tcp  open  http-alt    syn-ack ttl 61
8080/tcp  open  http        syn-ack ttl 62 SimpleHTTPServer 0.6 (Python 3.12.3)
9001/tcp  open  tor-orport? syn-ack ttl 61
13400/tcp open  http        syn-ack ttl 62 nginx 1.24.0 (Ubuntu)
13401/tcp open  http        syn-ack ttl 62 Werkzeug httpd 3.1.3 (Python 3.12.3)
13402/tcp open  http        syn-ack ttl 62 nginx 1.24.0 (Ubuntu)
13403/tcp open  unknown     syn-ack ttl 62
13404/tcp open  unknown     syn-ack ttl 62
21337/tcp open  http        syn-ack ttl 62 Werkzeug httpd 3.0.1 (Python 3.12.3)

  
```


### Puerto 80
```  
cat puerto80.html         
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>HopSec Asylum - Security Console</title>
<style>
body{
  margin:0;
  padding:0;
  min-height:100vh;
  font-family:"Lucida Console",Monaco,monospace;
  background:radial-gradient(circle at 30% 30%,#0a2626 0%,#041414 80%);
  color:#d9fff9;
}
.titlebar{
  background:linear-gradient(180deg,#2aaea0 0%,#04524c 100%);
  color:#fff;
  padding:6px 10px;
  font-weight:bold;
  text-shadow:1px 1px 0 #033;
  border-bottom:2px solid #0c6057;
}
.window{
  width:480px;
  margin:8% auto;
  border:2px solid #67d6c9;
  background:linear-gradient(180deg,#094443 0%,#021c1c 100%);
  box-shadow:0 0 15px #0ef5dc66,inset 0 0 6px #000;
  border-radius:4px;
}
.content{
  padding:20px;
  text-align:center;
}
label{
  display:block;
  margin-top:10px;
}
input{
  width:80%;
  padding:6px;
  background:#011b1b;
  color:#bdf2ea;
  border:2px inset #17786e;
  outline:none;
}
button{
  margin-top:16px;
  padding:6px 20px;
  font-weight:bold;
  background:linear-gradient(180deg,#24ccb9,#0a665c);
  border:2px outset #0a665c;
  cursor:pointer;
  color:#022;
}
button:hover{
  filter:brightness(1.2);
}
#mapScreen{
  display:none;
  width:92%;
  max-width:980px;
  margin:4% auto 60px;
  background:linear-gradient(180deg,#073333,#011818);
  border:2px solid #67d6c9;
  border-radius:4px;
  box-shadow:0 0 20px #0ef5dc55;
  padding:12px;
}
.map-wrap{
  position:relative;
  width:100%;
  padding-top:80%;
  border:1px solid #18a298;
  border-radius:3px;
  overflow:hidden;
  box-shadow:inset 0 0 30px #000a;
}
.map-wrap svg{
  position:absolute;
  inset:0;
  width:100%;
  height:100%;
  display:block;
}
.iconspot{
  --x:50%;
  --y:50%;
  position:absolute;
  left:var(--x);
  top:var(--y);
  transform:translate(-50%,-50%);
  width:44px;
  height:44px;
  background:transparent;
  border:none;
  padding:0;
  cursor:pointer;
  filter:drop-shadow(0 0 6px #00ffd966);
}
.iconspot img{
  width:44px;
  height:44px;
}
.keybtn img{
  filter:drop-shadow(0 0 6px #ffdd4a);
}
.keybtn.unlocked img{
  filter:hue-rotate(80deg) saturate(2) drop-shadow(0 0 7px #4dff4d);
}
.iconspot[data-label]::after{
  content:attr(data-label);
  position:absolute;
  left:50%;
  top:-10px;
  transform:translate(-50%,-100%);
  background:#013d3d;
  color:#c9ffef;
  border:1px solid #18a298;
  padding:3px 6px;
  font-size:11px;
  white-space:nowrap;
  border-radius:3px;
  opacity:0;
  pointer-events:none;
  transition:.15s;
}
.iconspot:hover::after{
  opacity:1;
}
.modal-bg{
  display:none;
  position:fixed;
  inset:0;
  background:rgba(0,0,0,0.7);
  align-items:center;
  justify-content:center;
  z-index:900;
}
.modal{
  background:linear-gradient(180deg,#094443,#032121);
  border:2px solid #58c8bc;
  padding:20px;
  border-radius:4px;
  width:380px;
  text-align:center;
  color:#cafff7;
  position:relative;
}
.modal input{
  width:90%;
  margin-top:6px;
}
.error{
  color:#ffbbbb;
  font-size:12px;
  margin-top:6px;
}
.success{
  color:#7effa8;
  font-size:13px;
  margin-top:10px;
  background:rgba(143,224,155,0.12);
  padding:10px;
  border-radius:6px;
  border-left:4px solid #7effa8;
}
.flag{
  display:inline-block;
  margin-top:6px;
  font-weight:bold;
  letter-spacing:0.5px;
  color:#d9fff9;
  background:#011b1b;
  border:1px solid #17786e;
  padding:6px 8px;
}
.flag-row{
  display:flex;
  align-items:center;
  justify-content:center;
  gap:8px;
  flex-wrap:wrap;
  margin-top:6px;
}
.copybtn{
  margin-top:0;
  padding:4px 10px;
  font-size:11px;
  background:linear-gradient(180deg,#2aaea0,#04524c);
  color:#eaffff;
  border:1px solid #18a298;
}
button.emergency{
  margin-top:18px;
  padding:8px 26px;
  font-weight:bold;
  background:linear-gradient(180deg,#ff5c5c,#b30000);
  border:2px outset #b30000;
  color:#fff;
}
button.emergency:hover{
  filter:brightness(1.15);
}
.modal-close{
  position:absolute;
  right:8px;
  top:4px;
  cursor:pointer;
  font-size:18px;
  color:#cafff7;
}
.modal-close:hover{
  color:#ffbbbb;
}
#escapeDoor{
  display:none;
}
</style>
</head>
<body>
<div class="window" id="loginWindow">
  <div class="titlebar">HOPSEC ASYLUM - ACCESS TERMINAL</div>
  <div class="content">
    <h3>Welcome to HopSec Security Console</h3>
    <p>Please input credentials</p>
    <form method="POST" action="/cgi-bin/login.sh">
      <label>Login:</label>
      <input type="text" name="username" placeholder="Email" required>
      <label>Password:</label>
      <input type="password" name="password" placeholder="Password" required>
      <button type="submit">Enter</button>
    </form>
    <p style="font-size:12px;color:#7ce7d6;margin-top:8px;">
      Hopkins, please stop forgetting your password
    </p>
  </div>
</div>

<div id="mapScreen">
  <div class="titlebar">FACILITY MAP - AUTHORIZED PERSONNEL ONLY</div>
  <div class="map-wrap">
    <svg viewBox="0 0 900 720" aria-label="HopSec Asylum Map">
      <defs>
        <filter id="glow">
          <feGaussianBlur stdDeviation="2.5" result="b"/>
          <feMerge>
            <feMergeNode in="b"/>
            <feMergeNode in="SourceGraphic"/>
          </feMerge>
        </filter>
      </defs>
      <rect x="0" y="0" width="900" height="720" fill="#001a10"/>
      <g fill="#0b5f28" stroke="#00b25a" stroke-width="3">
        <rect x="60" y="140" width="250" height="180" rx="8"/>
        <rect x="60" y="340" width="250" height="180" rx="8"/>
        <rect x="340" y="260" width="220" height="220" rx="8"/>
        <rect x="620" y="140" width="220" height="180" rx="8"/>
        <rect x="620" y="360" width="220" height="200" rx="8"/>
        <rect x="300" y="520" width="300" height="110" rx="8"/>
      </g>
      <g fill="#c6ffd6" font-size="14" font-family="Lucida Console, Monaco, monospace" opacity="0.85">
        <text x="90" y="200">Cell Block</text>
        <text x="90" y="400">Cells / Storage</text>
        <text x="360" y="340">Lobby</text>
        <text x="650" y="200">Psych Ward</text>
        <text x="650" y="440">Psych Ward Exit</text>
        <text x="420" y="600">Main Corridor</text>
      </g>
    </svg>

    <button class="iconspot keybtn" data-door="hopper" data-label="Cells / Storage Key" onclick="openDoor('hopper')" style="--x:33%;--y:60%;">
      <img src="key.svg" alt="Cell key">
    </button>

    <button class="iconspot keybtn" data-door="psych" data-label="Psych Ward Exit Key" onclick="openDoor('psych')" style="--x:93%;--y:64%;">
      <img src="key.svg" alt="Psych ward key">
    </button>

    <button class="iconspot keybtn" data-door="exit" data-label="Asylum Exit Key" onclick="openDoor('exit')" style="--x:50%;--y:88%;">
      <img src="key.svg" alt="Asylum exit key">
    </button>

    <button class="iconspot" data-label="Camera 1 - Cell Block" onclick="viewCamera('1')" style="--x:20%;--y:30%;">
      <img src="camera.svg" alt="Security camera 1">
    </button>

    <button class="iconspot" data-label="Camera 2 - Lobby" onclick="viewCamera('2')" style="--x:50%;--y:50%;">
      <img src="camera.svg" alt="Security camera 2">
    </button>

    <button class="iconspot" data-label="Camera 3 - Psych Ward Exit" onclick="viewCamera('3')" style="--x:85%;--y:55%;">
      <img src="camera.svg" alt="Security camera 3">
    </button>

    <button class="iconspot" id="escapeDoor" data-label="Exit Facility" onclick="showEscapeModal()" style="--x:50%;--y:95%;">
      <img src="door.svg" alt="Exit door">
    </button>
  </div>
  <p style="text-align:center;color:#7ce7d6;font-size:12px;margin:6px 0 2px;">
    Tip: Hover keys and cameras for labels.
  </p>
</div>

<div class="modal-bg" id="modalBg">
  <div class="modal">
    <h3 id="doorTitle">Authorisation Required</h3>
    <div id="doorAuthBlock">
      <label id="doorSecretLabel">Secret:</label>
      <input type="password" id="doorSecret" placeholder="Enter code">
      <div style="margin-top:10px;">
        <button onclick="submitDoorSecret()">Submit</button>
        <button onclick="closeModal()">Cancel</button>
      </div>
      <div class="error" id="doorError"></div>
      <div class="success" id="doorSuccess" style="display:none"></div>
    </div>
    <div id="hopperBlock" style="display:none;margin-top:6px;">
      <p style="font-size:13px;line-height:1.4;">
        As an <span style="color:#7effa8;">authenticated user</span> you can remotely unlock patient cell doors in the event of an emergency.<br><br>
        <span style="color:#ffbbbb;font-weight:bold;">
          This control should only be used when you have explicit authorisation.
        </span>
      </p>
      <button class="emergency" onclick="unlockCell()">Unlock Cell Door</button>
      <div class="success" id="hopperFlag" style="display:none;">
        <div><strong>Cell door unlocked.</strong></div>
        <div class="flag-row">
          <span class="flag" id="hopperFlagText"></span>
          <button class="copybtn" onclick="copyById('hopperFlagText')">Copy</button>
        </div>
      </div>
      <div style="margin-top:10px;">
        <button onclick="closeModal()">Close</button>
      </div>
    </div>
  </div>
</div>

<div class="modal-bg" id="escapeModal">
  <div class="modal">
    <span class="modal-close" onclick="closeEscapeModal()">✕</span>
    <h3>HopSec Asylum – Final Escape Challenge</h3>
    <p style="font-size:13px;line-height:1.5;margin-top:6px;">
      To fully escape HopSec Asylum, you must provide all three flags you have collected.
    </p>
    <div style="text-align:left;margin-top:10px;font-size:12px;">
      <label for="flag1Input">Flag 1:</label>
      <input id="flag1Input" type="text" placeholder="Enter first flag">
      <label for="flag2Input" style="margin-top:10px;">Flag 2:</label>
      <input id="flag2Input" type="text" placeholder="Enter second flag">
      <label for="flag3Input" style="margin-top:10px;">Flag 3:</label>
      <input id="flag3Input" type="text" placeholder="Enter third flag">
    </div>
    <div style="margin-top:12px;">
      <button onclick="submitEscapeFlags()">Submit Flags</button>
    </div>
    <div class="error" id="escapeError"></div>
    <div class="success" id="escapeResult" style="display:none"></div>
  </div>
</div>

<script>
const unlocked={hopper:false,psych:false,exit:false};
const STORAGE_KEY="hopsec_unlocked_v1";
let currentDoor=null;

function saveUnlocked(){
  try{
    localStorage.setItem(STORAGE_KEY,JSON.stringify(unlocked));
  }catch(e){}
}
function loadUnlocked(){
  try{
    const raw=localStorage.getItem(STORAGE_KEY);
    if(!raw)return;
    const data=JSON.parse(raw);
    if(typeof data==="object"){
      if(typeof data.hopper==="boolean")unlocked.hopper=data.hopper;
      if(typeof data.psych==="boolean")unlocked.psych=data.psych;
      if(typeof data.exit==="boolean")unlocked.exit=data.exit;
    }
  }catch(e){}
}
function applyUnlockedVisuals(){
  Object.keys(unlocked).forEach(d=>{
    if(unlocked[d]){
      const btn=document.querySelector('.keybtn[data-door="'+d+'"]');
      if(btn)btn.classList.add("unlocked");
    }
  });
  if(unlocked.hopper&&unlocked.psych&&unlocked.exit){
    const ed=document.getElementById("escapeDoor");
    if(ed)ed.style.display="block";
  }
}
function markUnlocked(d){
  if(!unlocked[d]){
    unlocked[d]=true;
    const btn=document.querySelector('.keybtn[data-door="'+d+'"]');
    if(btn)btn.classList.add("unlocked");
    saveUnlocked();
    if(unlocked.hopper&&unlocked.psych&&unlocked.exit){
      const ed=document.getElementById("escapeDoor");
      if(ed)ed.style.display="block";
    }
  }
}
function openDoor(door){
  currentDoor=door;
  const title=document.getElementById("doorTitle");
  const authBlock=document.getElementById("doorAuthBlock");
  const hopperBlock=document.getElementById("hopperBlock");
  const hopperFlag=document.getElementById("hopperFlag");
  const err=document.getElementById("doorError");
  const succ=document.getElementById("doorSuccess");
  const label=document.getElementById("doorSecretLabel");
  const secretInput=document.getElementById("doorSecret");
  err.textContent="";
  succ.innerHTML="";
  succ.style.display="none";
  if(door==="hopper"){
    title.textContent="EMERGENCY CONTROL: Cell / Storage Wing";
    authBlock.style.display="none";
    hopperBlock.style.display="block";
    if(hopperFlag)hopperFlag.style.display="none";
  }else{
    hopperBlock.style.display="none";
    authBlock.style.display="block";
    secretInput.value="";
    if(door==="psych"){
      title.textContent="Door Access: Psych Ward Exit";
      label.textContent="Keycode:";
      secretInput.placeholder="Enter keycode";
      secretInput.type="password";
    }else{
      title.textContent="Door Access: Asylum Exit";
      label.textContent="SCADA Unlock Passcode:";
      secretInput.placeholder="Enter passcode";
      secretInput.type="password";
    }
  }
  document.getElementById("modalBg").style.display="flex";
}
function closeModal(){
  document.getElementById("modalBg").style.display="none";
}
async function unlockCell(){
  const flagDiv=document.getElementById("hopperFlag");
  const span=document.getElementById("hopperFlagText");
  if(flagDiv)flagDiv.style.display="none";
  try{
    const res=await fetch("/cgi-bin/key_flag.sh?door=hopper");
    const data=await res.json();
    if(data&&data.ok&&data.flag){
      if(span)span.textContent=data.flag;
      if(flagDiv)flagDiv.style.display="block";
      markUnlocked("hopper");
    }else{
      if(flagDiv){
        flagDiv.style.display="block";
        flagDiv.innerHTML="<div>Unlock succeeded, but flag could not be retrieved.</div>";
      }
      markUnlocked("hopper");
    }
  }catch(e){
    if(flagDiv){
      flagDiv.style.display="block";
      flagDiv.innerHTML="<div>Error contacting server for flag.</div>";
    }
  }
}
async function submitDoorSecret(){
  if(currentDoor!=="psych"&&currentDoor!=="exit")return;
  const secret=document.getElementById("doorSecret").value.trim();
  const e=document.getElementById("doorError");
  const s=document.getElementById("doorSuccess");
  e.textContent="";
  s.innerHTML="";
  s.style.display="none";
  if(!secret){
    e.textContent="Please enter a code.";
    return;
  }
  const endpoint=currentDoor==="psych"?"/cgi-bin/psych_check.sh":"/cgi-bin/exit_check.sh";
  try{
    const res=await fetch(endpoint,{
      method:"POST",
      headers:{"Content-Type":"application/x-www-form-urlencoded"},
      body:"code="+encodeURIComponent(secret)
    });
    const data=await res.json();
    if(data&&data.error==="rate_limit"){
      e.textContent="Too many attempts. Please wait and try again.";
      return;
    }
    if(!data||!data.ok){
      e.textContent="Invalid code.";
      return;
    }
    const flag=data.flag||"";
    let html="";
    if(currentDoor==="psych"){
      html+='<div><strong>Psych Ward exit keycode accepted.</strong></div>';
      html+='<p style="margin:6px 0 4px;font-size:12px;">This is only the first part of your second flag. You will need to complete it elsewhere.</p>';
      if(flag){
        html+='<div class="flag-row"><span class="flag" id="psychFlagText"></span><button class="copybtn" onclick="copyById(\'psychFlagText\')">Copy</button></div>';
      }
      markUnlocked("psych");
    }else{
      html+='<div><strong>Asylum Exit SCADA passcode accepted.</strong></div>';
      if(flag){
        html+='<div class="flag-row"><span class="flag" id="exitFlagText"></span><button class="copybtn" onclick="copyById(\'exitFlagText\')">Copy</button></div>';
      }
      markUnlocked("exit");
    }
    s.innerHTML=html;
    s.style.display="block";
    if(currentDoor==="psych"&&flag){
      const span=document.getElementById("psychFlagText");
      if(span)span.textContent=flag;
    }
    if(currentDoor==="exit"&&flag){
      const span=document.getElementById("exitFlagText");
      if(span)span.textContent=flag;
    }
  }catch(err){
    e.textContent="Error contacting server.";
  }
}
function viewCamera(id){
  alert("Camera "+id+" feed is currently unavailable.");
}
function copyById(id){
  const el=document.getElementById(id);
  if(!el)return;
  const txt=el.textContent.trim();
  if(navigator.clipboard&&navigator.clipboard.writeText){
    navigator.clipboard.writeText(txt).catch(()=>{});
  }else{
    const ta=document.createElement("textarea");
    ta.value=txt;
    document.body.appendChild(ta);
    ta.select();
    try{document.execCommand("copy");}catch(e){}
    document.body.removeChild(ta);
  }
}
function showEscapeModal(){
  const modal=document.getElementById("escapeModal");
  const err=document.getElementById("escapeError");
  const res=document.getElementById("escapeResult");
  const f1=document.getElementById("flag1Input");
  const f2=document.getElementById("flag2Input");
  const f3=document.getElementById("flag3Input");
  if(f1)f1.value="";
  if(f2)f2.value="";
  if(f3)f3.value="";
  err.textContent="";
  res.innerHTML="";
  res.style.display="none";
  modal.style.display="flex";
}
function closeEscapeModal(){
  document.getElementById("escapeModal").style.display="none";
}
async function submitEscapeFlags(){
  const f1=document.getElementById("flag1Input").value.trim();
  const f2=document.getElementById("flag2Input").value.trim();
  const f3=document.getElementById("flag3Input").value.trim();
  const err=document.getElementById("escapeError");
  const res=document.getElementById("escapeResult");
  err.textContent="";
  res.innerHTML="";
  res.style.display="none";
  if(!f1||!f2||!f3){
    err.textContent="Please enter all three flags.";
    return;
  }
  try{
    const resp=await fetch("/cgi-bin/escape_check.sh",{
      method:"POST",
      headers:{"Content-Type":"application/x-www-form-urlencoded"},
      body:"flag1="+encodeURIComponent(f1)+"&flag2="+encodeURIComponent(f2)+"&flag3="+encodeURIComponent(f3)
    });
    const data=await resp.json();
    if(!data||!data.ok){
      err.textContent="One or more flags are incorrect.";
      return;
    }
    const url=data.invite_url||"";
    const code=data.invite_code||"";
    let html="<p>All three flags verified. Hopper grants you access to his next challenge.</p>";
    if(url){
      html+='<div class="flag-row"><span class="flag" id="escapeUrl"></span><button class="copybtn" onclick="copyById(\'escapeUrl\')">Copy URL</button></div>';
    }
    if(code){
      html+='<div class="flag-row"><span class="flag" id="escapeCode"></span><button class="copybtn" onclick="copyById(\'escapeCode\')">Copy invite code</button></div>';
    }
    res.innerHTML=html;
    res.style.display="block";
    if(url){
      const su=document.getElementById("escapeUrl");
      if(su)su.textContent=url;
    }
    if(code){
      const sc=document.getElementById("escapeCode");
      if(sc)sc.textContent=code;
    }
  }catch(e){
    err.textContent="Error contacting server.";
  }
}
async function checkSession(){
  const loginWin=document.getElementById("loginWindow");
  const map=document.getElementById("mapScreen");
  try{
    const res=await fetch("/cgi-bin/session_check.sh",{cache:"no-store"});
    const data=await res.json();
    if(data&&data.authed){
      loginWin.style.display="none";
      map.style.display="block";
    }else{
      loginWin.style.display="block";
      map.style.display="none";
    }
  }catch(e){
    loginWin.style.display="block";
    map.style.display="none";
  }
}
document.addEventListener("DOMContentLoaded",async function(){
  await checkSession();
  loadUnlocked();
  applyUnlockedVisuals();
});
</script>
</body>
</html>


main.js
// spa/main.js

const API = window.location.protocol + '//' + window.location.hostname + ':13401';

let token = localStorage.getItem('hopsec_token') || '';
let role  = localStorage.getItem('hopsec_role')  || '';

function inferRoleFromToken(t){
  try {
    const i = t.lastIndexOf('.');
    if (i <= 0) return '';
    const payload = t.slice(0, i);
    const j = JSON.parse(payload);
    return j.role || '';
  } catch(e){ return ''; }
}

function authedFetch(url, opts = {}) {
  opts.headers = Object.assign({ 'Authorization': 'Bearer ' + token }, (opts.headers || {}));
  return fetch(url, opts);
}

const timeFmt = new Intl.DateTimeFormat('fr-FR', {
  timeZone:'Europe/Paris', year:'numeric', month:'2-digit', day:'2-digit',
  hour:'2-digit', minute:'2-digit', second:'2-digit'
});
function startClock(){
  const el = document.getElementById('hudTime');
  if (!el) return;
  el.textContent = timeFmt.format(new Date());
  setInterval(() => { el.textContent = timeFmt.format(new Date()); }, 1000);
}

let hls = null;
const video   = (() => document.getElementById('v') || document.getElementById('player'))();
const hudSig  = document.getElementById('hudSignal');
const blocked = document.getElementById('blocked');

function setActiveCamera(id, title) {
  const el = document.getElementById('hudCam');
  if (el) el.textContent = (title || id || '—').toUpperCase();
}

function clearPlayer(){
  try {
    if (hls) {
      try { hls.stopLoad(); } catch(e){}
      try { hls.detachMedia(); } catch(e){}
      try { hls.destroy(); } catch(e){}
      hls = null;
    }
    if (video) {
      video.pause();
      video.removeAttribute('src');
      video.load();
    }
  } catch(e){}
  if (hudSig) hudSig.style.display = 'none';
}

function attachWithReconnect(src) {
  if (blocked) blocked.style.display='none';
  if (hudSig) hudSig.style.display = 'none';
  if (!video) return;

  if (hls) { try { hls.destroy(); } catch(e){} hls = null; }

  if (window.Hls && Hls.isSupported()) {
    hls = new Hls({ backBufferLength: 30, enableWorker: true });
    hls.on(Hls.Events.ERROR, (_, data) => {
      if (data.fatal) {
        if (hudSig) hudSig.style.display = 'inline-block';
        setTimeout(() => attachWithReconnect(src), 1500);
      }
    });
    hls.on(Hls.Events.MANIFEST_PARSED, () => { if (hudSig) hudSig.style.display = 'none'; });
    hls.loadSource(src);
    hls.attachMedia(video);
  } else {
    video.src = src;
    video.addEventListener('error', () => {
      if (hudSig) hudSig.style.display = 'inline-block';
      setTimeout(() => { video.load(); }, 1500);
    }, { once:true });
  }
  video.play().catch(()=>{});
}

async function loadCameras() {
  const r = await authedFetch(API + '/v1/cameras');
  if (!r.ok) throw new Error('cameras: ' + r.status);
  const j = await r.json();

  const listA = document.getElementById('camList');
  const listGuard = document.getElementById('guardCams');
  const listRestr = document.getElementById('restrictedCams');

  if (listA) listA.innerHTML = '';
  if (listGuard) listGuard.innerHTML = '';
  if (listRestr) listRestr.innerHTML = '';

  j.cameras.forEach(cam => {
    const name = cam.name || cam.desc || cam.id;
    const desc = cam.desc || cam.site || '';
    const required = cam.required_role || 'guard';
    const isAdminCam = cam.id === 'cam-admin';

    const el = document.createElement('div');
    el.className = (listA ? 'cam' : 'card');

    if (listA) {
      el.innerHTML = `
        <div>
          <div><strong>${name}</strong></div>
          <small>${desc}</small>
        </div>
        <span class="badge">${required}${isAdminCam ? ' · restricted' : ''}</span>
      `;
      el.addEventListener('click', () => handleCameraClick(cam));
      listA.appendChild(el);
    } else {
      if (required === 'admin') {
        const disabled = (role !== 'admin') ? 'disabled' : '';
        el.innerHTML = `
          <strong>${cam.id}</strong> <span class="badge">${cam.site}</span>
          <div>${desc}</div>
          <div class="note">Admin-only</div>
          <button data-id="${cam.id}" class="admin" ${disabled}>Admin View</button>`;
        (listRestr || listGuard).appendChild(el);
      } else {
        el.innerHTML = `
          <strong>${cam.id}</strong> <span class="badge">${cam.site}</span>
          <div>${desc}</div>
          <div>tier: guard</div>
          <button data-id="${cam.id}" class="req">Request Ticket</button>`;
        (listGuard || listA).appendChild(el);
      }
    }
  });

  document.querySelectorAll(".req").forEach(b => b.onclick = () => requestTicket(b.getAttribute("data-id"), "guard"));
  document.querySelectorAll(".admin").forEach(b => b.onclick = () => requestTicket(b.getAttribute("data-id"), "admin"));
}

async function handleCameraClick(cam){
  setActiveCamera(cam.id, cam.name || cam.desc);
  const isAdmin = (role === 'admin');

  if (cam.id === 'cam-admin' && !isAdmin) {
    if (blocked) blocked.style.display='flex';
    clearPlayer();
    return;
  }

  const desiredTier = (cam.id === 'cam-admin') ? 'admin' : 'guard';

  const r = await authedFetch(API + '/v1/streams/request', {
    method:'POST',
    headers:{ 'Content-Type':'application/json' },
    body: JSON.stringify({ camera_id: cam.id, tier: desiredTier })
  });

  const j = await r.json();
  if (!r.ok || !j.ticket_id) {
    clearPlayer();
    if (blocked) blocked.style.display='flex';
    return;
  }
  const src = API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8';
  attachWithReconnect(src);
}

async function requestTicket(camera_id, tier){
  const r = await authedFetch(API + '/v1/streams/request', {
    method:'POST',
    headers:{ 'Content-Type':'application/json' },
    body: JSON.stringify({ camera_id, tier })
  });
  const j = await r.json();
  if (!j.ticket_id) return;

  if (camera_id !== 'cam-admin' && j.effective_tier === 'guard') {
    attachWithReconnect(API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8');
  }
  if (camera_id === 'cam-admin' && j.effective_tier === 'admin') {
    attachWithReconnect(API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8');
  }
}

async function doLogin(){
  const u = (document.getElementById('u') || document.getElementById('username')).value.trim();
  const p = (document.getElementById('p') || document.getElementById('password')).value;
  const msg = document.getElementById('msg');
  if (msg) msg.textContent = '';

  try{
    const r = await fetch(API + '/v1/auth/login', {
      method:"POST", headers:{"Content-Type":"application/json"},
      body: JSON.stringify({ username: u, password: p })
    });
    const j = await r.json();
    if (!r.ok) { if (msg) msg.textContent = 'Login failed'; return; }

    token = j.token;
    role  = (j.profile && j.profile.role) ? j.profile.role : (inferRoleFromToken(token) || 'guard');
    localStorage.setItem('hopsec_token', token);
    localStorage.setItem('hopsec_role', role);

    const auth = document.getElementById('auth') || document.getElementById('loginPanel');
    const app  = document.getElementById('app')  || document.getElementById('mainGrid');

    if (auth) auth.classList.add('hidden');
    if (app)  { app.classList.remove('hidden'); app.style.display = 'grid'; }

    const pill = document.getElementById('rolepill') || document.getElementById('rolePill');
    if (pill) pill.textContent = (role === 'admin') ? 'Admin Console' : 'Guard Console';

    await loadCameras();
  } catch(e){
    if (msg) msg.textContent = 'API unreachable';
  }
}

function boot(){
  startClock();

  const loginBtn = document.getElementById('loginBtn') || document.getElementById('login');
  if (loginBtn) loginBtn.onclick = doLogin;

  if (token) {
    if (!role) role = inferRoleFromToken(token) || 'guard';
    localStorage.setItem('hopsec_role', role);

    const auth = document.getElementById('auth') || document.getElementById('loginPanel');
    const app  = document.getElementById('app')  || document.getElementById('mainGrid');
    if (auth) auth.classList.add('hidden');
    if (app)  { app.classList.remove('hidden'); app.style.display = 'grid'; }

    const pill = document.getElementById('rolepill') || document.getElementById('rolePill');
    if (pill) pill.textContent = (role === 'admin') ? 'Admin Console' : 'Guard Console';

    loadCameras().catch(()=>{});
  }
}

document.addEventListener('DOMContentLoaded', boot);



POST /cgi-bin/login.sh HTTP/1.1
Host: 10.65.169.88
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 27
Origin: http://10.65.169.88
Connection: keep-alive
Referer: http://10.65.169.88/
Cookie: csrftoken=6yPwZxDGJu4BKyNFuQTesleJzIk6mTfYWzYwNXhIsk0TNbd7zIM5yQClterNVPEo
Upgrade-Insecure-Requests: 1
Priority: u=0, i

username=hola&password=hola


HTTP/1.1 404 Not Found
Server: nginx/1.24.0 (Ubuntu)
Date: Tue, 02 Dec 2025 00:46:54 GMT
Content-Type: text/html
Connection: keep-alive
Content-Length: 162

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.24.0 (Ubuntu)</center>
</body>
</html>


GET /cgi-bin/session_check.sh HTTP/1.1
Host: 10.65.169.88
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://10.65.169.88/
Connection: keep-alive
Cookie: csrftoken=6yPwZxDGJu4BKyNFuQTesleJzIk6mTfYWzYwNXhIsk0TNbd7zIM5yQClterNVPEo
Priority: u=4
Pragma: no-cache
Cache-Control: no-cache


HTTP/1.1 404 Not Found
Server: nginx/1.24.0 (Ubuntu)
Date: Tue, 02 Dec 2025 00:46:47 GMT
Content-Type: text/html
Connection: keep-alive
Content-Length: 162

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.24.0 (Ubuntu)</center>
</body>
</html>









gobuster dir -u 10.65.169.88 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -x html,php,txt,json 
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.65.169.88
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              php,txt,json,html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 19522]
/cgi-bin              (Status: 301) [Size: 178] [--> http://10.65.169.88/cgi-bin/]
/success.html         (Status: 200) [Size: 179]




http://10.65.169.88/success.html
Access Granted
THM{ACCESS_PLACEHOLDER_FLAG}



```

### Puerto 13400
```
curl http://10.65.169.88:13400/ -o puerto13400.html

grep "<title>" puerto13400.html
  <title>HopSec Asylum – Facility Video Portal</title>

url -v http://10.65.169.88:13400/ 
*   Trying 10.65.169.88:13400...
* Established connection to 10.65.169.88 (10.65.169.88 port 13400) from 192.168.154.37 port 58292 
* using HTTP/1.x
> GET / HTTP/1.1
> Host: 10.65.169.88:13400
> User-Agent: curl/8.17.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Server: nginx/1.24.0 (Ubuntu)
< Date: Tue, 02 Dec 2025 00:54:12 GMT
< Content-Type: text/html
< Content-Length: 5888
< Last-Modified: Fri, 28 Nov 2025 07:13:17 GMT
< Connection: keep-alive
< ETag: "69294b8d-1700"
< Accept-Ranges: bytes
< 

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <title>HopSec Asylum – Facility Video Portal</title>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <link rel="icon" href="/favicon.ico"/>

<script src="/hls.min.js"></script>
  <style>
    :root { --bg:#0b0f14; --fg:#d6dde5; --muted:#7d8a97; --accent:#3aa675; --danger:#ff4d4f; }
    * { box-sizing:border-box; }
    html,body { height:100%; margin:0; background:var(--bg); color:var(--fg);
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; }
    .app { max-width:1200px; margin:0 auto; padding:20px; }
    header { display:flex; align-items:center; gap:10px; margin-bottom:14px; }
    header h1 { font-size:18px; margin:0; letter-spacing:.04em; color:#c7ffd5; }
    .pill { font-size:12px; padding:2px 8px; border:1px solid #204437; color:#8fe3b5; border-radius:999px; }

    .grid { display:grid; grid-template-columns: 280px 1fr; gap:16px; }
    .panel { border:1px solid #1e2a36; border-radius:8px; background:#0e141a; }
    .panel header { display:flex; justify-content:space-between; align-items:center; padding:10px 12px;
      border-bottom:1px solid #1e2a36; }
    .panel header h2 { font-size:13px; margin:0; text-transform:uppercase; letter-spacing:.08em; color:#aab8c6; }
    .panel .body { padding:12px; }

    /* login */
    .login { max-width:360px; margin:40px auto; }
    .form-row { display:flex; gap:8px; margin-bottom:8px; }
    input[type=text], input[type=password] {
      width:100%; padding:10px; border-radius:6px; border:1px solid #223447; background:#0c1117; color:var(--fg);
    }
    .btn { padding:10px 14px; border:1px solid #284a3c; background:#12251c; color:#b4f1c8; border-radius:6px; cursor:pointer; }
    .btn:disabled { opacity:.6; cursor:not-allowed; }
    .msg { color:#ffbcbc; min-height:1.2em; }

    /* camera list (HUD layout) */
    .cams { display:flex; flex-direction:column; gap:6px; }
    .cam { display:flex; justify-content:space-between; align-items:center; padding:8px 10px;
      border:1px solid #1e2a36; border-radius:6px; background:#0b1016; }
    .cam:hover { background:#0f1620; }
    .cam .badge { font-size:11px; padding:2px 6px; border-radius:999px; border:1px solid #293341; color:#9fb0c3; }

    /* player: 16:9 letterboxed, no cropping */
    .player-wrap { position:relative; width:100%; aspect-ratio: 16 / 9; background:#000;
      border:1px solid #1e2a36; border-radius:8px; overflow:hidden; }
    video { position:absolute; inset:0; width:100%; height:100%; object-fit:contain; background:#000; }

    /* HUD overlay */
    .hud { position:absolute; inset:0; pointer-events:none; }
    .hud-top { position:absolute; top:10px; left:10px; right:10px; display:flex; justify-content:space-between; gap:8px; }
    #hudCam { background:rgba(0,0,0,.65); color:#fff; padding:4px 8px; font-weight:700; letter-spacing:.06em; border-radius:4px; }
    #hudTime { background:rgba(0,0,0,.65); color:#b9ffc2; padding:4px 8px; border-radius:4px; font-variant-numeric:tabular-nums; }
    .hud-bottom { position:absolute; left:10px; bottom:10px; display:flex; gap:8px; align-items:center; }
    #hudStatus { background:rgba(230,0,0,.78); color:#fff; padding:3px 8px; border-radius:4px; font-weight:700; letter-spacing:.06em; }
    #hudSignal { background:rgba(0,0,0,.65); color:#ffcdcd; padding:3px 8px; border-radius:4px; display:none; }

    /* blocked overlay */
    .blocked {
      position:absolute; inset:0; display:none; align-items:center; justify-content:center; text-align:center;
      background:linear-gradient(0deg, rgba(0,0,0,0.65), rgba(0,0,0,0.65));
      color:#ffd6d6; font-weight:700; letter-spacing:.06em; text-transform:uppercase; padding:20px;
    }
    .blocked .box { border:2px solid #5a2a2a; border-radius:8px; padding:16px 20px; background:rgba(30,12,12,.6); }
    .blocked .title { font-size:20px; margin-bottom:6px; color:#ff8080; }
    .blocked .sub { font-size:12px; color:#ffbcbc; letter-spacing:0; text-transform:none; }

    .hidden { display:none !important; }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <h1>HopSec Asylum – Facility Video Portal</h1>
      <span id="rolePill" class="pill">Guard Console</span>
    </header>

    <div class="panel login" id="loginPanel">
      <header><h2>Sign in</h2></header>
      <div class="body">
        <div class="form-row"><input id="u" type="text" placeholder="Email"></div>
        <div class="form-row"><input id="p" type="password" placeholder="Password"></div>
        <div class="form-row"><button class="btn" id="loginBtn">Login</button></div>
        <div class="msg" id="msg"></div>
      </div>
    </div>

    <div class="grid" id="mainGrid" style="display:none;">
      <div class="panel">
        <header><h2>Cameras</h2></header>
        <div class="body">
          <div id="camList" class="cams"></div>
        </div>
      </div>

      <div class="panel">
        <header><h2>Viewer</h2></header>
        <div class="body">
          <div class="player-wrap">
            <video id="v" playsinline muted></video>
            <div class="hud">
              <div class="hud-top">
                <div id="hudCam">—</div>
                <div id="hudTime">--/--/---- --:--:--</div>
              </div>
              <div class="hud-bottom">
                <div id="hudStatus">LIVE</div>
                <div id="hudSignal">SIGNAL LOST — Reconnecting…</div>
              </div>
            </div>
            <div id="blocked" class="blocked">
              <div class="box">
                <div class="title">Access Restricted</div>
                <div class="sub">You do not have permission to view this feed.</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <script src="main.js"></script>
</body>
</html>
* Connection #0 to host 10.65.169.88:13400 left intact
  
main.js
// spa/main.js

const API = window.location.protocol + '//' + window.location.hostname + ':13401';

let token = localStorage.getItem('hopsec_token') || '';
let role  = localStorage.getItem('hopsec_role')  || '';

function inferRoleFromToken(t){
  try {
    const i = t.lastIndexOf('.');
    if (i <= 0) return '';
    const payload = t.slice(0, i);
    const j = JSON.parse(payload);
    return j.role || '';
  } catch(e){ return ''; }
}

function authedFetch(url, opts = {}) {
  opts.headers = Object.assign({ 'Authorization': 'Bearer ' + token }, (opts.headers || {}));
  return fetch(url, opts);
}

const timeFmt = new Intl.DateTimeFormat('fr-FR', {
  timeZone:'Europe/Paris', year:'numeric', month:'2-digit', day:'2-digit',
  hour:'2-digit', minute:'2-digit', second:'2-digit'
});
function startClock(){
  const el = document.getElementById('hudTime');
  if (!el) return;
  el.textContent = timeFmt.format(new Date());
  setInterval(() => { el.textContent = timeFmt.format(new Date()); }, 1000);
}

let hls = null;
const video   = (() => document.getElementById('v') || document.getElementById('player'))();
const hudSig  = document.getElementById('hudSignal');
const blocked = document.getElementById('blocked');

function setActiveCamera(id, title) {
  const el = document.getElementById('hudCam');
  if (el) el.textContent = (title || id || '—').toUpperCase();
}

function clearPlayer(){
  try {
    if (hls) {
      try { hls.stopLoad(); } catch(e){}
      try { hls.detachMedia(); } catch(e){}
      try { hls.destroy(); } catch(e){}
      hls = null;
    }
    if (video) {
      video.pause();
      video.removeAttribute('src');
      video.load();
    }
  } catch(e){}
  if (hudSig) hudSig.style.display = 'none';
}

function attachWithReconnect(src) {
  if (blocked) blocked.style.display='none';
  if (hudSig) hudSig.style.display = 'none';
  if (!video) return;

  if (hls) { try { hls.destroy(); } catch(e){} hls = null; }

  if (window.Hls && Hls.isSupported()) {
    hls = new Hls({ backBufferLength: 30, enableWorker: true });
    hls.on(Hls.Events.ERROR, (_, data) => {
      if (data.fatal) {
        if (hudSig) hudSig.style.display = 'inline-block';
        setTimeout(() => attachWithReconnect(src), 1500);
      }
    });
    hls.on(Hls.Events.MANIFEST_PARSED, () => { if (hudSig) hudSig.style.display = 'none'; });
    hls.loadSource(src);
    hls.attachMedia(video);
  } else {
    video.src = src;
    video.addEventListener('error', () => {
      if (hudSig) hudSig.style.display = 'inline-block';
      setTimeout(() => { video.load(); }, 1500);
    }, { once:true });
  }
  video.play().catch(()=>{});
}

async function loadCameras() {
  const r = await authedFetch(API + '/v1/cameras');
  if (!r.ok) throw new Error('cameras: ' + r.status);
  const j = await r.json();

  const listA = document.getElementById('camList');
  const listGuard = document.getElementById('guardCams');
  const listRestr = document.getElementById('restrictedCams');

  if (listA) listA.innerHTML = '';
  if (listGuard) listGuard.innerHTML = '';
  if (listRestr) listRestr.innerHTML = '';

  j.cameras.forEach(cam => {
    const name = cam.name || cam.desc || cam.id;
    const desc = cam.desc || cam.site || '';
    const required = cam.required_role || 'guard';
    const isAdminCam = cam.id === 'cam-admin';

    const el = document.createElement('div');
    el.className = (listA ? 'cam' : 'card');

    if (listA) {
      el.innerHTML = `
        <div>
          <div><strong>${name}</strong></div>
          <small>${desc}</small>
        </div>
        <span class="badge">${required}${isAdminCam ? ' · restricted' : ''}</span>
      `;
      el.addEventListener('click', () => handleCameraClick(cam));
      listA.appendChild(el);
    } else {
      if (required === 'admin') {
        const disabled = (role !== 'admin') ? 'disabled' : '';
        el.innerHTML = `
          <strong>${cam.id}</strong> <span class="badge">${cam.site}</span>
          <div>${desc}</div>
          <div class="note">Admin-only</div>
          <button data-id="${cam.id}" class="admin" ${disabled}>Admin View</button>`;
        (listRestr || listGuard).appendChild(el);
      } else {
        el.innerHTML = `
          <strong>${cam.id}</strong> <span class="badge">${cam.site}</span>
          <div>${desc}</div>
          <div>tier: guard</div>
          <button data-id="${cam.id}" class="req">Request Ticket</button>`;
        (listGuard || listA).appendChild(el);
      }
    }
  });

  document.querySelectorAll(".req").forEach(b => b.onclick = () => requestTicket(b.getAttribute("data-id"), "guard"));
  document.querySelectorAll(".admin").forEach(b => b.onclick = () => requestTicket(b.getAttribute("data-id"), "admin"));
}

async function handleCameraClick(cam){
  setActiveCamera(cam.id, cam.name || cam.desc);
  const isAdmin = (role === 'admin');

  if (cam.id === 'cam-admin' && !isAdmin) {
    if (blocked) blocked.style.display='flex';
    clearPlayer();
    return;
  }

  const desiredTier = (cam.id === 'cam-admin') ? 'admin' : 'guard';

  const r = await authedFetch(API + '/v1/streams/request', {
    method:'POST',
    headers:{ 'Content-Type':'application/json' },
    body: JSON.stringify({ camera_id: cam.id, tier: desiredTier })
  });

  const j = await r.json();
  if (!r.ok || !j.ticket_id) {
    clearPlayer();
    if (blocked) blocked.style.display='flex';
    return;
  }
  const src = API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8';
  attachWithReconnect(src);
}

async function requestTicket(camera_id, tier){
  const r = await authedFetch(API + '/v1/streams/request', {
    method:'POST',
    headers:{ 'Content-Type':'application/json' },
    body: JSON.stringify({ camera_id, tier })
  });
  const j = await r.json();
  if (!j.ticket_id) return;

  if (camera_id !== 'cam-admin' && j.effective_tier === 'guard') {
    attachWithReconnect(API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8');
  }
  if (camera_id === 'cam-admin' && j.effective_tier === 'admin') {
    attachWithReconnect(API + '/v1/streams/' + j.ticket_id + '/manifest.m3u8');
  }
}

async function doLogin(){
  const u = (document.getElementById('u') || document.getElementById('username')).value.trim();
  const p = (document.getElementById('p') || document.getElementById('password')).value;
  const msg = document.getElementById('msg');
  if (msg) msg.textContent = '';

  try{
    const r = await fetch(API + '/v1/auth/login', {
      method:"POST", headers:{"Content-Type":"application/json"},
      body: JSON.stringify({ username: u, password: p })
    });
    const j = await r.json();
    if (!r.ok) { if (msg) msg.textContent = 'Login failed'; return; }

    token = j.token;
    role  = (j.profile && j.profile.role) ? j.profile.role : (inferRoleFromToken(token) || 'guard');
    localStorage.setItem('hopsec_token', token);
    localStorage.setItem('hopsec_role', role);

    const auth = document.getElementById('auth') || document.getElementById('loginPanel');
    const app  = document.getElementById('app')  || document.getElementById('mainGrid');

    if (auth) auth.classList.add('hidden');
    if (app)  { app.classList.remove('hidden'); app.style.display = 'grid'; }

    const pill = document.getElementById('rolepill') || document.getElementById('rolePill');
    if (pill) pill.textContent = (role === 'admin') ? 'Admin Console' : 'Guard Console';

    await loadCameras();
  } catch(e){
    if (msg) msg.textContent = 'API unreachable';
  }
}

function boot(){
  startClock();

  const loginBtn = document.getElementById('loginBtn') || document.getElementById('login');
  if (loginBtn) loginBtn.onclick = doLogin;

  if (token) {
    if (!role) role = inferRoleFromToken(token) || 'guard';
    localStorage.setItem('hopsec_role', role);

    const auth = document.getElementById('auth') || document.getElementById('loginPanel');
    const app  = document.getElementById('app')  || document.getElementById('mainGrid');
    if (auth) auth.classList.add('hidden');
    if (app)  { app.classList.remove('hidden'); app.style.display = 'grid'; }

    const pill = document.getElementById('rolepill') || document.getElementById('rolePill');
    if (pill) pill.textContent = (role === 'admin') ? 'Admin Console' : 'Guard Console';

    loadCameras().catch(()=>{});
  }
}

document.addEventListener('DOMContentLoaded', boot);



```




### Puerto 13403

 ```
nc -v 10.65.169.88 13403
10.65.169.88: inverse host lookup failed: Unknown host
(UNKNOWN) [10.65.169.88] 13403 (?) open
hola
HTTP/1.1 400 Bad Request
Connection: close

```

### Puerto 9001

### Asylum gate

```
──(kali㉿kali)-[~]
└─$ nc -v 10.65.169.88 9001 
10.65.169.88: inverse host lookup failed: Unknown host
(UNKNOWN) [10.65.169.88] 9001 (?) open

╔═══════════════════════════════════════════════════════════════╗
║     ASYLUM GATE CONTROL SYSTEM - SCADA TERMINAL v2.1          ║
║              [AUTHORIZED PERSONNEL ONLY]                      ║
╚═══════════════════════════════════════════════════════════════╝

[!] WARNING: This system controls critical infrastructure
[!] All access attempts are logged and monitored
[!] Unauthorized access will result in immediate termination

[!] Authentication required to access SCADA terminal
[!] Provide authorization token from Part 1 to proceed


[AUTH] Enter authorization token: 

```

### Endpoints que sabemos que existen (del JavaScript):

javascript

```javascript
/cgi-bin/session_check.sh
/cgi-bin/key_flag.sh?door=hopper
/cgi-bin/psych_check.sh
/cgi-bin/exit_check.sh
/cgi-bin/escape_check.sh
/cgi-bin/login.sh
```






## Answer the questions below

What is the first flag?


What is the second flag?

What is the third flag?


