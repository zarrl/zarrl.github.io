<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Happy Birthday Tilamm</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      height: 100vh;
      overflow: hidden;
      background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
      font-family: 'Poppins', system-ui, sans-serif;
      color: #fff;
      position: relative;
    }

    /* Tombol play */
    #playBtn {
      position: absolute;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      padding: 16px 28px;
      font-size: 1.3rem;
      font-weight: bold;
      color: #1b2735;
      background: #ffd700;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      z-index: 1000;
      box-shadow: 0 0 20px rgba(255, 215, 0, 0.7);
      transition: transform 0.2s;
    }
    #playBtn:hover { transform: translate(-50%, -50%) scale(1.05); }

    /* Background elemen */
    .stars {
      position: absolute; inset: 0;
      background: transparent url("https://www.script-tutorials.com/demos/360/images/stars.png") repeat;
      animation: animStar 100s linear infinite;
      z-index: 0; display:none;
    }
    @keyframes animStar {
      from { transform: translateY(0); }
      to   { transform: translateY(-1000px); }
    }

    .moon {
      position: absolute; top: 40px; right: 60px;
      width: 120px; height: 120px;
      background: radial-gradient(circle at 30% 30%, #fff 60%, #ccc 100%);
      border-radius: 50%;
      box-shadow: 0 0 40px rgba(255,255,200,0.7);
      z-index: 1; display:none;
    }

    .cloud {
      position: absolute;
      top: var(--top, 20%); left: -300px;
      width: var(--w, 400px); height: var(--h, 120px);
      background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.25), rgba(255,255,255,0));
      border-radius: 50%; filter: blur(40px);
      opacity: 0.15;
      animation: moveCloud var(--dur, 60s) linear infinite;
      z-index: 1; display:none;
    }
    @keyframes moveCloud { from{transform:translateX(0);} to{transform:translateX(160vw);} }

    /* Bintang gemerlap */
    .twinkle {
      position: absolute; width: 4px; height: 4px;
      background: #fff; border-radius: 50%;
      box-shadow: 0 0 6px #fff, 0 0 12px rgba(255,255,255,0.6);
      animation: twinkleAnim 2s infinite alternate;
      z-index: 1; 
    }
    @keyframes twinkleAnim { 
      from{opacity:0.35;transform:scale(0.7);} 
      to{opacity:1;transform:scale(1.25);} 
    }

    /* Slideshow */
    .slideshow {
      position: relative;
      width: 100%; height: 100%;
      display: flex; justify-content: center; align-items: center;
      text-align: center; overflow: hidden;
      z-index: 2; padding: 16px;
    }
    .slide {
      position: absolute; opacity: 0;
      width: min(90vw, 500px);
      transition: opacity 1s ease-in-out;
    }
    .slide img {
      width: 100%; max-height: 70vh;
      object-fit: contain;
      box-shadow: 0 0 25px rgba(255,255,255,0.5);
      border-radius: 15px; background: rgba(0,0,0,0.2);
    }
    .slide p {
      font-size: clamp(1rem, 2.5vw, 1.5rem);
      margin-top: 14px; line-height: 1.4;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
      padding: 0 6px;
    }

    /* Foto kolase terakhir */
    .final-photos {
      display: flex; flex-wrap: wrap; justify-content: center;
      gap: 10px; margin: 12px 0;
    }
    .final-photos img {
      width: 85px; height: 85px;
      object-fit: cover; border-radius: 10px;
      box-shadow: 0 0 12px rgba(255,255,255,0.6);
      border: 2px solid #fff;
    }

    /* Kucing */
    .cat-ghibli {
      position: absolute; bottom: 8px; left: -200px;
      width: 110px; z-index: 3; pointer-events: none;
      filter: drop-shadow(0 4px 8px rgba(0,0,0,0.6));
      display:none;
    }
    @keyframes runCat {
      0%{left:-200px;transform:scaleX(1);}
      45%{left:110%;transform:scaleX(1);}
      50%{left:110%;transform:scaleX(-1);}
      95%{left:-200px;transform:scaleX(-1);}
      100%{left:-200px;transform:scaleX(1);}
    }

    /* Meteor */
    .meteor {
      position: absolute; pointer-events: none; z-index: 2;
      opacity: 0; transform: rotate(var(--angle, -45deg)) translateY(0);
      animation: fly var(--speed, 2s) linear forwards;
    }
    @keyframes fly {
      0%{transform:rotate(var(--angle)) translateY(0);opacity:0;}
      8%{opacity:1;} 80%{opacity:1;}
      100%{transform:rotate(var(--angle)) translateY(var(--distance,120vh));opacity:0;}
    }
    .meteor__head{width:var(--thick,3px);height:var(--thick,3px);border-radius:50%;background:white;}
    .meteor__tail{position:absolute;top:calc(-1*var(--len,140px));width:var(--thick,3px);height:var(--len,140px);
      border-radius:999px;background:linear-gradient(to top,var(--c1),var(--c2) 35%,rgba(255,255,255,0.15) 80%,rgba(255,255,255,0));
    }
  </style>
</head>
<body>
  <button id="playBtn">▶ Play</button>

  <div class="stars"></div>
  <div class="moon"></div>
  <div class="cloud" style="--top:15%; --w:500px; --h:160px; --dur:70s;"></div>
  <div class="cloud" style="--top:30%; --w:350px; --h:130px; --dur:90s;"></div>
  <div class="cloud" style="--top:50%; --w:600px; --h:180px; --dur:80s;"></div>

  <div class="slideshow">
    <div class="slide"><img src="IMG-20250825-WA0000.jpg"><p>Happy Birthday Tilamm</p></div>
    <div class="slide"><img src="IMG-20250824-WA0222.jpg"><p>Semoga kita bisa terus berlanjut hingga tutup usia</p></div>
    <div class="slide"><img src="IMG-20250824-WA0221.jpg"><p>Banyak hal kan lam, tapi kita tetep kita</p></div>
    <div class="slide"><img src="IMG-20250813-WA0097.jpg"><p>Proud Of You Tilamm</p></div>
    <div class="slide"><img src="IMG-20250824-WA0247.jpg"><p>Selamat Ulang Tahun Tilam, aku bakal selalu disinii</p></div>
    <div class="slide">
      <div class="final-photos">
        <img src="IMG_7166.JPG"><img src="IMG_20250818_133044_HDR.jpg"><img src="Screenshot_20250711-225834.png">
      </div>
      <p style="font-size:clamp(1.3rem,3.5vw,2rem);color:#ffd700;font-weight:bold;">✨ Wish U All The Best Tilamm ✨</p>
      <div class="final-photos"><img src="IMG-20250825-WA0000.jpg"><img src="IMG-20250824-WA0247.jpg"></div>
    </div>
  </div>

  <img src="cat-running.gif" class="cat-ghibli" id="cat" />
  <audio id="bgm" loop><source src="ifonly.mp3" type="audio/mpeg"></audio>

  <script>
    const playBtn=document.getElementById("playBtn");
    const slides=document.querySelectorAll(".slide");
    const bgm=document.getElementById("bgm");
    const cat=document.getElementById("cat");

    // Bikin bintang gemerlap
    function createTwinkles(n){
      for(let i=0;i<n;i++){
        const t=document.createElement("div");
        t.className="twinkle";
        t.style.top=Math.random()*window.innerHeight+"px";
        t.style.left=Math.random()*window.innerWidth+"px";
        document.body.appendChild(t);
      }
    }

    // Meteor
    function spawnMeteor({angleDeg,top,left,speed,len,thick,colors}){
      const m=document.createElement("div");
      m.className="meteor";
      m.style.top=top+"px"; m.style.left=left+"px";
      m.style.setProperty("--angle",angleDeg+"deg");
      m.style.setProperty("--speed",speed+"s");
      m.style.setProperty("--distance",Math.hypot(window.innerWidth,window.innerHeight)*1.3+"px");
      m.style.setProperty("--len",len+"px"); m.style.setProperty("--thick",thick+"px");
      m.style.setProperty("--c1",colors[0]); m.style.setProperty("--c2",colors[1]);
      const head=document.createElement("div");head.className="meteor__head";
      const tail=document.createElement("div");tail.className="meteor__tail";
      m.appendChild(head);m.appendChild(tail);document.body.appendChild(m);
      setTimeout(()=>m.remove(),(speed*1000)+100);
    }
    function meteorBurst(){
      const palettes=[["white","gold"],["#aaf","#55f"],["#f8f","#c4f"]];
      const count=Math.floor(Math.random()*3)+1;
      for(let i=0;i<count;i++){
        let angle=35+Math.random()*30;let left=20;
        if(Math.random()<0.5){angle=-60-Math.random()*30;left=window.innerWidth-20;}
        const top=Math.random()*window.innerHeight*0.3;
        const speed=1.4+Math.random()*0.9;
        const len=150+Math.random()*60; const thick=2+Math.random()*2;
        const colors=palettes[Math.floor(Math.random()*palettes.length)];
        setTimeout(()=>spawnMeteor({angleDeg:angle,top,left,speed,len,thick,colors}),i*200);
      }
    }

    // Start show
    function startShow(){
      playBtn.style.display="none";
      document.querySelector(".stars").style.display="block";
      document.querySelector(".moon").style.display="block";
      document.querySelectorAll(".cloud").forEach(c=>c.style.display="block");
      cat.style.display="block";
      cat.style.animation="runCat 4s linear infinite";
      createTwinkles(40);
      setInterval(meteorBurst,3000);
      bgm.play();

      let index=0;
      slides[index].style.opacity=1;
      const interval=5500; // 6 slide × 5.5s ≈ 33s total
      setInterval(()=>{
        slides[index].style.opacity=0;
        index=(index+1)%slides.length; // looping
        slides[index].style.opacity=1;
      },interval);
    }

    playBtn.addEventListener("click",startShow);
  </script>
</body>
</html>
