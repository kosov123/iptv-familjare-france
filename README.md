<!DOCTYPE html>
<html lang="sq">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>IPTV Familjare</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0b1628;
      color: white;
      text-align: center;
    }
    header {
      background: #12294d;
      padding: 15px;
      font-size: 20px;
      font-weight: bold;
    }
    .kanal {
      margin: 15px auto;
      background: #1e3357;
      width: 90%;
      max-width: 600px;
      padding: 10px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(255,255,255,0.1);
    }
    .kanal button {
      background: #29c86f;
      border: none;
      padding: 10px 20px;
      color: #000;
      font-weight: bold;
      border-radius: 8px;
      cursor: pointer;
    }
    video, iframe {
      width: 95%;
      max-width: 600px;
      height: 340px;
      border: none;
      border-radius: 10px;
      margin-top: 10px;
      background: black;
    }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
</head>
<body>

<header>📺 IPTV Familjare</header>

<div id="lista">
  <div class="kanal">
    <h3>RTSH 24</h3>
    <button onclick="luaj('https://stream.rtsh.al/rtsh_live/rtsh24/playlist.m3u8','hls')">Luaj</button>
  </div>
  <div class="kanal">
    <h3>France 24 (EN)</h3>
    <button onclick="luaj('https://static.france24.com/live/F24_EN_HI_HLS/live_web.m3u8','hls')">Luaj</button>
  </div>
  <div class="kanal">
    <h3>DW News</h3>
    <button onclick="luaj('https://dwstream3-lh.akamaihd.net/i/dwstream3_live@124967/master.m3u8','hls')">Luaj</button>
  </div>
  <div class="kanal">
    <h3>Red Bull TV</h3>
    <button onclick="luaj('https://rbmn-live.akamaized.net/hls/live/590964/BoRB-AT/master.m3u8','hls')">Luaj</button>
  </div>
  <div class="kanal">
    <h3>TRT World</h3>
    <button onclick="luaj('https://www.youtube.com/embed/J8x7tIh9lvk','yt')">Luaj</button>
  </div>
</div>

<div id="player"></div>

<script>
function luaj(src, tipi){
  const div = document.getElementById("player");
  div.innerHTML = "";
  if(tipi === "yt"){
    const iframe = document.createElement("iframe");
    iframe.src = src + "?autoplay=1";
    iframe.allow = "autoplay; fullscreen";
    div.appendChild(iframe);
  } else {
    const video = document.createElement("video");
    video.controls = true;
    video.autoplay = true;
    div.appendChild(video);
    if(Hls.isSupported()){
      const hls = new Hls();
      hls.loadSource(src);
      hls.attachMedia(video);
    } else if(video.canPlayType('application/vnd.apple.mpegurl')){
      video.src = src;
    } else {
      div.innerHTML = "<p>Nuk mbështetet HLS në këtë pajisje.</p>";
    }
  }
}
</script>

</body>
</html>
