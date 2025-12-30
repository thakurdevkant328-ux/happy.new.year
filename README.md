<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy New Year from Dev!</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;500&display=swap');

        body {
            margin: 0;
            overflow: hidden;
            background: #020202; /* Night sky */
            font-family: 'Poppins', sans-serif;
            color: white;
        }

        /* Fireworks Canvas */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
        }

        /* Main Container */
        .container {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
            width: 90%;
            max-width: 600px;
            text-align: center;
        }

        /* Glassmorphism Card */
        .card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 40px 20px;
            border-radius: 20px;
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
            animation: popIn 1.5s ease-out;
        }

        h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 4rem;
            margin: 0;
            background: linear-gradient(to right, #ff7e5f, #feb47b, #ff00cc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: glow 2s infinite alternate;
        }

        .year {
            font-size: 6rem;
            font-weight: bold;
            color: #fff;
            text-shadow: 0 0 20px #ff00cc, 0 0 40px #ff00cc;
            margin: -20px 0;
        }

        p.message {
            font-size: 1.2rem;
            line-height: 1.6;
            margin-top: 20px;
            color: #e0e0e0;
        }

        .footer {
            margin-top: 30px;
            font-size: 1.5rem;
            font-weight: bold;
            color: #feb47b;
        }

        /* Balloon Animation */
        .balloon {
            position: absolute;
            bottom: -100px;
            width: 40px;
            height: 50px;
            background: red;
            border-radius: 50%;
            z-index: 5;
            animation: floatUp 6s linear infinite;
            opacity: 0.8;
        }
        
        .balloon::before {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 15px;
            background: white;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-120vh) rotate(20deg); opacity: 0; }
        }

        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        @keyframes glow {
            from { text-shadow: 0 0 10px #fff, 0 0 20px #ff00de; }
            to { text-shadow: 0 0 20px #fff, 0 0 40px #ff00de, 0 0 60px #ff00de; }
        }

        /* Responsive */
        @media (max-width: 600px) {
            h1 { font-size: 3rem; }
            .year { font-size: 4rem; }
            .card { padding: 20px; }
        }
    </style>
</head>
<body>

    <canvas id="fireworks"></canvas>

    <div class="container">
        <div class="card">
            <h1>Happy New Year</h1>
            <div class="year">2026</div>
            <p class="message">
                "Another year has passed, filled with memories and lessons. As we step into 2026, I wish your life gets filled with the brightness of these fireworks and the lightness of these balloons. May you conquer your dreams and find happiness in every moment."
            </p>
            <div class="footer">
                With Love,<br> ~ Dev ❤️
            </div>
        </div>
    </div>

    <script>
        // --- BALLOON LOGIC ---
        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            
            // Random colors
            const colors = ['#ff7e5f', '#feb47b', '#86a8e7', '#91eae4', '#ff00cc', '#ffff00'];
            balloon.style.background = colors[Math.floor(Math.random() * colors.length)];
            
            // Random Position
            balloon.style.left = Math.random() * 100 + 'vw';
            
            // Random Speed
            balloon.style.animationDuration = (Math.random() * 3 + 4) + 's';
            
            document.body.appendChild(balloon);

            // Remove balloon after animation to keep browser light
            setTimeout(() => {
                balloon.remove();
            }, 7000);
        }

        setInterval(createBalloon, 500); // New balloon every 0.5s

        // --- FIREWORKS LOGIC ---
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const particles = [];

        function Particle(x, y, color) {
            this.x = x;
            this.y = y;
            this.color = color;
            this.velocity = {
                x: (Math.random() - 0.5) * 8,
                y: (Math.random() - 0.5) * 8
            };
            this.alpha = 1;
            this.friction = 0.96;
        }

        Particle.prototype.draw = function() {
            ctx.globalAlpha = this.alpha;
            ctx.beginPath();
            ctx.arc(this.x, this.y, 3, 0, Math.PI * 2, false);
            ctx.fillStyle = this.color;
            ctx.fill();
        }

        Particle.prototype.update = function() {
            this.velocity.x *= this.friction;
            this.velocity.y *= this.friction;
            this.x += this.velocity.x;
            this.y += this.velocity.y;
            this.alpha -= 0.01;
            this.draw();
        }

        function createFirework(x, y) {
            const colors = ['#ff0040', '#ff00cc', '#00ffcc', '#ffff00', '#ffffff'];
            const color = colors[Math.floor(Math.random() * colors.length)];
            for (let i = 0; i < 50; i++) {
                particles.push(new Particle(x, y, color));
            }
        }

        function animate() {
            requestAnimationFrame(animate);
            ctx.fillStyle = 'rgba(0, 0, 0, 0.1)'; // Fade effect
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            particles.forEach((particle, index) => {
                if (particle.alpha > 0) {
                    particle.update();
                } else {
                    particles.splice(index, 1);
                }
            });
        }
        
        // Auto launch fireworks randomly
        setInterval(() => {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height / 2;
            createFirework(x, y);
        }, 800);

        // Launch on click
        window.addEventListener('click', (e) => {
            createFirework(e.clientX, e.clientY);
        });
        
        // Resize handling
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        animate();
    </script>
</body>
</html>
