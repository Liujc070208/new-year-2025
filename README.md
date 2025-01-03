# new-year-2025
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>2025年新年快乐</title>
    <style>
        @media screen and (max-width: 768px) {
            #countdown {
                font-size: 120px;
            }

            #year {
                font-size: 140px;
            }

            #message {
                font-size: 80px;
            }

            #wish-display {
                font-size: 40px;
            }

            .lantern {
                width: 40px;
                height: 60px;
            }

            .lantern::before {
                font-size: 25px;
                line-height: 60px;
            }
        }
        @import url('https://fonts.googleapis.com/css2?family=Ma+Shan+Zheng&display=swap');
        
        body {
            margin: 0;
            padding: 0;
            background: #000;
            overflow: hidden;
            font-family: 'Ma Shan Zheng', cursive;
        }
        
        canvas {
            width: 100%;
            height: 100vh;
        }
        
        .text-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 100;
            text-align: center;
            width: 100%;
        }
        
        #countdown {
            font-size: 180px;
            color: #fff;
            text-shadow: 0 0 20px #ff3333,
                         0 0 40px #ff3333,
                         0 0 80px #ff3333;
            opacity: 0;
            transform: scale(0.5);
            transition: all 0.5s ease-out;
        }
        
        #countdown.active {
            opacity: 1;
            transform: scale(1);
        }
        
        #year {
            font-size: 200px;
            color: #fff;
            text-shadow: 0 0 20px #ffcc00,
                         0 0 40px #ffcc00,
                         0 0 80px #ffcc00;
            display: none;
            opacity: 0;
            transform: scale(0.5) rotate(-10deg);
            transition: all 0.8s ease-out;
        }
        
        #year.active {
            opacity: 1;
            transform: scale(1) rotate(0deg);
        }
        
        #message {
            font-size: 120px;
            color: #fff;
            text-shadow: 0 0 20px #ff3366,
                         0 0 40px #ff3366,
                         0 0 80px #ff3366;
            display: none;
            opacity: 0;
            transform: translateY(50px);
            transition: all 0.8s ease-out;
            margin-bottom: 20px;
        }

        #message.active {
            opacity: 1;
            transform: translateY(0);
        }
        
        #wish-display {
            font-size: 60px;
            color: #fff;
            text-shadow: 0 0 15px #ffcc00,
                         0 0 30px #ffcc00;
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
            margin-top: 20px;
            display: none;
        }
        
        #wish-display.active {
            opacity: 1;
            transform: translateY(0);
        }

        #input-container {
            position: fixed;
            top: 65%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 200;
            text-align: center;
            width: 300px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 15px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 0 20px rgba(255, 51, 102, 0.5);
            opacity: 0;
            transform: translate(-50%, -30%);
            transition: all 0.8s ease-out;
        }

        #input-container.active {
            opacity: 1;
            transform: translate(-50%, -50%);
        }

        #wish-input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 5px;
            color: #fff;
            font-size: 16px;
            font-family: 'Ma Shan Zheng', cursive;
        }

        #submit-wish {
            padding: 10px 20px;
            background: #ff3366;
            border: none;
            border-radius: 5px;
            color: #fff;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Ma Shan Zheng', cursive;
        }

        #submit-wish:hover {
            background: #ff6699;
            transform: scale(1.05);
        }

        .lantern {
            position: fixed;
            width: 60px;
            height: 80px;
            background: linear-gradient(135deg, 
                #ff2d2d 0%, 
                #ff1a1a 50%,
                #e60000 100%);
            border-radius: 30% / 15%;
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.6),
                       inset 0 5px 15px rgba(255, 255, 255, 0.2),
                       inset 0 -10px 20px rgba(0, 0, 0, 0.3);
            z-index: 90;
            animation: none;
            opacity: 0;
            transform: translateY(100vh);
        }

        .lantern.rise {
            animation: riseUp 1.5s ease-out forwards;
        }

        .lantern.swing {
            animation: swing 3s infinite ease-in-out;
        }

        .lantern::before {
            content: "福";
            position: absolute;
            color: #ffd700;
            font-size: 35px;
            width: 100%;
            height: 100%;
            text-align: center;
            line-height: 80px;
            font-weight: bold;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.5),
                         2px 2px 2px rgba(0, 0, 0, 0.3);
            animation: glowText 2s infinite alternate;
            font-family: "Ma Shan Zheng", cursive;
        }

        .lantern::after {
            content: "";
            position: absolute;
            width: 100%;
            height: 12%;
            background: linear-gradient(to bottom, 
                #ffd700 0%,
                #e60000 100%);
            border-radius: 50%;
            top: -6%;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.3),
                        inset 0 2px 3px rgba(255, 255, 255, 0.5);
            border: 1px solid #cc0000;
        }

        .lantern-top {
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 20px;
            height: 15px;
            background: #ffd700;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
        }

        .lantern-tassel {
            position: absolute;
            width: 4px;
            height: 25px;
            background: linear-gradient(to bottom, 
                #ffd700 0%,
                #ff9900 100%);
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.3);
            animation: swingTassel 3s infinite ease-in-out;
        }

        .lantern-tassel::before,
        .lantern-tassel::after {
            content: "";
            position: absolute;
            width: 4px;
            height: 25px;
            background: linear-gradient(to bottom, 
                #ffd700 0%,
                #ff9900 100%);
            bottom: 0;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.3);
        }

        .lantern-tassel::before {
            transform: rotate(24deg);
            left: -12px;
        }

        .lantern-tassel::after {
            transform: rotate(-24deg);
            right: -12px;
        }

        .lantern-decoration {
            position: absolute;
            width: 90%;
            height: 90%;
            top: 5%;
            left: 5%;
            border: 2px solid rgba(255, 215, 0, 0.3);
            border-radius: 30% / 15%;
        }

        .lantern-glow {
            position: absolute;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, 
                rgba(255, 215, 0, 0.3) 0%, 
                rgba(255, 0, 0, 0.2) 50%, 
                transparent 70%);
            animation: glow 2s infinite alternate;
            border-radius: 30% / 15%;
            filter: blur(5px);
        }

        @keyframes riseUp {
            0% {
                transform: translateY(100vh) rotate(-5deg);
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(0) rotate(-5deg);
                opacity: 1;
            }
        }

        @keyframes swing {
            0%, 100% {
                transform: rotate(-5deg);
            }
            50% {
                transform: rotate(5deg);
            }
        }

        @keyframes swingTassel {
            0%, 100% {
                transform: translateX(-50%) rotate(8deg);
            }
            50% {
                transform: translateX(-50%) rotate(-8deg);
            }
        }

        @keyframes glowText {
            0% {
                text-shadow: 0 0 5px rgba(255, 215, 0, 0.8),
                             0 0 10px rgba(255, 215, 0, 0.5),
                             2px 2px 2px rgba(0, 0, 0, 0.3);
            }
            100% {
                text-shadow: 0 0 10px rgba(255, 215, 0, 1),
                             0 0 20px rgba(255, 215, 0, 0.7),
                             0 0 30px rgba(255, 215, 0, 0.5),
                             2px 2px 2px rgba(0, 0, 0, 0.3);
            }
        }

        @keyframes glow {
            0% {
                opacity: 0.5;
                filter: brightness(1);
            }
            100% {
                opacity: 1;
                filter: brightness(1.2);
            }
        }

        .lantern-left {
            left: 50px;
            animation-delay: -1.5s, 0s;
        }

        .lantern-right {
            right: 50px;
            animation-delay: -0.5s, 0.3s;
        }

        /* 添加星星样式 */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #fff;
            border-radius: 50%;
        }

        .star.small {
            width: 1px;
            height: 1px;
        }

        .star.medium {
            width: 2px;
            height: 2px;
        }

        .star.large {
            width: 3px;
            height: 3px;
        }

        .star.twinkle-1 {
            animation: twinkle 1s infinite ease-in-out;
        }

        .star.twinkle-2 {
            animation: twinkle 1.5s infinite ease-in-out;
        }

        .star.twinkle-3 {
            animation: twinkle 2s infinite ease-in-out;
        }

        @keyframes twinkle {
            0%, 100% {
                opacity: 0.2;
                transform: scale(0.8);
            }
            50% {
                opacity: 1;
                transform: scale(1.2);
            }
        }

        #musicControl {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
            background: rgba(255, 51, 51, 0.2);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 0 20px rgba(255, 51, 51, 0.3);
        }

        #musicControl:hover {
            transform: scale(1.1);
            background: rgba(255, 51, 51, 0.3);
        }

        #musicControl.playing {
            animation: rotate 5s linear infinite;
        }

        @keyframes rotate {
            from {
                transform: rotate(0deg);
            }
            to {
                transform: rotate(360deg);
            }
        }

        #musicIcon {
            font-size: 20px;
            color: #fff;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }
    </style>
    <audio id="bgMusic" loop>
        <source src="https://link.jscdn.cn/1drv/aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBdDZScWVpYVFVWXNoUVVVVkRBbmVJZmJfY0pOP2U9ZWNkbmJH.mp3" type="audio/mpeg">
    </audio>
</head>
<body>
    <div id="musicControl">
        <span id="musicIcon">🎵</span>
    </div>
    <div class="stars"></div>
    <div class="lantern lantern-left">
        <div class="lantern-glow"></div>
        <div class="lantern-tassel"></div>
    </div>
    <div class="lantern lantern-right">
        <div class="lantern-glow"></div>
        <div class="lantern-tassel"></div>
    </div>
    <div class="text-container">
        <div id="countdown">3</div>
        <div id="year">2025</div>
        <div id="message">新年快乐</div>
        <div id="wish-display"></div>
    </div>
    <div id="input-container" style="display: none;">
        <input type="text" id="wish-input" placeholder="写下你的新年愿望..." maxlength="50">
        <button id="submit-wish">发送祝福</button>
    </div>
    <canvas id="canvas"></canvas>
    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        // 设置画布尺寸
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // 在脚本开始处添加变量声明
        let particles = [];
        let fireworks = [];

        // 烟花粒子类
        class Particle {
            constructor(x, y, hue, isMultiColor = false, angle = null, speed = null) {
                this.x = x;
                this.y = y;
                this.isMultiColor = isMultiColor;
                this.hue = isMultiColor ? Math.random() * 360 : hue + Math.random() * 30 - 15;
                
                if (angle !== null) {
                    this.velocity = {
                        x: Math.cos(angle) * speed,
                        y: Math.sin(angle) * speed
                    };
                } else {
                    this.velocity = {
                        x: (Math.random() - 0.5) * 12,
                        y: (Math.random() - 0.5) * 12
                    };
                }
                
                this.alpha = 1;
                this.friction = 0.99;
                this.gravity = 0.08;
                this.size = Math.random() * 3 + 2;
                this.decay = Math.random() * 0.001 + 0.0005;
                this.brightness = Math.random() * 30 + 70;
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = `hsla(${this.hue}, 100%, ${this.brightness}%, ${this.alpha})`;
                ctx.fill();
            }

            update() {
                this.velocity.x *= this.friction;
                this.velocity.y *= this.friction;
                this.velocity.y += this.gravity;
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                this.alpha -= this.decay;
                return this.alpha > 0;
            }
        }

        // 颜色数组
        const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff'];

        // 新年时间
        const newYearTime = new Date('2025-02-09T00:00:00').getTime();
        const countdownEl = document.getElementById('countdown');
        const newYearEl = document.getElementById('newYear');

        // 修改倒计时逻辑
        let countdownNumber = 3;
        let countdownStarted = false;
        let phase = 'countdown'; // countdown -> year -> message

        // 音乐控制
        const bgMusic = document.getElementById('bgMusic');
        const musicControl = document.getElementById('musicControl');
        const musicIcon = document.getElementById('musicIcon');
        let isMusicPlaying = false;

        // 音乐控制点击事件
        musicControl.addEventListener('click', () => {
            if (isMusicPlaying) {
                bgMusic.pause();
                musicControl.classList.remove('playing');
                musicIcon.textContent = '🎵';
            } else {
                bgMusic.play().catch(e => console.log('Music play failed:', e));
                musicControl.classList.add('playing');
                musicIcon.textContent = '🎶';
            }
            isMusicPlaying = !isMusicPlaying;
        });

        function startCountdown() {
            if (!countdownStarted) {
                countdownStarted = true;
                const countdownEl = document.getElementById('countdown');
                countdownEl.style.display = 'block';
                countdownEl.classList.add('active');

                const countInterval = setInterval(() => {
                    countdownNumber--;
                    if (countdownNumber > 0) {
                        countdownEl.classList.remove('active');
                        setTimeout(() => {
                            countdownEl.textContent = countdownNumber;
                            countdownEl.classList.add('active');
                        }, 500);
                    } else {
                        clearInterval(countInterval);
                        countdownEl.classList.remove('active');
                        setTimeout(() => {
                            countdownEl.style.display = 'none';
                            showYear();
                        }, 500);
                    }
                }, 1500);

                // 尝试播放背景音乐
                bgMusic.play().then(() => {
                    isMusicPlaying = true;
                    musicControl.classList.add('playing');
                    musicIcon.textContent = '🎶';
                }).catch(e => console.log('Auto play failed:', e));
            }
        }

        function showYear() {
            const yearEl = document.getElementById('year');
            yearEl.style.display = 'block';
            setTimeout(() => yearEl.classList.add('active'), 100);
            
            createMultipleFireworks();

            setTimeout(() => {
                yearEl.classList.remove('active');
                setTimeout(() => {
                    yearEl.style.display = 'none';
                    showMessage();
                }, 800);
            }, 2000);
        }

        function showMessage() {
            const messageEl = document.getElementById('message');
            const inputContainer = document.getElementById('input-container');
            
            messageEl.style.display = 'block';
            setTimeout(() => {
                messageEl.classList.add('active');
            }, 100);
            
            setInterval(createMultipleFireworks, 2000);
            
            // 显示输入框
            setTimeout(() => {
                inputContainer.style.display = 'block';
                setTimeout(() => {
                    inputContainer.classList.add('active');
                }, 100);
            }, 1000);
        }

        function createMultipleFireworks() {
            for(let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const x = Math.random() * canvas.width;
                    const y = canvas.height * 0.3 + Math.random() * (canvas.height * 0.4);
                    fireworks.push(new Firework(x, y));
                }, i * 200);
            }
        }

        // 修改烟花发射器，新年特效
        class Firework {
            constructor(targetX, targetY) {
                this.x = targetX;
                this.y = canvas.height;
                this.targetY = targetY;
                this.speed = 15 + Math.random() * 5;
                this.angle = Math.atan2(targetY - this.y, 0);
                this.hue = Math.random() * 360;
                this.trail = [];
                this.size = 3;
                this.shouldExplode = false;
                this.specialEffect = Math.random() < 0.3; // 30%概率产生特殊效果
            }

            draw() {
                for(let i = 0; i < this.trail.length; i++) {
                    const pos = this.trail[i];
                    const alpha = i / this.trail.length * 0.3;
                    ctx.beginPath();
                    ctx.arc(pos.x, pos.y, this.size * 0.5, 0, Math.PI * 2);
                    ctx.fillStyle = `hsla(${this.hue}, 100%, 60%, ${alpha})`;
                    ctx.fill();
                }

                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = `hsl(${this.hue}, 100%, 60%)`;
                ctx.fill();
            }

            update() {
                this.trail.push({x: this.x, y: this.y});
                if(this.trail.length > 5) {
                    this.trail.shift();
                }
                this.y -= this.speed;
                return this.y > this.targetY;
            }
        }

        // 修改爆炸效果，添加新年特效
        function createExplosion(x, y, hue) {
            const patterns = [
                // 普通圆形爆炸
                () => {
                    const particleCount = 100;
                    const angleStep = (Math.PI * 2) / particleCount;
                    for(let i = 0; i < particleCount; i++) {
                        const angle = angleStep * i;
                        const speed = 8 + Math.random() * 4;
                        particles.push(new Particle(x, y, hue, true, angle, speed));
                    }
                },
                // "福"形状
                () => {
                    const points = [
                        // 简化的"福"字点阵，可以根据需要调整
                        {x: 0, y: -20}, {x: 20, y: -10}, {x: -20, y: 0},
                        {x: 0, y: 0}, {x: 20, y: 10}, {x: -20, y: 20},
                        {x: 0, y: 20}
                    ];
                    points.forEach(point => {
                        for(let i = 0; i < 5; i++) {
                            const angle = Math.random() * Math.PI * 2;
                            const speed = 2 + Math.random() * 2;
                            particles.push(new Particle(
                                x + point.x,
                                y + point.y,
                                hue,
                                true,
                                angle,
                                speed
                            ));
                        }
                    });
                }
            ];

            // 随机选择爆炸模式
            const pattern = patterns[Math.floor(Math.random() * patterns.length)];
            pattern();
        }

        // 修改动画循环
        function animate() {
            requestAnimationFrame(animate);
            ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.globalCompositeOperation = 'lighter';

            // 更新烟花
            for(let i = fireworks.length - 1; i >= 0; i--) {
                const firework = fireworks[i];
                if (!firework.update()) {
                    createExplosion(firework.x, firework.y, firework.hue);
                    fireworks.splice(i, 1);
                }
                firework.draw();
            }

            // 更新粒子
            for(let i = particles.length - 1; i >= 0; i--) {
                const particle = particles[i];
                if (!particle.update()) {
                    particles.splice(i, 1);
                } else {
                    particle.draw();
                }
            }

            ctx.globalCompositeOperation = 'source-over';
        }

        // 修改点击事件
        canvas.addEventListener('click', (e) => {
            if (!countdownStarted) {
                startCountdown();
            }
        });

        // 添加点击节流
        let lastClickTime = 0;

        // 启动动画
        animate();

        // 窗口大小改变时重置画布尺寸
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // 修改提交愿望的处理函数
        document.getElementById('submit-wish').addEventListener('click', () => {
            const wish = document.getElementById('wish-input').value.trim();
            if (wish) {
                const wishDisplay = document.getElementById('wish-display');
                wishDisplay.textContent = wish;
                wishDisplay.style.display = 'block';
                
                // 隐藏输入框
                document.getElementById('input-container').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('input-container').style.display = 'none';
                    // 显示愿望
                    setTimeout(() => {
                        wishDisplay.classList.add('active');
                    }, 100);
                }, 800);

                // 触发更多烟花
                createMultipleFireworks();
            }
        });

        // 创建星星背景
        function createStars() {
            const starsContainer = document.querySelector('.stars');
            const starCount = 200; // 星星数量

            for(let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                
                // 随机大小
                const sizes = ['small', 'medium', 'large'];
                star.classList.add(sizes[Math.floor(Math.random() * sizes.length)]);
                
                // 随机闪烁动画
                star.classList.add(`twinkle-${Math.floor(Math.random() * 3 + 1)}`);
                
                // 随机位置
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                
                // 随机延迟
                star.style.animationDelay = `${Math.random() * 2}s`;
                
                starsContainer.appendChild(star);
            }
        }

        // 修改创建灯笼函数
        function createLanterns() {
            const lanternCount = Math.floor(window.innerHeight / 300);
            const leftContainer = document.createElement('div');
            const rightContainer = document.createElement('div');
            
            leftContainer.style.position = 'fixed';
            rightContainer.style.position = 'fixed';
            leftContainer.style.left = '50px';
            rightContainer.style.right = '50px';
            leftContainer.style.top = '0';
            rightContainer.style.top = '0';
            leftContainer.style.height = '100%';
            rightContainer.style.height = '100%';
            
            for(let i = 0; i < lanternCount; i++) {
                const leftLantern = document.createElement('div');
                const rightLantern = document.createElement('div');
                
                leftLantern.className = 'lantern';
                rightLantern.className = 'lantern';
                
                leftLantern.style.top = `${(i * 300) + 50}px`;
                rightLantern.style.top = `${(i * 300) + 200}px`;
                
                // 添加内容
                leftLantern.innerHTML = `
                    <div class="lantern-glow"></div>
                    <div class="lantern-tassel"></div>
                `;
                rightLantern.innerHTML = `
                    <div class="lantern-glow"></div>
                    <div class="lantern-tassel"></div>
                `;
                
                leftContainer.appendChild(leftLantern);
                rightContainer.appendChild(rightLantern);

                // 延迟添加动画类
                setTimeout(() => {
                    leftLantern.classList.add('rise');
                    rightLantern.classList.add('rise');
                    
                    // 上升动画结束后添加摇摆动画
                    setTimeout(() => {
                        leftLantern.classList.add('swing');
                        rightLantern.classList.add('swing');
                    }, 1500);
                }, i * 200);
            }
            
            document.body.appendChild(leftContainer);
            document.body.appendChild(rightContainer);
        }

        // 页面加载时创建星星和灯笼
        window.addEventListener('load', () => {
            createStars();
            createLanterns();
            bgMusic.volume = 0.5; // 设置适中的音量
        });

        // 窗口大小改变时重新创建灯笼
        window.addEventListener('resize', () => {
            const containers = document.querySelectorAll('div[style*="position: fixed"]');
            containers.forEach(container => {
                if(container.querySelector('.lantern')) {
                    container.remove();
                }
            });
            createLanterns();
        });
    </script>
</body>
</html>
