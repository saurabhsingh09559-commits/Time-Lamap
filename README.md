# Time-Lamap
This is time lamp for students
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>StudyLamp — Focus & Streak Tracker</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Lora:wght@500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #1c1a17;
    --bg-raised: #262320;
    --bg-raised2: #2e2a26;
    --line: #3a352f;
    --text: #f0e9dd;
    --text-dim: #a89e8e;
    --amber: #f2a65a;
    --sage: #8fae7a;
    --coral: #e0745f;
    --serif: 'Lora', serif;
    --sans: 'Inter', sans-serif;
    --mono: 'JetBrains Mono', monospace;
  }
  *{ box-sizing:border-box; margin:0; padding:0; }
  body{ background: var(--bg); color: var(--text); font-family: var(--sans); line-height:1.5; -webkit-font-smoothing: antialiased; }
  .wrap{ max-width: 760px; margin:0 auto; padding: 0 24px; }
  a{ color: inherit; }

  header{ padding: 28px 0; }
  header .wrap{ display:flex; align-items:center; justify-content:space-between; }
  .logo{ font-family: var(--serif); font-weight:700; font-size: 20px; display:flex; align-items:center; gap:10px; }
  .logo .bulb{ width:10px; height:10px; border-radius:50%; background: var(--amber); box-shadow: 0 0 14px 4px rgba(242,166,90,0.55); }
  .tagline{ font-size: 12.5px; color: var(--text-dim); font-family: var(--mono); }

  main{ padding: 20px 0 60px; }

  .hero-text{ text-align:center; margin-bottom: 34px; }
  .hero-text h1{ font-family: var(--serif); font-size: 26px; font-weight: 600; margin-bottom: 8px; }
  .hero-text p{ color: var(--text-dim); font-size: 14.5px; max-width: 420px; margin: 0 auto; }

  .timer-card{
    background: radial-gradient(ellipse at top, var(--bg-raised2), var(--bg-raised));
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 44px 24px 36px;
    text-align:center;
    box-shadow: 0 24px 70px rgba(0,0,0,.4);
    margin-bottom: 40px;
  }
  #clock{ font-family: var(--mono); font-size: 68px; font-weight: 700; letter-spacing: 2px; color: var(--amber); text-shadow: 0 0 30px rgba(242,166,90,0.35); }
  .mode-label{ font-family: var(--mono); font-size: 12px; color: var(--text-dim); letter-spacing: 1.5px; margin-top: 6px; text-transform: uppercase; }

  .mode-switch{ display:flex; justify-content:center; gap: 8px; margin-top: 22px; }
  .mode-btn{ font-family: var(--mono); font-size: 12px; padding: 7px 14px; border-radius: 20px; border: 1px solid var(--line); background: none; color: var(--text-dim); cursor: pointer; transition: all .15s; }
  .mode-btn.active{ background: var(--sage); color: #16261a; border-color: var(--sage); font-weight: 600; }

  .controls{ display:flex; justify-content:center; gap: 12px; margin-top: 26px; }
  .btn{ font-family: var(--sans); font-weight: 600; font-size: 14px; padding: 12px 26px; border-radius: 8px; border: 1px solid var(--line); background: none; color: var(--text); cursor: pointer; transition: transform .15s, border-color .15s; }
  .btn:hover{ transform: translateY(-1px); border-color: var(--amber); }
  .btn.primary{ background: var(--amber); color: #2a1c0c; border-color: var(--amber); }

  .stats-grid{ display:grid; grid-template-columns: repeat(3,1fr); gap: 14px; margin-bottom: 34px; }
  .stat-card{ background: var(--bg-raised); border: 1px solid var(--line); border-radius: 10px; padding: 18px; text-align:center; }
  .stat-card .num{ font-family: var(--serif); font-size: 28px; font-weight: 700; color: var(--sage); }
  .stat-card .lbl{ font-size: 12px; color: var(--text-dim); margin-top: 4px; }

  h2{ font-family: var(--serif); font-size: 16px; font-weight:600; margin-bottom: 16px; color: var(--amber); }

  .weekday-row{ display:grid; grid-template-columns: repeat(7, 1fr); gap: 6px; margin-bottom: 8px; }
  .weekday-row span{ text-align:center; font-family: var(--mono); font-size: 11px; color: var(--text-dim); }
  .month-labels{ display:flex; justify-content: space-between; font-family: var(--mono); font-size: 11px; color: var(--text-dim); margin-bottom: 6px; padding: 0 2px; }
  .heatmap{ display:grid; grid-template-columns: repeat(7, 1fr); gap: 6px; margin-bottom: 40px; }
  .day-cell{ aspect-ratio: 1; border-radius: 4px; background: var(--bg-raised); border: 1px solid var(--line); display:flex; align-items:center; justify-content:center; font-family: var(--mono); font-size: 10px; color: var(--text-dim); }
  .day-cell.done{ background: var(--sage); border-color: var(--sage); color: #16261a; font-weight:700; }
  .day-cell.today{ box-shadow: 0 0 0 2px var(--amber) inset; }

  .quote-box{ border-left: 3px solid var(--coral); padding: 14px 18px; background: var(--bg-raised); border-radius: 0 8px 8px 0; font-family: var(--serif); font-style: italic; font-size: 15px; color: var(--text); min-height: 20px; }

  footer{ text-align:center; padding: 30px 0; color: var(--text-dim); font-size: 12.5px; font-family: var(--mono); border-top: 1px solid var(--line); }

  @media(max-width:520px){
    #clock{ font-size: 52px; }
    .stats-grid{ grid-template-columns: 1fr 1fr 1fr; gap: 8px; }
  }
</style>
</head>
<body>

<header>
  <div class="wrap">
    <div class="logo"><div class="bulb"></div>StudyLamp</div>
    <div class="tagline">focus · streak · repeat</div>
  </div>
</header>

<main class="wrap">
  <div class="hero-text">
    <h1>One lamp. One session. One streak.</h1>
    <p>A focus timer built for students — start a session, build a streak, and watch the habit stick.</p>
  </div>

  <div class="timer-card">
    <div id="clock">25:00</div>
    <div class="mode-label" id="modeLabel">Focus session</div>

    <div class="mode-switch">
      <button class="mode-btn active" data-mins="25" data-mode="Focus session">Focus 25</button>
      <button class="mode-btn" data-mins="45" data-mode="Deep focus">Deep 45</button>
      <button class="mode-btn" data-mins="5" data-mode="Short break">Break 5</button>
    </div>

    <div class="controls">
      <button class="btn primary" id="startBtn">Start</button>
      <button class="btn" id="resetBtn">Reset</button>
    </div>
  </div>

  <div class="stats-grid">
    <div class="stat-card"><div class="num" id="streakNum">0</div><div class="lbl">day streak</div></div>
    <div class="stat-card"><div class="num" id="sessionsNum">0</div><div class="lbl">sessions today</div></div>
    <div class="stat-card"><div class="num" id="totalNum">0</div><div class="lbl">total sessions</div></div>
  </div>

  <h2>// last 35 days</h2>
  <div class="month-labels" id="monthLabels"></div>
  <div class="weekday-row">
    <span>Mon</span><span>Tue</span><span>Wed</span><span>Thu</span><span>Fri</span><span>Sat</span><span>Sun</span>
  </div>
  <div class="heatmap" id="heatmap"></div>

  <h2>// today's fuel</h2>
  <div class="quote-box" id="quoteBox">Small sessions, done daily, beat long sessions done rarely.</div>
</main>

<footer>built with StudyLamp — edit freely, ship it as your hackathon project</footer>

<script>
  const clockEl = document.getElementById('clock');
  const modeLabelEl = document.getElementById('modeLabel');
  const startBtn = document.getElementById('startBtn');
  const resetBtn = document.getElementById('resetBtn');
  const modeBtns = document.querySelectorAll('.mode-btn');

  let totalSeconds = 25 * 60;
  let remaining = totalSeconds;
  let timerId = null;
  let running = false;

  function formatTime(s){
    const m = Math.floor(s/60).toString().padStart(2,'0');
    const sec = (s%60).toString().padStart(2,'0');
    return `${m}:${sec}`;
  }

  function updateClock(){ clockEl.textContent = formatTime(remaining); }

  modeBtns.forEach(btn => {
    btn.addEventListener('click', () => {
      if(running) return;
      modeBtns.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      totalSeconds = parseInt(btn.dataset.mins) * 60;
      remaining = totalSeconds;
      modeLabelEl.textContent = btn.dataset.mode;
      updateClock();
    });
  });

  startBtn.addEventListener('click', () => {
    if(running){
      clearInterval(timerId);
      running = false;
      startBtn.textContent = 'Start';
    } else {
      running = true;
      startBtn.textContent = 'Pause';
      timerId = setInterval(() => {
        remaining--;
        updateClock();
        if(remaining <= 0){
          clearInterval(timerId);
          running = false;
          startBtn.textContent = 'Start';
          onSessionComplete();
        }
      }, 1000);
    }
  });

  resetBtn.addEventListener('click', () => {
    clearInterval(timerId);
    running = false;
    startBtn.textContent = 'Start';
    remaining = totalSeconds;
    updateClock();
  });

  // ---- streak / stats logic ----
  const todayKey = () => new Date().toISOString().slice(0,10);

  function loadData(){
    const raw = localStorage.getItem('studylamp_data');
    return raw ? JSON.parse(raw) : { days: {}, total: 0 };
  }
  function saveData(data){ localStorage.setItem('studylamp_data', JSON.stringify(data)); }

  function onSessionComplete(){
    const data = loadData();
    const t = todayKey();
    data.days[t] = (data.days[t] || 0) + 1;
    data.total += 1;
    saveData(data);
    renderStats();
    renderHeatmap();
    showQuote();
  }

  function calcStreak(data){
    let streak = 0;
    let d = new Date();
    while(true){
      const key = d.toISOString().slice(0,10);
      if(data.days[key] && data.days[key] > 0){
        streak++;
        d.setDate(d.getDate() - 1);
      } else break;
    }
    return streak;
  }

  function renderStats(){
    const data = loadData();
    document.getElementById('streakNum').textContent = calcStreak(data);
    document.getElementById('sessionsNum').textContent = data.days[todayKey()] || 0;
    document.getElementById('totalNum').textContent = data.total;
  }

  const monthNames = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];

  function renderHeatmap(){
    const data = loadData();
    const container = document.getElementById('heatmap');
    const monthLabelsEl = document.getElementById('monthLabels');
    container.innerHTML = '';
    monthLabelsEl.innerHTML = '';

    const today = new Date();
    // Find the most recent Sunday on/after today, then go back 5 full weeks (35 days)
    // so the grid always ends on a Sunday and starts on a Monday.
    const endOfWeek = new Date(today);
    const jsDay = endOfWeek.getDay(); // 0=Sun..6=Sat
    const daysToSunday = (7 - jsDay) % 7;
    endOfWeek.setDate(endOfWeek.getDate() + daysToSunday);

    const startDate = new Date(endOfWeek);
    startDate.setDate(startDate.getDate() - 34);

    const monthsSeen = [];
    for(let i = 0; i < 35; i++){
      const d = new Date(startDate);
      d.setDate(startDate.getDate() + i);
      const key = d.toISOString().slice(0,10);
      const isFuture = d > today;

      const cell = document.createElement('div');
      cell.className = 'day-cell';
      cell.textContent = d.getDate();
      if(isFuture){
        cell.style.opacity = '0.25';
      } else {
        if(data.days[key] && data.days[key] > 0) cell.classList.add('done');
        cell.title = `${key}: ${data.days[key] || 0} session(s)`;
      }
      if(key === todayKey()) cell.classList.add('today');
      container.appendChild(cell);

      if(d.getDate() === 1 || i === 0){
        monthsSeen.push(monthNames[d.getMonth()]);
      }
    }
    monthLabelsEl.textContent = '';
    [...new Set(monthsSeen)].forEach(m => {
      const span = document.createElement('span');
      span.textContent = m;
      monthLabelsEl.appendChild(span);
    });
  }

  const quotes = [
    "Small sessions, done daily, beat long sessions done rarely.",
    "You don't need more time — you need one more focused session.",
    "The streak isn't the goal. The habit it builds is.",
    "One session down. Future you says thanks.",
    "Progress hides inside boring, repeated sessions.",
    "Discipline is just remembered motivation."
  ];
  function showQuote(){
    document.getElementById('quoteBox').textContent = quotes[Math.floor(Math.random() * quotes.length)];
  }

  // init
  updateClock();
  renderStats();
  renderHeatmap();
</script>

</body>
</html>
