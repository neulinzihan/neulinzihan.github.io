---
permalink: /
layout: null
redirect_from: 
  - /about/
  - /about.html
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    /* ===== Reset ===== */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, Arial, sans-serif;
      color: #333;
      line-height: 1.6;
    }
    
    /* ===== 滚动进度条 ===== */
    .scroll-indicator {
      position: fixed;
      top: 0;
      left: 0;
      height: 4px;
      background: linear-gradient(90deg, #3498db, #9b59b6);
      width: 0%;
      z-index: 1000;
    }
    
    /* ===== 导航栏 ===== */
    .navbar {
      position: fixed;
      top: 0;
      width: 100%;
      background: rgba(255,255,255,0.95);
      backdrop-filter: blur(10px);
      padding: 15px 50px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 999;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }
    
    .navbar.hidden { transform: translateY(-100%); }
    
    .nav-logo {
      font-size: 1.5rem;
      font-weight: 700;
      color: #2c3e50;
      text-decoration: none;
    }
    
    .nav-links a {
      margin-left: 30px;
      text-decoration: none;
      color: #555;
      font-weight: 500;
      transition: color 0.3s;
    }
    
    .nav-links a:hover { color: #3498db; }
    
    /* ===== Hero ===== */
    .hero {
      height: 100vh;
      background: linear-gradient(135deg, rgba(44,62,80,0.9), rgba(52,152,219,0.8)),
                  url('{{ site.baseurl }}/images/hero-bg.jpg') center/cover fixed;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      color: white;
      position: relative;
    }
    
    .hero-content h1 {
      font-size: 4rem;
      margin-bottom: 1rem;
      animation: fadeInUp 1s ease;
    }
    
    .hero-content h1 span {
      background: linear-gradient(90deg, #fff, #74b9ff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    
    .hero-content .subtitle {
      font-size: 1.5rem;
      opacity: 0.9;
      margin-bottom: 1.5rem;
      animation: fadeInUp 1s ease 0.2s both;
    }
    
    .hero-content .tagline {
      font-size: 1.1rem;
      opacity: 0.8;
      max-width: 600px;
      margin: 0 auto 2rem;
      animation: fadeInUp 1s ease 0.4s both;
    }
    
    .hero-buttons { animation: fadeInUp 1s ease 0.6s both; }
    
    .hero-buttons a {
      display: inline-block;
      padding: 12px 30px;
      margin: 0 10px;
      border-radius: 30px;
      text-decoration: none;
      font-weight: 600;
      transition: all 0.3s;
    }
    
    .btn-primary { background: white; color: #2c3e50; }
    .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(0,0,0,0.2); }
    .btn-secondary { border: 2px solid white; color: white; }
    .btn-secondary:hover { background: white; color: #2c3e50; }
    
    .scroll-down {
      position: absolute;
      bottom: 30px;
      left: 50%;
      transform: translateX(-50%);
      animation: bounce 2s infinite;
    }
    
    .scroll-down i { font-size: 2rem; color: white; opacity: 0.7; }
    
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    @keyframes bounce {
      0%, 100% { transform: translateX(-50%) translateY(0); }
      50% { transform: translateX(-50%) translateY(10px); }
    }
    
    /* ===== Sections ===== */
    .section {
      padding: 100px 20px;
      max-width: 1100px;
      margin: 0 auto;
    }
    
    .section-title {
      font-size: 2.5rem;
      color: #2c3e50;
      margin-bottom: 50px;
      text-align: center;
      position: relative;
    }
    
    .section-title::after {
      content: '';
      position: absolute;
      bottom: -15px;
      left: 50%;
      transform: translateX(-50%);
      width: 60px;
      height: 4px;
      background: linear-gradient(90deg, #3498db, #9b59b6);
      border-radius: 2px;
    }
    
    /* ===== 滚动动画 ===== */
    .scroll-reveal, .scroll-zoom, .scroll-left, .scroll-right {
      opacity: 0;
      transition: all 0.8s ease;
    }
    
    .scroll-reveal { transform: translateY(40px); }
    .scroll-zoom { transform: scale(0.9); }
    .scroll-left { transform: translateX(-60px); }
    .scroll-right { transform: translateX(60px); }
    
    .scroll-reveal.visible, .scroll-zoom.visible, .scroll-left.visible, .scroll-right.visible {
      opacity: 1;
      transform: translateY(0) translateX(0) scale(1);
    }
    
    /* ===== About ===== */
    .about-content {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 60px;
      align-items: center;
    }
    
    .about-image { position: relative; }
    
    .about-image img {
      width: 100%;
      border-radius: 20px;
      box-shadow: 0 20px 50px rgba(0,0,0,0.15);
    }
    
    .about-image::before {
      content: '';
      position: absolute;
      top: -20px;
      left: -20px;
      right: 20px;
      bottom: 20px;
      border: 3px solid #3498db;
      border-radius: 20px;
      z-index: -1;
    }
    
    .about-text p { font-size: 1.1rem; color: #555; margin-bottom: 1.5rem; }
    .about-text .highlight { color: #3498db; font-weight: 600; }
    
    .status-badge {
      display: inline-block;
      background: linear-gradient(135deg, #00b894, #00cec9);
      color: white;
      padding: 10px 20px;
      border-radius: 30px;
      font-weight: 600;
      margin-top: 1rem;
    }
    
    .status-badge i { margin-right: 8px; }
    
    /* ===== News ===== */
    .news-section { background: #f8f9fa; }
    
    .news-list { max-width: 800px; margin: 0 auto; }
    
    .news-item {
      display: flex;
      align-items: flex-start;
      padding: 25px;
      background: white;
      border-radius: 15px;
      margin-bottom: 20px;
      box-shadow: 0 5px 20px rgba(0,0,0,0.05);
      transition: transform 0.3s, box-shadow 0.3s;
    }
    
    .news-item:hover {
      transform: translateX(10px);
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    }
    
    .news-date {
      background: linear-gradient(135deg, #3498db, #9b59b6);
      color: white;
      padding: 10px 15px;
      border-radius: 10px;
      font-weight: 700;
      font-size: 0.9rem;
      min-width: 100px;
      text-align: center;
      margin-right: 20px;
    }
    
    .news-content h4 { color: #2c3e50; margin-bottom: 5px; }
    .news-content p { color: #666; font-size: 0.95rem; }
    
    /* ===== Interests ===== */
    .interests-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 30px;
    }
    
    .interest-card {
      background: white;
      padding: 40px 25px;
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 10px 30px rgba(0,0,0,0.08);
      transition: all 0.3s;
    }
    
    .interest-card:hover {
      transform: translateY(-10px);
      box-shadow: 0 20px 50px rgba(0,0,0,0.15);
    }
    
    .interest-card i {
      font-size: 3rem;
      background: linear-gradient(135deg, #3498db, #9b59b6);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 20px;
    }
    
    .interest-card h3 { color: #2c3e50; font-size: 1.1rem; }
    
    /* ===== Parallax ===== */
    .parallax-divider {
      height: 50vh;
      background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
                  url('https://images.unsplash.com/photo-1518770660439-4636190af475?w=1920') center/cover fixed;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      text-align: center;
    }
    
    .parallax-divider h2 { font-size: 3rem; margin-bottom: 1rem; }
    .parallax-divider p { font-size: 1.2rem; opacity: 0.9; }
    
    /* ===== Projects ===== */
    .project-card {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 50px;
      align-items: center;
      margin-bottom: 80px;
      padding: 40px;
      background: white;
      border-radius: 20px;
      box-shadow: 0 15px 40px rgba(0,0,0,0.08);
    }
    
    .project-card:nth-child(even) { direction: rtl; }
    .project-card:nth-child(even) > * { direction: ltr; }
    
    .project-image { border-radius: 15px; overflow: hidden; }
    
    .project-image img {
      width: 100%;
      height: 280px;
      object-fit: cover;
      transition: transform 0.5s;
    }
    
    .project-card:hover .project-image img { transform: scale(1.05); }
    
    .project-info .project-date { color: #3498db; font-weight: 600; font-size: 0.9rem; margin-bottom: 10px; }
    .project-info h3 { font-size: 1.5rem; color: #2c3e50; margin-bottom: 15px; }
    .project-info p { color: #666; line-height: 1.8; }
    
    .project-tags { margin-top: 20px; }
    
    .project-tags span {
      display: inline-block;
      background: #e8f4fc;
      color: #3498db;
      padding: 5px 15px;
      border-radius: 20px;
      font-size: 0.85rem;
      margin-right: 10px;
      margin-bottom: 10px;
    }
    
    /* ===== Timeline ===== */
    .timeline {
      position: relative;
      max-width: 900px;
      margin: 0 auto;
    }
    
    .timeline::before {
      content: '';
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      width: 4px;
      height: 100%;
      background: linear-gradient(to bottom, #3498db, #9b59b6);
      border-radius: 2px;
    }
    
    .timeline-item {
      display: flex;
      justify-content: flex-end;
      padding-right: 50%;
      position: relative;
      margin-bottom: 50px;
    }
    
    .timeline-item:nth-child(even) {
      justify-content: flex-start;
      padding-right: 0;
      padding-left: 50%;
    }
    
    .timeline-item::before {
      content: '';
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      width: 20px;
      height: 20px;
      background: white;
      border: 4px solid #3498db;
      border-radius: 50%;
      z-index: 1;
    }
    
    .timeline-content {
      background: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.08);
      width: 90%;
      margin-right: 30px;
      transition: all 0.3s;
    }
    
    .timeline-item:nth-child(even) .timeline-content { margin-right: 0; margin-left: 30px; }
    
    .timeline-content:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 40px rgba(0,0,0,0.12);
    }
    
    .timeline-content .date { color: #3498db; font-weight: 700; margin-bottom: 10px; }
    .timeline-content h3 { color: #2c3e50; margin-bottom: 5px; }
    .timeline-content .company { color: #9b59b6; font-weight: 500; margin-bottom: 10px; }
    .timeline-content p { color: #666; font-size: 0.95rem; }
    
    /* ===== Education ===== */
    .education-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 40px;
    }
    
    .education-card {
      background: white;
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 15px 40px rgba(0,0,0,0.08);
      position: relative;
      overflow: hidden;
      transition: all 0.3s;
    }
    
    .education-card:hover {
      transform: translateY(-10px);
      box-shadow: 0 20px 50px rgba(0,0,0,0.12);
    }
    
    .education-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 5px;
      background: linear-gradient(90deg, #3498db, #9b59b6);
    }
    
    .education-card .degree { font-size: 1.3rem; color: #2c3e50; font-weight: 700; margin-bottom: 10px; }
    .education-card .school { color: #3498db; font-weight: 600; margin-bottom: 5px; }
    .education-card .year { color: #999; font-size: 0.9rem; }
    
    /* ===== Skills ===== */
    .skills-section { background: #f8f9fa; }
    
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 30px;
    }
    
    .skill-category {
      background: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.05);
    }
    
    .skill-category h3 {
      color: #2c3e50;
      margin-bottom: 20px;
      display: flex;
      align-items: center;
    }
    
    .skill-category h3 i { margin-right: 10px; color: #3498db; }
    
    .skill-bar { margin-bottom: 15px; }
    
    .skill-bar .skill-name {
      display: flex;
      justify-content: space-between;
      margin-bottom: 8px;
      font-size: 0.9rem;
      color: #555;
    }
    
    .skill-bar .bar {
      height: 8px;
      background: #e0e0e0;
      border-radius: 4px;
      overflow: hidden;
    }
    
    .skill-bar .progress {
      height: 100%;
      background: linear-gradient(90deg, #3498db, #9b59b6);
      border-radius: 4px;
      width: 0;
      transition: width 1.5s ease;
    }
    
    .skill-bar.visible .progress { width: var(--progress); }
    
    /* ===== CTA ===== */
    .cta-section {
      background: linear-gradient(135deg, #2c3e50, #3498db);
      color: white;
      text-align: center;
      padding: 100px 20px;
    }
    
    .cta-section h2 { font-size: 2.5rem; margin-bottom: 1rem; }
    .cta-section p { font-size: 1.2rem; opacity: 0.9; margin-bottom: 2rem; }
    
    .cta-buttons a {
      display: inline-block;
      padding: 15px 40px;
      margin: 0 10px;
      border-radius: 30px;
      text-decoration: none;
      font-weight: 600;
      transition: all 0.3s;
    }
    
    .cta-buttons .btn-white { background: white; color: #2c3e50; }
    .cta-buttons .btn-outline { border: 2px solid white; color: white; }
    .cta-buttons a:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(0,0,0,0.2); }
    
    /* ===== Footer ===== */
    .site-footer {
      background: #1a252f;
      color: white;
      padding: 60px 20px 30px;
    }
    
    .footer-content {
      max-width: 1100px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: 2fr 1fr 1fr;
      gap: 50px;
    }
    
    .footer-about h3 { font-size: 1.5rem; margin-bottom: 15px; }
    .footer-about p { color: #aaa; line-height: 1.8; }
    
    .footer-links h4, .footer-contact h4 { margin-bottom: 20px; font-size: 1.1rem; }
    .footer-links ul { list-style: none; }
    .footer-links a { color: #aaa; text-decoration: none; display: block; padding: 8px 0; transition: color 0.3s; }
    .footer-links a:hover { color: #3498db; }
    
    .footer-contact p { color: #aaa; margin-bottom: 10px; }
    .footer-contact i { margin-right: 10px; color: #3498db; }
    
    .social-links { margin-top: 20px; }
    
    .social-links a {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 40px;
      height: 40px;
      background: #2c3e50;
      border-radius: 50%;
      margin-right: 10px;
      color: white;
      transition: all 0.3s;
    }
    
    .social-links a:hover { background: #3498db; transform: translateY(-3px); }
    
    .footer-bottom {
      max-width: 1100px;
      margin: 40px auto 0;
      padding-top: 30px;
      border-top: 1px solid #2c3e50;
      text-align: center;
      color: #666;
    }
    
    /* ===== 响应式 ===== */
    @media (max-width: 992px) {
      .about-content, .project-card, .education-grid, .skills-grid, .footer-content { grid-template-columns: 1fr; }
      .interests-grid { grid-template-columns: repeat(2, 1fr); }
      
      .timeline::before { left: 20px; }
      .timeline-item, .timeline-item:nth-child(even) { padding-left: 60px; padding-right: 0; justify-content: flex-start; }
      .timeline-item::before { left: 20px; }
      .timeline-content, .timeline-item:nth-child(even) .timeline-content { margin-left: 0; margin-right: 0; width: 100%; }
      .footer-content { text-align: center; }
    }
    
    @media (max-width: 768px) {
      .navbar { padding: 15px 20px; }
      .nav-links { display: none; }
      .hero-content h1 { font-size: 2.5rem; }
      .interests-grid { grid-template-columns: 1fr; }
      .project-card:nth-child(even) { direction: ltr; }
    }
  </style>
</head>
<body>

  <div class="scroll-indicator" id="scrollIndicator"></div>

  <nav class="navbar" id="navbar">
    <a href="/" class="nav-logo">Zihan Lin</a>
    <div class="nav-links">
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
      <a href="#experience">Experience</a>
      <a href="{{ site.baseurl }}/cv/">CV</a>
      <a href="{{ site.baseurl }}/publications/">Publications</a>
    </div>
  </nav>

  <section class="hero">
    <div class="hero-content">
      <h1>Hello, I'm <span>Zihan!</span></h1>
      <p class="subtitle">Robotics Engineer | AI & Mechatronics</p>
      <p class="tagline">M.S. in Robotics from Northeastern University with research interests in reinforcement learning, mechatronic systems, and healthcare technology.</p>
      <div class="hero-buttons">
        <a href="{{ site.baseurl }}/cv/" class="btn-primary">View CV</a>
        <a href="#projects" class="btn-secondary">See Projects</a>
      </div>
    </div>
    <div class="scroll-down"><i class="fas fa-chevron-down"></i></div>
  </section>

  <section class="section" id="about">
    <h2 class="section-title scroll-reveal">About Me</h2>
    <div class="about-content">
      <div class="about-image scroll-left">
        <img src="{{ site.baseurl }}/images/zihan_linkedin_avatar.jpeg" alt="Zihan Lin">
      </div>
      <div class="about-text scroll-right">
        <p>I am a <span class="highlight">Robotics M.S. graduate</span> from Northeastern University with a B.S. in Mechanical Engineering.</p>
        <p>My research interests span <span class="highlight">robotics</span>, <span class="highlight">reinforcement learning</span>, <span class="highlight">mechatronic systems</span>, and <span class="highlight">healthcare technology</span>.</p>
        <p>I combine hands-on engineering experience from SharkNinja and HiRain Technologies with academic research in soft material mechanics and AI-driven robotics.</p>
        <div class="status-badge">
          <i class="fas fa-briefcase"></i>
          Seeking full-time opportunities starting Jan 2026
        </div>
      </div>
    </div>
  </section>

  <section class="section news-section">
    <h2 class="section-title scroll-reveal">Latest News</h2>
    <div class="news-list">
      <div class="news-item scroll-reveal">
        <div class="news-date">Aug 2025</div>
        <div class="news-content">
          <h4>🎓 Graduation</h4>
          <p>Completed M.S. in Robotics at Northeastern University</p>
        </div>
      </div>
      <div class="news-item scroll-reveal">
        <div class="news-date">May 2025</div>
        <div class="news-content">
          <h4>🤖 AI/RL Project</h4>
          <p>Finished drone coverage optimization project using Q-learning</p>
        </div>
      </div>
      <div class="news-item scroll-reveal">
        <div class="news-date">Dec 2024</div>
        <div class="news-content">
          <h4>👁️ Assistive Tech</h4>
          <p>Developed wearable assistive navigation system for visually impaired users</p>
        </div>
      </div>
    </div>
  </section>

  <section class="section">
    <h2 class="section-title scroll-reveal">Research Interests</h2>
    <div class="interests-grid">
      <div class="interest-card scroll-zoom"><i class="fas fa-robot"></i><h3>Robotics & Mechatronics</h3></div>
      <div class="interest-card scroll-zoom"><i class="fas fa-brain"></i><h3>Reinforcement Learning & AI</h3></div>
      <div class="interest-card scroll-zoom"><i class="fas fa-heartbeat"></i><h3>Healthcare & Assistive Tech</h3></div>
      <div class="interest-card scroll-zoom"><i class="fas fa-drafting-compass"></i><h3>CAD & Simulation</h3></div>
    </div>
  </section>

  <section class="parallax-divider" id="projects">
    <div class="scroll-reveal">
      <h2>Selected Projects</h2>
      <p>Innovative solutions in robotics, AI, and healthcare</p>
    </div>
  </section>

  <section class="section">
    <div class="project-card scroll-reveal">
      <div class="project-image"><img src="https://images.unsplash.com/photo-1473968512647-3e447244af8f?w=600" alt="Drone"></div>
      <div class="project-info">
        <div class="project-date">Spring 2025</div>
        <h3>Drone Coverage Optimization with Reinforcement Learning</h3>
        <p>Designed a Q-learning-based drone placement policy achieving 100% area coverage with only 4 drones, outperforming PPO and MCTS baselines. Implemented A* pathfinding for emergency responder navigation.</p>
        <div class="project-tags"><span>Q-Learning</span><span>Python</span><span>A* Pathfinding</span></div>
      </div>
    </div>
    
    <div class="project-card scroll-reveal">
      <div class="project-image"><img src="https://images.unsplash.com/photo-1581092160562-40aa08e78837?w=600" alt="Wearable"></div>
      <div class="project-info">
        <div class="project-date">Fall 2024</div>
        <h3>Wearable Assistive Navigation System</h3>
        <p>Built a real-time obstacle detection system using ToF depth camera and Raspberry Pi with haptic feedback for visually impaired users.</p>
        <div class="project-tags"><span>Raspberry Pi</span><span>ToF Camera</span><span>Haptic Feedback</span></div>
      </div>
    </div>
    
    <div class="project-card scroll-reveal">
      <div class="project-image"><img src="https://images.unsplash.com/photo-1559757175-5700dde675bc?w=600" alt="Medical"></div>
      <div class="project-info">
        <div class="project-date">Spring 2024</div>
        <h3>Robotic Finger for Tumor Detection</h3>
        <p>Designed a flexible robotic finger with dual IMU sensors to detect subdermal inclusions, demonstrating potential for home-use biomedical diagnostics.</p>
        <div class="project-tags"><span>IMU Sensors</span><span>Kalman Filter</span><span>Medical Robotics</span></div>
      </div>
    </div>
  </section>

  <section class="section" id="experience">
    <h2 class="section-title scroll-reveal">Experience</h2>
    <div class="timeline">
      <div class="timeline-item scroll-left">
        <div class="timeline-content">
          <div class="date">2022 - 2025</div>
          <h3>Part-time Lab Researcher</h3>
          <div class="company">Northeastern University</div>
          <p>Soft material mechanics research. Published in European Journal of Mechanics.</p>
        </div>
      </div>
      <div class="timeline-item scroll-right">
        <div class="timeline-content">
          <div class="date">2023</div>
          <h3>Mechanical Engineering Co-op</h3>
          <div class="company">HiRain Technologies, Beijing</div>
          <p>PCB quality assurance, CAD modeling in SolidWorks/CREO.</p>
        </div>
      </div>
      <div class="timeline-item scroll-left">
        <div class="timeline-content">
          <div class="date">2021</div>
          <h3>Production/Design Engineer Co-op</h3>
          <div class="company">SharkNinja, Needham MA</div>
          <p>CFD simulation, 3D printing prototypes, sensor integration.</p>
        </div>
      </div>
    </div>
  </section>

  <section class="section">
    <h2 class="section-title scroll-reveal">Education</h2>
    <div class="education-grid">
      <div class="education-card scroll-left">
        <div class="degree">M.S. in Robotics</div>
        <div class="school">Northeastern University</div>
        <div class="year">2024 - 2025 | GPA: 3.67</div>
      </div>
      <div class="education-card scroll-right">
        <div class="degree">B.S. in Mechanical Engineering</div>
        <div class="school">Northeastern University</div>
        <div class="year">2019 - 2023 | Minor in Math</div>
      </div>
    </div>
  </section>

  <section class="section skills-section">
    <h2 class="section-title scroll-reveal">Technical Skills</h2>
    <div class="skills-grid">
      <div class="skill-category scroll-reveal">
        <h3><i class="fas fa-code"></i> Programming</h3>
        <div class="skill-bar" style="--progress: 90%"><div class="skill-name"><span>Python</span><span>90%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 85%"><div class="skill-name"><span>MATLAB</span><span>85%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 70%"><div class="skill-name"><span>C++</span><span>70%</span></div><div class="bar"><div class="progress"></div></div></div>
      </div>
      <div class="skill-category scroll-reveal">
        <h3><i class="fas fa-cube"></i> CAD & Simulation</h3>
        <div class="skill-bar" style="--progress: 85%"><div class="skill-name"><span>SolidWorks</span><span>85%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 80%"><div class="skill-name"><span>Simulink</span><span>80%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 75%"><div class="skill-name"><span>AutoCAD</span><span>75%</span></div><div class="bar"><div class="progress"></div></div></div>
      </div>
      <div class="skill-category scroll-reveal">
        <h3><i class="fas fa-microchip"></i> Hardware</h3>
        <div class="skill-bar" style="--progress: 80%"><div class="skill-name"><span>Arduino</span><span>80%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 75%"><div class="skill-name"><span>Raspberry Pi</span><span>75%</span></div><div class="bar"><div class="progress"></div></div></div>
        <div class="skill-bar" style="--progress: 70%"><div class="skill-name"><span>ROS</span><span>70%</span></div><div class="bar"><div class="progress"></div></div></div>
      </div>
    </div>
  </section>

  <section class="cta-section">
    <h2 class="scroll-reveal">Let's Connect!</h2>
    <p class="scroll-reveal">Interested in robotics, AI, or collaboration?</p>
    <div class="cta-buttons scroll-reveal">
      <a href="{{ site.baseurl }}/cv/" class="btn-white">View Full CV</a>
      <a href="{{ site.baseurl }}/publications/" class="btn-outline">Publications</a>
    </div>
  </section>

  <footer class="site-footer">
    <div class="footer-content">
      <div class="footer-about">
        <h3>Zihan Lin</h3>
        <p>Robotics M.S. graduate passionate about building intelligent systems that improve lives.</p>
        <div class="social-links">
          <a href="https://github.com/neulinzihan"><i class="fab fa-github"></i></a>
          <a href="https://linkedin.com/in/zihanlin"><i class="fab fa-linkedin-in"></i></a>
          <a href="https://scholar.google.com/citations?user=0Yic6NcAAAAJ"><i class="fas fa-graduation-cap"></i></a>
        </div>
      </div>
      <div class="footer-links">
        <h4>Quick Links</h4>
        <ul>
          <li><a href="#about">About</a></li>
          <li><a href="#projects">Projects</a></li>
          <li><a href="{{ site.baseurl }}/cv/">CV</a></li>
          <li><a href="{{ site.baseurl }}/publications/">Publications</a></li>
        </ul>
      </div>
      <div class="footer-contact">
        <h4>Contact</h4>
        <p><i class="fas fa-envelope"></i> lin.zihan@northeastern.edu</p>
        <p><i class="fas fa-map-marker-alt"></i> Boston, MA</p>
      </div>
    </div>
    <div class="footer-bottom"><p>© 2025 Zihan Lin. All rights reserved.</p></div>
  </footer>

  <script>
    window.addEventListener('scroll', () => {
      const scrollTop = window.scrollY;
      const docHeight = document.documentElement.scrollHeight - window.innerHeight;
      document.getElementById('scrollIndicator').style.width = (scrollTop / docHeight) * 100 + '%';
    });

    let lastScroll = 0;
    window.addEventListener('scroll', () => {
      const navbar = document.getElementById('navbar');
      if (window.scrollY > lastScroll && window.scrollY > 100) navbar.classList.add('hidden');
      else navbar.classList.remove('hidden');
      lastScroll = window.scrollY;
    });

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => { if (entry.isIntersecting) entry.target.classList.add('visible'); });
    }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

    document.querySelectorAll('.scroll-reveal, .scroll-zoom, .scroll-left, .scroll-right, .skill-bar').forEach(el => observer.observe(el));

    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) target.scrollIntoView({ behavior: 'smooth' });
      });
    });
  </script>

</body>
</html>