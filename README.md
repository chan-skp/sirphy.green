<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SIRPHY GREENS</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r148/three.min.js"></script>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #eef3e5;
      color: #2f4f4f;
    }
    header {
      background: linear-gradient(to right, #6dbf47, #a8d08d);
      color: white;
      padding: 3rem 2rem;
      text-align: center;
      position: relative;
      animation: fadeIn 1s ease-out;
    }
    header h1 {
      font-size: 3rem;
      margin: 0;
    }
    header p {
      font-size: 1.5rem;
      margin-top: 0.5rem;
    }
    nav {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      background-color: #2f4f4f;
      animation: slideInDown 1s ease-out;
    }
    nav a {
      color: white;
      padding: 1rem;
      text-decoration: none;
    }
    nav a:hover {
      background-color: #4f705f;
    }
    section {
      padding: 3rem 2rem;
      max-width: 1200px;
      margin: auto;
      animation: fadeInUp 0.8s ease forwards;
      opacity: 0;
    }
    section.visible {
      opacity: 1;
    }
    .hero-3d {
      height: 500px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 8px;
      margin-bottom: 2rem;
    }
    .hero-canvas {
      width: 100%;
      height: 100%;
      display: block;
    }
    .home, .farm-model, .products, .partners, .sustainability, .quote {
      margin-top: 2rem;
      background: white;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.05);
    }
    .home {
      background-image: url('background.jpg');
      background-size: cover;
      background-position: center;
      color: white;
      text-shadow: 1px 1px 2px #000;
    }
    .home h2 {
      font-size: 2.5rem;
    }
    .home p {
      font-size: 1.2rem;
      max-width: 600px;
    }
    .home button {
      margin-top: 1.5rem;
      padding: 0.75rem 1.5rem;
      background-color: #6dbf47;
      border: none;
      color: white;
      font-size: 1rem;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .home button:hover {
      background-color: #5aa73b;
    }
    .home iframe {
      margin-top: 2rem;
      max-width: 100%;
      height: 315px;
      border: none;
      border-radius: 8px;
    }
    footer {
      text-align: center;
      padding: 2rem;
      background-color: #6dbf47;
      color: white;
      margin-top: 2rem;
      animation: fadeIn 1s ease-in;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    @keyframes slideInDown {
      from { transform: translateY(-100%); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
    @keyframes fadeInUp {
      from { transform: translateY(30px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
  </style>
</head>
<body>
  <header>
    <h1>SIRPHY GREENS</h1>
    <p>Growing sustainably, trading globally</p>
  </header>

  <nav>
    <a href="#home">Home</a>
    <a href="#products">Products</a>
    <a href="#partners">Global Partners</a>
    <a href="#sustainability">Sustainability</a>
    <a href="#quote">Get a Quote</a>
  </nav>

  <section id="home" class="home">
    <h2>Welcome to SIRPHY GREENS</h2>
    <p>Your trusted partner in sustainable agricultural import and export. Discover how we grow responsibly and trade globally.</p>
    <button onclick="document.getElementById('quote').scrollIntoView({behavior: 'smooth'});">Get a Free Quote</button>
    

  <section class="hero-3d">
    <canvas id="globeCanvas" class="hero-canvas"></canvas>
  </section>

  <section class="farm-model">
    <h2>Interactive 3D Farm</h2>
    <p>Explore how our crops are grown, processed, and exported using state-of-the-art logistics. (3D farm simulation coming soon.)</p>
    <canvas id="farmCanvas" class="hero-canvas" style="height: 400px;"></canvas>
  </section>

  <section id="products" class="products">
    <h2>Our Products</h2>
    <ul>
      <li>Fertilizer</li>
      <li>Organic Products</li>
      <li>Processed Agricultural Goods</li>
    </ul>
    <p>Each product is grown with eco-conscious methods and sustainable practices.</p>
  </section>

  <section id="partners" class="partners">
    <h2>Global Partners</h2>
    <p>We collaborate with importers, exporters, and distributors across the world to build a greener supply chain.</p>
  </section>

  <section id="sustainability" class="sustainability">
    <h2>Our Sustainability Commitment</h2>
    <p>AgroGlobal uses renewable energy, supports biodiversity, and promotes sustainable farming techniques.</p>
  </section>

  <section id="quote" class="quote">
    <h2>Get a Quote</h2>
    <form class="contact-form">
      <input type="text" placeholder="Your Name" required><br>
      <input type="email" placeholder="Your Email" required><br>
      <textarea rows="4" placeholder="Your Request" required></textarea><br>
      <button type="submit">Submit</button>
    </form>
  </section>

  <footer>
    <p>&copy; 2025 SIRPHY GREENS. All rights reserved.</p>
  </footer>

  <script>
    // Animate sections on scroll
    const sections = document.querySelectorAll('section');
    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    }, {
      threshold: 0.1
    });
    sections.forEach(section => observer.observe(section));

    // Three.js Globe animation
    const canvas = document.getElementById('globeCanvas');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, canvas.clientWidth / canvas.clientHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true });
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);

    const geometry = new THREE.SphereGeometry(1, 32, 32);
    const material = new THREE.MeshBasicMaterial({ color: 0x228b22, wireframe: true });
    const sphere = new THREE.Mesh(geometry, material);
    scene.add(sphere);

    camera.position.z = 3;

    function animate() {
      requestAnimationFrame(animate);
      sphere.rotation.y += 0.01;
      renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
      camera.aspect = canvas.clientWidth / canvas.clientHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(canvas.clientWidth, canvas.clientHeight);
    });

    // Farm placeholder
    const farmCanvas = document.getElementById('farmCanvas');
    const farmRenderer = new THREE.WebGLRenderer({ canvas: farmCanvas, antialias: true });
    const farmScene = new THREE.Scene();
    const farmCamera = new THREE.PerspectiveCamera(75, farmCanvas.clientWidth / farmCanvas.clientHeight, 0.1, 1000);
    farmRenderer.setSize(farmCanvas.clientWidth, farmCanvas.clientHeight);
    
    const boxGeometry = new THREE.BoxGeometry(1, 1, 1);
    const boxMaterial = new THREE.MeshBasicMaterial({ color: 0x8b5e3c });
    const box = new THREE.Mesh(boxGeometry, boxMaterial);
    farmScene.add(box);

    farmCamera.position.z = 3;
    function animateFarm() {
      requestAnimationFrame(animateFarm);
      box.rotation.y += 0.01;
      farmRenderer.render(farmScene, farmCamera);
    }
    animateFarm();
  </script>
</body>
</html>
