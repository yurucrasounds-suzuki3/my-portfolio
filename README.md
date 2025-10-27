<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>すずきIII｜Portfolio & Quiz</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Noto+Sans+JP:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1:#0f1020; --bg2:#11122a; --acc:#72f5e6; --acc2:#ffb86b; --txt:#e7e7f3; --mut:#a4a6bf;
      --card:#171831aa; --blur:16px; --radius:22px;
    }
    *{box-sizing:border-box}
    html,body{height:100%;}
    body{
      margin:0; color:var(--txt); font-family:"Poppins","Noto Sans JP",system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,"Apple Color Emoji","Segoe UI Emoji";
      background: radial-gradient(1200px 900px at 20% 10%, #1a1b3a 0%, #0f1020 40%, #0b0c17 100%);
      overflow-x:hidden;
    }
    /* Animated aurora */
    .aurora{
      position:fixed; inset:-20% -20% auto -20%; height:80vh; pointer-events:none; filter:blur(60px); opacity:.45; mix-blend-mode:screen;
      background: conic-gradient(from 180deg at 50% 50%, #72f5e6cc, #b388ffcc, #ff7eb3cc, #72f5e6cc);
      animation: swirl 18s linear infinite;
    }
    @keyframes swirl{0%{transform:translateY(-10%) rotate(0deg)}100%{transform:translateY(-10%) rotate(360deg)}}

    header{
      position:sticky; top:0; z-index:20; backdrop-filter:saturate(1.2) blur(10px);
      background:linear-gradient(180deg, #101127cc, #10112766 70%, transparent);
      border-bottom:1px solid #2a2c52; padding:14px 20px;
    }
    .wrap{max-width:1100px; margin:0 auto; display:flex; align-items:center; gap:14px;}
    .brand{display:flex; align-items:center; gap:12px; text-decoration:none; color:var(--txt)}
    .avatar{
      width:40px; height:40px; border-radius:12px; display:grid; place-items:center; font-weight:700; letter-spacing:.5px;
      background:linear-gradient(135deg,#72f5e6,#7bd1ff,#b388ff); color:#0c0f13; box-shadow:0 6px 24px #72f5e655;
    }
    nav{margin-left:auto; display:flex; gap:8px;}
    .btn{appearance:none; border:none; color:#0b0c17; font-weight:700; cursor:pointer; padding:10px 14px; border-radius:14px; transition:transform .15s ease, box-shadow .2s ease, filter .2s ease;}
    .btn-primary{background:linear-gradient(135deg, var(--acc), #8ef3ff); box-shadow:0 10px 30px #72f5e644;}
    .btn-ghost{background:#ffffff10; color:var(--txt); border:1px solid #ffffff22}
    .btn:hover{transform:translateY(-2px)}

    main{padding:48px 20px 96px}
    .grid{
      max-width:1100px; margin:0 auto; display:grid; grid-template-columns:1.2fr .8fr; gap:28px;
    }
    @media (max-width:900px){.grid{grid-template-columns:1fr;}}

    .card{
      background:var(--card); border:1px solid #2a2c52; border-radius:var(--radius); padding:26px; backdrop-filter:blur(var(--blur));
      box-shadow:0 30px 80px #00000066, inset 0 1px 0 #ffffff0f;
    }
    .hero{
      position:relative; overflow:hidden; min-height:260px; display:grid; align-content:center; gap:14px;
    }
    .chip{display:inline-flex; align-items:center; gap:8px; padding:8px 12px; background:#ffffff12; border:1px solid #ffffff22; border-radius:999px; color:var(--mut); font-size:.9rem}
    h1{font-size: clamp(28px, 4vw, 44px); margin:0; letter-spacing:.2px}
    .accent{background:linear-gradient(90deg,#72f5e6,#b388ff,#ffb86b); -webkit-background-clip:text; background-clip:text; color:transparent}
    p{color:#cfd1ea; line-height:1.75}

    .info{display:grid; gap:12px;}
    .row{display:flex; gap:12px; align-items:center}
    .icon{width:24px; height:24px; display:inline-grid; place-items:center; background:#ffffff10; border:1px solid #ffffff22; border-radius:8px}
    .kv{display:grid; gap:3px}
    .label{font-size:.8rem; color:var(--mut)}
    .value{font-weight:700}

    .cta{display:flex; gap:12px; flex-wrap:wrap; margin-top:14px}

    .footnote{font-size:.92rem; color:var(--mut)}

    /* QUIZ */
    .quiz-panel{position:fixed; inset:0; display:none; place-items:center; background:#0a0b15e6; z-index:40;}
    .quiz-card{width:min(680px,92vw);}
    .quiz-q{font-weight:700; font-size:1.15rem; margin-bottom:14px}
    .quiz-choices{display:grid; gap:10px}
    .choice{border:1px solid #2a2c52; background:#15162d; color:var(--txt); padding:12px 14px; border-radius:12px; cursor:pointer; transition:transform .1s ease, background .2s ease, border .2s ease}
    .choice:hover{transform:translateY(-1px); background:#1b1d3b}
    .choice.correct{border-color:#35f5c8; box-shadow:0 0 0 3px #35f5c833 inset}
    .choice.wrong{border-color:#ff6b6b; box-shadow:0 0 0 3px #ff6b6b33 inset}
    .quiz-bottom{display:flex; justify-content:space-between; align-items:center; margin-top:18px}
    .progress{height:10px; background:#1a1b36; border-radius:999px; overflow:hidden; border:1px solid #2a2c52}
    .bar{height:100%; width:0%; background:linear-gradient(90deg,#72f5e6,#b388ff);}

    /* Confetti (simple) */
    .confetti{position:fixed; inset:0; pointer-events:none; overflow:hidden; z-index:90}
    .confetti i{position:absolute; width:10px; height:14px; opacity:0; animation:fall 1800ms linear forwards}
    @keyframes fall{0%{transform:translateY(-20%) rotate(0); opacity:1} 100%{transform:translateY(120vh) rotate(540deg); opacity:0}}

    footer{max-width:1100px; margin:40px auto 0; padding:0 20px; color:var(--mut)}
  </style>
</head>
<body>
  <div class="aurora" aria-hidden="true"></div>
  <header>
    <div class="wrap">
      <a class="brand" href="#" onclick="toTop(event)">
        <div class="avatar" aria-hidden="true">すIII</div>
        <strong>すずきIII</strong>
      </a>
      <nav>
        <button class="btn btn-ghost" onclick="scrollToSection('about')">自己紹介</button>
        <button class="btn btn-ghost" onclick="scrollToSection('facts')">プロフィール</button>
        <button class="btn btn-primary" onclick="openQuiz()">クイズに挑戦</button>
      </nav>
    </div>
  </header>

  <main>
    <section class="grid" id="about">
      <article class="card hero">
        <span class="chip">こんにちは 👋</span>
        <h1>
          北海道生まれ、ラーメンを愛し、<span class="accent">キャンプとゴルフ</span>で自然を満喫する<br/>
          <span class="accent">すずきIII</span>の自己紹介サイトへようこそ。
        </h1>
        <p class="footnote">家族は妻と4歳の息子。日々の小さな冒険とものづくりが大好きです。</p>
        <div class="cta">
          <button class="btn btn-primary" onclick="openQuiz()">プロフィールクイズで遊ぶ</button>
          <a class="btn btn-ghost" href="#facts">詳しいプロフィールを見る</a>
        </div>
      </article>

      <aside class="card info" id="facts">
        <div class="row">
          <span class="icon">🏷️</span>
          <div class="kv"><span class="label">名前</span><span class="value">すずきIII</span></div>
        </div>
        <div class="row">
          <span class="icon">📍</span>
          <div class="kv"><span class="label">出身地</span><span class="value">北海道</span></div>
        </div>
        <div class="row">
          <span class="icon">🍜</span>
          <div class="kv"><span class="label">好きな食べ物</span><span class="value">ラーメン</span></div>
        </div>
        <div class="row">
          <span class="icon">⛺</span>
          <div class="kv"><span class="label">趣味</span><span class="value">キャンプ、ゴルフ</span></div>
        </div>
        <div class="row">
          <span class="icon">👨‍👩‍👦</span>
          <div class="kv"><span class="label">家族構成</span><span class="value">妻、4歳息子</span></div>
        </div>
        <div class="cta">
          <button class="btn btn-primary" onclick="openQuiz()">この内容でクイズを出題</button>
        </div>
      </aside>
    </section>

    <section class="grid" style="margin-top:28px">
      <article class="card" style="grid-column:1/-1">
        <h2 style="margin:0 0 8px">このサイトについて</h2>
        <p>
          このページは初心者でも編集しやすい<strong>単一HTMLファイル</strong>で作られており、
          そのままアップロードすれば公開できます。上部の「クイズに挑戦」から、プロフィールをもとにしたクイズで遊べます。
        </p>
      </article>
    </section>
  </main>

  <!-- QUIZ PANEL -->
  <div id="quiz" class="quiz-panel" role="dialog" aria-modal="true" aria-label="プロフィールクイズ">
    <div class="card quiz-card">
      <div style="display:flex; gap:12px; align-items:center; justify-content:space-between; margin-bottom:6px">
        <h3 style="margin:0">プロフィールクイズ</h3>
        <button class="btn btn-ghost" onclick="closeQuiz()">閉じる</button>
      </div>
      <div id="qwrap"></div>
      <div class="quiz-bottom">
        <div class="progress" style="flex:1; margin-right:12px"><div class="bar" id="bar"></div></div>
        <span id="meta" class="footnote">1 / 5</span>
        <button id="next" class="btn btn-primary" style="margin-left:12px">次へ</button>
      </div>
    </div>
  </div>

  <div id="confetti" class="confetti" aria-hidden="true"></div>

  <footer>
    <p>© <span id="year"></span> すずきIII. All rights reserved.</p>
  </footer>

  <script>
    // Utility scroll
    function scrollToSection(id){document.getElementById(id)?.scrollIntoView({behavior:'smooth'})}
    function toTop(e){e?.preventDefault(); window.scrollTo({top:0,behavior:'smooth'})}

    // Profile data (編集はここだけでOK)
    const profile = {
      name: 'すずきIII',
      home: '北海道',
      food: 'ラーメン',
      hobbies: ['キャンプ','ゴルフ'],
      family: '妻、4歳息子'
    };

    // Build quiz from profile
    const quizData = [
      { q: '出身地はどこ？', a: profile.home, choices: ['北海道','青森','東京','福岡'] },
      { q: '好きな食べ物は？', a: profile.food, choices: ['寿司','ピザ','ラーメン','ステーキ'] },
      { q: '趣味として正しい組み合わせは？', a: 'キャンプ、ゴルフ', choices: ['読書、釣り','キャンプ、サッカー','キャンプ、ゴルフ','将棋、野球'] },
      { q: '家族構成は？', a: profile.family, choices: ['独身','妻、4歳息子','妻、娘2人','両親と同居'] },
      { q: 'このサイトの持ち主の名前は？', a: profile.name, choices: ['すずきIII','すずきII','すずきIV','すずきJr.'] },
    ];

    // Quiz state
    let idx = 0, score = 0, locked=false;
    const panel = document.getElementById('quiz');
    const qwrap = document.getElementById('qwrap');
    const meta = document.getElementById('meta');
    const next = document.getElementById('next');
    const bar = document.getElementById('bar');

    function openQuiz(){ panel.style.display='grid'; renderQ(); }
    function closeQuiz(){ panel.style.display='none'; idx=0; score=0; locked=false; }

    function renderQ(){
      const data = quizData[idx];
      meta.textContent = `${idx+1} / ${quizData.length}`;
      bar.style.width = `${(idx)/quizData.length*100}%`;
      qwrap.innerHTML = `
        <div class="quiz-q">Q${idx+1}. ${data.q}</div>
        <div class="quiz-choices">
          ${shuffle([...data.choices]).map(c=>`<div class="choice" data-choice="${c}">${c}</div>`).join('')}
        </div>
      `;
      qwrap.querySelectorAll('.choice').forEach(el=>{
        el.addEventListener('click',()=>choose(el,data.a))
      });
      next.onclick = ()=>{
        if(idx < quizData.length-1){ idx++; locked=false; renderQ(); }
        else { finish(); }
      }
    }

    function choose(el,answer){
      if(locked) return; locked=true;
      const v = el.getAttribute('data-choice');
      if(v===answer){
        el.classList.add('correct'); score++;
      } else {
        el.classList.add('wrong');
        // also mark correct
        qwrap.querySelectorAll('.choice').forEach(c=>{ if(c.getAttribute('data-choice')===answer) c.classList.add('correct'); });
      }
    }

    function finish(){
      bar.style.width = '100%';
      qwrap.innerHTML = `
        <div class="quiz-q">結果</div>
        <p>あなたのスコアは <strong>${score} / ${quizData.length}</strong> でした！</p>
        <div class="cta">
          <button class="btn btn-primary" onclick="restart()">もう一度挑戦する</button>
          <button class="btn btn-ghost" onclick="closeQuiz()">閉じる</button>
        </div>
      `;
      if(score === quizData.length) burstConfetti();
      next.onclick = ()=>{};
    }

    function restart(){ idx=0; score=0; locked=false; renderQ(); }

    function shuffle(a){ for(let i=a.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [a[i],a[j]]=[a[j],a[i]];} return a }

    // Simple confetti animation
    function burstConfetti(){
      const root = document.getElementById('confetti');
      const colors = ['#72f5e6','#b388ff','#ffb86b','#7bd1ff','#ff7eb3'];
      for(let i=0;i<120;i++){
        const p = document.createElement('i');
        const size = 6 + Math.random()*10;
        p.style.left = Math.random()*100 + 'vw';
        p.style.top = - (Math.random()*20) + 'vh';
        p.style.width = size+'px'; p.style.height = (size*0.6)+'px';
        p.style.background = colors[i%colors.length];
        p.style.boxShadow = '0 0 8px #ffffff22';
        p.style.transform = `rotate(${Math.random()*360}deg)`;
        p.style.animationDelay = (Math.random()*0.2)+'s';
        root.appendChild(p);
        setTimeout(()=>p.remove(), 2000);
      }
    }

    // Footer year
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
