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
      width: 100%;
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
