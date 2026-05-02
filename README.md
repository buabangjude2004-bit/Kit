<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FitLog — Daily Tracker</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0f;
    --surface: #13131a;
    --border: #1e1e2e;
    --accent: #c8f135;
    --accent2: #ff6b6b;
    --accent3: #6bb5ff;
    --text: #e8e8f0;
    --muted: #6b6b80;
    --card: #16161f;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Noise texture overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.5;
  }

  header {
    padding: 2rem 2rem 1rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  header h1 {
    font-size: 1.4rem;
    font-weight: 800;
    letter-spacing: -0.03em;
  }

  header h1 span { color: var(--accent); }

  .date-badge {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 0.3rem 0.75rem;
    border-radius: 100px;
  }

  .main {
    max-width: 480px;
    margin: 0 auto;
    padding: 1.5rem 1.25rem 6rem;
  }

  /* NAV TABS */
  .tabs {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1.75rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 0.35rem;
  }

  .tab {
    flex: 1;
    padding: 0.55rem 0;
    text-align: center;
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--muted);
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.03em;
    border: none;
    background: none;
  }

  .tab.active {
    background: var(--accent);
    color: #0a0a0f;
  }

  /* SECTION */
  .section { display: none; }
  .section.active { display: block; }

  /* CARDS */
  .card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.25rem;
    margin-bottom: 1rem;
  }

  .card-title {
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 1rem;
  }

  /* WATER TRACKER */
  .water-display {
    display: flex;
    align-items: flex-end;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .water-number {
    font-size: 3.5rem;
    font-weight: 800;
    line-height: 1;
    color: var(--accent3);
  }

  .water-unit {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: var(--muted);
    padding-bottom: 0.6rem;
  }

  .water-glasses {
    display: flex;
    gap: 0.35rem;
    flex-wrap: wrap;
    margin-bottom: 1rem;
  }

  .glass {
    width: 32px;
    height: 38px;
    border-radius: 4px 4px 7px 7px;
    border: 2px solid var(--border);
    cursor: pointer;
    transition: all 0.15s;
    position: relative;
    overflow: hidden;
    background: var(--surface);
  }

  .glass.filled {
    border-color: var(--accent3);
    background: var(--accent3);
  }

  .glass:hover { transform: translateY(-2px); }

  .water-btn {
    display: flex;
    gap: 0.5rem;
  }

  .btn {
    flex: 1;
    padding: 0.65rem;
    border: none;
    border-radius: 10px;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.85rem;
    cursor: pointer;
    transition: all 0.15s;
  }

  .btn-primary {
    background: var(--accent3);
    color: #0a0a0f;
  }

  .btn-ghost {
    background: var(--surface);
    color: var(--muted);
    border: 1px solid var(--border);
  }

  .btn:hover { filter: brightness(1.1); transform: translateY(-1px); }
  .btn:active { transform: translateY(0); }

  /* STEPS */
  .steps-ring-wrap {
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }

  svg.ring { transform: rotate(-90deg); }

  .ring-center {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .ring-wrap {
    position: relative;
    width: 110px;
    height: 110px;
    flex-shrink: 0;
  }

  .steps-info { flex: 1; }

  .steps-big {
    font-size: 2.2rem;
    font-weight: 800;
    line-height: 1;
    color: var(--accent);
  }

  .steps-goal {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    margin-top: 0.25rem;
  }

  .steps-input-row {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
  }

  input[type="number"], input[type="text"], select {
    background: var(--surface);
    border: 1px solid var(--border);
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.9rem;
    padding: 0.6rem 0.85rem;
    border-radius: 10px;
    flex: 1;
    outline: none;
    transition: border-color 0.2s;
  }

  input:focus, select:focus { border-color: var(--accent); }

  /* WORKOUTS */
  .workout-list { list-style: none; }

  .workout-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.8rem 0;
    border-bottom: 1px solid var(--border);
  }

  .workout-item:last-child { border-bottom: none; }

  .workout-left { display: flex; align-items: center; gap: 0.75rem; }

  .workout-icon {
    width: 36px;
    height: 36px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.1rem;
    background: var(--surface);
    border: 1px solid var(--border);
  }

  .workout-name { font-weight: 700; font-size: 0.9rem; }
  .workout-meta { font-family: 'DM Mono', monospace; font-size: 0.7rem; color: var(--muted); }

  .workout-cal {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: var(--accent2);
    font-weight: 500;
  }

  .del-btn {
    background: none;
    border: none;
    color: var(--muted);
    cursor: pointer;
    font-size: 1rem;
    padding: 0.25rem;
    margin-left: 0.5rem;
    transition: color 0.15s;
  }
  .del-btn:hover { color: var(--accent2); }

  .add-workout-form {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
    flex-wrap: wrap;
  }

  select { flex: 1; min-width: 120px; }

  /* SUMMARY */
  .summary-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.75rem;
    margin-bottom: 1rem;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1rem;
  }

  .stat-label {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 0.4rem;
  }

  .stat-value {
    font-size: 1.8rem;
    font-weight: 800;
    line-height: 1;
  }

  .stat-sub {
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    color: var(--muted);
    margin-top: 0.25rem;
  }

  .progress-bar-wrap {
    height: 6px;
    background: var(--border);
    border-radius: 100px;
    overflow: hidden;
    margin-top: 0.5rem;
  }

  .progress-bar {
    height: 100%;
    border-radius: 100px;
    transition: width 0.5s ease;
  }

  .tip-card {
    background: linear-gradient(135deg, #1a1a2e, #16213e);
    border: 1px solid #2a2a4e;
    border-radius: 16px;
    padding: 1.25rem;
    margin-top: 1rem;
  }

  .tip-label {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 0.5rem;
  }

  .tip-text {
    font-size: 0.88rem;
    line-height: 1.55;
    color: #b0b0d0;
  }

  /* TOAST */
  .toast {
    position: fixed;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: var(--accent);
    color: #0a0a0f;
    font-weight: 700;
    font-size: 0.85rem;
    padding: 0.65rem 1.5rem;
    border-radius: 100px;
    transition: transform 0.3s cubic-bezier(0.34,1.56,0.64,1);
    z-index: 999;
    white-space: nowrap;
  }

  .toast.show { transform: translateX(-50%) translateY(0); }

  @media (max-width: 400px) {
    .water-number { font-size: 2.5rem; }
    .steps-big { font-size: 1.8rem; }
  }
</style>
</head>
<body>

<header>
  <h1>Fit<span>Log</span></h1>
  <div class="date-badge" id="dateBadge"></div>
</header>

<div class="main">
  <div class="tabs">
    <button class="tab active" onclick="switchTab('water', this)">💧 Water</button>
    <button class="tab" onclick="switchTab('steps', this)">👟 Steps</button>
    <button class="tab" onclick="switchTab('workout', this)">🏋️ Workout</button>
    <button class="tab" onclick="switchTab('summary', this)">📊 Summary</button>
  </div>

  <!-- WATER -->
  <div class="section active" id="water">
    <div class="card">
      <div class="card-title">Daily Hydration</div>
      <div class="water-display">
        <div class="water-number" id="waterCount">0</div>
        <div class="water-unit">/ 8 glasses</div>
      </div>
      <div class="water-glasses" id="glassesGrid"></div>
      <div class="water-btn">
        <button class="btn btn-primary" onclick="addWater()">+ Add Glass</button>
        <button class="btn btn-ghost" onclick="resetWater()">Reset</button>
      </div>
    </div>
    <div class="card">
      <div class="card-title">Why it matters</div>
      <p style="font-size:0.85rem;line-height:1.6;color:var(--muted)">Staying hydrated improves energy, focus, and metabolism. Aim for 8 glasses (2L) daily. Your kidneys, skin, and joints will thank you.</p>
    </div>
  </div>

  <!-- STEPS -->
  <div class="section" id="steps">
    <div class="card">
      <div class="card-title">Step Count</div>
      <div class="steps-ring-wrap">
        <div class="ring-wrap">
          <svg class="ring" width="110" height="110" viewBox="0 0 110 110">
            <circle cx="55" cy="55" r="46" fill="none" stroke="var(--border)" stroke-width="9"/>
            <circle cx="55" cy="55" r="46" fill="none" stroke="var(--accent)" stroke-width="9"
              stroke-linecap="round" stroke-dasharray="289" stroke-dashoffset="289" id="stepsRing"
              style="transition: stroke-dashoffset 0.6s ease"/>
          </svg>
          <div class="ring-center" style="transform:none;">
            <div style="font-size:0.65rem;font-weight:700;letter-spacing:0.08em;color:var(--muted);text-align:center;padding-top:2px">DONE</div>
          </div>
        </div>
        <div class="steps-info">
          <div class="steps-big" id="stepsDisplay">0</div>
          <div class="steps-goal">Goal: <span id="stepsGoal">10,000</span> steps</div>
          <div style="margin-top:0.6rem">
            <div class="progress-bar-wrap">
              <div class="progress-bar" id="stepsBar" style="width:0%;background:var(--accent)"></div>
            </div>
            <div style="font-family:'DM Mono',monospace;font-size:0.7rem;color:var(--muted);margin-top:0.35rem" id="stepsPct">0% of goal</div>
          </div>
        </div>
      </div>
      <div class="steps-input-row">
        <input type="number" id="stepsInput" placeholder="Enter steps..." min="0" max="99999">
        <button class="btn btn-primary" style="flex:0;padding:0.65rem 1.1rem" onclick="logSteps()">Log</button>
      </div>
    </div>
  </div>

  <!-- WORKOUT -->
  <div class="section" id="workout">
    <div class="card">
      <div class="card-title">Today's Workouts</div>
      <ul class="workout-list" id="workoutList">
        <li style="color:var(--muted);font-size:0.85rem;padding:0.75rem 0;font-family:'DM Mono',monospace">No workouts logged yet.</li>
      </ul>
      <div class="add-workout-form">
        <select id="workoutType">
          <option value="🏃 Running">🏃 Running</option>
          <option value="🚴 Cycling">🚴 Cycling</option>
          <option value="🏊 Swimming">🏊 Swimming</option>
          <option value="🏋️ Lifting">🏋️ Lifting</option>
          <option value="🧘 Yoga">🧘 Yoga</option>
          <option value="🥊 Boxing">🥊 Boxing</option>
          <option value="🚶 Walking">🚶 Walking</option>
          <option value="⚽ Sports">⚽ Sports</option>
        </select>
        <input type="number" id="workoutDur" placeholder="min" min="1" max="300" style="flex:0;width:72px">
        <button class="btn btn-primary" style="flex:0;padding:0.65rem 1rem" onclick="addWorkout()">Add</button>
      </div>
    </div>
  </div>

  <!-- SUMMARY -->
  <div class="section" id="summary">
    <div class="summary-grid">
      <div class="stat-card">
        <div class="stat-label">💧 Water</div>
        <div class="stat-value" style="color:var(--accent3)" id="sumWater">0</div>
        <div class="stat-sub">glasses today</div>
        <div class="progress-bar-wrap" style="margin-top:0.6rem">
          <div class="progress-bar" id="sumWaterBar" style="width:0%;background:var(--accent3)"></div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-label">👟 Steps</div>
        <div class="stat-value" style="color:var(--accent)" id="sumSteps">0</div>
        <div class="stat-sub">steps today</div>
        <div class="progress-bar-wrap" style="margin-top:0.6rem">
          <div class="progress-bar" id="sumStepsBar" style="width:0%;background:var(--accent)"></div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-label">🔥 Calories</div>
        <div class="stat-value" style="color:var(--accent2)" id="sumCals">0</div>
        <div class="stat-sub">kcal burned</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">⏱ Active</div>
        <div class="stat-value" style="color:#c084fc" id="sumMins">0</div>
        <div class="stat-sub">minutes total</div>
      </div>
    </div>
    <div class="tip-card">
      <div class="tip-label">✦ Daily Tip</div>
      <div class="tip-text" id="tipText"></div>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
  const state = {
    water: 0,
    steps: 0,
    workouts: []
  };

  const tips = [
    "Even 30 minutes of moderate exercise per day can reduce the risk of heart disease by up to 35%.",
    "Drink a glass of water first thing in the morning to kickstart your metabolism.",
    "A 10-minute walk after meals improves blood sugar levels significantly.",
    "Rest days are not lazy days — muscles grow during recovery, not just during exercise.",
    "Consistency beats intensity. Showing up every day matters more than going hard occasionally.",
    "Sleep 7–9 hours. It's when your body repairs, builds muscle, and regulates hunger hormones."
  ];

  const calPerMin = {
    '🏃 Running': 11,
    '🚴 Cycling': 8,
    '🏊 Swimming': 9,
    '🏋️ Lifting': 6,
    '🧘 Yoga': 3,
    '🥊 Boxing': 10,
    '🚶 Walking': 4,
    '⚽ Sports': 7
  };

  function init() {
    const now = new Date();
    document.getElementById('dateBadge').textContent = now.toLocaleDateString('en-GB', { weekday: 'short', day: 'numeric', month: 'short' });
    document.getElementById('tipText').textContent = tips[now.getDay() % tips.length];
    renderGlasses();
  }

  function switchTab(id, el) {
    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    el.classList.add('active');
    if (id === 'summary') updateSummary();
  }

  /* WATER */
  function renderGlasses() {
    const grid = document.getElementById('glassesGrid');
    grid.innerHTML = '';
    for (let i = 0; i < 8; i++) {
      const g = document.createElement('div');
      g.className = 'glass' + (i < state.water ? ' filled' : '');
      g.onclick = () => { state.water = i + 1 < state.water ? i : i + 1; renderGlasses(); };
      grid.appendChild(g);
    }
    document.getElementById('waterCount').textContent = state.water;
  }

  function addWater() {
    if (state.water >= 8) { showToast('Goal reached! 🎉'); return; }
    state.water++;
    renderGlasses();
    if (state.water === 8) showToast('Hydration goal hit! 💧');
  }

  function resetWater() { state.water = 0; renderGlasses(); }

  /* STEPS */
  function logSteps() {
    const val = parseInt(document.getElementById('stepsInput').value);
    if (!val || val < 0) return;
    state.steps = val;
    document.getElementById('stepsInput').value = '';
    updateStepsUI();
    showToast('Steps logged ✓');
  }

  function updateStepsUI() {
    const goal = 10000;
    const pct = Math.min(state.steps / goal, 1);
    document.getElementById('stepsDisplay').textContent = state.steps.toLocaleString();
    document.getElementById('stepsBar').style.width = (pct * 100) + '%';
    document.getElementById('stepsPct').textContent = Math.round(pct * 100) + '% of goal';
    document.getElementById('stepsRing').style.strokeDashoffset = 289 - (289 * pct);
  }

  /* WORKOUT */
  function addWorkout() {
    const type = document.getElementById('workoutType').value;
    const dur = parseInt(document.getElementById('workoutDur').value);
    if (!dur || dur < 1) return;
    const cal = Math.round((calPerMin[type] || 6) * dur);
    state.workouts.push({ type, dur, cal });
    document.getElementById('workoutDur').value = '';
    renderWorkouts();
    showToast('Workout added 🔥');
  }

  function renderWorkouts() {
    const list = document.getElementById('workoutList');
    if (!state.workouts.length) {
      list.innerHTML = '<li style="color:var(--muted);font-size:0.85rem;padding:0.75rem 0;font-family:\'DM Mono\',monospace">No workouts logged yet.</li>';
      return;
    }
    list.innerHTML = state.workouts.map((w, i) => `
      <li class="workout-item">
        <div class="workout-left">
          <div class="workout-icon">${w.type.split(' ')[0]}</div>
          <div>
            <div class="workout-name">${w.type.split(' ').slice(1).join(' ')}</div>
            <div class="workout-meta">${w.dur} min</div>
          </div>
        </div>
        <div style="display:flex;align-items:center;gap:0.25rem">
          <div class="workout-cal">~${w.cal} kcal</div>
          <button class="del-btn" onclick="removeWorkout(${i})">✕</button>
        </div>
      </li>
    `).join('');
  }

  function removeWorkout(i) {
    state.workouts.splice(i, 1);
    renderWorkouts();
  }

  /* SUMMARY */
  function updateSummary() {
    const totalCals = state.workouts.reduce((s, w) => s + w.cal, 0);
    const totalMins = state.workouts.reduce((s, w) => s + w.dur, 0);
    document.getElementById('sumWater').textContent = state.water;
    document.getElementById('sumSteps').textContent = state.steps.toLocaleString();
    document.getElementById('sumCals').textContent = totalCals;
    document.getElementById('sumMins').textContent = totalMins;
    document.getElementById('sumWaterBar').style.width = Math.min(state.water / 8 * 100, 100) + '%';
    document.getElementById('sumStepsBar').style.width = Math.min(state.steps / 10000 * 100, 100) + '%';
  }

  /* TOAST */
  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 2200);
  }

  init();
</script>
</body>
</html>
