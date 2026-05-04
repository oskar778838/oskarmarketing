<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Passives Einkommen mit Affiliate Marketing &mdash; ohne Produkt, ohne Startkapital">
  <title>Oskar Marketing</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;0,700;1,400;1,600&family=DM+Sans:wght@400;500&display=swap');

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #050505;
      --card: rgba(11,11,11,0.9);
      --surf-el: #161616;
      --gold: #C9A84C;
      --gold-l: #E8C96A;
      --gold-p: #F5E6B8;
      --gold-b: rgba(201,168,76,0.22);
      --text: #EDE9E3;
      --text-2: #7a7570;
      --text-m: #383838;
    }

    html { background: var(--bg); }

    body {
      font-family: 'DM Sans', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100dvh;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      padding: 44px 16px 56px;
      position: relative;
      overflow-x: hidden;
    }

    /* WebGL Canvas background */
    #bg-canvas {
      position: fixed;
      inset: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    /* Grain overlay on top of shader */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.88' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
      opacity: 0.028;
      pointer-events: none;
      z-index: 1;
    }

    /* Particles */
    .particles { position: fixed; inset: 0; overflow: hidden; pointer-events: none; z-index: 2; }
    .particles span {
      position: absolute;
      bottom: -6px;
      left: var(--l);
      width: var(--s);
      height: var(--s);
      background: var(--gold);
      border-radius: 50%;
      opacity: 0;
      animation: float-up var(--d) linear var(--dl) infinite;
    }
    @keyframes float-up {
      0%  { transform: translateY(0) translateX(0); opacity: 0; }
      6%  { opacity: 0.35; }
      90% { opacity: 0.08; }
      100%{ transform: translateY(-105vh) translateX(var(--dx)); opacity: 0; }
    }

    /* CARD */
    .card {
      position: relative;
      z-index: 3;
      width: 100%;
      max-width: 400px;
      background: var(--card);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border: 1px solid var(--gold-b);
      border-radius: 26px;
      padding: 42px 28px 38px;
      box-shadow:
        0 0 0 1px rgba(255,255,255,0.022),
        0 28px 90px rgba(0,0,0,0.88),
        0 6px 24px rgba(201,168,76,0.055);
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 18%; right: 18%;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.55), transparent);
      border-radius: 1px;
    }

    /* AVATAR */
    .avatar-wrap {
      position: relative;
      width: 108px;
      height: 108px;
      margin-bottom: 22px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.06s forwards;
    }
    .avatar-glow {
      position: absolute;
      inset: -14px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(201,168,76,0.22) 0%, transparent 62%);
    }
    .ring-outer {
      position: absolute;
      inset: -4px;
      border-radius: 50%;
      background: conic-gradient(
        from 0deg,
        #C9A84C 0deg, #E8C96A 45deg, #C9A84C 90deg,
        rgba(60,42,8,0.15) 140deg, rgba(40,28,4,0.08) 180deg,
        rgba(60,42,8,0.15) 220deg, #C9A84C 270deg,
        #E8C96A 315deg, #C9A84C 360deg
      );
      animation: r-spin 7s linear infinite;
      -webkit-mask: radial-gradient(farthest-side, transparent calc(100% - 3px), #fff calc(100% - 3px));
      mask: radial-gradient(farthest-side, transparent calc(100% - 3px), #fff calc(100% - 3px));
    }
    .ring-inner {
      position: absolute;
      inset: 5px;
      border-radius: 50%;
      background: conic-gradient(
        from 0deg,
        transparent 0deg, rgba(201,168,76,0.55) 70deg,
        transparent 130deg, transparent 230deg,
        rgba(201,168,76,0.4) 295deg, transparent 360deg
      );
      animation: r-spin 10s linear infinite reverse;
      -webkit-mask: radial-gradient(farthest-side, transparent calc(100% - 2px), #fff calc(100% - 2px));
      mask: radial-gradient(farthest-side, transparent calc(100% - 2px), #fff calc(100% - 2px));
    }
    .avatar-img {
      position: absolute;
      inset: 8px;
      width: calc(100% - 16px);
      height: calc(100% - 16px);
      border-radius: 50%;
      object-fit: cover;
      object-position: center top;
    }
    @keyframes r-spin { to { transform: rotate(360deg); } }

    /* NAME */
    .profile-name {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 700;
      font-size: 31px;
      letter-spacing: 0.07em;
      text-align: center;
      margin-bottom: 5px;
      background: linear-gradient(110deg, #C9A84C 0%, #E8C96A 32%, #F5E6B8 50%, #E8C96A 68%, #C9A84C 100%);
      background-size: 200% auto;
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      opacity: 0;
      animation:
        fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.16s forwards,
        name-shimmer 5s ease-in-out 1.8s infinite;
    }
    @keyframes name-shimmer {
      0%, 100% { background-position: 0% center; }
      50% { background-position: 100% center; }
    }
    .profile-handle {
      font-size: 11px;
      font-weight: 400;
      color: var(--text-m);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 24px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.22s forwards;
    }

    /* ORNAMENT */
    .ornament {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 22px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.28s forwards;
    }
    .ornament::before, .ornament::after {
      content: ''; display: block; width: 52px; height: 1px;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.45));
    }
    .ornament::after { background: linear-gradient(90deg, rgba(201,168,76,0.45), transparent); }
    .orn-gem {
      width: 5px; height: 5px;
      background: var(--gold);
      transform: rotate(45deg);
      flex-shrink: 0;
      box-shadow: 0 0 6px rgba(201,168,76,0.5);
    }

    /* BIO */
    .bio {
      text-align: center;
      margin-bottom: 28px;
      padding: 0 2px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.34s forwards;
    }
    .bio-main { font-size: 14px; line-height: 1.82; color: var(--text-2); letter-spacing: 0.01em; }
    .bio-hook {
      display: block;
      margin-top: 11px;
      font-family: 'Cormorant Garamond', serif;
      font-style: italic;
      font-weight: 400;
      font-size: 19px;
      color: var(--gold);
      letter-spacing: 0.04em;
    }

    /* STATS */
    .stats {
      display: flex; gap: 9px; width: 100%; margin-bottom: 26px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.44s forwards;
    }
    .stat-card {
      flex: 1;
      background: var(--surf-el);
      border: 1px solid var(--gold-b);
      border-radius: 13px;
      padding: 16px 6px 14px;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .stat-card::after {
      content: '';
      position: absolute; top: 0; left: 0; right: 0; height: 1px;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.75), transparent);
    }
    .stat-value {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 700; font-size: 22px; color: var(--gold);
      display: block; line-height: 1;
      animation: stat-pop 0.5s cubic-bezier(0.34,1.56,0.64,1) 0.9s both;
    }
    @keyframes stat-pop {
      0%   { transform: scale(0.75); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    .stat-label { font-size: 10px; color: var(--text-m); letter-spacing: 0.06em; margin-top: 5px; display: block; line-height: 1.4; }

    /* CTA */
    .cta-wrap {
      width: 100%; margin-bottom: 30px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.54s forwards;
    }
    .cta-btn {
      display: block; width: 100%; padding: 22px 24px 20px;
      text-decoration: none; text-align: center; border-radius: 17px;
      position: relative; overflow: hidden;
      background: linear-gradient(110deg, #8a6018 0%, #C9A84C 22%, #E8C96A 44%, #F5E6B8 50%, #E8C96A 56%, #C9A84C 78%, #8a6018 100%);
      background-size: 300% 100%;
      box-shadow: 0 0 0 0 rgba(201,168,76,0.45), 0 12px 44px rgba(201,168,76,0.22), 0 4px 14px rgba(0,0,0,0.55), inset 0 1px 0 rgba(255,255,255,0.22);
      -webkit-tap-highlight-color: transparent;
      animation: shimmer-btn 3.2s ease-in-out infinite, pulse-ring 2.4s ease-in-out 1.2s infinite;
      transition: transform 0.12s ease;
    }
    .cta-btn:active { transform: scale(0.975); }
    .cta-btn::before {
      content: '';
      position: absolute; top: 0; left: -8%; right: -8%; height: 48%;
      background: linear-gradient(180deg, rgba(255,255,255,0.14), transparent);
      border-radius: 17px 17px 50% 50%;
      pointer-events: none;
    }
    @keyframes shimmer-btn {
      0%, 100% { background-position: 0% center; }
      50%       { background-position: 100% center; }
    }
    @keyframes pulse-ring {
      0%, 100% { box-shadow: 0 0 0 0 rgba(201,168,76,0.45), 0 12px 44px rgba(201,168,76,0.22), 0 4px 14px rgba(0,0,0,0.55), inset 0 1px 0 rgba(255,255,255,0.22); }
      50%       { box-shadow: 0 0 0 7px rgba(201,168,76,0), 0 12px 52px rgba(201,168,76,0.32), 0 4px 14px rgba(0,0,0,0.55), inset 0 1px 0 rgba(255,255,255,0.22); }
    }
    .cta-eyebrow { display: block; font-size: 10px; font-weight: 500; letter-spacing: 0.28em; text-transform: uppercase; color: rgba(6,6,6,0.52); margin-bottom: 7px; }
    .cta-title { display: block; font-family: 'Cormorant Garamond', serif; font-weight: 700; font-size: 28px; color: #080808; letter-spacing: 0.07em; line-height: 1; }
    .cta-price { display: block; font-size: 13px; font-weight: 500; color: rgba(6,6,6,0.58); margin-top: 7px; }
    .cta-sub { display: block; font-size: 11px; color: rgba(6,6,6,0.42); margin-top: 5px; letter-spacing: 0.1em; }

    /* DIVIDER */
    .section-divider {
      display: flex; align-items: center; gap: 12px; width: 100%; margin-bottom: 18px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.64s forwards;
    }
    .section-divider::before { content: ''; flex: 1; height: 1px; background: linear-gradient(90deg, transparent, rgba(255,255,255,0.055)); }
    .section-divider::after  { content: ''; flex: 1; height: 1px; background: linear-gradient(90deg, rgba(255,255,255,0.055), transparent); }
    .section-divider span { font-size: 9px; font-weight: 500; letter-spacing: 0.3em; text-transform: uppercase; color: #252525; white-space: nowrap; }

    /* SOCIALS */
    .socials {
      display: grid; grid-template-columns: 1fr 1fr; gap: 10px; width: 100%; margin-bottom: 34px;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.74s forwards;
    }
    .social-link {
      display: flex; align-items: center; gap: 11px;
      padding: 16px; min-height: 52px;
      background: rgba(255,255,255,0.025);
      border: 1px solid rgba(255,255,255,0.055);
      border-radius: 13px;
      text-decoration: none; color: #908b85;
      -webkit-tap-highlight-color: transparent;
      position: relative; overflow: hidden;
      transition: transform 0.15s ease, border-color 0.2s ease, background 0.2s ease;
    }
    .social-link::after {
      content: '';
      position: absolute; top: 0; left: -100%; width: 55%; height: 100%;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.09), transparent);
      transition: left 0.48s ease;
    }
    .social-link:hover::after, .social-link:active::after { left: 160%; }
    .social-link:hover, .social-link:active { transform: scale(1.04); border-color: var(--gold-b); background: rgba(201,168,76,0.06); }
    .social-icon { width: 19px; height: 19px; flex-shrink: 0; fill: currentColor; }
    .social-name { font-size: 13px; font-weight: 500; }

    /* FOOTER */
    .footer {
      font-size: 10px; color: #1e1e1e; letter-spacing: 0.16em; text-align: center; text-transform: uppercase;
      opacity: 0;
      animation: fadeUp 0.9s cubic-bezier(0.16,1,0.3,1) 0.9s forwards;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after { animation: none !important; transition: none !important; opacity: 1 !important; transform: none !important; }
      .profile-name { -webkit-text-fill-color: var(--gold); }
    }
  </style>
</head>
<body>

  <canvas id="bg-canvas"></canvas>

  <div class="particles">
    <span style="--l:7%;--s:3px;--d:21s;--dl:0s;--dx:35px"></span>
    <span style="--l:17%;--s:2px;--d:26s;--dl:-8s;--dx:-22px"></span>
    <span style="--l:29%;--s:2px;--d:19s;--dl:-3s;--dx:42px"></span>
    <span style="--l:44%;--s:3px;--d:23s;--dl:-13s;--dx:-38px"></span>
    <span style="--l:57%;--s:2px;--d:29s;--dl:-6s;--dx:28px"></span>
    <span style="--l:79%;--s:2px;--d:25s;--dl:-10s;--dx:18px"></span>
  </div>

  <div class="card">
    <div class="avatar-wrap">
      <div class="avatar-glow"></div>
      <div class="ring-outer"></div>
      <div class="ring-inner"></div>
      <img class="avatar-img" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAB9AAAAfQCAIAAAAVWlMuAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAF2GlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSfvu78nIGlkPSdXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQnPz4KPHg6eG1wbWV0YSB4bWxuczp4PSdhZG9iZTpuczptZXRhLyc+CjxyZGY6UkRGIHhtbG5zOnJkZj0naHR0cDovL3d3dy53My5vcmcvMTk5OS8wMi8yMi1yZGYtc3ludGF4LW5zIyc+CgogPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9JycKICB4bWxuczpBdHRyaWI9J2h0dHA6Ly9ucy5hdHRyaWJ1dGlvbi5jb20vYWRzLzEuMC8nPgogIDxBdHRyaWI6QWRzPgogICA8cmRmOlNlcT4KICAgIDxyZGY6bGkgcmRmOnBhcnNlVHlwZT0nUmVzb3VyY2UnPgogICAgIDxBdHRyaWI6Q3JlYXRlZD4yMDI2LTA0LTE5PC9BdHRyaWI6Q3JlYXRlZD4KICAgICA8QXR0cmliOkRhdGE+eyZxdW90O2RvYyZxdW90OzomcXVvdDtEQUhHbmplLXp6cyZxdW90OywmcXVvdDt1c2VyJnF1b3Q7OiZxdW90O1VBR2FxVHpUZDNRJnF1b3Q7LCZxdW90O2JyYW5kJnF1b3Q7OiZxdW90O0JBR2FxU1VZOUZBJnF1b3Q7LCZxdW90O3RlbXBsYXRlJnF1b3Q7OiZxdW90O0VsZWdhbnQgTW9ub2dyYW0gTG9nbyBNaW5pbWFsaXN0IFNjaHdhcnomcXVvdDt9PC9BdHRyaWI6RGF0YT4KICAgICA8QXR0cmliOkV4dElkPjBlN2MwZGZkLTNhN2ItNDQ4Yi04ZTYzLWY0MjU1NTFiMjBiYTwvQXR0cmliOkV4dElkPgogICAgIDxBdHRyaWI6RmJJZD41MjUyNjU5MTQxNzk1ODA8L0F0dHJpYjpGYklkPgogICAgIDxBdHRyaWI6VG91Y2hUeXBlPjI8L0F0dHJpYjpUb3VjaFR5cGU+CiAgICA8L3JkZjpsaT4KICAgPC9yZGY6U2VxPgogIDwvQXR0cmliOkFkcz4KIDwvcmRmOkRlc2NyaXB0aW9uPgoK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
