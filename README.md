<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lale'ye Doğum Günü Sürprizi</title>
  <style>
    * { box-sizing: border-box; }
    body {
      background: #fdf1f1;
      margin: 0;
      padding: 0;
      height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', sans-serif;
      position: relative;
    }

    /* Kalp & Balon süsleri */
    .decor {
      position: absolute;
      font-size: 28px;
      animation: float 8s infinite ease-in-out;
      pointer-events: none;
      opacity: 0.6;
    }
    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); opacity: 0.4; }
      50% { opacity: 1; }
      100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
    }

    .envelope {
      width: 100vw;
      max-width: 600px;
      aspect-ratio: 3 / 2;
      position: relative;
      background: #ffffff;
      border: 2px solid #ccc;
      border-radius: 8px;
      cursor: pointer;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
      overflow: hidden;
      perspective: 1200px;
      z-index: 10;
    }

    .flap {
      position: absolute;
      width: 0;
      height: 0;
      border-left: 50% solid transparent;
      border-right: 50% solid transparent;
      border-bottom: 50% solid #eee;
      top: 0;
      left: 0;
      transform-origin: top center;
      transition: transform 1s ease;
      z-index: 2;
    }

    .letter {
      position: absolute;
      top: 120%;
      left: 5%;
      width: 90%;
      background: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      transition: top 2s ease;
      z-index: 1;
      font-size: 16px;
      line-height: 1.6;
      text-align: center;
    }

    .envelope.open .flap { transform: rotateX(-180deg); }
    .envelope.open .letter { top: 30px; }

    .particle {
      position: absolute;
      pointer-events: none;
      animation: rise 2s ease-out forwards;
    }

    @keyframes rise {
      0% { transform: scale(0) translateY(0); opacity: 1; }
      100% { transform: scale(1.3) translateY(-200px); opacity: 0; }
    }

    .heart { color: #e63946; font-size: 24px; }
    .firework {
      width: 4px;
      height: 4px;
      background: #ffd166;
      border-radius: 50%;
      box-shadow: 0 0 8px 2px #f4a261;
    }

    @media (max-width: 400px) {
      .letter {
        font-size: 14px;
        padding: 14px;
      }
    }
  </style>
</head>
<body>

<!-- Dekoratif Kalpler ve Balonlar -->
<script>
  const emojis = ['🎈', '❤️', '💖', '💝'];
  for (let i = 0; i < 40; i++) {
    const d = document.createElement('div');
    d.classList.add('decor');
    d.innerText = emojis[Math.floor(Math.random() * emojis.length)];
    d.style.left = Math.random() * 100 + 'vw';
    d.style.top = Math.random() * 100 + 'vh';
    d.style.animationDelay = (Math.random() * 5) + 's';
    document.body.appendChild(d);
  }
</script>

<div class="envelope" onclick="openEnvelope(this)">
  <div class="flap"></div>
  <div class="letter">
    <h3>🎉 Doğum Günün Kutlu Olsun Lale! 🎉</h3>
    <p>Yeni yaşın sana;<br>
    ✨ bol kahkahalı günler,<br>
    💖 sevgiyle dolu anlar,<br>
    🌟 hayallerine bir adım daha yaklaşacağın fırsatlar getirsin.</p>
    <p>İyi ki varsın, iyi ki doğmuşsun Lale!<br>
    Nice mutlu, sağlıklı, başarılı yıllara! 🍰🎁</p>
  </div>
</div>

<!-- MP3 müzik dosyası -->
<audio id="music" preload="auto">
  <source src="iyi-ki-dogdun-lale-isme-ozel-dogum-gunu-sarkisi_(mp3tur.com).mp3" type="audio/mp3">
  Tarayıcınız ses etiketini desteklemiyor.
</audio>

<script>
  function openEnvelope(el) {
    if (el.classList.contains("open")) return;
    el.classList.add("open");
    createParticles(30, 'heart');
    createParticles(30, 'firework');
    const music = document.getElementById('music');
    music.play().catch(() => {
      alert("🔇 Tarayıcı otomatik müzik çalmayı engelledi. Lütfen tekrar tıklayarak deneyin.");
    });
  }

  function createParticles(count, type) {
    for (let i = 0; i < count; i++) {
      const p = document.createElement('div');
      p.classList.add('particle');
      if (type === 'heart') {
        p.innerText = '❤';
        p.classList.add('heart');
      } else {
        p.classList.add('firework');
      }
      document.body.appendChild(p);
      const angle = Math.random() * 2 * Math.PI;
      const radius = Math.random() * 120;
      const x = window.innerWidth / 2 + Math.cos(angle) * radius;
      const y = window.innerHeight / 2 + Math.sin(angle) * radius;
      p.style.left = x + 'px';
      p.style.top = y + 'px';
      p.style.animationDelay = (Math.random() * 0.5) + 's';
      setTimeout(() => p.remove(), 2500);
    }
  }
</script>

</body>
</html>

