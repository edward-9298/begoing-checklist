[index.html](https://github.com/user-attachments/files/25759359/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>주간 체크리스트</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #13131a;
    --surface2: #1c1c28;
    --border: #2a2a3d;
    --text: #e8e8f0;
    --text-muted: #6b6b8a;
    --gold: #ffd700;
    --free: #4ade80;
    --paid: #fb923c;

    --begoing: #6c63ff;
    --begoing-dim: rgba(108,99,255,0.12);
    --miracle: #f472b6;
    --miracle-dim: rgba(244,114,182,0.12);
    --attack: #34d399;
    --attack-dim: rgba(52,211,153,0.12);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Noto Sans KR', sans-serif;
    min-height: 100vh;
    padding: 24px 16px 80px;
    background-image:
      radial-gradient(ellipse at 15% 10%, rgba(108,99,255,0.07) 0%, transparent 50%),
      radial-gradient(ellipse at 85% 80%, rgba(244,114,182,0.05) 0%, transparent 50%),
      radial-gradient(ellipse at 50% 50%, rgba(52,211,153,0.03) 0%, transparent 60%);
  }

  /* Header */
  header {
    text-align: center;
    margin-bottom: 28px;
  }
  .header-label {
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--text-muted);
    text-transform: uppercase;
    margin-bottom: 6px;
  }
  h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(32px, 7vw, 56px);
    letter-spacing: 4px;
    color: #fff;
    line-height: 1;
  }
  .week-info {
    margin-top: 8px;
    font-size: 12px;
    color: var(--text-muted);
    letter-spacing: 1px;
  }
  .week-info span { color: var(--gold); font-weight: 700; }

  /* Channel Tabs */
  .tabs {
    display: flex;
    gap: 8px;
    max-width: 660px;
    margin: 0 auto 24px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 6px;
  }
  .tab {
    flex: 1;
    padding: 10px 0;
    border-radius: 10px;
    border: none;
    background: transparent;
    color: var(--text-muted);
    font-family: 'Noto Sans KR', sans-serif;
    font-size: 13px;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 1px;
  }
  .tab.active-begoing { background: var(--begoing-dim); color: var(--begoing); }
  .tab.active-miracle { background: var(--miracle-dim); color: var(--miracle); }
  .tab.active-attack { background: var(--attack-dim); color: var(--attack); }
  .tab:hover { color: var(--text); }

  /* Progress */
  .progress-wrap {
    max-width: 660px;
    margin: 0 auto 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 16px 20px;
  }
  .progress-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
  .progress-label { font-size: 11px; color: var(--text-muted); letter-spacing: 1px; }
  .progress-count { font-size: 20px; font-weight: 900; }
  .progress-count span { font-size: 12px; color: var(--text-muted); font-weight: 400; }
  .bar-bg { height: 6px; background: var(--border); border-radius: 99px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 99px; transition: width 0.5s cubic-bezier(0.4,0,0.2,1); width: 0%; }
  .bar-begoing { background: linear-gradient(90deg, var(--begoing), #a78bfa); }
  .bar-miracle { background: linear-gradient(90deg, var(--miracle), #fb7185); }
  .bar-attack { background: linear-gradient(90deg, var(--attack), #60a5fa); }

  /* Reset */
  .reset-btn {
    display: block;
    margin: 0 auto 20px;
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text-muted);
    font-family: 'Noto Sans KR', sans-serif;
    font-size: 11px;
    padding: 7px 18px;
    border-radius: 99px;
    cursor: pointer;
    letter-spacing: 1px;
    transition: all 0.2s;
  }
  .reset-btn:hover { border-color: var(--miracle); color: var(--miracle); }

  /* Channel Panels */
  .panel { display: none; max-width: 660px; margin: 0 auto; }
  .panel.active { display: block; }

  /* Day Cards */
  .days-grid { display: flex; flex-direction: column; gap: 12px; }

  .day-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  .day-card.all-done-begoing { border-color: var(--begoing); box-shadow: 0 0 18px rgba(108,99,255,0.12); }
  .day-card.all-done-miracle { border-color: var(--miracle); box-shadow: 0 0 18px rgba(244,114,182,0.12); }
  .day-card.all-done-attack { border-color: var(--attack); box-shadow: 0 0 18px rgba(52,211,153,0.12); }

  .day-header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 18px;
    border-bottom: 1px solid var(--border);
    background: var(--surface2);
  }
  .day-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 26px;
    letter-spacing: 2px;
    line-height: 1;
    min-width: 24px;
  }
  .day-full { font-size: 10px; color: var(--text-muted); letter-spacing: 2px; }
  .day-done-badge {
    margin-left: auto;
    font-size: 10px;
    padding: 3px 10px;
    border-radius: 99px;
    opacity: 0;
    transition: opacity 0.3s;
    letter-spacing: 1px;
  }
  .badge-begoing { background: rgba(108,99,255,0.15); color: var(--begoing); border: 1px solid rgba(108,99,255,0.3); }
  .badge-miracle { background: rgba(244,114,182,0.15); color: var(--miracle); border: 1px solid rgba(244,114,182,0.3); }
  .badge-attack { background: rgba(52,211,153,0.15); color: var(--attack); border: 1px solid rgba(52,211,153,0.3); }
  .day-card.all-done-begoing .day-done-badge,
  .day-card.all-done-miracle .day-done-badge,
  .day-card.all-done-attack .day-done-badge { opacity: 1; }

  .tasks { padding: 10px 14px; display: flex; flex-direction: column; gap: 6px; }

  .task-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 12px;
    border-radius: 10px;
    border: 1px solid transparent;
    cursor: pointer;
    transition: all 0.2s;
    user-select: none;
  }
  .task-item:hover { background: var(--surface2); border-color: var(--border); }
  .task-item.checked-begoing { background: rgba(108,99,255,0.06); border-color: rgba(108,99,255,0.18); }
  .task-item.checked-miracle { background: rgba(244,114,182,0.06); border-color: rgba(244,114,182,0.18); }
  .task-item.checked-attack { background: rgba(52,211,153,0.06); border-color: rgba(52,211,153,0.18); }

  .checkbox {
    width: 20px; height: 20px;
    border-radius: 5px;
    border: 2px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
    transition: all 0.2s;
    font-size: 11px;
  }
  .checked-begoing .checkbox { background: var(--begoing); border-color: var(--begoing); }
  .checked-miracle .checkbox { background: var(--miracle); border-color: var(--miracle); }
  .checked-attack .checkbox { background: var(--attack); border-color: var(--attack); }

  .task-text { font-size: 13px; color: var(--text); transition: all 0.2s; line-height: 1.4; }
  .task-item[class*="checked"] .task-text { color: var(--text-muted); text-decoration: line-through; }

  .tbadge {
    margin-left: auto;
    font-size: 9px;
    padding: 2px 8px;
    border-radius: 99px;
    font-weight: 500;
    flex-shrink: 0;
    letter-spacing: 0.3px;
  }
  .tbadge.free { background: rgba(74,222,128,0.1); color: var(--free); border: 1px solid rgba(74,222,128,0.2); }
  .tbadge.paid { background: rgba(251,146,60,0.1); color: var(--paid); border: 1px solid rgba(251,146,60,0.2); }

  /* Day name colors per channel */
  .ch-begoing .mon { color: #60a5fa; }
  .ch-begoing .tue { color: #a78bfa; }
  .ch-begoing .wed { color: #34d399; }
  .ch-begoing .thu { color: #fb923c; }
  .ch-begoing .fri { color: #f472b6; }
  .ch-begoing .sat { color: #ffd700; }

  .ch-miracle .mon { color: #f472b6; }
  .ch-miracle .tue { color: #fb923c; }
  .ch-miracle .wed { color: #a78bfa; }
  .ch-miracle .thu { color: #60a5fa; }

  .ch-attack .mon { color: #34d399; }
  .ch-attack .tue { color: #60a5fa; }
  .ch-attack .wed { color: #a78bfa; }
  .ch-attack .thu { color: #fb923c; }

  /* Confetti */
  .confetti-wrap { position: fixed; top:0; left:0; width:100%; height:100%; pointer-events:none; z-index:999; }
  @keyframes fall {
    0% { transform: translateY(-20px) rotate(0deg); opacity:1; }
    100% { transform: translateY(100vh) rotate(720deg); opacity:0; }
  }
  .confetti-piece { position:absolute; width:8px; height:8px; border-radius:2px; animation: fall linear forwards; }
</style>
</head>
<body>

<header>
  <div class="header-label">Weekly Checklist</div>
  <h1>채널 관리</h1>
  <div class="week-info" id="weekInfo"></div>
</header>

<!-- Tabs -->
<div class="tabs">
  <button class="tab active-begoing" onclick="switchChannel('begoing')">비고잉</button>
  <button class="tab" onclick="switchChannel('miracle')">미라클</button>
  <button class="tab" onclick="switchChannel('attack')">공략수</button>
</div>

<!-- Progress -->
<div class="progress-wrap">
  <div class="progress-top">
    <div class="progress-label">주간 진행률</div>
    <div class="progress-count" id="progressCount">0 <span>/ 0</span></div>
  </div>
  <div class="bar-bg"><div class="bar-fill bar-begoing" id="barFill"></div></div>
</div>

<button class="reset-btn" onclick="resetCurrent()">↺ 이번 주 초기화</button>

<!-- Panels -->
<div class="panel active ch-begoing" id="panel-begoing"></div>
<div class="panel ch-miracle" id="panel-miracle"></div>
<div class="panel ch-attack" id="panel-attack"></div>

<div class="confetti-wrap" id="confettiWrap"></div>

<script>
const CHANNELS = {
  begoing: {
    label: '비고잉',
    days: [
      { day:'월', full:'MONDAY', cls:'mon', tasks:[
        { text:'기본영상 1편 업로드 확인', type:'free' },
      ]},
      { day:'화', full:'TUESDAY', cls:'tue', tasks:[
        { text:'기본영상 2편 업로드 확인', type:'free' },
        { text:'브런치 패턴자료 제작 및 발송', type:'paid' },
        { text:'비비스 1편 업로드 확인', type:'paid' },
        { text:'파이널 1편 업로드 확인', type:'paid' },
      ]},
      { day:'수', full:'WEDNESDAY', cls:'wed', tasks:[
        { text:'기본영상 3편 업로드 확인', type:'free' },
      ]},
      { day:'목', full:'THURSDAY', cls:'thu', tasks:[
        { text:'브런치 패턴자료 제작 및 발송', type:'paid' },
        { text:'비비스 2편 업로드 확인', type:'paid' },
        { text:'파이널 스페셜 업로드 확인', type:'paid' },
        { text:'최종예상수 자료 제작', type:'paid' },
        { text:'조합 만들기', type:'paid' },
      ]},
      { day:'금', full:'FRIDAY', cls:'fri', tasks:[
        { text:'위너 영상 업로드 확인', type:'paid' },
      ]},
      { day:'토', full:'SATURDAY', cls:'sat', tasks:[
        { text:'최종 매회차 노란색 업데이트', type:'paid' },
      ]},
    ]
  },
  miracle: {
    label: '미라클',
    days: [
      { day:'월', full:'MONDAY', cls:'mon', tasks:[
        { text:'기본영상 1편 업로드 확인', type:'free' },
      ]},
      { day:'화', full:'TUESDAY', cls:'tue', tasks:[
        { text:'기본영상 2편 업로드 확인', type:'free' },
      ]},
      { day:'수', full:'WEDNESDAY', cls:'wed', tasks:[
        { text:'커피후원 멤버십 - 기본영상 1,2편 내용정리 자료 제작', type:'paid' },
      ]},
      { day:'목', full:'THURSDAY', cls:'thu', tasks:[
        { text:'기본영상 3편 업로드 확인', type:'free' },
        { text:'커피후원 멤버십 - 기본영상 3편 내용정리 자료 제작', type:'paid' },
        { text:'반자동3수 4조합 제작', type:'paid' },
        { text:'퀸즈 멤버십 1,2편 네이버카페 업로드 확인', type:'paid' },
        { text:'퀸즈 자료 사진 유튜브 퀸즈등급 업로드 확인', type:'paid' },
        { text:'조합 만들기', type:'paid' },
      ]},
    ]
  },
  attack: {
    label: '공략수',
    days: [
      { day:'월', full:'MONDAY', cls:'mon', tasks:[
        { text:'기본영상 1편 업로드 확인', type:'free' },
      ]},
      { day:'화', full:'TUESDAY', cls:'tue', tasks:[
        { text:'기본영상 2편 업로드 확인', type:'free' },
      ]},
      { day:'수', full:'WEDNESDAY', cls:'wed', tasks:[
        { text:'기본영상 3편 업로드 확인', type:'free' },
      ]},
      { day:'목', full:'THURSDAY', cls:'thu', tasks:[
        { text:'기본영상 4편 업로드 확인', type:'free' },
      ]},
    ]
  }
};

const STORAGE_KEY = 'checklist_v2';
let currentChannel = 'begoing';

function getWeekKey() {
  const now = new Date();
  const day = now.getDay();
  const diff = now.getDate() - day + (day === 0 ? -6 : 1);
  const monday = new Date(now);
  monday.setDate(diff);
  return monday.toISOString().split('T')[0];
}

function loadState() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return {};
    const parsed = JSON.parse(raw);
    if (parsed.week !== getWeekKey()) return {};
    return parsed.data || {};
  } catch { return {}; }
}

function saveState() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify({ week: getWeekKey(), data: state }));
}

let state = loadState();

function switchChannel(ch) {
  currentChannel = ch;
  document.querySelectorAll('.tab').forEach((t,i) => {
    const chs = ['begoing','miracle','attack'];
    t.className = 'tab';
    if (chs[i] === ch) t.className = `tab active-${ch}`;
  });
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  document.getElementById(`panel-${ch}`).classList.add('active');
  document.getElementById('barFill').className = `bar-fill bar-${ch}`;
  renderProgress();
}

function renderPanel(ch) {
  const panel = document.getElementById(`panel-${ch}`);
  const chData = CHANNELS[ch];
  panel.innerHTML = '<div class="days-grid" id="grid-' + ch + '"></div>';
  const grid = document.getElementById(`grid-${ch}`);

  chData.days.forEach((dayObj, di) => {
    const allChecked = dayObj.tasks.every((_, ti) => state[`${ch}-${di}-${ti}`]);
    const card = document.createElement('div');
    card.className = `day-card${allChecked ? ` all-done-${ch}` : ''}`;
    card.id = `card-${ch}-${di}`;

    card.innerHTML = `
      <div class="day-header">
        <div class="day-name ${dayObj.cls}">${dayObj.day}</div>
        <div class="day-full">${dayObj.full}</div>
        <div class="day-done-badge badge-${ch}">완료 ✓</div>
      </div>
      <div class="tasks" id="tasks-${ch}-${di}"></div>
    `;
    grid.appendChild(card);

    const tasksEl = document.getElementById(`tasks-${ch}-${di}`);
    dayObj.tasks.forEach((task, ti) => {
      const key = `${ch}-${di}-${ti}`;
      const checked = !!state[key];
      const item = document.createElement('div');
      item.className = `task-item${checked ? ` checked-${ch}` : ''}`;
      item.innerHTML = `
        <div class="checkbox">${checked ? '✓' : ''}</div>
        <div class="task-text">${task.text}</div>
        <div class="tbadge ${task.type}">${task.type === 'free' ? '무료' : '유료'}</div>
      `;
      item.onclick = () => toggleTask(ch, di, ti);
      tasksEl.appendChild(item);
    });
  });
}

function toggleTask(ch, di, ti) {
  const key = `${ch}-${di}-${ti}`;
  state[key] = !state[key];
  saveState();
  renderPanel(ch);
  renderProgress();

  // Check if all done
  const total = CHANNELS[ch].days.reduce((a, d) => a + d.tasks.length, 0);
  const done = CHANNELS[ch].days.reduce((a, d, dIdx) =>
    a + d.tasks.filter((_, tIdx) => state[`${ch}-${dIdx}-${tIdx}`]).length, 0);
  if (done === total) launchConfetti(ch);
}

function renderProgress() {
  const ch = currentChannel;
  const chData = CHANNELS[ch];
  let total = 0, done = 0;
  chData.days.forEach((d, di) => {
    d.tasks.forEach((_, ti) => {
      total++;
      if (state[`${ch}-${di}-${ti}`]) done++;
    });
  });
  document.getElementById('progressCount').innerHTML = `${done} <span>/ ${total}</span>`;
  const pct = total > 0 ? (done / total) * 100 : 0;
  document.getElementById('barFill').style.width = pct + '%';
}

function resetCurrent() {
  const ch = currentChannel;
  if (!confirm(`${CHANNELS[ch].label} 체크리스트를 초기화할까요?`)) return;
  CHANNELS[ch].days.forEach((d, di) => {
    d.tasks.forEach((_, ti) => { delete state[`${ch}-${di}-${ti}`]; });
  });
  saveState();
  renderPanel(ch);
  renderProgress();
}

function updateWeekInfo() {
  const now = new Date();
  const day = now.getDay();
  const diff = now.getDate() - day + (day === 0 ? -6 : 1);
  const mon = new Date(now); mon.setDate(diff);
  const sat = new Date(mon); sat.setDate(mon.getDate() + 5);
  const fmt = d => `${d.getMonth()+1}/${d.getDate()}`;
  const days = ['일','월','화','수','목','금','토'];
  document.getElementById('weekInfo').innerHTML =
    `${fmt(mon)} ~ ${fmt(sat)} &nbsp;|&nbsp; 오늘: <span>${days[new Date().getDay()]}요일</span>`;
}

function launchConfetti(ch) {
  const colors = {
    begoing: ['#6c63ff','#a78bfa','#fff'],
    miracle: ['#f472b6','#fb7185','#fff'],
    attack: ['#34d399','#60a5fa','#fff']
  }[ch];
  const wrap = document.getElementById('confettiWrap');
  for (let i = 0; i < 60; i++) {
    const el = document.createElement('div');
    el.className = 'confetti-piece';
    el.style.left = Math.random() * 100 + '%';
    el.style.background = colors[Math.floor(Math.random() * colors.length)];
    el.style.animationDuration = (1.5 + Math.random() * 2) + 's';
    el.style.animationDelay = Math.random() * 0.8 + 's';
    el.style.width = el.style.height = (6 + Math.random() * 8) + 'px';
    wrap.appendChild(el);
    setTimeout(() => el.remove(), 4000);
  }
}

// Init
updateWeekInfo();
Object.keys(CHANNELS).forEach(ch => renderPanel(ch));
renderProgress();
</script>
</body>
</html>
