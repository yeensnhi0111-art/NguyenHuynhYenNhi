# NguyenHuynhYenNhi
hocamini
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Hồ Cá Mini</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background: #0b192c;
      font-family: sans-serif;
    }
    .tank {
      position: relative;
      width: 720px;
      max-width: 95vw;
      height: 420px;
      border: 6px solid #4cc9f0;
      border-radius: 12px;
      overflow: hidden;
      background: linear-gradient(180deg, #1b9aaa 0%, #0b525b 75%, #062f35 100%);
      box-shadow: 0 12px 35px rgba(0, 0, 0, 0.5);
    }
    .sand {
      position: absolute;
      bottom: 0;
      width: 100%;
      height: 55px;
      background: #e9c46a;
      border-top: 4px solid #f4a261;
    }
    .fish {
      position: absolute;
      font-size: 36px;
      user-select: none;
      transition: transform 0.2s linear;
    }
    .bubble {
      position: absolute;
      bottom: 55px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.35);
      border: 1px solid rgba(255, 255, 255, 0.7);
      animation: rise linear forwards;
    }
    @keyframes rise {
      from { transform: translateY(0); opacity: 0.9; }
      to { transform: translateY(-360px); opacity: 0; }
    }
  </style>
</head>
<body>
  <div class="tank" id="tank">
    <div class="sand"></div>
  </div>

  <script>
    const tank = document.getElementById("tank");
    const icons = ["🐠", "🐟", "🐡"];
    const fishes = [];

    for (let i = 0; i < 6; i++) {
      const el = document.createElement("div");
      el.className = "fish";
      el.textContent = icons[i % icons.length];
      const fish = {
        el,
        x: Math.random() * 600 + 30,
        y: Math.random() * 260 + 30,
        vx: (Math.random() * 2 + 1) * (Math.random() < 0.5 ? 1 : -1),
        vy: (Math.random() - 0.5) * 1.2
      };
      tank.appendChild(el);
      fishes.push(fish);
    }

    function update() {
      const w = tank.clientWidth;
      const h = tank.clientHeight - 95;

      for (const f of fishes) {
        f.x += f.vx;
        f.y += f.vy;

        if (f.x <= 10 || f.x >= w - 45) f.vx *= -1;
        if (f.y <= 10 || f.y >= h) f.vy *= -1;

        const dir = f.vx >= 0 ? -1 : 1;
        f.el.style.left = `${f.x}px`;
        f.el.style.top = `${f.y}px`;
        f.el.style.transform = `scaleX(${dir})`;
      }
      requestAnimationFrame(update);
    }

    setInterval(() => {
      const b = document.createElement("div");
      const size = Math.random() * 10 + 6;
      b.className = "bubble";
      b.style.width = `${size}px`;
      b.style.height = `${size}px`;
      b.style.left = `${Math.random() * (tank.clientWidth - 40) + 20}px`;
      b.style.animationDuration = `${Math.random() * 2.5 + 2.5}s`;
      tank.appendChild(b);
      setTimeout(() => b.remove(), 5000);
    }, 450);

    update();
  </script>
</body>
</html>

