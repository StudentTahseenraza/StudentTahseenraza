<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Tahseen Raza | Full Stack AI Developer Portfolio</title>
  <!-- Google Fonts & Font Awesome -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <!-- Three.js core for advanced 3D background -->
  <script type="importmap">
    {
      "imports": {
        "three": "https://unpkg.com/three@0.128.0/build/three.module.js"
      }
    }
  </script>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', sans-serif;
      background-color: #0a0a1a;
      color: #eef5ff;
      overflow-x: hidden;
      line-height: 1.5;
    }

    /* Canvas 3D background */
    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      pointer-events: none;
    }

    /* Main content overlay */
    .content {
      position: relative;
      z-index: 2;
      max-width: 1300px;
      margin: 0 auto;
      padding: 2rem 1.5rem 4rem;
      backdrop-filter: blur(2px);
    }

    /* Glass morphism cards */
    .glass-card {
      background: rgba(15, 25, 45, 0.55);
      backdrop-filter: blur(12px);
      border-radius: 2rem;
      border: 1px solid rgba(0, 201, 167, 0.3);
      box-shadow: 0 20px 35px -12px rgba(0,0,0,0.4);
      transition: transform 0.3s ease, border-color 0.2s;
    }

    .glass-card:hover {
      border-color: #00C9A7;
      transform: translateY(-4px);
    }

    /* Typography */
    h1, h2, h3 {
      font-weight: 700;
      letter-spacing: -0.02em;
    }

    .gradient-text {
      background: linear-gradient(135deg, #00F2FE 0%, #4FACFE 50%, #00C9A7 100%);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      display: inline-block;
    }

    .glow-text {
      text-shadow: 0 0 8px rgba(0,201,167,0.5);
    }

    /* Animated profile header */
    .profile-header {
      text-align: center;
      margin-bottom: 3rem;
      padding: 2rem 1rem;
    }

    .avatar-wrapper {
      display: inline-block;
      position: relative;
    }

    .avatar-glow {
      width: 130px;
      height: 130px;
      background: linear-gradient(45deg, #00C9A7, #4FACFE);
      border-radius: 50%;
      animation: pulseGlow 3s infinite;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 1rem;
    }

    @keyframes pulseGlow {
      0% { box-shadow: 0 0 0 0 rgba(0,201,167,0.4); transform: scale(0.98);}
      70% { box-shadow: 0 0 0 20px rgba(0,201,167,0); transform: scale(1.02);}
      100% { box-shadow: 0 0 0 0 rgba(0,201,167,0); transform: scale(0.98);}
    }

    .avatar-icon {
      font-size: 4.5rem;
      color: white;
      background: #0f172a;
      width: 110px;
      height: 110px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      background: rgba(10,20,35,0.8);
      backdrop-filter: blur(4px);
    }

    .typing-container {
      font-size: 1.6rem;
      font-weight: 500;
      margin-top: 1rem;
      min-height: 80px;
    }

    /* Skills Grid animated */
    .skills-grid {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 0.8rem;
      margin: 2rem 0;
    }

    .skill-badge {
      background: rgba(0, 201, 167, 0.15);
      border: 1px solid rgba(0, 201, 167, 0.5);
      padding: 0.5rem 1.2rem;
      border-radius: 40px;
      font-weight: 600;
      font-size: 0.9rem;
      transition: all 0.2s;
      backdrop-filter: blur(4px);
    }

    .skill-badge:hover {
      background: #00C9A7;
      color: #0a0a1a;
      transform: scale(1.05);
      box-shadow: 0 0 12px #00C9A7;
    }

    /* Timeline / experience */
    .timeline-item {
      padding: 1rem 0;
      border-left: 3px solid #00C9A7;
      margin-left: 1.2rem;
      padding-left: 1.8rem;
      position: relative;
    }

    /* Stats & project cards */
    .project-card {
      background: rgba(20, 30, 55, 0.6);
      backdrop-filter: blur(8px);
      border-radius: 1.5rem;
      padding: 1.5rem;
      transition: all 0.25s;
      border: 1px solid rgba(79, 172, 254, 0.2);
    }

    .project-card:hover {
      border-color: #00C9A7;
      transform: translateY(-6px);
    }

    .btn-outline-glow {
      border: 1px solid #00C9A7;
      background: transparent;
      padding: 0.5rem 1.2rem;
      border-radius: 40px;
      color: #00C9A7;
      font-weight: 600;
      transition: 0.2s;
    }

    .btn-outline-glow:hover {
      background: #00C9A7;
      color: #0a0a1a;
      box-shadow: 0 0 12px #00C9A7;
    }

    a {
      text-decoration: none;
    }

    footer {
      text-align: center;
      margin-top: 4rem;
      font-size: 0.85rem;
      opacity: 0.7;
    }

    @keyframes fadeUp {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .animate-fadeup {
      animation: fadeUp 0.8s cubic-bezier(0.2, 0.9, 0.4, 1.1) forwards;
    }

    .stats-row {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
      justify-content: center;
    }

    .stat-card {
      background: rgba(0,0,0,0.4);
      border-radius: 1.5rem;
      padding: 1rem 1.8rem;
      backdrop-filter: blur(8px);
      text-align: center;
    }

    @media (max-width: 768px) {
      .content {
        padding: 1rem;
      }
      .typing-container {
        font-size: 1.2rem;
      }
    }
  </style>
</head>
<body>

<div id="canvas-container"></div>

<div class="content">
  <!-- Header Section -->
  <div class="profile-header animate-fadeup">
    <div class="avatar-wrapper">
      <div class="avatar-glow">
        <div class="avatar-icon">
          <i class="fas fa-code" style="font-size: 3.4rem;"></i>
        </div>
      </div>
    </div>
    <h1 style="font-size: 2.7rem; margin-top: 1rem;">
      Hey there, I'm <span class="gradient-text">Tahseen Raza</span> 
      <i class="fas fa-hand-peace" style="color:#00C9A7;"></i>
    </h1>
    <div class="typing-container">
      <span id="dynamic-role" style="font-weight: 500; color: #00F2FE;"></span>
    </div>
  </div>

  <!-- About & summary from resume -->
  <div class="glass-card" style="padding: 2rem; margin-bottom: 2.5rem;">
    <div style="display: flex; flex-wrap: wrap; gap: 1.5rem; align-items: center;">
      <div style="flex:2">
        <h2><i class="fas fa-user-astronaut" style="color:#00C9A7; margin-right: 10px;"></i> Profile Summary</h2>
        <p style="margin-top: 12px; font-size: 1.05rem; line-height: 1.5;">Full Stack Developer with strong foundations in data structures and scalable backend systems, experienced in building <span class="gradient-text">AI-powered applications</span> using React, Node.js, and LLM APIs. Passionate about developing efficient systems and intelligent automation tools. <strong>Solved 300+ LeetCode problems</strong> & continuous learner.</p>
        <div style="display: flex; gap: 1rem; flex-wrap: wrap; margin-top: 1rem;">
          <span><i class="fas fa-graduation-cap"></i> B.Tech CSE (2026) · CGPA 8.84</span>
          <span><i class="fas fa-map-marker-alt"></i> Hyderabad, India</span>
        </div>
      </div>
      <div style="flex:1; text-align: center;">
        <div class="stat-card">
          <i class="fas fa-code-branch fa-2x" style="color:#00C9A7;"></i>
          <div style="font-size: 2rem; font-weight: 800;">300+</div>
          <div>LeetCode Solved</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Tech Stack section - with Skill Icons animated -->
  <h2 style="margin: 2rem 0 1rem 0; display: flex; align-items: center; gap: 8px;"><i class="fas fa-cogs"></i> Tech Stack & Tools</h2>
  <div class="glass-card" style="padding: 1.8rem;">
    <div class="skills-grid" id="skill-grid">
      <!-- JS, TS, React, Next, Node, Express, Python, Java, MongoDB, Postgres, Docker, AWS etc -->
    </div>
    <p class="gradient-text" style="text-align: center; margin-top: 1rem;"><i class="fas fa-brain"></i> AI & LLMs · Prompt Engineering · Scalable APIs · System Design Basics</p>
  </div>

  <!-- Experience & Education row -->
  <div style="display: flex; flex-wrap: wrap; gap: 1.8rem; margin: 2rem 0;">
    <div class="glass-card" style="flex: 1; padding: 1.5rem;">
      <h3><i class="fas fa-briefcase"></i> Experience</h3>
      <div class="timeline-item">
        <strong>Frontend Developer Intern</strong> @ College Tips Startup <br>
        <span style="color: #9ca3af;">Apr 2025 - May 2025</span>
        <p style="margin-top: 6px;">Developed 15+ reusable React components, integrated REST APIs, optimized performance. Collaborated in 5-member team, increased engagement by 40%.</p>
      </div>
      <div class="timeline-item">
        <strong>JP Morgan Virtual Internship</strong> (Kafka, APIs, Microservices) <br>
        <span style="color: #9ca3af;">Certification earned</span>
        <p>Hands-on experience with event streaming & microservices architecture.</p>
      </div>
    </div>
    <div class="glass-card" style="flex: 1; padding: 1.5rem;">
      <h3><i class="fas fa-university"></i> Education & Achievements</h3>
      <p><strong>B.Tech CS & IT</strong> · MANUU, Hyderabad (2022-2026) <br> CGPA: 8.84/10</p>
      <hr style="border-color: #2d3e5f; margin: 12px 0;">
      <ul style="list-style: none; padding-left: 0;">
        <li><i class="fas fa-certificate" style="color:#00C9A7;"></i> Artificial Intelligence Primer – Infosys Springboard</li>
        <li><i class="fas fa-shield-alt"></i> Saviynt Identity Security Certification</li>
        <li><i class="fab fa-java"></i> Java Full Stack Development Certificate</li>
      </ul>
    </div>
  </div>

  <!-- Featured Projects (Dynamic from resume) -->
  <h2 style="margin: 1rem 0 1rem;"><i class="fas fa-rocket"></i> Live Flagship Projects</h2>
  <div class="stats-row" style="margin-bottom: 2rem;">
    <div class="project-card" style="flex:1; min-width: 260px;">
      <i class="fas fa-chalkboard-teacher fa-2x" style="color:#4FACFE;"></i>
      <h3 style="margin: 8px 0;">DSA Visualizer</h3>
      <p>30+ algorithm visualizations, step-by-step execution, real-time simulation using React & Node.js, MongoDB. Built REST APIs and interactive UI.</p>
      <span class="skill-badge" style="background:rgba(0,201,167,0.2);">React.js</span> <span class="skill-badge">Node.js</span> <span class="skill-badge">MongoDB</span>
    </div>
    <div class="project-card" style="flex:1; min-width: 260px;">
      <i class="fas fa-database fa-2x" style="color:#00C9A7;"></i>
      <h3 style="margin: 8px 0;">CipherSQLStudio</h3>
      <p>SQL practice platform with real database execution. Integrated AI-based query hints to enhance learning accuracy. (PostgreSQL, AI APIs)</p>
      <span class="skill-badge">PostgreSQL</span> <span class="skill-badge">AI Integration</span>
    </div>
    <div class="project-card" style="flex:1; min-width: 260px;">
      <i class="fas fa-robot fa-2x" style="color:#F97316;"></i>
      <h3 style="margin: 8px 0;">AI Counsellor</h3>
      <p>AI-driven personalized study planning using LLM APIs. Designed structured workflows based on user data and goals → adaptive learning assistant.</p>
      <span class="skill-badge">React.js</span> <span class="skill-badge">LLM APIs</span> <span class="skill-badge">Prompt Eng</span>
    </div>
  </div>

  <!-- GitHub Stats & Animated Contributions -->
  <h2 style="margin: 1rem 0 0.5rem;"><i class="fab fa-github-alt"></i> GitHub Analytics</h2>
  <div style="display: flex; flex-wrap: wrap; gap: 1rem; justify-content: center; margin-bottom: 2rem;">
    <div class="glass-card" style="padding: 0.8rem; background: transparent;">
      <img src="https://github-readme-stats.vercel.app/api?username=StudentTahseenraza&show_icons=true&theme=radical&hide_border=true&bg_color=0a0a1a&title_color=00C9A7&icon_color=4FACFE" width="100%" style="max-width: 460px;" alt="stats"/>
    </div>
    <div class="glass-card" style="padding: 0.8rem;">
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=StudentTahseenraza&layout=compact&theme=radical&hide_border=true&bg_color=0a0a1a&title_color=00C9A7" width="100%" style="max-width: 360px;" alt="top-langs"/>
    </div>
  </div>
  
  <!-- GitHub TROPHY - advanced animation and cool -->
  <div style="text-align: center; margin: 2rem 0;">
    <img src="https://github-profile-trophy.vercel.app/?username=StudentTahseenraza&theme=radical&no-frame=true&no-bg=true&margin-w=12&column=5" alt="trophy" style="max-width: 100%; border-radius: 12px;"/>
  </div>

  <!-- Tech Timeline (CS Concepts) -->
  <div class="glass-card" style="padding: 1.8rem; margin-bottom: 2rem;">
    <h3><i class="fas fa-microchip"></i> CS Core Strengths</h3>
    <div style="display: flex; flex-wrap: wrap; gap: 12px; margin-top: 12px;">
      <span class="skill-badge">DSA (300+ problems)</span>
      <span class="skill-badge">OOP & DBMS</span>
      <span class="skill-badge">Operating Systems</span>
      <span class="skill-badge">Computer Networks</span>
      <span class="skill-badge">System Design (Basics)</span>
      <span class="skill-badge">Scalable APIs & WebSockets</span>
      <span class="skill-badge">Docker & AWS (cloud basics)</span>
    </div>
  </div>

  <!-- Connect and live badges -->
  <div class="glass-card" style="text-align: center; padding: 2rem;">
    <h3>🌐 Let's Connect & Collaborate</h3>
    <div style="display: flex; justify-content: center; gap: 1.8rem; margin: 1.5rem 0; flex-wrap: wrap;">
      <a href="mailto:toushifraza2015@gmail.com" target="_blank" class="btn-outline-glow"><i class="fas fa-envelope"></i> Email</a>
      <a href="https://github.com/StudentTahseenraza" target="_blank" class="btn-outline-glow"><i class="fab fa-github"></i> GitHub</a>
      <a href="https://www.linkedin.com/in/tahseen-raza-a71582262/" target="_blank" class="btn-outline-glow"><i class="fab fa-linkedin"></i> LinkedIn</a>
    </div>
    <div>
      <img src="https://komarev.com/ghpvc/?username=StudentTahseenraza&label=PROFILE+VIEWS&color=00C9A7&style=flat-square" alt="views" style="margin-top: 8px;">
    </div>
  </div>
  
  <footer>
    <i class="fas fa-code"></i> crafted with Three.js & Reactivist energy — “Always building, always learning” 🚀
  </footer>
</div>

<script type="module">
  import * as THREE from 'three';

  const container = document.getElementById('canvas-container');
  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0x050510);
  
  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  camera.position.z = 25;
  
  const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.setPixelRatio(window.devicePixelRatio);
  container.appendChild(renderer.domElement);
  
  // Create dynamic particle network
  const particlesGeometry = new THREE.BufferGeometry();
  const particlesCount = 1800;
  const posArray = new Float32Array(particlesCount * 3);
  for(let i = 0; i < particlesCount; i++) {
    posArray[i*3] = (Math.random() - 0.5) * 100;
    posArray[i*3+1] = (Math.random() - 0.5) * 60;
    posArray[i*3+2] = (Math.random() - 0.5) * 40 - 20;
  }
  particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
  
  const particlesMaterial = new THREE.PointsMaterial({
    size: 0.12,
    color: 0x4FACFE,
    transparent: true,
    opacity: 0.6,
    blending: THREE.AdditiveBlending
  });
  
  const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
  scene.add(particlesMesh);
  
  // Add glowing wireframe torus knots for modern look
  const knotGeo = new THREE.TorusKnotGeometry(3.2, 0.45, 180, 24, 3, 4);
  const knotMat = new THREE.MeshStandardMaterial({ color: 0x00C9A7, emissive: 0x006655, emissiveIntensity: 0.4, wireframe: true, transparent: true, opacity: 0.25 });
  const knot = new THREE.Mesh(knotGeo, knotMat);
  scene.add(knot);
  
  // second floating ring
  const ringGeo = new THREE.TorusGeometry(5, 0.2, 64, 200);
  const ringMat = new THREE.MeshStandardMaterial({ color: 0x4FACFE, emissive: 0x1f6390, emissiveIntensity: 0.3 });
  const ring = new THREE.Mesh(ringGeo, ringMat);
  ring.rotation.x = Math.PI / 2;
  scene.add(ring);
  
  // adding ambient and point lights
  const ambientLight = new THREE.AmbientLight(0x111122);
  scene.add(ambientLight);
  const pointLight = new THREE.PointLight(0x00C9A7, 1, 40);
  pointLight.position.set(5, 5, 10);
  scene.add(pointLight);
  const backLight = new THREE.PointLight(0x4FACFE, 0.6);
  backLight.position.set(-4, -3, -8);
  scene.add(backLight);
  
  let time = 0;
  
  function animate() {
    requestAnimationFrame(animate);
    time += 0.005;
    particlesMesh.rotation.y = time * 0.05;
    particlesMesh.rotation.x = Math.sin(time * 0.2) * 0.1;
    knot.rotation.x += 0.005;
    knot.rotation.y += 0.008;
    knot.rotation.z += 0.003;
    ring.rotation.z += 0.003;
    ring.rotation.y += 0.004;
    camera.position.x = Math.sin(time * 0.1) * 0.8;
    camera.position.y = Math.cos(time * 0.2) * 0.4;
    camera.lookAt(0, 0, 0);
    renderer.render(scene, camera);
  }
  
  animate();
  
  window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  });
</script>

<script>
  // dynamic role typing effect
  const roles = [
    "Full Stack Developer 🚀",
    "AI & LLM Enthusiast 🤖",
    "300+ LeetCode & Problem Solver ⚡",
    "Open Source Contributor 🌍",
    "Scalable Backend Architect 🏗️"
  ];
  let idx = 0;
  let charIdx = 0;
  let currentText = "";
  const typingElem = document.getElementById("dynamic-role");
  
  function typeEffect() {
    if (charIdx < roles[idx].length) {
      currentText += roles[idx].charAt(charIdx);
      typingElem.innerHTML = currentText + '<span style="border-right: 2px solid #00C9A7; animation: blink 0.7s step-end infinite;">|</span>';
      charIdx++;
      setTimeout(typeEffect, 80);
    } else {
      setTimeout(eraseEffect, 1800);
    }
  }
  
  function eraseEffect() {
    if (charIdx > 0) {
      currentText = currentText.slice(0, -1);
      typingElem.innerHTML = currentText + '<span style="border-right: 2px solid #00C9A7; animation: blink 0.7s step-end infinite;">|</span>';
      charIdx--;
      setTimeout(eraseEffect, 40);
    } else {
      idx = (idx + 1) % roles.length;
      setTimeout(typeEffect, 200);
    }
  }
  
  // inject style for blink
  const styleSheet = document.createElement("style");
  styleSheet.textContent = `@keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }`;
  document.head.appendChild(styleSheet);
  setTimeout(typeEffect, 300);
  
  // skills from resume: full list languages, front/back, db, tools
  const skillsList = [
    "JavaScript", "TypeScript", "Java", "Python", "React.js", "Next.js", "Redux Toolkit",
    "Node.js", "Express.js", "REST APIs", "WebSockets", "FastAPI", "MongoDB", "MySQL",
    "PostgreSQL", "Git", "Docker", "AWS", "Postman", "LLM APIs", "Prompt Engineering"
  ];
  
  const skillGrid = document.getElementById("skill-grid");
  skillsList.forEach(skill => {
    const badge = document.createElement("span");
    badge.className = "skill-badge";
    badge.innerHTML = skill;
    skillGrid.appendChild(badge);
  });
  
  // additional small hover animation for project cards
  const cards = document.querySelectorAll('.project-card');
  cards.forEach(card => {
    card.addEventListener('mouseenter', () => {
      card.style.transition = '0.25s';
    });
  });
  
  // make sure trophy images are responsive & fix broken if needed
  console.log("Special animated overview repo ready — Tahseen Raza's premium GitHub style");
</script>

</body>
</html>
