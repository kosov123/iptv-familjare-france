hls.js# iptv-familjare
shikim i kendshem familjar
<!DOCTYPE html>
<html lang="sq">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>📡 IPTV Familjare</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #0b132b;
      color: white;
      text-align: center;
      margin: 0;
      padding: 0;
    }
    h1 {
      background: #1c2541;
      padding: 20px;
      margin: 0;
      font-size: 24px;
    }
    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
      padding: 20px;
    }
    .card {
      background: #3a506b;
      border-radius: 12px;
      padding: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.5);
    }
    video {
      width: 100%;<!doctype html>
<html lang="sq">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>IPTV Familjare — Kategoritë</title>

  <style>
    :root{
      --bg:#071028; --panel:#0f1a2b; --card:#122235; --accent:#3ecf8e; --muted:#9fb2d7;
      --text:#e6eef6;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,Arial,Helvetica,sans-serif;background:linear-gradient(180deg,var(--bg),#081428);color:var(--text)}
    header{background:linear-gradient(90deg,#0b1b33,#0d2a45);padding:14px 18px;display:flex;align-items:center;justify-content:space-between}
    header h1{margin:0;font-size:18px}
    .subtitle{opacity:.85;font-size:13px}
    nav{display:flex;gap:8px;padding:12px 18px;background:var(--panel);overflow:auto}
    .tab{padding:8px 12px;border-radius:8px;background:transparent;border:1px solid rgba(255,255,255,0.03);cursor:pointer;color:var(--muted);white-space:nowrap}
    .tab.active{background:linear-gradient(90deg,var(--accent),#65e2ab);color:#04121a;font-weight:700}
    .container{max-width:1200px;margin:18px auto;padding:0 16px}
    .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:14px}
    .card{background:var(--card);border-radius:12px;padding:10px;display:flex;flex-direction:column;gap:8px;box-shadow:0 8px 30px rgba(2,8,23,.6)}
    .card .meta{font-size:13px;color:var(--muted)}
    .play{margin-top:auto;padding:8px 12px;border-radius:8px;background:linear-gradient(90deg,var(--accent),#5be8a1);border:none;color:#02121a;cursor:pointer;font-weight:700}
    /* modal */
    .modal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(1,6,20,.75);z-index:9999;padding:18px}
    .modal.open{display:flex}
    .player-box{width:100%;max-width:1100px;background:#051428;border-radius:12px;padding:12px}
    .player-top{display:flex;justify-content:space-between;align-items:center;gap:10px}
    .player-title{font-size:16px;margin:0}
    .close-btn{background:transparent;border:0;color:var(--text);font-size:22px;cursor:pointer}
    iframe, video{width:100%;height:540px;border-radius:8px;background:black}
    @media (max-width:800px){ iframe,video{height:260px} }
    .footer{max-width:1200px;margin:18px auto;padding:12px 16px;color:var(--muted);font-size:13px}
  </style>

  <!-- hls.js për M3U8 -->
  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
</head>
<body>

<header>
  <div>
    <h1>📺 IPTV Familjare</h1>
    <div class="subtitle">Zgjidh kategori dhe kliko "LUAJ" — vetëm kanale publike/ligjore</div>
  </div>
  <div style="font-size:13px;opacity:.85">Version demo</div>
</header>

<!-- Menu kategori -->
<nav id="tabs">
  <div class="tab active" data-cat="all">Të GJITHA</div>
  <div class="tab" data-cat="shqip">Shqip/Kosovë</div>
  <div class="tab" data-cat="turqi">Turqi</div>
  <div class="tab" data-cat="lajme">Lajme</div>
  <div class="tab" data-cat="sport">Sport</div>
  <div class="tab" data-cat="muzike">Muzikë</div>
  <div class="tab" data-cat="dokumentar">Dokumentarë</div>
  <div class="tab" data-cat="femije">Fëmijë</div>
</nav>

<div class="container">
  <div id="grid" class="grid"></div>
</div>

<div class="footer">Shtoni vetëm kanale publike/zyrtare. Për kanale me pagesë duhet licencë.</div>

<!-- Modal player -->
<div id="modal" class="modal" aria-hidden="true">
  <div class="player-box" role="dialog" aria-modal="true">
    <div class="player-top">
      <h3 id="playerTitle" class="player-title">Duke u ngarkuar...</h3>
      <button id="close" class="close-btn" title="Mbyll">✕</button>
    </div>
    <div id="playerWrap" style="margin-top:10px"></div>
    <div style="margin-top:8px;color:#9fb2d7;font-size:13px">Për HLS: në TV përdor Chrome/Edge apo pajisje që mbështesin HLS.</div>
  </div>
</div>

<script>
/* Lista e kanaleve - SIGURISHT vetëm burime publike/zyrtare.
   Mund t'i shtosh vetë më shumë objekte sipas udhëzimeve më poshtë.
   Fusha: id, title, category (një nga: shqip,turqi,lajme,sport,muzike,dokumentar,femije), type ('hls' ose 'youtube'), src (embed ose m3u8)
*/
const channels = [
  // Shqiptare / Kosovare (shembull me burime publike kur të disponueshme)
  {id:1, title:'RTSH 24 (Shqipëri)', category:'shqip', type:'hls', src:'https://stream.rtsh.al/rtsh_live/rtsh24/playlist.m3u8'},
  {id:2, title:'RTK 1 (Kosovë)', category:'shqip', type:'youtube', src:'https://www.youtube.com/embed/HQ1KfKUPgR4'},
  {id:3, title:'RTSH 1 (Shqipëri)', category:'shqip', type:'hls', src:'https://stream.rtsh.al/rtsh_live/rtsh1/playlist.m3u8'},
  {id:4, title:'RTV21 Info (Kosovë)', category:'shqip', type:'youtube', src:'https://www.youtube.com/embed/EXAMPLE_RTV21'},

  // Turqia
  {id:10, title:'TRT World (Anglisht)', category:'turqi', type:'youtube', src:'https://www.youtube.com/embed/J8x7tIh9lvk'},
  {id:11, title:'TRT Haber (TR)', category:'turqi', type:'youtube', src:'https://www.youtube.com/embed/EXAMPLE_TRT_HABER'},

  // Lajme ndërkombëtare
  {id:20, title:'France24 (EN)', category:'lajme', type:'hls', src:'https://static.france24.com/live/F24_EN_HI_HLS/live_web.m3u8'},
  {id:21, title:'DW News', category:'lajme', type:'hls', src:'https://dwstream3-lh.akamaihd.net/i/dwstream3_live@124967/master.m3u8'},
  {id:22, title:'Al Jazeera English', category:'lajme', type:'youtube', src:'https://www.youtube.com/embed/7LR3wRQD0Rk'},

  // Sport (kanale publike / Red Bull)
  {id:30, title:'Red Bull TV', category:'sport', type:'hls', src:'https://rbmn-live.akamaized.net/hls/live/590964/BoRB-AT/master.m3u8'},
  // (për evente sportive të drejtpërdrejta, kërko link zyrtar)

  // Muzikë / dokumentarë / fëmijë
  {id:40, title:'NASA TV', category:'dokumentar', type:'hls', src:'https://ntv1.akamaized.net/hls/live/2014075/NASA-NTV1/master.m3u8'},
  {id:41, title:'Arirang TV', category:'muzike', type:'hls', src:'https://amdlive-ch01.ctnd.com.edgesuite.net/arirang_1ch/smil:arirang_1ch.smil/playlist.m3u8'},
  {id:42, title:'CGTN Documentary', category:'dokumentar', type:'hls', src:'https://live.cgtn.com/500d/prog_index.m3u8'},
  {id:43, title:'Kids (Shembull Cartoon)', category:'femije', type:'youtube', src:'https://www.youtube.com/embed/EXAMPLE_KIDS'}
];

// Ndërtimi i grid bazuar në kategori
const grid = document.getElementById('grid');
const tabs = Array.from(document.querySelectorAll('.tab'));
let activeCat = 'all';

function renderList(){
  grid.innerHTML = '';
  const list = (activeCat === 'all') ? channels : channels.filter(c=>c.category===activeCat);
  if(list.length === 0){
    grid.innerHTML = '<div style="color:#9fb2d7;padding:12px">Nuk ka kanale për këtë kategori.</div>';
    return;
  }
  list.forEach(ch=>{
    const el = document.createElement('div');
    el.className = 'card';
    el.innerHTML = `
      <div style="padding:8px;display:flex;flex-direction:column;height:100%">
        <div style="font-weight:700">${ch.title}</div>
        <div class="meta">${ch.category.toUpperCase()}</div>
        <div style="flex:1"></div>
        <button class="play" data-id="${ch.id}">LUAJ</button>
      </div>
    `;
    grid.appendChild(el);
  });

  // event listener play
  document.querySelectorAll('.play').forEach(b=>{
    b.addEventListener('click', (e)=>{
      const id = Number(e.currentTarget.dataset.id);
      const ch = channels.find(x=>x.id===id);
      if(ch) openPlayer(ch);
    });
  });
}

// tabs click
tabs.forEach(t=>{
  t.addEventListener('click', ()=>{
    tabs.forEach(x=>x.classList.remove('active'));
    t.classList.add('active');
    activeCat = t.dataset.cat;
    renderList();
  });
});

// modal/player logic
const modal = document.getElementById('modal');
const playerWrap = document.getElementById('playerWrap');
const playerTitle = document.getElementById('playerTitle');
const closeBtn = document.getElementById('close');

closeBtn.addEventListener('click', closePlayer);
modal.addEventListener('click', (e)=>{ if(e.target===modal) closePlayer(); });

function openPlayer(ch){
  playerTitle.textContent = ch.title;
  playerWrap.innerHTML = '';

  if(ch.type === 'youtube'){
    const iframe = document.createElement('iframe');
    iframe.src = ch.src + '?autoplay=1&rel=0';
    iframe.setAttribute('allow','accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture');
    iframe.setAttribute('allowfullscreen','');
    playerWrap.appendChild(iframe);
  } else if(ch.type === 'hls'){
    const video = document.createElement('video');
    video.controls = true;
    video.autoplay = true;
    video.muted = false;
    playerWrap.appendChild(video);

    const hlsUrl = ch.src;
    if(Hls.isSupported()){
      const hls = new Hls();
      hls.loadSource(hlsUrl);
      hls.attachMedia(video);
      hls.on(Hls.Events.MANIFEST_PARSED, function() { video.play().catch(()=>{}); });
    } else if(video.canPlayType('application/vnd.apple.mpegurl')){
      video.src = hlsUrl;
      video.addEventListener('loadedmetadata', function(){ video.play().catch(()=>{}); });
    } else {
      playerWrap.innerHTML = '<div style="color:#f7b7b7;padding:12px">Ky shfletues nuk mbështet HLS. Përdor Chrome/Edge/Firefox.</div>';
    }
  } else {
    playerWrap.innerHTML = '<div style="color:#f7b7b7;padding:12px">Formati i panjohur.</div>';
  }

  modal.classList.add('open');
}

function closePlayer(){
  modal.classList.remove('open');
  playerWrap.innerHTML = '';
}

// inicializo
renderList();

/* SI SHTOJNË KANALET VETË:
   - Në listën 'channels' shto një objekt si:
     { id:100, title:'Emri Kanali', category:'sport', type:'hls', src:'https://.../playlist.m3u8' }
   - Për YouTube: type:'youtube' dhe src:'https://www.youtube.com/embed/VIDEOID'
   - Ruaj (Commit changes) -> Vercel përditëson faqen automatikisht.
   - MOS SHTONI kanale me pagesë pa licencë.
*/
</script>
</body>
</html>

      border-radius: 10px;
      background: black;
    }
    h3 {
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <h1>📺 IPTV Familjare – Kanale Live</h1>

  <div class="container">
    <div class="card">
      <h3>🇫🇷 France 24 (Anglisht)</h3>
      <video controls autoplay muted>
        <source src="https://static.france24.com/live/F24_EN_HI_HLS/live_web.m3u8" type="application/x-mpegURL">
      </video>
    </div>

    <div class="card">
      <h3>🇦🇱 RTK 1 (Kosovë)</h3>
      <video controls autoplay muted>
        <source src="https://iptv-all.lanesh4d0w.repl.co/kosovo/rtk1" type="application/x-mpegURL">
      </video>
    </div>

    <div class="card">
      <h3>🇦🇱 RTSH 24 (Shqipëri)</h3>
      <video controls autoplay muted>
        <source src="https://stream.rtsh.al/rtsh_live/rtsh24/playlist.m3u8" type="application/x-mpegURL">
      </video>
    </div>

    <div class="card">
      <h3>🌍 Euronews Albania</h3>
      <video controls autoplay muted>
        <source src="https://tv-trtworld.live.trt.com.tr/master.m3u8" type="application/x-mpegURL">
      </video>
    </div>
  </div>
</body>
</html>
