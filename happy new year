<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy New Year 2026!</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap');

        body {
            margin: 0;
            overflow: hidden;
            background: #050505;
            font-family: 'Poppins', sans-serif;
            color: white;
            user-select: none;
        }

        /* Fireworks Canvas */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            cursor: crosshair;
        }

        /* Main Container */
        .container {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
            width: 90%;
            max-width: 650px;
            text-align: center;
        }

        /* Glassmorphism Card */
        .card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.6);
            animation: popIn 1.2s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            position: relative;
            overflow: hidden;
        }

        /* Header Line */
        .wisher-line {
            font-size: 1.2rem;
            color: #feb47b;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 5px;
            font-weight: 600;
        }

        h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 3.8rem;
            margin: 0;
            line-height: 1.1;
            background: linear-gradient(to right, #ff9a9e, #fecfef, #feada6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(255, 0, 204, 0.3);
            animation: glow 3s infinite alternate;
        }

        .year {
            font-size: 5rem;
            font-weight: 800;
            color: #fff;
            margin: 10px 0;
            text-shadow: 0 0 15px #00d2ff, 0 0 30px #00d2ff;
        }

        p.message {
            font-size: 1.05rem;
            line-height: 1.7;
            color: #f0f0f0;
            background: rgba(0,0,0,0.2);
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #feb47b;
            text-align: justify;
            text-align-last: center;
            margin-bottom: 25px;
        }

        .signature {
            font-size: 1.4rem;
            font-family: 'Dancing Script', cursive;
            color: #ff9a9e;
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
            animation: floatUp 8s linear infinite;
            opacity: 0.7;
            pointer-events: none;
        }
        
        .balloon::before {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 15px;
            background: rgba(255,255,255,0.5);
        }

        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 0.8; }
            100% { transform: translateY(-120vh) rotate(20deg); opacity: 0; }
        }

        @keyframes popIn {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 2px #fff); }
            to { filter: drop-shadow(0 0 10px #ff00de); }
        }

        /* Responsive */
        @media (max-width: 600px) {
            h1 { font-size: 2.8rem; }
            .year { font-size: 3.5rem; }
            .card { padding: 25px 20px; width: 85%; }
        }
    </style>
</head>
<body>

    <canvas id="fireworks"></canvas>

    <div class="container">
        <div class="card">
            <div class="wisher-line" id="wisherText">Dev is wishing you</div>
            
            <h1>Happy New Year</h1>
            <div class="year">2026</div>
            
            <p class="message">
                "A new year means a new chapter, and I’m truly grateful to start it with people who mean the most to me. Thank you, my friends and family, for your love, patience, and support through every high and low. You make my life richer just by being in it. May this New Year bring us peace in our hearts, strength in tough times, success in our efforts, and countless moments worth smiling for. Let’s grow, heal, and create beautiful memories together. Wishing you all a year full of happiness, love, and blessings."
            </p>
            
            <div class="signature">
                Happy New Year 🤍✨<br>
                ~ <span id="signName">Dev</span>
            </div>
        </div>
    </div>

    <script>
        // --- 1. DYNAMIC NAME LOGIC (Optional) ---
        // Input box hata diya hai, but agar URL me ?from=Name hoga to abhi bhi chalega.
        // Default "Dev" hi rahega.
        
        const urlParams = new URLSearchParams(window.location.search);
        const fromName = urlParams.get('from');
        const sender = fromName ? decodeURIComponent(fromName) : 'Dev';
        
        document.getElementById('wisherText').innerText = sender + " is wishing you";
        document.getElementById('signName').innerText = sender;


        // --- 2. BALLOON LOGIC ---
        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            const colors = ['#ff7e5f', '#feb47b', '#86a8e7', '#91eae4', '#ff00cc', '#ffff00', '#ff0040'];
            balloon.style.background = colors[Math.floor(Math.random() * colors.length)];
            balloon.style.left = Math.random() * 100 + 'vw';
            balloon.style.animationDuration = (Math.random() * 3 + 5) + 's';
            document.body.appendChild(balloon);
            setTimeout(() => balloon.remove(), 8000);
        }
        setInterval(createBalloon, 600);


        // --- 3. FIREWORKS LOGIC (TOUCH & BOOM) ---
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let particles = [];

        function Particle(x, y, color) {
            this.x = x;
            this.y = y;
            this.color = color;
            const velocity = Math.random() * 15; 
            const angle = Math.random() * Math.PI * 2;
            this.velocity = {
                x: Math.cos(angle) * velocity,
                y: Math.sin(angle) * velocity
            };
            this.alpha = 1;
            this.friction = 0.95;
            this.gravity = 0.05;
        }

        Particle.prototype.draw = function() {
            ctx.save();
            ctx.globalAlpha = this.alpha;
            ctx.beginPath();
            ctx.arc(this.x, this.y, 4, 0, Math.PI * 2, false);
            ctx.fillStyle = this.color;
            ctx.fill();
            ctx.restore();
        }

        Particle.prototype.update = function() {
            this.velocity.x *= this.friction;
            this.velocity.y *= this.friction;
            this.velocity.y += this.gravity;
            this.x += this.velocity.x;
            this.y += this.velocity.y;
            this.alpha -= 0.015;
            this.draw();
        }

        function createExplosion(x, y) {
            const colors = ['#ff0040', '#ff00cc', '#00ffcc', '#ffff00', '#ffffff', '#ff7e5f'];
            for (let i = 0; i < 80; i++) {
                const color = colors[Math.floor(Math.random() * colors.length)];
                particles.push(new Particle(x, y, color));
            }
        }

        function animate() {
            requestAnimationFrame(animate);
            ctx.fillStyle = 'rgba(0, 0, 0, 0.15)'; 
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            particles.forEach((particle, index) => {
                if (particle.alpha > 0) {
                    particle.update();
                } else {
                    particles.splice(index, 1);
                }
            });
        }
        
        // Auto Fireworks Randomly
        setInterval(() => {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height * 0.6;
            createExplosion(x, y);
        }, 1000);

        // Click Handler
        window.addEventListener('mousedown', (e) => {
            createExplosion(e.clientX, e.clientY);
        });

        // Touch Handler
        window.addEventListener('touchstart', (e) => {
            for (let i = 0; i < e.touches.length; i++) {
                createExplosion(e.touches[i].clientX, e.touches[i].clientY);
            }
        }, {passive: false});

        // Resize Handling
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        animate();
    </script>
</body>
</html>
