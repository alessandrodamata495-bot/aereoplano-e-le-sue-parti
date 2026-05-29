# aereoplano-e-le-sue-parti<!DOCTYPE html>
<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Anatomia del Volo — Architettura e Strumentazione del Velivolo</title>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@300;400;600;700;900&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --sky: #0a1628;
    --sky-mid: #0d2044;
    --horizon: #0e3460;
    --cloud: #e8f0fe;
    --accent: #4fc3f7;
    --accent2: #f97316;
    --accent3: #22c55e;
    --accent4: #a78bfa;
    --gold: #fbbf24;
    --text: #cdd6f4;
    --text-dim: #7c8db8;
    --card-bg: rgba(13, 32, 68, 0.7);
    --card-border: rgba(79, 195, 247, 0.2);
    --modal-bg: #07112a;
    --font-display: 'Barlow Condensed', sans-serif;
    --font-body: 'Crimson Pro', serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--sky);
    color: var(--text);
    font-family: var(--font-body);
    font-size: 16px;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* STARS BACKGROUND */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      radial-gradient(1px 1px at 10% 15%, rgba(255,255,255,0.6) 0%, transparent 100%),
      radial-gradient(1px 1px at 30% 40%, rgba(255,255,255,0.4) 0%, transparent 100%),
      radial-gradient(1px 1px at 55% 20%, rgba(255,255,255,0.5) 0%, transparent 100%),
      radial-gradient(1px 1px at 75% 60%, rgba(255,255,255,0.3) 0%, transparent 100%),
      radial-gradient(1px 1px at 90% 10%, rgba(255,255,255,0.6) 0%, transparent 100%),
      radial-gradient(1px 1px at 20% 80%, rgba(255,255,255,0.4) 0%, transparent 100%),
      radial-gradient(1px 1px at 45% 70%, rgba(255,255,255,0.5) 0%, transparent 100%),
      radial-gradient(1px 1px at 65% 85%, rgba(255,255,255,0.3) 0%, transparent 100%),
      radial-gradient(2px 2px at 85% 35%, rgba(255,255,255,0.2) 0%, transparent 100%),
      radial-gradient(1px 1px at 5% 55%, rgba(255,255,255,0.5) 0%, transparent 100%);
    pointer-events: none;
    z-index: 0;
  }

  /* HEADER */
  .header {
    position: relative;
    z-index: 10;
    padding: 80px 40px 60px;
    text-align: center;
    overflow: hidden;
  }

  .header::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), var(--accent2), transparent);
  }

  .header-eyebrow {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.2s forwards;
  }

  .header h1 {
    font-family: var(--font-display);
    font-size: clamp(36px, 7vw, 80px);
    font-weight: 900;
    line-height: 0.95;
    letter-spacing: -1px;
    color: #fff;
    text-transform: uppercase;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.4s forwards;
  }

  .header h1 span {
    color: var(--accent);
  }

  .header-sub {
    margin-top: 20px;
    font-size: 18px;
    font-style: italic;
    color: var(--text-dim);
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.6s forwards;
  }

  /* PLANE SVG HERO */
  .plane-hero {
    position: relative;
    z-index: 10;
    display: flex;
    justify-content: center;
    padding: 40px 20px;
    opacity: 0;
    animation: fadeUp 1s ease 0.8s forwards;
  }

  .plane-hero svg {
    filter: drop-shadow(0 0 30px rgba(79,195,247,0.3));
  }

  /* SECTIONS GRID */
  .sections-title {
    text-align: center;
    font-family: var(--font-display);
    font-size: 13px;
    letter-spacing: 5px;
    color: var(--text-dim);
    text-transform: uppercase;
    padding: 20px 40px 30px;
    position: relative;
    z-index: 10;
  }

  .grid {
    position: relative;
    z-index: 10;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
    padding: 20px 40px 80px;
    max-width: 1400px;
    margin: 0 auto;
  }

  /* CARDS */
  .card {
    background: var(--card-bg);
    border: 1px solid var(--card-border);
    border-radius: 4px;
    padding: 28px 24px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    backdrop-filter: blur(12px);
    transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
    opacity: 0;
    transform: translateY(30px);
  }

  .card.visible {
    opacity: 1;
    transform: translateY(0);
    transition: opacity 0.6s ease, transform 0.6s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  }

  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: var(--card-accent, var(--accent));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s ease;
  }

  .card:hover::before { transform: scaleX(1); }

  .card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(79,195,247,0.06) 0%, transparent 60%);
    pointer-events: none;
    opacity: 0;
    transition: opacity 0.3s;
  }

  .card:hover::after { opacity: 1; }
  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 0 1px var(--card-accent, var(--accent));
    border-color: var(--card-accent, var(--accent));
  }

  .card-icon {
    width: 48px;
    height: 48px;
    margin-bottom: 16px;
    opacity: 0.9;
  }

  .card-tag {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--card-accent, var(--accent));
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .card h2 {
    font-family: var(--font-display);
    font-size: 22px;
    font-weight: 700;
    color: #fff;
    margin-bottom: 10px;
    line-height: 1.1;
  }

  .card p {
    font-size: 14px;
    color: var(--text-dim);
    line-height: 1.5;
  }

  .card-arrow {
    position: absolute;
    bottom: 20px;
    right: 20px;
    font-family: var(--font-mono);
    font-size: 20px;
    color: var(--card-accent, var(--accent));
    opacity: 0.4;
    transition: opacity 0.3s, transform 0.3s;
  }

  .card:hover .card-arrow {
    opacity: 1;
    transform: translate(4px, -4px);
  }

  /* MODAL */
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(2, 6, 18, 0.92);
    z-index: 1000;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    overflow-y: auto;
    padding: 20px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
    backdrop-filter: blur(4px);
  }

  .modal-overlay.open {
    opacity: 1;
    pointer-events: all;
  }

  .modal {
    background: var(--modal-bg);
    border: 1px solid rgba(79,195,247,0.25);
    border-radius: 8px;
    max-width: 860px;
    width: 100%;
    margin: auto;
    position: relative;
    transform: translateY(40px) scale(0.97);
    transition: transform 0.4s cubic-bezier(0.34,1.56,0.64,1);
    overflow: hidden;
  }

  .modal-overlay.open .modal {
    transform: translateY(0) scale(1);
  }

  .modal-header {
    padding: 32px 36px 24px;
    border-bottom: 1px solid rgba(79,195,247,0.1);
    position: relative;
  }

  .modal-tag {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--modal-accent, var(--accent));
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .modal-header h2 {
    font-family: var(--font-display);
    font-size: 36px;
    font-weight: 900;
    color: #fff;
    line-height: 1;
    text-transform: uppercase;
  }

  .modal-close {
    position: absolute;
    top: 24px; right: 24px;
    background: none;
    border: 1px solid rgba(79,195,247,0.2);
    color: var(--text-dim);
    width: 36px; height: 36px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 18px;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }

  .modal-close:hover {
    background: rgba(79,195,247,0.1);
    color: #fff;
    border-color: var(--accent);
  }

  .modal-body {
    padding: 32px 36px;
  }

  .modal-body h3 {
    font-family: var(--font-display);
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--modal-accent, var(--accent));
    margin: 28px 0 12px;
    padding-bottom: 6px;
    border-bottom: 1px solid rgba(79,195,247,0.1);
  }

  .modal-body p {
    font-size: 16px;
    color: var(--text);
    line-height: 1.7;
    margin-bottom: 14px;
  }

  .formula-box {
    background: rgba(0,0,0,0.4);
    border: 1px solid rgba(79,195,247,0.15);
    border-left: 3px solid var(--modal-accent, var(--accent));
    border-radius: 4px;
    padding: 16px 20px;
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--cloud);
    margin: 14px 0;
    overflow-x: auto;
    line-height: 1.8;
  }

  .example-box {
    background: rgba(34,197,94,0.06);
    border: 1px solid rgba(34,197,94,0.2);
    border-radius: 4px;
    padding: 16px 20px;
    margin: 14px 0;
  }

  .example-box .ex-label {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--accent3);
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .example-box p {
    font-size: 14px;
    color: var(--text);
  }

  .info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 12px;
    margin: 16px 0;
  }

  .info-item {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 4px;
    padding: 14px;
  }

  .info-item .label {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--text-dim);
    text-transform: uppercase;
    margin-bottom: 4px;
  }

  .info-item .value {
    font-family: var(--font-display);
    font-size: 18px;
    font-weight: 600;
    color: #fff;
  }

  svg text {
    font-family: var(--font-display), sans-serif;
  }

  /* Table */
  table {
    width: 100%;
    border-collapse: collapse;
    margin: 14px 0;
    font-size: 14px;
  }

  th {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-dim);
    padding: 8px 12px;
    text-align: left;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  td {
    padding: 8px 12px;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    color: var(--text);
  }

  tr:hover td { background: rgba(255,255,255,0.03); }

  /* FOOTER */
  footer {
    position: relative;
    z-index: 10;
    text-align: center;
    padding: 40px;
    border-top: 1px solid rgba(255,255,255,0.05);
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--text-dim);
    letter-spacing: 2px;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes spinSlow {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 0.6; }
    50% { opacity: 1; }
  }

  @keyframes dash {
    to { stroke-dashoffset: -20; }
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    .header { padding: 50px 20px 40px; }
    .grid { padding: 20px; gap: 14px; }
    .modal-body, .modal-header { padding: 20px; }
    .modal-header h2 { font-size: 26px; }
  }

  /* NACA CANVAS */
  #naca-canvas {
    background: #05090f;
    border-radius: 6px;
    border: 1px solid rgba(79,195,247,0.2);
    display: block;
    width: 100%;
    height: 300px;
  }

  .naca-controls {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    margin: 12px 0;
    align-items: center;
  }

  .naca-controls label {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 1px;
    color: var(--text-dim);
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .naca-controls input[type=range] {
    accent-color: var(--accent);
    width: 100px;
  }

  .naca-controls span {
    color: var(--accent);
    font-weight: 500;
  }

  /* Instrument dial animation */
  @keyframes needleSway {
    0%, 100% { transform: rotate(-30deg); transform-origin: bottom center; }
    50% { transform: rotate(40deg); transform-origin: bottom center; }
  }

  .gauge-needle { animation: needleSway 4s ease-in-out infinite; transform-origin: 50% 90%; }

  /* Axis animation */
  @keyframes axisRotX {
    0%, 100% { transform: rotateX(0deg); }
    50% { transform: rotateX(15deg); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }
  .plane-float { animation: float 4s ease-in-out infinite; }
</style>
</head>
<body>

<!-- HEADER -->
<header class="header">
  <div class="header-eyebrow">Costruzioni Aeronautiche · Meccanica del Volo</div>
  <h1>Anatomia del <span>Volo</span></h1>
  <p class="header-sub">Architettura, dinamica e strumentazione del velivolo — dalla struttura portante ai profili NACA</p>
</header>

<!-- HERO PLANE SVG -->
<div class="plane-hero">
  <svg class="plane-float" width="520" height="200" viewBox="0 0 520 200" xmlns="http://www.w3.org/2000/svg">
    <!-- Fuselage -->
    <ellipse cx="260" cy="110" rx="180" ry="28" fill="#0d2550" stroke="#4fc3f7" stroke-width="1.2"/>
    <!-- Nose -->
    <path d="M440 110 Q490 110 502 110 Q490 108 440 106 Z" fill="#4fc3f7" opacity="0.6"/>
    <!-- Wings -->
    <path d="M200 112 L130 160 L130 168 L200 130 Z" fill="#1a3a6b" stroke="#4fc3f7" stroke-width="1"/>
    <path d="M200 108 L130 60 L130 52 L200 90 Z" fill="#1a3a6b" stroke="#4fc3f7" stroke-width="1"/>
    <!-- Wing details -->
    <line x1="150" y1="158" x2="200" y2="130" stroke="#4fc3f7" stroke-width="0.5" opacity="0.4"/>
    <line x1="150" y1="62" x2="200" y2="90" stroke="#4fc3f7" stroke-width="0.5" opacity="0.4"/>
    <!-- Tail -->
    <path d="M90 110 L60 145 L70 148 L90 118 Z" fill="#1a3a6b" stroke="#4fc3f7" stroke-width="1"/>
    <path d="M90 108 L60 75 L70 72 L90 102 Z" fill="#1a3a6b" stroke="#4fc3f7" stroke-width="1"/>
    <!-- Vertical tail -->
    <path d="M90 110 L75 75 L80 73 L95 110 Z" fill="#1a3a6b" stroke="#4fc3f7" stroke-width="1"/>
    <!-- Engine 1 -->
    <ellipse cx="180" cy="138" rx="20" ry="9" fill="#0a1f40" stroke="#f97316" stroke-width="1.2"/>
    <!-- Engine 2 -->
    <ellipse cx="180" cy="82" rx="20" ry="9" fill="#0a1f40" stroke="#f97316" stroke-width="1.2"/>
    <!-- Windows -->
    <circle cx="380" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <circle cx="360" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <circle cx="340" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <circle cx="320" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <circle cx="300" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <circle cx="280" cy="105" r="4" fill="none" stroke="#4fc3f7" stroke-width="1" opacity="0.6"/>
    <!-- Axes labels -->
    <text x="500" y="118" fill="#f97316" font-size="10" font-family="'Barlow Condensed',sans-serif" opacity="0.7">→ IMBARDATA</text>
    <text x="168" y="46" fill="#22c55e" font-size="10" font-family="'Barlow Condensed',sans-serif" opacity="0.7">↑ ROLLIO</text>
    <text x="100" y="148" fill="#a78bfa" font-size="10" font-family="'Barlow Condensed',sans-serif" opacity="0.7">↻ BECCHEGGIO</text>
    <!-- Glow effect -->
    <ellipse cx="260" cy="110" rx="200" ry="40" fill="none" stroke="#4fc3f7" stroke-width="0.3" opacity="0.2"/>
  </svg>
</div>

<div class="sections-title">— Seleziona una sezione per approfondire —</div>

<!-- CARDS GRID -->
<div class="grid">

  <!-- Card 1: Componenti Strutturali -->
  <div class="card" style="--card-accent:#4fc3f7" onclick="openModal('strutturali')">
    <div class="card-tag">Struttura</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M24 8 L40 36 L8 36 Z" stroke="#4fc3f7" stroke-width="1.5" fill="rgba(79,195,247,0.1)"/>
      <line x1="24" y1="8" x2="24" y2="36" stroke="#4fc3f7" stroke-width="0.8" opacity="0.5"/>
      <line x1="16" y1="22" x2="32" y2="22" stroke="#4fc3f7" stroke-width="0.8" opacity="0.5"/>
    </svg>
    <h2>Componenti Strutturali Fondamentali</h2>
    <p>Ala, fusoliera, impennaggi e carrello. Analisi delle funzioni portanti e dei carichi strutturali.</p>
    <span class="card-arrow">↗</span>
  </div>

  <!-- Card 2: Tre Assi -->
  <div class="card" style="--card-accent:#f97316" onclick="openModal('assi')">
    <div class="card-tag">Dinamica del Volo</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="24" cy="24" r="12" stroke="#f97316" stroke-width="1.5" fill="rgba(249,115,22,0.08)"/>
      <line x1="4" y1="24" x2="44" y2="24" stroke="#f97316" stroke-width="1.5"/>
      <line x1="24" y1="4" x2="24" y2="44" stroke="#22c55e" stroke-width="1.5"/>
      <ellipse cx="24" cy="24" rx="12" ry="5" stroke="#a78bfa" stroke-width="1" fill="none"/>
    </svg>
    <h2>I Tre Assi di Volo</h2>
    <p>Rollio (longitudinale), beccheggio (trasversale) e imbardata (verticale). Superfici di controllo.</p>
    <span class="card-arrow">↗</span>
  </div>

  <!-- Card 3: Geometria Alare -->
  <div class="card" style="--card-accent:#a78bfa" onclick="openModal('alare')">
    <div class="card-tag">Aerodinamica</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M4 28 Q20 10 44 20" stroke="#a78bfa" stroke-width="2" fill="none"/>
      <path d="M4 28 Q20 38 44 20" stroke="#a78bfa" stroke-width="2" fill="rgba(167,139,250,0.1)"/>
      <line x1="4" y1="28" x2="44" y2="20" stroke="#a78bfa" stroke-width="0.6" stroke-dasharray="3,3"/>
    </svg>
    <h2>Geometria Alare e Profili NACA</h2>
    <p>Allungamento alare, winglets, profili NACA a 4 cifre. Formule per la distribuzione degli spessori.</p>
    <span class="card-arrow">↗</span>
  </div>

  <!-- Card 4: Sistema Pitot-Statica -->
  <div class="card" style="--card-accent:#22c55e" onclick="openModal('pitot')">
    <div class="card-tag">Strumentazione</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="18" y="20" width="20" height="16" rx="2" stroke="#22c55e" stroke-width="1.5" fill="rgba(34,197,94,0.08)"/>
      <path d="M8 28 L18 28" stroke="#22c55e" stroke-width="2"/>
      <circle cx="6" cy="28" r="3" fill="#22c55e" opacity="0.6"/>
      <line x1="22" y1="28" x2="34" y2="28" stroke="#22c55e" stroke-width="0.8" opacity="0.5"/>
      <line x1="22" y1="24" x2="34" y2="24" stroke="#22c55e" stroke-width="0.8" opacity="0.5"/>
      <line x1="22" y1="32" x2="34" y2="32" stroke="#22c55e" stroke-width="0.8" opacity="0.5"/>
    </svg>
    <h2>Sistema Pitot-Statica</h2>
    <p>Misura di velocità, quota e rateo di salita tramite pressione totale e statica. Teorema di Bernoulli.</p>
    <span class="card-arrow">↗</span>
  </div>

  <!-- Card 5: Strumenti Barometrici -->
  <div class="card" style="--card-accent:#fbbf24" onclick="openModal('barometrici')">
    <div class="card-tag">Strumentazione</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="24" cy="24" r="18" stroke="#fbbf24" stroke-width="1.5" fill="rgba(251,191,36,0.05)"/>
      <path d="M14 32 L24 16 L34 32" stroke="#fbbf24" stroke-width="1.5" fill="none"/>
      <!-- Tick marks -->
      <line x1="24" y1="7" x2="24" y2="11" stroke="#fbbf24" stroke-width="1.5"/>
      <line x1="37" y1="14" x2="34" y2="17" stroke="#fbbf24" stroke-width="1.5"/>
      <line x1="41" y1="24" x2="37" y2="24" stroke="#fbbf24" stroke-width="1.5"/>
    </svg>
    <h2>Strumenti a Capsula Barometrica</h2>
    <p>Altimetro, anemometro (IAS) e variometro. Principi fisici, scale di lettura e codice colori.</p>
    <span class="card-arrow">↗</span>
  </div>

  <!-- Card 6: Strumenti Giroscopici -->
  <div class="card" style="--card-accent:#e879f9" onclick="openModal('giroscopici')">
    <div class="card-tag">Strumentazione</div>
    <svg class="card-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="24" cy="24" r="10" stroke="#e879f9" stroke-width="1.5" fill="rgba(232,121,249,0.08)"/>
      <ellipse cx="24" cy="24" rx="10" ry="4" stroke="#e879f9" stroke-width="1" fill="none" transform="rotate(30 24 24)"/>
      <ellipse cx="24" cy="24" rx="10" ry="4" stroke="#e879f9" stroke-width="1" fill="none" transform="rotate(-30 24 24)"/>
      <circle cx="24" cy="24" r="2" fill="#e879f9"/>
    </svg>
    <h2>Strumenti Giroscopici</h2>
    <p>Orizzonte artificiale, virosbandometro, girodirezionale. Rigidità giroscopica e precessione.</p>
    <span class="card-arrow">↗</span>
  </div>

</div>

<!-- FOOTER -->
<footer>
  <p>Anatomia del Volo · Costruzioni Aeronautiche · Meccanica del Volo</p>
</footer>

<!-- MODAL OVERLAY -->
<div class="modal-overlay" id="modal-overlay" onclick="handleOverlayClick(event)">
  <div class="modal" id="modal-content">
    <div class="modal-header">
      <div class="modal-tag" id="modal-tag"></div>
      <h2 id="modal-title"></h2>
      <button class="modal-close" onclick="closeModal()">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<script>
// ─── SCROLL REVEAL ───────────────────────────────────
const observer = new IntersectionObserver((entries) => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 100);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.card').forEach(c => observer.observe(c));

// ─── MOUSE GLOW ON CARDS ─────────────────────────────
document.querySelectorAll('.card').forEach(card => {
  card.addEventListener('mousemove', e => {
    const r = card.getBoundingClientRect();
    card.style.setProperty('--mx', ((e.clientX - r.left) / r.width * 100) + '%');
    card.style.setProperty('--my', ((e.clientY - r.top) / r.height * 100) + '%');
  });
});

// ─── MODAL SYSTEM ────────────────────────────────────
const modals = {

  strutturali: {
    tag: 'Struttura del Velivolo',
    title: 'Componenti Strutturali Fondamentali',
    accent: '#4fc3f7',
    body: `
      <p>Il velivolo è un sistema meccanico complesso la cui struttura deve resistere ai carichi aerodinamici, inerziali e gravitazionali durante tutte le fasi del volo. I quattro componenti primari sono l'ala, la fusoliera, gli impennaggi e gli organi di decollo/atterraggio.</p>

      <h3>Ala — Portanza</h3>
      <p>L'ala è la superficie portante principale. Genera la forza di portanza <b>L</b> grazie alla forma asimmetrica del profilo alare e all'angolo di attacco α. La portanza si oppone al peso dell'aeromobile e consente il volo livellato quando <em>L = W</em>.</p>
      <div class="formula-box">
L = ½ · ρ · V² · S · C<sub>L</sub>
<br>
Dove:
  ρ = densità dell'aria [kg/m³]
  V = velocità dell'aria [m/s]
  S = superficie alare [m²]
  C<sub>L</sub> = coefficiente di portanza (adimensionale)
      </div>
      <p>Il coefficiente C<sub>L</sub> dipende dall'angolo di attacco α e dal profilo alare scelto. Cresce linearmente con α fino allo stallo (α<sub>stallo</sub> ≈ 15°–20° per profili standard).</p>

      <h3>Fusoliera — Struttura</h3>
      <p>La fusoliera è il corpo principale del velivolo e svolge funzioni strutturali (collegamento di tutti i sottosistemi), aerodinamiche (riduzione della resistenza) e di carico (passeggeri, cargo, carburante). Le costruzioni moderne adottano la struttura <em>semimonoscocca</em> (longheroni + centine + rivestimento portante).</p>

      <svg viewBox="0 0 500 140" xmlns="http://www.w3.org/2000/svg" style="width:100%;margin:16px 0;border-radius:4px;background:rgba(0,0,0,0.3)">
        <!-- Fuselage cross section -->
        <ellipse cx="250" cy="70" rx="160" ry="50" fill="none" stroke="#4fc3f7" stroke-width="1.5"/>
        <!-- Frames (centine) -->
        <line x1="130" y1="40" x2="130" y2="100" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <line x1="175" y1="23" x2="175" y2="117" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <line x1="220" y1="20" x2="220" y2="120" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <line x1="265" y1="20" x2="265" y2="120" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <line x1="310" y1="22" x2="310" y2="118" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <line x1="355" y1="30" x2="355" y2="110" stroke="#4fc3f7" stroke-width="0.8" opacity="0.4"/>
        <!-- Longherons -->
        <line x1="90" y1="50" x2="410" y2="50" stroke="#f97316" stroke-width="1.2" opacity="0.6"/>
        <line x1="90" y1="90" x2="410" y2="90" stroke="#f97316" stroke-width="1.2" opacity="0.6"/>
        <line x1="90" y1="70" x2="410" y2="70" stroke="#f97316" stroke-width="0.6" opacity="0.3" stroke-dasharray="4,4"/>
        <!-- Labels -->
        <text x="420" y="53" fill="#f97316" font-size="10" font-family="'Barlow Condensed',sans-serif">Longheroni</text>
        <text x="420" y="93" fill="#f97316" font-size="10" font-family="'Barlow Condensed',sans-serif">Longheroni</text>
        <text x="170" y="13" fill="#4fc3f7" font-size="10" font-family="'Barlow Condensed',sans-serif">Centine (frames)</text>
        <text x="200" y="135" fill="#22c55e" font-size="10" font-family="'Barlow Condensed',sans-serif">Struttura Semimonoscocca</text>
      </svg>

      <h3>Impennaggi — Stabilità</h3>
      <p>Gli impennaggi orizzontali (stabilizzatore + equilibratore) e verticali (deriva + timone di direzione) forniscono stabilità statica e dinamica intorno agli assi di beccheggio e imbardata. Il piano orizzontale è solitamente dimensionato per avere un coefficiente di superficie <em>V<sub>H</sub></em> (volume di coda) compreso tra 0,3 e 0,6 per velivoli da trasporto.</p>

      <h3>Organi di Decollo/Atterraggio</h3>
      <p>Il carrello di atterraggio deve assorbire l'energia cinetica verticale durante il touchdown. L'energia da dissipare è:</p>
      <div class="formula-box">
E = ½ · m · V<sub>z</sub>²
Dove V<sub>z</sub> = velocità verticale di atterraggio (tipicamente 3 m/s per aviazione generale, 2 m/s per trasporto)
      </div>

      <div class="info-grid">
        <div class="info-item"><div class="label">Portanza max</div><div class="value" style="color:#4fc3f7">L = W</div></div>
        <div class="info-item"><div class="label">α stallo tipico</div><div class="value" style="color:#f97316">~15–20°</div></div>
        <div class="info-item"><div class="label">Struttura fusoliera</div><div class="value" style="color:#22c55e">Semimonoscocca</div></div>
        <div class="info-item"><div class="label">V coda orizzontale</div><div class="value" style="color:#a78bfa">0.3–0.6</div></div>
      </div>

      <div class="example-box">
        <div class="ex-label">Esempio Applicato</div>
        <p>Un Cessna 172 ha una superficie alare S = 16,2 m². A velocità di crociera V = 58 m/s a livello del mare (ρ = 1,225 kg/m³), con C<sub>L</sub> = 0,4, la portanza generata è:<br><br>
        <strong>L = ½ × 1,225 × 58² × 16,2 × 0,4 ≈ 13.400 N ≈ 1.367 kgf</strong><br><br>
        Questo bilancia il peso massimo al decollo del velivolo (MTOW ≈ 1.111 kg + carburante e passeggeri).</p>
      </div>
    `
  },

  assi: {
    tag: 'Dinamica del Volo',
    title: 'I Tre Assi di Volo',
    accent: '#f97316',
    body: `
      <p>Il moto di un velivolo nello spazio tridimensionale è descritto attorno a tre assi ortogonali tra loro, tutti passanti per il centro di gravità (CG) del velivolo. Ogni asse corrisponde a un rotazione specifica e a una superficie di controllo dedicata.</p>

      <!-- INTERACTIVE 3D AXES WIDGET -->
      <div id="axes-widget" style="position:relative;border-radius:8px;overflow:hidden;background:#04080f;border:1px solid rgba(79,195,247,0.2);margin:16px 0;">
        <canvas id="axes-canvas" style="display:block;width:100%;height:360px;cursor:grab;touch-action:none;"></canvas>
        <div style="position:absolute;top:12px;left:50%;transform:translateX(-50%);display:flex;gap:8px;z-index:10;flex-wrap:wrap;justify-content:center;">
          <button onclick="axisAnim('roll')"  id="btn-roll"
            style="font-family:'Barlow Condensed',sans-serif;font-size:12px;letter-spacing:2px;padding:6px 14px;border-radius:4px;border:1px solid #22c55e;background:rgba(34,197,94,0.12);color:#22c55e;cursor:pointer;text-transform:uppercase;transition:all .2s">
            ↺ ROLLIO
          </button>
          <button onclick="axisAnim('pitch')" id="btn-pitch"
            style="font-family:'Barlow Condensed',sans-serif;font-size:12px;letter-spacing:2px;padding:6px 14px;border-radius:4px;border:1px solid #a78bfa;background:rgba(167,139,250,0.12);color:#a78bfa;cursor:pointer;text-transform:uppercase;transition:all .2s">
            ↕ BECCHEGGIO
          </button>
          <button onclick="axisAnim('yaw')"   id="btn-yaw"
            style="font-family:'Barlow Condensed',sans-serif;font-size:12px;letter-spacing:2px;padding:6px 14px;border-radius:4px;border:1px solid #f97316;background:rgba(249,115,22,0.12);color:#f97316;cursor:pointer;text-transform:uppercase;transition:all .2s">
            ↻ IMBARDATA
          </button>
          <button onclick="axisAnim('reset')" id="btn-reset"
            style="font-family:'Barlow Condensed',sans-serif;font-size:12px;letter-spacing:2px;padding:6px 14px;border-radius:4px;border:1px solid rgba(255,255,255,0.2);background:rgba(255,255,255,0.05);color:rgba(255,255,255,0.5);cursor:pointer;text-transform:uppercase;transition:all .2s">
            ⟳ RESET
          </button>
        </div>
        <div style="position:absolute;bottom:10px;left:50%;transform:translateX(-50%);font-family:'Barlow Condensed',sans-serif;font-size:10px;letter-spacing:2px;color:rgba(255,255,255,0.25);white-space:nowrap;pointer-events:none;">
          TRASCINA PER RUOTARE · CLICCA UN ASSE PER ANIMARE
        </div>
      </div>

      <h3>Rollio — Asse Longitudinale</h3>
      <p>Il rollio è la rotazione attorno all'asse longitudinale (che va dalla coda al muso). È controllato dagli <strong>alettoni</strong>, superfici mobili posizionate sul bordo d'uscita delle ali. Quando l'alettone destro si abbassa, la portanza dell'ala destra aumenta e l'aereo ruota verso sinistra (rollio a sinistra).</p>
      <div class="formula-box">
Momento di rollio:  L = q · S · b · C<sub>l</sub>
Dove:
  q = pressione dinamica = ½ρV²
  b = apertura alare
  C<sub>l</sub> = coefficiente di momento di rollio
      </div>

      <h3>Beccheggio — Asse Trasversale</h3>
      <p>Il beccheggio è la rotazione dell'asse trasversale (che va da un'ala all'altra). Corrisponde alla variazione dell'angolo di assetto longitudinale θ. È controllato dall'<strong>equilibratore</strong> (elevator), superficie mobile sull'impennaggio orizzontale.</p>
      <div class="formula-box">
Momento di beccheggio:  M = q · S · c̄ · C<sub>m</sub>
Dove:
  c̄ = corda media aerodinamica (MAC)
  C<sub>m</sub> = coefficiente di momento di beccheggio
  Stabilità statica longitudinale: dC<sub>m</sub>/dC<sub>L</sub> < 0
      </div>

      <h3>Imbardata — Asse Verticale</h3>
      <p>L'imbardata è la rotazione attorno all'asse verticale che passa per il CG. Corrisponde alla variazione dell'angolo di rotta ψ. È controllata dal <strong>timone di direzione</strong> (rudder), superficie mobile sulla deriva verticale. Un'imbardata non coordinata produce lo <em>slipping</em> del velivolo.</p>

      <div class="info-grid">
        <div class="info-item"><div class="label">Rollio → Controllo</div><div class="value" style="color:#22c55e">Alettoni</div></div>
        <div class="info-item"><div class="label">Beccheggio → Controllo</div><div class="value" style="color:#a78bfa">Equilibratore</div></div>
        <div class="info-item"><div class="label">Imbardata → Controllo</div><div class="value" style="color:#f97316">Timone dir.</div></div>
        <div class="info-item"><div class="label">Stabilità statica</div><div class="value" style="color:#4fc3f7">dCm/dCL < 0</div></div>
      </div>

      <div class="example-box">
        <div class="ex-label">Esempio — Virata Coordinata</div>
        <p>Per eseguire una virata coordinata a 30° di banco, l'aereo deve aumentare la portanza totale per compensare la componente verticale ridotta. Il <strong>fattore di carico</strong> diventa:<br><br>
        <strong>n = 1/cos(30°) = 1/0,866 ≈ 1,15 g</strong><br><br>
        La velocità di stallo aumenta di: V<sub>s,virata</sub> = V<sub>s</sub> × √n = V<sub>s</sub> × 1,07</p>
      </div>
    `
  },

  alare: {
    tag: 'Aerodinamica',
    title: 'Geometria Alare e Profili NACA',
    accent: '#a78bfa',
    body: `
      <p>La geometria dell'ala e la forma del profilo alare determinano le caratteristiche aerodinamiche del velivolo: portanza, resistenza, efficienza e comportamento allo stallo. I profili NACA (National Advisory Committee for Aeronautics) forniscono una famiglia sistematica di profili definiti matematicamente.</p>

      <h3>Profili NACA a 4 Cifre</h3>
      <p>La nomenclatura NACA [M][P][SS] codifica tre parametri geometrici fondamentali del profilo:</p>

      <table>
        <tr><th>Cifra</th><th>Parametro</th><th>Calcolo</th></tr>
        <tr><td style="color:#a78bfa">1ª cifra (M)</td><td>Freccia massima (max camber)</td><td>m = M/100 × c</td></tr>
        <tr><td style="color:#a78bfa">2ª cifra (P)</td><td>Posizione freccia massima</td><td>p = P/10 × c</td></tr>
        <tr><td style="color:#a78bfa">3ª–4ª cifra (SS)</td><td>Spessore massimo</td><td>t = SS/100 × c</td></tr>
      </table>

      <h3>Distribuzione degli Spessori</h3>
      <p>La distribuzione dello spessore lungo la corda per un profilo NACA 4 cifre è espressa dalla formula (con x ∈ [0,1]):</p>
      <div class="formula-box">
y<sub>t</sub> = ± (t / 0,20) · [ 0,2969·√x − 0,126·x − 0,3516·x² + 0,2843·x³ − 0,1015·x⁴ ]
<br>
Il raggio di curvatura al bordo d'attacco:  r = 1,1019 · t²
      </div>

      <h3>Linea Media (Camber Line)</h3>
      <p>La linea media (y<sub>c</sub>) rappresenta la curvatura del profilo ed è calcolata a tratti:</p>
      <div class="formula-box">
Per x &lt; p:   y<sub>c</sub> = (m/p²) · (2px − x²)
Per x &gt; p:   y<sub>c</sub> = (m/(1−p)²) · [(1−2p) + 2px − x²]
      </div>

      <!-- Interactive NACA Canvas -->
      <h3>Visualizzatore Profilo NACA Interattivo</h3>
      <div class="naca-controls">
        <label>M (freccia max %):<br><input type="range" min="0" max="9" value="2" id="naca-m" oninput="drawNACA()"><br><span id="naca-m-val">2</span></label>
        <label>P (pos. freccia /10):<br><input type="range" min="0" max="9" value="4" id="naca-p" oninput="drawNACA()"><br><span id="naca-p-val">4</span></label>
        <label>SS (spessore %):<br><input type="range" min="4" max="24" value="12" id="naca-ss" oninput="drawNACA()"><br><span id="naca-ss-val">12</span></label>
        <label style="color:#a78bfa;font-size:14px">Profilo: <span id="naca-name" style="color:#fff;font-size:16px">NACA 2412</span></label>
      </div>
      <canvas id="naca-canvas" width="780" height="220"></canvas>

      <h3>Geometria Alare — Allungamento e Winglets</h3>
      <p>L'<strong>allungamento alare</strong> (Aspect Ratio, AR) è il rapporto tra il quadrato dell'apertura alare e la superficie:</p>
      <div class="formula-box">
AR = b² / S
<br>
Resistenza indotta:  C<sub>Di</sub> = C<sub>L</sub>² / (π · e · AR)
Dove e = fattore di efficienza di Oswald (tipico: 0,75–0,95)
      </div>
      <p>I <strong>winglets</strong> aumentano l'AR effettivo riducendo i vortici di estremità alare, migliorando l'efficienza aerodinamica (E/P) di circa il 3–5%.</p>

      <div class="example-box">
        <div class="ex-label">Esempio — NACA 2412 vs NACA 0012</div>
        <p><strong>NACA 2412</strong>: profilo asimmetrico, m=0,02c, p=0,4c, spessore=0,12c. Usato sul Cessna 172, offre buona portanza a bassi angoli di attacco con C<sub>L,max</sub> ≈ 1,5.<br><br>
        <strong>NACA 0012</strong>: profilo simmetrico (M=P=0), spessore=0,12c. Usato su impennaggi e ali di aerei acrobatici che richiedono uguale portanza in entrambe le direzioni.</p>
      </div>

      <table>
        <tr><th>Profilo</th><th>m</th><th>p</th><th>t/c</th><th>Applicazione tipica</th></tr>
        <tr><td>NACA 2412</td><td>0,02c</td><td>0,4c</td><td>0,12c</td><td>Aviazione generale</td></tr>
        <tr><td>NACA 6409</td><td>0,06c</td><td>0,4c</td><td>0,09c</td><td>Vellivoli ad alta portanza</td></tr>
        <tr><td>NACA 0012</td><td>0</td><td>0</td><td>0,12c</td><td>Impennaggi, aerei acrobatici</td></tr>
        <tr><td>NACA 2415</td><td>0,02c</td><td>0,4c</td><td>0,15c</td><td>Ali con maggiore rigidità</td></tr>
      </table>
    `
  },

  pitot: {
    tag: 'Strumentazione di Pilotaggio',
    title: 'Sistema Pitot-Statica',
    accent: '#22c55e',
    body: `
      <p>Il sistema Pitot-Statica è il cuore della strumentazione barometrica del velivolo. Misura due tipi di pressione dell'aria: la <strong>pressione totale</strong> (o di ristagno) tramite il tubo di Pitot, e la <strong>pressione statica</strong> tramite le prese statiche. Dalla differenza tra le due si ricavano velocità, quota e rateo di salita.</p>

      <svg viewBox="0 0 500 180" xmlns="http://www.w3.org/2000/svg" style="width:100%;margin:16px 0;background:rgba(0,0,0,0.3);border-radius:4px">
        <!-- Airflow arrows -->
        <line x1="20" y1="60" x2="80" y2="60" stroke="#22c55e" stroke-width="1.5" marker-end="url(#ag1)"/>
        <line x1="20" y1="90" x2="80" y2="90" stroke="#22c55e" stroke-width="1.5" marker-end="url(#ag1)"/>
        <line x1="20" y1="120" x2="80" y2="120" stroke="#22c55e" stroke-width="1.5" marker-end="url(#ag1)"/>
        <!-- Pitot tube -->
        <path d="M80 75 L140 75 L140 65 L155 90 L140 115 L140 105 L80 105 Z" fill="#0a3020" stroke="#22c55e" stroke-width="1.5"/>
        <circle cx="155" cy="90" r="4" fill="#22c55e" opacity="0.7"/>
        <text x="100" y="94" fill="#22c55e" font-size="10" font-family="'Barlow Condensed',sans-serif">PITOT TUBE</text>
        <!-- Lines to instruments -->
        <line x1="140" y1="72" x2="260" y2="50" stroke="#22c55e" stroke-width="1" stroke-dasharray="3,3"/>
        <line x1="140" y1="108" x2="260" y2="130" stroke="#22c55e" stroke-width="1" stroke-dasharray="3,3" opacity="0.5"/>
        <!-- Static port -->
        <rect x="140" y="140" width="15" height="15" rx="2" fill="#0a2040" stroke="#4fc3f7" stroke-width="1"/>
        <text x="162" y="151" fill="#4fc3f7" font-size="10" font-family="'Barlow Condensed',sans-serif">STATIC PORT</text>
        <line x1="148" y1="140" x2="260" y2="130" stroke="#4fc3f7" stroke-width="1" stroke-dasharray="3,3"/>
        <!-- Instruments -->
        <circle cx="290" cy="50" r="22" fill="#0d1e3a" stroke="#f97316" stroke-width="1.5"/>
        <text x="290" y="47" fill="#f97316" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">ANEMO-</text>
        <text x="290" y="57" fill="#f97316" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">METRO</text>
        <circle cx="360" cy="90" r="22" fill="#0d1e3a" stroke="#fbbf24" stroke-width="1.5"/>
        <text x="360" y="87" fill="#fbbf24" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">ALTI-</text>
        <text x="360" y="97" fill="#fbbf24" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">METRO</text>
        <circle cx="430" cy="130" r="22" fill="#0d1e3a" stroke="#a78bfa" stroke-width="1.5"/>
        <text x="430" y="127" fill="#a78bfa" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">VARIO-</text>
        <text x="430" y="137" fill="#a78bfa" font-size="9" font-family="'Barlow Condensed',sans-serif" text-anchor="middle">METRO</text>
        <!-- Connections -->
        <line x1="260" y1="50" x2="268" y2="50" stroke="#f97316" stroke-width="1"/>
        <line x1="260" y1="130" x2="338" y2="90" stroke="#fbbf24" stroke-width="1" stroke-dasharray="2,2"/>
        <line x1="260" y1="130" x2="408" y2="130" stroke="#a78bfa" stroke-width="1" stroke-dasharray="2,2"/>
        <!-- Labels -->
        <text x="245" y="40" fill="#22c55e" font-size="9" font-family="'Barlow Condensed',sans-serif">P<tspan baseline-shift="sub">tot</tspan></text>
        <text x="245" y="145" fill="#4fc3f7" font-size="9" font-family="'Barlow Condensed',sans-serif">P<tspan baseline-shift="sub">stat</tspan></text>
        <defs>
          <marker id="ag1" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 Z" fill="#22c55e"/></marker>
        </defs>
      </svg>

      <h3>Teorema di Bernoulli — Base Fisica</h3>
      <p>Il principio su cui si basa il sistema è il <strong>Teorema di Bernoulli</strong> per flusso stazionario incomprimibile:</p>
      <div class="formula-box">
P<sub>tot</sub> = P<sub>stat</sub> + P<sub>din</sub> = P<sub>stat</sub> + ½ · ρ · V²  = costante

Velocità IAS:  V = √[ 2(P<sub>tot</sub> − P<sub>stat</sub>) / ρ<sub>0</sub> ]
Dove ρ<sub>0</sub> = densità ISA al livello del mare = 1,225 kg/m³
      </div>

      <h3>Pressione Statica e Quota</h3>
      <p>La pressione statica decresce con l'altitudine secondo l'atmosfera standard ISA (International Standard Atmosphere). Per quota inferiore a 11.000 m (troposfera):</p>
      <div class="formula-box">
P(h) = P<sub>0</sub> · [1 − L·h/T<sub>0</sub>]^(g/(R·L))
Dove:
  P<sub>0</sub> = 101.325 Pa  (pressione livello del mare)
  L = 0,0065 K/m  (gradiente termico)
  T<sub>0</sub> = 288,15 K
  g = 9,80665 m/s²
  R = 287,05 J/(kg·K)
      </div>

      <h3>Variometro — Rateo di Salita</h3>
      <p>Il variometro (VSI, Vertical Speed Indicator) misura la <em>derivata temporale</em> della quota. Internamente utilizza una capsula barometrica che risponde lentamente tramite un orifizio calibrato, generando una differenza di pressione proporzionale a dh/dt.</p>
      <div class="formula-box">
RC = dh/dt  [ft/min o m/s]
<br>
Relazione con potenza eccedente:
RC = (P<sub>disp</sub> − P<sub>richiesta</sub>) / (W)  = P<sub>eccedente</sub> / W
      </div>

      <div class="example-box">
        <div class="ex-label">Esempio — Calibrazione Anemometro</div>
        <p>A FL100 (10.000 ft, ~3048 m) la pressione statica ISA è circa 69.682 Pa. Se il tubo di Pitot misura una pressione totale di 71.550 Pa, la velocità IAS è:<br><br>
        <strong>V<sub>IAS</sub> = √[2×(71.550 − 69.682)/1,225] = √[3051] ≈ 55,2 m/s ≈ 107 kt</strong><br><br>
        La velocità vera (TAS) sarà superiore per la minore densità in quota.</p>
      </div>
    `
  },

  barometrici: {
    tag: 'Strumenti a Capsula Barometrica',
    title: 'Altimetro, Anemometro, Variometro',
    accent: '#fbbf24',
    body: `
      <p>Gli strumenti a capsula barometrica traducono variazioni di pressione pneumatica in indicazioni meccaniche tramite capsule metalliche aneroidali (prive di aria interna) che si espandono o contraggono al variare della pressione esterna.</p>

      <!-- Instrument dials SVG -->
      <svg viewBox="0 0 500 160" xmlns="http://www.w3.org/2000/svg" style="width:100%;margin:16px 0;background:rgba(0,0,0,0.3);border-radius:4px">
        <!-- ALTIMETRO -->
        <circle cx="90" cy="80" r="60" fill="#06102a" stroke="#fbbf24" stroke-width="2"/>
        <circle cx="90" cy="80" r="54" fill="none" stroke="#fbbf24" stroke-width="0.5" opacity="0.3"/>
        <!-- Tick marks altimetro -->
        <g stroke="#fbbf24" stroke-width="1.5" opacity="0.8">
          <line x1="90" y1="27" x2="90" y2="34"/>
          <line x1="133" y1="37" x2="129" y2="43"/>
          <line x1="143" y1="80" x2="136" y2="80"/>
          <line x1="133" y1="123" x2="129" y2="117"/>
          <line x1="90" y1="133" x2="90" y2="126"/>
          <line x1="47" y1="123" x2="51" y2="117"/>
          <line x1="37" y1="80" x2="44" y2="80"/>
          <line x1="47" y1="37" x2="51" y2="43"/>
        </g>
        <text x="90" y="58" fill="#fbbf24" font-size="8" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">1000ft</text>
        <!-- Needle altimetro -->
        <line x1="90" y1="80" x2="113" y2="43" stroke="white" stroke-width="2" stroke-linecap="round"/>
        <circle cx="90" cy="80" r="4" fill="#fbbf24"/>
        <text x="90" y="167" fill="#fbbf24" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">ALTIMETRO</text>
        <text x="90" y="155" fill="#888" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">(Quota)</text>

        <!-- ANEMOMETRO -->
        <circle cx="250" cy="80" r="60" fill="#06102a" stroke="#f97316" stroke-width="2"/>
        <!-- Color arcs -->
        <!-- White arc (Flap) 40-85kt ~200° to 310° -->
        <path d="M204 106 A54 54 0 0 1 262 27" fill="none" stroke="white" stroke-width="6" opacity="0.9"/>
        <!-- Green arc (Normal) 65-165kt ~270° to 60° -->
        <path d="M196 80 A54 54 0 1 1 277 117" fill="none" stroke="#22c55e" stroke-width="6" opacity="0.9"/>
        <!-- Yellow arc (Caution) 165-200kt -->
        <path d="M277 117 A54 54 0 0 1 296 53" fill="none" stroke="#fbbf24" stroke-width="6" opacity="0.9"/>
        <!-- Red line (Never exceed) -->
        <line x1="296" y1="53" x2="304" y2="45" stroke="#ef4444" stroke-width="3"/>
        <text x="250" y="58" fill="#f97316" font-size="8" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">100kt</text>
        <!-- Needle -->
        <line x1="250" y1="80" x2="268" y2="35" stroke="white" stroke-width="2" stroke-linecap="round"/>
        <circle cx="250" cy="80" r="4" fill="#f97316"/>
        <text x="250" y="167" fill="#f97316" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">ANEMOMETRO</text>
        <text x="250" y="155" fill="#888" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">(Velocità IAS)</text>

        <!-- VARIOMETRO -->
        <circle cx="410" cy="80" r="60" fill="#06102a" stroke="#a78bfa" stroke-width="2"/>
        <!-- Center zero -->
        <line x1="356" y1="80" x2="364" y2="80" stroke="#a78bfa" stroke-width="2"/>
        <line x1="410" y1="26" x2="410" y2="34" stroke="#a78bfa" stroke-width="1.5"/>
        <line x1="410" y1="126" x2="410" y2="134" stroke="#a78bfa" stroke-width="1.5"/>
        <line x1="456" y1="80" x2="464" y2="80" stroke="#a78bfa" stroke-width="2"/>
        <text x="388" y="60" fill="#22c55e" font-size="7" font-family="'Barlow Condensed',sans-serif">+1000</text>
        <text x="388" y="104" fill="#ef4444" font-size="7" font-family="'Barlow Condensed',sans-serif">−1000</text>
        <text x="420" y="84" fill="#a78bfa" font-size="8" font-family="'Barlow Condensed',sans-serif">0</text>
        <!-- Needle up slightly (climbing) -->
        <line x1="410" y1="80" x2="370" y2="50" stroke="white" stroke-width="2" stroke-linecap="round"/>
        <circle cx="410" cy="80" r="4" fill="#a78bfa"/>
        <text x="410" y="167" fill="#a78bfa" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">VARIOMETRO</text>
        <text x="410" y="155" fill="#888" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">(Vel. Verticale)</text>
      </svg>

      <h3>Altimetro — Principio di Funzionamento</h3>
      <p>L'altimetro contiene capsule aneroidali sensibili alla pressione statica esterna. All'aumentare della quota, la pressione diminuisce e le capsule si espandono, muovendo il meccanismo d'orologeria che ruota le lancette indicatrici. L'altimetro è regolabile con il <strong>QNH</strong> (pressione al livello del mare della stazione meteorologica locale) per correggere la lettura all'aeroporto di destinazione.</p>
      <div class="formula-box">
Quota pressione:   h = (T<sub>0</sub>/L) × [1 − (P/P<sub>0</sub>)^(R·L/g)] = 44.330 × [1 − (P/101325)^0,1903]
Errore di quota per ΔP<sub>QNH</sub> = 1 hPa:  Δh ≈ 27 ft (≈ 8,2 m)
      </div>

      <h3>Codice Colori dell'Anemometro</h3>
      <table>
        <tr><th>Colore</th><th>Velocità</th><th>Significato</th></tr>
        <tr><td><span style="color:white">● Bianco</span></td><td>V<sub>S0</sub> → V<sub>FE</sub></td><td>Range flap estesi (operativo con flap)</td></tr>
        <tr><td><span style="color:#22c55e">● Verde</span></td><td>V<sub>S1</sub> → V<sub>NO</sub></td><td>Range operativo normale</td></tr>
        <tr><td><span style="color:#fbbf24">● Giallo</span></td><td>V<sub>NO</sub> → V<sub>NE</sub></td><td>Range di cautela (solo aria calma)</td></tr>
        <tr><td><span style="color:#ef4444">● Rosso</span></td><td>V<sub>NE</sub></td><td>Velocità limite strutturale (Never Exceed)</td></tr>
      </table>

      <div class="example-box">
        <div class="ex-label">Esempio — Cessna 172S</div>
        <p>
        V<sub>S0</sub> (stallo, flap) = 44 kt | V<sub>S1</sub> (stallo, config. pulita) = 53 kt<br>
        V<sub>FE</sub> (max con flap) = 85 kt | V<sub>NO</sub> (normale operativa) = 129 kt<br>
        V<sub>NE</sub> (mai superare) = 163 kt<br><br>
        In una virata a 45° di banco: V<sub>s,eff</sub> = 53 × √(1/cos45°) = 53 × 1,19 ≈ <strong>63 kt</strong>
        </p>
      </div>
    `
  },

  giroscopici: {
    tag: 'Strumenti Giroscopici',
    title: 'Orizzonte Artificiale, Virosbandometro, Girodirezionale',
    accent: '#e879f9',
    body: `
      <p>Gli strumenti giroscopici sfruttano le proprietà fisiche del <strong>giroscopio</strong> — un corpo in rapida rotazione — per mantenere un riferimento spaziale fisso indipendentemente dai movimenti del velivolo. I due principi fondamentali sono la <em>rigidità giroscopica</em> e la <em>precessione</em>.</p>

      <h3>Principi Fisici del Giroscopio</h3>
      <div class="formula-box">
Rigidità:    L = I · ω  (il vettore momento angolare si mantiene fisso nello spazio)
Dove:  I = momento d'inerzia  [kg·m²]
       ω = velocità angolare di rotazione  [rad/s]

Precessione: τ = dL/dt → l'asse di spin si sposta perpendicolarmente
             alla coppia applicata e al vettore L
             Ω<sub>prec</sub> = τ / (I · ω)
      </div>

      <svg viewBox="0 0 500 180" xmlns="http://www.w3.org/2000/svg" style="width:100%;margin:16px 0;background:rgba(0,0,0,0.3);border-radius:4px">
        <!-- ORIZZONTE ARTIFICIALE -->
        <rect x="20" y="20" width="140" height="140" rx="4" fill="#06102a" stroke="#e879f9" stroke-width="1.5"/>
        <rect x="20" y="20" width="140" height="140" rx="4" fill="none" stroke="#e879f9" stroke-width="1.5"/>
        <!-- Sky / Ground division -->
        <rect x="22" y="22" width="136" height="65" rx="3" fill="#0a2e5c" opacity="0.9"/>
        <rect x="22" y="87" width="136" height="71" rx="3" fill="#4a2208" opacity="0.9"/>
        <!-- Horizon line -->
        <line x1="22" y1="87" x2="158" y2="87" stroke="white" stroke-width="2.5"/>
        <!-- Pitch lines -->
        <line x1="60" y1="72" x2="100" y2="72" stroke="white" stroke-width="1" opacity="0.5"/>
        <line x1="60" y1="102" x2="100" y2="102" stroke="white" stroke-width="1" opacity="0.5"/>
        <!-- Aircraft symbol -->
        <line x1="75" y1="90" x2="90" y2="90" stroke="#fbbf24" stroke-width="2.5"/>
        <line x1="90" y1="90" x2="90" y2="83" stroke="#fbbf24" stroke-width="2.5"/>
        <line x1="90" y1="90" x2="105" y2="90" stroke="#fbbf24" stroke-width="2.5"/>
        <text x="90" y="170" fill="#e879f9" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">ORIZZONTE ARTIFICIALE</text>

        <!-- VIROSBANDOMETRO -->
        <rect x="185" y="20" width="140" height="140" rx="4" fill="#06102a" stroke="#4fc3f7" stroke-width="1.5"/>
        <!-- Turn indicator -->
        <path d="M220 90 A35 35 0 0 1 290 90" fill="none" stroke="#4fc3f7" stroke-width="1.5"/>
        <circle cx="255" cy="55" r="6" fill="none" stroke="#4fc3f7" stroke-width="1.5"/>
        <!-- Bank lines -->
        <line x1="225" y1="65" x2="225" y2="75" stroke="#4fc3f7" stroke-width="1" opacity="0.5"/>
        <line x1="255" y1="60" x2="255" y2="70" stroke="#4fc3f7" stroke-width="1.5"/>
        <line x1="285" y1="65" x2="285" y2="75" stroke="#4fc3f7" stroke-width="1" opacity="0.5"/>
        <!-- Slip indicator -->
        <rect x="225" y="100" width="60" height="14" rx="7" fill="none" stroke="white" stroke-width="1.5"/>
        <circle cx="255" cy="107" r="4" fill="white"/>
        <!-- Needle -->
        <line x1="255" y1="90" x2="245" y2="62" stroke="white" stroke-width="2"/>
        <text x="255" y="170" fill="#4fc3f7" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">VIROSBANDOMETRO</text>

        <!-- GIRODIREZIONALE -->
        <rect x="350" y="20" width="140" height="140" rx="4" fill="#06102a" stroke="#22c55e" stroke-width="1.5"/>
        <circle cx="420" cy="90" r="52" fill="none" stroke="#22c55e" stroke-width="1" opacity="0.5"/>
        <!-- Compass points -->
        <text x="420" y="44" fill="white" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">N</text>
        <text x="466" y="93" fill="white" font-size="10" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">E</text>
        <text x="420" y="146" fill="white" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">S</text>
        <text x="374" y="93" fill="white" font-size="11" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">W</text>
        <!-- Course -->
        <line x1="420" y1="90" x2="437" y2="46" stroke="#fbbf24" stroke-width="2"/>
        <text x="420" y="94" fill="#22c55e" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">360°</text>
        <text x="420" y="170" fill="#22c55e" font-size="9" text-anchor="middle" font-family="'Barlow Condensed',sans-serif">GIRODIREZIONALE</text>
      </svg>

      <h3>Orizzonte Artificiale (AI)</h3>
      <p>L'orizzonte artificiale indica l'assetto del velivolo attorno agli assi di rollio e beccheggio. Il giroscopio interno mantiene la sua posizione verticale per rigidità giroscopica. Funziona su <strong>2 gradi di libertà</strong>: il gimbal esterno mantiene il rollio e quello interno il beccheggio.</p>
      <div class="formula-box">
Principio:  L = I · ω → mantenuto verticale (allineato con la gravità)
Errore di precessione dovuto alla rotazione terrestre:  ε ≈ 15°/h × sin(lat)
      </div>

      <h3>Virosbandometro (T&S)</h3>
      <p>Il virosbandometro (Turn & Slip Indicator) combina due indicatori: l'<em>indicatore di virata</em> (giroscopio a 1 grado di libertà che misura la velocità di imbardata) e il <em>bandometro</em> a bolla (o pallina) che indica la coordinazione della virata tramite forze di inerzia.</p>
      <div class="formula-box">
Velocità di virata standard:  ψ̇ = 3°/s (virata 1)
Raggio di virata:  R = V / (g · tan φ)
Dove φ = angolo di banco, g = 9,81 m/s²
      </div>

      <h3>Girodirezionale (DI)</h3>
      <p>Il girodirezionale fornisce un'indicazione stabile della prua, non soggetta alle oscillazioni del compasso magnetico durante virare e accelerazioni. Funziona su <strong>3 gradi di libertà</strong> e deve essere riallineato periodicamente al compasso magnetico (ogni 10–15 minuti) per correggere la precessione.</p>

      <div class="info-grid">
        <div class="info-item"><div class="label">AI — Gradi libertà</div><div class="value" style="color:#e879f9">2 DoF</div></div>
        <div class="info-item"><div class="label">Virosbandometro</div><div class="value" style="color:#4fc3f7">1 DoF</div></div>
        <div class="info-item"><div class="label">Girodirezionale</div><div class="value" style="color:#22c55e">3 DoF</div></div>
        <div class="info-item"><div class="label">Virata std</div><div class="value" style="color:#fbbf24">3°/sec</div></div>
      </div>

      <div class="example-box">
        <div class="ex-label">Esempio — Virata Coordinata a 360°</div>
        <p>A 3°/s (virata 1), un giro completo di 360° richiede 120 secondi = 2 minuti. Il virosbandometro mostrerà la pallina centrata se la virata è coordinata. Se la pallina è fuori centro (verso l'esterno della virata), l'aereo sta scivolando (<em>skidding</em>); verso l'interno, strisciando (<em>slipping</em>).<br><br>
        A V = 100 kt = 51,4 m/s con virata standard: <strong>φ = arctan(V·ψ̇/g) = arctan(51,4×0,0524/9,81) ≈ 15,5°</strong></p>
      </div>
    `
  }
};

function openModal(id) {
  const m = modals[id];
  if (!m) return;
  const overlay = document.getElementById('modal-overlay');
  document.getElementById('modal-tag').textContent = m.tag;
  document.getElementById('modal-title').textContent = m.title;
  document.getElementById('modal-body').innerHTML = m.body;
  document.getElementById('modal-content').style.setProperty('--modal-accent', m.accent);
  document.querySelector('.modal-header').style.borderColor = m.accent + '30';

  overlay.classList.add('open');
  document.body.style.overflow = 'hidden';

  // Init NACA canvas if present
  if (id === 'alare') {
    setTimeout(() => {
      drawNACA();
      const canvas = document.getElementById('naca-canvas');
      if (canvas && !canvas._roAttached) {
        canvas._roAttached = true;
        new ResizeObserver(() => drawNACA()).observe(canvas);
      }
    }, 120);
  }
  // Init 3D axes widget
  if (id === 'assi') {
    setTimeout(() => initAxesWidget(), 120);
  }
}

function closeModal() {
  document.getElementById('modal-overlay').classList.remove('open');
  document.body.style.overflow = '';
}

function handleOverlayClick(e) {
  if (e.target === document.getElementById('modal-overlay')) closeModal();
}

document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

// ─── NACA PROFILE DRAWING ─────────────────────────────
// Helper: draw arrow between two points
function drawArrow(ctx, x1, y1, x2, y2, color, headSize) {
  const hs = headSize || 6;
  const angle = Math.atan2(y2 - y1, x2 - x1);
  ctx.strokeStyle = color;
  ctx.fillStyle = color;
  ctx.lineWidth = 1;
  ctx.beginPath(); ctx.moveTo(x1, y1); ctx.lineTo(x2, y2); ctx.stroke();
  ctx.beginPath();
  ctx.moveTo(x2, y2);
  ctx.lineTo(x2 - hs * Math.cos(angle - 0.4), y2 - hs * Math.sin(angle - 0.4));
  ctx.lineTo(x2 - hs * Math.cos(angle + 0.4), y2 - hs * Math.sin(angle + 0.4));
  ctx.closePath(); ctx.fill();
}

// Helper: double-headed dimension arrow
function drawDimArrow(ctx, x1, y1, x2, y2, color, label, labelSide) {
  drawArrow(ctx, x2, y2, x1, y1, color, 5);
  drawArrow(ctx, x1, y1, x2, y2, color, 5);
  const mx = (x1 + x2) / 2, my = (y1 + y2) / 2;
  ctx.fillStyle = color;
  ctx.font = 'bold 11px "Barlow Condensed", sans-serif';
  ctx.textAlign = 'center';
  const off = labelSide || -10;
  const ang = Math.atan2(y2 - y1, x2 - x1);
  ctx.save();
  ctx.translate(mx, my);
  ctx.rotate(ang);
  ctx.fillText(label, 0, off);
  ctx.restore();
  ctx.textAlign = 'left';
}

function nacaThickness(xc, t) {
  return (t / 0.20) * (
    0.2969 * Math.sqrt(xc)
    - 0.126  * xc
    - 0.3516 * xc ** 2
    + 0.2843 * xc ** 3
    - 0.1015 * xc ** 4
  );
}

function nacaCamber(xc, m, p) {
  if (p <= 0 || m <= 0) return { yc: 0, dyc: 0 };
  if (xc <= p) {
    return {
      yc:  (m / (p * p)) * (2 * p * xc - xc * xc),
      dyc: (2 * m / (p * p)) * (p - xc)
    };
  }
  return {
    yc:  (m / ((1 - p) ** 2)) * ((1 - 2 * p) + 2 * p * xc - xc * xc),
    dyc: (2 * m / ((1 - p) ** 2)) * (p - xc)
  };
}

function drawNACA() {
  const canvas = document.getElementById('naca-canvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');

  const Mval = parseInt(document.getElementById('naca-m').value);
  const Pval = parseInt(document.getElementById('naca-p').value);
  const SSval = parseInt(document.getElementById('naca-ss').value);

  document.getElementById('naca-m-val').textContent = Mval;
  document.getElementById('naca-p-val').textContent = Pval;
  document.getElementById('naca-ss-val').textContent = SSval;

  const mStr  = Mval.toString();
  const pStr  = Pval.toString();
  const ssStr = SSval.toString().padStart(2, '0');
  document.getElementById('naca-name').textContent = `NACA ${mStr}${pStr}${ssStr}`;

  const m = Mval / 100;
  const p = Pval / 10;
  const t = SSval / 100;

  // Canvas layout — more vertical space for annotations below
  const DPR = window.devicePixelRatio || 1;
  const cssW = canvas.clientWidth || 780;
  const cssH = 300;
  canvas.width  = cssW * DPR;
  canvas.height = cssH * DPR;
  canvas.style.height = cssH + 'px';
  ctx.scale(DPR, DPR);
  const W = cssW, H = cssH;

  // Profile drawing area: leave margins for annotations
  const marginL = 52, marginR = 40, marginTop = 60, marginBot = 70;
  const cW = W - marginL - marginR;   // chord width in px
  const scale = cW;                    // 1 chord unit = cW px
  const ox = marginL;                  // x origin = leading edge
  const oy = marginTop + (H - marginTop - marginBot) * 0.52; // baseline (chord line)

  // ── Background ────────────────────────────────────────
  ctx.fillStyle = '#05090f';
  ctx.fillRect(0, 0, W, H);

  // Subtle grid
  ctx.strokeStyle = 'rgba(79,195,247,0.06)';
  ctx.lineWidth = 0.5;
  for (let gx = 0; gx <= 10; gx++) {
    const px = ox + gx / 10 * cW;
    ctx.beginPath(); ctx.moveTo(px, marginTop - 20); ctx.lineTo(px, H - marginBot + 20); ctx.stroke();
  }

  // ── Compute profile points ────────────────────────────
  const N = 300;
  const upperX = [], upperY = [], lowerX = [], lowerY = [];
  const camberX = [], camberY = [];
  // Find max thickness location and value
  let maxYt = 0, maxYtX = 0;
  // Find max camber location and value
  let maxYc = 0, maxYcX = 0;

  for (let i = 0; i <= N; i++) {
    // Cosine spacing for better leading edge resolution
    const xc = 0.5 * (1 - Math.cos(Math.PI * i / N));
    const yt = nacaThickness(xc, t);
    const { yc, dyc } = nacaCamber(xc, m, p);
    const theta = Math.atan(dyc);

    const uxPx = ox + (xc - yt * Math.sin(theta)) * scale;
    const uyPx = oy - (yc + yt * Math.cos(theta)) * scale;
    const lxPx = ox + (xc + yt * Math.sin(theta)) * scale;
    const lyPx = oy - (yc - yt * Math.cos(theta)) * scale;

    upperX.push(uxPx); upperY.push(uyPx);
    lowerX.push(lxPx); lowerY.push(lyPx);
    camberX.push(ox + xc * scale);
    camberY.push(oy - yc * scale);

    if (yt > maxYt) { maxYt = yt; maxYtX = xc; }
    if (yc > maxYc) { maxYc = yc; maxYcX = xc; }
  }

  // ── Chord line (dashed) ───────────────────────────────
  ctx.strokeStyle = 'rgba(255,255,255,0.18)';
  ctx.lineWidth = 1;
  ctx.setLineDash([5, 5]);
  ctx.beginPath(); ctx.moveTo(ox, oy); ctx.lineTo(ox + cW, oy); ctx.stroke();
  ctx.setLineDash([]);

  // ── Profile fill ─────────────────────────────────────
  ctx.beginPath();
  ctx.moveTo(upperX[0], upperY[0]);
  for (let i = 1; i <= N; i++) ctx.lineTo(upperX[i], upperY[i]);
  for (let i = N; i >= 0; i--) ctx.lineTo(lowerX[i], lowerY[i]);
  ctx.closePath();

  const grad = ctx.createLinearGradient(ox, 0, ox + cW, 0);
  grad.addColorStop(0,   'rgba(79,195,247,0.22)');
  grad.addColorStop(0.3, 'rgba(79,195,247,0.14)');
  grad.addColorStop(1,   'rgba(79,195,247,0.04)');
  ctx.fillStyle = grad;
  ctx.fill();

  // ── Upper surface ─────────────────────────────────────
  ctx.beginPath();
  ctx.moveTo(upperX[0], upperY[0]);
  for (let i = 1; i <= N; i++) ctx.lineTo(upperX[i], upperY[i]);
  ctx.strokeStyle = '#4fc3f7';
  ctx.lineWidth = 2.2;
  ctx.setLineDash([]);
  ctx.stroke();

  // ── Lower surface ─────────────────────────────────────
  ctx.beginPath();
  ctx.moveTo(lowerX[0], lowerY[0]);
  for (let i = 1; i <= N; i++) ctx.lineTo(lowerX[i], lowerY[i]);
  ctx.strokeStyle = '#7dd3f0';
  ctx.lineWidth = 1.6;
  ctx.stroke();

  // ── Camber line (dashed orange) ───────────────────────
  if (m > 0) {
    ctx.beginPath();
    ctx.moveTo(camberX[0], camberY[0]);
    for (let i = 1; i <= N; i++) ctx.lineTo(camberX[i], camberY[i]);
    ctx.strokeStyle = '#f97316';
    ctx.lineWidth = 1.4;
    ctx.setLineDash([6, 4]);
    ctx.stroke();
    ctx.setLineDash([]);
  }

  // ── ANNOTATIONS ──────────────────────────────────────

  // 1) Corda (c) — horizontal dimension below profile
  const dimY = oy + t * scale + 28;
  const dimLineY = dimY + 14;
  // Vertical tick marks
  ctx.strokeStyle = 'rgba(255,255,255,0.3)';
  ctx.lineWidth = 1;
  ctx.beginPath(); ctx.moveTo(ox, oy + 6); ctx.lineTo(ox, dimLineY + 4); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(ox + cW, oy + 6); ctx.lineTo(ox + cW, dimLineY + 4); ctx.stroke();
  drawDimArrow(ctx, ox, dimLineY, ox + cW, dimLineY, 'rgba(255,255,255,0.55)', 'corda  (c)', 9);

  // 2) Bordo d'attacco label
  ctx.fillStyle = '#4fc3f7';
  ctx.font = 'bold 11px "Barlow Condensed", sans-serif';
  ctx.textAlign = 'center';
  ctx.fillText('bordo d\'attacco', ox, marginTop - 10);
  ctx.strokeStyle = 'rgba(79,195,247,0.35)';
  ctx.lineWidth = 1;
  ctx.beginPath(); ctx.moveTo(ox, marginTop - 6); ctx.lineTo(ox, oy - 4); ctx.stroke();

  // 3) Bordo d'uscita label
  ctx.fillText('bordo d\'uscita', ox + cW, marginTop - 10);
  ctx.beginPath(); ctx.moveTo(ox + cW, marginTop - 6); ctx.lineTo(ox + cW, oy - 2); ctx.stroke();
  ctx.textAlign = 'left';

  // 4) Spessore massimo (t) — vertical arrow at max-thickness x
  const tXpx = ox + maxYtX * scale;
  const tUpY  = oy - maxYt * scale;  // upper surface at max-t
  const tLoY  = oy + maxYt * scale;  // lower surface at max-t (symmetric around chord)
  // Vertical dashed drop line
  ctx.strokeStyle = 'rgba(251,191,36,0.3)';
  ctx.lineWidth = 0.8;
  ctx.setLineDash([3, 4]);
  ctx.beginPath(); ctx.moveTo(tXpx, marginTop - 20); ctx.lineTo(tXpx, oy); ctx.stroke();
  ctx.setLineDash([]);
  // Double arrow
  drawDimArrow(ctx, tXpx - 22, tUpY, tXpx - 22, tLoY, '#fbbf24',
    `t = ${SSval}%`, -7);
  // Horizontal tick lines at arrow ends
  ctx.strokeStyle = 'rgba(251,191,36,0.5)';
  ctx.lineWidth = 0.8;
  ctx.beginPath(); ctx.moveTo(tXpx - 26, tUpY); ctx.lineTo(tXpx - 2, tUpY); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(tXpx - 26, tLoY); ctx.lineTo(tXpx - 2, tLoY); ctx.stroke();
  // x/c label at bottom
  ctx.fillStyle = '#fbbf24';
  ctx.font = '10px "Barlow Condensed", sans-serif';
  ctx.textAlign = 'center';
  ctx.fillText(`x/c = ${maxYtX.toFixed(2)}`, tXpx, H - marginBot + 16);
  ctx.textAlign = 'left';

  // 5) Freccia massima (m) — if camber exists
  if (m > 0 && p > 0) {
    const mXpx = ox + maxYcX * scale;
    const mYpx = oy - maxYc * scale;   // top of camber
    const mYbase = oy;                  // chord line

    // Vertical dashed drop line from camber peak to chord
    ctx.strokeStyle = 'rgba(249,115,22,0.35)';
    ctx.lineWidth = 0.8;
    ctx.setLineDash([3, 4]);
    ctx.beginPath(); ctx.moveTo(mXpx, mYpx - 4); ctx.lineTo(mXpx, mYbase); ctx.stroke();
    ctx.setLineDash([]);

    // Double arrow: camber height
    const arrowX = mXpx + 18;
    drawDimArrow(ctx, arrowX, mYbase, arrowX, mYpx, '#f97316',
      `m = ${Mval}%`, 9);
    ctx.strokeStyle = 'rgba(249,115,22,0.45)';
    ctx.lineWidth = 0.8;
    ctx.beginPath(); ctx.moveTo(mXpx + 2, mYpx);   ctx.lineTo(arrowX + 4, mYpx);   ctx.stroke();
    ctx.beginPath(); ctx.moveTo(mXpx + 2, mYbase); ctx.lineTo(arrowX + 4, mYbase); ctx.stroke();

    // Horizontal arrow: position of max camber from LE
    const hArrowY = mYpx - 16;
    drawDimArrow(ctx, ox, hArrowY, mXpx, hArrowY, 'rgba(249,115,22,0.7)',
      `p·c = ${Pval}0%`, -7);
    ctx.strokeStyle = 'rgba(249,115,22,0.3)';
    ctx.lineWidth = 0.8;
    ctx.beginPath(); ctx.moveTo(ox,   hArrowY - 4); ctx.lineTo(ox,   mYpx + 2); ctx.stroke();
    ctx.beginPath(); ctx.moveTo(mXpx, hArrowY - 4); ctx.lineTo(mXpx, mYpx + 2); ctx.stroke();

    // Camber label on curve
    ctx.fillStyle = '#f97316';
    ctx.font = 'bold 11px "Barlow Condensed", sans-serif';
    ctx.fillText('linea media', mXpx + 24, mYpx + 4);
  }

  // 6) Leading edge radius arc
  const r = 1.1019 * t * t;
  const rPx = r * scale;
  ctx.strokeStyle = 'rgba(167,139,250,0.7)';
  ctx.lineWidth = 1.2;
  ctx.beginPath();
  ctx.arc(ox + rPx, oy, rPx, 0, Math.PI * 2);
  ctx.stroke();
  ctx.fillStyle = '#a78bfa';
  ctx.font = '10px "Barlow Condensed", sans-serif';
  ctx.fillText(`r = ${(r * 100).toFixed(2)}%·c`, ox + 2, oy - rPx - 5);

  // 7) Surface labels
  ctx.fillStyle = '#4fc3f7';
  ctx.font = 'bold 11px "Barlow Condensed", sans-serif';
  ctx.fillText('superficie superiore', ox + cW * 0.22, upperY[Math.round(N * 0.25)] - 8);
  ctx.fillStyle = 'rgba(125,211,240,0.8)';
  ctx.fillText('superficie inferiore', ox + cW * 0.22, lowerY[Math.round(N * 0.25)] + 14);

  // 8) x/c axis ticks at 0.2 intervals
  ctx.strokeStyle = 'rgba(255,255,255,0.12)';
  ctx.lineWidth = 0.8;
  ctx.fillStyle = 'rgba(255,255,255,0.3)';
  ctx.font = '9px "Barlow Condensed", sans-serif';
  ctx.textAlign = 'center';
  [0.2, 0.4, 0.6, 0.8, 1.0].forEach(xv => {
    const px = ox + xv * cW;
    ctx.beginPath(); ctx.moveTo(px, oy - 3); ctx.lineTo(px, oy + 3); ctx.stroke();
    ctx.fillText(xv.toFixed(1), px, oy + 12);
  });
  ctx.fillText('0', ox, oy + 12);
  ctx.fillStyle = 'rgba(255,255,255,0.25)';
  ctx.font = '9px "Barlow Condensed", sans-serif';
  ctx.fillText('x/c', ox + cW + 8, oy + 12);
  ctx.textAlign = 'left';

  // 9) Profile name watermark
  ctx.font = 'bold 22px "Barlow Condensed", sans-serif';
  ctx.fillStyle = 'rgba(79,195,247,0.07)';
  ctx.textAlign = 'right';
  ctx.fillText(`NACA ${mStr}${pStr}${ssStr}`, ox + cW, H - marginBot + 36);
  ctx.textAlign = 'left';
}

// ═══════════════════════════════════════════════════════
// 3D AXES WIDGET — software renderer (no WebGL needed)
// ═══════════════════════════════════════════════════════

let _axesRAF = null;
let _axesState = null;

function initAxesWidget() {
  const canvas = document.getElementById('axes-canvas');
  if (!canvas) return;
  if (_axesRAF) { cancelAnimationFrame(_axesRAF); _axesRAF = null; }

  const DPR = window.devicePixelRatio || 1;
  const cssW = canvas.clientWidth  || 700;
  const cssH = 360;
  canvas.width  = cssW * DPR;
  canvas.height = cssH * DPR;
  canvas.style.height = cssH + 'px';
  const ctx = canvas.getContext('2d');
  ctx.scale(DPR, DPR);
  const W = cssW, H = cssH;

  const state = {
    rx: 0.28,   // view rotation x (pitch of camera)
    ry: 0.52,   // view rotation y (yaw of camera)
    // animation state
    animMode: null,  // 'roll'|'pitch'|'yaw'|null
    animAngle: 0,
    animTarget: 0,
    animSpeed: 0,
    rollAng: 0,
    pitchAng: 0,
    yawAng: 0,
    // drag
    dragging: false,
    lastX: 0, lastY: 0,
    // hover
    trailPoints: [],
  };
  _axesState = state;

  // ── Input handling ───────────────────────────────────
  canvas.addEventListener('mousedown', e => {
    state.dragging = true; state.lastX = e.clientX; state.lastY = e.clientY;
    canvas.style.cursor = 'grabbing';
  });
  window.addEventListener('mouseup', () => { state.dragging = false; canvas.style.cursor = 'grab'; });
  window.addEventListener('mousemove', e => {
    if (!state.dragging) return;
    const dx = e.clientX - state.lastX, dy = e.clientY - state.lastY;
    state.ry += dx * 0.008; state.rx += dy * 0.008;
    state.rx = Math.max(-1.2, Math.min(1.2, state.rx));
    state.lastX = e.clientX; state.lastY = e.clientY;
  });
  canvas.addEventListener('touchstart', e => {
    const t = e.touches[0]; state.dragging = true;
    state.lastX = t.clientX; state.lastY = t.clientY; e.preventDefault();
  }, { passive: false });
  canvas.addEventListener('touchmove', e => {
    if (!state.dragging) return;
    const t = e.touches[0];
    const dx = t.clientX - state.lastX, dy = t.clientY - state.lastY;
    state.ry += dx * 0.008; state.rx += dy * 0.008;
    state.rx = Math.max(-1.2, Math.min(1.2, state.rx));
    state.lastX = t.clientX; state.lastY = t.clientY; e.preventDefault();
  }, { passive: false });
  canvas.addEventListener('touchend', () => { state.dragging = false; });

  // ── 3D math ──────────────────────────────────────────
  function rotX(v, a) {
    const c = Math.cos(a), s = Math.sin(a);
    return [v[0], v[1]*c - v[2]*s, v[1]*s + v[2]*c];
  }
  function rotY(v, a) {
    const c = Math.cos(a), s = Math.sin(a);
    return [v[0]*c + v[2]*s, v[1], -v[0]*s + v[2]*c];
  }
  function rotZ(v, a) {
    const c = Math.cos(a), s = Math.sin(a);
    return [v[0]*c - v[1]*s, v[0]*s + v[1]*c, v[2]];
  }
  function project(v) {
    // simple perspective projection
    const fov = 500;
    const z = v[2] + 5;
    return [W/2 + v[0] * fov / z, H/2 - v[1] * fov / z, z];
  }
  function applyView(v) {
    let u = rotX(v, state.rx);
    return rotY(u, state.ry);
  }
  function applyPlaneRot(v) {
    let u = rotZ(v, state.rollAng);
    u = rotX(u, state.pitchAng);
    u = rotY(u, state.yawAng);
    return u;
  }
  function tf(v) { return project(applyView(applyPlaneRot(v))); }

  // ── Airplane geometry ────────────────────────────────
  // All coords in plane-local space, unit ≈ 1 = half-fuselage length
  // x = right, y = up, z = forward (nose direction)

  function getPlaneGeometry() {
    const geom = [];

    // ── FUSELAGE (tube segments) ──────────────────────
    const fsLen = 2.2, fsR = 0.13;
    const fsSects = 16;
    for (let i = 0; i < fsSects; i++) {
      const z0 = -1.1 + fsLen * i / fsSects;
      const z1 = -1.1 + fsLen * (i+1) / fsSects;
      const r0 = fsR * (1 - 0.25*(z0/1.1)**4);
      const r1 = fsR * (1 - 0.25*(z1/1.1)**4);
      // Taper nose
      const taper0 = z0 > 0.8 ? Math.pow((1.1 - z0)/0.3, 0.6) : 1;
      const taper1 = z1 > 0.8 ? Math.pow((1.1 - z1)/0.3, 0.6) : 1;
      const segs = 10;
      for (let j = 0; j < segs; j++) {
        const a0 = (j/segs)*Math.PI*2, a1 = ((j+1)/segs)*Math.PI*2;
        geom.push({
          type: 'quad',
          pts: [
            [Math.cos(a0)*r0*taper0, Math.sin(a0)*r0*taper0, z0],
            [Math.cos(a1)*r0*taper0, Math.sin(a1)*r0*taper0, z0],
            [Math.cos(a1)*r1*taper1, Math.sin(a1)*r1*taper1, z1],
            [Math.cos(a0)*r1*taper1, Math.sin(a0)*r1*taper1, z1],
          ],
          color: [20, 50, 100], stroke: [79, 195, 247], alpha: 0.85
        });
      }
    }

    // ── WINGS ─────────────────────────────────────────
    // Right wing
    const wingRoot = 0.14, wingTip = 0.05;
    const wingSpan = 1.5, wingSweep = 0.25, wingThk = 0.03;
    const wingZ = -0.1; // position along fuselage
    const wingPts = (side) => {
      const s = side; // +1 right, -1 left
      return [
        // root LE, root TE, tip TE, tip LE
        [s * fsR,        0, wingZ + wingRoot],        // root LE
        [s * fsR,        0, wingZ - wingRoot],        // root TE
        [s * wingSpan,   0, wingZ - wingRoot + wingSweep - wingTip], // tip TE
        [s * wingSpan,   0, wingZ + wingRoot - wingSweep + wingTip], // tip LE
      ];
    };
    for (const side of [1, -1]) {
      const pts = wingPts(side);
      // Top surface
      geom.push({ type: 'quad', pts: pts.map(p => [p[0], p[1]+wingThk, p[2]]),
        color: [15, 45, 110], stroke: [79, 195, 247], alpha: 0.9 });
      // Bottom surface
      geom.push({ type: 'quad', pts: [...pts].reverse().map(p => [p[0], p[1]-wingThk*0.3, p[2]]),
        color: [10, 35, 85], stroke: [79, 195, 247], alpha: 0.75 });
      // Winglet
      const tip = pts[3];
      const tipTE = pts[2];
      geom.push({ type: 'quad', pts: [
        [tip[0],    tip[1]-wingThk*0.3, tip[2]],
        [tipTE[0],  tipTE[1]-wingThk*0.3, tipTE[2]],
        [tipTE[0],  tipTE[1]+wingThk+0.12*side, tipTE[2]+0.05],
        [tip[0],    tip[1]+wingThk+0.12*side,   tip[2]+0.05],
      ], color: [20, 55, 120], stroke: [79, 195, 247], alpha: 0.85 });
    }

    // ── ALETTONI (ailerons) — highlighted ──────────────
    for (const side of [1, -1]) {
      const ay = wingThk + 0.001;
      const aSpanIn = wingSpan * 0.55, aSpanOut = wingSpan * 0.9;
      const aRootZ0 = wingZ - wingRoot + wingSweep*0.55 - wingTip*0.55;
      const aRootZ1 = wingZ - wingRoot + wingSweep*0.55 - wingTip*0.55 - 0.12;
      const aTipZ0  = wingZ - wingRoot + wingSweep*0.9  - wingTip*0.9;
      const aTipZ1  = wingZ - wingRoot + wingSweep*0.9  - wingTip*0.9 - 0.10;
      geom.push({ type: 'quad', pts: [
        [side*aSpanIn,  ay,  aRootZ0],
        [side*aSpanIn,  ay,  aRootZ1],
        [side*aSpanOut, ay,  aTipZ1],
        [side*aSpanOut, ay,  aTipZ0],
      ], color: [10, 80, 50], stroke: [34, 197, 94], alpha: 0.95,
         label: side > 0 ? 'ALETTONE' : null, labelColor: '#22c55e' });
    }

    // ── HORIZONTAL TAIL ──────────────────────────────
    const htSpan = 0.55, htZ = -0.95, htRoot = 0.07, htTip = 0.03;
    for (const side of [1, -1]) {
      geom.push({ type: 'quad', pts: [
        [side*0.14,    0.01, htZ + htRoot],
        [side*0.14,    0.01, htZ - htRoot],
        [side*htSpan,  0.01, htZ - htRoot + 0.08 - htTip],
        [side*htSpan,  0.01, htZ + htRoot - 0.08 + htTip],
      ], color: [18, 45, 100], stroke: [79, 195, 247], alpha: 0.9 });
    }

    // ── ELEVATORS ────────────────────────────────────
    for (const side of [1, -1]) {
      const eRoot = 0.03, eTip = 0.02;
      geom.push({ type: 'quad', pts: [
        [side*0.18,   0.012, -0.95 - htRoot + 0.01],
        [side*0.18,   0.012, -0.95 - htRoot - eRoot],
        [side*htSpan, 0.012, -0.95 - htRoot + 0.08 - htTip - 0.08 - eTip],
        [side*htSpan, 0.012, -0.95 - htRoot + 0.08 - htTip - 0.08 - eTip + eTip+eRoot],
      ], color: [10, 70, 90], stroke: [167, 139, 250], alpha: 0.95,
         label: side > 0 ? 'EQUILIBRATORE' : null, labelColor: '#a78bfa' });
    }

    // ── VERTICAL TAIL ────────────────────────────────
    const vtH = 0.45, vtBase = 0.28, vtSweep = 0.18;
    geom.push({ type: 'quad', pts: [
      [0, 0.14,    -0.82 + vtBase],
      [0, 0.14,    -0.82 - vtBase*0.1],
      [0, 0.14+vtH, -0.82 - vtBase*0.1 + vtSweep],
      [0, 0.14+vtH, -0.82 + vtBase - vtSweep],
    ], color: [18, 45, 100], stroke: [79, 195, 247], alpha: 0.9 });

    // ── RUDDER ───────────────────────────────────────
    const rvOff = 0.01;
    geom.push({ type: 'quad', pts: [
      [rvOff, 0.14,      -0.82 - vtBase*0.1 + 0.02],
      [rvOff, 0.14,      -0.82 - vtBase*0.1 - 0.08],
      [rvOff, 0.14+vtH,  -0.82 - vtBase*0.1 + vtSweep - 0.06],
      [rvOff, 0.14+vtH,  -0.82 - vtBase*0.1 + vtSweep + 0.06],
    ], color: [60, 20, 20], stroke: [249, 115, 22], alpha: 0.95,
       label: 'TIMONE', labelColor: '#f97316' });

    // ── ENGINES ──────────────────────────────────────
    for (const side of [1, -1]) {
      const ex = side * 0.55, ey = -0.09, ez = 0.0;
      const er = 0.065, el = 0.3;
      const eSegs = 10;
      for (let j = 0; j < eSegs; j++) {
        const a0 = (j/eSegs)*Math.PI*2, a1 = ((j+1)/eSegs)*Math.PI*2;
        geom.push({ type: 'quad', pts: [
          [ex + Math.cos(a0)*er, ey + Math.sin(a0)*er, ez + el/2],
          [ex + Math.cos(a1)*er, ey + Math.sin(a1)*er, ez + el/2],
          [ex + Math.cos(a1)*er, ey + Math.sin(a1)*er, ez - el/2],
          [ex + Math.cos(a0)*er, ey + Math.sin(a0)*er, ez - el/2],
        ], color: [12, 30, 70], stroke: [249, 115, 22], alpha: 0.9 });
      }
      // Engine inlet
      geom.push({ type: 'circle3d', center: [ex, ey, ez + el/2], r: er,
        normal: [0,0,1], color: [249, 115, 22], alpha: 0.7 });
    }

    return geom;
  }

  // ── Draw axes ────────────────────────────────────────
  function drawAxis(ctx, dir3, color, label, len) {
    const L = len || 1.8;
    const start = tf([0,0,0]);
    const end   = tf([dir3[0]*L, dir3[1]*L, dir3[2]*L]);
    // Line
    ctx.strokeStyle = color;
    ctx.lineWidth = 2;
    ctx.globalAlpha = 0.85;
    ctx.beginPath(); ctx.moveTo(start[0], start[1]); ctx.lineTo(end[0], end[1]); ctx.stroke();
    // Arrow head
    const ang = Math.atan2(end[1]-start[1], end[0]-start[0]);
    const hs = 9;
    ctx.fillStyle = color;
    ctx.globalAlpha = 1;
    ctx.beginPath();
    ctx.moveTo(end[0], end[1]);
    ctx.lineTo(end[0] - hs*Math.cos(ang-0.35), end[1] - hs*Math.sin(ang-0.35));
    ctx.lineTo(end[0] - hs*Math.cos(ang+0.35), end[1] - hs*Math.sin(ang+0.35));
    ctx.closePath(); ctx.fill();
    // Label
    ctx.fillStyle = color;
    ctx.font = 'bold 13px "Barlow Condensed", sans-serif';
    ctx.textAlign = 'center';
    ctx.fillText(label, end[0] + Math.cos(ang)*18, end[1] + Math.sin(ang)*18 + 4);
    ctx.textAlign = 'left';
    ctx.globalAlpha = 1;
  }

  function drawRotArc(ctx, axis, color, label, angle) {
    // Draw a rotation arc around the given world axis
    const N = 48;
    const r = 0.28;
    const pts = [];
    let perp1, perp2;
    if (axis === 'x') { perp1 = [0,1,0]; perp2 = [0,0,1]; }
    else if (axis === 'y') { perp1 = [1,0,0]; perp2 = [0,0,1]; }
    else { perp1 = [1,0,0]; perp2 = [0,1,0]; }

    const start = angle < 0 ? angle : 0;
    const end   = angle > 0 ? angle : 0;
    const sweep = Math.abs(angle);
    for (let i = 0; i <= N; i++) {
      const a = start + (end - start) * i / N;
      pts.push(tf([
        perp1[0]*r*Math.cos(a) + perp2[0]*r*Math.sin(a),
        perp1[1]*r*Math.cos(a) + perp2[1]*r*Math.sin(a),
        perp1[2]*r*Math.cos(a) + perp2[2]*r*Math.sin(a),
      ]));
    }
    if (pts.length < 2) return;
    ctx.strokeStyle = color;
    ctx.lineWidth = 2.5;
    ctx.globalAlpha = 0.9;
    ctx.setLineDash([]);
    ctx.beginPath();
    ctx.moveTo(pts[0][0], pts[0][1]);
    for (let i = 1; i < pts.length; i++) ctx.lineTo(pts[i][0], pts[i][1]);
    ctx.stroke();
    // Arrowhead at end
    const last = pts[pts.length-1], prev = pts[pts.length-3];
    if (last && prev) {
      const ang = Math.atan2(last[1]-prev[1], last[0]-prev[0]);
      const hs = 8;
      ctx.fillStyle = color;
      ctx.globalAlpha = 1;
      ctx.beginPath();
      ctx.moveTo(last[0], last[1]);
      ctx.lineTo(last[0]-hs*Math.cos(ang-0.4), last[1]-hs*Math.sin(ang-0.4));
      ctx.lineTo(last[0]-hs*Math.cos(ang+0.4), last[1]-hs*Math.sin(ang+0.4));
      ctx.closePath(); ctx.fill();
    }
    ctx.globalAlpha = 1;
  }

  // ── Painter's sort and draw face ──────────────────────
  function centroidZ(face) {
    let z = 0;
    for (const p of face.pts) { const v = applyView(applyPlaneRot(p)); z += v[2]; }
    return z / face.pts.length;
  }

  function drawFace(ctx, face) {
    const proj = face.pts.map(p => tf(p));
    // Compute face normal for lighting
    const a = face.pts[0], b = face.pts[1], c = face.pts[2];
    const ab = [b[0]-a[0], b[1]-a[1], b[2]-a[2]];
    const ac = [c[0]-a[0], c[1]-a[1], c[2]-a[2]];
    const nx = ab[1]*ac[2] - ab[2]*ac[1];
    const ny = ab[2]*ac[0] - ab[0]*ac[2];
    const nz = ab[0]*ac[1] - ab[1]*ac[0];
    const nl = Math.sqrt(nx*nx+ny*ny+nz*nz) || 1;
    // Light direction (camera space)
    const light = [0.4, 0.7, 0.6];
    const dot = Math.max(0.15, (nx/nl)*light[0] + (ny/nl)*light[1] + (nz/nl)*light[2]);

    const [r,g,b2] = face.color;
    const [sr,sg,sb] = face.stroke || [79,195,247];
    const lit = dot;

    ctx.globalAlpha = face.alpha || 0.85;
    ctx.fillStyle = `rgb(${Math.round(r*lit)},${Math.round(g*lit)},${Math.round(b2*lit)})`;
    ctx.strokeStyle = `rgba(${sr},${sg},${sb},0.6)`;
    ctx.lineWidth = 0.5;

    ctx.beginPath();
    ctx.moveTo(proj[0][0], proj[0][1]);
    for (let i = 1; i < proj.length; i++) ctx.lineTo(proj[i][0], proj[i][1]);
    ctx.closePath();
    ctx.fill();
    ctx.stroke();

    // Label if present
    if (face.label) {
      const mx = proj.reduce((s,p)=>s+p[0],0)/proj.length;
      const my = proj.reduce((s,p)=>s+p[1],0)/proj.length;
      ctx.globalAlpha = 1;
      ctx.fillStyle = face.labelColor || '#fff';
      ctx.font = 'bold 10px "Barlow Condensed", sans-serif';
      ctx.textAlign = 'center';
      ctx.fillText(face.label, mx, my - 8);
      ctx.textAlign = 'left';
    }
    ctx.globalAlpha = 1;
  }

  // ── HUD overlay ──────────────────────────────────────
  function drawHUD(ctx) {
    const labels = [
      { text: '● ROLLIO (φ)',       color: '#22c55e', desc: 'asse longitudinale · alettoni' },
      { text: '● BECCHEGGIO (θ)',   color: '#a78bfa', desc: 'asse trasversale · equilibratore' },
      { text: '● IMBARDATA (ψ)',    color: '#f97316', desc: 'asse verticale · timone di direzione' },
    ];
    let y = H - 72;
    for (const l of labels) {
      ctx.globalAlpha = 0.9;
      ctx.fillStyle = l.color;
      ctx.font = 'bold 11px "Barlow Condensed", sans-serif';
      ctx.fillText(l.text, 14, y);
      ctx.fillStyle = 'rgba(255,255,255,0.35)';
      ctx.font = '10px "Barlow Condensed", sans-serif';
      ctx.fillText(l.desc, 14, y + 13);
      y += 26;
    }
    ctx.globalAlpha = 1;

    // Active mode badge
    if (state.animMode && state.animMode !== 'none') {
      const modeInfo = {
        roll:  { label: 'ROLLIO ATTIVO',       color: '#22c55e' },
        pitch: { label: 'BECCHEGGIO ATTIVO',   color: '#a78bfa' },
        yaw:   { label: 'IMBARDATA ATTIVA',    color: '#f97316' },
      };
      const info = modeInfo[state.animMode];
      if (info) {
        ctx.globalAlpha = 0.95;
        ctx.fillStyle = info.color + '22';
        ctx.strokeStyle = info.color;
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.roundRect(W - 180, 50, 166, 28, 4);
        ctx.fill(); ctx.stroke();
        ctx.fillStyle = info.color;
        ctx.font = 'bold 12px "Barlow Condensed", sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText(info.label, W - 97, 69);
        ctx.textAlign = 'left';
        ctx.globalAlpha = 1;
      }
    }
  }

  // ── Main render loop ─────────────────────────────────
  const geom = getPlaneGeometry();

  function render() {
    // Animate
    if (state.animMode === 'roll') {
      state.rollAng += 0.03;
    } else if (state.animMode === 'pitch') {
      state.pitchAng += 0.025;
    } else if (state.animMode === 'yaw') {
      state.yawAng += 0.025;
    }

    ctx.clearRect(0, 0, W, H);

    // Background gradient
    const bg = ctx.createRadialGradient(W/2, H/2, 0, W/2, H/2, W*0.7);
    bg.addColorStop(0, '#060e20');
    bg.addColorStop(1, '#020508');
    ctx.fillStyle = bg; ctx.fillRect(0, 0, W, H);

    // Sort faces back-to-front
    const sorted = [...geom].sort((a, b) => {
      if (a.type === 'circle3d' || b.type === 'circle3d') return 0;
      return centroidZ(a) - centroidZ(b);
    });

    // Draw faces
    for (const face of sorted) {
      if (face.type === 'circle3d') {
        // Engine inlet circle
        const c = tf(face.center);
        ctx.globalAlpha = face.alpha;
        ctx.strokeStyle = `rgba(${face.color[0]},${face.color[1]},${face.color[2]},0.8)`;
        ctx.lineWidth = 1.5;
        ctx.beginPath();
        ctx.arc(c[0], c[1], face.r * 500 / (face.center[2] + 5), 0, Math.PI*2);
        ctx.stroke();
        ctx.globalAlpha = 1;
      } else {
        drawFace(ctx, face);
      }
    }

    // ── Draw 3D axes ─────────────────────────────────
    // X axis (longitudinal) = roll axis → green
    drawAxis(ctx, [0, 0, 1],  '#22c55e', 'ASSE LONG. (φ)', 1.55);
    // Y axis (vertical) = yaw axis → orange
    drawAxis(ctx, [0, 1, 0],  '#f97316', 'ASSE VERT. (ψ)', 1.3);
    // Z axis (transverse) = pitch axis → purple
    drawAxis(ctx, [1, 0, 0],  '#a78bfa', 'ASSE TRASV. (θ)', 1.5);

    // ── Draw rotation arcs ────────────────────────────
    if (state.animMode === 'roll') {
      drawRotArc(ctx, 'z', '#22c55e', 'φ', state.rollAng % (Math.PI*2));
    } else if (state.animMode === 'pitch') {
      drawRotArc(ctx, 'x', '#a78bfa', 'θ', state.pitchAng % (Math.PI*2));
    } else if (state.animMode === 'yaw') {
      drawRotArc(ctx, 'y', '#f97316', 'ψ', state.yawAng % (Math.PI*2));
    }

    // ── CG dot ────────────────────────────────────────
    const cg = tf([0,0,0]);
    ctx.globalAlpha = 1;
    ctx.strokeStyle = '#ffffff';
    ctx.fillStyle = '#ffffff';
    ctx.lineWidth = 1.5;
    ctx.beginPath(); ctx.arc(cg[0], cg[1], 5, 0, Math.PI*2); ctx.stroke();
    ctx.beginPath(); ctx.arc(cg[0], cg[1], 2, 0, Math.PI*2); ctx.fill();
    ctx.fillStyle = 'rgba(255,255,255,0.6)';
    ctx.font = '10px "Barlow Condensed", sans-serif';
    ctx.fillText('CG', cg[0]+8, cg[1]-6);

    drawHUD(ctx);

    _axesRAF = requestAnimationFrame(render);
  }
  render();
}

function axisAnim(mode) {
  if (!_axesState) return;
  if (mode === 'reset') {
    _axesState.animMode = null;
    _axesState.rollAng = 0;
    _axesState.pitchAng = 0;
    _axesState.yawAng = 0;
    ['roll','pitch','yaw'].forEach(m => {
      const btn = document.getElementById('btn-' + m);
      if (btn) btn.style.opacity = '1';
    });
    return;
  }
  if (_axesState.animMode === mode) {
    _axesState.animMode = null;
    const btn = document.getElementById('btn-' + mode);
    if (btn) btn.style.opacity = '1';
  } else {
    _axesState.animMode = mode;
    ['roll','pitch','yaw'].forEach(m => {
      const btn = document.getElementById('btn-' + m);
      if (btn) btn.style.opacity = (m === mode) ? '1' : '0.45';
    });
  }
}
</script>
</body>
</html>
