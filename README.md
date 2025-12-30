<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>초대장 — 낙원농원에 어서오세요!</title>
<style>
  :root{
    --bg:#000;
    --card-bg: rgba(255,255,255,0.02);
    --text:#f6f7fb;
    --muted:#9aa3b2;
    --accent:#ff6b6b;
    --max-width:1100px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  html,body{height:100%}
  body{
    background:var(--bg);
    color:var(--text);
    font-family: "Noto Sans KR", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:24px;
  }

  /* 카드 레이아웃 */
  .invite{
    width:100%;
    max-width:var(--max-width);
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    border-radius:14px;
    padding:28px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.6);
    display:flex;
    gap:32px;
    align-items:flex-start;
    justify-content:center;
  }

  .col{ flex:1 1 0; min-width:0; }
  .left{ display:flex; align-items:center; justify-content:center; }
  .right{ padding:6px 8px; }

  /* 이미지 프레임 — 크게 조정 */
  .frame{
    width:720px;           /* 데스크톱 기본 너비 */
    max-width:60vw;        /* 화면 너비의 60%까지 */
    min-width:260px;
    position:relative;
    border-radius:12px;
    overflow:visible;
    padding:12px;
    background: linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.02));
    box-shadow: 0 10px 40px rgba(0,0,0,0.6);
  }
  .img-wrap{ position:relative; width:100%; border-radius:10px; overflow:hidden; }
  .frame img{ display:block; width:100%; height:auto; object-fit:cover; transform: translateZ(0); }

  /* 글리치 레이어 (아주 약함) */
  .glitch-layer{ position:absolute; inset:0; pointer-events:none; }
  .glitch-layer img{ position:absolute; inset:0; width:100%; height:100%; object-fit:cover; top:0; left:0; }

  .glitch-r{ mix-blend-mode:screen; opacity:0.22; filter: blur(0.6px) saturate(0.9); }
  .glitch-g{ mix-blend-mode:screen; opacity:0.18; filter: blur(0.6px) saturate(0.9); }
  .glitch-b{ mix-blend-mode:screen; opacity:0.20; filter: blur(0.6px) saturate(0.95); }

  @keyframes glitchShift {
    0% { transform: translate(0,0); clip-path: inset(0 0 0 0); }
    12% { transform: translate(-1px, -0.5px); clip-path: inset(6% 0 80% 0); }
    24% { transform: translate(1px, 0.6px); clip-path: inset(70% 0 8% 0); }
    36% { transform: translate(-0.6px, -0.4px); clip-path: inset(18% 0 50% 0); }
    48% { transform: translate(0.8px, 0.5px); clip-path: inset(0 0 36% 0); }
    60% { transform: translate(-0.7px, -0.6px); clip-path: inset(28% 0 18% 0); }
    72% { transform: translate(0.5px, 0.4px); clip-path: inset(0 0 56% 0); }
    84% { transform: translate(-0.4px, -0.3px); clip-path: inset(12% 0 48% 0); }
    100% { transform: translate(0,0); clip-path: inset(0 0 0 0); }
  }
  .glitch-r { animation: glitchShift 6s infinite ease-in-out; }
  .glitch-g { animation: glitchShift 7s infinite ease-in-out reverse; }
  .glitch-b { animation: glitchShift 5.5s infinite ease-in-out; }

  .scanline{
    position:absolute; inset:0;
    background-image:
      linear-gradient(rgba(255,255,255,0.01) 1px, transparent 1px),
      repeating-linear-gradient(0deg, rgba(255,255,255,0.01) 0 1px, transparent 1px 3px);
    background-size:100% 4px, 100% 8px;
    mix-blend-mode:overlay; opacity:0.06; animation: scanMove 12s linear infinite; pointer-events:none;
  }
  @keyframes scanMove { from { background-position:0 0; } to { background-position:0 120px; } }

  /* 텍스트 스타일 */
  .title{ font-size: clamp(18px, 3vw, 26px); font-weight:800; margin-bottom:6px; text-align:center; }
  .subtitle{ color:var(--muted); font-size:15px; margin-bottom:12px; text-align:center; }
  .small-strong{
    display:block;
    font-weight:800;
    font-size:14px;
    margin:10px 0;
    text-align:left;
    letter-spacing:0.02em;
    white-space:pre-wrap;
  }
  .body{ color:var(--text); font-size:16px; line-height:1.6; text-align:center; padding:12px 6px; white-space:pre-wrap; }
  .meta{ margin-top:10px; text-align:center; font-weight:600; }
  .meta span{ display:block; color:var(--muted); font-weight:500; margin-top:6px; }

  /* 모바일에서 이미지 거의 전체 너비로 표시 */
  @media (max-width:1100px){
    .frame{ max-width:80vw; width:80vw; }
  }
  @media (max-width:820px){
    .invite{ flex-direction:column; padding:18px; gap:18px; align-items:center; }
    .frame{ width:92vw; max-width:92vw; }
    .title{ font-size: clamp(16px, 5.5vw, 22px); }
    .small-strong{ text-align:left; }
  }
</style>
</head>
<body>
  <main class="invite" role="main" aria-labelledby="inviteTitle">
    <div class="col left">
      <div class="frame" aria-hidden="false">
        <div class="img-wrap">
          <!-- 같은 폴더에 '낙원농원.png' 파일을 넣으세요 -->
          <img id="mainImage" src="낙원농원.png" alt="초대장 이미지" />
          <div class="glitch-layer" aria-hidden="true">
            <img class="glitch-r" id="gR" src="" alt="" />
            <img class="glitch-g" id="gG" src="" alt="" />
            <img class="glitch-b" id="gB" src="" alt="" />
            <div class="scanline"></div>
          </div>
        </div>
      </div>
    </div>

    <div class="col right">
      <h1 id="inviteTitle" class="title">낙원농원에 어서오세요!</h1>
      <p class="subtitle">함께 해주시면 기쁩니다</p>

      <div class="small-strong">
김솔음을찾습니다낙원은김솔음이필요합니다낙원을떠나지마세요이곳으로오세요
      </div>

      <div class="meta">
        일시: <span>[2066.66.66 / 44:44]</span>
        장소: <span>[낙원농원]</span>
      </div>

      <div class="body" id="inviteBody">
낙원농원에서 가족, 연인과 함께 하는 행복한 사과 따기 체험을 실시합니다!
이 광고를 보신 분들께 무료 농장 체험 기회를 드려요.
낙원농원에서 소중한 시간을 보내보세요!

모든 나무의 열매를 드셔도 좋지만, 먹은 만큼 어린 나무를 심어두고 떠나는 것을 잊지 마세요.
세상이 멸망하더라도 사과 나무는 심어야 합니다!
누군가가 지켜보고 있으니까요.
      </div>
    </div>
  </main>

<script>
  (function(){
    const main = document.getElementById('mainImage');
    const r = document.getElementById('gR');
    const g = document.getElementById('gG');
    const b = document.getElementById('gB');

    function applySrc(){
      const src = main.getAttribute('src') || '';
      r.src = src; g.src = src; b.src = src;
      r.style.transform = 'translate(-1px, -0.5px)';
      g.style.transform = 'translate(0.8px, 0.6px)';
      b.style.transform = 'translate(0px, 0px)';
    }

    if(main.complete){ applySrc(); } else { main.addEventListener('load', applySrc); }
  })();
</script>
</body>
</html>
