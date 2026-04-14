<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sriram K.T — Full Stack Developer</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
  <style>
    /* ===== RESET & VARIABLES ===== */
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --gold: #FFD700;
      --cyan: #00FFFF;
      --bg: #050505;
      --bg2: #0d0d0d;
      --card: rgba(255,255,255,0.04);
      --border: rgba(255,215,0,0.15);
      --text: #e8e8e8;
      --muted: #888;
      --font-head: 'Syne', sans-serif;
      --font-mono: 'Space Mono', monospace;
    }

    html { scroll-behavior: smooth; overflow-x: hidden; }

    body {
      font-family: var(--font-mono);
      background: var(--bg);
      color: var(--text);
      overflow-x: hidden;
    }

    /* ===== CUSTOM SCROLLBAR ===== */
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 2px; }

    /* ===== NOISE OVERLAY ===== */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none; z-index: 9999; opacity: 0.4;
    }

    /* ===== NAVBAR ===== */
    nav {
      position: fixed; top: 0; width: 100%; z-index: 1000;
      background: rgba(5,5,5,0.85);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
      transition: all 0.3s;
    }
    nav.scrolled { background: rgba(5,5,5,0.98); box-shadow: 0 2px 30px rgba(255,215,0,0.08); }

    .nav-inner {
      max-width: 1100px; margin: 0 auto;
      display: flex; align-items: center; justify-content: space-between;
      padding: 18px 24px;
    }

    .logo {
      font-family: var(--font-head);
      font-weight: 800; font-size: 1.2rem;
      background: linear-gradient(90deg, var(--gold), var(--cyan));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      letter-spacing: 1px;
    }

    .nav-links { display: flex; gap: 32px; list-style: none; }
    .nav-links a {
      color: var(--muted); text-decoration: none;
      font-size: 0.78rem; letter-spacing: 2px; text-transform: uppercase;
      transition: color 0.3s; position: relative; padding-bottom: 4px;
    }
    .nav-links a::after {
      content: ''; position: absolute; bottom: 0; left: 0;
      width: 0; height: 1px; background: var(--gold);
      transition: width 0.3s;
    }
    .nav-links a:hover { color: var(--gold); }
    .nav-links a:hover::after { width: 100%; }

    .hamburger {
      display: none; cursor: pointer;
      font-size: 1.5rem; color: var(--gold);
      background: none; border: none;
      transition: 0.3s;
    }

    /* ===== MOBILE NAV ===== */
    @media (max-width: 768px) {
      .hamburger { display: block; }
      .nav-links {
        position: fixed; top: 0; right: -100%;
        width: 260px; height: 100vh;
        background: rgba(5,5,5,0.97);
        flex-direction: column; gap: 0;
        padding-top: 80px;
        border-left: 1px solid var(--border);
        transition: right 0.35s cubic-bezier(0.4,0,0.2,1);
        z-index: 999;
      }
      .nav-links.open { right: 0; }
      .nav-links li a {
        display: block; padding: 18px 32px;
        font-size: 0.85rem;
        border-bottom: 1px solid rgba(255,215,0,0.05);
      }
      .close-btn {
        position: absolute; top: 22px; right: 24px;
        background: none; border: none;
        color: var(--gold); font-size: 1.4rem; cursor: pointer;
      }
    }

    /* ===== HERO ===== */
    #hero {
      min-height: 100vh;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      text-align: center;
      padding: 100px 24px 60px;
      position: relative;
      overflow: hidden;
    }

    /* Animated background grid */
    #hero::before {
      content: '';
      position: absolute; inset: 0;
      background-image:
        linear-gradient(rgba(255,215,0,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,215,0,0.03) 1px, transparent 1px);
      background-size: 50px 50px;
      animation: gridMove 20s linear infinite;
    }
    @keyframes gridMove { 0% { transform: translateY(0); } 100% { transform: translateY(50px); } }

    /* Glow orbs */
    .orb {
      position: absolute; border-radius: 50%;
      filter: blur(80px); pointer-events: none;
    }
    .orb1 { width: 400px; height: 400px; background: rgba(255,215,0,0.07); top: -100px; left: -100px; }
    .orb2 { width: 350px; height: 350px; background: rgba(0,255,255,0.05); bottom: -50px; right: -50px; }

    .hero-photo {
      width: 150px; height: 150px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid var(--gold);
      box-shadow: 0 0 0 6px rgba(255,215,0,0.08), 0 0 40px rgba(255,215,0,0.3), 0 0 80px rgba(0,255,255,0.15);
      margin-bottom: 32px;
      position: relative; z-index: 1;
      animation: photoFloat 4s ease-in-out infinite;
    }
    @keyframes photoFloat {
      0%,100% { transform: translateY(0); }
      50% { transform: translateY(-8px); }
    }

    .hero-tag {
      font-size: 0.7rem; letter-spacing: 4px; text-transform: uppercase;
      color: var(--gold); margin-bottom: 16px;
      position: relative; z-index: 1;
      opacity: 0; animation: fadeUp 0.6s 0.2s forwards;
    }

    #hero h1 {
      font-family: var(--font-head);
      font-size: clamp(3rem, 8vw, 6rem);
      font-weight: 800;
      line-height: 1;
      background: linear-gradient(135deg, #fff 0%, var(--gold) 50%, var(--cyan) 100%);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      margin-bottom: 16px;
      position: relative; z-index: 1;
      opacity: 0; animation: fadeUp 0.7s 0.4s forwards;
    }

    .hero-subtitle {
      font-size: clamp(0.85rem, 2vw, 1rem);
      color: var(--muted); margin-bottom: 8px;
      letter-spacing: 2px;
      position: relative; z-index: 1;
      opacity: 0; animation: fadeUp 0.7s 0.6s forwards;
    }

    .typing-wrap {
      font-size: clamp(0.9rem, 2.5vw, 1.1rem);
      color: var(--cyan); margin-bottom: 40px;
      min-height: 1.6em;
      position: relative; z-index: 1;
      opacity: 0; animation: fadeUp 0.7s 0.8s forwards;
    }
    .cursor { display: inline-block; animation: blink 0.9s infinite; }
    @keyframes blink { 0%,100% { opacity:1; } 50% { opacity:0; } }

    .hero-btns {
      display: flex; gap: 16px; flex-wrap: wrap; justify-content: center;
      position: relative; z-index: 1;
      opacity: 0; animation: fadeUp 0.7s 1s forwards;
    }

    .btn-primary, .btn-ghost {
      padding: 13px 32px;
      border-radius: 3px;
      font-family: var(--font-mono);
      font-size: 0.78rem; letter-spacing: 2px; text-transform: uppercase;
      text-decoration: none; font-weight: 700;
      transition: all 0.3s;
      cursor: pointer; border: none;
    }
    .btn-primary {
      background: linear-gradient(90deg, var(--gold), #f0b800);
      color: #000;
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(255,215,0,0.4); }
    .btn-ghost {
      background: transparent;
      color: var(--cyan);
      border: 1px solid var(--cyan);
    }
    .btn-ghost:hover { background: rgba(0,255,255,0.08); transform: translateY(-2px); }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Scroll indicator */
    .scroll-hint {
      position: absolute; bottom: 32px;
      display: flex; flex-direction: column; align-items: center; gap: 8px;
      opacity: 0.4; z-index: 1;
      animation: fadeIn 1s 1.5s forwards;
    }
    .scroll-hint span { font-size: 0.65rem; letter-spacing: 3px; text-transform: uppercase; }
    .scroll-line {
      width: 1px; height: 40px;
      background: linear-gradient(var(--gold), transparent);
      animation: scrollPulse 2s infinite;
    }
    @keyframes scrollPulse { 0%,100% { opacity:0.4; } 50% { opacity:1; } }
    @keyframes fadeIn { to { opacity: 0.4; } }

    /* ===== SECTION COMMON ===== */
    section {
      max-width: 1000px; margin: 0 auto;
      padding: 100px 24px;
    }

    .section-label {
      font-size: 0.65rem; letter-spacing: 4px; text-transform: uppercase;
      color: var(--gold); margin-bottom: 12px;
      display: flex; align-items: center; gap: 12px;
    }
    .section-label::after {
      content: ''; flex: 1; height: 1px;
      background: linear-gradient(90deg, var(--border), transparent);
    }

    .section-title {
      font-family: var(--font-head);
      font-size: clamp(2rem, 5vw, 3rem);
      font-weight: 800;
      color: #fff;
      margin-bottom: 48px;
      line-height: 1.1;
    }
    .section-title span { color: var(--gold); }

    /* Reveal animation */
    .reveal {
      opacity: 0; transform: translateY(30px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    /* ===== ABOUT ===== */
    #about { border-top: 1px solid var(--border); }

    .about-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center;
    }
    @media (max-width: 700px) { .about-grid { grid-template-columns: 1fr; gap: 32px; } }

    .about-text p {
      color: var(--muted); line-height: 1.9; font-size: 0.9rem; margin-bottom: 16px;
    }
    .about-text strong { color: var(--gold); }

    .about-stats {
      display: grid; grid-template-columns: 1fr 1fr; gap: 16px;
    }
    .stat-box {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: 24px 20px;
      text-align: center;
      transition: 0.3s;
    }
    .stat-box:hover { border-color: var(--gold); background: rgba(255,215,0,0.05); }
    .stat-num {
      font-family: var(--font-head);
      font-size: 2.2rem; font-weight: 800;
      background: linear-gradient(90deg, var(--gold), var(--cyan));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .stat-label { font-size: 0.68rem; letter-spacing: 2px; color: var(--muted); margin-top: 4px; text-transform: uppercase; }

    /* ===== SKILLS ===== */
    #skills { border-top: 1px solid var(--border); }

    .skills-tabs {
      display: flex; gap: 8px; margin-bottom: 32px; flex-wrap: wrap;
    }
    .tab-btn {
      padding: 8px 20px; border-radius: 2px;
      background: transparent; border: 1px solid var(--border);
      color: var(--muted); font-family: var(--font-mono);
      font-size: 0.72rem; letter-spacing: 2px; text-transform: uppercase;
      cursor: pointer; transition: 0.3s;
    }
    .tab-btn.active, .tab-btn:hover {
      background: rgba(255,215,0,0.1); border-color: var(--gold); color: var(--gold);
    }

    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
      gap: 16px;
    }

    .skill-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: 24px 16px;
      text-align: center;
      transition: 0.35s cubic-bezier(0.4,0,0.2,1);
      cursor: default;
    }
    .skill-card:hover {
      transform: translateY(-6px);
      border-color: var(--gold);
      background: rgba(255,215,0,0.06);
      box-shadow: 0 12px 30px rgba(255,215,0,0.1);
    }
    .skill-card img { width: 52px; height: 52px; object-fit: contain; margin-bottom: 12px; }
    .skill-card p { font-size: 0.72rem; letter-spacing: 1px; color: var(--muted); text-transform: uppercase; }
    .skill-card:hover p { color: var(--gold); }

    /* ===== PROJECTS ===== */
    #projects { border-top: 1px solid var(--border); }

    .projects-grid {
      display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 24px;
    }

    .project-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 6px;
      overflow: hidden;
      transition: 0.4s;
      position: relative;
    }
    .project-card:hover {
      transform: translateY(-8px);
      border-color: var(--cyan);
      box-shadow: 0 20px 60px rgba(0,255,255,0.1);
    }

    .project-img-wrap { position: relative; overflow: hidden; aspect-ratio: 16/9; }
    .project-img-wrap img {
      width: 100%; height: 100%; object-fit: cover;
      transition: transform 0.5s;
    }
    .project-card:hover .project-img-wrap img { transform: scale(1.05); }

    .project-overlay {
      position: absolute; inset: 0;
      background: linear-gradient(transparent, rgba(0,0,0,0.7));
    }

    .project-tag {
      position: absolute; top: 12px; right: 12px;
      background: rgba(255,215,0,0.15);
      border: 1px solid var(--gold);
      color: var(--gold);
      font-size: 0.62rem; letter-spacing: 2px; text-transform: uppercase;
      padding: 4px 10px; border-radius: 2px;
    }

    .project-body { padding: 24px; }
    .project-body h3 {
      font-family: var(--font-head); font-size: 1.2rem;
      font-weight: 700; color: #fff; margin-bottom: 8px;
    }
    .project-body p { color: var(--muted); font-size: 0.82rem; line-height: 1.7; margin-bottom: 16px; }

    .project-chips { display: flex; gap: 6px; flex-wrap: wrap; margin-bottom: 20px; }
    .chip {
      font-size: 0.62rem; padding: 3px 10px; border-radius: 20px;
      background: rgba(0,255,255,0.08); border: 1px solid rgba(0,255,255,0.2);
      color: var(--cyan); letter-spacing: 1px; text-transform: uppercase;
    }

    .project-link {
      display: inline-flex; align-items: center; gap: 8px;
      color: var(--gold); text-decoration: none;
      font-size: 0.72rem; letter-spacing: 2px; text-transform: uppercase;
      border-bottom: 1px solid transparent; transition: 0.3s;
    }
    .project-link:hover { border-bottom-color: var(--gold); }
    .project-link svg { transition: transform 0.3s; }
    .project-link:hover svg { transform: translate(3px, -3px); }

    /* ===== TOOLS ===== */
    #tools { border-top: 1px solid var(--border); }

    .tools-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
      gap: 12px;
    }
    .tool-card {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 4px; padding: 18px 12px;
      text-align: center; transition: 0.3s;
    }
    .tool-card:hover { border-color: var(--cyan); background: rgba(0,255,255,0.04); }
    .tool-card img { width: 38px; height: 38px; object-fit: contain; margin-bottom: 8px; }
    .tool-card p { font-size: 0.65rem; letter-spacing: 1px; color: var(--muted); text-transform: uppercase; }

    /* ===== CONTACT ===== */
    #contact { border-top: 1px solid var(--border); padding-bottom: 60px; }

    .contact-box {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 6px; padding: 48px;
      text-align: center;
      position: relative; overflow: hidden;
    }
    .contact-box::before {
      content: '';
      position: absolute; top: -80px; left: 50%; transform: translateX(-50%);
      width: 300px; height: 300px;
      background: radial-gradient(circle, rgba(255,215,0,0.06), transparent 70%);
    }

    .contact-box h3 {
      font-family: var(--font-head); font-size: 1.8rem; font-weight: 800;
      color: #fff; margin-bottom: 12px;
    }
    .contact-box p { color: var(--muted); font-size: 0.85rem; margin-bottom: 32px; line-height: 1.8; }

    .contact-email {
      display: inline-flex; align-items: center; gap: 12px;
      background: rgba(255,215,0,0.08); border: 1px solid var(--gold);
      color: var(--gold); padding: 16px 32px; border-radius: 3px;
      text-decoration: none; font-size: 0.88rem; letter-spacing: 2px;
      transition: 0.3s; margin-bottom: 32px;
    }
    .contact-email:hover { background: rgba(255,215,0,0.15); transform: translateY(-2px); box-shadow: 0 8px 30px rgba(255,215,0,0.2); }

    .social-links { display: flex; justify-content: center; gap: 16px; }
    .social-link {
      width: 44px; height: 44px; border-radius: 4px;
      border: 1px solid var(--border);
      display: flex; align-items: center; justify-content: center;
      color: var(--muted); text-decoration: none;
      transition: 0.3s; font-size: 1.1rem;
    }
    .social-link:hover { border-color: var(--cyan); color: var(--cyan); background: rgba(0,255,255,0.08); }

    /* ===== FOOTER ===== */
    footer {
      text-align: center; padding: 24px;
      border-top: 1px solid var(--border);
      color: var(--muted); font-size: 0.72rem; letter-spacing: 2px;
    }
    footer span { color: var(--gold); }

    /* ===== MOBILE RESPONSIVE ===== */
    @media (max-width: 600px) {
      section { padding: 70px 20px; }
      .contact-box { padding: 32px 20px; }
      .hero-photo { width: 120px; height: 120px; }
    }
  </style>
</head>
<body>

<!-- ===== NAVBAR ===== -->
<nav id="navbar">
  <div class="nav-inner">
    <div class="logo">Sriram K.T</div>
    <ul class="nav-links" id="navLinks">
      <button class="close-btn" id="closeBtn">✕</button>
      <li><a href="#about">About</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#tools">Tools</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <button class="hamburger" id="hamburger">☰</button>
  </div>
</nav>

<!-- ===== HERO ===== -->
<section id="hero">
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>

  <img src="./images/Srriram photo1.jpeg" class="hero-photo" alt="Sriram K.T"
       onerror="this.src='https://ui-avatars.com/api/?name=Sriram+KT&background=FFD700&color=000&size=300'">

  <div class="hero-tag">// Full Stack Developer</div>
  <h1>Sriram K.T</h1>
  <div class="hero-subtitle">Python · Django · React</div>
  <div class="typing-wrap" id="typingText"><span class="cursor">|</span></div>
  <div class="hero-btns">
    <a href="#projects" class="btn-primary">View Projects</a>
    <a href="#contact" class="btn-ghost">Get In Touch</a>
  </div>

  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ===== ABOUT ===== -->
<section id="about">
  <div class="reveal">
    <div class="section-label">01 — About Me</div>
    <h2 class="section-title">Who I <span>Am</span></h2>
    <div class="about-grid">
      <div class="about-text">
        <p>
          I'm a <strong>B.Com (Computer Applications)</strong> graduate with a deep passion
          for full-stack development. I specialise in building clean, scalable web applications
          using <strong>Python & Django</strong> on the backend and <strong>React</strong> on the frontend.
        </p>
        <p>
          From designing REST APIs to crafting pixel-perfect UIs, I enjoy every layer of the
          stack. I've built real-world projects including a full student management system with
          authentication, attendance tracking, and grade management.
        </p>
        <p>
          Currently based in <strong>Chennai, India</strong> and open to exciting opportunities.
        </p>
      </div>
      <div class="about-stats">
        <div class="stat-box">
          <div class="stat-num">2+</div>
          <div class="stat-label">Projects Built</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">7+</div>
          <div class="stat-label">Tech Skills</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">Full</div>
          <div class="stat-label">Stack Dev</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">∞</div>
          <div class="stat-label">Curiosity</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ===== SKILLS ===== -->
<section id="skills">
  <div class="reveal">
    <div class="section-label">02 — Technical Skills</div>
    <h2 class="section-title">My <span>Stack</span></h2>

    <div class="skills-tabs">
      <button class="tab-btn active" data-filter="all">All</button>
      <button class="tab-btn" data-filter="frontend">Frontend</button>
      <button class="tab-btn" data-filter="backend">Backend</button>
      <button class="tab-btn" data-filter="database">Database</button>
    </div>

    <div class="skills-grid" id="skillsGrid">
      <!-- Frontend -->
      <div class="skill-card" data-category="frontend">
        <img src="./images/REACT-JS.webp" alt="React"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/1126/1126012.png'">
        <p>React JS</p>
      </div>
      <div class="skill-card" data-category="frontend">
        <img src="./images/JAVASCRIPT.webp" alt="JavaScript"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/5968/5968292.png'">
        <p>JavaScript</p>
      </div>
      <div class="skill-card" data-category="frontend">
        <img src="./images/HTML.webp" alt="HTML"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/732/732212.png'">
        <p>HTML5</p>
      </div>
      <div class="skill-card" data-category="frontend">
        <img src="./images/CSS.png" alt="CSS"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/732/732190.png'">
        <p>CSS3</p>
      </div>
      <!-- Backend -->
      <div class="skill-card" data-category="backend">
        <img src="./images/python.png" alt="Python"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/5968/5968350.png'">
        <p>Python</p>
      </div>
      <div class="skill-card" data-category="backend">
        <img src="./images/django-icon.svg" alt="Django"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/9307/9307629.png'">
        <p>Django</p>
      </div>
      <!-- Database -->
      <div class="skill-card" data-category="database">
        <img src="./images/SQL.png" alt="MySQL"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/919/919836.png'">
        <p>MySQL</p>
      </div>
      <!-- Bonus -->
      <div class="skill-card" data-category="frontend">
        <img src="./images/MS-OFFICE.webp" alt="MS Office"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/732/732221.png'">
        <p>MS Office</p>
      </div>
    </div>
  </div>
</section>

<!-- ===== PROJECTS ===== -->
<section id="projects">
  <div class="reveal">
    <div class="section-label">03 — Work</div>
    <h2 class="section-title">Featured <span>Projects</span></h2>

    <div class="projects-grid">

      <!-- Student Management -->
      <div class="project-card">
        <div class="project-img-wrap">
          <img src="./images/Student management image.png" alt="Student Management System"
               onerror="this.src='https://via.placeholder.com/600x340/0d0d0d/FFD700?text=Student+Management'">
          <div class="project-overlay"></div>
          <span class="project-tag">Live</span>
        </div>
        <div class="project-body">
          <h3>Student Management System</h3>
          <p>Full-stack application with user authentication, real-time attendance tracking, marks management, and an interactive dashboard.</p>
          <div class="project-chips">
            <span class="chip">Django</span>
            <span class="chip">React</span>
            <span class="chip">MySQL</span>
            <span class="chip">REST API</span>
          </div>
          <a href="https://student-management-frontend-2cuu.onrender.com" target="_blank" class="project-link">
            View Live Project
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M7 17L17 7M17 7H7M17 7v10"/>
            </svg>
          </a>
        </div>
      </div>

      <!-- Game Store -->
      <div class="project-card">
        <div class="project-img-wrap">
          <img src="./images/Game store image.jpeg" alt="Game Store Website"
               onerror="this.src='https://via.placeholder.com/600x340/0d0d0d/00FFFF?text=Game+Store'">
          <div class="project-overlay"></div>
          <span class="project-tag">Live</span>
        </div>
        <div class="project-body">
          <h3>Game Store Website</h3>
          <p>Responsive e-commerce UI for a gaming store with interactive cart functionality, product listings, and a clean modern design.</p>
          <div class="project-chips">
            <span class="chip">HTML</span>
            <span class="chip">CSS</span>
            <span class="chip">JavaScript</span>
          </div>
          <a href="https://srriram04.github.io/game-store-website/" target="_blank" class="project-link">
            View Live Project
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M7 17L17 7M17 7H7M17 7v10"/>
            </svg>
          </a>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ===== TOOLS ===== -->
<section id="tools">
  <div class="reveal">
    <div class="section-label">04 — Dev Environment</div>
    <h2 class="section-title">My <span>Tools</span></h2>
    <div class="tools-grid">
      <div class="tool-card">
        <img src="./images/VS_code.jpeg" alt="VS Code"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/906/906324.png'">
        <p>VS Code</p>
      </div>
      <div class="tool-card">
        <img src="./images/Git-Icon.png" alt="Git"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/733/733553.png'">
        <p>Git</p>
      </div>
      <div class="tool-card">
        <img src="./images/github_logo.webp" alt="GitHub"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/733/733553.png'">
        <p>GitHub</p>
      </div>
      <div class="tool-card">
        <img src="./images/postman.png" alt="Postman"
             onerror="this.src='https://cdn-icons-png.flaticon.com/512/5968/5968532.png'">
        <p>Postman</p>
      </div>
    </div>
  </div>
</section>

<!-- ===== CONTACT ===== -->
<section id="contact">
  <div class="reveal">
    <div class="section-label">05 — Contact</div>
    <h2 class="section-title">Let's <span>Connect</span></h2>
    <div class="contact-box">
      <h3>Open to Opportunities</h3>
      <p>
        Whether you have a job offer, freelance project, or just want to say hello —<br>
        my inbox is always open.
      </p>
      <a href="mailto:sriram04@gmail.com" class="contact-email">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <rect x="2" y="4" width="20" height="16" rx="2"/>
          <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
        </svg>
        sriram04@gmail.com
      </a>
      <br><br>
      <div class="social-links">
        <a href="https://github.com/srriram04" target="_blank" class="social-link" title="GitHub">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.48 2 2 6.58 2 12.26c0 4.53 2.87 8.37 6.84 9.73.5.09.68-.22.68-.49v-1.71C6.73 20.35 6.14 18.5 6.14 18.5c-.45-1.17-1.1-1.48-1.1-1.48-.9-.63.07-.62.07-.62 1 .07 1.52 1.05 1.52 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.07 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.3.1-2.71 0 0 .84-.28 2.75 1.05A9.38 9.38 0 0 1 12 7.4c.85 0 1.7.12 2.5.34 1.91-1.33 2.75-1.05 2.75-1.05.55 1.41.2 2.45.1 2.71.64.72 1.03 1.63 1.03 2.75 0 3.94-2.34 4.81-4.57 5.06.36.32.68.94.68 1.9v2.82c0 .27.18.59.69.49A10.27 10.27 0 0 0 22 12.26C22 6.58 17.52 2 12 2z"/>
          </svg>
        </a>
        <a href="https://tinyurl.com/33tfcc2b" target="_blank" class="social-link" title="LinkedIn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
            <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z"/>
            <circle cx="4" cy="4" r="2"/>
          </svg>
        </a>
      </div>
    </div>
  </div>
</section>

<!-- ===== FOOTER ===== -->
<footer>
  <p>© 2026 <span>Sriram K.T</span> — Crafted with passion in Chennai 🇮🇳</p>
</footer>

<script>
  // ===== TYPING ANIMATION =====
  const phrases = [
    "Building scalable web apps with Django & React",
    "Turning ideas into production-ready code",
    "Full Stack Developer · Open to work",
  ];
  let phraseIdx = 0, charIdx = 0, deleting = false;
  const el = document.getElementById("typingText");

  function type() {
    const current = phrases[phraseIdx];
    if (!deleting) {
      el.innerHTML = current.substring(0, charIdx + 1) + '<span class="cursor">|</span>';
      charIdx++;
      if (charIdx === current.length) {
        deleting = true;
        setTimeout(type, 2000);
        return;
      }
    } else {
      el.innerHTML = current.substring(0, charIdx - 1) + '<span class="cursor">|</span>';
      charIdx--;
      if (charIdx === 0) {
        deleting = false;
        phraseIdx = (phraseIdx + 1) % phrases.length;
      }
    }
    setTimeout(type, deleting ? 40 : 70);
  }
  setTimeout(type, 1400);

  // ===== NAVBAR SCROLL =====
  window.addEventListener("scroll", () => {
    document.getElementById("navbar").classList.toggle("scrolled", window.scrollY > 50);
  });

  // ===== HAMBURGER =====
  const ham = document.getElementById("hamburger");
  const navLinks = document.getElementById("navLinks");
  const closeBtn = document.getElementById("closeBtn");

  ham.addEventListener("click", () => {
    navLinks.classList.toggle("open");
    ham.textContent = navLinks.classList.contains("open") ? "✕" : "☰";
  });
  closeBtn.addEventListener("click", () => {
    navLinks.classList.remove("open");
    ham.textContent = "☰";
  });
  navLinks.querySelectorAll("a").forEach(a => {
    a.addEventListener("click", () => {
      navLinks.classList.remove("open");
      ham.textContent = "☰";
    });
  });

  // ===== SCROLL REVEAL =====
  const revealEls = document.querySelectorAll(".reveal");
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add("visible"); } });
  }, { threshold: 0.1 });
  revealEls.forEach(el => observer.observe(el));

  // ===== SKILLS FILTER =====
  const tabs = document.querySelectorAll(".tab-btn");
  const cards = document.querySelectorAll(".skill-card");
  tabs.forEach(tab => {
    tab.addEventListener("click", () => {
      tabs.forEach(t => t.classList.remove("active"));
      tab.classList.add("active");
      const filter = tab.dataset.filter;
      cards.forEach(card => {
        if (filter === "all" || card.dataset.category === filter) {
          card.style.display = "block";
          card.style.animation = "fadeUp 0.4s forwards";
        } else {
          card.style.display = "none";
        }
      });
    });
  });
</script>
</body>
</html>
