# aereoplano-e-le-sue-parti<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Come Vola un Aereo — Fisica e Strumenti</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;500;600;700&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --sky: #0a1628;
    --sky-mid: #0d2040;
    --sky-light: #1a3a6e;
    --accent: #4fc3f7;
    --accent2: #81d4fa;
    --gold: #ffd54f;
    --red: #ef5350;
    --green: #66bb6a;
    --orange: #ffa726;
    --purple: #ab47bc;
    --text: #e8f4fd;
    --text-dim: #8ab4c8;
    --card-bg: rgba(13,32,64,0.85);
    --border: rgba(79,195,247,0.25);
    --modal-bg: #07111f;
    --font-head: 'Rajdhani', sans-serif;
    --font-body: 'Crimson Pro', Georgia, serif;
    --glow: 0 0 24px rgba(79,195,247,0.3);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

  html { -webkit-text-size-adjust: 100%; }

  body {
    background: var(--sky);
    color: var(--text);
    font-family: var(--font-body);
    font-size: 17px;
    line-height: 1.55;
    min-height: 100vh;
    min-height: 100dvh;
    overflow-x: hidden;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  /* ── Stars background (lighter on mobile) ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      radial-gradient(1px 1px at 15% 10%, rgba(255,255,255,0.7) 0%, transparent 100%),
      radial-gradient(1px 1px at 42% 5%, rgba(255,255,255,0.5) 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 70% 15%, rgba(255,255,255,0.6) 0%, transparent 100%),
      radial-gradient(1px 1px at 88% 8%, rgba(255,255,255,0.4) 0%, transparent 100%),
      radial-gradient(1px 1px at 25% 22%, rgba(255,255,255,0.5) 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 55% 28%, rgba(255,255,255,0.3) 0%, transparent 100%),
      radial-gradient(1px 1px at 80% 35%, rgba(255,255,255,0.6) 0%, transparent 100%),
      radial-gradient(1px 1px at 10% 45%, rgba(255,255,255,0.4) 0%, transparent 100%),
      radial-gradient(1px 1px at 35% 55%, rgba(255,255,255,0.3) 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 62% 48%, rgba(255,255,255,0.5) 0%, transparent 100%),
      radial-gradient(1px 1px at 92% 52%, rgba(255,255,255,0.4) 0%, transparent 100%),
      radial-gradient(1px 1px at 18% 68%, rgba(255,255,255,0.3) 0%, transparent 100%),
      radial-gradient(1px 1px at 75% 72%, rgba(255,255,255,0.5) 0%, transparent 100%);
    pointer-events: none;
    z-index: 0;
  }

  /* ── Aurora glow background gradient ── */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 80% 50% at 50% 100%, rgba(26,58,110,0.55), transparent 70%),
      radial-gradient(ellipse 60% 40% at 20% 30%, rgba(79,195,247,0.08), transparent 60%),
      radial-gradient(ellipse 50% 35% at 85% 60%, rgba(171,71,188,0.06), transparent 60%);
    pointer-events: none;
    z-index: 0;
  }

  /* ── Header ── */
  header {
    position: relative;
    z-index: 10;
    text-align: center;
    padding: 56px 20px 36px;
  }

  .header-eyebrow {
    font-family: var(--font-head);
    font-size: 0.78rem;
    letter-spacing: 0.32em;
    color: var(--accent);
    text-transform: uppercase;
    opacity: 0;
    animation: fadeDown 0.8s 0.2s forwards;
    padding: 0 10px;
  }

  header h1 {
    font-family: var(--font-head);
    font-size: clamp(2rem, 7vw, 4.2rem);
    font-weight: 700;
    letter-spacing: 0.04em;
    line-height: 1.08;
    background: linear-gradient(135deg, #fff 0%, var(--accent2) 50%, var(--accent) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin: 14px 0 10px;
    opacity: 0;
    animation: fadeDown 0.8s 0.4s forwards;
  }

  header p {
    font-size: 1rem;
    font-style: italic;
    color: var(--text-dim);
    max-width: 560px;
    margin: 0 auto;
    padding: 0 8px;
    opacity: 0;
    animation: fadeDown 0.8s 0.6s forwards;
  }

  /* ── Plane SVG decorative ── */
  .plane-deco {
    width: 72px;
    margin: 0 auto 14px;
    animation: floatPlane 4s ease-in-out infinite, fadeIn 1s 0.8s forwards;
    opacity: 0;
    display: block;
    filter: drop-shadow(0 4px 12px rgba(79,195,247,0.35));
  }

  /* ── Grid ── */
  .grid {
    position: relative;
    z-index: 10;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(290px, 1fr));
    gap: 22px;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 20px 60px;
  }

  /* ── Cards ── */
  .card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 18px;
    padding: 28px 24px 64px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s cubic-bezier(0.34,1.4,0.64,1),
                box-shadow 0.3s ease,
                border-color 0.3s ease;
    opacity: 0;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    user-select: none;
  }

  .card.visible { animation: slideUp 0.55s forwards; }

  /* Top gradient accent (cockpit panel feel) */
  .card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% -20%, rgba(79,195,247,0.14), transparent 70%);
    opacity: 0;
    transition: opacity 0.3s;
    pointer-events: none;
  }

  /* Corner brackets (HUD aesthetic) */
  .card::after {
    content: '';
    position: absolute;
    top: 12px; left: 12px; right: 12px; bottom: 12px;
    border-radius: 12px;
    border: 1px solid transparent;
    pointer-events: none;
    background:
      linear-gradient(to right, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) top left/100% 1px no-repeat,
      linear-gradient(to bottom, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) top left/1px 100% no-repeat,
      linear-gradient(to left, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) top right/100% 1px no-repeat,
      linear-gradient(to bottom, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) top right/1px 100% no-repeat,
      linear-gradient(to right, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) bottom left/100% 1px no-repeat,
      linear-gradient(to top, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) bottom left/1px 100% no-repeat,
      linear-gradient(to left, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) bottom right/100% 1px no-repeat,
      linear-gradient(to top, var(--t, var(--accent)) 0, var(--t, var(--accent)) 14px, transparent 14px) bottom right/1px 100% no-repeat;
    opacity: 0.5;
    transition: opacity 0.3s;
  }

  .card:hover::before, .card:active::before { opacity: 1; }
  .card:hover::after, .card:active::after { opacity: 1; }

  @media (hover: hover) {
    .card:hover {
      transform: translateY(-6px) scale(1.015);
      box-shadow: var(--glow), 0 20px 40px rgba(0,0,0,0.5);
      border-color: color-mix(in srgb, var(--t, var(--accent)) 55%, transparent);
    }
  }

  .card:active {
    transform: scale(0.985);
    transition: transform 0.1s;
  }

  .card-tag {
    font-family: var(--font-head);
    font-size: 0.7rem;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    padding: 5px 11px;
    border-radius: 4px;
    margin-bottom: 18px;
    display: inline-block;
    font-weight: 600;
    position: relative;
    z-index: 1;
  }

  .card-number {
    position: absolute;
    top: 18px; right: 22px;
    font-family: var(--font-head);
    font-size: 3rem;
    font-weight: 700;
    opacity: 0.08;
    color: var(--t, var(--accent));
    line-height: 1;
    z-index: 1;
  }

  .card h2 {
    font-family: var(--font-head);
    font-size: 1.4rem;
    font-weight: 700;
    letter-spacing: 0.03em;
    margin-bottom: 10px;
    line-height: 1.2;
    position: relative;
    z-index: 1;
  }

  .card p {
    color: var(--text-dim);
    font-size: 0.95rem;
    line-height: 1.6;
    position: relative;
    z-index: 1;
  }

  .card-icon {
    width: 60px;
    height: 60px;
    margin-bottom: 18px;
    position: relative;
    z-index: 1;
  }

  /* Animated streamlines inside card icons */
  .card-icon path[stroke-dasharray] {
    animation: streamFlow 3s linear infinite;
  }

  .card-arrow {
    position: absolute;
    bottom: 20px; right: 22px;
    width: 32px; height: 32px;
    border-radius: 50%;
    border: 1.5px solid rgba(255,255,255,0.15);
    display: flex; align-items: center; justify-content: center;
    font-size: 0.95rem;
    transition: all 0.3s;
    color: var(--t, var(--accent));
    z-index: 1;
  }

  @media (hover: hover) {
    .card:hover .card-arrow {
      background: var(--t, var(--accent));
      color: var(--sky);
      border-color: var(--t, var(--accent));
      transform: translateX(3px);
    }
  }

  /* ── Theme colors per card ── */
  .card[data-theme="blue"] { --t: var(--accent); }
  .card[data-theme="purple"] { --t: var(--purple); }
  .card[data-theme="orange"] { --t: var(--orange); }
  .card[data-theme="green"] { --t: var(--green); }
  .card[data-theme="red"] { --t: var(--red); }

  .card .card-tag { background: rgba(255,255,255,0.06); color: var(--t, var(--accent)); }
  .card h2 { color: var(--t, var(--accent)); }

  /* ── Modal overlay ── */
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(4,10,20,0.88);
    z-index: 100;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    padding: 16px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
  }

  .modal-overlay.open {
    opacity: 1;
    pointer-events: all;
  }

  .modal {
    background: var(--modal-bg);
    border: 1px solid rgba(79,195,247,0.3);
    border-radius: 18px;
    max-width: 780px;
    width: 100%;
    padding: 40px 42px;
    position: relative;
    transform: translateY(30px) scale(0.97);
    transition: transform 0.4s cubic-bezier(0.34,1.3,0.64,1);
    margin: auto 0;
    box-shadow: 0 40px 80px rgba(0,0,0,0.7), var(--glow);
  }

  .modal-overlay.open .modal {
    transform: translateY(0) scale(1);
  }

  .modal-close {
    position: absolute;
    top: 14px; right: 14px;
    background: rgba(255,255,255,0.08);
    border: 1px solid rgba(255,255,255,0.1);
    color: var(--text);
    width: 44px; height: 44px;
    border-radius: 50%;
    font-size: 1.2rem;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
    z-index: 5;
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    box-shadow: 0 2px 12px rgba(0,0,0,0.5);
  }

  .modal-close:hover, .modal-close:active { background: var(--red); color: #fff; transform: scale(1.05); }

  .modal-tag {
    font-family: var(--font-head);
    font-size: 0.72rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    padding: 5px 11px;
    border-radius: 4px;
    margin-bottom: 14px;
    display: inline-block;
    font-weight: 600;
  }

  .modal h2 {
    font-family: var(--font-head);
    font-size: clamp(1.5rem, 5.5vw, 2.2rem);
    font-weight: 700;
    margin-bottom: 22px;
    line-height: 1.15;
    padding-right: 50px;
  }

  .modal-section { margin-bottom: 30px; }

  .modal-section h3 {
    font-family: var(--font-head);
    font-size: 1.05rem;
    letter-spacing: 0.06em;
    font-weight: 600;
    margin-bottom: 10px;
    padding-bottom: 6px;
    border-bottom: 1px solid rgba(255,255,255,0.08);
    color: var(--accent2);
    text-transform: uppercase;
  }

  .modal-section p {
    line-height: 1.75;
    color: #c5dde8;
    font-size: 1rem;
  }

  .formula-box {
    background: rgba(79,195,247,0.06);
    border-left: 3px solid var(--accent);
    border-radius: 0 8px 8px 0;
    padding: 16px 18px;
    margin: 14px 0;
    font-family: 'Courier New', monospace;
    font-size: 0.92rem;
    color: var(--accent2);
    line-height: 1.7;
    overflow-x: auto;
    word-break: break-word;
  }

  .formula-box .label {
    font-family: var(--font-body);
    font-size: 0.82rem;
    color: var(--text-dim);
    display: block;
    margin-top: 6px;
  }

  .example-box {
    background: rgba(255,213,79,0.06);
    border: 1px solid rgba(255,213,79,0.2);
    border-radius: 10px;
    padding: 16px 18px;
    margin-top: 14px;
  }

  .example-box .ex-title {
    font-family: var(--font-head);
    font-size: 0.78rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 8px;
  }

  .example-box p { color: #d4c8a0; font-size: 0.95rem; }

  .svg-wrap {
    width: 100%;
    margin: 20px 0;
    text-align: center;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }

  .svg-wrap svg { max-width: 100%; height: auto; display: inline-block; }

  /* ── Animations ── */
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-16px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    to { opacity: 0.55; }
  }

  @keyframes slideUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes floatPlane {
    0%, 100% { transform: translateY(0) rotate(-3deg); }
    50% { transform: translateY(-10px) rotate(3deg); }
  }

  @keyframes drawLine {
    from { stroke-dashoffset: 400; }
    to { stroke-dashoffset: 0; }
  }

  @keyframes streamFlow {
    from { stroke-dashoffset: 0; }
    to { stroke-dashoffset: -10; }
  }

  .airflow-line {
    stroke-dasharray: 400;
    stroke-dashoffset: 400;
    animation: drawLine 2s ease forwards;
  }
  .airflow-line:nth-child(2) { animation-delay: 0.1s; }
  .airflow-line:nth-child(3) { animation-delay: 0.2s; }
  .airflow-line:nth-child(4) { animation-delay: 0.3s; }
  .airflow-line:nth-child(5) { animation-delay: 0.4s; }

  @keyframes arcPulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
  }

  .modal-divider {
    border: none;
    border-top: 1px solid rgba(255,255,255,0.06);
    margin: 28px 0;
  }

  /* Table */
  .table-wrap { overflow-x: auto; -webkit-overflow-scrolling: touch; margin: 14px 0; }

  .info-table {
    width: 100%;
    min-width: 380px;
    border-collapse: collapse;
    font-size: 0.92rem;
  }

  .info-table th {
    font-family: var(--font-head);
    letter-spacing: 0.08em;
    font-size: 0.75rem;
    text-transform: uppercase;
    padding: 10px 12px;
    background: rgba(79,195,247,0.08);
    color: var(--accent);
    text-align: left;
    border-bottom: 1px solid rgba(79,195,247,0.2);
    white-space: nowrap;
  }

  .info-table td {
    padding: 10px 12px;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    color: #c5dde8;
    vertical-align: top;
  }

  .info-table tr:last-child td { border-bottom: none; }
  .info-table tr:hover td { background: rgba(255,255,255,0.02); }

  /* ── Header decoration ── */
  .title-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 18px;
    margin: 14px 0 10px;
  }

  .title-tick {
    flex: 0 0 auto;
    width: clamp(28px, 8vw, 56px);
    height: 1px;
    background: linear-gradient(to right, transparent, var(--accent), transparent);
    opacity: 0;
    animation: fadeIn 1s 0.6s forwards;
  }

  .title-wrap h1 {
    margin: 0;
  }

  .header-meta {
    margin-top: 18px;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    opacity: 0;
    animation: fadeDown 0.8s 0.8s forwards;
    flex-wrap: wrap;
    justify-content: center;
  }

  .meta-chip {
    font-family: var(--font-head);
    font-size: 0.66rem;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    padding: 5px 12px;
    border: 1px solid rgba(79,195,247,0.25);
    border-radius: 20px;
    color: var(--accent2);
    background: rgba(79,195,247,0.04);
  }

  .meta-sep {
    color: var(--text-dim);
    opacity: 0.5;
  }

  /* ── Footer ── */
  footer {
    position: relative;
    z-index: 10;
    text-align: center;
    padding: 40px 20px 56px;
    color: var(--text-dim);
    font-size: 0.85rem;
    border-top: 1px solid rgba(79,195,247,0.08);
    margin-top: 20px;
  }

  footer .foot-brand {
    font-family: var(--font-head);
    font-size: 0.95rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--accent2);
    margin-bottom: 6px;
  }

  footer .foot-sub {
    font-style: italic;
    color: var(--text-dim);
    font-size: 0.82rem;
  }

  /* ── Responsive: tablet ── */
  @media (max-width: 900px) {
    .modal { padding: 36px 32px; }
  }

  /* ── Responsive: phone landscape / large phone ── */
  @media (max-width: 640px) {
    body { font-size: 16px; }
    header { padding: 40px 18px 28px; }
    .header-eyebrow { font-size: 0.7rem; letter-spacing: 0.25em; }
    header h1 { letter-spacing: 0.02em; }
    header p { font-size: 0.95rem; }
    .plane-deco { width: 60px; }
    .grid { grid-template-columns: 1fr; padding: 0 16px 40px; gap: 18px; }
    .card { padding: 24px 22px 60px; border-radius: 16px; }
    .card-number { font-size: 2.6rem; top: 14px; right: 18px; }
    .card h2 { font-size: 1.3rem; }
    .card p { font-size: 0.92rem; }
    .card-icon { width: 54px; height: 54px; margin-bottom: 14px; }
    .card-arrow { width: 36px; height: 36px; bottom: 16px; right: 18px; }
    .modal-overlay { padding: 10px; }
    .modal { padding: 28px 22px 36px; border-radius: 16px; }
    .modal h2 { margin-bottom: 18px; }
    .modal-section { margin-bottom: 24px; }
    .modal-section p { font-size: 0.96rem; line-height: 1.7; }
    .modal-section h3 { font-size: 0.98rem; }
    .formula-box { font-size: 0.85rem; padding: 14px 14px; }
    .example-box { padding: 14px 14px; }
    .example-box p { font-size: 0.9rem; }
    .info-table { font-size: 0.85rem; }
    .info-table th, .info-table td { padding: 8px 10px; }
    /* Disable card corner brackets on small screens for cleaner look */
    .card::after { display: none; }
    footer { padding: 32px 16px 44px; }
  }

  /* ── Responsive: small phone ── */
  @media (max-width: 380px) {
    header { padding: 32px 14px 24px; }
    .header-eyebrow { font-size: 0.66rem; letter-spacing: 0.2em; }
    .grid { padding: 0 12px 36px; }
    .card { padding: 22px 18px 56px; }
    .card-tag { font-size: 0.66rem; letter-spacing: 0.22em; padding: 4px 9px; }
    .card h2 { font-size: 1.2rem; }
    .modal { padding: 24px 18px 32px; }
    .formula-box { font-size: 0.78rem; padding: 12px 12px; }
  }

  /* ── Reduce visual effects for users who prefer reduced motion ── */
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.01ms !important;
    }
    .plane-deco { animation: none; opacity: 0.5; }
    .card-icon path[stroke-dasharray] { animation: none; }
  }

  /* ── Low-perf devices: disable backdrop-filter ── */
  @supports not (backdrop-filter: blur(6px)) {
    .card, .modal-overlay, .modal-close { backdrop-filter: none; }
  }
</style>
</head>
<body>

<!-- ══ HEADER ══ -->
<header>
  <div class="header-eyebrow">Costruzioni Aeronautiche · Aerodinamica · Meccanica del Volo</div>

  <!-- Decorative plane -->
  <svg class="plane-deco" viewBox="0 0 120 60" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M5 30 L85 10 L115 30 L85 38 Z" fill="rgba(79,195,247,0.6)" stroke="rgba(79,195,247,0.9)" stroke-width="1"/>
    <path d="M60 30 L80 50 L65 40 Z" fill="rgba(79,195,247,0.4)" stroke="rgba(79,195,247,0.7)" stroke-width="1"/>
    <path d="M30 25 L50 18 L48 30 Z" fill="rgba(79,195,247,0.3)" stroke="rgba(79,195,247,0.6)" stroke-width="0.8"/>
  </svg>

  <div class="title-wrap">
    <span class="title-tick"></span>
    <h1>Come Vola un Aereo</h1>
    <span class="title-tick"></span>
  </div>
  <p>Fisica, Aerodinamica e Strumenti — Infografica Interattiva</p>
  <div class="header-meta">
    <span class="meta-chip">6 SCHEDE</span>
    <span class="meta-sep">·</span>
    <span class="meta-chip">TOCCA PER APRIRE</span>
  </div>
</header>

<!-- ══ CARDS GRID ══ -->
<div class="grid">

  <!-- 1 — Bernoulli -->
  <div class="card" data-theme="blue" data-modal="bernoulli">
    <span class="card-number">01</span>
    <div class="card-tag">Aerodinamica Fondamentale</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <!-- Linee di corrente sopra (accelerate, ravvicinate → bassa p) -->
      <path d="M2 19 Q14 12 28 13 Q42 14 54 19" stroke="#4fc3f7" stroke-width="0.9" fill="none" stroke-dasharray="3 2" opacity="0.85"/>
      <path d="M2 23 Q14 17 28 18 Q42 19 54 23" stroke="#4fc3f7" stroke-width="0.9" fill="none" stroke-dasharray="3 2" opacity="0.6"/>
      <!-- Linee di corrente sotto (decelerate, distanziate → alta p) -->
      <path d="M2 42 Q14 47 28 47 Q42 47 54 42" stroke="#4fc3f7" stroke-width="0.9" fill="none" stroke-dasharray="3 2" opacity="0.45"/>
      <!-- Profilo NACA 2412 -->
      <path d="M 6.00 32.00 L 6.04 31.68 L 6.23 31.37 L 6.55 31.05 L 7.02 30.73 L 7.63 30.42 L 8.38 30.12 L 9.26 29.83 L 10.26 29.56 L 11.38 29.31 L 12.61 29.09 L 13.95 28.90 L 15.38 28.75 L 16.90 28.63 L 18.49 28.55 L 20.15 28.52 L 21.85 28.52 L 23.60 28.57 L 25.36 28.65 L 27.14 28.76 L 28.92 28.89 L 30.69 29.04 L 32.45 29.22 L 34.17 29.41 L 35.85 29.61 L 37.48 29.83 L 39.05 30.05 L 40.55 30.27 L 41.96 30.49 L 43.28 30.71 L 44.51 30.93 L 45.62 31.13 L 46.62 31.32 L 47.50 31.49 L 48.26 31.64 L 48.88 31.76 L 49.37 31.87 L 49.72 31.94 L 49.93 31.98 L 50.00 32.00 L 49.93 32.01 L 49.71 32.02 L 49.35 32.05 L 48.86 32.09 L 48.22 32.14 L 47.46 32.19 L 46.57 32.26 L 45.55 32.33 L 44.43 32.41 L 43.20 32.50 L 41.87 32.59 L 40.45 32.69 L 38.95 32.79 L 37.38 32.90 L 35.75 33.00 L 34.07 33.11 L 32.36 33.22 L 30.61 33.32 L 28.86 33.42 L 27.09 33.52 L 25.34 33.60 L 23.60 33.67 L 21.90 33.73 L 20.25 33.79 L 18.64 33.83 L 17.10 33.86 L 15.62 33.86 L 14.22 33.85 L 12.91 33.82 L 11.69 33.76 L 10.57 33.67 L 9.56 33.56 L 8.66 33.42 L 7.89 33.25 L 7.24 33.05 L 6.73 32.83 L 6.34 32.58 L 6.10 32.30 L 6.00 32.00 Z"
            fill="rgba(79,195,247,0.18)" stroke="#4fc3f7" stroke-width="1.4" stroke-linejoin="round"/>
      <!-- Freccia portanza L -->
      <path d="M22 28 L22 8" stroke="#81d4fa" stroke-width="1.8" marker-end="url(#arrB1)"/>
      <text x="24" y="14" fill="#81d4fa" font-size="7" font-family="Rajdhani,sans-serif" font-weight="600">L</text>
      <!-- Simboli pressione -->
      <text x="13" y="11" fill="#4fc3f7" font-size="7" font-family="Rajdhani,sans-serif" opacity="0.85">−p</text>
      <text x="13" y="51" fill="#4fc3f7" font-size="7" font-family="Rajdhani,sans-serif" opacity="0.65">+p</text>
      <defs><marker id="arrB1" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0 0 L6 3 L0 6 Z" fill="#81d4fa"/></marker></defs>
    </svg>
    <h2>Bernoulli &amp; Portanza</h2>
    <p>Il principio che trasforma l'aria in forza ascensionale — cuore di ogni profilo alare.</p>
    <div class="card-arrow">→</div>
  </div>

  <!-- 2 — Profili alari -->
  <div class="card" data-theme="purple" data-modal="profili">
    <span class="card-number">02</span>
    <div class="card-tag">Geometria del Profilo</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <!-- Linea di corda -->
      <line x1="6" y1="32" x2="50" y2="32" stroke="rgba(171,71,188,0.45)" stroke-width="0.7" stroke-dasharray="2 1.5"/>
      <!-- Profilo NACA 2412 -->
      <path d="M 6.00 32.00 L 6.04 31.68 L 6.23 31.37 L 6.55 31.05 L 7.02 30.73 L 7.63 30.42 L 8.38 30.12 L 9.26 29.83 L 10.26 29.56 L 11.38 29.31 L 12.61 29.09 L 13.95 28.90 L 15.38 28.75 L 16.90 28.63 L 18.49 28.55 L 20.15 28.52 L 21.85 28.52 L 23.60 28.57 L 25.36 28.65 L 27.14 28.76 L 28.92 28.89 L 30.69 29.04 L 32.45 29.22 L 34.17 29.41 L 35.85 29.61 L 37.48 29.83 L 39.05 30.05 L 40.55 30.27 L 41.96 30.49 L 43.28 30.71 L 44.51 30.93 L 45.62 31.13 L 46.62 31.32 L 47.50 31.49 L 48.26 31.64 L 48.88 31.76 L 49.37 31.87 L 49.72 31.94 L 49.93 31.98 L 50.00 32.00 L 49.93 32.01 L 49.71 32.02 L 49.35 32.05 L 48.86 32.09 L 48.22 32.14 L 47.46 32.19 L 46.57 32.26 L 45.55 32.33 L 44.43 32.41 L 43.20 32.50 L 41.87 32.59 L 40.45 32.69 L 38.95 32.79 L 37.38 32.90 L 35.75 33.00 L 34.07 33.11 L 32.36 33.22 L 30.61 33.32 L 28.86 33.42 L 27.09 33.52 L 25.34 33.60 L 23.60 33.67 L 21.90 33.73 L 20.25 33.79 L 18.64 33.83 L 17.10 33.86 L 15.62 33.86 L 14.22 33.85 L 12.91 33.82 L 11.69 33.76 L 10.57 33.67 L 9.56 33.56 L 8.66 33.42 L 7.89 33.25 L 7.24 33.05 L 6.73 32.83 L 6.34 32.58 L 6.10 32.30 L 6.00 32.00 Z"
            fill="rgba(171,71,188,0.18)" stroke="#ab47bc" stroke-width="1.4" stroke-linejoin="round"/>
      <!-- Linea di camber media -->
      <path d="M 6 32 Q 17 30.5 28 30.7 Q 39 31 50 32" stroke="rgba(171,71,188,0.75)" stroke-width="0.9" fill="none" stroke-dasharray="2 1.5"/>
      <!-- Indicatore spessore t -->
      <line x1="22" y1="28.5" x2="22" y2="33.7" stroke="#ffd54f" stroke-width="0.8"/>
      <text x="24" y="32" fill="#ffd54f" font-size="6" font-family="Rajdhani,sans-serif" font-style="italic">t</text>
      <!-- LE / TE -->
      <circle cx="6" cy="32" r="1.1" fill="#ab47bc"/>
      <circle cx="50" cy="32" r="0.8" fill="#ab47bc"/>
    </svg>
    <h2>Profili Alari</h2>
    <p>Corda, camber, spessore relativo: come la forma dell'ala determina le sue caratteristiche aerodinamiche.</p>
    <div class="card-arrow">→</div>
  </div>

  <!-- 3 — Strumenti barometrici vs giroscopici -->
  <div class="card" data-theme="orange" data-modal="strumenti">
    <span class="card-number">03</span>
    <div class="card-tag">Strumentazione di Bordo</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <circle cx="18" cy="28" r="14" stroke="#ffa726" stroke-width="1.5" fill="rgba(255,167,38,0.08)"/>
      <path d="M18 28 L18 16" stroke="#ffa726" stroke-width="2" stroke-linecap="round"/>
      <path d="M18 28 L25 32" stroke="#ffa726" stroke-width="1.5" stroke-linecap="round"/>
      <rect x="35" y="14" width="18" height="28" rx="3" stroke="#ffa726" stroke-width="1.2" fill="rgba(255,167,38,0.06)"/>
      <circle cx="44" cy="28" r="6" stroke="#ffa726" stroke-width="1" fill="none"/>
      <path d="M44 22 L44 34 M38 28 L50 28" stroke="#ffa726" stroke-width="0.8" opacity="0.6"/>
    </svg>
    <h2>Barometrici vs Giroscopici</h2>
    <p>Due famiglie di strumenti con principi fisici opposti: pressione dell'aria contro inerzia rotazionale.</p>
    <div class="card-arrow">→</div>
  </div>

  <!-- 4 — Stallo -->
  <div class="card" data-theme="red" data-modal="stallo">
    <span class="card-number">04</span>
    <div class="card-tag">Meccanica del Volo</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <!-- Profilo NACA 4415 ruotato a alpha=18 deg -->
      <path d="M 10.49 28.91 L 10.60 28.57 L 10.83 28.25 L 11.20 27.97 L 11.70 27.72 L 12.32 27.52 L 13.07 27.35 L 13.93 27.23 L 14.91 27.17 L 15.98 27.17 L 17.15 27.22 L 18.41 27.35 L 19.74 27.54 L 21.13 27.81 L 22.57 28.14 L 24.06 28.55 L 25.57 29.03 L 27.10 29.57 L 28.60 30.16 L 30.11 30.79 L 31.61 31.45 L 33.10 32.14 L 34.55 32.84 L 35.97 33.57 L 37.35 34.29 L 38.68 35.02 L 39.94 35.73 L 41.14 36.44 L 42.27 37.11 L 43.32 37.76 L 44.28 38.37 L 45.15 38.94 L 45.93 39.46 L 46.61 39.92 L 47.19 40.32 L 47.67 40.66 L 48.05 40.92 L 48.32 41.12 L 48.48 41.23 L 48.53 41.27 L 48.47 41.25 L 48.28 41.20 L 47.96 41.11 L 47.52 40.99 L 46.95 40.84 L 46.27 40.65 L 45.48 40.43 L 44.59 40.19 L 43.59 39.92 L 42.50 39.62 L 41.33 39.31 L 40.07 38.97 L 38.75 38.62 L 37.37 38.25 L 35.94 37.88 L 34.46 37.49 L 32.96 37.10 L 31.43 36.71 L 29.89 36.31 L 28.35 35.90 L 26.82 35.50 L 25.30 35.09 L 23.85 34.70 L 22.43 34.32 L 21.05 33.94 L 19.72 33.58 L 18.45 33.22 L 17.25 32.86 L 16.13 32.51 L 15.09 32.15 L 14.14 31.79 L 13.28 31.44 L 12.53 31.08 L 11.89 30.71 L 11.36 30.35 L 10.95 29.99 L 10.67 29.63 L 10.51 29.27 L 10.49 28.91 Z"
            fill="rgba(239,83,80,0.20)" stroke="#ef5350" stroke-width="1.4" stroke-linejoin="round"/>
      <!-- Linea di corrente che si separa sull'estradosso -->
      <path d="M2 26 Q8 22 14 21" stroke="#ef5350" stroke-width="0.9" fill="none" opacity="0.8"/>
      <!-- Vortici di scia (separazione) -->
      <path d="M22 19 q 2 -3 4 0 q 2 3 4 0" stroke="#ef5350" stroke-width="0.9" fill="none" opacity="0.85"/>
      <path d="M32 16 q 2 -3 4 0 q 2 3 4 0" stroke="#ef5350" stroke-width="0.9" fill="none" opacity="0.7"/>
      <path d="M42 14 q 2 -3 4 0 q 2 3 4 0" stroke="#ef5350" stroke-width="0.9" fill="none" opacity="0.55"/>
      <!-- Indicazione angolo di incidenza alpha -->
      <line x1="2" y1="34" x2="14" y2="34" stroke="rgba(239,83,80,0.4)" stroke-width="0.7" stroke-dasharray="2 1.5"/>
      <path d="M6 34 A 4 4 0 0 0 9.5 30.5" stroke="#ef5350" stroke-width="0.8" fill="none"/>
      <text x="8" y="33" fill="#ef5350" font-size="6" font-family="Rajdhani,sans-serif" font-style="italic">α</text>
    </svg>
    <h2>Lo Stallo</h2>
    <p>Quando l'angolo di incidenza supera il critico, il flusso si separa e la portanza crolla: fisica e prevenzione.</p>
    <div class="card-arrow">→</div>
  </div>

  <!-- 5 — Pitot-Statico -->
  <div class="card" data-theme="green" data-modal="pitot">
    <span class="card-number">05</span>
    <div class="card-tag">Sensori Esterni</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <rect x="4" y="24" width="40" height="8" rx="4" fill="rgba(102,187,106,0.15)" stroke="#66bb6a" stroke-width="1.5"/>
      <rect x="44" y="26" width="8" height="4" rx="1" fill="rgba(102,187,106,0.3)" stroke="#66bb6a" stroke-width="1"/>
      <path d="M20 28 L20 18 L44 18" stroke="#66bb6a" stroke-width="1.2" stroke-dasharray="2 2" fill="none"/>
      <circle cx="44" cy="18" r="5" stroke="#66bb6a" stroke-width="1.2" fill="rgba(102,187,106,0.1)"/>
      <path d="M42 18 L46 18" stroke="#66bb6a" stroke-width="1"/>
    </svg>
    <h2>Impianto Pitot-Statico</h2>
    <p>Il sistema che misura velocità e quota: come le differenze di pressione alimentano altimetro e anemometro.</p>
    <div class="card-arrow">→</div>
  </div>

  <!-- 6 — Codici colore / Velocità limite -->
  <div class="card" data-theme="red" data-modal="codici">
    <span class="card-number">06</span>
    <div class="card-tag">Sicurezza del Volo</div>
    <svg class="card-icon" viewBox="0 0 56 56" fill="none">
      <path d="M8 44 A24 24 0 0 1 48 44" stroke="#333" stroke-width="8" stroke-linecap="round" fill="none"/>
      <path d="M8 44 A24 24 0 0 1 32 20" stroke="#66bb6a" stroke-width="8" stroke-linecap="round" fill="none"/>
      <path d="M38 22 A24 24 0 0 1 48 44" stroke="#ef5350" stroke-width="8" stroke-linecap="round" fill="none"/>
      <path d="M28 44 L38 28" stroke="white" stroke-width="2" stroke-linecap="round"/>
    </svg>
    <h2>Codici Colore &amp; Limiti</h2>
    <p>Verde, giallo, rosso sull'anemometro: l'arcobaleno dei limiti strutturali e operativi dell'aeromobile.</p>
    <div class="card-arrow">→</div>
  </div>

</div>

<!-- ══ FOOTER ══ -->
<footer>
  <div class="foot-brand">D'Amata Alessandro</div>
  <div class="foot-sub">Costruzioni Aeronautiche · ITIS E. Majorana — Infografica didattica</div>
</footer>

<!-- ══ MODAL ══ -->
<div class="modal-overlay" id="modalOverlay" role="dialog" aria-modal="true">
  <div class="modal" id="modalBox">
    <button class="modal-close" id="modalClose" aria-label="Chiudi">✕</button>
    <div id="modalContent"></div>
  </div>
</div>

<!-- ══ MODAL CONTENT DATA ══ -->
<script>
const MODALS = {

  bernoulli: {
    tag: 'Aerodinamica Fondamentale',
    theme: '#4fc3f7',
    title: 'Bernoulli e la Portanza',
    html: `
      <div class="modal-section">
        <h3>Il Principio di Bernoulli</h3>
        <p>Il teorema di Bernoulli afferma che in un fluido in moto stazionario e incomprimibile, lungo una linea di flusso, la somma dell'energia cinetica, potenziale e di pressione rimane costante:</p>
        <div class="formula-box">
          p + ½ρv² + ρgh = costante
          <span class="label">p = pressione statica [Pa] · ρ = densità del fluido [kg/m³] · v = velocità [m/s] · h = quota [m]</span>
        </div>
        <p>Per il volo orizzontale si trascura il termine ρgh, ottenendo la relazione più usata in aerodinamica: <em>dove la velocità aumenta, la pressione diminuisce</em>.</p>
      </div>

      <!-- SVG: profilo con flusso -->
      <div class="svg-wrap">
        <svg viewBox="0 0 500 180" xmlns="http://www.w3.org/2000/svg" style="max-width:100%">
          <defs>
            <marker id="mArr" markerWidth="7" markerHeight="7" refX="6" refY="3.5" orient="auto">
              <polygon points="0 0, 7 3.5, 0 7" fill="#4fc3f7" opacity="0.7"/>
            </marker>
          </defs>
          <!-- Wing cross-section: NACA 2412 (m=2%, p=40%, t=12%) -->
          <path d="M 60.00 100.00 L 60.09 98.20 L 60.73 96.39 L 61.91 94.57 L 63.63 92.75 L 65.89 90.93 L 68.68 89.12 L 72.00 87.33 L 75.84 85.58 L 80.19 83.86 L 85.03 82.19 L 90.36 80.59 L 96.15 79.06 L 102.40 77.61 L 109.09 76.26 L 116.19 75.02 L 123.68 73.90 L 131.54 72.90 L 139.76 72.04 L 148.30 71.31 L 157.13 70.73 L 166.24 70.31 L 175.59 70.03 L 185.15 69.91 L 194.90 69.94 L 204.80 70.13 L 214.81 70.47 L 224.86 70.93 L 234.98 71.49 L 245.14 72.16 L 255.31 72.92 L 265.46 73.76 L 275.56 74.68 L 285.58 75.68 L 295.50 76.74 L 305.28 77.85 L 314.90 79.02 L 324.33 80.22 L 333.55 81.46 L 342.53 82.71 L 351.24 83.99 L 359.65 85.27 L 367.76 86.54 L 375.52 87.81 L 382.93 89.06 L 389.96 90.28 L 396.59 91.46 L 402.80 92.59 L 408.58 93.68 L 413.91 94.69 L 418.78 95.64 L 423.17 96.52 L 427.07 97.30 L 430.47 98.00 L 433.37 98.60 L 435.75 99.10 L 437.60 99.49 L 438.93 99.77 L 439.73 99.94 L 440.00 100.00 L 439.73 100.02 L 438.91 100.08 L 437.56 100.19 L 435.67 100.33 L 433.24 100.52 L 430.30 100.74 L 426.84 101.01 L 422.87 101.30 L 418.42 101.64 L 413.48 102.00 L 408.08 102.40 L 402.23 102.82 L 395.95 103.27 L 389.26 103.75 L 382.17 104.25 L 374.71 104.77 L 366.90 105.31 L 358.77 105.87 L 350.32 106.44 L 341.60 107.03 L 332.62 107.63 L 323.42 108.24 L 314.01 108.85 L 304.42 109.47 L 294.69 110.08 L 284.83 110.69 L 274.88 111.29 L 264.86 111.87 L 254.81 112.43 L 244.75 112.96 L 234.70 113.46 L 224.70 113.92 L 214.78 114.33 L 205.01 114.70 L 195.40 115.04 L 185.94 115.35 L 176.66 115.62 L 167.59 115.83 L 158.74 115.99 L 150.14 116.08 L 141.82 116.10 L 133.80 116.04 L 126.09 115.89 L 118.71 115.66 L 111.70 115.33 L 105.06 114.90 L 98.82 114.37 L 92.98 113.74 L 87.58 113.00 L 82.62 112.16 L 78.12 111.22 L 74.09 110.17 L 70.55 109.02 L 67.50 107.76 L 64.96 106.41 L 62.93 104.95 L 61.42 103.40 L 60.45 101.75 L 60.00 100.00 Z"
                fill="rgba(79,195,247,0.18)" stroke="#4fc3f7" stroke-width="2" stroke-linejoin="round"/>

          <!-- Upper streamlines (accelerated) -->
          <path class="airflow-line" d="M10 60 Q100 40 200 55 Q300 65 490 58" stroke="#81d4fa" stroke-width="1.5" fill="none" opacity="0.9"/>
          <path class="airflow-line" d="M10 50 Q100 32 200 46 Q310 58 490 46" stroke="#81d4fa" stroke-width="1.2" fill="none" opacity="0.7"/>
          <path class="airflow-line" d="M10 38 Q100 28 200 36 Q310 44 490 38" stroke="#81d4fa" stroke-width="1" fill="none" opacity="0.5"/>

          <!-- Lower streamlines (slower) -->
          <path class="airflow-line" d="M10 128 Q130 128 200 125 Q310 122 490 126" stroke="#4fc3f7" stroke-width="1.5" fill="none" opacity="0.7" style="animation-delay:0.5s"/>
          <path class="airflow-line" d="M10 142 Q130 140 200 138 Q310 136 490 140" stroke="#4fc3f7" stroke-width="1" fill="none" opacity="0.5" style="animation-delay:0.6s"/>

          <!-- Lift arrow -->
          <path d="M250 70 L250 20" stroke="#ffd54f" stroke-width="3" marker-end="url(#lArr)"/>
          <defs>
            <marker id="lArr" markerWidth="8" markerHeight="8" refX="4" refY="4" orient="auto">
              <polygon points="0 0, 8 4, 0 8" fill="#ffd54f"/>
            </marker>
          </defs>
          <text x="260" y="18" fill="#ffd54f" font-family="Rajdhani,sans-serif" font-size="13" font-weight="600">PORTANZA L</text>

          <!-- Labels -->
          <text x="490" y="56" fill="#81d4fa" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="end">v alta → p bassa</text>
          <text x="490" y="130" fill="#4fc3f7" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="end">v bassa → p alta</text>

          <!-- incoming arrow -->
          <path d="M5 95 L42 95" stroke="#4fc3f7" stroke-width="2" marker-end="url(#mArr)"/>
          <text x="5" y="88" fill="#4fc3f7" font-size="11" font-family="Rajdhani,sans-serif">V∞</text>
        </svg>
      </div>

      <div class="modal-section">
        <h3>La Forza di Portanza</h3>
        <p>La portanza (L) è determinata dalla differenza di pressione tra intradosso ed estradosso moltiplicata per la superficie alare:</p>
        <div class="formula-box">
          L = ½ · ρ · V² · S · C<sub>L</sub>
          <span class="label">ρ = densità aria ISA [kg/m³] · V = velocità TAS [m/s] · S = superficie alare [m²] · C<sub>L</sub> = coefficiente di portanza [-]</span>
        </div>
        <p>Il C<sub>L</sub> dipende dall'angolo di incidenza α e dalla geometria del profilo. Per piccoli angoli è approssimativamente lineare: <strong>C<sub>L</sub> ≈ 2π sin(α)</strong> (teoria delle ali sottili di Joukowski).</p>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Esempio Pratico — Cessna 172</div>
        <p>S = 16,2 m² · C<sub>L</sub> max ≈ 1,45 · ρ<sub>SL</sub> = 1,225 kg/m³<br>
        Velocità di stallo V<sub>S</sub> = √(2W / ρ S C<sub>L max</sub>) = √(2×11.100 / 1,225×16,2×1,45) ≈ <strong>31,5 m/s (61 kt)</strong>.
        </p>
      </div>
    `
  },

  profili: {
    tag: 'Geometria del Profilo',
    theme: '#ab47bc',
    title: 'Profili Alari: Geometria e Nomenclatura',
    html: `
      <div class="modal-section">
        <h3>Anatomia del Profilo</h3>
        <p>Un profilo alare (airfoil) è la sezione trasversale dell'ala. I parametri fondamentali sono:</p>
        <div class="table-wrap"><table class="info-table">
          <tr><th>Parametro</th><th>Definizione</th><th>Simbolo tipico</th></tr>
          <tr><td>Corda</td><td>Segmento dal bordo d'attacco al bordo di uscita</td><td>c</td></tr>
          <tr><td>Camber (freccia)</td><td>Distanza max tra linea media e corda</td><td>f</td></tr>
          <tr><td>Spessore massimo</td><td>Distanza massima tra estradosso e intradosso</td><td>t</td></tr>
          <tr><td>Spessore relativo</td><td>t / c × 100 (%)</td><td>τ</td></tr>
          <tr><td>Posizione camber max</td><td>Distanza dal bordo d'attacco / c</td><td>p</td></tr>
        </table></div>
      </div>

      <!-- SVG profilo annotato -->
      <div class="svg-wrap">
        <svg viewBox="0 0 500 160" xmlns="http://www.w3.org/2000/svg">
          <!-- Chord line -->
          <line x1="30" y1="80" x2="470" y2="80" stroke="rgba(171,71,188,0.4)" stroke-width="1.5" stroke-dasharray="5 3"/>

          <!-- Airfoil: NACA 4412 (m=4%, p=40%, t=12%) -->
          <path d="M 30.00 80.00 L 29.91 77.91 L 30.45 75.75 L 31.63 73.52 L 33.46 71.22 L 35.91 68.87 L 39.00 66.47 L 42.72 64.05 L 47.05 61.61 L 52.00 59.18 L 57.54 56.78 L 63.66 54.41 L 70.35 52.12 L 77.58 49.90 L 85.35 47.80 L 93.61 45.82 L 102.35 43.99 L 111.55 42.32 L 121.16 40.84 L 131.17 39.55 L 141.54 38.48 L 152.23 37.63 L 163.21 37.01 L 174.45 36.64 L 185.91 36.51 L 197.55 36.64 L 209.28 37.01 L 220.99 37.57 L 232.77 38.28 L 244.60 39.15 L 256.43 40.16 L 268.24 41.30 L 279.98 42.57 L 291.63 43.96 L 303.15 45.45 L 314.51 47.04 L 325.67 48.70 L 336.60 50.44 L 347.28 52.24 L 357.67 54.08 L 367.75 55.95 L 377.48 57.84 L 386.84 59.74 L 395.81 61.62 L 404.35 63.49 L 412.46 65.31 L 420.10 67.09 L 427.25 68.80 L 433.91 70.43 L 440.04 71.97 L 445.63 73.40 L 450.68 74.72 L 455.16 75.91 L 459.07 76.97 L 462.39 77.88 L 465.12 78.63 L 467.25 79.23 L 468.78 79.65 L 469.69 79.91 L 470.00 80.00 L 469.68 80.00 L 468.73 80.01 L 467.15 80.03 L 464.94 80.05 L 462.11 80.09 L 458.67 80.13 L 454.63 80.17 L 450.00 80.23 L 444.80 80.30 L 439.05 80.38 L 432.75 80.47 L 425.94 80.58 L 418.63 80.71 L 410.84 80.85 L 402.61 81.01 L 393.94 81.19 L 384.87 81.40 L 375.43 81.63 L 365.64 81.89 L 355.53 82.18 L 345.14 82.49 L 334.48 82.83 L 323.60 83.20 L 312.52 83.60 L 301.27 84.03 L 289.90 84.47 L 278.42 84.93 L 266.87 85.41 L 255.28 85.90 L 243.69 86.39 L 232.12 86.87 L 220.61 87.34 L 209.19 87.80 L 198.03 88.24 L 187.07 88.72 L 176.28 89.23 L 165.70 89.75 L 155.35 90.27 L 145.26 90.78 L 135.44 91.26 L 125.93 91.69 L 116.74 92.07 L 107.90 92.38 L 99.43 92.60 L 91.35 92.73 L 83.69 92.76 L 76.46 92.66 L 69.68 92.45 L 63.38 92.09 L 57.57 91.60 L 52.27 90.96 L 47.49 90.17 L 43.26 89.21 L 39.59 88.10 L 36.49 86.82 L 33.97 85.37 L 32.04 83.75 L 30.72 81.96 L 30.00 80.00 Z"
                fill="rgba(171,71,188,0.15)" stroke="#ab47bc" stroke-width="2.5" stroke-linejoin="round"/>

          <!-- Mean camber line (real NACA 4412) -->
          <path d="M 30.00 80.00 L 30.31 79.94 L 32.80 79.44 L 37.75 78.48 L 45.11 77.11 L 54.78 75.39 L 66.67 73.43 L 80.64 71.33 L 96.52 69.21 L 114.14 67.19 L 133.31 65.40 L 153.79 63.95 L 175.37 62.93 L 197.79 62.44 L 220.80 62.46 L 244.14 62.77 L 267.55 63.36 L 290.76 64.21 L 313.51 65.32 L 335.54 66.64 L 356.60 68.13 L 376.45 69.74 L 394.87 71.41 L 411.65 73.08 L 426.60 74.69 L 439.54 76.17 L 450.34 77.48 L 458.87 78.55 L 465.03 79.34 L 469.69 79.96 L 470.00 80.00"
                stroke="rgba(171,71,188,0.85)" stroke-width="1.5" fill="none" stroke-dasharray="4 3"/>

          <!-- LE / TE labels -->
          <text x="30" y="72" fill="#ab47bc" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="middle">LE</text>
          <text x="470" y="72" fill="#ab47bc" font-size="11" font-family="Rajdhani,sans-serif">TE</text>

          <!-- Chord annotation -->
          <path d="M30 130 L470 130" stroke="rgba(171,71,188,0.4)" stroke-width="1" marker-end="url(#pa)" marker-start="url(#pb)"/>
          <defs>
            <marker id="pa" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0 0 L6 3 L0 6 Z" fill="#ab47bc"/></marker>
            <marker id="pb" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto-start-reverse"><path d="M0 0 L6 3 L0 6 Z" fill="#ab47bc"/></marker>
          </defs>
          <text x="250" y="145" fill="#ab47bc" font-size="13" font-family="Rajdhani,sans-serif" text-anchor="middle" font-weight="600">CORDA c</text>

          <!-- Thickness t arrow at x=165 (point of max thickness for NACA 4412) -->
          <line x1="165" y1="37" x2="165" y2="89.8" stroke="#ffd54f" stroke-width="1.5" stroke-dasharray="3 2"/>
          <text x="171" y="65" fill="#ffd54f" font-size="12" font-family="Rajdhani,sans-serif" font-style="italic">t</text>

          <!-- Camber f arrow at x=209 (point of max camber: from chord y=80 up to camber line y=62.4) -->
          <line x1="209" y1="80" x2="209" y2="62.4" stroke="#ffa726" stroke-width="1.5" stroke-dasharray="3 2"/>
          <text x="215" y="74" fill="#ffa726" font-size="12" font-family="Rajdhani,sans-serif" font-style="italic">f</text>

          <!-- AoA (angle of attack indication from LE) -->
          <path d="M30 80 L0 92" stroke="#ef5350" stroke-width="1.5"/>
          <text x="2" y="89" fill="#ef5350" font-size="11" font-family="Rajdhani,sans-serif" font-style="italic">α</text>
        </svg>
      </div>

      <div class="modal-section">
        <h3>Nomenclatura NACA</h3>
        <p>La serie <strong>NACA a 4 cifre</strong> (es. NACA 2412) codifica la forma del profilo in modo compatto:</p>
        <div class="formula-box">
          NACA [M][P][SS]
          <span class="label">M = camber max in % della corda · P = posizione camber in decimi di corda · SS = spessore max in % della corda<br>Es. NACA 2412 → 2% camber a 0,4c · spessore 12%</span>
        </div>
        <p>Profili simmetrici (NACA 0012) non generano portanza ad α = 0, ideali per impennaggi e acrobazia. Profili con camber positivo generano portanza anche ad incidenza nulla.</p>
      </div>

      <div class="modal-section">
        <h3>Centro di Pressione e Punto Aerodinamico</h3>
        <div class="formula-box">
          x<sub>PA</sub> ≈ 0,25 · c  (teoria dei profili sottili — profili reali ~ 23-27%)
          <span class="label">Il punto aerodinamico (fuoco) è il punto in cui il momento risultante non varia con α: garantisce stabilità longitudinale.</span>
        </div>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Esempio Pratico — Confronto Profili</div>
        <p>NACA 2412 (aliante leggero): spessore 12%, discreto C<sub>L</sub> max ~1,6.<br>
        NACA 63-415 (aereo da turismo): profilo laminare, bassa resistenza, C<sub>L</sub> max ~1,3 ma volo crociering efficiente.<br>
        NACA 0012 (elicottero, rotore): profilo simmetrico, momento a cerniera nullo.</p>
      </div>
    `
  },

  strumenti: {
    tag: 'Strumentazione di Bordo',
    theme: '#ffa726',
    title: 'Strumenti Barometrici vs Giroscopici',
    html: `
      <div class="modal-section">
        <h3>Strumenti Barometrici</h3>
        <p>Sfruttano la variazione di pressione dell'aria con l'altitudine (legge barometrica) per misurare quota e velocità. I principali sono:</p>
        <div class="table-wrap"><table class="info-table">
          <tr><th>Strumento</th><th>Misura</th><th>Principio</th></tr>
          <tr><td>Altimetro</td><td>Quota pressione [ft/m]</td><td>Capsula aneroide che si espande al diminuire di p</td></tr>
          <tr><td>Anemometro (ASI)</td><td>Velocità indicata IAS [kt]</td><td>Δp = p<sub>tot</sub> − p<sub>st</sub> → ½ρV²</td></tr>
          <tr><td>Variometro (VSI)</td><td>Rateo di salita/discesa [ft/min]</td><td>Flusso d'aria attraverso capillare calibrato</td></tr>
        </table></div>
      </div>

      <!-- SVG altimetro semplificato -->
      <div class="svg-wrap">
        <svg viewBox="0 0 320 160" xmlns="http://www.w3.org/2000/svg">
          <!-- Altimeter dial -->
          <circle cx="80" cy="80" r="65" fill="rgba(255,167,38,0.05)" stroke="#ffa726" stroke-width="1.5"/>
          <circle cx="80" cy="80" r="58" fill="rgba(255,167,38,0.03)" stroke="rgba(255,167,38,0.3)" stroke-width="0.5"/>
          <!-- Tick marks -->
          <g stroke="#ffa726" stroke-width="1.5" opacity="0.7">
            <line x1="80" y1="18" x2="80" y2="28"/>
            <line x1="80" y1="132" x2="80" y2="142"/>
            <line x1="18" y1="80" x2="28" y2="80"/>
            <line x1="132" y1="80" x2="142" y2="80"/>
            <line x1="34" y1="34" x2="41" y2="41"/>
            <line x1="126" y1="34" x2="119" y2="41"/>
            <line x1="34" y1="126" x2="41" y2="119"/>
            <line x1="126" y1="126" x2="119" y2="119"/>
          </g>
          <!-- Hands -->
          <line x1="80" y1="80" x2="80" y2="32" stroke="white" stroke-width="2.5" stroke-linecap="round"/>
          <line x1="80" y1="80" x2="108" y2="60" stroke="#ffa726" stroke-width="1.5" stroke-linecap="round"/>
          <circle cx="80" cy="80" r="4" fill="#ffa726"/>
          <!-- Labels -->
          <text x="80" y="68" fill="#ffa726" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">10</text>
          <text x="80" y="100" fill="#ffa726" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">5</text>
          <text x="58" y="84" fill="#ffa726" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">7,5</text>
          <text x="102" y="84" fill="#ffa726" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">2,5</text>
          <text x="80" y="112" fill="#ffa726" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="middle" font-weight="600">ALTIMETRO</text>

          <!-- Gyro diagram -->
          <circle cx="240" cy="80" r="55" fill="rgba(79,195,247,0.05)" stroke="#4fc3f7" stroke-width="1.5"/>
          <!-- gyro wheel -->
          <ellipse cx="240" cy="80" rx="30" ry="15" fill="rgba(79,195,247,0.12)" stroke="#4fc3f7" stroke-width="1.5"/>
          <ellipse cx="240" cy="80" rx="30" ry="8" fill="none" stroke="rgba(79,195,247,0.4)" stroke-width="0.8"/>
          <!-- gimbal rings -->
          <ellipse cx="240" cy="80" rx="40" ry="20" fill="none" stroke="rgba(79,195,247,0.4)" stroke-width="1"/>
          <ellipse cx="240" cy="80" rx="50" ry="28" fill="none" stroke="rgba(79,195,247,0.25)" stroke-width="1"/>
          <!-- spin arrows -->
          <path d="M218 76 Q228 68 240 70 Q252 68 258 76" stroke="#4fc3f7" stroke-width="1.5" fill="none" stroke-dasharray="3 2" opacity="0.8"/>
          <text x="240" y="118" fill="#4fc3f7" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="middle" font-weight="600">GIROSCOPIO</text>
          <text x="240" y="130" fill="rgba(79,195,247,0.6)" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">Asse nello spazio fisso</text>
        </svg>
      </div>

      <div class="modal-section">
        <h3>Strumenti Giroscopici</h3>
        <p>Si basano sulla <strong>rigidità giroscopica</strong> (l'asse del giroscopio mantiene la direzione nello spazio) e sulla <strong>precessione</strong> (applicando un momento, l'asse ruota perpendicolarmente). I principali:</p>
        <div class="table-wrap"><table class="info-table">
          <tr><th>Strumento</th><th>Misura</th><th>Proprietà usata</th></tr>
          <tr><td>Indicatore d'assetto (ADI/AI)</td><td>Beccheggio e rollio</td><td>Rigidità — asse verticale</td></tr>
          <tr><td>Direttore di rotta (DI/HI)</td><td>Prua magnetica</td><td>Rigidità — asse orizzontale</td></tr>
          <tr><td>Coordinatore di virata (TC)</td><td>Rateo di virata</td><td>Precessione</td></tr>
        </table></div>
      </div>

      <div class="modal-section">
        <h3>Equazione della Precessione Giroscopica</h3>
        <div class="formula-box">
          Ω<sub>prec</sub> = M / (I · ω)
          <span class="label">M = momento applicato [N·m] · I = momento d'inerzia della ruota [kg·m²] · ω = velocità angolare di spin [rad/s]</span>
        </div>
        <p>Maggiore è la velocità di spin ω, minore è la precessione per un dato momento perturbante: principio alla base della stabilità degli strumenti giroscopici.</p>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Errori Strumentali Tipici</div>
        <p><strong>Altimetro:</strong> mostra quota pressione (QNH), non quota vera (QFE locale). In discesa rapida può ritardare la lettura.<br>
        <strong>ADI:</strong> in virate prolungate accumula deriva giroscopica (~3°/min); richiede riallineamento periodico col compasso magnetico.</p>
      </div>
    `
  },

  stallo: {
    tag: 'Meccanica del Volo',
    theme: '#ef5350',
    title: 'Lo Stallo Aerodinamico',
    html: `
      <div class="modal-section">
        <h3>Definizione di Stallo</h3>
        <p>Lo stallo si verifica quando l'<strong>angolo di incidenza α supera il valore critico α<sub>cr</sub></strong> (tipicamente 15–20° per profili convenzionali). A questo punto il flusso non riesce più a seguire il profilo nell'estradosso: si separa, diventa turbolento, e il C<sub>L</sub> cala bruscamente mentre la resistenza cresce.</p>
        <div class="formula-box">
          C<sub>L</sub> = f(α) → massimo a α<sub>cr</sub>, poi crollo
          V<sub>S</sub> = √( 2W / ρ S C<sub>L max</sub> )
          <span class="label">V<sub>S</sub> = velocità di stallo · W = peso aereo [N] · C<sub>L max</sub> = valore massimo del coefficiente di portanza</span>
        </div>
      </div>

      <!-- SVG: CL vs alfa curve + separated flow -->
      <div class="svg-wrap">
        <svg viewBox="0 0 500 200" xmlns="http://www.w3.org/2000/svg">
          <!-- Axes -->
          <line x1="40" y1="170" x2="480" y2="170" stroke="rgba(239,83,80,0.4)" stroke-width="1.5"/>
          <line x1="40" y1="20" x2="40" y2="170" stroke="rgba(239,83,80,0.4)" stroke-width="1.5"/>
          <text x="490" y="173" fill="rgba(239,83,80,0.7)" font-size="12" font-family="Rajdhani,sans-serif">α</text>
          <text x="28" y="18" fill="rgba(239,83,80,0.7)" font-size="12" font-family="Rajdhani,sans-serif">C<tspan font-size="9" dy="3">L</tspan></text>

          <!-- CL curve -->
          <path d="M40 160 Q150 80 300 40 Q360 28 370 32 Q385 40 400 90 Q420 140 450 155"
                stroke="#ef5350" stroke-width="2.5" fill="none"/>

          <!-- Stall point marker -->
          <circle cx="370" cy="32" r="5" fill="#ef5350"/>
          <line x1="370" y1="32" x2="370" y2="170" stroke="rgba(239,83,80,0.3)" stroke-width="1" stroke-dasharray="4 3"/>
          <text x="362" y="185" fill="#ef5350" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="middle">α<tspan font-size="9" dy="2">cr</tspan></text>
          <text x="370" y="24" fill="#ffd54f" font-size="11" font-family="Rajdhani,sans-serif" text-anchor="middle">C<tspan font-size="9" dy="2">L max</tspan></text>

          <!-- Stall label -->
          <text x="410" y="80" fill="#ef5350" font-size="11" font-family="Rajdhani,sans-serif">STALLO</text>
          <path d="M405 83 L395 100" stroke="#ef5350" stroke-width="1.2" marker-end="url(#sa)"/>
          <defs>
            <marker id="sa" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0 0 L6 3 L0 6 Z" fill="#ef5350"/></marker>
          </defs>

          <!-- Separated flow (stalled wing) - background blob -->
          <path d="M60 80 Q100 65 200 72" fill="rgba(239,83,80,0.1)" stroke="none"/>
          <!-- Airfoil stalled: NACA 4415 @ alpha=18° (m=4%, p=40%, t=15%) -->
          <path d="M 346.16 137.66 L 346.30 137.12 L 346.56 136.60 L 346.97 136.12 L 347.51 135.66 L 348.19 135.25 L 348.99 134.86 L 349.93 134.52 L 351.00 134.23 L 352.20 133.98 L 353.51 133.77 L 354.94 133.63 L 356.49 133.54 L 358.14 133.50 L 359.90 133.54 L 361.75 133.64 L 363.68 133.81 L 365.70 134.04 L 367.80 134.36 L 369.96 134.74 L 372.18 135.20 L 374.45 135.74 L 376.76 136.35 L 379.11 137.03 L 381.48 137.78 L 383.88 138.61 L 386.27 139.49 L 388.64 140.42 L 391.01 141.38 L 393.37 142.39 L 395.73 143.42 L 398.07 144.49 L 400.38 145.58 L 402.67 146.69 L 404.93 147.82 L 407.14 148.95 L 409.30 150.09 L 411.42 151.23 L 413.47 152.37 L 415.47 153.50 L 417.39 154.61 L 419.24 155.70 L 421.02 156.77 L 422.71 157.81 L 424.33 158.81 L 425.85 159.78 L 427.28 160.70 L 428.61 161.57 L 429.85 162.40 L 430.99 163.16 L 432.03 163.87 L 432.96 164.51 L 433.79 165.08 L 434.51 165.59 L 435.12 166.02 L 435.62 166.38 L 436.01 166.66 L 436.29 166.86 L 436.46 166.98 L 436.51 167.02 L 436.45 167.00 L 436.25 166.94 L 435.92 166.85 L 435.45 166.73 L 434.86 166.56 L 434.14 166.36 L 433.29 166.13 L 432.33 165.87 L 431.24 165.57 L 430.04 165.24 L 428.72 164.88 L 427.29 164.49 L 425.77 164.07 L 424.14 163.63 L 422.42 163.16 L 420.60 162.67 L 418.71 162.16 L 416.73 161.64 L 414.69 161.09 L 412.57 160.53 L 410.40 159.96 L 408.17 159.37 L 405.90 158.78 L 403.58 158.17 L 401.23 157.56 L 398.85 156.94 L 396.45 156.32 L 394.04 155.70 L 391.62 155.07 L 389.20 154.43 L 386.79 153.80 L 384.39 153.16 L 382.01 152.52 L 379.70 151.89 L 377.43 151.28 L 375.19 150.68 L 373.00 150.09 L 370.86 149.51 L 368.77 148.94 L 366.74 148.37 L 364.78 147.81 L 362.89 147.25 L 361.07 146.69 L 359.34 146.13 L 357.69 145.57 L 356.14 145.01 L 354.68 144.45 L 353.32 143.89 L 352.06 143.33 L 350.92 142.76 L 349.89 142.19 L 348.98 141.63 L 348.19 141.06 L 347.53 140.49 L 346.99 139.92 L 346.58 139.35 L 346.31 138.79 L 346.17 138.22 L 346.16 137.66 Z"
                fill="rgba(239,83,80,0.18)" stroke="#ef5350" stroke-width="1.8" stroke-linejoin="round"/>
          <!-- Separation streamline arriving at LE upper -->
          <path d="M320 132 Q335 130 348 132" stroke="#ef5350" stroke-width="1.2" fill="none" opacity="0.7"/>
          <!-- Turbulent wake vortices over the separated upper surface -->
          <path d="M362 128 q 5 -6 10 0 q 5 6 10 0" stroke="#ef5350" stroke-width="1.2" fill="none" opacity="0.85"/>
          <path d="M387 124 q 5 -6 10 0 q 5 6 10 0" stroke="#ef5350" stroke-width="1.2" fill="none" opacity="0.7"/>
          <path d="M412 120 q 5 -6 10 0 q 5 6 10 0" stroke="#ef5350" stroke-width="1.2" fill="none" opacity="0.55"/>
          <!-- Trailing wake -->
          <path d="M440 168 Q452 162 462 168 Q472 160 482 166" stroke="#ef5350" stroke-width="1" fill="none" opacity="0.5" stroke-dasharray="2 2"/>
        </svg>
      </div>

      <div class="modal-section">
        <h3>Fattore di Carico e Stallo in Virata</h3>
        <p>In una virata con angolo di bank φ, il fattore di carico aumenta: <strong>n = 1/cos(φ)</strong>. Questo richiede un C<sub>L</sub> maggiore per mantenere quota, quindi lo stallo avviene a velocità più alta:</p>
        <div class="formula-box">
          V<sub>S,virata</sub> = V<sub>S,livello</sub> · √n = V<sub>S</sub> · √(1/cos φ)
          <span class="label">Bank 60° → n = 2 → V<sub>S</sub> aumenta del 41% rispetto al volo livellato</span>
        </div>
      </div>

      <div class="modal-section">
        <h3>Indicatori e Prevenzione</h3>
        <p>Il <strong>segnalatore di stallo</strong> è un foro nel bordo d'attacco collegato a una palette: quando α si avvicina ad α<sub>cr</sub>, l'aria investe la palette e genera un segnale acustico/elettrico. Lo <strong>stick shaker</strong> (aerei di linea) fa vibrare il volantino meccanicamente per avvertire il pilota.</p>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Esempio — Stallo in Avvicinamento</div>
        <p>Un Cessna 172 pesa 1.100 kg, V<sub>S0</sub> (flap estesi) = 44 kt.<br>
        In finale con virata a 30° di bank: n = 1/cos30° = 1,155 → V<sub>S,virata</sub> = 44 × √1,155 ≈ <strong>47 kt</strong>.<br>
        Volare a meno di 47 kt in quella virata causa stallo: motivo per cui le basse virate in corto finale sono pericolose.</p>
      </div>
    `
  },

  pitot: {
    tag: 'Sensori Esterni',
    theme: '#66bb6a',
    title: 'Impianto Pitot-Statico',
    html: `
      <div class="modal-section">
        <h3>Architettura del Sistema</h3>
        <p>L'impianto Pitot-Statico è il sistema di misura delle pressioni che alimenta altimetro, anemometro e variometro. È composto da due tipi di prese:</p>
        <div class="table-wrap"><table class="info-table">
          <tr><th>Presa</th><th>Misura</th><th>Posizione</th></tr>
          <tr><td>Tubo di Pitot</td><td>Pressione totale p<sub>tot</sub> = p<sub>st</sub> + p<sub>din</sub></td><td>Bordo d'attacco, perpendicolare al flusso</td></tr>
          <tr><td>Prese statiche</td><td>Pressione statica p<sub>st</sub></td><td>Fiancate fusoliera (flusso tangente)</td></tr>
        </table></div>
      </div>

      <!-- SVG: sistema pitot-statico -->
      <div class="svg-wrap">
        <svg viewBox="0 0 500 180" xmlns="http://www.w3.org/2000/svg">
          <!-- Fuselage outline -->
          <path d="M30 80 Q60 60 180 55 Q300 50 480 70 L480 90 Q300 105 180 100 Q60 98 30 80Z"
                fill="rgba(102,187,106,0.08)" stroke="#66bb6a" stroke-width="1.5"/>

          <!-- Pitot tube -->
          <rect x="160" y="46" width="40" height="8" rx="3" fill="rgba(102,187,106,0.3)" stroke="#66bb6a" stroke-width="1.5"/>
          <path d="M200 50 L210 50" stroke="#66bb6a" stroke-width="2" stroke-linecap="round"/>
          <text x="172" y="42" fill="#66bb6a" font-size="10" font-family="Rajdhani,sans-serif" text-anchor="middle">Tubo di Pitot</text>

          <!-- Static port -->
          <circle cx="120" cy="77" r="5" fill="rgba(102,187,106,0.3)" stroke="#66bb6a" stroke-width="1.5"/>
          <text x="120" y="70" fill="#66bb6a" font-size="10" font-family="Rajdhani,sans-serif" text-anchor="middle">Presa Statica</text>

          <!-- Lines to instruments -->
          <path d="M180 54 L180 140 L320 140" stroke="#66bb6a" stroke-width="1.2" stroke-dasharray="4 3" fill="none" opacity="0.6"/>
          <path d="M120 82 L120 155 L320 155" stroke="#ffa726" stroke-width="1.2" stroke-dasharray="4 3" fill="none" opacity="0.6"/>

          <!-- Airspeed indicator (difference) -->
          <rect x="320" y="125" width="60" height="36" rx="6" fill="rgba(79,195,247,0.07)" stroke="#4fc3f7" stroke-width="1"/>
          <text x="350" y="140" fill="#4fc3f7" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">ASI</text>
          <text x="350" y="153" fill="rgba(79,195,247,0.6)" font-size="8" font-family="Rajdhani,sans-serif" text-anchor="middle">p<tspan font-size="7" dy="1">tot</tspan> − p<tspan font-size="7" dy="1">st</tspan></text>

          <!-- Altimeter (static only) -->
          <rect x="395" y="140" width="55" height="28" rx="6" fill="rgba(255,167,38,0.07)" stroke="#ffa726" stroke-width="1"/>
          <text x="422" y="153" fill="#ffa726" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle">ALT</text>
          <path d="M375 143 L393 149" stroke="rgba(255,167,38,0.5)" stroke-width="1" stroke-dasharray="2 2"/>

          <!-- Air flow arrow -->
          <path d="M5 80 L25 80" stroke="#66bb6a" stroke-width="2" marker-end="url(#ga)"/>
          <defs>
            <marker id="ga" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0 0 L6 3 L0 6 Z" fill="#66bb6a"/></marker>
          </defs>
          <text x="5" y="73" fill="#66bb6a" font-size="10" font-family="Rajdhani,sans-serif">V∞</text>
        </svg>
      </div>

      <div class="modal-section">
        <h3>Formula dell'Anemometro</h3>
        <p>L'anemometro misura la <strong>pressione dinamica</strong> (differenza tra pressione totale e statica) e la converte in velocità indicata (IAS):</p>
        <div class="formula-box">
          q = p<sub>tot</sub> − p<sub>st</sub> = ½ · ρ<sub>0</sub> · V<sub>IAS</sub>²
          <span class="label">ρ<sub>0</sub> = 1,225 kg/m³ (ISA SL) · Lo strumento è tarato con densità standard, quindi mostra IAS, non TAS</span>
        </div>
        <div class="formula-box">
          TAS = IAS · √(ρ<sub>0</sub> / ρ<sub>quota</sub>)  ≈  IAS · (1 + 2% ogni 1000 ft)
          <span class="label">A FL350: ρ ≈ 0,38 kg/m³ → TAS ≈ IAS × 1,80 (80% più veloce dell'indicata!)</span>
        </div>
      </div>

      <div class="modal-section">
        <h3>Problemi e Ridondanza</h3>
        <p>Il ghiaccio che ottura il tubo di Pitot è causa di numerosi incidenti (vd. Air France AF447). Per questo le prese sono riscaldate elettricamente. Nei velivoli certificati sono richieste <strong>almeno due prese statiche indipendenti</strong> su lati opposti della fusoliera per compensare le asimmetrie di flusso in virata.</p>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Esempio — Boeing 737 a FL350</div>
        <p>IAS = 280 kt · Densità a FL350 ≈ 0,38 kg/m³<br>
        TAS = 280 × √(1,225/0,38) = 280 × 1,795 ≈ <strong>502 kt</strong> (Mach ≈ 0,82).<br>
        Il Mach-metro usa la stessa differenza di pressione ma con la formula comprimibile per regimi transonici.</p>
      </div>
    `
  },

  codici: {
    tag: 'Sicurezza del Volo',
    theme: '#ef5350',
    title: 'Codici Colore e Limiti di Velocità',
    html: `
      <div class="modal-section">
        <h3>L'Anemometro a Codice Colore</h3>
        <p>Per la certificazione FAR/CS-23 e CS-25, l'anemometro deve riportare archi colorati che indicano i regimi operativi e i limiti strutturali dell'aeromobile:</p>
        <div class="table-wrap"><table class="info-table">
          <tr><th>Colore</th><th>Range</th><th>Significato</th></tr>
          <tr><td style="color:#ef5350">Linea Rossa VNE</td><td>Limite superiore</td><td>Never Exceed Speed — limite strutturale assoluto</td></tr>
          <tr><td style="color:#ffa726">Arco Giallo</td><td>V<sub>NO</sub> → V<sub>NE</sub></td><td>Cautela — solo in aria calma e liscia</td></tr>
          <tr><td style="color:#66bb6a">Arco Verde</td><td>V<sub>S1</sub> → V<sub>NO</sub></td><td>Normal Operating Range — operatività normale</td></tr>
          <tr><td style="color:#4fc3f7">Arco Bianco</td><td>V<sub>S0</sub> → V<sub>FE</sub></td><td>Flap Operating Range — flap estendibili</td></tr>
        </table></div>
      </div>

      <!-- SVG: anemometro con archi colorati -->
      <div class="svg-wrap">
        <svg viewBox="0 0 280 280" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <filter id="glow">
              <feGaussianBlur stdDeviation="3" result="blur"/>
              <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
            </filter>
          </defs>
          <!-- Outer ring -->
          <circle cx="140" cy="140" r="125" fill="rgba(10,22,40,0.9)" stroke="rgba(255,255,255,0.1)" stroke-width="2"/>
          <circle cx="140" cy="140" r="118" fill="none" stroke="rgba(255,255,255,0.05)" stroke-width="1"/>

          <!-- Background arc (gray) -->
          <path d="M 30 200 A 115 115 0 1 1 250 200" stroke="#333" stroke-width="18" fill="none" stroke-linecap="round"/>

          <!-- White arc (V_S0 to V_FE): ~40–85 kt mapped to 210°–290° on dial -->
          <path d="M 30 200 A 115 115 0 0 1 62 75" stroke="#ddd" stroke-width="18" fill="none" stroke-linecap="round" opacity="0.9"/>

          <!-- Green arc (V_S1 to V_NO): ~50–140 kt, larger section -->
          <path d="M 42 154 A 115 115 0 0 1 220 58" stroke="#66bb6a" stroke-width="18" fill="none" filter="url(#glow)"/>

          <!-- Yellow arc (V_NO to V_NE): cautionary range -->
          <path d="M 220 58 A 115 115 0 0 1 248 165" stroke="#ffa726" stroke-width="18" fill="none" filter="url(#glow)"/>

          <!-- Red line (V_NE) -->
          <path d="M 248 165 A 115 115 0 0 1 250 200" stroke="#ef5350" stroke-width="18" fill="none" filter="url(#glow)"/>

          <!-- Tick marks and numbers -->
          <g fill="#ccc" font-family="Rajdhani,sans-serif" font-size="13" font-weight="600">
            <text x="124" y="35" text-anchor="middle">200</text>
            <text x="36" y="100" text-anchor="middle">60</text>
            <text x="20" y="190" text-anchor="middle">40</text>
            <text x="238" y="100" text-anchor="end">160</text>
            <text x="254" y="190" text-anchor="end">180</text>
          </g>

          <!-- Needle -->
          <line x1="140" y1="140" x2="185" y2="62" stroke="white" stroke-width="3" stroke-linecap="round"/>
          <circle cx="140" cy="140" r="8" fill="#666" stroke="white" stroke-width="2"/>
          <circle cx="140" cy="140" r="3" fill="white"/>

          <!-- Center label -->
          <text x="140" y="195" fill="#aaa" font-size="10" font-family="Rajdhani,sans-serif" text-anchor="middle" letter-spacing="2">AIRSPEED</text>
          <text x="140" y="208" fill="#aaa" font-size="9" font-family="Rajdhani,sans-serif" text-anchor="middle" letter-spacing="1">KNOTS</text>

          <!-- Legend -->
          <rect x="10" y="235" width="12" height="8" rx="2" fill="#66bb6a"/>
          <text x="26" y="243" fill="#aaa" font-size="10" font-family="Rajdhani,sans-serif">Op. Normale</text>
          <rect x="110" y="235" width="12" height="8" rx="2" fill="#ffa726"/>
          <text x="126" y="243" fill="#aaa" font-size="10" font-family="Rajdhani,sans-serif">Cautela</text>
          <rect x="190" y="235" width="12" height="8" rx="2" fill="#ef5350"/>
          <text x="206" y="243" fill="#aaa" font-size="10" font-family="Rajdhani,sans-serif">Limite V<tspan font-size="8" dy="1">NE</tspan></text>
        </svg>
      </div>

      <div class="modal-section">
        <h3>Definizioni EASA/FAA dei Limiti</h3>
        <div class="formula-box">
          V<sub>S0</sub> = stallo flap estesi (atterraggio)
          V<sub>S1</sub> = stallo flap retratti (crociera)
          V<sub>A</sub>  = manovra — limite per piena deflessione comandi
          V<sub>NO</sub> = max velocità operativa normale
          V<sub>NE</sub> = Never Exceed (VNE = 0,9 · V<sub>D</sub> in CS-23)
          <span class="label">V<sub>D</sub> = velocità di progetto in picchiata · V<sub>A</sub> non è segnata sull'ASI, riportata nel manuale (POH/AFM)</span>
        </div>
      </div>

      <div class="modal-section">
        <h3>V<sub>A</sub> e il Limite di Manovra</h3>
        <p>La velocità di manovra V<sub>A</sub> garantisce che se un comando viene portato al pieno arresto, l'ala va in stallo prima che le strutture cedano. La relazione è:</p>
        <div class="formula-box">
          V<sub>A</sub> = V<sub>S</sub> · √n<sub>lim</sub>
          <span class="label">n<sub>lim</sub> = fattore di carico limite di progetto (es. +3,8g per Utility, +2,5g per Normal category CS-23)</span>
        </div>
      </div>

      <div class="example-box">
        <div class="ex-title">✈ Esempio — Cessna 172S (KIAS)</div>
        <p>V<sub>S0</sub> = 44 kt · V<sub>S1</sub> = 48 kt · V<sub>FE</sub> = 85 kt (arco bianco)<br>
        V<sub>NO</sub> = 129 kt (limite arco verde) · V<sub>NE</sub> = 163 kt (linea rossa)<br>
        V<sub>A</sub> = 105 kt @ MTOW (non sull'ASI — solo nel POH).<br>
        Volare nell'arco giallo (>129 kt) in turbolenza può generare carichi imprevisti sulle superfici di controllo.</p>
      </div>
    `
  }

};

// ── Intersection Observer for scroll reveal ──
const cards = document.querySelectorAll('.card');
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry, i) => {
    if (entry.isIntersecting) {
      entry.target.style.animationDelay = (Array.from(cards).indexOf(entry.target) * 0.1) + 's';
      entry.target.classList.add('visible');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });
cards.forEach(c => observer.observe(c));

// ── Modal open ──
const overlay = document.getElementById('modalOverlay');
const modalContent = document.getElementById('modalContent');
const modalClose = document.getElementById('modalClose');

function openModalFor(card) {
  const key = card.dataset.modal;
  const data = MODALS[key];
  if (!data) return;

  const themeColor = data.theme || '#4fc3f7';

  modalContent.innerHTML = `
    <div class="modal-tag" style="background:rgba(255,255,255,0.07);color:${themeColor}">${data.tag}</div>
    <h2 style="color:${themeColor}">${data.title}</h2>
    ${data.html}
  `;

  document.getElementById('modalBox').style.setProperty('--t', themeColor);
  overlay.classList.add('open');
  document.body.style.overflow = 'hidden';
  // Reset scroll position to top of modal each time
  overlay.scrollTop = 0;
}

cards.forEach(card => {
  // Accessibility: make cards keyboard-focusable
  card.setAttribute('tabindex', '0');
  card.setAttribute('role', 'button');

  card.addEventListener('click', () => openModalFor(card));
  card.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      openModalFor(card);
    }
  });
});

// ── Modal close ──
function closeModal() {
  overlay.classList.remove('open');
  document.body.style.overflow = '';
}

modalClose.addEventListener('click', closeModal);
overlay.addEventListener('click', (e) => {
  if (e.target === overlay) closeModal();
});
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') closeModal();
});
</script>
</body>
</html>
