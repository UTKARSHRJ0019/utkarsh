<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Design  - Interactive Experience</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(45deg, #0f0f23, #1a1a2e, #16213e);
            color: white;
            overflow-x: hidden;
            perspective: 1000px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            z-index: 1000;
            padding: 1rem 0;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .nav-links a:hover {
            color: #4ecdc4;
            text-shadow: 0 0 10px #4ecdc4;
        }

        /* Hero Section with 3D Elements */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .hero-content {
            text-align: center;
            z-index: 10;
            transform-style: preserve-3d;
        }

        .hero h1 {
            font-size: 4rem;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: float 3s ease-in-out infinite;
            transform: translateZ(50px);
        }

        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.8;
            animation: slideInUp 1s ease 0.5s both;
            transform: translateZ(25px);
        }

        /* 3D Floating Shapes */
        .floating-shapes {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .shape {
            position: absolute;
            opacity: 0.1;
            animation: rotate3d 20s infinite linear;
        }

        .cube {
            width: 100px;
            height: 100px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            transform-style: preserve-3d;
            animation: rotate3d 15s infinite linear;
        }

        .sphere {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #4ecdc4, #45b7d1, #1a1a2e);
            animation: bounce3d 4s infinite ease-in-out;
        }

        .pyramid {
            width: 0;
            height: 0;
            border-left: 50px solid transparent;
            border-right: 50px solid transparent;
            border-bottom: 100px solid #ff6b6b;
            animation: spin3d 12s infinite linear;
        }

        /* 3D Cards Section */
        .cards-section {
            padding: 100px 0;
            perspective: 1200px;
        }

        .section-title {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 3rem;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .card-3d {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            padding: 2rem;
            text-align: center;
            transform-style: preserve-3d;
            transition: all 0.6s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .card-3d::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transform: rotate(45deg);
            transition: all 0.6s ease;
            opacity: 0;
        }

        .card-3d:hover {
            transform: rotateY(10deg) rotateX(10deg) translateZ(50px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }

        .card-3d:hover::before {
            opacity: 1;
            animation: shine 1s ease-in-out;
        }

        .card-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            display: block;
            transform: translateZ(30px);
        }

        .card-3d h3 {
            margin-bottom: 1rem;
            color: #4ecdc4;
            transform: translateZ(20px);
        }

        .card-3d p {
            opacity: 0.8;
            line-height: 1.6;
            transform: translateZ(10px);
        }

        /* Interactive 3D Scene */
        .interactive-scene {
            padding: 100px 0;
            text-align: center;
        }

        .scene-container {
            perspective: 1500px;
            height: 500px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 2rem 0;
        }

        .rotating-cube {
            width: 200px;
            height: 200px;
            position: relative;
            transform-style: preserve-3d;
            animation: autoRotate 10s infinite linear;
            cursor: pointer;
        }

        .cube-face {
            position: absolute;
            width: 200px;
            height: 200px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: bold;
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .cube-face.front { 
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e);
            transform: translateZ(100px); 
        }
        .cube-face.back { 
            background: linear-gradient(45deg, #4ecdc4, #6fd4d1);
            transform: rotateY(180deg) translateZ(100px); 
        }
        .cube-face.right { 
            background: linear-gradient(45deg, #45b7d1, #6bc5e0);
            transform: rotateY(90deg) translateZ(100px); 
        }
        .cube-face.left { 
            background: linear-gradient(45deg, #96ceb4, #a8d5c4);
            transform: rotateY(-90deg) translateZ(100px); 
        }
        .cube-face.top { 
            background: linear-gradient(45deg, #feca57, #fed85d);
            transform: rotateX(90deg) translateZ(100px); 
        }
        .cube-face.bottom { 
            background: linear-gradient(45deg, #ff9ff3, #ffb3f7);
            transform: rotateX(-90deg) translateZ(100px); 
        }

        /* Controls */
        .controls {
            margin: 2rem 0;
            display: flex;
            justify-content: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .control-btn {
            padding: 10px 20px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            border: none;
            border-radius: 25px;
            color: white;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        .control-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        /* 3D Gallery */
        .gallery-3d {
            padding: 100px 0;
            perspective: 1200px;
        }

        .gallery-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 400px;
            position: relative;
        }

        .gallery-item {
            position: absolute;
            width: 250px;
            height: 300px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.6s ease;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        /* Particle System */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #4ecdc4;
            border-radius: 50%;
            animation: particleFloat 15s infinite linear;
        }

        /* Footer */
        footer {
            padding: 50px 0;
            text-align: center;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
        }

        /* Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0px) translateZ(50px); }
            50% { transform: translateY(-20px) translateZ(50px); }
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px) translateZ(25px);
            }
            to {
                opacity: 0.8;
                transform: translateY(0) translateZ(25px);
            }
        }

        @keyframes rotate3d {
            from { transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg); }
            to { transform: rotateX(360deg) rotateY(360deg) rotateZ(360deg); }
        }

        @keyframes bounce3d {
            0%, 100% { transform: translateY(0px) translateZ(0px); }
            50% { transform: translateY(-30px) translateZ(20px); }
        }

        @keyframes spin3d {
            from { transform: rotateY(0deg); }
            to { transform: rotateY(360deg); }
        }

        @keyframes autoRotate {
            from { transform: rotateX(0deg) rotateY(0deg); }
            to { transform: rotateX(360deg) rotateY(360deg); }
        }

        @keyframes shine {
            0% { transform: translateX(-100%) rotate(45deg); }
            100% { transform: translateX(100%) rotate(45deg); }
        }

        @keyframes particleFloat {
            0% {
                transform: translateY(100vh) translateX(0px) rotateZ(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) translateX(100px) rotateZ(360deg);
                opacity: 0;
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 { font-size: 2.5rem; }
            .section-title { font-size: 2rem; }
            .nav-links { display: none; }
            .rotating-cube { width: 150px; height: 150px; }
            .cube-face { width: 150px; height: 150px; font-size: 1.5rem; }
            .cube-face.front, .cube-face.back, .cube-face.right, 
            .cube-face.left, .cube-face.top, .cube-face.bottom { 
                transform: translateZ(75px); 
            }
            .cube-face.back { transform: rotateY(180deg) translateZ(75px); }
            .cube-face.right { transform: rotateY(90deg) translateZ(75px); }
            .cube-face.left { transform: rotateY(-90deg) translateZ(75px); }
            .cube-face.top { transform: rotateX(90deg) translateZ(75px); }
            .cube-face.bottom { transform: rotateX(-90deg) translateZ(75px); }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <header>
        <nav class="container">
            <div class="logo">3D Showcase</div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#cards">3D Cards</a></li>
                <li><a href="#interactive">Interactive</a></li>
                <li><a href="#gallery">Gallery</a></li>
            </ul>
        </nav>
    </header>

    <section id="home" class="hero">
        <div class="floating-shapes">
            <div class="shape cube" style="top: 10%; left: 10%;"></div>
            <div class="shape sphere" style="top: 20%; right: 15%;"></div>
            <div class="shape pyramid" style="bottom: 30%; left: 20%;"></div>
            <div class="shape cube" style="bottom: 20%; right: 10%;"></div>
            <div class="shape sphere" style="top: 50%; left: 5%;"></div>
        </div>
        
        <div class="hero-content">
            <h1>3D Design Experience</h1>
            <p>Immerse yourself in a world of three-dimensional beauty and interactive elements</p>
        </div>
    </section>

    <section id="cards" class="cards-section">
        <div class="container">
            <h2 class="section-title">3D Interactive Cards</h2>
            <div class="cards-grid">
                <div class="card-3d">
                    <span class="card-icon">🎨</span>
                    <h3>Creative Design</h3>
                    <p>Explore limitless possibilities with our 3D design tools and creative workflows that bring your imagination to life.</p>
                </div>
                <div class="card-3d">
                    <span class="card-icon">⚡</span>
                    <h3>Performance</h3>
                    <p>Lightning-fast rendering and smooth animations powered by advanced 3D graphics optimization techniques.</p>
                </div>
                <div class="card-3d">
                    <span class="card-icon">🔮</span>
                    <h3>Innovation</h3>
                    <p>Cutting-edge 3D technologies that push the boundaries of what's possible in web-based experiences.</p>
                </div>
                <div class="card-3d">
                    <span class="card-icon">🌟</span>
                    <h3>Interactive</h3>
                    <p>Engaging user interactions that respond to mouse movements and create immersive 3D environments.</p>
                </div>
                <div class="card-3d">
                    <span class="card-icon">🎯</span>
                    <h3>Precision</h3>
                    <p>Pixel-perfect 3D transformations and animations crafted with mathematical precision and artistic flair.</p>
                </div>
                <div class="card-3d">
                    <span class="card-icon">🚀</span>
                    <h3>Future Ready</h3>
                    <p>Next-generation 3D web technologies that are compatible with modern browsers and devices.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="interactive" class="interactive-scene">
        <div class="container">
            <h2 class="section-title">Interactive 3D Cube</h2>
            <p>Click and drag to rotate, or use the controls below</p>
            
            <div class="scene-container">
                <div class="rotating-cube" id="cube">
                    <div class="cube-face front">FRONT</div>
                    <div class="cube-face back">BACK</div>
                    <div class="cube-face right">RIGHT</div>
                    <div class="cube-face left">LEFT</div>
                    <div class="cube-face top">TOP</div>
                    <div class="cube-face bottom">BOTTOM</div>
                </div>
            </div>
            
            <div class="controls">
                <button class="control-btn" onclick="rotateCube('x')">Rotate X</button>
                <button class="control-btn" onclick="rotateCube('y')">Rotate Y</button>
                <button class="control-btn" onclick="rotateCube('z')">Rotate Z</button>
                <button class="control-btn" onclick="resetCube()">Reset</button>
                <button class="control-btn" onclick="toggleAutoRotate()">Auto Rotate</button>
            </div>
        </div>
    </section>

    <section id="gallery" class="gallery-3d">
        <div class="container">
            <h2 class="section-title">3D Gallery</h2>
            <p>A circular 3D gallery that rotates automatically</p>
            
            <div class="gallery-container" id="gallery">
                <div class="gallery-item" data-index="0">Item 1</div>
                <div class="gallery-item" data-index="1">Item 2</div>
                <div class="gallery-item" data-index="2">Item 3</div>
                <div class="gallery-item" data-index="3">Item 4</div>
                <div class="gallery-item" data-index="4">Item 5</div>
                <div class="gallery-item" data-index="5">Item 6</div>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <h3>3D Design Showcase</h3>
            <p>Experience the future of web design with immersive 3D elements</p>
            <p>&copy; 2024 3D Showcase. All rights reserved.</p>
        </div>
    </footer>

    <script>
        // Smooth scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Particle system
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 50;

            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 15 + 's';
                particle.style.animationDuration = (Math.random() * 10 + 10) + 's';
                particlesContainer.appendChild(particle);
            }
        }

        // Interactive cube controls
        let cubeRotationX = 0;
        let cubeRotationY = 0;
        let cubeRotationZ = 0;
        let autoRotating = true;
        const cube = document.getElementById('cube');

        function rotateCube(axis) {
            switch(axis) {
                case 'x':
                    cubeRotationX += 90;
                    break;
                case 'y':
                    cubeRotationY += 90;
                    break;
                case 'z':
                    cubeRotationZ += 90;
                    break;
            }
            updateCubeRotation();
        }

        function resetCube() {
            cubeRotationX = 0;
            cubeRotationY = 0;
            cubeRotationZ = 0;
            updateCubeRotation();
        }

        function updateCubeRotation() {
            if (!autoRotating) {
                cube.style.transform = `rotateX(${cubeRotationX}deg) rotateY(${cubeRotationY}deg) rotateZ(${cubeRotationZ}deg)`;
            }
        }

        function toggleAutoRotate() {
            autoRotating = !autoRotating;
            if (autoRotating) {
                cube.style.animation = 'autoRotate 10s infinite linear';
            } else {
                cube.style.animation = 'none';
                updateCubeRotation();
            }
        }

        // Mouse interaction with cube
        let isDragging = false;
        let previousMousePosition = { x: 0, y: 0 };

        cube.addEventListener('mousedown', (e) => {
            isDragging = true;
            previousMousePosition = { x: e.clientX, y: e.clientY };
            autoRotating = false;
            cube.style.animation = 'none';
        });

        document.addEventListener('mousemove', (e) => {
            if (isDragging) {
                const deltaMove = {
                    x: e.clientX - previousMousePosition.x,
                    y: e.clientY - previousMousePosition.y
                };

                cubeRotationY += deltaMove.x * 0.5;
                cubeRotationX -= deltaMove.y * 0.5;

                updateCubeRotation();
                previousMousePosition = { x: e.clientX, y: e.clientY };
            }
        });

        document.addEventListener('mouseup', () => {
            isDragging = false;
        });

        // 3D Gallery rotation
        function setup3DGallery() {
            const galleryItems = document.querySelectorAll('.gallery-item');
            const radius = 300;
            const itemCount = galleryItems.length;

            galleryItems.forEach((item, index) => {
                const angle = (index / itemCount) * 2 * Math.PI;
                const x = Math.cos(angle) * radius;
                const z = Math.sin(angle) * radius;
                
                item.style.transform = `translate3d(${x}px, 0, ${z}px) rotateY(${angle}rad)`;
            });

            // Auto-rotate gallery
            let galleryRotation = 0;
            setInterval(() => {
                galleryRotation += 0.5;
                document.getElementById('gallery').style.transform = `rotateY(${galleryRotation}deg)`;
            }, 50);
        }

        // Parallax effect for floating shapes
        function updateParallax() {
            const shapes = document.querySelectorAll('.shape');
            const scrolled = window.pageYOffset;
            const rate = scrolled * -0.5;

            shapes.forEach((shape, index) => {
                const speed = (index + 1) * 0.3;
                shape.style.transform = `translate3d(0, ${rate * speed}px, 0)`;
            });
        }

        // Card 3D effects
        function setup3DCards() {
            const cards = document.querySelectorAll('.card-3d');
            
            cards.forEach(card => {
                card.addEventListener('mousemove', (e) => {
                    const rect = card.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    
                    const centerX = rect.width / 2;
                    const centerY = rect.height / 2;
                    
                    const rotateX = (y - centerY) / 10;
                    const rotateY = (centerX - x) / 10;
                    
                    card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateZ(50px)`;
                });
                
                card.addEventListener('mouseleave', () => {
                    card.style.transform = 'perspective(1000px) rotateX(0deg) rotateY(0deg) translateZ(0px)';
                });
            });
        }

        // Initialize everything
        document.addEventListener('DOMContentLoaded', () => {
            createParticles();
            setup3DGallery();
            setup3DCards();
            
            // Parallax on scroll
            window.addEventListener('scroll', updateParallax);
            
            // Random floating shapes animation
            setInterval(() => {
                const shapes = document.querySelectorAll('.floating-shapes .shape');
                shapes.forEach(shape => {
                    const randomX = Math.random() * 20 - 10;
                    const randomY = Math.random() * 20 - 10;
                    shape.style.transform += ` translate(${randomX}px, ${randomY}px)`;
                });
            }, 3000);
        });

        // Add some interactive sound effects (visual feedback)
        document.addEventListener('click', (e) => {
            if (e.target.classList.contains('control-btn') || e.target.classList.contains('card-3d')) {
                // Create ripple effect
                const ripple = document.createElement('div');
                ripple.style.cssText = `
                    position: fixed;
                    border-radius: 50%;
                    background: rgba(78, 205, 196, 0.6);
                    transform: scale(0);
                    animation: ripple 0.6s linear;
                    pointer-events: none;
                    z-index: 9999;
                    left: ${e.clientX - 25}px;
                    top: ${e.clientY - 25}px;
                    width: 50px;
                    height: 50px;
                `;
                
                document.body.appendChild(ripple);
                
                setTimeout(() => {
                    ripple.remove();
                }, 600);
            }
        });

        // Add ripple animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes ripple {
                to {
                    transform: scale(4);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        console.log('🎨 3D Showcase loaded successfully!');
        console.log('✨ Features: Interactive cube, 3D cards, particle system, rotating gallery');
    </script>
</body>
</html>
