
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Brightway App</title>
  <style>
    body { background:#111; color:#fff; font-family:sans-serif; text-align:center; }
    .music-selector { display:flex; justify-content:center; gap:10px; margin:20px; }
    .music-option { font-size:2em; cursor:pointer; padding:10px; border-radius:10px; transition:0.3s; }
    .music-option.active { background:#444; }
  </style>
</head>
<body>
  <h1>🎶 Brightway App</h1>

  <!-- Panel de música -->
  <div class="music-selector">
    <div class="music-option" id="marioMusic" title="Música estilo Mario Bros">🍄</div>
    <div class="music-option active" id="megaloMusic" title="Música estilo Megalovania">💀</div>
    <div class="music-option" id="toyStoryMusic" title="Toy Story - Hay un amigo en mí">🤠</div>
    <div class="music-option" id="kungFuPandaMusic" title="Kung Fu Panda - Hero">🐼</div>
    <div class="music-option" id="spiderManMusic" title="Spider-Man - Main Titles">🕷️</div>
  </div>

  <button id="toggleMusic">▶️ / ⏸️ Música</button>

  <script>
    let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    let bgMusic = null;
    let musicOn = false;
    let musicVol = 0.5;
    let musicType = "megalo";

    function playClick() {
      const o = audioCtx.createOscillator();
      const g = audioCtx.createGain();
      o.connect(g); g.connect(audioCtx.destination);
      o.frequency.value = 600;
      o.start();
      o.stop(audioCtx.currentTime + 0.05);
    }

    // === Melodías ===
    const marioNotes = [
      {f:659.25,d:0.12},{f:659.25,d:0.24},{f:659.25,d:0.24},{f:523.25,d:0.12},
      {f:659.25,d:0.24},{f:783.99,d:0.48},{f:392,d:0.48},{f:523.25,d:0.36},
      {f:392,d:0.36},{f:329.63,d:0.36},{f:440,d:0.36},{f:493.88,d:0.32},
      {f:466.16,d:0.28},{f:440,d:0.32},{f:392,d:0.24},{f:659.25,d:0.24},
      {f:783.99,d:0.24},{f:880,d:0.28},{f:698.46,d:0.24},{f:783.99,d:0.24},
      {f:659.25,d:0.32},{f:523.25,d:0.24},{f:587.33,d:0.24},{f:493.88,d:0.32}
    ];

    const megaloNotes = [
      {f:293.66,d:0.15},{f:293.66,d:0.15},{f:587.33,d:0.3},{f:440,d:0.3},
      {f:415.3,d:0.25},{f:392,d:0.25},{f:349.23,d:0.25},{f:293.66,d:0.15},
      {f:349.23,d:0.15},{f:392,d:0.15},{f:261.63,d:0.15},{f:261.63,d:0.15},
      {f:587.33,d:0.3},{f:440,d:0.3},{f:415.3,d:0.25},{f:392,d:0.25},
      {f:349.23,d:0.25},{f:293.66,d:0.15},{f:349.23,d:0.15},{f:392,d:0.15}
    ];

    const toyStoryNotes = [
      {f:392,d:0.4},{f:440,d:0.4},{f:392,d:0.4},{f:349,d:0.4},
      {f:392,d:0.6},{f:330,d:0.6},{f:392,d:0.4},{f:523,d:0.6},
      {f:440,d:0.6},{f:392,d:0.6},{f:349,d:0.4},{f:330,d:0.4},
      {f:349,d:0.6},{f:392,d:0.6},{f:330,d:0.6},{f:294,d:0.6},
      {f:392,d:0.5},{f:440,d:0.5},{f:392,d:0.5},{f:349,d:0.5},
      {f:330,d:0.7},{f:392,d:0.7},{f:523,d:0.8},{f:440,d:0.8}
    ];

    const kungFuPandaNotes = [
      {f:392,d:0.5},{f:440,d:0.5},{f:466.16,d:0.5},{f:523.25,d:0.7},
      {f:587.33,d:0.6},{f:523.25,d:0.5},{f:466.16,d:0.5},{f:440,d:0.6},
      {f:392,d:0.7},{f:349.23,d:0.7},{f:392,d:0.6},{f:440,d:0.5},
      {f:466.16,d:0.6},{f:523.25,d:0.6},{f:587.33,d:0.7},{f:698.46,d:0.8},
      {f:587.33,d:0.7},{f:523.25,d:0.7},{f:440,d:0.7},{f:392,d:0.8},
      {f:349.23,d:0.8},{f:392,d:0.9},{f:466.16,d:1.0}
    ];

    const spiderManNotes = [
      {f:261.63,d:0.6},{f:329.63,d:0.6},{f:392,d:0.6},{f:523.25,d:0.8},
      {f:440,d:0.6},{f:392,d:0.6},{f:349.23,d:0.7},{f:329.63,d:0.7},
      {f:293.66,d:0.9},{f:261.63,d:0.6},{f:329.63,d:0.6},{f:392,d:0.6},
      {f:440,d:0.6},{f:523.25,d:0.8},{f:587.33,d:0.8},{f:523.25,d:0.7},
      {f:440,d:0.7},{f:392,d:0.7},{f:349.23,d:0.8},{f:293.66,d:0.9},
      {f:261.63,d:1.0}
    ];

    // === Control de música ===
    function stopMusic() {
      if (bgMusic && bgMusic.stop) bgMusic.stop();
      bgMusic = null;
    }

    function startMusic() {
      if (!musicOn) return;
      stopMusic();

      bgMusic = { g: audioCtx.createGain(), stop: null };
      bgMusic.g.connect(audioCtx.destination);
      bgMusic.g.gain.value = Math.min(musicVol * 1.8, 0.8);

      let notes;
      switch(musicType) {
        case 'mario': notes = marioNotes; break;
        case 'megalo': notes = megaloNotes; break;
        case 'toyStory': notes = toyStoryNotes; break;
        case 'kungFuPanda': notes = kungFuPandaNotes; break;
        case 'spiderMan': notes = spiderManNotes; break;
      }

      let shouldStop = false;
      bgMusic.stop = () => { shouldStop = true; };

      async function playMelody() {
        if (shouldStop || !musicOn) return;
        for (let note of notes) {
          if (shouldStop || !musicOn) break;
          await new Promise(resolve => {
            setTimeout(() => {
              if (shouldStop || !musicOn || !bgMusic) {
                resolve(); return;
              }
              const o = audioCtx.createOscillator();
              const g = audioCtx.createGain();
              o.connect(g); g.connect(bgMusic.g);
              o.frequency.value = note.f;
              o.type = 'triangle';
              const now = audioCtx.currentTime;
              g.gain.setValueAtTime(0, now);
              g.gain.linearRampToValueAtTime(0.4, now + 0.05);
              g.gain.linearRampToValueAtTime(0, now + note.d - 0.05);
              o.start(now);
              o.stop(now + note.d);
              setTimeout(resolve, note.d * 1000);
            }, 0);
          });
        }
        await new Promise(r => setTimeout(r, 400));
        if (musicOn && bgMusic && !shouldStop) playMelody();
      }

      playMelody();
    }

    // Botón toggle música
    document.getElementById("toggleMusic").onclick = () => {
      playClick();
      musicOn = !musicOn;
      if (musicOn) startMusic(); else stopMusic();
    };

    // === Botones de selección de melodía ===
    function setActiveMusic(id, type) {
      playClick();
      musicType = type;
      document.querySelectorAll('.music-option').forEach(el => el.classList.remove('active'));
      document.getElementById(id).classList.add('active');
      if (musicOn) startMusic();
    }

    document.getElementById('marioMusic').onclick = () => setActiveMusic('marioMusic','mario');
    document.getElementById('megaloMusic').onclick = () => setActiveMusic('megaloMusic','megalo');
    document.getElementById('toyStoryMusic').onclick = () => setActiveMusic('toyStoryMusic','toyStory');
    document.getElementById('kungFuPandaMusic').onclick = () => setActiveMusic('kungFuPandaMusic','kungFuPanda');
    document.getElementById('spiderManMusic').onclick = () => setActiveMusic('spiderManMusic','spiderMan');
  </script>
</body>
</html>
