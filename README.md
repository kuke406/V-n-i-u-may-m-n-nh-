<!doctype html>

<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Lời chúc 20/10 — Trái tim bay</title>
  <style>
    html,body{height:100%;margin:0;font-family: 'Segoe UI', Roboto, system-ui, -apple-system; background: radial-gradient(#0b1020 0%, #071226 60%); color:#fff;}
    .wrap{height:100%;display:flex;align-items:center;justify-content:center;flex-direction:column;padding:20px;}
    .stage{width:360px;height:360px;position:relative}
    svg{width:100%;height:100%;display:block}
    /* text circling */
    .circle-text{font-size:16px;letter-spacing:2px;font-weight:600;fill:#ffe6f0}
    /* heart center message */
    .center-msg{font-family: Georgia, 'Times New Roman', serif; font-size:22px; text-anchor:middle; fill:#fff}
    /* star particles */
    .star{fill:#fff;opacity:0.9}
    /* animation keyframes */
    @keyframes rise {
      0%{transform:translateY(0) scale(1);opacity:1}
      100%{transform:translateY(-260px) scale(0.5);opacity:0}
    }
    .particle{position:absolute;left:50%;top:50%;width:8px;height:8px;border-radius:50%;background:#fff;opacity:0;transform:translate(-50%,-50%);} 
    /* different trajectories */
    .p1{animation:rise 2.2s cubic-bezier(.2,.9,.3,1) forwards; animation-delay:0.2s}
    .p2{animation:rise 2.6s cubic-bezier(.15,.85,.25,1) forwards; animation-delay:0.4s}
    .p3{animation:rise 1.9s cubic-bezier(.25,.8,.3,1) forwards; animation-delay:0.6s}
    .p4{animation:rise 2.4s cubic-bezier(.3,.7,.2,1) forwards; animation-delay:0.8s}/* small sparkle */
.spark{width:4px;height:4px;border-radius:50%;position:absolute;background:#fff;opacity:0;transform:translate(-50%,-50%)}
.spark.animate{animation:rise 1.5s ease-out forwards}

/* instruction */
.hint{margin-top:14px;opacity:0.85;font-size:14px}

/* make the path-text rotate slowly */
.rotor{transform-origin:50% 50%; animation:spin 10s linear infinite}
@keyframes spin {from{transform:rotate(0deg)} to{transform:rotate(360deg)}}

/* responsive */
@media (min-width:700px){.stage{width:520px;height:520px}}

  </style>
</head>
<body>
  <div class="wrap">
    <div class="stage" id="stage">
      <svg viewBox="0 0 200 200" preserveAspectRatio="xMidYMid meet">
        <!-- decorative glow -->
        <defs>
          <radialGradient id="g1" cx="50%" cy="40%">
            <stop offset="0%" stop-color="#ff9ccf" stop-opacity="0.9" />
            <stop offset="60%" stop-color="#59124a" stop-opacity="0.06" />
            <stop offset="100%" stop-color="#000" stop-opacity="0" />
          </radialGradient>
          <filter id="blur"><feGaussianBlur stdDeviation="6" /></filter>
        </defs><!-- circular path for text -->
    <g class="rotor">
      <path id="circlePath" d="M100,15 a85,85 0 1,1 0,170 a85,85 0 1,1 0,-170" fill="none" />
      <text class="circle-text">
        <textPath href="#circlePath" startOffset="0%">  祝：20/10 心想事成 · 母親節快樂 · 謹此獻上滿滿心意   </textPath>
      </text>
    </g>

    <!-- heart shape -->
    <g transform="translate(0,0)">
      <path id="heart" d="M100 140 C 60 110, 40 80, 70 55 C 95 35, 105 40, 100 70 C 95 40, 105 35, 130 55 C 160 80, 140 110, 100 140 Z" fill="#ff3d7a" stroke="#ff7aa6" stroke-width="2" />
      <circle cx="100" cy="100" r="40" fill="url(#g1)" filter="url(#blur)" opacity="0.25"/>
      <text x="100" y="105" class="center-msg">Lời chúc 20/10</text>
    </g>

    <!-- stars that will animate with JS (initially hidden) -->
  </svg>
</div>

<div class="hint">Sao nhập vào trái tim — khởi động bằng một chạm hoặc ấn phím cách.</div>

  </div>  <script>
    // tạo các ngôi sao (particles)
    const stage = document.getElementById('stage');
    function makeStar(x,y,cls){
      const s = document.createElement('div');
      s.className = 'particle ' + cls;
      s.style.left = (50 + x) + '%';
      s.style.top = (50 + y) + '%';
      s.style.width = (6 + Math.random()*8) + 'px';
      s.style.height = s.style.width;
      s.style.background = '#fff';
      s.style.borderRadius = '50%';
      stage.appendChild(s);
      // random left/right drift using transform
      const dx = (Math.random()*160 - 80);
      s.animate([
        {transform: 'translate(-50%,-50%) translateX(0px) translateY(0px) scale(1)', opacity:1},
        {transform: `translate(-50%,-50%) translateX(${dx}px) translateY(-260px) scale(0.5)`, opacity:0}
      ], {duration: 1800 + Math.random()*900, easing: 'cubic-bezier(.2,.9,.3,1)', fill: 'forwards'});
      setTimeout(()=>s.remove(), 3500);
    }

    function burst(){
      // make many small stars in a burst from around heart
      for(let i=0;i<18;i++){
        const angle = Math.random()*Math.PI*2;
        const radius = 10 + Math.random()*18;
        const x = Math.cos(angle)*radius/1.6; // percent offsets
        const y = Math.sin(angle)*radius/1.6;
        makeStar(x,y,'p'+(1+Math.floor(Math.random()*4)));
      }
    }

    // circle text will rotate already via CSS. We'll animate the heart text flying like stars into heart
    // on click or spacebar, run the sequence: circle rotate (already), then burst, then small hearts fly up

    window.addEventListener('click', ()=>start());
    window.addEventListener('keydown',(e)=>{ if(e.code==='Space') start();});

    let started=false;
    function start(){
      if(started) return; started=true;
      // quick pulse of heart
      const heart = document.querySelector('#heart');
      heart.animate([
        {transform:'scale(1)'}, {transform:'scale(1.08)'}, {transform:'scale(0.96)'}, {transform:'scale(1)'}
      ], {duration:700, iterations:1, easing:'ease-out'});

      // circular text speed up then normal
      const rotor = document.querySelector('.rotor');
      rotor.style.animationDuration='4s';
      setTimeout(()=>{ rotor.style.animationDuration='10s'; },1200);

      // burst stars repeatedly
      let times=0;
      const t = setInterval(()=>{ burst(); times++; if(times>6){ clearInterval(t); started=false;} }, 420);
    }

    // accessibility: autoplay a small burst when page loads on mobile (user gesture policies vary)
    window.addEventListener('load', ()=>{ /* no autoplay to respect policies */ });
  </script></body>
</html>
