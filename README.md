# PochaccoAmorGame
Happy aniversary, I luv u sooooo much
[Uploading index.html.html…]()
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pochacco Amor 💖</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Press Start 2P', cursive;
            background: linear-gradient(135deg, #ffd1dc 0%, #e0c3fc 50%, #c3d9ff 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
        }
        
        #gameContainer {
            position: relative;
            width: 800px;
            height: 500px;
            background: linear-gradient(to bottom, #ffb3d9 0%, #ffd9ec 100%);
            border: 8px solid #ff69b4;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(255, 105, 180, 0.4);
            overflow: hidden;
        }
        
        #gameCanvas {
            display: block;
            width: 100%;
            height: 100%;
        }
        
        .screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ffb3d9 0%, #c3b1e1 100%);
            padding: 40px;
            text-align: center;
        }
        
        .screen.active {
            display: flex;
        }
        
        h1 {
            font-size: 48px;
            color: #ff1493;
            text-shadow: 4px 4px 0 #fff, 8px 8px 0 #ffb6c1;
            margin-bottom: 20px;
            animation: float 3s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .heart {
            display: inline-block;
            animation: pulse 1s ease-in-out infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }
        
        .instructions {
            font-size: 12px;
            color: #ff69b4;
            margin: 20px 0;
            line-height: 1.8;
            max-width: 600px;
        }
        
        button {
            font-family: 'Press Start 2P', cursive;
            font-size: 16px;
            padding: 20px 40px;
            background: linear-gradient(135deg, #ff69b4 0%, #ff1493 100%);
            color: white;
            border: 4px solid #fff;
            border-radius: 15px;
            cursor: pointer;
            box-shadow: 0 6px 0 #c71585, 0 10px 20px rgba(255, 20, 147, 0.3);
            transition: all 0.1s;
            margin-top: 20px;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 0 #c71585, 0 12px 25px rgba(255, 20, 147, 0.4);
        }
        
        button:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #c71585, 0 4px 10px rgba(255, 20, 147, 0.3);
        }
        
        .message {
            font-size: 14px;
            color: #ff1493;
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 15px;
            border: 4px solid #ffb6c1;
            margin: 20px 0;
            line-height: 1.8;
            max-width: 650px;
            box-shadow: 0 5px 15px rgba(255, 105, 180, 0.3);
        }
        
        .final-message {
            font-size: 13px;
            line-height: 2;
        }
        
        #levelInfo {
            position: absolute;
            top: 20px;
            left: 20px;
            font-size: 12px;
            color: #ff1493;
            background: rgba(255, 255, 255, 0.9);
            padding: 10px 20px;
            border-radius: 10px;
            border: 3px solid #ffb6c1;
            z-index: 100;
        }
        
        #score {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 12px;
            color: #ff1493;
            background: rgba(255, 255, 255, 0.9);
            padding: 10px 20px;
            border-radius: 10px;
            border: 3px solid #ffb6c1;
            z-index: 100;
        }
        
        .floating-hearts {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
        }
        
        .floating-heart {
            position: absolute;
            font-size: 20px;
            animation: floatUp 4s linear infinite;
            opacity: 0.6;
        }
        
        @keyframes floatUp {
            from {
                transform: translateY(0) rotate(0deg);
                opacity: 0.6;
            }
            to {
                transform: translateY(-500px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <div class="floating-hearts" id="floatingHearts"></div>
        
        <!-- Start Screen -->
        <div id="startScreen" class="screen active">
            <h1>Pochacco Amor <span class="heart">💖</span></h1>
            <div class="instructions">
                Ayuda a Pochacco a superar<br>
                los niveles del amor 💖<br><br>
                <strong>ESPACIO</strong> o <strong>TOQUE</strong> → Saltar<br>
                <strong>SHIFT</strong> → Agacharse
            </div>
            <button id="startBtn">Empezar intento</button>
        </div>
        
        <!-- Game Screen -->
        <div id="gameScreen" class="screen">
            <canvas id="gameCanvas"></canvas>
            <div id="levelInfo">Nivel: <span id="levelName">Isi Pisi</span></div>
            <div id="score">Distancia: <span id="scoreValue">0</span>m</div>
        </div>
        
        <!-- Level Complete Screens -->
        <div id="level1Complete" class="screen">
            <h1>¡Nivel 1 Completado!</h1>
            <div class="message">Muy bien pequeño gato!</div>
            <button id="level2Btn">Continuar al nivel Tigrillo</button>
        </div>
        
        <div id="level2Complete" class="screen">
            <h1>¡Nivel 2 Completado!</h1>
            <div class="message">Parece que papá tigrillo<br>va con toda</div>
            <button id="level3Btn">Continuar al nivel Lunatacho</button>
        </div>
        
        <div id="level3Complete" class="screen">
            <h1>¡Nivel 3 Completado!</h1>
            <div class="message">Un beso para que continúes<br>con la aventura 💋</div>
            <button id="level4Btn">Continuar al nivel Lanito</button>
        </div>
        
        <div id="level4Complete" class="screen">
            <h1>¡Nivel 4 Completado!</h1>
            <div class="message">Ya casi estás cerca<br>de la gran meta</div>
            <button id="level5Btn">Continuar al nivel Estebini Sopini</button>
        </div>
        
        <div id="gameComplete" class="screen">
            <h1>¡FELICIDADES! <span class="heart">💖</span></h1>
            <div class="message final-message">
                Pochacco ha encontrado<br>el corazón del amor 💖<br><br>
                En agradecimiento, Pochacco quiere<br>regalarte un boleto para continuar<br>
                un año más de compartir con Chini,<br>que te ama con todo su corazón.<br><br>
                Si el boleto caduca, podrás ganar<br>otro pasando los niveles.
            </div>
            <button id="restartBtn">Volver al inicio</button>
        </div>
        
        <!-- Game Over Screen -->
        <div id="gameOverScreen" class="screen">
            <h1>¡Ups! 💔</h1>
            <div class="message">Pochacco necesita<br>intentar de nuevo</div>
            <button id="retryBtn">Reintentar nivel</button>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        canvas.width = 800;
        canvas.height = 500;
        
        // Audio Context for sound effects
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        
        // Sound effects functions
        function playJumpSound() {
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            
            oscillator.frequency.setValueAtTime(400, audioCtx.currentTime);
            oscillator.frequency.exponentialRampToValueAtTime(600, audioCtx.currentTime + 0.1);
            
            gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
            
            oscillator.start(audioCtx.currentTime);
            oscillator.stop(audioCtx.currentTime + 0.1);
        }
        
        function playCollisionSound() {
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            
            oscillator.type = 'sawtooth';
            oscillator.frequency.setValueAtTime(200, audioCtx.currentTime);
            oscillator.frequency.exponentialRampToValueAtTime(50, audioCtx.currentTime + 0.3);
            
            gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
            
            oscillator.start(audioCtx.currentTime);
            oscillator.stop(audioCtx.currentTime + 0.3);
        }
        
        function playButtonSound() {
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            
            oscillator.type = 'square';
            oscillator.frequency.setValueAtTime(800, audioCtx.currentTime);
            oscillator.frequency.setValueAtTime(1000, audioCtx.currentTime + 0.05);
            
            gainNode.gain.setValueAtTime(0.2, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
            
            oscillator.start(audioCtx.currentTime);
            oscillator.stop(audioCtx.currentTime + 0.1);
        }
        
        function playLevelCompleteSound() {
            const notes = [523.25, 659.25, 783.99, 1046.50]; // C5, E5, G5, C6
            
            notes.forEach((freq, index) => {
                const oscillator = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                
                oscillator.type = 'sine';
                oscillator.frequency.setValueAtTime(freq, audioCtx.currentTime + index * 0.1);
                
                gainNode.gain.setValueAtTime(0.2, audioCtx.currentTime + index * 0.1);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + index * 0.1 + 0.2);
                
                oscillator.start(audioCtx.currentTime + index * 0.1);
                oscillator.stop(audioCtx.currentTime + index * 0.1 + 0.2);
            });
        }
        
        // Game state
        let currentLevel = 1;
        let gameRunning = false;
        let score = 0;
        let gameSpeed = 5;
        let frameCount = 0;
        
        // Level configurations
        const levels = {
            1: { name: 'Isi Pisi', speed: 4, obstacleFreq: 120, duration: 500 },
            2: { name: 'Tigrillo', speed: 5.5, obstacleFreq: 90, duration: 500 },
            3: { name: 'Lunatacho', speed: 7, obstacleFreq: 70, duration: 500 },
            4: { name: 'Lanito', speed: 8.5, obstacleFreq: 60, duration: 500 },
            5: { name: 'Estebini Sopini', speed: 6, obstacleFreq: 80, duration: 500, hearts: true }
        };
        
        // Pochacco (player)
        const player = {
            x: 100,
            y: 350,
            width: 40,
            height: 40,
            jumping: false,
            ducking: false,
            velocityY: 0,
            gravity: 0.8,
            jumpPower: -15,
            groundY: 350,
            duckHeight: 25
        };
        
        // Obstacles
        let obstacles = [];
        let hearts = [];
        
        class Obstacle {
            constructor(type) {
                this.type = type; // 'ground' or 'flying'
                this.width = 30;
                this.height = type === 'ground' ? 40 : 30;
                this.x = canvas.width;
                this.y = type === 'ground' ? player.groundY : player.groundY - 60;
                this.passed = false;
            }
            
            update() {
                this.x -= gameSpeed;
            }
            
            draw() {
                ctx.fillStyle = '#ff1493';
                ctx.fillRect(this.x, this.y, this.width, this.height);
                
                // Add spikes for visual
                ctx.fillStyle = '#c71585';
                for (let i = 0; i < this.width; i += 10) {
                    ctx.beginPath();
                    ctx.moveTo(this.x + i, this.y);
                    ctx.lineTo(this.x + i + 5, this.y - 8);
                    ctx.lineTo(this.x + i + 10, this.y);
                    ctx.fill();
                }
            }
            
            collidesWith(player) {
                const playerHeight = player.ducking ? player.duckHeight : player.height;
                const playerY = player.ducking ? player.groundY + (player.height - player.duckHeight) : player.y;
                
                return this.x < player.x + player.width &&
                       this.x + this.width > player.x &&
                       this.y < playerY + playerHeight &&
                       this.y + this.height > playerY;
            }
        }
        
        class Heart {
            constructor(broken = false) {
                this.broken = broken;
                this.width = 25;
                this.height = 25;
                this.x = canvas.width;
                this.y = player.groundY + 15;
                this.passed = false;
            }
            
            update() {
                this.x -= gameSpeed;
            }
            
            draw() {
                ctx.font = '25px Arial';
                ctx.fillText(this.broken ? '💔' : '❤️', this.x, this.y);
            }
            
            collidesWith(player) {
                if (!this.broken) return false;
                
                const playerHeight = player.ducking ? player.duckHeight : player.height;
                const playerY = player.ducking ? player.groundY + (player.height - player.duckHeight) : player.y;
                
                return this.x < player.x + player.width &&
                       this.x + this.width > player.x &&
                       this.y - this.height < playerY + playerHeight &&
                       this.y > playerY;
            }
        }
        
        function drawPlayer() {
            const playerHeight = player.ducking ? player.duckHeight : player.height;
            const playerY = player.ducking ? player.groundY + (player.height - player.duckHeight) : player.y;
            
            // Body
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(player.x, playerY, player.width, playerHeight);
            
            // Ears
            if (!player.ducking) {
                ctx.fillStyle = '#87ceeb';
                ctx.fillRect(player.x + 8, playerY - 8, 8, 12);
                ctx.fillRect(player.x + 24, playerY - 8, 8, 12);
            }
            
            // Face details
            ctx.fillStyle = '#000000';
            // Eyes
            ctx.fillRect(player.x + 12, playerY + 12, 4, 4);
            ctx.fillRect(player.x + 24, playerY + 12, 4, 4);
            // Nose
            ctx.fillRect(player.x + 18, playerY + 20, 4, 3);
            
            // Blush
            ctx.fillStyle = '#ffb6c1';
            ctx.fillRect(player.x + 6, playerY + 18, 6, 4);
            ctx.fillRect(player.x + 28, playerY + 18, 6, 4);
        }
        
        function drawBackground() {
            // Sky gradient
            const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
            gradient.addColorStop(0, '#ffb3d9');
            gradient.addColorStop(1, '#ffd9ec');
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Clouds
            ctx.fillStyle = 'rgba(255, 255, 255, 0.6)';
            for (let i = 0; i < 3; i++) {
                const x = (frameCount * 0.3 + i * 250) % (canvas.width + 100) - 50;
                ctx.beginPath();
                ctx.arc(x, 80 + i * 40, 20, 0, Math.PI * 2);
                ctx.arc(x + 25, 80 + i * 40, 25, 0, Math.PI * 2);
                ctx.arc(x + 50, 80 + i * 40, 20, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Stars
            ctx.fillStyle = '#fffacd';
            for (let i = 0; i < 5; i++) {
                const x = (frameCount * 0.5 + i * 180) % canvas.width;
                drawStar(x, 50 + i * 30, 5, 8, 4);
            }
            
            // Ground
            ctx.fillStyle = '#ffb6c1';
            ctx.fillRect(0, player.groundY + player.height, canvas.width, canvas.height);
            
            // Ground decoration
            ctx.fillStyle = '#ff69b4';
            for (let i = 0; i < canvas.width; i += 40) {
                ctx.fillRect(i, player.groundY + player.height, 20, 10);
            }
        }
        
        function drawStar(cx, cy, spikes, outerRadius, innerRadius) {
            let rot = Math.PI / 2 * 3;
            let x = cx;
            let y = cy;
            const step = Math.PI / spikes;
            
            ctx.beginPath();
            ctx.moveTo(cx, cy - outerRadius);
            for (let i = 0; i < spikes; i++) {
                x = cx + Math.cos(rot) * outerRadius;
                y = cy + Math.sin(rot) * outerRadius;
                ctx.lineTo(x, y);
                rot += step;
                
                x = cx + Math.cos(rot) * innerRadius;
                y = cy + Math.sin(rot) * innerRadius;
                ctx.lineTo(x, y);
                rot += step;
            }
            ctx.lineTo(cx, cy - outerRadius);
            ctx.closePath();
            ctx.fill();
        }
        
        function updatePlayer() {
            if (player.jumping) {
                player.velocityY += player.gravity;
                player.y += player.velocityY;
                
                if (player.y >= player.groundY) {
                    player.y = player.groundY;
                    player.jumping = false;
                    player.velocityY = 0;
                }
            }
        }
        
        function spawnObstacle() {
            const level = levels[currentLevel];
            
            if (level.hearts) {
                // Level 5: spawn hearts
                if (frameCount % 60 === 0) {
                    const isBroken = Math.random() < 0.3; // 30% broken hearts
                    hearts.push(new Heart(isBroken));
                }
                // Also spawn some flying obstacles
                if (frameCount % level.obstacleFreq === 0 && Math.random() < 0.4) {
                    obstacles.push(new Obstacle('flying'));
                }
            } else {
                if (frameCount % level.obstacleFreq === 0) {
                    const type = Math.random() < 0.7 ? 'ground' : 'flying';
                    obstacles.push(new Obstacle(type));
                }
            }
        }
        
        function gameLoop() {
            if (!gameRunning) return;
            
            frameCount++;
            const level = levels[currentLevel];
            gameSpeed = level.speed;
            
            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw
            drawBackground();
            
            // Update and draw obstacles
            obstacles.forEach((obstacle, index) => {
                obstacle.update();
                obstacle.draw();
                
                if (obstacle.collidesWith(player)) {
                    gameOver();
                }
                
                if (!obstacle.passed && obstacle.x + obstacle.width < player.x) {
                    obstacle.passed = true;
                    score += 10;
                }
                
                if (obstacle.x + obstacle.width < 0) {
                    obstacles.splice(index, 1);
                }
            });
            
            // Update and draw hearts (level 5)
            hearts.forEach((heart, index) => {
                heart.update();
                heart.draw();
                
                if (heart.collidesWith(player)) {
                    gameOver();
                }
                
                if (!heart.passed && heart.x + heart.width < player.x && !heart.broken) {
                    heart.passed = true;
                    score += 5;
                }
                
                if (heart.x + heart.width < 0) {
                    hearts.splice(index, 1);
                }
            });
            
            updatePlayer();
            drawPlayer();
            spawnObstacle();
            
            // Update score display
            document.getElementById('scoreValue').textContent = score;
            
            // Check level completion
            if (score >= level.duration) {
                levelComplete();
            }
            
            requestAnimationFrame(gameLoop);
        }
        
        function startLevel(level) {
            currentLevel = level;
            score = 0;
            frameCount = 0;
            obstacles = [];
            hearts = [];
            gameRunning = true;
            
            const levelConfig = levels[level];
            document.getElementById('levelName').textContent = levelConfig.name;
            document.getElementById('scoreValue').textContent = '0';
            
            showScreen('gameScreen');
            gameLoop();
        }
        
        function levelComplete() {
            gameRunning = false;
            playLevelCompleteSound();
            
            if (currentLevel === 5) {
                showScreen('gameComplete');
            } else {
                showScreen(`level${currentLevel}Complete`);
            }
        }
        
        function gameOver() {
            gameRunning = false;
            playCollisionSound();
            showScreen('gameOverScreen');
        }
        
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }
        
        // Controls
        document.addEventListener('keydown', (e) => {
            if (!gameRunning) return;
            
            if (e.code === 'Space' && !player.jumping) {
                e.preventDefault();
                player.jumping = true;
                player.velocityY = player.jumpPower;
                playJumpSound();
            }
            
            if (e.code === 'ShiftLeft' || e.code === 'ShiftRight') {
                e.preventDefault();
                player.ducking = true;
            }
        });
        
        document.addEventListener('keyup', (e) => {
            if (e.code === 'ShiftLeft' || e.code === 'ShiftRight') {
                player.ducking = false;
            }
        });
        
        // Touch controls
        canvas.addEventListener('touchstart', (e) => {
            e.preventDefault();
            if (!gameRunning) return;
            
            if (!player.jumping) {
                player.jumping = true;
                player.velocityY = player.jumpPower;
                playJumpSound();
            }
        });
        
        // Click to jump
        canvas.addEventListener('click', () => {
            if (!gameRunning) return;
            
            if (!player.jumping) {
                player.jumping = true;
                player.velocityY = player.jumpPower;
                playJumpSound();
            }
        });
        
        // Button events
        document.getElementById('startBtn').addEventListener('click', () => {
            playButtonSound();
            startLevel(1);
        });
        document.getElementById('level2Btn').addEventListener('click', () => {
            playButtonSound();
            startLevel(2);
        });
        document.getElementById('level3Btn').addEventListener('click', () => {
            playButtonSound();
            startLevel(3);
        });
        document.getElementById('level4Btn').addEventListener('click', () => {
            playButtonSound();
            startLevel(4);
        });
        document.getElementById('level5Btn').addEventListener('click', () => {
            playButtonSound();
            startLevel(5);
        });
        document.getElementById('restartBtn').addEventListener('click', () => {
            playButtonSound();
            showScreen('startScreen');
        });
        document.getElementById('retryBtn').addEventListener('click', () => {
            playButtonSound();
            startLevel(currentLevel);
        });
        
        // Floating hearts animation
        function createFloatingHeart() {
            const heart = document.createElement('div');
            heart.className = 'floating-heart';
            heart.textContent = '💖';
            heart.style.left = Math.random() * 100 + '%';
            heart.style.animationDelay = Math.random() * 2 + 's';
            heart.style.animationDuration = (3 + Math.random() * 2) + 's';
            document.getElementById('floatingHearts').appendChild(heart);
            
            setTimeout(() => heart.remove(), 5000);
        }
        
        setInterval(createFloatingHeart, 800);
    </script>
</body>
</html>
