<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Elias Gourai — Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Sans:wght@300;400;500&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* ─── RESET & TOKENS ─────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #0a0a0f;
      --bg2:       #111118;
      --bg3:       #1a1a25;
      --card:      #14141e;
      --border:    rgba(255,255,255,0.07);
      --accent:    #c8a96e;
      --accent2:   #7c6ff7;
      --accent3:   #4ecdc4;
      --text:      #e8e6e0;
      --muted:     #888;
      --heading:   #f5f2eb;
      --ff-display: 'Playfair Display', Georgia, serif;
      --ff-body:   'DM Sans', sans-serif;
      --ff-mono:   'JetBrains Mono', monospace;
      --radius:    12px;
      --transition: 0.35s cubic-bezier(.4,0,.2,1);
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--ff-body);
      font-size: 15px;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* ─── NOISE OVERLAY ──────────────────────────────── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9999;
      opacity: 0.35;
    }

    /* ─── SCROLLBAR ───────────────────────────────────── */
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

    /* ─── NAV ─────────────────────────────────────────── */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 1000;
      display: flex; align-items: center; justify-content: space-between;
      padding: 18px 48px;
      backdrop-filter: blur(20px);
      background: rgba(10,10,15,0.85);
      border-bottom: 1px solid var(--border);
      transition: padding var(--transition);
    }
    nav.scrolled { padding: 12px 48px; }

    .nav-logo {
      font-family: var(--ff-display);
      font-size: 1.25rem;
      font-weight: 700;
      color: var(--accent);
      text-decoration: none;
      letter-spacing: 0.02em;
    }

    .nav-links {
      display: flex; gap: 36px; list-style: none;
    }
    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.82rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      transition: color var(--transition);
      position: relative;
    }
    .nav-links a::after {
      content: '';
      position: absolute; bottom: -3px; left: 0; right: 0;
      height: 1px; background: var(--accent);
      transform: scaleX(0); transform-origin: right;
      transition: transform var(--transition);
    }
    .nav-links a:hover { color: var(--accent); }
    .nav-links a:hover::after { transform: scaleX(1); transform-origin: left; }

    .nav-burger {
      display: none; flex-direction: column; gap: 5px;
      background: none; border: none; cursor: pointer; padding: 4px;
    }
    .nav-burger span {
      display: block; width: 24px; height: 2px;
      background: var(--text); border-radius: 2px;
      transition: var(--transition);
    }

    /* ─── HERO ────────────────────────────────────────── */
    #hero {
      min-height: 100vh;
      display: flex; align-items: center;
      padding: 120px 48px 80px;
      position: relative;
      overflow: hidden;
    }

    .hero-bg {
      position: absolute; inset: 0;
      background:
        radial-gradient(ellipse 70% 50% at 60% 50%, rgba(124,111,247,0.08) 0%, transparent 70%),
        radial-gradient(ellipse 40% 40% at 20% 80%, rgba(200,169,110,0.06) 0%, transparent 60%),
        radial-gradient(ellipse 50% 60% at 80% 20%, rgba(78,205,196,0.05) 0%, transparent 60%);
      pointer-events: none;
    }

    .hero-grid {
      position: absolute; inset: 0;
      background-image:
        linear-gradient(var(--border) 1px, transparent 1px),
        linear-gradient(90deg, var(--border) 1px, transparent 1px);
      background-size: 60px 60px;
      mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 30%, transparent 100%);
      pointer-events: none;
    }

    .hero-content {
      position: relative; z-index: 1;
      max-width: 800px;
    }

    .hero-tag {
      display: inline-flex; align-items: center; gap: 8px;
      font-family: var(--ff-mono); font-size: 0.75rem;
      color: var(--accent); letter-spacing: 0.15em;
      text-transform: uppercase;
      border: 1px solid rgba(200,169,110,0.25);
      padding: 6px 14px; border-radius: 100px;
      margin-bottom: 32px;
      animation: fadeUp 0.8s ease both;
    }
    .hero-tag::before {
      content: '';
      width: 6px; height: 6px; border-radius: 50%;
      background: var(--accent);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }

    .hero-name {
      font-family: var(--ff-display);
      font-size: clamp(3.5rem, 8vw, 7rem);
      font-weight: 900;
      line-height: 1.0;
      color: var(--heading);
      letter-spacing: -0.02em;
      animation: fadeUp 0.8s 0.1s ease both;
    }
    .hero-name em {
      font-style: italic;
      color: var(--accent);
    }

    .hero-sub {
      margin-top: 20px;
      font-size: 1.1rem;
      color: var(--muted);
      max-width: 500px;
      animation: fadeUp 0.8s 0.2s ease both;
    }

    .hero-cta {
      margin-top: 40px;
      display: flex; gap: 16px; flex-wrap: wrap;
      animation: fadeUp 0.8s 0.3s ease both;
    }

    .btn {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 12px 28px; border-radius: 8px;
      font-size: 0.875rem; font-weight: 500;
      text-decoration: none; cursor: pointer; border: none;
      transition: all var(--transition);
    }
    .btn-primary {
      background: var(--accent); color: #0a0a0f;
    }
    .btn-primary:hover { background: #d4bb7e; transform: translateY(-2px); box-shadow: 0 8px 24px rgba(200,169,110,0.3); }

    .btn-outline {
      background: transparent;
      border: 1px solid var(--border);
      color: var(--text);
    }
    .btn-outline:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

    .hero-scroll {
      position: absolute; bottom: 40px; left: 50%;
      transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center;
      gap: 8px; color: var(--muted); font-size: 0.75rem;
      letter-spacing: 0.1em; text-transform: uppercase;
      animation: fadeUp 0.8s 0.6s ease both;
    }
    .scroll-line {
      width: 1px; height: 50px;
      background: linear-gradient(var(--accent), transparent);
      animation: scrollLine 1.5s ease-in-out infinite;
    }
    @keyframes scrollLine {
      0%, 100% { transform: scaleY(0); transform-origin: top; }
      50% { transform: scaleY(1); transform-origin: top; }
      51% { transform: scaleY(1); transform-origin: bottom; }
      100% { transform: scaleY(0); transform-origin: bottom; }
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ─── SECTION BASE ────────────────────────────────── */
    section {
      padding: 100px 48px;
    }

    .section-header {
      margin-bottom: 60px;
    }
    .section-label {
      font-family: var(--ff-mono); font-size: 0.72rem;
      color: var(--accent); letter-spacing: 0.2em;
      text-transform: uppercase; margin-bottom: 12px;
    }
    .section-title {
      font-family: var(--ff-display); font-size: clamp(2rem, 4vw, 3rem);
      font-weight: 700; color: var(--heading); line-height: 1.15;
    }
    .section-line {
      width: 48px; height: 2px; background: var(--accent);
      margin-top: 16px;
    }

    .container {
      max-width: 1200px; margin: 0 auto;
    }

    /* ─── PRÉSENTATION ────────────────────────────────── */
    #presentation {
      background: var(--bg2);
    }

    .pres-layout {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 80px; align-items: center;
    }

    .pres-avatar {
      position: relative;
    }
    .pres-avatar-frame {
      width: 100%; max-width: 380px;
      aspect-ratio: 3/4;
      border-radius: 16px;
      background: var(--bg3);
      border: 1px solid var(--border);
      overflow: hidden;
      position: relative;
    }
    .pres-avatar-frame::before {
      content: 'EG';
      position: absolute; inset: 0;
      display: flex; align-items: center; justify-content: center;
      font-family: var(--ff-display); font-size: 5rem;
      font-weight: 900; color: var(--border);
      letter-spacing: -0.05em;
    }
    .avatar-deco {
      position: absolute; top: -16px; right: -16px;
      width: 80px; height: 80px;
      border: 2px solid var(--accent);
      border-radius: 50%; opacity: 0.4;
    }
    .avatar-deco2 {
      position: absolute; bottom: -20px; left: -20px;
      width: 120px; height: 120px;
      border: 1px solid var(--accent2);
      border-radius: 50%; opacity: 0.2;
    }

    .pres-text p {
      color: var(--muted); margin-bottom: 20px; line-height: 1.9;
    }

    .pres-stats {
      display: grid; grid-template-columns: 1fr 1fr 1fr;
      gap: 20px; margin-top: 36px;
    }
    .stat-card {
      background: var(--bg3); border: 1px solid var(--border);
      border-radius: var(--radius); padding: 20px 16px; text-align: center;
      transition: border-color var(--transition), transform var(--transition);
    }
    .stat-card:hover { border-color: var(--accent); transform: translateY(-3px); }
    .stat-num {
      font-family: var(--ff-display); font-size: 2rem;
      font-weight: 900; color: var(--accent);
    }
    .stat-label {
      font-size: 0.75rem; color: var(--muted);
      text-transform: uppercase; letter-spacing: 0.1em;
      margin-top: 4px;
    }

    /* ─── CV & LETTRE ─────────────────────────────────── */
    #documents {
      background: var(--bg);
    }
    .docs-grid {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 32px;
    }
    .doc-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px; padding: 40px;
      text-decoration: none; color: inherit;
      display: flex; align-items: flex-start; gap: 24px;
      transition: all var(--transition);
      position: relative; overflow: hidden;
    }
    .doc-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, var(--accent), transparent);
      transform: scaleX(0); transform-origin: left;
      transition: transform var(--transition);
    }
    .doc-card:hover { border-color: rgba(200,169,110,0.3); transform: translateY(-4px); box-shadow: 0 20px 40px rgba(0,0,0,0.3); }
    .doc-card:hover::before { transform: scaleX(1); }

    .doc-icon {
      width: 56px; height: 56px; border-radius: 12px;
      background: var(--bg3); border: 1px solid var(--border);
      display: flex; align-items: center; justify-content: center;
      font-size: 1.5rem; flex-shrink: 0;
      transition: background var(--transition);
    }
    .doc-card:hover .doc-icon { background: rgba(200,169,110,0.1); }

    .doc-info h3 {
      font-family: var(--ff-display); font-size: 1.2rem;
      color: var(--heading); margin-bottom: 6px;
    }
    .doc-info p { color: var(--muted); font-size: 0.875rem; margin: 0; }
    .doc-badge {
      display: inline-block; margin-top: 12px;
      font-family: var(--ff-mono); font-size: 0.7rem;
      color: var(--accent); letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    /* ─── COMPÉTENCES ─────────────────────────────────── */
    #competences {
      background: var(--bg2);
    }

    .comp-grid {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 24px;
    }

    .comp-card {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 16px; overflow: hidden;
      transition: border-color var(--transition);
    }
    .comp-card:hover { border-color: rgba(200,169,110,0.2); }

    .comp-header {
      padding: 24px 28px;
      display: flex; align-items: center; gap: 16px;
      cursor: pointer; user-select: none;
      transition: background var(--transition);
    }
    .comp-header:hover { background: rgba(255,255,255,0.02); }

    .comp-num {
      font-family: var(--ff-mono); font-size: 0.75rem;
      color: var(--accent); letter-spacing: 0.1em;
      background: rgba(200,169,110,0.1); border: 1px solid rgba(200,169,110,0.2);
      padding: 4px 10px; border-radius: 100px;
      flex-shrink: 0;
    }
    .comp-title {
      font-family: var(--ff-display); font-size: 1rem;
      font-weight: 700; color: var(--heading); flex: 1;
      line-height: 1.3;
    }
    .comp-arrow {
      color: var(--muted); transition: transform var(--transition);
      font-size: 1rem;
    }
    .comp-card.open .comp-arrow { transform: rotate(180deg); }

    .comp-body {
      max-height: 0; overflow: hidden;
      transition: max-height 0.4s cubic-bezier(.4,0,.2,1);
    }
    .comp-card.open .comp-body { max-height: 600px; }

    .comp-content {
      padding: 0 28px 24px;
      border-top: 1px solid var(--border);
      padding-top: 20px;
    }
    .comp-content p {
      color: var(--muted); font-size: 0.875rem; margin-bottom: 16px;
    }
    .ac-list {
      list-style: none; display: flex; flex-direction: column; gap: 10px;
    }
    .ac-item {
      display: flex; align-items: flex-start; gap: 12px;
      background: var(--bg3); border-radius: 8px; padding: 12px 14px;
      border: 1px solid var(--border);
    }
    .ac-dot {
      width: 6px; height: 6px; border-radius: 50%;
      background: var(--accent); margin-top: 7px; flex-shrink: 0;
    }
    .ac-text {
      font-size: 0.82rem; color: var(--text); line-height: 1.6;
    }
    .ac-level {
      font-family: var(--ff-mono); font-size: 0.68rem;
      color: var(--accent2); margin-top: 3px;
    }

    /* COLOR VARIANTS */
    .comp-card:nth-child(1) .comp-num { color: var(--accent); background: rgba(200,169,110,0.1); border-color: rgba(200,169,110,0.2); }
    .comp-card:nth-child(2) .comp-num { color: var(--accent2); background: rgba(124,111,247,0.1); border-color: rgba(124,111,247,0.2); }
    .comp-card:nth-child(2) .ac-dot { background: var(--accent2); }
    .comp-card:nth-child(2) .section-line { background: var(--accent2); }
    .comp-card:nth-child(3) .comp-num { color: var(--accent3); background: rgba(78,205,196,0.1); border-color: rgba(78,205,196,0.2); }
    .comp-card:nth-child(3) .ac-dot { background: var(--accent3); }
    .comp-card:nth-child(4) .comp-num { color: #f07167; background: rgba(240,113,103,0.1); border-color: rgba(240,113,103,0.2); }
    .comp-card:nth-child(4) .ac-dot { background: #f07167; }

    /* ─── SAE ─────────────────────────────────────────── */
    #sae {
      background: var(--bg);
    }

    .sae-filters {
      display: flex; gap: 10px; flex-wrap: wrap; margin-bottom: 40px;
    }
    .filter-btn {
      padding: 8px 18px; border-radius: 100px;
      border: 1px solid var(--border);
      background: transparent; color: var(--muted);
      font-size: 0.78rem; font-family: var(--ff-body);
      cursor: pointer; transition: all var(--transition);
      letter-spacing: 0.05em;
    }
    .filter-btn.active, .filter-btn:hover {
      border-color: var(--accent); color: var(--accent);
      background: rgba(200,169,110,0.08);
    }

    .sae-grid {
      display: grid; grid-template-columns: repeat(3, 1fr);
      gap: 20px;
    }

    .sae-card {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 16px; overflow: hidden;
      cursor: pointer; transition: all var(--transition);
      position: relative;
    }
    .sae-card:hover {
      border-color: rgba(200,169,110,0.25);
      transform: translateY(-4px);
      box-shadow: 0 16px 40px rgba(0,0,0,0.3);
    }

    .sae-thumb {
      height: 120px;
      position: relative; overflow: hidden;
      background: var(--bg3);
    }
    .sae-thumb-inner {
      position: absolute; inset: 0;
      display: flex; align-items: center; justify-content: center;
      font-family: var(--ff-display); font-size: 3rem;
      font-weight: 900; opacity: 0.15;
    }
    .sae-thumb-gradient {
      position: absolute; bottom: 0; left: 0; right: 0; height: 40px;
      background: linear-gradient(transparent, var(--card));
    }

    .sae-body { padding: 20px; }
    .sae-code {
      font-family: var(--ff-mono); font-size: 0.68rem;
      color: var(--accent); letter-spacing: 0.1em;
      text-transform: uppercase; margin-bottom: 8px;
    }
    .sae-title {
      font-family: var(--ff-display); font-size: 1rem;
      font-weight: 700; color: var(--heading);
      line-height: 1.3; margin-bottom: 12px;
    }
    .sae-tags {
      display: flex; flex-wrap: wrap; gap: 6px;
    }
    .tag {
      font-size: 0.7rem; padding: 3px 8px; border-radius: 100px;
      border: 1px solid var(--border); color: var(--muted);
    }
    .sae-card:hover .tag { border-color: rgba(200,169,110,0.2); }

    /* ─── SAE MODAL ───────────────────────────────────── */
    .modal-overlay {
      position: fixed; inset: 0; z-index: 2000;
      background: rgba(0,0,0,0.85);
      backdrop-filter: blur(8px);
      display: flex; align-items: flex-start; justify-content: center;
      padding: 40px 20px; overflow-y: auto;
      opacity: 0; pointer-events: none;
      transition: opacity 0.3s ease;
    }
    .modal-overlay.open { opacity: 1; pointer-events: all; }

    .modal {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 20px; width: 100%; max-width: 820px;
      position: relative; overflow: hidden;
      transform: translateY(30px);
      transition: transform 0.3s ease;
    }
    .modal-overlay.open .modal { transform: translateY(0); }

    .modal-header {
      padding: 40px 40px 28px;
      border-bottom: 1px solid var(--border);
      position: relative;
    }
    .modal-header-bg {
      position: absolute; top: 0; left: 0; right: 0; height: 3px;
      background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent3));
    }
    .modal-code {
      font-family: var(--ff-mono); font-size: 0.72rem;
      color: var(--accent); letter-spacing: 0.15em;
      text-transform: uppercase; margin-bottom: 8px;
    }
    .modal-title {
      font-family: var(--ff-display); font-size: 1.8rem;
      font-weight: 700; color: var(--heading);
      line-height: 1.2;
    }

    .modal-close {
      position: absolute; top: 20px; right: 20px;
      width: 36px; height: 36px; border-radius: 50%;
      background: var(--bg3); border: 1px solid var(--border);
      color: var(--muted); cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      font-size: 1rem; transition: all var(--transition);
    }
    .modal-close:hover { background: var(--accent); color: #0a0a0f; border-color: var(--accent); }

    .modal-body {
      padding: 32px 40px;
      max-height: calc(100vh - 200px);
      overflow-y: auto;
    }

    .modal-section {
      margin-bottom: 32px;
    }
    .modal-section-title {
      font-family: var(--ff-display); font-size: 1.1rem;
      font-weight: 700; color: var(--heading);
      margin-bottom: 12px;
      display: flex; align-items: center; gap: 10px;
    }
    .modal-section-title::before {
      content: '';
      width: 20px; height: 2px; background: var(--accent); flex-shrink: 0;
    }
    .modal-section p, .modal-section li {
      color: var(--muted); font-size: 0.875rem; line-height: 1.8;
    }
    .modal-section ul, .modal-section ol {
      padding-left: 20px; display: flex; flex-direction: column; gap: 6px;
    }

    .modal-images {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 12px; margin-top: 12px;
    }
    .modal-img-wrap {
      border-radius: 10px; overflow: hidden;
      border: 1px solid var(--border);
      background: var(--bg3); cursor: zoom-in;
      transition: border-color var(--transition);
      aspect-ratio: 16/9;
    }
    .modal-img-wrap:only-child { grid-column: 1 / -1; }
    .modal-img-wrap img {
      width: 100%; height: 100%; object-fit: cover;
      transition: transform 0.5s ease;
    }
    .modal-img-wrap:hover { border-color: var(--accent); }
    .modal-img-wrap:hover img { transform: scale(1.04); }

    .modal-ac {
      background: var(--bg3); border-radius: 12px;
      padding: 20px 24px; border: 1px solid var(--border);
    }
    .modal-ac h4 {
      font-family: var(--ff-mono); font-size: 0.72rem;
      color: var(--accent); letter-spacing: 0.15em;
      text-transform: uppercase; margin-bottom: 14px;
    }
    .ac-badges {
      display: flex; flex-wrap: wrap; gap: 8px;
    }
    .ac-badge {
      padding: 5px 12px; border-radius: 100px;
      font-size: 0.72rem; font-weight: 500;
      border: 1px solid;
    }
    .ac-badge.c1 { color: var(--accent); border-color: rgba(200,169,110,0.3); background: rgba(200,169,110,0.08); }
    .ac-badge.c2 { color: var(--accent2); border-color: rgba(124,111,247,0.3); background: rgba(124,111,247,0.08); }
    .ac-badge.c3 { color: var(--accent3); border-color: rgba(78,205,196,0.3); background: rgba(78,205,196,0.08); }
    .ac-badge.c4 { color: #f07167; border-color: rgba(240,113,103,0.3); background: rgba(240,113,103,0.08); }

    /* ─── LIGHTBOX ─────────────────────────────────────── */
    .lightbox {
      position: fixed; inset: 0; z-index: 3000;
      background: rgba(0,0,0,0.95);
      display: flex; align-items: center; justify-content: center;
      opacity: 0; pointer-events: none; transition: opacity 0.3s ease;
      padding: 20px;
    }
    .lightbox.open { opacity: 1; pointer-events: all; }
    .lightbox img {
      max-width: 90vw; max-height: 90vh;
      object-fit: contain; border-radius: 8px;
    }
    .lightbox-close {
      position: absolute; top: 20px; right: 20px;
      background: none; border: none; color: white;
      font-size: 2rem; cursor: pointer; line-height: 1;
      opacity: 0.7; transition: opacity var(--transition);
    }
    .lightbox-close:hover { opacity: 1; }

    /* ─── FOOTER ──────────────────────────────────────── */
    footer {
      background: var(--bg2);
      border-top: 1px solid var(--border);
      padding: 48px;
      display: flex; align-items: center; justify-content: space-between;
      flex-wrap: wrap; gap: 20px;
    }
    .footer-logo {
      font-family: var(--ff-display); font-size: 1.1rem;
      font-weight: 700; color: var(--accent);
    }
    .footer-text { color: var(--muted); font-size: 0.82rem; }
    .footer-links {
      display: flex; gap: 20px; list-style: none;
    }
    .footer-links a {
      color: var(--muted); text-decoration: none;
      font-size: 0.82rem; transition: color var(--transition);
    }
    .footer-links a:hover { color: var(--accent); }

    /* ─── SCROLL REVEAL ───────────────────────────────── */
    .reveal {
      opacity: 0; transform: translateY(24px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible { opacity: 1; transform: none; }
    .reveal-delay-1 { transition-delay: 0.1s; }
    .reveal-delay-2 { transition-delay: 0.2s; }
    .reveal-delay-3 { transition-delay: 0.3s; }

    /* ─── MOBILE ──────────────────────────────────────── */
    @media (max-width: 900px) {
      nav { padding: 16px 24px; }
      nav.scrolled { padding: 12px 24px; }
      .nav-links { display: none; }
      .nav-links.open {
        display: flex; flex-direction: column;
        position: absolute; top: 100%; left: 0; right: 0;
        background: rgba(10,10,15,0.97);
        padding: 20px 24px; gap: 16px;
        border-bottom: 1px solid var(--border);
      }
      .nav-burger { display: flex; }
      section { padding: 60px 24px; }
      #hero { padding: 100px 24px 60px; }
      .pres-layout { grid-template-columns: 1fr; gap: 40px; }
      .docs-grid { grid-template-columns: 1fr; }
      .comp-grid { grid-template-columns: 1fr; }
      .sae-grid { grid-template-columns: 1fr 1fr; }
      .modal-body { padding: 20px 24px; }
      .modal-header { padding: 28px 24px 20px; }
      footer { padding: 32px 24px; flex-direction: column; gap: 16px; }
    }
    @media (max-width: 600px) {
      .sae-grid { grid-template-columns: 1fr; }
      .pres-stats { grid-template-columns: 1fr 1fr 1fr; }
      .modal-images { grid-template-columns: 1fr; }
      .hero-name { font-size: 3rem; }
    }
  </style>
</head>
<body>

<!-- ══════════════════════════════════ NAV ══════════════════════════════════ -->
<nav id="navbar">
  <a class="nav-logo" href="#hero">Elias Gourai</a>
  <ul class="nav-links" id="navLinks">
    <li><a href="#presentation">Présentation</a></li>
    <li><a href="#documents">Documents</a></li>
    <li><a href="#competences">Compétences</a></li>
    <li><a href="#sae">Projets & SAE</a></li>
    <li><a href="#stage">Stage</a></li>
  </ul>
  <button class="nav-burger" id="burger" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- ══════════════════════════════════ HERO ══════════════════════════════════ -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <div class="hero-content">
    <div class="hero-tag">BUT Sciences des Données · Université de Lorraine</div>
    <h1 class="hero-name">Elias<br /><em>Gourai</em></h1>
    <p class="hero-sub">Étudiant passionné par la data, la programmation et l'analyse statistique — 2ème année.</p>
    <div class="hero-cta">
      <a href="#sae" class="btn btn-primary">Voir mes projets</a>
      <a href="#documents" class="btn btn-outline">Télécharger mon CV</a>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ══════════════════════════════════ PRÉSENTATION ══════════════════════════ -->
<section id="presentation">
  <div class="container">
    <div class="pres-layout">
      <div class="pres-avatar reveal">
        <div class="pres-avatar-frame" style="background:var(--bg3);">
          <img src="Portfolio/Photo Elias.jpg" alt="Photo Elias Gourai"
               style="width:100%;height:100%;object-fit:cover;display:block;border-radius:16px;" />
        </div>
        <div class="avatar-deco"></div>
        <div class="avatar-deco2"></div>
      </div>
      <div class="pres-text">
        <div class="section-header">
          <p class="section-label">// 01 — À propos</p>
          <h2 class="section-title">Qui suis-<em style="font-family:var(--ff-display);color:var(--accent);font-style:italic;">je</em> ?</h2>
          <div class="section-line"></div>
        </div>
        <p class="reveal reveal-delay-1">
          En ce début de parcours en BUT Sciences des Données à l'Université de Lorraine, j'entreprends la conception d'un portfolio appelé à devenir le témoin évolutif de mon cheminement universitaire et professionnel. Bien plus qu'un atout pour décrocher un stage, cette démarche me prépare activement à rejoindre le monde du travail avec rigueur et sérénité.
        </p>
        <p class="reveal reveal-delay-2">
          J'y consignerai, au fil de mes années d'étude, les apprentissages, projets et découvertes façonnant ma vision des données et de leur potentiel. Animé par une passion pour l'informatique et la programmation, je trouve dans leur alliance avec la statistique un terrain d'expression aussi vaste que captivant.
        </p>
        <p class="reveal reveal-delay-3">
          Ces domaines, en perpétuel mouvement, ouvrent chaque jour de nouveaux horizons. Mon ambition : repousser mes limites, m'investir avec passion dans cette formation, et devenir à terme un acteur capable d'apporter une contribution innovante à ce secteur en pleine expansion.
        </p>
        <div class="pres-stats reveal">
          <div class="stat-card">
            <div class="stat-num">2A</div>
            <div class="stat-label">BUT SD</div>
          </div>
          <div class="stat-card">
            <div class="stat-num">11</div>
            <div class="stat-label">SAE réalisées</div>
          </div>
          <div class="stat-card">
            <div class="stat-num">4</div>
            <div class="stat-label">Compétences</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════════════════════ DOCUMENTS ══════════════════════════════ -->
<section id="documents">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-label">// 02 — Documents</p>
      <h2 class="section-title">CV & Lettre de motivation</h2>
      <div class="section-line"></div>
    </div>
    <div class="docs-grid">
      <a href="Portfolio/CV ELIAS GOURAI.jpg" target="_blank" class="doc-card reveal">
        <div class="doc-icon">📄</div>
        <div class="doc-info">
          <h3>Curriculum Vitæ</h3>
          <p>Parcours académique, compétences et expériences professionnelles.</p>
          <span class="doc-badge">→ Ouvrir le CV</span>
        </div>
      </a>
      <a href="Portfolio/Lettre de motivation Stage.pdf" target="_blank" class="doc-card reveal reveal-delay-1">
        <div class="doc-icon">✉️</div>
        <div class="doc-info">
          <h3>Lettre de motivation</h3>
          <p>Candidature pour un stage chez <strong style="color:var(--accent)">NaTran</strong> — rédigée avec soin.</p>
          <span class="doc-badge">→ Ouvrir la lettre (PDF)</span>
        </div>
      </a>
    </div>
  </div>
</section>

<!-- ══════════════════════════════════ COMPÉTENCES ══════════════════════════ -->
<section id="competences">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-label">// 03 — Référentiel</p>
      <h2 class="section-title">Compétences &amp; Apprentissages critiques</h2>
      <div class="section-line"></div>
      <p style="color:var(--muted);margin-top:12px;font-size:0.9rem;">Cliquez sur une compétence pour déplier les apprentissages critiques associés (niveaux 1 &amp; 2).</p>
    </div>
    <div class="comp-grid">

      <!-- C1 — TRAITER -->
      <div class="comp-card reveal" data-comp="1">
        <div class="comp-header">
          <span class="comp-num">C1</span>
          <span class="comp-title">Traiter — Traiter des données à des fins décisionnelles</span>
          <span class="comp-arrow">▾</span>
        </div>
        <div class="comp-body">
          <div class="comp-content">
            <p>Traiter des données à des fins décisionnelles, dans le contexte du développement d'un système d'information décisionnel et de la préparation des données à des fins d'analyse statistique.</p>
            <ul class="ac-list">
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.01 — Correctement interpréter et prendre en compte le besoin du commanditaire ou du client</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.02 — Respecter les formalismes de notation</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.03 — Connaître la syntaxe des langages et savoir l'utiliser</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.04 — Mesurer l'importance de maîtriser la structure des données à exploiter</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.05 — Comprendre les structures algorithmiques de base et leur contexte d'usage</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC11.06 — Prendre conscience de l'intérêt de la programmation</div><div class="ac-level">Niveau 1 · Traiter des données structurées</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC21.01 — Comprendre l'organisation des données de l'entreprise</div><div class="ac-level">Niveau 2 · Automatiser le traitement de données multidimensionnelles</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC21.02 — Réaliser le rôle central et spécifique de l'entrepôt de données dans la chaîne décisionnelle</div><div class="ac-level">Niveau 2 · Automatiser le traitement de données multidimensionnelles</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC21.03 — Identifier et résoudre les problèmes d'intégration de sources complémentaires et hétérogènes</div><div class="ac-level">Niveau 2 · Automatiser le traitement de données multidimensionnelles</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC21.04 — Comprendre la nécessité de tester, corriger et documenter un programme</div><div class="ac-level">Niveau 2 · Automatiser le traitement de données multidimensionnelles</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC21.05 — Apprécier l'intérêt de briques logicielles existantes et savoir les utiliser</div><div class="ac-level">Niveau 2 · Automatiser le traitement de données multidimensionnelles</div></div></li>
            </ul>
          </div>
        </div>
      </div>

      <!-- C2 — ANALYSER -->
      <div class="comp-card reveal reveal-delay-1" data-comp="2">
        <div class="comp-header">
          <span class="comp-num">C2</span>
          <span class="comp-title">Analyser — Analyser statistiquement les données</span>
          <span class="comp-arrow">▾</span>
        </div>
        <div class="comp-body">
          <div class="comp-content">
            <p>Analyser statistiquement les données, dans le contexte de la programmation d'un outil d'aide à la décision et d'un projet d'étude statistique.</p>
            <ul class="ac-list">
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.01 — Réaliser que les sources de données ont des caractéristiques propres à considérer (variation, précision, mise à jour…)</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.02 — Comprendre qu'une analyse correcte ne peut émaner que de données propres et préparées</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.03 — Comprendre l'intérêt des synthèses numériques et graphiques pour décrire une variable statistique</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.04 — Comprendre l'intérêt des synthèses numériques et graphiques pour mettre en évidence des liaisons entre variables</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.05 — Comprendre l'intérêt de l'utilisation d'un modèle probabiliste</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC12.06 — Appréhender la notion de fluctuation d'échantillonnage, notamment à l'aide de simulations probabilistes</div><div class="ac-level">Niveau 1 · Mettre en œuvre une analyse descriptive</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC22.01 — Prendre conscience de la différence entre modélisation statistique et analyse exploratoire</div><div class="ac-level">Niveau 2 · Mettre en œuvre une analyse exploratoire</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC22.02 — Saisir la spécificité de l'analyse des données temporelles</div><div class="ac-level">Niveau 2 · Mettre en œuvre une analyse exploratoire</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC22.03 — Comprendre l'intérêt des analyses multivariées pour synthétiser et résumer l'information portée par plusieurs variables</div><div class="ac-level">Niveau 2 · Mettre en œuvre une analyse exploratoire</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC22.04 — Appréhender l'idée de confronter une hypothèse avec la réalité pour prendre une décision</div><div class="ac-level">Niveau 2 · Mettre en œuvre une analyse exploratoire</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC22.05 — Apprécier les limites de validité et les conditions d'application d'une analyse</div><div class="ac-level">Niveau 2 · Mettre en œuvre une analyse exploratoire</div></div></li>
            </ul>
          </div>
        </div>
      </div>

      <!-- C3 — VALORISER -->
      <div class="comp-card reveal reveal-delay-2" data-comp="3">
        <div class="comp-header">
          <span class="comp-num">C3</span>
          <span class="comp-title">Valoriser — Valoriser une production dans un contexte professionnel</span>
          <span class="comp-arrow">▾</span>
        </div>
        <div class="comp-body">
          <div class="comp-content">
            <p>Valoriser une production dans un contexte professionnel, dans le contexte du développement d'outils décisionnels et d'une étude statistique.</p>
            <ul class="ac-list">
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.01 — Prendre connaissance des biais rencontrés dans la mise en place d'une enquête</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.02 — Identifier l'importance de contextualiser ses données</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.03 — Mesurer l'importance de mettre en évidence des résultats clés par l'utilisation d'indicateurs pertinents</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.04 — Lors de la restitution des résultats, mesurer l'importance d'expliciter également la démarche suivie</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.05 — Comprendre les intérêts de la data visualisation et de l'infographie</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC13.06 — Mesurer l'importance d'une expression précise et nuancée dans la communication en français et dans une langue étrangère des résultats</div><div class="ac-level">Niveau 1 · Contextualiser et présenter les données</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC23.01 — Saisir l'intérêt de mobiliser de manière proactive des ressources métiers liées à l'environnement (y compris économique, international…)</div><div class="ac-level">Niveau 2 · Restituer et argumenter ses résultats</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC23.02 — Savoir défendre ses choix d'analyses</div><div class="ac-level">Niveau 2 · Restituer et argumenter ses résultats</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC23.03 — Saisir la nécessité de choisir des indicateurs pertinents pour communiquer sur les résultats</div><div class="ac-level">Niveau 2 · Restituer et argumenter ses résultats</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC23.04 — Prendre conscience de la rigueur requise dans ses productions et dans la communication à leur propos</div><div class="ac-level">Niveau 2 · Restituer et argumenter ses résultats</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC23.05 — Comprendre les enjeux des relations en milieu professionnel adaptées à l'interlocuteur et à sa culture</div><div class="ac-level">Niveau 2 · Restituer et argumenter ses résultats</div></div></li>
            </ul>
          </div>
        </div>
      </div>

      <!-- C4 — MODÉLISER -->
      <div class="comp-card reveal reveal-delay-3" data-comp="4">
        <div class="comp-header">
          <span class="comp-num">C4</span>
          <span class="comp-title">Modéliser — Modéliser les données dans un cadre statistique</span>
          <span class="comp-arrow">▾</span>
        </div>
        <div class="comp-body">
          <div class="comp-content">
            <p>Modéliser les données dans un cadre statistique, dans le contexte d'une analyse statistique et d'un développement statistique.</p>
            <ul class="ac-list">
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC24.01EMS — Comprendre l'intérêt de planifier le recueil des données</div><div class="ac-level">Niveau 1 · Mettre en œuvre un modèle statistique</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC24.02EMS — Appréhender les difficultés et les limites rencontrées dans la mise en œuvre d'un terrain de collecte</div><div class="ac-level">Niveau 1 · Mettre en œuvre un modèle statistique</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC24.03EMS — Comprendre l'impact du type de données sur le choix de la modélisation à mettre en œuvre</div><div class="ac-level">Niveau 1 · Mettre en œuvre un modèle statistique</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC24.04EMS — Apprécier les limites de validité et les conditions d'application d'un modèle</div><div class="ac-level">Niveau 1 · Mettre en œuvre un modèle statistique</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC24.05EMS — Réaliser l'importance de la mise en œuvre d'une procédure de test statistique pour valider ou non une hypothèse</div><div class="ac-level">Niveau 1 · Mettre en œuvre un modèle statistique</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC34.01EMS — Comprendre l'intérêt des approches statistiques pour la fiabilisation, la validation, les incertitudes, les imprécisions des données</div><div class="ac-level">Niveau 2 · Réaliser l'ensemble de la démarche de modélisation</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC34.02EMS — Comprendre l'intérêt de la problématique métier pour réaliser la modélisation</div><div class="ac-level">Niveau 2 · Réaliser l'ensemble de la démarche de modélisation</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC34.03EMS — Viser la réalisation d'un processus de modélisation dans son ensemble</div><div class="ac-level">Niveau 2 · Réaliser l'ensemble de la démarche de modélisation</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC34.04EMS — Prendre conscience des différences entre les modèles pour choisir le plus adapté</div><div class="ac-level">Niveau 2 · Réaliser l'ensemble de la démarche de modélisation</div></div></li>
              <li class="ac-item"><span class="ac-dot"></span><div><div class="ac-text">AC34.05EMS — Prendre conscience de la nécessité d'utiliser des moyens spécifiques pour analyser les données massives ou les flux de données</div><div class="ac-level">Niveau 2 · Réaliser l'ensemble de la démarche de modélisation</div></div></li>
            </ul>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ══════════════════════════════════ SAE ════════════════════════════════════ -->
<section id="sae">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-label">// 04 — Travaux</p>
      <h2 class="section-title">Projets &amp; SAE</h2>
      <div class="section-line"></div>
    </div>

    <div class="sae-filters reveal">
      <button class="filter-btn active" data-filter="all">Tous</button>
      <button class="filter-btn" data-filter="1A">1ère année</button>
      <button class="filter-btn" data-filter="2A">2ème année</button>
      <button class="filter-btn" data-filter="data">Data / SQL</button>
      <button class="filter-btn" data-filter="stat">Statistiques</button>
      <button class="filter-btn" data-filter="prog">Programmation</button>
    </div>

    <div class="sae-grid" id="saeGrid">

      <!-- SAE 101 -->
      <div class="sae-card reveal" data-years="1A" data-topics="data" data-sae="101">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f0f18);">
          <div class="sae-thumb-inner" style="color:var(--accent)">101</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 101</div>
          <div class="sae-title">Création de reporting</div>
          <div class="sae-tags">
            <span class="tag">MySQL</span><span class="tag">Excel</span><span class="tag">SQL</span><span class="tag">Reporting</span>
          </div>
        </div>
      </div>

      <!-- SAE 102 -->
      <div class="sae-card reveal reveal-delay-1" data-years="1A" data-topics="prog" data-sae="102">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1218);">
          <div class="sae-thumb-inner" style="color:var(--accent2)">102</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 102</div>
          <div class="sae-title">Lecture / Écriture de fichiers</div>
          <div class="sae-tags">
            <span class="tag">VBA</span><span class="tag">Excel</span><span class="tag">Automatisation</span>
          </div>
        </div>
      </div>

      <!-- SAE 103 -->
      <div class="sae-card reveal reveal-delay-2" data-years="1A" data-topics="stat data" data-sae="103">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1a1a);">
          <div class="sae-thumb-inner" style="color:var(--accent3)">103</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 103</div>
          <div class="sae-title">Analyse exploratoire de données</div>
          <div class="sae-tags">
            <span class="tag">Analyse</span><span class="tag">Excel</span><span class="tag">SQL</span><span class="tag">Statistiques</span>
          </div>
        </div>
      </div>

      <!-- SAE 104 -->
      <div class="sae-card reveal" data-years="1A" data-topics="data stat" data-sae="104">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#1a140f);">
          <div class="sae-thumb-inner" style="color:#f07167">104</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 104</div>
          <div class="sae-title">Production données d'entreprise</div>
          <div class="sae-tags">
            <span class="tag">Pareto</span><span class="tag">ABC</span><span class="tag">Excel</span><span class="tag">CA</span>
          </div>
        </div>
      </div>

      <!-- SAE 105 -->
      <div class="sae-card reveal reveal-delay-1" data-years="1A" data-topics="stat" data-sae="105">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#101a14);">
          <div class="sae-thumb-inner" style="color:var(--accent)">105</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 105</div>
          <div class="sae-title">Présentation anglais d'un territoire</div>
          <div class="sae-tags">
            <span class="tag">Anglais</span><span class="tag">Comparaison</span><span class="tag">Données publiques</span>
          </div>
        </div>
      </div>

      <!-- SAE 106 -->
      <div class="sae-card reveal reveal-delay-2" data-years="1A" data-topics="stat" data-sae="106">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1825,#0f0f18);">
          <div class="sae-thumb-inner" style="color:var(--accent2)">106</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 106</div>
          <div class="sae-title">Mise en œuvre d'une enquête</div>
          <div class="sae-tags">
            <span class="tag">Enquête</span><span class="tag">Google Forms</span><span class="tag">Analyse</span>
          </div>
        </div>
      </div>

      <!-- SAE 107 -->
      <div class="sae-card reveal" data-years="1A" data-topics="stat data" data-sae="107">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1a10);">
          <div class="sae-thumb-inner" style="color:var(--accent3)">107</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 107</div>
          <div class="sae-title">Traitement d'enquête</div>
          <div class="sae-tags">
            <span class="tag">Excel</span><span class="tag">RECHERCHEV</span><span class="tag">Nettoyage</span>
          </div>
        </div>
      </div>

      <!-- SAE 201 -->
      <div class="sae-card reveal reveal-delay-1" data-years="2A" data-topics="data prog" data-sae="201">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#181025);">
          <div class="sae-thumb-inner" style="color:var(--accent)">201</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 201</div>
          <div class="sae-title">Conception et implémentation de BDD</div>
          <div class="sae-tags">
            <span class="tag">Access</span><span class="tag">Looping</span><span class="tag">MCD</span><span class="tag">SQL</span>
          </div>
        </div>
      </div>

      <!-- SAE 202 -->
      <div class="sae-card reveal reveal-delay-2" data-years="2A" data-topics="stat" data-sae="202">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1818);">
          <div class="sae-thumb-inner" style="color:var(--accent2)">202</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 202</div>
          <div class="sae-title">Estimation par sondage</div>
          <div class="sae-tags">
            <span class="tag">Sondage</span><span class="tag">IC 95%</span><span class="tag">TCL</span><span class="tag">Test t</span>
          </div>
        </div>
      </div>

      <!-- SAE Programmation -->
      <div class="sae-card reveal" data-years="2A" data-topics="prog" data-sae="prog">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#1a1810);">
          <div class="sae-thumb-inner" style="color:#f07167">VBA</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE Programmation</div>
          <div class="sae-title">Immobilier — Gestion de visites</div>
          <div class="sae-tags">
            <span class="tag">VBA</span><span class="tag">Excel</span><span class="tag">Planning</span>
          </div>
        </div>
      </div>

      <!-- SAE 206 -->
      <div class="sae-card reveal reveal-delay-1" data-years="2A" data-topics="data" data-sae="206">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1518);">
          <div class="sae-thumb-inner" style="color:var(--accent3)">206</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 206</div>
          <div class="sae-title">Analyse, Reporting, Datavisualisation</div>
          <div class="sae-tags">
            <span class="tag">Reporting</span><span class="tag">Excel</span><span class="tag">Datavisualisation</span>
          </div>
        </div>
      </div>

      <!-- SAE 302 -->
      <div class="sae-card reveal reveal-delay-2" data-years="2A" data-topics="data prog" data-sae="302">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#101a14);">
          <div class="sae-thumb-inner" style="color:var(--accent)">302</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 302</div>
          <div class="sae-title">Intégration dans un datawarehouse</div>
          <div class="sae-tags">
            <span class="tag">ETL</span><span class="tag">Apache Hop</span><span class="tag">XML</span><span class="tag">SQL</span>
          </div>
        </div>
      </div>

      <!-- SAE 303 -->
      <div class="sae-card reveal" data-years="2A" data-topics="stat" data-sae="303">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#180f1a);">
          <div class="sae-thumb-inner" style="color:var(--accent2)">303</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">SAE 303</div>
          <div class="sae-title">Prévision de données temporelles</div>
          <div class="sae-tags">
            <span class="tag">Séries temporelles</span><span class="tag">COVID</span><span class="tag">Saisonnalité</span>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ══════════════════════════════════ STAGE ══════════════════════════════════ -->
<section id="stage" style="background:var(--bg2);">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-label">// 05 — Expérience professionnelle</p>
      <h2 class="section-title">Mon Stage</h2>
      <div class="section-line"></div>
    </div>

    <div class="sae-grid" style="grid-template-columns: repeat(1, 1fr); max-width: 460px;">
      <div class="sae-card reveal" data-sae="stage" style="cursor:pointer;">
        <div class="sae-thumb" style="background:linear-gradient(135deg,#1a1a25,#0f1a0f); height:140px;">
          <div class="sae-thumb-inner" style="color:var(--accent3); font-size:2rem; letter-spacing:0.05em;">NaTran</div>
          <div class="sae-thumb-gradient"></div>
        </div>
        <div class="sae-body">
          <div class="sae-code">Stage 2025</div>
          <div class="sae-title">Analyse des données de comptage gazier — NaTran</div>
          <div class="sae-tags">
            <span class="tag">Analyse données</span>
            <span class="tag">Séries temporelles</span>
            <span class="tag">ETR</span>
            <span class="tag">Gaz</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>


<!-- ══════════════════════════════════ FOOTER ════════════════════════════════ -->
<footer>
  <div class="footer-logo">Elias Gourai</div>
  <p class="footer-text">BUT Sciences des Données · Université de Lorraine · 2024–2025</p>
  <ul class="footer-links">
    <li><a href="#hero">Haut de page ↑</a></li>
  </ul>
</footer>

<!-- ══════════════════════════════════ MODAL ══════════════════════════════════ -->
<div class="modal-overlay" id="modalOverlay">
  <div class="modal" id="modal">
    <div class="modal-header">
      <div class="modal-header-bg"></div>
      <div class="modal-code" id="modalCode"></div>
      <h2 class="modal-title" id="modalTitle"></h2>
      <button class="modal-close" id="modalClose">✕</button>
    </div>
    <div class="modal-body" id="modalBody"></div>
  </div>
</div>

<!-- ══════════════════════════════════ LIGHTBOX ════════════════════════════════ -->
<div class="lightbox" id="lightbox">
  <button class="lightbox-close" id="lightboxClose">✕</button>
  <img src="" alt="" id="lightboxImg" />
</div>

<!-- ══════════════════════════════════ SCRIPTS ════════════════════════════════ -->
<script>
/* ── NAV ──────────────────────────── */
const navbar = document.getElementById('navbar');
const burger = document.getElementById('burger');
const navLinks = document.getElementById('navLinks');

window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 40);
});

burger.addEventListener('click', () => {
  navLinks.classList.toggle('open');
});

document.querySelectorAll('.nav-links a').forEach(a => {
  a.addEventListener('click', () => navLinks.classList.remove('open'));
});

/* ── SCROLL REVEAL ─────────────────── */
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

/* ── COMPÉTENCES ACCORDION ─────────── */
document.querySelectorAll('.comp-card').forEach(card => {
  card.querySelector('.comp-header').addEventListener('click', () => {
    const isOpen = card.classList.contains('open');
    document.querySelectorAll('.comp-card').forEach(c => c.classList.remove('open'));
    if (!isOpen) card.classList.add('open');
  });
});

/* ── SAE FILTER ─────────────────────── */
document.querySelectorAll('.filter-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    const filter = btn.dataset.filter;
    document.querySelectorAll('.sae-card').forEach(card => {
      if (filter === 'all') {
        card.style.display = '';
      } else {
        const years = card.dataset.years || '';
        const topics = card.dataset.topics || '';
        const match = years.includes(filter) || topics.includes(filter);
        card.style.display = match ? '' : 'none';
      }
    });
  });
});

/* ── SAE DATA ────────────────────────── */
const saeData = {
  '101': {
    code: 'SAE 101',
    title: 'Création de reporting',
    sections: [
      { title: 'Introduction', text: `Dans le cadre de notre formation en BUT Sciences des Données, nous avons mené à bien une SAE consacrée à la création de reporting. Ce projet nous a permis d'exploiter des données provenant d'une base MySQL, en mettant en pratique différentes techniques d'extraction, de traitement et de visualisation.
<br><br>Notre mission consistait à produire un rapport complet, en suivant plusieurs étapes clés :
<ul><li>Interroger la base de données à l'aide de requêtes SQL pour extraire les informations pertinentes ;</li><li>Nettoyer et organiser les données dans Excel en utilisant des tableaux croisés dynamiques ;</li><li>Créer des visualisations graphiques pour faciliter l'interprétation.</li></ul>
À travers ce travail, nous avons approfondi notre maîtrise des outils de gestion de bases de données, tout en développant notre capacité à analyser des jeux de données complexes.` },
      { title: 'Mes impressions', text: `Ce que j'ai apprécié : Ce projet m'a permis de découvrir MySQL et de manipuler une base de données volumineuse. J'ai pu développer mes compétences en SQL, en apprenant à concevoir des requêtes pour extraire des données pertinentes. L'utilisation d'Excel pour créer des tableaux croisés dynamiques et des graphiques a également été très enrichissante.` },
      { title: 'Ce qui a été plus difficile', text: `La rédaction de requêtes SQL complexes a parfois posé problème, notamment en raison d'erreurs de syntaxe ou de logique difficiles à identifier. La gestion des outils multiples (MySQL, Notepad++, Excel) a également pu être fastidieuse. Enfin, le travail nécessitait une grande rigueur.` },
      { title: 'Illustrations', images: ['SAE 101 Extrait du rapport.png', 'SAE 101 exemple de code.png'] }
    ],
    ac: [
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
      { label: 'AC11.03 — Décrire une base de données', cls: 'c1' },
      { label: 'AC41.01 — Interroger une BDD (SQL)', cls: 'c4' },
      { label: 'AC31.02 — Produire des visualisations graphiques', cls: 'c3' },
      { label: 'AC31.03 — Rédiger des rapports d\'analyse', cls: 'c3' },
    ]
  },
  '102': {
    code: 'SAE 102',
    title: 'Lecture / Écriture de fichiers',
    sections: [
      { title: 'Introduction', text: `Dans le cadre de mon projet SAE : Lecture / Écriture de fichiers, j'ai travaillé sur la conception de plusieurs programmes en VBA afin d'atteindre un objectif final. Ce projet m'a permis d'explorer la manipulation des fichiers à travers le langage VBA, en développant différents programmes permettant de rassembler et transformer différentes feuilles Excel en un seul fichier respectant les consignes.` },
      { title: 'Remarques en cours de SAE', text: `<ul><li>Mauvaise maîtrise de certains outils et méthodologies</li><li>Gestion du temps, organisation et communication en équipe à revoir</li></ul>` },
      { title: 'Illustrations', images: ['SAE 102 VBA.png'] },
      { title: 'Difficultés rencontrées et leurs causes', text: `<ul><li>Difficultés techniques : manques de notion, difficulté à appliquer une vraie méthode</li><li>Problème organisationnel : mauvaise répartition des tâches, délais sous-estimés, manque de planification</li></ul>` },
      { title: 'Vers l\'amélioration', text: `<ol><li>Améliorer ses compétences : pratiquer davantage, demander de l'aide</li><li>Optimiser l'organisation : mieux planifier le travail, définir des objectifs clairs</li><li>Améliorer la communication : mettre en place des discussions plus régulières, clarifier les rôles et responsabilités</li></ol>` },
    ],
    ac: [
      { label: 'AC41.02 — Lire et écrire des fichiers structurés', cls: 'c4' },
      { label: 'AC41.03 — Développer des scripts d\'automatisation (VBA)', cls: 'c4' },
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
    ]
  },
  '103': {
    code: 'SAE 103',
    title: 'Analyse exploratoire de données',
    sections: [
      { title: 'Introduction', text: `Dans le cadre de notre formation en BUT Sciences des Données, nous avons réalisé un projet concret de création de reporting à partir de données issues d'une base MySQL. Notre mission principale consistait à : extraire des données pertinentes en élaborant des requêtes SQL complexes, structurer et nettoyer ces données dans Excel, créer des visualisations claires et des tableaux de bord interactifs.` },
      { title: 'Démarche suivie', text: `<ol><li><strong>Extraction des données</strong> : Conception et optimisation de requêtes SQL pour sélectionner les informations les plus pertinentes dans la base MySQL.</li><li><strong>Transformation et analyse</strong> : Nettoyage (gestion des valeurs manquantes, formatage), organisation dans des tableaux croisés dynamiques, enrichissement par des calculs statistiques.</li><li><strong>Visualisation</strong> : Création de différents types de graphiques (histogrammes, camemberts, courbes) pour rendre les données facilement interprétables.</li></ol>` },
      { title: 'Données et Problématique', images: ['SAE 103 Données analyse exploratoire de données.png', 'SAE 103 Problématique analyse exploratoire de données.png'] },
      { title: 'Résultats d\'analyse', images: ['SAE 103 Analyse exploratoire de données.png'] },
      { title: 'Conclusion', text: `En conclusion, cette analyse met en lumière plusieurs tendances importantes. Les jeunes de 18 à 24 ans sont globalement plus exposés aux accidents, particulièrement sur le trajet domicile-école, avec une vulnérabilité accrue face à la gravité des accidents. À l'inverse, les adultes de 45 à 54 ans sont davantage impliqués dans les accidents sur le trajet domicile-travail. Les hommes, toutes catégories confondues, sont bien plus touchés que les femmes. Ces résultats appellent à des actions de sensibilisation, en particulier auprès des jeunes et des piétons isolés.` },
    ],
    ac: [
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
      { label: 'AC21.01 — Calculer des indicateurs statistiques descriptifs', cls: 'c2' },
      { label: 'AC21.02 — Représenter graphiquement des données', cls: 'c2' },
      { label: 'AC22.01 — Mener une analyse exploratoire multivariée', cls: 'c2' },
      { label: 'AC31.02 — Produire des visualisations graphiques adaptées', cls: 'c3' },
      { label: 'AC41.01 — Interroger une BDD (SQL)', cls: 'c4' },
    ]
  },
  '104': {
    code: 'SAE 104',
    title: 'Production données d\'entreprise',
    sections: [
      { title: 'Explication de la SAE', text: `En tant qu'employé d'une agence de localisation de véhicules à Metz, j'ai analysé les données de localisation de l'année 2024 pour évaluer la performance du parc automobile. J'ai utilisé la loi de Pareto et la méthode ABC afin d'identifier les véhicules les plus rentables.` },
      { title: 'Objectifs', text: `<ol><li>Calculer le chiffre d'affaires généré par chaque véhicule (forfait + coût kilométrique)</li><li>Repérer les informations importantes pour répondre aux questions</li><li>Appliquer la loi de Pareto (20/80) pour déterminer si 20% des véhicules génèrent 80% du CA</li><li>Classer les véhicules selon la méthode ABC : Catégorie A (80% du CA), B (15% du CA), C (5% du CA)</li></ol>` },
      { title: 'Base de données & Chiffres d\'affaires', images: ['SAE 104 Base de donnée, production de donnée en entreprise.png', 'SAE 104 Chiffres d\'affaire voiture.png'] },
      { title: 'Scoring RFM & Loi Pareto', images: ['SAE 104 Scoring RFM donnee de production en entreprise.png', 'SAE 104 Loi pareto donnee de production en entreprise.png'] },
      { title: 'Données de production', images: ['SAE 104 Donnee de production en entreprise.png'] },
      { title: 'Résultats attendus', text: `Cette analyse permettra à l'agence d'optimiser la composition de sa flotte en favorisant les véhicules les plus rentables, adapter sa stratégie commerciale (promotions, tarifs, retrait de modèles peu performants), et améliorer la gestion des stocks et des investissements futurs.` },
    ],
    ac: [
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
      { label: 'AC12.01 — Identifier et sélectionner les données pertinentes', cls: 'c1' },
      { label: 'AC21.01 — Calculer des indicateurs statistiques descriptifs', cls: 'c2' },
      { label: 'AC31.03 — Rédiger des rapports d\'analyse', cls: 'c3' },
    ]
  },
  '105': {
    code: 'SAE 105',
    title: 'Présentation anglais d\'un territoire',
    sections: [
      { title: 'Introduction', text: `Dans le cadre d'une étude sur le système éducatif local, nous avons mené une analyse comparative des collèges Ernest Bichat et Charles Guérin de Lunéville entre 2019 et 2024. Ce projet visait à identifier les forces et spécificités de chaque établissement à travers des indicateurs clés.` },
      { title: 'Objectifs du projet', text: `<ul><li>Collecter des données fiables auprès de sources officielles</li><li>Analyser les performances académiques et éducatives</li><li>Comparer les infrastructures et projets pédagogiques</li><li>Identifier les particularités de chaque établissement</li></ul>` },
      { title: 'Méthodologie employée', text: `<strong>Collecte des données</strong> : Recours aux sources officielles (Ministère de l'Éducation, Académie de Nancy-Metz), consultation de l'ONISEP et analyse d'articles locaux.<br><br><strong>Indicateurs analysés</strong> : Résultats académiques (taux de réussite et mentions au DNB), données démographiques (effectifs scolaires), conditions d'enseignement, offre pédagogique.` },
      { title: 'Principaux résultats', text: `<ul><li><strong>Collège Ernest Bichat</strong> : Organisation d'un forum des métiers en 2024 impliquant 40 professionnels, dynamisme des projets éducatifs.</li><li><strong>Collège Charles Guérin</strong> : Données moins accessibles pour la période étudiée.</li></ul>` },
      { title: 'Compétences développées', text: `<ul><li>Recherche et validation d'informations officielles</li><li>Analyse comparative d'indicateurs éducatifs</li><li>Synthèse de données qualitatives et quantitatives</li><li>Identification des limites méthodologiques</li></ul>` },
    ],
    ac: [
      { label: 'AC11.04 — Collecter des données en respectant la réglementation', cls: 'c1' },
      { label: 'AC31.03 — Rédiger des rapports d\'analyse clairs', cls: 'c3' },
      { label: 'AC31.04 — Communiquer en français et en anglais', cls: 'c3' },
    ]
  },
  '106': {
    code: 'SAE 106',
    title: 'Mise en œuvre d\'une enquête',
    sections: [
      { title: 'Introduction', text: `Dans le cadre de mon projet SAE : Mise en œuvre d'une enquête, j'ai choisi d'explorer le thème "Les effets des réseaux sociaux sur la vie étudiante". Cette étude m'a permis d'analyser l'utilisation des réseaux sociaux par les étudiants et d'évaluer leur impact sur le bien-être émotionnel, les relations sociales et les résultats académiques.` },
      { title: 'Une SAE réussie', text: `<ul><li>Respect des objectifs : mission réalisée dans les délais et répondait aux attentes</li><li>Qualité du travail : livrables clairs, structurés et pertinents, utilisation efficace des outils</li><li>Implication et autonomie : bonne gestion du travail, prise d'initiative, capacité à résoudre des problèmes</li></ul>` },
      { title: 'Questionnaire & Présentation', images: ['SAE 106 Questionnaire.png', 'SAE 106 Diapo.png'] },
      { title: 'Mes acquis et mon niveau de maîtrise', text: `<ul><li><strong>Compétences techniques</strong> : maîtrise du logiciel, de la méthodologie, de l'outil de collecte et d'analyse de données</li><li><strong>Compétences organisationnelles</strong> : gestion du temps, bonne répartition des tâches, autonomie</li><li><strong>Compétences relationnelles</strong> : communication claire avec les répondants</li></ul>` },
    ],
    ac: [
      { label: 'AC11.04 — Collecter des données', cls: 'c1' },
      { label: 'AC21.01 — Calculer des indicateurs statistiques', cls: 'c2' },
      { label: 'AC32.03 — Mettre en œuvre une démarche d\'enquête', cls: 'c3' },
      { label: 'AC31.04 — Communiquer à l\'écrit et à l\'oral', cls: 'c3' },
    ]
  },
  '107': {
    code: 'SAE 107',
    title: 'Traitement d\'enquête',
    sections: [
      { title: 'Introduction', text: `Ce projet consistait à mener une étude descriptive complète à partir d'un jeu de données sur les étudiants, en suivant un processus rigoureux de nettoyage, d'analyse et de restitution.` },
      { title: 'Ce que j\'ai dû faire', text: `<ul><li><strong>Nettoyage des données</strong> : Traçabilité complète de chaque étape, remplacement des cellules vides par N/A, utilisation de fonctions comme RECHERCHEV.</li><li><strong>Rendus intermédiaires et finaux</strong> : Compte-rendu partiel (PDF), fichier tableau avec étapes de nettoyage, CSV nettoyé, rapport final.</li><li><strong>Contraintes techniques</strong> : Encodage UTF-8, séparateurs de colonnes (point-virgule) et décimaux (point) strictement respectés.</li></ul>` },
      { title: 'Feuilles Excel & Jeu de données nettoyé', images: ['SAE 107 Feuille du Excel.png', 'SAE 107 Exemple jeux de données traitement d\'enquete.png'] },
      { title: 'RECHERCHEV & Graphiques', images: ['SAE 107 Recherche V.png', 'SAE 107 Graphique.png'] },
      { title: 'Graphique supplémentaire', images: ['SAE 107 Graphique 2.png'] },
      { title: 'Compétences mobilisées', text: `Maîtrise des outils (Excel, encodage CSV), rigueur dans la gestion des données, capacité à documenter des processus techniques, et analyse critique pour valider la qualité des données.` },
    ],
    ac: [
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
      { label: 'AC12.02 — Structurer et préparer des données pour l\'analyse', cls: 'c1' },
      { label: 'AC21.01 — Calculer des indicateurs statistiques descriptifs', cls: 'c2' },
      { label: 'AC21.02 — Représenter graphiquement des données', cls: 'c2' },
      { label: 'AC32.03 — Mettre en œuvre une démarche d\'enquête', cls: 'c3' },
    ]
  },
  '201': {
    code: 'SAE 201',
    title: 'Conception et implémentation de base de données',
    sections: [
      { title: 'Contexte & Objectifs', text: `Pour ce projet j'ai réalisé une SAE visant à concevoir et implémenter une application de gestion pour un magasin de vente de films (physique et en ligne). L'objectif principal était de mettre en place une base de données fonctionnelle permettant l'achat de films, l'ajout de nouveaux films, la consultation du détail des films, le suivi des stocks, prix et ventes par client.` },
      { title: 'Démarche technique', text: `<ol><li><strong>Constitution des données</strong> : Création d'une base sous Excel à partir de données réelles (plus d'1 million d'entrées en France). Identification des 10 films ayant eu le plus d'entrées en 2023.</li><li><strong>Modélisation conceptuelle (MCD) avec Looping</strong> : Définition des entités principales (FILM, GENRE, VENTE, CLIENT, RÉALISATEUR) et de leurs associations.</li><li><strong>Implémentation sous Access</strong> : Import des feuilles Excel, création des relations entre les tables, interface utilisateur.</li></ol>` },
      { title: 'Base de données & MCD Looping', images: ['SAE 201 Base de données.png', 'SAE 201 MCD Looping.png'] },
      { title: 'Entités & Associations', images: ['SAE 201 entité principale.png', 'SAE 201 Associations.png'] },
      { title: 'Interface Access', images: ['SAE 201 Access.png'] },
    ],
    ac: [
      { label: 'AC11.03 — Décrire une base de données', cls: 'c1' },
      { label: 'AC12.03 — Concevoir et alimenter un entrepôt de données', cls: 'c1' },
      { label: 'AC42.01 — Concevoir un modèle de données (MCD, MLD)', cls: 'c4' },
      { label: 'AC42.02 — Implémenter et administrer une base de données', cls: 'c4' },
      { label: 'AC41.01 — Interroger une BDD (SQL)', cls: 'c4' },
    ]
  },
  '202': {
    code: 'SAE 202',
    title: 'Estimation par sondage',
    sections: [
      { title: 'Contexte & Objectifs', text: `Dans le cadre de ma deuxième année de BUT Sciences des données, j'ai réalisé une SAE visant à étudier comment l'échantillonnage aléatoire permet d'estimer et de comparer des paramètres de population. Le sujet portait sur les effectifs d'élèves par niveau et par nombre de classes pour différentes années scolaires (2019 et 2022).` },
      { title: 'Distribution & Convergence', images: ['SAE 202 Distribution.png'] },
      { title: 'Démarche & Résultats clés', text: `<ol><li>Préparation des données : Nettoyage et recodage des variables.</li><li>Effet de la taille d'échantillon : Dès n ≥ 1000, convergence rapide vers la vraie moyenne (135,36 pour 2019 ; 133,20 pour 2022).</li><li>Validation des intervalles de confiance (95%) : Sur 1000 échantillons, environ 95 % des IC contiennent la vraie moyenne.</li><li>Convergence vers la loi normale (TCL) : À partir de n ≥ 100, distribution normale.</li><li>Comparaison 2019 vs 2022 : Test t de Student, p-value = 5,9 × 10⁻⁸ → différence significative, baisse de ~2,17 élèves par école.</li></ol>` },
      { title: 'Moyennes & Échantillons', images: ['SAE 202 Moyennes echantillon.png'] },
    ],
    ac: [
      { label: 'AC21.03 — Caractériser des distributions de probabilités', cls: 'c2' },
      { label: 'AC21.04 — Mettre en œuvre une démarche inférentielle', cls: 'c2' },
      { label: 'AC22.02 — Estimer des paramètres et construire des IC', cls: 'c2' },
      { label: 'AC22.03 — Réaliser des tests d\'hypothèses', cls: 'c2' },
      { label: 'AC31.03 — Rédiger des rapports d\'analyse', cls: 'c3' },
    ]
  },
  'prog': {
    code: 'SAE Programmation',
    title: 'Immobilier — Gestion de visites',
    sections: [
      { title: 'Explication du projet', text: `Ce projet vise à développer un outil pratique pour les agents immobiliers, permettant une gestion simplifiée des visites de biens. L'application stocke chaque propriété avec un identifiant unique, son adresse, sa superficie et son statut (vente ou location), ainsi que la date de signature en cas de compromis.` },
      { title: 'Fonctionnalités clés', text: `<ul><li>L'ajout de nouveaux biens</li><li>La création et suppression de visites par simple clic</li><li>La mise à jour automatique lors d'un compromis (suppression des visites futures)</li><li>Une visualisation claire de l'emploi du temps avec planning coloré (vente vs location)</li></ul>` },
      { title: 'Structure du classeur', text: `Le classeur Excel est constitué de 3 feuilles :<ul><li>Une première feuille avec les informations sur les biens disponibles</li><li>Une deuxième feuille avec les informations sur les visites prévues</li><li>Une troisième feuille avec le planning affiché</li></ul>` },
      { title: 'Feuilles Biens & Visites', images: ['SAE Programmation Donnée feuille bien.png', 'SAE Programmation Donnée feuille visite.png'] },
      { title: 'Planning généré', images: ['SAE Programmation Planning généré.png'] },
    ],
    ac: [
      { label: 'AC41.03 — Développer des scripts d\'automatisation (VBA)', cls: 'c4' },
      { label: 'AC41.02 — Lire et écrire des fichiers structurés', cls: 'c4' },
      { label: 'AC11.01 — Recenser et caractériser des données', cls: 'c1' },
      { label: 'AC32.01 — Concevoir des tableaux de bord interactifs', cls: 'c3' },
    ]
  },
  '206': {
    code: 'SAE 206',
    title: 'Analyse, Reporting, Datavisualisation',
    sections: [
      { title: 'Introduction', text: `Dans le cadre de ce projet, mon objectif était d'analyser des données commerciales pour créer un tableau de bord comparatif entre deux enseignes concurrentes. J'ai sélectionné trois magasins Auchan répartis en Moselle, afin d'étudier leur stratégie en ligne : analyse de leur site marchand, des gammes de produits, des prix pratiqués, des promotions et des dispositifs de fidélisation.` },
      { title: 'Démarche', text: `3 feuilles pour les catégories des 3 magasins et 3 nouvelles feuilles pour leurs produits, prix et promotions. J'ai calculé des indicateurs clés tels que les écarts de prix, les taux d'évolution et d'autres ratios pertinents pour évaluer la performance concurrentielle. Mise en place d'une datavisualisation efficace avec des graphiques mettant en lumière les tendances et différences majeures.` },
      { title: 'Magasins & Reporting', images: ['SAE Reporting Magasin.png', 'SAE Reporting Reporting des magasins .png'] },
      { title: 'Produits, prix & promotions', images: ['SAE Reporting Produitt prix promotion.png'] },
    ],
    ac: [
      { label: 'AC12.01 — Identifier et sélectionner les données pertinentes', cls: 'c1' },
      { label: 'AC21.01 — Calculer des indicateurs statistiques descriptifs', cls: 'c2' },
      { label: 'AC31.02 — Produire des visualisations graphiques adaptées', cls: 'c3' },
      { label: 'AC32.01 — Concevoir des tableaux de bord interactifs', cls: 'c3' },
      { label: 'AC32.02 — Construire et présenter un rapport d\'analyse complet', cls: 'c3' },
    ]
  },
  '302': {
    code: 'SAE 302',
    title: 'Intégration dans un datawarehouse',
    sections: [
      { title: 'Contexte & Objectifs', text: `Dans le cadre de ma deuxième année de BUT Sciences des données, j'ai conçu et alimenté un entrepôt de données dédié aux associations loi 1901 à partir de fichiers XML publics (fichier 2024).` },
      { title: 'Architecture technique', text: `<ul><li><strong>Outils</strong> : Apache Hop (ETL), HeidiSQL (base de données), XML/XPath (extraction)</li><li><strong>Modèle</strong> : 5 tables créées – GEOGRAPHIE, DATE, THEME, ASSOCIATION_LISTING, ASSOCIATION_THEMES (table de liaison)</li></ul>` },
      { title: 'Fichier XML & Workflow ETL', images: ['SAE 302 Fichier XML.png', 'SAE 302 Workflow final.png'] },
      { title: 'Workflow ETL', text: `<ul><li>Extraction XML via chemins XPath</li><li>Nettoyage (suppression doublons, conversion dates)</li><li>Jointures avec tables de référence</li><li>Chargement dans les tables cibles</li><li>Tests & validation sur échantillon</li></ul>` },
      { title: 'Difficultés & Limites', text: `Structure XML complexe (définition difficile des chemins XPath), jointures délicates entre clés des tables, incohérences de formats de dates source/cible.` },
    ],
    ac: [
      { label: 'AC12.03 — Concevoir et alimenter un entrepôt de données', cls: 'c1' },
      { label: 'AC12.02 — Structurer et préparer des données pour l\'analyse', cls: 'c1' },
      { label: 'AC41.02 — Lire et écrire des fichiers structurés (XML)', cls: 'c4' },
      { label: 'AC42.03 — Mettre en place un pipeline ETL', cls: 'c4' },
    ]
  },
  '303': {
    code: 'SAE 303',
    title: 'Prévision de données temporelles',
    sections: [
      { title: 'Contexte & Objectifs', text: `Dans le cadre de ma deuxième année de BUT Sciences des données, j'ai réalisé une analyse comparative de l'impact du COVID-19 sur le transport aérien de passagers (Autriche et Allemagne) et de fret.` },
      { title: 'Analyse saisonnière', text: `Décomposition multiplicative des séries mensuelles (2010-2025).<ul><li>Pic estival : +25% en Autriche, +23,7% en Allemagne</li><li>Creux hivernal : -19,4% en Autriche, -24,6% en Allemagne</li></ul>` },
      { title: 'Variations saisonnières', images: ['SAE 303 Variations saisonnière.png'] },
      { title: 'Impact COVID & Trajectoire sans COVID', text: `Chute brutale début 2020 (série désaisonnalisée). Autriche : reprise presque complète en 2023-2024. Allemagne : retard persistant (~10% sous le niveau pré-COVID). Construction de prévisions à partir des données 2008-2019.` },
      { title: 'Chute COVID', images: ['SAE 303 Chute Covid.png'] },
      { title: 'Analyse du fret & Synthèse', text: `<ul><li>Impact COVID moins sévère que pour les passagers</li><li>Rebond rapide en 2021 (e-commerce, livraisons)</li><li>Fret allemand 6 à 7 fois plus important qu'autrichien</li><li>Profil saisonnier stable avant et après la pandémie</li><li>Reprise autrichienne plus rapide que l'allemande</li></ul>` },
    ],
    ac: [
      { label: 'AC12.01 — Réaliser que les sources ont des caractéristiques propres', cls: 'c2' },
      { label: 'AC22.02 — Saisir la spécificité de l\'analyse des données temporelles', cls: 'c2' },
      { label: 'AC22.01 — Différence modélisation statistique / analyse exploratoire', cls: 'c2' },
      { label: 'AC23.02 — Savoir défendre ses choix d\'analyses', cls: 'c3' },
    ]
  },
  'stage': {
    code: 'Stage 2025',
    title: 'Analyse des données de comptage gazier — NaTran',
    sections: [
      { title: 'Présentation du stage', text: `J'effectue actuellement mon stage au sein de <strong style="color:var(--accent)">NaTran</strong>, entreprise reconnue dans le secteur du transport de gaz. J'ai été accueilli au sein de la <strong>Direction Clients et Optimisation du réseau (DCO)</strong>, et plus spécifiquement dans l'équipe du comptage bilan, au sein du département <strong>Analyse et Bilan Est</strong>.<br><br>Cette expérience me permet de mettre en pratique les notions acquises en formation tout en découvrant les spécificités du monde industriel.` },
      { title: 'Déroulement d\'une journée type — Matin 8h', text: `À mon arrivée sur site, j'ouvre une application appelée <strong>ETR</strong>. Sur la page d'accueil, je me concentre sur les <strong>PorteFeuilles</strong> (regroupement de différents postes de comptage où passe le gaz à analyser chaque matin). Il y en a 4, chacun rattaché à un analyste présent sur site.<br><br>Les journées les plus chargées sont les <strong>lundis</strong>, car il faut analyser les alertes du vendredi, samedi et dimanche.<br><br>Trois types de postes sont à analyser, chacun avec un temps limité (fenêtres de tir) :<ul><li><strong>Jaune et Bleu</strong> → DP (clients particuliers)</li><li><strong>Rouge</strong> → clients industriels</li><li><strong>Vert</strong> → Biométhane (gaz 100% renouvelable injecté sur le réseau NaTran)</li></ul>` },
      { title: 'Interface ETR & Alertes', images: ['1. Capture ETR.png', '2. Capture Alertes P2 surligner.png'] },
      { title: 'Analyse d\'un poste fonctionnel', text: `Prenons un poste qui fonctionne normalement. On y trouve :<ul><li>Toutes les journées gazières (6h → 6h)</li><li>Volumes en Nm³ (normo mètre cube)</li><li>Volume pris en compte</li><li>PCS (qualité du gaz)</li><li>Énergie facturée</li><li>Pression et température</li></ul>Ce poste est dit <strong>« maillé »</strong> : d'autres postes tournent avec lui. Mon objectif est d'analyser uniquement les postes en alerte. Pour faciliter l'analyse, j'ai accès à plusieurs graphiques : courbe du volume, courbe de température, courbe de pression.` },
      { title: 'Poste fonctionnel — données & graphiques', images: ['3. Capture DP fonctionnel.png', '4. Capture DP fonctionnel journalier.png'] },
      { title: 'Graphique poste fonctionnel', images: ['5. Capture DP fonctionnel graphique.png'] },
      { title: 'Analyse d\'un poste en panne', text: `Différentes pannes peuvent survenir :<ul><li>Défauts communication</li><li>Défauts compteurs (mesure du volume livré)</li><li>Problèmes de sonde de température</li><li>Vannes de sécurité activées (chute de pression)</li><li>Numéros interdits (arrêt de la télétransmission)</li></ul>Dans l'exemple ci-dessous, la panne est signalée par l'acronyme <strong>NI</strong>. L'outil indique <strong>AF</strong> (Acquis fiable) jusqu'au 19 mai, puis <strong>CS</strong> (Substitution) à partir du 20 mai (valeurs estimées par l'outil). On observe : pression figée, température à 0 (manquant), volumes journaliers anormaux.<br><br>Lors d'une panne, le gaz continue de circuler. Il faut donc <strong>estimer le volume journalier</strong> par comparaison avec des postes similaires (agrégat) et analyse du profil de consommation. Une fois la panne résolue, un autre service procède à une réinterrogation pour récupérer les données manquantes.` },
      { title: 'Poste en panne — données & graphiques', images: ['6. Capture Marly DP NI.png', '7. Capture Marly DP NI journalier.png'] },
      { title: 'Graphique poste en panne', images: ['8. Capture Marly DP NI graphique.png'] },
    ],
    ac: [
      { label: 'AC11.03 — Connaître la syntaxe des langages et savoir l\'utiliser', cls: 'c1' },
      { label: 'AC11.04 — Mesurer l\'importance de maîtriser la structure des données à exploiter', cls: 'c1' },
      { label: 'AC12.01 — Réaliser que les sources de données ont des caractéristiques propres à considérer', cls: 'c2' },
      { label: 'AC22.02 — Saisir la spécificité de l\'analyse des données temporelles', cls: 'c2' },
      { label: 'AC13.03 — Mesurer l\'importance de mettre en évidence des résultats clés par des indicateurs pertinents', cls: 'c3' },
      { label: 'AC23.02 — Savoir défendre ses choix d\'analyses', cls: 'c3' },
      { label: 'AC24.04EMS — Apprécier les limites de validité et les conditions d\'application d\'un modèle', cls: 'c4' },
      { label: 'AC34.04EMS — Prendre conscience des différences entre les modèles pour choisir le plus adapté', cls: 'c4' },
    ]
  }
};

/* ── MODAL OPEN ─────────────────────── */
const overlay = document.getElementById('modalOverlay');
const modalCode = document.getElementById('modalCode');
const modalTitle = document.getElementById('modalTitle');
const modalBody = document.getElementById('modalBody');
const modalClose = document.getElementById('modalClose');

function buildModalHTML(data) {
  let html = '';
  data.sections.forEach(sec => {
    html += `<div class="modal-section">`;
    if (sec.title) html += `<h3 class="modal-section-title">${sec.title}</h3>`;
    if (sec.text) html += `<div style="color:var(--muted);font-size:.875rem;line-height:1.8">${sec.text}</div>`;
    if (sec.images && sec.images.length) {
      html += `<div class="modal-images">`;
      sec.images.forEach(img => {
        html += `<div class="modal-img-wrap" onclick="openLightbox('Portfolio/${img}')"><img src="Portfolio/${img}" alt="${img}" loading="lazy" /></div>`;
      });
      html += `</div>`;
    }
    html += `</div>`;
  });

  // AC & Compétences
  html += `<div class="modal-ac">
    <h4>Apprentissages critiques &amp; Compétences validées</h4>
    <div class="ac-badges">`;
  data.ac.forEach(a => {
    html += `<span class="ac-badge ${a.cls}">${a.label}</span>`;
  });
  html += `</div></div>`;
  return html;
}

document.querySelectorAll('.sae-card').forEach(card => {
  card.addEventListener('click', () => {
    const key = card.dataset.sae;
    const data = saeData[key];
    if (!data) return;
    modalCode.textContent = data.code;
    modalTitle.textContent = data.title;
    modalBody.innerHTML = buildModalHTML(data);
    overlay.classList.add('open');
    document.body.style.overflow = 'hidden';
  });
});

function closeModal() {
  overlay.classList.remove('open');
  document.body.style.overflow = '';
}

modalClose.addEventListener('click', closeModal);
overlay.addEventListener('click', e => { if (e.target === overlay) closeModal(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape') { closeModal(); closeLightbox(); } });

/* ── LIGHTBOX ─────────────────────────── */
const lightbox = document.getElementById('lightbox');
const lightboxImg = document.getElementById('lightboxImg');
const lightboxClose = document.getElementById('lightboxClose');

function openLightbox(src) {
  lightboxImg.src = src;
  lightbox.classList.add('open');
}
function closeLightbox() {
  lightbox.classList.remove('open');
  lightboxImg.src = '';
}
lightboxClose.addEventListener('click', closeLightbox);
lightbox.addEventListener('click', e => { if (e.target === lightbox) closeLightbox(); });
</script>
</body>
</html>
