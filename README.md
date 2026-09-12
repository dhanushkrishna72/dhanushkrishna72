<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<title>Dhanush 98</title>
<meta name="viewport" content="width=device-width, initial-scale=1"/>
<style>
  * { box-sizing: border-box; }
  html, body {
    margin: 0; padding: 0; height: 100%;
    font-family: Tahoma, Verdana, Arial, sans-serif;
    overflow: hidden;
    -webkit-user-select: none; user-select: none;
  }
  body { background: #3A6EA5; }

  /* ---------- boot screen ---------- */
  #boot {
    position: fixed; inset: 0; background: #000; color: #B0B0B0;
    font-family: "Courier New", monospace; font-size: 14px;
    padding: 24px; z-index: 9999; line-height: 1.6;
  }
  #boot .cursor { display:inline-block; width:8px; height:14px; background:#B0B0B0; animation: blink 1s steps(2) infinite; vertical-align:-2px;}
  @keyframes blink { 50% { opacity: 0; } }
  #boot .bar-outer { border:1px solid #B0B0B0; width:300px; height:14px; margin-top:14px; }
  #boot .bar-inner { height:100%; width:0%; background:#B0B0B0; animation: load 1.8s ease-in-out forwards; }
  @keyframes load { to { width: 100%; } }
  #boot.hide { display:none; }

  /* ---------- desktop ---------- */
  #desktop {
    position: fixed; inset: 0;
    background: #3A6EA5;
    background-image: repeating-linear-gradient(45deg, rgba(255,255,255,0.02) 0 2px, transparent 2px 8px);
  }
  #icons {
    position: absolute; top: 14px; left: 14px;
    display: flex; flex-direction: column; gap: 18px;
    z-index: 2;
  }
  .icon {
    width: 76px; text-align: center; cursor: pointer; padding: 4px;
  }
  .icon:active, .icon.selected { background: rgba(255,255,255,0.15); outline: 1px dotted #fff; }
  .icon .glyph {
    width: 40px; height: 40px; margin: 0 auto 4px; border: 2px solid #000;
    display: flex; align-items: center; justify-content: center; font-size: 20px;
    box-shadow: 2px 2px 0 rgba(0,0,0,0.35);
  }
  .icon .label {
    color: #fff; font-size: 11px; text-shadow: 1px 1px 1px #000;
    line-height: 1.2;
  }

  /* ---------- window chrome ---------- */
  .win {
    position: absolute;
    background: #ECE9D8;
    border: 2px solid #000;
    box-shadow: 3px 3px 0 rgba(0,0,0,0.4);
    display: flex; flex-direction: column;
    min-width: 260px;
  }
  .win.hidden { display: none; }
  .win .titlebar {
    height: 24px; flex: 0 0 24px;
    background: linear-gradient(to right, #0A246A, #A6CAF0);
    display: flex; align-items: center; padding: 0 4px;
    cursor: default;
  }
  .win .titlebar .ticon { width:14px; height:14px; background:#fff; border-radius:2px; margin-right:6px; display:flex; align-items:center; justify-content:center; font-size:10px;}
  .win .titlebar .ttext { color: #fff; font-weight: bold; font-size: 12px; flex: 1; white-space:nowrap; overflow:hidden; }
  .win .capbtn {
    width: 16px; height: 14px; background: #ECE9D8; border: 1px solid #000;
    box-shadow: inset 1px 1px 0 #fff, inset -1px -1px 0 #808080;
    margin-left: 3px; display:flex; align-items:center; justify-content:center;
    font-size: 10px; font-weight:bold; cursor: pointer; line-height:1;
  }
  .win .menubar { flex: 0 0 18px; background:#ECE9D8; display:flex; align-items:center; padding:0 8px; gap:16px; font-size:11px; border-bottom:1px solid #D4D0C8;}
  .win .toolbar { flex: 0 0 34px; background:#ECE9D8; display:flex; align-items:center; padding:4px 6px; gap:6px; border-bottom:1px solid #D4D0C8; }
  .win .tbtn { background:#ECE9D8; border:1px solid #000; box-shadow: inset 1px 1px 0 #fff, inset -1px -1px 0 #808080; font-size:10.5px; padding:4px 10px; cursor:pointer; }
  .win .addrbar { flex: 0 0 24px; background:#ECE9D8; display:flex; align-items:center; padding:2px 8px; gap:6px; font-size:11px; border-bottom:1px solid #D4D0C8;}
  .win .addrbar input { flex:1; font-size:11px; border:1px solid #000; box-shadow: inset 1px 1px 0 #808080; padding:2px 4px; font-family: Tahoma, sans-serif;}
  .win .body {
    flex: 1; background: #fff; border: 1px inset #808080; margin: 3px;
    overflow: auto; padding: 10px; font-size: 12px; color:#000;
  }
  .win .resize-handle { position:absolute; right:0; bottom:0; width:14px; height:14px; cursor: nwse-resize; }

  a { color: #0000EE; text-decoration: underline; cursor:pointer; }
  a:visited { color: #551A8B; }

  button.retro, input[type=button], .btn98 {
    background:#ECE9D8; border:1px solid #000;
    box-shadow: inset 1px 1px 0 #fff, inset -1px -1px 0 #808080;
    font-family: Tahoma, sans-serif; font-size:11.5px; padding:4px 12px; cursor:pointer;
  }
  button.retro:active, .btn98:active { box-shadow: inset -1px -1px 0 #fff, inset 1px 1px 0 #808080; }
  input.field98, textarea.field98 {
    border:1px solid #000; box-shadow: inset 1px 1px 0 #808080; background:#fff;
    font-family: Tahoma, sans-serif; font-size:12px; padding:4px;
  }
  .sep { border-top: 1px solid #D4D0C8; margin: 8px 0; }

  /* mail */
  .mail-row { padding:5px 6px; cursor:pointer; border-bottom:1px solid #eee; }
  .mail-row:hover { background:#EAF2FB; }
  .mail-row.unread { font-weight:bold; }
  .mail-read { background:#F7F7F7; border:1px solid #ccc; padding:10px; margin-top:8px; }

  /* GATE tracker */
  .gate-item { display:flex; align-items:center; gap:8px; padding:4px 0; }
  .gate-bar-outer { border:1px solid #000; box-shadow: inset 1px 1px 0 #808080; height:18px; background:#fff; margin:8px 0; }
  .gate-bar-inner { height:100%; background:#2E7D32; width:0%; transition: width .3s; }

  /* taskbar */
  #taskbar {
    position:absolute; left:0; right:0; bottom:0; height:34px;
    background:#ECE9D8; border-top:2px solid #fff;
    display:flex; align-items:center; padding:3px 4px; gap:6px; z-index:5000;
  }
  #start-btn {
    background:#ECE9D8; border:1px solid #000;
    box-shadow: inset 1px 1px 0 #fff, inset -1px -1px 0 #808080;
    font-weight:bold; font-size:12.5px; padding:4px 10px; cursor:pointer;
    display:flex; align-items:center; gap:6px;
  }
  #taskbar-buttons { flex:1; display:flex; gap:4px; overflow:hidden; }
  .taskbtn {
    background:#ECE9D8; border:1px solid #000;
    box-shadow: inset 1px 1px 0 #fff, inset -1px -1px 0 #808080;
    font-size:11px; padding:4px 10px; cursor:pointer; max-width:160px;
    white-space:nowrap; overflow:hidden; text-overflow:ellipsis;
  }
  .taskbtn.active { box-shadow: inset -1px -1px 0 #fff, inset 1px 1px 0 #808080; }
  #clock {
    background:#ECE9D8; border:1px solid #808080; box-shadow: inset 1px 1px 0 #fff;
    font-size:11px; padding:5px 10px;
  }
  #start-menu {
    position:absolute; left:2px; bottom:36px; width:230px;
    background:#ECE9D8; border:2px solid #000; box-shadow: 3px 3px 0 rgba(0,0,0,0.4);
    display:none; z-index:6000; padding:4px 0;
  }
  #start-menu.open { display:block; }
  #start-menu .smitem { padding:7px 14px; font-size:12.5px; cursor:pointer; display:flex; align-items:center; gap:10px; }
  #start-menu .smitem:hover { background:#0A246A; color:#fff; }
  #start-menu .smsep { border-top:1px solid #D4D0C8; margin:4px 0; }

  .colorword span:nth-child(1){color:#3369E8}
  .colorword span:nth-child(2){color:#D50F25}
  .colorword span:nth-child(3){color:#EEB211}
  .colorword span:nth-child(4){color:#3369E8}
  .colorword span:nth-child(5){color:#009925}
  .colorword span:nth-child(6){color:#D50F25}
  .colorword span:nth-child(7){color:#EEB211}
  .colorword span:nth-child(8){color:#3369E8}
</style>
</head>
<body>

<div id="boot">
  <div>Dhanush98 (C) 1998-2026 Hadhaan Technologies Pvt. Ltd.</div>
  <div>&nbsp;</div>
  <div>Detecting curiosity module............. OK</div>
  <div>Detecting coffee reserves................ OK</div>
  <div>Loading GATE_DA_2027.SYS.................. OK</div>
  <div>Mounting HADHAAN.DRV...................... OK</div>
  <div>Starting Dhanush98<span class="cursor"></span></div>
  <div class="bar-outer"><div class="bar-inner"></div></div>
</div>

<div id="desktop">

  <div id="icons">
    <div class="icon" data-win="search"><div class="glyph" style="background:#fff;">&#128269;</div><div class="label">Dhanush! Search</div></div>
    <div class="icon" data-win="mail"><div class="glyph" style="background:#CFE8E8;">&#9993;</div><div class="label">Pluto Mail</div></div>
    <div class="icon" data-win="hadhaan"><div class="glyph" style="background:#F2C36B;">&#128188;</div><div class="label">Hadhaan.com</div></div>
    <div class="icon" data-win="samiksha"><div class="glyph" style="background:#C9B6E4;">&#127891;</div><div class="label">Samiksha</div></div>
    <div class="icon" data-win="gate"><div class="glyph" style="background:#FFE8A3;">&#128197;</div><div class="label">GATE DA 2027</div></div>
    <div class="icon" data-win="ask"><div class="glyph" style="background:#FBF6E3;">&#128172;</div><div class="label">Ask Dhanush</div></div>
    <div class="icon" data-win="panel"><div class="glyph" style="background:#DADADA;">&#9881;</div><div class="label">Control Panel</div></div>
    <div class="icon" data-win="connect"><div class="glyph" style="background:#B58ED6;">&#9742;</div><div class="label">Dial-Up Connect</div></div>
  </div>

  <!-- ================= SEARCH ================= -->
  <div class="win" id="win-search" style="left:220px; top:40px; width:480px; height:340px;">
    <div class="titlebar"><div class="ticon">&#128269;</div><div class="ttext">Dhanush! - Home</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="menubar"><span style="margin-right:16px;">File</span><span style="margin-right:16px;">Edit</span><span style="margin-right:16px;">View</span><span style="margin-right:16px;">Favorites</span><span>Help</span></div>
    <div class="addrbar"><span>Address</span><input class="field98" readonly value="http://www.hadhaan.com/"/></div>
    <div class="body" style="text-align:center; padding-top:24px;">
      <div class="colorword" style="font-family:Georgia,serif; font-weight:bold; font-size:40px;">
        <span>D</span><span>h</span><span>a</span><span>n</span><span>u</span><span>s</span><span>h</span><span>!</span>
      </div>
      <div style="margin:8px 0 16px; font-size:12px;">Search the web using Dhanush</div>
      <input class="field98" id="search-input" style="width:70%; max-width:320px;" placeholder="AI &middot; startups &middot; DSA &middot; Hadhaan"/>
      <div style="margin-top:12px;">
        <button class="retro" id="search-go">Dhanush Search</button>
        <button class="retro" id="search-lucky">Feeling Curious</button>
      </div>
      <div id="search-results" style="text-align:left; margin-top:16px; font-size:12px;"></div>
      <div style="margin-top:20px; font-size:11px;"><a href="https://hadhaan.com" target="_blank">Hadhaan.com</a> &middot; <a href="https://www.linkedin.com/in/dhanush-k-aka-matrix/" target="_blank">About Dhanush</a></div>
    </div>
  </div>

  <!-- ================= MAIL ================= -->
  <div class="win" id="win-mail" style="left:120px; top:400px; width:460px; height:300px;">
    <div class="titlebar"><div class="ticon">&#9993;</div><div class="ttext">Pluto Mail - Inbox</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="toolbar">
      <div class="tbtn">Read</div><div class="tbtn">Write</div><div class="tbtn">Reply</div><div class="tbtn">Delete</div>
    </div>
    <div class="body" id="mail-body">
      <div id="mail-list">
        <div class="mail-row unread" data-mail="manush">&#9993; <b>Manush G</b> &mdash; pipeline review 3pm today</div>
        <div class="mail-row unread" data-mail="gate">&#9993; <b>GATE DA Cell</b> &mdash; mock test results are in</div>
        <div class="mail-row" data-mail="hadhaan">&#9993; Hadhaan Ops &mdash; deploy checklist for Simcuit</div>
      </div>
      <div id="mail-reader"></div>
    </div>
  </div>

  <!-- ================= HADHAAN ================= -->
  <div class="win hidden" id="win-hadhaan" style="left:640px; top:60px; width:340px; height:260px;">
    <div class="titlebar"><div class="ticon">&#128188;</div><div class="ttext">Hadhaan.com - Portal</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body">
      <h3 style="margin:0 0 6px; color:#8a4b00;">Hadhaan Technologies Pvt. Ltd.</h3>
      <div class="sep"></div>
      <p style="margin:6px 0;">Building from the ground up, one shipped feature at a time.</p>
      <ul style="margin:6px 0 0 18px; padding:0;">
        <li>Dhanush K &mdash; Co-founder &amp; CPTO</li>
        <li>Manush G &mdash; Co-founder &amp; CEO</li>
      </ul>
      <div style="background:#fff4da; border:1px solid #e0a030; padding:8px; margin-top:12px; font-size:11.5px;">
        NEW: Simcuit is now in private beta.
      </div>
    </div>
  </div>

  <!-- ================= SAMIKSHA ================= -->
  <div class="win hidden" id="win-samiksha" style="left:660px; top:340px; width:320px; height:250px;">
    <div class="titlebar"><div class="ticon">&#127891;</div><div class="ttext">Samiksha - Learning</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body">
      <h3 style="margin:0 0 4px; color:#4B2E83;">SAMIKSHA</h3>
      <div style="font-size:11px; color:#555;">Learning Solutions Portal</div>
      <div class="sep"></div>
      <div><a>Courses</a></div>
      <div><a>Mentors</a></div>
      <div><a>Assessments</a></div>
      <div><a>Community</a></div>
    </div>
  </div>

  <!-- ================= GATE DA TRACKER ================= -->
  <div class="win hidden" id="win-gate" style="left:260px; top:80px; width:380px; height:340px;">
    <div class="titlebar"><div class="ticon">&#128197;</div><div class="ttext">GATE DA 2027 - Prep Tracker</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body">
      <b>Syllabus checklist</b>
      <div id="gate-list">
        <label class="gate-item"><input type="checkbox" class="gate-check"/> Linear Algebra &amp; Probability</label>
        <label class="gate-item"><input type="checkbox" class="gate-check"/> DSA &amp; Programming</label>
        <label class="gate-item"><input type="checkbox" class="gate-check"/> Machine Learning</label>
        <label class="gate-item"><input type="checkbox" class="gate-check"/> Statistics</label>
        <label class="gate-item"><input type="checkbox" class="gate-check"/> Deep Learning basics</label>
        <label class="gate-item"><input type="checkbox" class="gate-check"/> Aptitude &amp; General English</label>
      </div>
      <div class="gate-bar-outer"><div class="gate-bar-inner" id="gate-bar"></div></div>
      <div id="gate-pct" style="font-size:11.5px;">0% covered</div>
      <div class="sep"></div>
      <div style="font-size:11px; color:#555;">Progress saves automatically in this browser.</div>
    </div>
  </div>

  <!-- ================= ASK DHANUSH ================= -->
  <div class="win hidden" id="win-ask" style="left:340px; top:420px; width:360px; height:260px;">
    <div class="titlebar"><div class="ticon">&#128172;</div><div class="ttext">Ask Dhanush - Q&amp;A</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body" style="background:#FBF6E3;">
      <div style="text-align:center; font-family:Georgia,serif; font-weight:bold; font-size:18px; color:#8a1f1f;">Ask Dhanush</div>
      <div style="text-align:center; font-style:italic; font-size:11px; margin-bottom:10px;">Got a question? Just type it in and ask!</div>
      <input class="field98" id="ask-input" style="width:100%;" placeholder="how do I go from EEE to software?"/>
      <div style="text-align:center; margin-top:8px;"><button class="retro" id="ask-btn">Ask!</button></div>
      <div id="ask-answer" style="margin-top:12px; font-size:12px;"></div>
    </div>
  </div>

  <!-- ================= CONTROL PANEL ================= -->
  <div class="win hidden" id="win-panel" style="left:700px; top:120px; width:340px; height:300px;">
    <div class="titlebar"><div class="ticon">&#9881;</div><div class="ttext">Control Panel - Stack &amp; Status</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body">
      <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0; border-bottom:1px solid #eee;">
        <span>Coffee level</span><input type="range" id="coffee" min="0" max="100" value="70"/>
      </div>
      <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0; border-bottom:1px solid #eee;">
        <span>Chaos mode</span><input type="checkbox" id="chaos"/>
      </div>
      <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0; border-bottom:1px solid #eee;">
        <span>Debug mode</span><input type="checkbox" id="debugmode" checked/>
      </div>
      <div id="panel-msg" style="margin-top:12px; font-size:11.5px; color:#555;">System status: nominal.</div>
    </div>
  </div>

  <!-- ================= DIAL-UP CONNECT ================= -->
  <div class="win hidden" id="win-connect" style="left:200px; top:180px; width:420px; height:230px;">
    <div class="titlebar"><div class="ticon">&#9742;</div><div class="ttext">Dial-Up Connection - Dhanush</div>
      <div class="capbtn" data-act="min">_</div><div class="capbtn" data-act="max">&#9633;</div><div class="capbtn" data-act="close">X</div></div>
    <div class="body" style="text-align:center;">
      <div id="connect-status" style="font-weight:bold; margin-bottom:6px;">Connecting to the outside world&hellip;</div>
      <div class="gate-bar-outer" style="width:80%; margin:0 auto;"><div class="gate-bar-inner" id="connect-bar" style="background:#0A246A;"></div></div>
      <div style="margin-top:16px; display:flex; justify-content:center; gap:14px;">
        <a href="https://www.linkedin.com/in/dhanush-k-aka-matrix/" target="_blank" class="btn98">LinkedIn</a>
        <a href="https://x.com/dhanushk_" target="_blank" class="btn98">X / Twitter</a>
        <a href="https://hadhaan.com" target="_blank" class="btn98">Portfolio</a>
      </div>
    </div>
  </div>

</div>

<div id="taskbar">
  <div id="start-btn"><span>&#8801;</span> Start</div>
  <div id="taskbar-buttons"></div>
  <div id="clock"></div>
</div>

<div id="start-menu">
  <div class="smitem" data-win="search">&#128269; Dhanush! Search</div>
  <div class="smitem" data-win="mail">&#9993; Pluto Mail</div>
  <div class="smitem" data-win="hadhaan">&#128188; Hadhaan.com</div>
  <div class="smitem" data-win="samiksha">&#127891; Samiksha</div>
  <div class="smitem" data-win="gate">&#128197; GATE DA 2027</div>
  <div class="smitem" data-win="ask">&#128172; Ask Dhanush</div>
  <div class="smitem" data-win="panel">&#9881; Control Panel</div>
  <div class="smitem" data-win="connect">&#9742; Dial-Up Connect</div>
  <div class="smsep"></div>
  <div class="smitem" id="shutdown-item">&#9211; Shut Down...</div>
</div>

<script>
(function(){
  var boot = document.getElementById('boot');
  setTimeout(function(){ boot.classList.add('hide'); }, 2000);

  var windows = {};
  document.querySelectorAll('.win').forEach(function(w){
    windows[w.id.replace('win-','')] = w;
  });

  var zTop = 10;
  var openList = [];
  var taskbarButtons = document.getElementById('taskbar-buttons');

  function bringToFront(key){
    zTop += 1;
    windows[key].style.zIndex = zTop;
    document.querySelectorAll('.taskbtn').forEach(function(b){ b.classList.remove('active'); });
    var tb = document.getElementById('task-'+key);
    if (tb) tb.classList.add('active');
  }

  function openWin(key){
    var w = windows[key];
    if (!w) return;
    w.classList.remove('hidden');
    bringToFront(key);
    if (!document.getElementById('task-'+key)){
      var btn = document.createElement('div');
      btn.className = 'taskbtn';
      btn.id = 'task-'+key;
      btn.textContent = w.querySelector('.ttext').textContent;
      btn.onclick = function(){
        if (w.classList.contains('hidden')){
          w.classList.remove('hidden');
          bringToFront(key);
        } else {
          w.classList.add('hidden');
          document.querySelectorAll('.taskbtn').forEach(function(b){ b.classList.remove('active'); });
        }
      };
      taskbarButtons.appendChild(btn);
    }
  }

  function closeWin(key){
    windows[key].classList.add('hidden');
    var tb = document.getElementById('task-'+key);
    if (tb) tb.remove();
  }

  document.querySelectorAll('.icon').forEach(function(ic){
    ic.addEventListener('click', function(){ openWin(ic.dataset.win); });
  });
  document.querySelectorAll('#start-menu .smitem[data-win]').forEach(function(it){
    it.addEventListener('click', function(){
      openWin(it.dataset.win);
      document.getElementById('start-menu').classList.remove('open');
    });
  });

  document.getElementById('start-btn').addEventListener('click', function(e){
    document.getElementById('start-menu').classList.toggle('open');
    e.stopPropagation();
  });
  document.addEventListener('click', function(e){
    var sm = document.getElementById('start-menu');
    if (!sm.contains(e.target) && e.target.id !== 'start-btn' && !document.getElementById('start-btn').contains(e.target)){
      sm.classList.remove('open');
    }
  });
  document.getElementById('shutdown-item').addEventListener('click', function(){
    document.body.innerHTML = '<div style="background:#000;color:#fff;height:100vh;display:flex;align-items:center;justify-content:center;font-family:Tahoma,sans-serif;font-size:20px;">It is now safe to close this tab.</div>';
  });

  document.querySelectorAll('.win').forEach(function(w){
    var key = w.id.replace('win-','');
    w.addEventListener('mousedown', function(){ bringToFront(key); });
    var bar = w.querySelector('.titlebar');
    var drag = null;
    bar.addEventListener('mousedown', function(e){
      if (e.target.classList.contains('capbtn')) return;
      var rect = w.getBoundingClientRect();
      drag = { dx: e.clientX - rect.left, dy: e.clientY - rect.top };
      bringToFront(key);
      e.preventDefault();
    });
    document.addEventListener('mousemove', function(e){
      if (!drag) return;
      var deskRect = document.getElementById('desktop').getBoundingClientRect();
      var nx = e.clientX - drag.dx - deskRect.left;
      var ny = e.clientY - drag.dy - deskRect.top;
      nx = Math.max(0, Math.min(nx, deskRect.width - 80));
      ny = Math.max(0, Math.min(ny, deskRect.height - 40));
      w.style.left = nx + 'px';
      w.style.top = ny + 'px';
    });
    document.addEventListener('mouseup', function(){ drag = null; });

    w.querySelectorAll('.capbtn').forEach(function(btn){
      btn.addEventListener('click', function(e){
        e.stopPropagation();
        var act = btn.dataset.act;
        if (act === 'close') closeWin(key);
        else if (act === 'min') {
          w.classList.add('hidden');
          document.querySelectorAll('.taskbtn').forEach(function(b){ b.classList.remove('active'); });
        }
        else if (act === 'max') {
          if (w.dataset.maxed === '1'){
            w.style.width = w.dataset.pw; w.style.height = w.dataset.ph;
            w.style.left = w.dataset.pl; w.style.top = w.dataset.pt;
            w.dataset.maxed = '0';
          } else {
            w.dataset.pw = w.style.width; w.dataset.ph = w.style.height;
            w.dataset.pl = w.style.left; w.dataset.pt = w.style.top;
            var deskRect = document.getElementById('desktop').getBoundingClientRect();
            w.style.left = '4px'; w.style.top = '4px';
            w.style.width = (deskRect.width-14)+'px'; w.style.height = (deskRect.height-46)+'px';
            w.dataset.maxed = '1';
          }
        }
      });
    });
  });

  openWin('search');

  function tick(){
    var d = new Date();
    var h = d.getHours(); var m = d.getMinutes();
    var ampm = h >= 12 ? 'PM' : 'AM';
    var hh = h % 12; if (hh === 0) hh = 12;
    var mm = (m < 10 ? '0' : '') + m;
    document.getElementById('clock').textContent = hh + ':' + mm + ' ' + ampm;
  }
  tick(); setInterval(tick, 15000);

  var searchResults = [
    ['hadhaan.com &mdash; official site', 'Flagship startup. Building every layer from the ground up.'],
    ['GATE DA 2027 prep log', 'Probability, algorithms, transformers, business fundamentals.'],
    ['Ask Dhanush: EEE to software', 'How a self-taught path led from circuits to shipped code.'],
    ['Samiksha Learning Solutions', 'Co-founded platform for structured, mentor-backed learning.']
  ];
  function runSearch(){
    var box = document.getElementById('search-results');
    var q = document.getElementById('search-input').value.trim();
    var html = '<div style="font-size:11px; color:#555; margin-bottom:6px;">Results ' + (q? 'for "'+q+'"' : '') + ':</div>';
    searchResults.forEach(function(r){
      html += '<div style="margin-bottom:8px;"><a>'+r[0]+'</a><div style="font-size:11px; color:#333;">'+r[1]+'</div></div>';
    });
    box.innerHTML = html;
  }
  document.getElementById('search-go').addEventListener('click', runSearch);
  document.getElementById('search-lucky').addEventListener('click', function(){
    var box = document.getElementById('search-results');
    box.innerHTML = '<div style="margin-top:10px;"><b>Feeling curious result:</b> Simcuit is currently in private beta. Ask Dhanush about it in the Ask Dhanush window.</div>';
  });
  document.getElementById('search-input').addEventListener('keydown', function(e){ if (e.key === 'Enter') runSearch(); });

  var mails = {
    manush: { from: 'Manush G', subj: 'pipeline review 3pm today', body: 'Hey, quick reminder we have the pipeline review at 3pm. Bring the latest Simcuit numbers.' },
    gate: { from: 'GATE DA Cell', subj: 'mock test results are in', body: 'Your latest mock test results are ready. Quant and DSA are strong, revisit Stats this week.' },
    hadhaan: { from: 'Hadhaan Ops', subj: 'deploy checklist for Simcuit', body: 'Please run through the deploy checklist before pushing the Simcuit build to staging.' }
  };
  document.querySelectorAll('.mail-row').forEach(function(row){
    row.addEventListener('click', function(){
      row.classList.remove('unread');
      var m = mails[row.dataset.mail];
      document.getElementById('mail-reader').innerHTML =
        '<div class="mail-read"><b>From:</b> '+m.from+'<br/><b>Subject:</b> '+m.subj+'<div class="sep"></div>'+m.body+'</div>';
    });
  });

  var gateChecks = document.querySelectorAll('.gate-check');
  var gateKey = 'dhanush98-gate';
  try {
    var saved = JSON.parse(localStorage.getItem(gateKey) || '[]');
    gateChecks.forEach(function(c, i){ c.checked = !!saved[i]; });
  } catch(e){}
  function updateGate(){
    var total = gateChecks.length, done = 0;
    gateChecks.forEach(function(c){ if (c.checked) done++; });
    var pct = Math.round(done/total*100);
    document.getElementById('gate-bar').style.width = pct + '%';
    document.getElementById('gate-pct').textContent = pct + '% covered';
    try { localStorage.setItem(gateKey, JSON.stringify(Array.from(gateChecks).map(function(c){return c.checked;}))); } catch(e){}
  }
  gateChecks.forEach(function(c){ c.addEventListener('change', updateGate); });
  updateGate();

  var askAnswers = [
    'Dhanush suggests starting with one small project and finishing it, before starting the next one.',
    'Curiosity beats a syllabus every time. Pick something confusing and take it apart.',
    'Cold coffee and CLRS. That is the whole secret.',
    'Ask Hadhaan.com, they might already be building it.',
    'The attack surface is half the system. Learn how things break.'
  ];
  document.getElementById('ask-btn').addEventListener('click', function(){
    var input = document.getElementById('ask-input');
    var box = document.getElementById('ask-answer');
    if (!input.value.trim()){
      box.innerHTML = '<span style="color:#8a1f1f;">Type a question first.</span>';
      return;
    }
    var ans = askAnswers[Math.floor(Math.random()*askAnswers.length)];
    box.innerHTML = '<b>Q:</b> '+input.value+'<br/><b>A:</b> '+ans;
  });

  document.getElementById('chaos').addEventListener('change', function(){
    var msg = document.getElementById('panel-msg');
    if (this.checked){
      document.getElementById('icons').style.transition = 'transform .3s';
      document.getElementById('icons').style.animation = 'wiggle .4s infinite';
      var style = document.createElement('style');
      style.innerHTML = '@keyframes wiggle{0%{transform:rotate(0)}25%{transform:rotate(1deg)}75%{transform:rotate(-1deg)}}';
      document.head.appendChild(style);
      msg.textContent = 'System status: mild chaos detected. Icons are vibrating.';
    } else {
      document.getElementById('icons').style.animation = 'none';
      msg.textContent = 'System status: nominal.';
    }
  });
  document.getElementById('coffee').addEventListener('input', function(){
    var msg = document.getElementById('panel-msg');
    var v = this.value;
    if (v < 20) msg.textContent = 'Coffee level low. Productivity at risk.';
    else if (v > 80) msg.textContent = 'Coffee level high. Typing speed: excessive.';
    else msg.textContent = 'System status: nominal.';
  });

  var connectPct = 0;
  var connectInterval = setInterval(function(){
    connectPct += 4;
    if (connectPct >= 100){
      connectPct = 100;
      document.getElementById('connect-status').textContent = 'Connected at 56.6 Kbps.';
      clearInterval(connectInterval);
    }
    document.getElementById('connect-bar').style.width = connectPct + '%';
  }, 120);

})();
</script>

</body>
</html>
