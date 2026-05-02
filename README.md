<!D

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX — Train Beyond Limits</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
–black: #0a0a0a;
–off-black: #111111;
–card-bg: #161616;
–lime: #c8f53b;
–lime-dim: #9dba2a;
–white: #f0ede8;
–muted: #888;
–border: rgba(255,255,255,0.07);
}

html { scroll-behavior: smooth; }

body {
background: var(–black);
color: var(–white);
font-family: ‘DM Sans’, sans-serif;
font-weight: 300;
overflow-x: hidden;
cursor: none;
}

/* CUSTOM CURSOR */
.cursor {
width: 12px; height: 12px;
background: var(–lime);
border-radius: 50%;
position: fixed; top: 0; left: 0;
pointer-events: none; z-index: 9999;
transform: translate(-50%,-50%);
transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
mix-blend-mode: difference;
}
.cursor-ring {
width: 36px; height: 36px;
border: 1px solid rgba(200,245,59,0.5);
border-radius: 50%;
position: fixed; top: 0; left: 0;
pointer-events: none; z-index: 9998;
transform: translate(-50%,-50%);
transition: transform 0.18s ease, width 0.25s, height 0.25s;
}
body:has(a:hover) .cursor, body:has(button:hover) .cursor { width: 20px; height: 20px; }

/* NAV */
nav {
position: fixed; top: 0; left: 0; right: 0; z-index: 100;
display: flex; align-items: center; justify-content: space-between;
padding: 24px 48px;
background: linear-gradient(to bottom, rgba(10,10,10,0.95), transparent);
backdrop-filter: blur(0px);
}
.nav-logo {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 28px; letter-spacing: 3px;
color: var(–lime);
}
.nav-links { display: flex; gap: 36px; list-style: none; }
.nav-links a {
color: var(–muted); text-decoration: none;
font-size: 13px; letter-spacing: 1.5px; text-transform: uppercase;
transition: color 0.2s;
}
.nav-links a:hover { color: var(–white); }
.nav-cta {
background: var(–lime); color: var(–black);
border: none; padding: 10px 24px;
font-family: ‘DM Sans’, sans-serif;
font-size: 13px; font-weight: 500;
letter-spacing: 1px; text-transform: uppercase;
cursor: none; transition: background 0.2s, transform 0.15s;
}
.nav-cta:hover { background: #d9ff50; transform: translateY(-1px); }

/* HERO */
.hero {
min-height: 100vh;
display: grid;
grid-template-columns: 1fr 1fr;
position: relative;
overflow: hidden;
}

.hero-left {
display: flex; flex-direction: column;
justify-content: flex-end;
padding: 0 48px 80px 48px;
position: relative; z-index: 2;
}

.hero-tag {
display: inline-flex; align-items: center; gap: 10px;
font-size: 11px; letter-spacing: 3px; text-transform: uppercase;
color: var(–lime); margin-bottom: 28px;
}
.hero-tag::before {
content: ‘’; width: 32px; height: 1px; background: var(–lime);
}

.hero-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: clamp(80px, 10vw, 140px);
line-height: 0.9;
letter-spacing: 2px;
margin-bottom: 28px;
}
.hero-title span { color: var(–lime); }

.hero-sub {
max-width: 400px;
font-size: 15px; line-height: 1.7;
color: rgba(240,237,232,0.6);
margin-bottom: 48px;
}

.hero-actions { display: flex; align-items: center; gap: 28px; }
.btn-primary {
background: var(–lime); color: var(–black);
border: none; padding: 16px 40px;
font-family: ‘DM Sans’, sans-serif;
font-size: 14px; font-weight: 500;
letter-spacing: 1.5px; text-transform: uppercase;
cursor: none; transition: all 0.2s;
position: relative; overflow: hidden;
}
.btn-primary::after {
content: ‘’; position: absolute;
inset: 0; background: rgba(255,255,255,0.15);
transform: translateX(-100%) skewX(-12deg);
transition: transform 0.4s;
}
.btn-primary:hover::after { transform: translateX(150%) skewX(-12deg); }
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 12px 40px rgba(200,245,59,0.3); }

.btn-ghost {
background: transparent; color: var(–white);
border: 1px solid var(–border);
padding: 16px 40px;
font-family: ‘DM Sans’, sans-serif;
font-size: 14px; letter-spacing: 1.5px; text-transform: uppercase;
cursor: none; transition: all 0.2s; text-decoration: none;
display: inline-block;
}
.btn-ghost:hover { border-color: var(–white); background: rgba(255,255,255,0.04); }

.hero-stats {
display: flex; gap: 48px;
margin-top: 64px;
padding-top: 40px;
border-top: 1px solid var(–border);
}
.stat-num {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 42px; color: var(–lime); line-height: 1;
}
.stat-label { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(–muted); margin-top: 4px; }

.hero-right {
position: relative; overflow: hidden;
}
.hero-img {
width: 100%; height: 100%; object-fit: cover;
filter: grayscale(30%) contrast(1.1);
}
.hero-overlay {
position: absolute; inset: 0;
background: linear-gradient(to right, var(–black) 0%, transparent 40%),
linear-gradient(to top, var(–black) 0%, transparent 30%);
}

/* Floating badge */
.hero-badge {
position: absolute; bottom: 80px; right: 48px;
background: var(–lime); color: var(–black);
padding: 20px 28px;
font-family: ‘Bebas Neue’, sans-serif;
font-size: 15px; letter-spacing: 2px;
text-align: center; z-index: 3;
animation: float 3s ease-in-out infinite;
}
.hero-badge span { display: block; font-size: 36px; line-height: 1; }
@keyframes float {
0%, 100% { transform: translateY(0); }
50% { transform: translateY(-10px); }
}

/* MARQUEE */
.marquee-section {
background: var(–lime); padding: 14px 0;
overflow: hidden; white-space: nowrap;
}
.marquee-track {
display: inline-flex; gap: 0;
animation: marquee 20s linear infinite;
}
.marquee-item {
display: inline-flex; align-items: center; gap: 20px;
font-family: ‘Bebas Neue’, sans-serif;
font-size: 16px; letter-spacing: 3px;
color: var(–black); padding: 0 40px;
}
.marquee-item::after { content: ‘◆’; font-size: 10px; }
@keyframes marquee {
from { transform: translateX(0); }
to { transform: translateX(-50%); }
}

/* PROGRAMS */
section { padding: 100px 48px; }
.section-label {
font-size: 11px; letter-spacing: 3px; text-transform: uppercase;
color: var(–lime); margin-bottom: 16px;
display: flex; align-items: center; gap: 12px;
}
.section-label::before { content: ‘’; width: 24px; height: 1px; background: var(–lime); }
.section-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: clamp(42px, 5vw, 64px);
letter-spacing: 2px; line-height: 1;
margin-bottom: 60px;
}

.programs-grid {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 2px;
}
.program-card {
background: var(–card-bg);
padding: 40px 36px;
position: relative; overflow: hidden;
border: 1px solid var(–border);
transition: border-color 0.3s, transform 0.3s;
cursor: none;
}
.program-card::before {
content: ‘’; position: absolute;
bottom: 0; left: 0; right: 0; height: 3px;
background: var(–lime);
transform: scaleX(0); transform-origin: left;
transition: transform 0.4s;
}
.program-card:hover { border-color: rgba(200,245,59,0.3); transform: translateY(-4px); }
.program-card:hover::before { transform: scaleX(1); }

.program-num {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 72px; color: rgba(200,245,59,0.08);
line-height: 1; position: absolute;
top: 20px; right: 24px;
transition: color 0.3s;
}
.program-card:hover .program-num { color: rgba(200,245,59,0.15); }

.program-icon { font-size: 32px; margin-bottom: 20px; }
.program-name {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 28px; letter-spacing: 2px;
margin-bottom: 12px;
}
.program-desc { font-size: 14px; line-height: 1.65; color: rgba(240,237,232,0.55); margin-bottom: 28px; }
.program-meta {
display: flex; gap: 20px;
font-size: 11px; letter-spacing: 1.5px; text-transform: uppercase;
color: var(–muted);
}
.program-meta span { display: flex; align-items: center; gap: 6px; }
.program-meta span::before { content: ‘’; width: 4px; height: 4px; background: var(–lime); border-radius: 50%; }

/* ABOUT / PHILOSOPHY */
.philosophy {
display: grid; grid-template-columns: 1fr 1fr;
gap: 80px; align-items: center;
}
.philosophy-visual {
position: relative; aspect-ratio: 4/5;
background: var(–card-bg);
border: 1px solid var(–border);
overflow: hidden;
}
.philosophy-visual img {
width: 100%; height: 100%; object-fit: cover;
filter: grayscale(40%);
transition: filter 0.5s, transform 0.5s;
}
.philosophy-visual:hover img { filter: grayscale(0%); transform: scale(1.03); }
.philosophy-accent {
position: absolute; top: 28px; left: 28px;
background: var(–lime); color: var(–black);
font-family: ‘Bebas Neue’, sans-serif;
font-size: 13px; letter-spacing: 2px;
padding: 6px 14px;
}

.philosophy-content {}
.philosophy-content p {
font-size: 15px; line-height: 1.8;
color: rgba(240,237,232,0.65);
margin-bottom: 20px;
}
.philosophy-content p:first-of-type {
font-size: 20px; line-height: 1.6; font-weight: 300;
color: var(–white); font-style: italic;
}

.features-list { margin-top: 40px; display: flex; flex-direction: column; gap: 0; }
.feature-item {
display: flex; align-items: flex-start; gap: 20px;
padding: 20px 0; border-bottom: 1px solid var(–border);
}
.feature-item:first-child { border-top: 1px solid var(–border); }
.feature-check {
width: 24px; height: 24px; min-width: 24px;
border: 1px solid var(–lime);
display: flex; align-items: center; justify-content: center;
font-size: 12px; color: var(–lime); margin-top: 2px;
}
.feature-text { font-size: 14px; color: rgba(240,237,232,0.7); line-height: 1.6; }
.feature-text strong { color: var(–white); font-weight: 500; }

/* TRAINERS */
.trainers-grid {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 24px;
}
.trainer-card {
position: relative; overflow: hidden;
aspect-ratio: 3/4;
background: var(–card-bg);
cursor: none;
}
.trainer-card img {
width: 100%; height: 100%; object-fit: cover;
filter: grayscale(60%) contrast(1.1);
transition: filter 0.5s, transform 0.5s;
}
.trainer-card:hover img { filter: grayscale(0%); transform: scale(1.05); }
.trainer-info {
position: absolute; bottom: 0; left: 0; right: 0;
padding: 28px 24px 24px;
background: linear-gradient(to top, rgba(10,10,10,0.95) 0%, transparent 100%);
transform: translateY(0);
}
.trainer-name {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 26px; letter-spacing: 2px;
}
.trainer-role { font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(–lime); margin-top: 4px; }
.trainer-social {
display: flex; gap: 12px; margin-top: 14px;
opacity: 0; transform: translateY(10px);
transition: all 0.3s;
}
.trainer-card:hover .trainer-social { opacity: 1; transform: translateY(0); }
.social-btn {
width: 34px; height: 34px; border: 1px solid rgba(255,255,255,0.3);
display: flex; align-items: center; justify-content: center;
font-size: 13px; color: var(–white); text-decoration: none;
transition: all 0.2s;
}
.social-btn:hover { background: var(–lime); border-color: var(–lime); color: var(–black); }

/* PRICING */
.pricing-grid {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 2px;
}
.pricing-card {
background: var(–card-bg);
padding: 48px 36px;
border: 1px solid var(–border);
position: relative; overflow: hidden;
transition: transform 0.3s;
}
.pricing-card.featured {
background: var(–lime);
border-color: var(–lime);
}
.pricing-card.featured * { color: var(–black) !important; }
.pricing-card.featured .plan-feature::before { background: var(–black) !important; }
.pricing-card.featured .plan-btn { background: var(–black); color: var(–lime) !important; }
.pricing-card.featured .plan-btn:hover { background: var(–off-black); }
.pricing-card:hover { transform: translateY(-6px); }

.plan-badge {
display: inline-block;
font-size: 10px; letter-spacing: 2.5px; text-transform: uppercase;
background: rgba(200,245,59,0.15); color: var(–lime);
padding: 5px 12px; margin-bottom: 28px;
}
.pricing-card.featured .plan-badge { background: rgba(0,0,0,0.2); color: var(–black); }
.plan-name {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 36px; letter-spacing: 2px; margin-bottom: 8px;
}
.plan-price {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 72px; line-height: 1; color: var(–white);
margin-bottom: 4px;
}
.plan-price sup { font-size: 28px; vertical-align: super; }
.plan-period { font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(–muted); margin-bottom: 36px; }
.plan-features { list-style: none; margin-bottom: 40px; display: flex; flex-direction: column; gap: 14px; }
.plan-feature {
font-size: 14px; color: rgba(240,237,232,0.65);
display: flex; align-items: center; gap: 12px;
}
.plan-feature::before {
content: ‘’; width: 5px; height: 5px; min-width: 5px;
background: var(–lime); border-radius: 50%;
}
.plan-btn {
width: 100%; padding: 16px;
background: transparent;
border: 1px solid var(–border);
color: var(–white);
font-family: ‘DM Sans’, sans-serif;
font-size: 13px; font-weight: 500;
letter-spacing: 1.5px; text-transform: uppercase;
cursor: none; transition: all 0.2s;
}
.plan-btn:hover { background: rgba(255,255,255,0.06); border-color: rgba(255,255,255,0.3); }

/* TESTIMONIALS */
.testimonials-bg {
background: var(–off-black);
border-top: 1px solid var(–border);
border-bottom: 1px solid var(–border);
}
.testimonials-grid {
display: grid; grid-template-columns: repeat(3, 1fr);
gap: 2px;
}
.testimonial-card {
background: var(–card-bg);
padding: 40px 32px;
border: 1px solid var(–border);
position: relative;
}
.testimonial-card::before {
content: ‘”’;
font-family: ‘Bebas Neue’, sans-serif;
font-size: 120px; line-height: 0.8;
color: rgba(200,245,59,0.07);
position: absolute; top: 20px; left: 24px;
}
.testimonial-stars { color: var(–lime); font-size: 14px; margin-bottom: 20px; letter-spacing: 2px; }
.testimonial-text { font-size: 14px; line-height: 1.75; color: rgba(240,237,232,0.7); margin-bottom: 28px; font-style: italic; }
.testimonial-author { display: flex; align-items: center; gap: 14px; }
.author-avatar {
width: 42px; height: 42px; border-radius: 50%;
background: linear-gradient(135deg, var(–lime-dim), var(–lime));
display: flex; align-items: center; justify-content: center;
font-family: ‘Bebas Neue’, sans-serif; font-size: 18px; color: var(–black);
}
.author-name { font-size: 14px; font-weight: 500; }
.author-since { font-size: 11px; letter-spacing: 1px; color: var(–muted); margin-top: 2px; }

/* CTA */
.cta-section {
background: var(–lime);
text-align: center; padding: 100px 48px;
}
.cta-section .section-label { color: rgba(0,0,0,0.5); justify-content: center; }
.cta-section .section-label::before { background: rgba(0,0,0,0.4); }
.cta-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: clamp(52px, 7vw, 96px);
color: var(–black); line-height: 0.95;
letter-spacing: 3px; margin-bottom: 24px;
}
.cta-sub { font-size: 16px; color: rgba(0,0,0,0.6); max-width: 480px; margin: 0 auto 48px; line-height: 1.7; }
.btn-dark {
background: var(–black); color: var(–lime);
border: none; padding: 18px 56px;
font-family: ‘DM Sans’, sans-serif;
font-size: 14px; font-weight: 500;
letter-spacing: 2px; text-transform: uppercase;
cursor: none; transition: all 0.2s;
display: inline-block; text-decoration: none;
}
.btn-dark:hover { background: var(–off-black); transform: translateY(-2px); box-shadow: 0 16px 48px rgba(0,0,0,0.3); }

/* FOOTER */
footer {
background: var(–off-black);
padding: 64px 48px 36px;
border-top: 1px solid var(–border);
}
.footer-grid {
display: grid; grid-template-columns: 2fr 1fr 1fr 1fr;
gap: 60px; margin-bottom: 60px;
}
.footer-brand .nav-logo { display: block; margin-bottom: 16px; font-size: 32px; }
.footer-brand p { font-size: 13px; color: var(–muted); line-height: 1.7; max-width: 260px; }
.footer-col h4 {
font-size: 11px; letter-spacing: 2.5px; text-transform: uppercase;
color: var(–white); margin-bottom: 20px;
}
.footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
.footer-col a {
font-size: 13px; color: var(–muted); text-decoration: none;
transition: color 0.2s;
}
.footer-col a:hover { color: var(–lime); }
.footer-bottom {
display: flex; justify-content: space-between; align-items: center;
padding-top: 28px; border-top: 1px solid var(–border);
font-size: 12px; color: var(–muted);
}

/* ANIMATIONS */
.fade-in {
opacity: 0; transform: translateY(30px);
animation: fadeIn 0.7s forwards;
}
@keyframes fadeIn {
to { opacity: 1; transform: translateY(0); }
}
.delay-1 { animation-delay: 0.1s; }
.delay-2 { animation-delay: 0.25s; }
.delay-3 { animation-delay: 0.4s; }
.delay-4 { animation-delay: 0.55s; }
.delay-5 { animation-delay: 0.7s; }

/* Scroll reveal */
.reveal {
opacity: 0; transform: translateY(40px);
transition: opacity 0.7s, transform 0.7s;
}
.reveal.visible { opacity: 1; transform: translateY(0); }

/* Mobile adjustments */
@media (max-width: 900px) {
nav { padding: 20px 24px; }
.nav-links { display: none; }
.hero { grid-template-columns: 1fr; min-height: auto; }
.hero-left { padding: 120px 24px 60px; }
.hero-right { height: 60vw; }
section { padding: 70px 24px; }
.programs-grid, .trainers-grid, .pricing-grid, .testimonials-grid { grid-template-columns: 1fr; }
.philosophy { grid-template-columns: 1fr; }
.footer-grid { grid-template-columns: 1fr 1fr; gap: 36px; }
}
</style>

</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->

<nav>
  <div class="nav-logo">APEX</div>
  <ul class="nav-links">
    <li><a href="#programs">Programs</a></li>
    <li><a href="#trainers">Trainers</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#about">About</a></li>
  </ul>
  <button class="nav-cta">Join Now</button>
</nav>

<!-- HERO -->

<section class="hero" style="padding:0">
  <div class="hero-left">
    <div class="hero-tag fade-in">Est. 2019 — Elite Fitness</div>
    <h1 class="hero-title fade-in delay-1">
      FORGE<br>YOUR<br><span>LIMIT</span>
    </h1>
    <p class="hero-sub fade-in delay-2">
      Science-backed training programs designed to push you past your threshold. Real results, relentless community, expert coaching.
    </p>
    <div class="hero-actions fade-in delay-3">
      <button class="btn-primary">Start Free Trial</button>
      <a href="#programs" class="btn-ghost">View Programs</a>
    </div>
    <div class="hero-stats fade-in delay-4">
      <div>
        <div class="stat-num">12K+</div>
        <div class="stat-label">Members</div>
      </div>
      <div>
        <div class="stat-num">98%</div>
        <div class="stat-label">Retention Rate</div>
      </div>
      <div>
        <div class="stat-num">47</div>
        <div class="stat-label">Expert Trainers</div>
      </div>
    </div>
  </div>
  <div class="hero-right">
    <img src="https://images.unsplash.com/photo-1534438327276-14e5300c3a48?w=900&q=80" alt="Training" class="hero-img">
    <div class="hero-overlay"></div>
    <div class="hero-badge fade-in delay-5">
      <span>#1</span>
      RATED GYM
    </div>
  </div>
</section>

<!-- MARQUEE -->

<div class="marquee-section">
  <div class="marquee-track">
    <span class="marquee-item">Strength Training</span>
    <span class="marquee-item">HIIT Workouts</span>
    <span class="marquee-item">Nutrition Plans</span>
    <span class="marquee-item">Recovery Sessions</span>
    <span class="marquee-item">Mental Resilience</span>
    <span class="marquee-item">Personal Coaching</span>
    <span class="marquee-item">Body Composition</span>
    <span class="marquee-item">Strength Training</span>
    <span class="marquee-item">HIIT Workouts</span>
    <span class="marquee-item">Nutrition Plans</span>
    <span class="marquee-item">Recovery Sessions</span>
    <span class="marquee-item">Mental Resilience</span>
    <span class="marquee-item">Personal Coaching</span>
    <span class="marquee-item">Body Composition</span>
  </div>
</div>

<!-- PROGRAMS -->

<section id="programs">
  <div class="section-label reveal">Training Programs</div>
  <h2 class="section-title reveal">BUILT TO<br>TRANSFORM</h2>
  <div class="programs-grid">
    <div class="program-card reveal">
      <div class="program-num">01</div>
      <div class="program-icon">⚡</div>
      <div class="program-name">Power Surge</div>
      <p class="program-desc">Maximum strength and explosive power training. Built for athletes who refuse to plateau. Compound lifts, progressive overload, and periodization.</p>
      <div class="program-meta">
        <span>5 Days/Week</span>
        <span>90 Min</span>
        <span>Advanced</span>
      </div>
    </div>
    <div class="program-card reveal">
      <div class="program-num">02</div>
      <div class="program-icon">🔥</div>
      <div class="program-name">Inferno HIIT</div>
      <p class="program-desc">High-intensity interval training engineered to shred fat and skyrocket conditioning. Zero wasted minutes. All signal, no noise.</p>
      <div class="program-meta">
        <span>4 Days/Week</span>
        <span>45 Min</span>
        <span>Intermediate</span>
      </div>
    </div>
    <div class="program-card reveal">
      <div class="program-num">03</div>
      <div class="program-icon">🧘</div>
      <div class="program-name">Zen Force</div>
      <p class="program-desc">Mobility, flexibility, and mind-body harmony. The missing piece in most training routines. Reduce injury, accelerate recovery, move better.</p>
      <div class="program-meta">
        <span>3 Days/Week</span>
        <span>60 Min</span>
        <span>All Levels</span>
      </div>
    </div>
    <div class="program-card reveal">
      <div class="program-num">04</div>
      <div class="program-icon">🏋️</div>
      <div class="program-name">Atlas Build</div>
      <p class="program-desc">Body recomposition mastery. Gain lean muscle while burning fat simultaneously. A precise blend of resistance training and metabolic conditioning.</p>
      <div class="program-meta">
        <span>6 Days/Week</span>
        <span>75 Min</span>
        <span>Intermediate</span>
      </div>
    </div>
    <div class="program-card reveal">
      <div class="program-num">05</div>
      <div class="program-icon">🏃</div>
      <div class="program-name">Velocity Run</div>
      <p class="program-desc">Endurance and speed training for those who want to go further and faster. Trail prep, marathon training, or just outrunning yesterday's version of you.</p>
      <div class="program-meta">
        <span>4 Days/Week</span>
        <span>60 Min</span>
        <span>All Levels</span>
      </div>
    </div>
    <div class="program-card reveal">
      <div class="program-num">06</div>
      <div class="program-icon">🥊</div>
      <div class="program-name">Combat Ready</div>
      <p class="program-desc">Boxing, kickboxing, and functional combat conditioning. Builds coordination, reaction time, and full-body strength while being undeniably fun.</p>
      <div class="program-meta">
        <span>3 Days/Week</span>
        <span>60 Min</span>
        <span>All Levels</span>
      </div>
    </div>
  </div>
</section>

<!-- ABOUT / PHILOSOPHY -->

<section id="about" style="background: var(--off-black); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);">
  <div class="philosophy">
    <div class="philosophy-visual reveal">
      <img src="https://images.unsplash.com/photo-1571019614242-c5c5dee9f50b?w=600&q=80" alt="Philosophy">
      <div class="philosophy-accent">Our Philosophy</div>
    </div>
    <div class="philosophy-content">
      <div class="section-label reveal">The APEX Way</div>
      <h2 class="section-title reveal" style="margin-bottom: 32px;">MORE THAN<br>A GYM</h2>
      <p class="reveal">"Most gyms sell you a membership. We sell you a transformation. The difference is everything."</p>
      <p class="reveal">At APEX, we believe the gap between who you are and who you can be is closed through consistent, intelligent effort — guided by people who genuinely care about your outcomes.</p>
      <div class="features-list">
        <div class="feature-item reveal">
          <div class="feature-check">✓</div>
          <div class="feature-text"><strong>Evidence-based programming</strong> — Every session is designed around sports science, not trends or guesswork.</div>
        </div>
        <div class="feature-item reveal">
          <div class="feature-check">✓</div>
          <div class="feature-text"><strong>Personalized coaching</strong> — Your coach knows your goals, your history, and your next breakthrough.</div>
        </div>
        <div class="feature-item reveal">
          <div class="feature-check">✓</div>
          <div class="feature-text"><strong>Community accountability</strong> — A culture that celebrates hard work and holds you to your highest standard.</div>
        </div>
        <div class="feature-item reveal">
          <div class="feature-check">✓</div>
          <div class="feature-text"><strong>Holistic approach</strong> — Training, nutrition, recovery, and mindset — the four pillars of lasting transformation.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- TRAINERS -->

<section id="trainers">
  <div class="section-label reveal">Expert Team</div>
  <h2 class="section-title reveal">MEET YOUR<br>COACHES</h2>
  <div class="trainers-grid">
    <div class="trainer-card reveal">
      <img src="https://images.unsplash.com/photo-1571731956672-f2b94d7dd0cb?w=500&q=80" alt="Trainer">
      <div class="trainer-info">
        <div class="trainer-name">Marcus Cole</div>
        <div class="trainer-role">Strength & Power Coach</div>
        <div class="trainer-social">
          <a class="social-btn" href="#">in</a>
          <a class="social-btn" href="#">ig</a>
        </div>
      </div>
    </div>
    <div class="trainer-card reveal">
      <img src="https://images.unsplash.com/photo-1594381898411-846e7d193883?w=500&q=80" alt="Trainer">
      <div class="trainer-info">
        <div class="trainer-name">Sofia Reyes</div>
        <div class="trainer-role">HIIT & Conditioning</div>
        <div class="trainer-social">
          <a class="social-btn" href="#">in</a>
          <a class="social-btn" href="#">ig</a>
        </div>
      </div>
    </div>
    <div class="trainer-card reveal">
      <img src="https://images.unsplash.com/photo-1567013127542-490d757e51cd?w=500&q=80" alt="Trainer">
      <div class="trainer-info">
        <div class="trainer-name">James Park</div>
        <div class="trainer-role">Mobility & Recovery</div>
        <div class="trainer-social">
          <a class="social-btn" href="#">in</a>
          <a class="social-btn" href="#">ig</a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->

<section id="pricing" style="background: var(--off-black); border-top: 1px solid var(--border);">
  <div class="section-label reveal">Simple Pricing</div>
  <h2 class="section-title reveal">CHOOSE YOUR<br>COMMITMENT</h2>
  <div class="pricing-grid">
    <div class="pricing-card reveal">
      <div class="plan-badge">Starter</div>
      <div class="plan-name">Foundation</div>
      <div class="plan-price"><sup>$</sup>49</div>
      <div class="plan-period">Per Month</div>
      <ul class="plan-features">
        <li class="plan-feature">Gym floor access</li>
        <li class="plan-feature">2 group classes/week</li>
        <li class="plan-feature">Basic app access</li>
        <li class="plan-feature">Fitness assessment</li>
      </ul>
      <button class="plan-btn">Get Started</button>
    </div>
    <div class="pricing-card featured reveal">
      <div class="plan-badge">Most Popular</div>
      <div class="plan-name">Elite</div>
      <div class="plan-price"><sup>$</sup>99</div>
      <div class="plan-period">Per Month</div>
      <ul class="plan-features">
        <li class="plan-feature">Unlimited access</li>
        <li class="plan-feature">All group classes</li>
        <li class="plan-feature">1 PT session/month</li>
        <li class="plan-feature">Full app + nutrition</li>
        <li class="plan-feature">Recovery lounge</li>
      </ul>
      <button class="plan-btn">Get Started</button>
    </div>
    <div class="pricing-card reveal">
      <div class="plan-badge">Ultimate</div>
      <div class="plan-name">Apex</div>
      <div class="plan-price"><sup>$</sup>189</div>
      <div class="plan-period">Per Month</div>
      <ul class="plan-features">
        <li class="plan-feature">Everything in Elite</li>
        <li class="plan-feature">4 PT sessions/month</li>
        <li class="plan-feature">Custom meal plans</li>
        <li class="plan-feature">Priority booking</li>
        <li class="plan-feature">Body composition scans</li>
      </ul>
      <button class="plan-btn">Get Started</button>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->

<section class="testimonials-bg">
  <div class="section-label reveal">Social Proof</div>
  <h2 class="section-title reveal">REAL PEOPLE,<br>REAL RESULTS</h2>
  <div class="testimonials-grid">
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p class="testimonial-text">Lost 28 lbs in 4 months and gained more confidence than I ever thought possible. The coaches here don't let you make excuses — and that's exactly what I needed.</p>
      <div class="testimonial-author">
        <div class="author-avatar">JM</div>
        <div>
          <div class="author-name">Jordan M.</div>
          <div class="author-since">Member since 2023</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p class="testimonial-text">I've tried 5 other gyms. APEX is different. The programming is intelligent, the community is tight-knit, and I've hit PRs every single month for the past year.</p>
      <div class="testimonial-author">
        <div class="author-avatar">AT</div>
        <div>
          <div class="author-name">Alex T.</div>
          <div class="author-since">Member since 2022</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p class="testimonial-text">Came back from a knee injury thinking I'd never train hard again. The mobility and recovery program here rebuilt me from the ground up. Game changer.</p>
      <div class="testimonial-author">
        <div class="author-avatar">SR</div>
        <div>
          <div class="author-name">Sam R.</div>
          <div class="author-since">Member since 2024</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CTA -->

<section class="cta-section" style="padding-top:100px;padding-bottom:100px">
  <div class="section-label reveal">Limited Spots Available</div>
  <h2 class="cta-title reveal">READY TO<br>START?</h2>
  <p class="cta-sub reveal">Your first 14 days are on us. No credit card needed. Just show up ready to work.</p>
  <a href="#" class="btn-dark reveal">Claim Free Trial</a>
</section>

<!-- FOOTER -->

<footer>
  <div class="footer-grid">
    <div class="footer-brand">
      <span class="nav-logo">APEX</span>
      <p>Train beyond limits. We exist to push human potential — one session at a time.</p>
    </div>
    <div class="footer-col">
      <h4>Programs</h4>
      <ul>
        <li><a href="#">Power Surge</a></li>
        <li><a href="#">Inferno HIIT</a></li>
        <li><a href="#">Zen Force</a></li>
        <li><a href="#">Atlas Build</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Company</h4>
      <ul>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Our Trainers</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Press</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Support</h4>
      <ul>
        <li><a href="#">Contact</a></li>
        <li><a href="#">FAQ</a></li>
        <li><a href="#">Privacy Policy</a></li>
        <li><a href="#">Terms</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span>© 2026 APEX Fitness. All rights reserved.</span>
    <span>Crafted with obsession.</span>
  </div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animateCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animateCursor);
  }
  animateCursor();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 60);
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(r => io.observe(r));
</script>

</body>
</html>
