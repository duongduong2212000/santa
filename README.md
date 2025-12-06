<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8" />
<title>New Year Fortune Event</title>
<style>
  body {
    margin: 0;
    padding: 0;
    overflow: hidden;
    background: url('https://i.imgur.com/2yZq7oT.jpeg') center/cover no-repeat fixed;
    font-family: sans-serif;
  }

  #lion {
    position: absolute;
    width: 180px;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    transition: filter 0.3s ease;
  }

  .flash {
    filter: brightness(2) drop-shadow(0 0 20px yellow);
  }

  .lixi {
    position: absolute;
    width: 80px;
    cursor: pointer;
    transition: transform 0.5s ease, opacity 0.5s ease;
  }

  .spin { transform: rotate(720deg) scale(1.2); }

  .fall { animation: fallAnim 1.2s forwards ease-in; }

  @keyframes fallAnim {
    0% { transform: translateY(0); opacity: 1; }
    100% { transform: translateY(200px); opacity: 0; }
  }

  .bloom { animation: bloomAnim 0.6s forwards ease-out; }

  @keyframes bloomAnim {
    0% { transform: scale(1); filter: brightness(1); }
    100% { transform: scale(1.8); filter: brightness(2) drop-shadow(0 0 20px gold); opacity: 0; }
  }

  .firework {
    position: absolute;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: white;
    animation: explode 0.8s ease-out forwards;
  }

  @keyframes explode {
    0% { transform: scale(0.5) rotate(0deg); opacity: 1; }
    100% { transform: scale(3) rotate(360deg); opacity: 0; }
  }

  .firework:after {
    content: '✿';
    color: gold;
    font-size: 20px;
    position: absolute;
    transform: translate(-50%, -50%);
  }

  @keyframes rise {
    0% { transform: translateY(0); opacity: 1; }
    100% { transform: translateY(-80px); opacity: 0; }
  }

  @keyframes fallPetal {
    0% { transform: translateY(0) rotate(0deg); }
    100% { transform: translateY(700px) rotate(360deg); opacity: 0; }
  }
</style>
</head>
<body>

<audio id="bgm" src="https://files.catbox.moe/4x4k0y.mp3" autoplay loop></audio>

<img id="lion" src="https://i.imgur.com/En0Rm1G.png" />

<script>
const lion = document.getElementById('lion');
let angle = 0;

// Âm thanh
const soundFire = new Audio('https://www.myinstants.com/media/sounds/firework.mp3');
const soundThrow = new Audio('https://www.myinstants.com/media/sounds/pop.mp3');

// Di chuyển con lân vòng tròn
setInterval(() => {
  angle += 0.02;
  const radius = 200;
  const x = window.innerWidth / 2 + Math.cos(angle) * radius;
  const y = window.innerHeight / 2 + Math.sin(angle) * radius;
  lion.style.left = x + 'px';
  lion.style.top = y + 'px';
}, 16);

// Tung bao lì xì mỗi 2 giây
setInterval(() => {
  soundThrow.play();
  createLixi();

  lion.classList.add('flash');
  setTimeout(() => lion.classList.remove('flash'), 300);

  createFirework(lion.offsetLeft, lion.offsetTop);
}, 2000);

function createLixi() {
  const img = document.createElement('img');
  const randomId = Math.floor(Math.random()*6)+1;
  img.src = `https://i.imgur.com/0${randomId}lixi.png`;
  img.className = 'lixi';
  img.style.left = lion.offsetLeft + 'px';
  img.style.top = lion.offsetTop + 'px';
  document.body.appendChild(img);

  img.addEventListener('click', () => {
    img.classList.add('spin');

    // RANDOM TIỀN THEO TỈ LỆ
    const prizes = [
      { label: '2500 Naira', weight: 5 },
      { label: '1000 Naira', weight: 10 },
      { label: '800 Naira', weight: 20 },
      { label: '600 Naira', weight: 25 },
      { label: '500 Naira', weight: 30 },
      { label: 'Next time', weight: 10 }
    ];

    function weightedRandom(arr) {
      const total = arr.reduce((sum, item) => sum + item.weight, 0);
      let r = Math.random() * total;
      for (let i = 0; i < arr.length; i++) {
        if (r < arr[i].weight) return arr[i].label;
        r -= arr[i].weight;
      }
      return arr[arr.length - 1].label;
    }

    const moneyValue = weightedRandom(prizes);

    const money = document.createElement('div');
    money.innerText = moneyValue;
    money.style.position='absolute';
    money.style.left=img.style.left;
    money.style.top=img.style.top;
    money.style.fontSize='22px';
    money.style.fontWeight='bold';
    money.style.color='gold';
    money.style.textShadow='0 0 10px red';
    money.style.animation='rise 1.2s forwards';
    document.body.appendChild(money);
    setTimeout(()=>money.remove(),1200);

    setTimeout(() => img.classList.add('fall'), 300);
    setTimeout(() => img.classList.add('bloom'), 900);
    setTimeout(() => img.remove(), 1500);
  });
}

function createFirework(x, y) {
  for (let i = 0; i < 25; i++) {
    const fw = document.createElement('div');
    fw.className = 'firework';
    fw.style.left = x + 'px';
    fw.style.top = y + 'px';
    fw.style.background = `hsl(${Math.random()*360},100%,60%)`;
    document.body.appendChild(fw);
    setTimeout(() => fw.remove(), 800);
  }
}

// HOA MAI RƠI
setInterval(()=>{
  const petal=document.createElement('div');
  petal.innerHTML='🌸';
  petal.style.position='absolute';
  petal.style.left=Math.random()*window.innerWidth+'px';
  petal.style.top='-30px';
  petal.style.fontSize='24px';
  petal.style.animation='fallPetal 5s linear forwards';
  document.body.appendChild(petal);
  setTimeout(()=>petal.remove(),5000);
},300);

</script>

</body>
</html>
<img width="1024" height="1024" alt="ChatGPT Image 12_14_37 6 thg 12, 2025" src="https://github.com/user-attachments/assets/3023faed-5892-4280-b778-c37ef626ec68" />

