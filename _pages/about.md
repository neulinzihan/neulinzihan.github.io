---
permalink: /
title: "Hello, I'm Zihan!"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<style>
/* ===== 滚动动画 ===== */
.scroll-reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease;
}
.scroll-reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

.scroll-zoom {
  opacity: 0;
  transform: scale(0.95);
  transition: all 0.8s ease;
}
.scroll-zoom.visible {
  opacity: 1;
  transform: scale(1);
}

.scroll-left {
  opacity: 0;
  transform: translateX(-40px);
  transition: all 0.8s ease;
}
.scroll-left.visible {
  opacity: 1;
  transform: translateX(0);
}

/* ===== 状态徽章 ===== */
.status-badge {
  display: inline-block;
  background: linear-gradient(135deg, #00b894, #00cec9);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-weight: 600;
  font-size: 0.9rem;
  margin: 15px 0;
}

/* ===== News 卡片 ===== */
.news-item {
  display: flex;
  align-items: flex-start;
  padding: 15px;
  background: #f8f9fa;
  border-radius: 10px;
  margin-bottom: 12px;
  border-left: 4px solid #3498db;
  transition: transform 0.3s, box-shadow 0.3s;
}
.news-item:hover {
  transform: translateX(5px);
  box-shadow: 0 5px 20px rgba(0,0,0,0.1);
}
.news-date {
  background: linear-gradient(135deg, #3498db, #9b59b6);
  color: white;
  padding: 5px 12px;
  border-radius: 5px;
  font-weight: 600;
  font-size: 0.8rem;
  margin-right: 15px;
  white-space: nowrap;
}
.news-content {
  flex: 1;
}
.news-content strong {
  color: #2c3e50;
}

/* ===== Research Interest 卡片 ===== */
.interest-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 15px;
  margin: 20px 0;
}
.interest-card {
  background: linear-gradient(135deg, #f8f9fa, #fff);
  padding: 20px;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 4px 15px rgba(0,0,0,0.05);
  transition: all 0.3s;
  border: 1px solid #eee;
}
.interest-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  border-color: #3498db;
}
.interest-card i {
  font-size: 2rem;
  background: linear-gradient(135deg, #3498db, #9b59b6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 10px;
  display: block;
}

/* ===== 项目卡片 ===== */
.project-card {
  background: #fff;
  border-radius: 12px;
  padding: 25px;
  margin-bottom: 20px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.08);
  border-left: 4px solid #3498db;
  transition: all 0.3s;
}
.project-card:hover {
  transform: translateX(5px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.12);
}
.project-card h3 {
  color: #2c3e50;
  margin-bottom: 8px;
}
.project-date {
  color: #3498db;
  font-weight: 600;
  font-size: 0.85rem;
  margin-bottom: 10px;
}
.project-tags {
  margin-top: 12px;
}
.project-tags span {
  display: inline-block;
  background: #e8f4fc;
  color: #3498db;
  padding: 4px 12px;
  border-radius: 15px;
  font-size: 0.8rem;
  margin-right: 8px;
  margin-bottom: 5px;
}

/* ===== 经历时间线 ===== */
.timeline {
  position: relative;
  padding-left: 25px;
  margin: 20px 0;
}
.timeline::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 3px;
  background: linear-gradient(to bottom, #3498db, #9b59b6);
  border-radius: 2px;
}
.timeline-item {
  position: relative;
  padding: 15px 0 15px 20px;
}
.timeline-item::before {
  content: '';
  position: absolute;
  left: -31px;
  top: 20px;
  width: 12px;
  height: 12px;
  background: #3498db;
  border-radius: 50%;
  border: 3px solid white;
  box-shadow: 0 0 0 3px #3498db;
}
.timeline-item h4 {
  color: #2c3e50;
  margin-bottom: 3px;
}
.timeline-item .company {
  color: #9b59b6;
  font-weight: 500;
  font-size: 0.9rem;
}
.timeline-item .date {
  color: #3498db;
  font-size: 0.85rem;
  font-weight: 600;
}
.timeline-item p {
  color: #666;
  font-size: 0.9rem;
  margin-top: 5px;
}

/* ===== 教育卡片 ===== */
.education-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin: 20px 0;
}
.education-card {
  background: #fff;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.08);
  border-top: 4px solid #3498db;
  transition: all 0.3s;
}
.education-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.12);
}
.education-card .degree {
  font-size: 1.1rem;
  color: #2c3e50;
  font-weight: 700;
  margin-bottom: 5px;
}
.education-card .school {
  color: #3498db;
  font-weight: 500;
}
.education-card .year {
  color: #999;
  font-size: 0.85rem;
}

/* ===== 技能进度条 ===== */
.skill-section {
  margin: 20px 0;
}
.skill-bar {
  margin-bottom: 15px;
}
.skill-bar .skill-name {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
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
.skill-bar.visible .progress {
  width: var(--progress);
}

/* ===== CTA 按钮 ===== */
.cta-buttons {
  margin-top: 30px;
  text-align: center;
}
.cta-buttons a {
  display: inline-block;
  padding: 12px 30px;
  margin: 5px 10px;
  border-radius: 25px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s;
}
.btn-primary {
  background: linear-gradient(135deg, #3498db, #9b59b6);
  color: white;
}
.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(52,152,219,0.3);
}
.btn-secondary {
  background: #f8f9fa;
  color: #2c3e50;
  border: 2px solid #3498db;
}
.btn-secondary:hover {
  background: #3498db;
  color: white;
}

/* ===== 响应式 ===== */
@media (max-width: 768px) {
  .interest-grid, .education-grid {
    grid-template-columns: 1fr;
  }
  .news-item {
    flex-direction: column;
  }
  .news-date {
    margin-bottom: 10px;
  }
}
</style>

<!-- Font Awesome for icons -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<p class="scroll-reveal">
I am a <strong>Robotics M.S. graduate</strong> from Northeastern University with a B.S. in Mechanical Engineering. My research interests span <strong>robotics</strong>, <strong>reinforcement learning</strong>, <strong>mechatronic systems</strong>, and <strong>healthcare technology</strong>.
</p>

<div class="status-badge scroll-reveal">
  <i class="fas fa-briefcase"></i> Seeking full-time opportunities starting Jan 2026
</div>

## <i class="fas fa-newspaper"></i> News
{: .scroll-reveal}

<div class="news-item scroll-reveal">
  <span class="news-date">Aug 2025</span>
  <div class="news-content"><strong>🎓 Graduation</strong> — Completed M.S. in Robotics at Northeastern University</div>
</div>

<div class="news-item scroll-reveal">
  <span class="news-date">May 2025</span>
  <div class="news-content"><strong>🤖 AI/RL Project</strong> — Finished drone coverage optimization using Q-learning</div>
</div>

<div class="news-item scroll-reveal">
  <span class="news-date">Dec 2024</span>
  <div class="news-content"><strong>👁️ Assistive Tech</strong> — Developed wearable navigation system for visually impaired users</div>
</div>

## <i class="fas fa-lightbulb"></i> Research Interests
{: .scroll-reveal}

<div class="interest-grid">
  <div class="interest-card scroll-zoom">
    <i class="fas fa-robot"></i>
    <strong>Robotics & Mechatronics</strong>
  </div>
  <div class="interest-card scroll-zoom">
    <i class="fas fa-brain"></i>
    <strong>Reinforcement Learning & AI</strong>
  </div>
  <div class="interest-card scroll-zoom">
    <i class="fas fa-heartbeat"></i>
    <strong>Healthcare & Assistive Tech</strong>
  </div>
  <div class="interest-card scroll-zoom">
    <i class="fas fa-drafting-compass"></i>
    <strong>CAD & Simulation</strong>
  </div>
</div>

## <i class="fas fa-code-branch"></i> Selected Projects
{: .scroll-reveal}

<div class="project-card scroll-left">
  <div class="project-date">Spring 2025</div>
  <h3>Drone Coverage Optimization with Reinforcement Learning</h3>
  <p>Designed a Q-learning-based drone placement policy achieving 100% area coverage with only 4 drones, outperforming PPO and MCTS baselines. Implemented A* pathfinding for emergency responder navigation.</p>
  <div class="project-tags">
    <span>Q-Learning</span>
    <span>Python</span>
    <span>A* Pathfinding</span>
  </div>
</div>

<div class="project-card scroll-left">
  <div class="project-date">Fall 2024</div>
  <h3>Wearable Assistive Navigation System</h3>
  <p>Built a real-time obstacle detection system using ToF depth camera and Raspberry Pi with haptic feedback for visually impaired users.</p>
  <div class="project-tags">
    <span>Raspberry Pi</span>
    <span>ToF Camera</span>
    <span>Haptic Feedback</span>
  </div>
</div>

<div class="project-card scroll-left">
  <div class="project-date">Spring 2024</div>
  <h3>Robotic Finger for Tumor Detection</h3>
  <p>Designed a flexible robotic finger with dual IMU sensors to detect subdermal inclusions, demonstrating potential for home-use biomedical diagnostics.</p>
  <div class="project-tags">
    <span>IMU Sensors</span>
    <span>Kalman Filter</span>
    <span>Medical Robotics</span>
  </div>
</div>

## <i class="fas fa-briefcase"></i> Experience
{: .scroll-reveal}

<div class="timeline">
  <div class="timeline-item scroll-reveal">
    <span class="date">2022 - 2025</span>
    <h4>Part-time Lab Researcher</h4>
    <span class="company">Northeastern University</span>
    <p>Soft material mechanics research under PhD candidate Duo Wen</p>
  </div>
  
  <div class="timeline-item scroll-reveal">
    <span class="date">2023</span>
    <h4>Mechanical Engineering Co-op</h4>
    <span class="company">HiRain Technologies, Beijing</span>
    <p>PCB quality assurance, CAD modeling in SolidWorks/CREO</p>
  </div>
  
  <div class="timeline-item scroll-reveal">
    <span class="date">2021</span>
    <h4>Production/Design Engineer Co-op</h4>
    <span class="company">SharkNinja, Needham MA</span>
    <p>CFD simulation, 3D printing prototypes, sensor integration</p>
  </div>
</div>

## <i class="fas fa-graduation-cap"></i> Education
{: .scroll-reveal}

<div class="education-grid">
  <div class="education-card scroll-zoom">
    <div class="degree">M.S. in Robotics</div>
    <div class="school">Northeastern University</div>
    <div class="year">2024 - 2025 | GPA: 3.67</div>
  </div>
  <div class="education-card scroll-zoom">
    <div class="degree">B.S. in Mechanical Engineering</div>
    <div class="school">Northeastern University</div>
    <div class="year">2019 - 2023 | Minor in Math</div>
  </div>
</div>

## <i class="fas fa-tools"></i> Skills
{: .scroll-reveal}

<div class="skill-section">
  <div class="skill-bar scroll-reveal" style="--progress: 90%">
    <div class="skill-name"><span>Python</span><span>90%</span></div>
    <div class="bar"><div class="progress"></div></div>
  </div>
  <div class="skill-bar scroll-reveal" style="--progress: 85%">
    <div class="skill-name"><span>MATLAB / Simulink</span><span>85%</span></div>
    <div class="bar"><div class="progress"></div></div>
  </div>
  <div class="skill-bar scroll-reveal" style="--progress: 80%">
    <div class="skill-name"><span>SolidWorks / CAD</span><span>80%</span></div>
    <div class="bar"><div class="progress"></div></div>
  </div>
  <div class="skill-bar scroll-reveal" style="--progress: 75%">
    <div class="skill-name"><span>Arduino / Raspberry Pi / ROS</span><span>75%</span></div>
    <div class="bar"><div class="progress"></div></div>
  </div>
  <div class="skill-bar scroll-reveal" style="--progress: 70%">
    <div class="skill-name"><span>C++</span><span>70%</span></div>
    <div class="bar"><div class="progress"></div></div>
  </div>
</div>

<div class="cta-buttons scroll-reveal">
  <a href="/cv/" class="btn-primary"><i class="fas fa-file-alt"></i> View Full CV</a>
  <a href="/publications/" class="btn-secondary"><i class="fas fa-book"></i> Publications</a>
</div>

<script>
// 滚动动画观察器
const observerOptions = {
  threshold: 0.1,
  rootMargin: '0px 0px -50px 0px'
};

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, observerOptions);

// 观察所有需要动画的元素
document.querySelectorAll('.scroll-reveal, .scroll-zoom, .scroll-left, .skill-bar').forEach(el => {
  observer.observe(el);
});
</script>