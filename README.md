<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Anniversary</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .envelope-wrapper {
            position: relative;
            perspective: 1000px;
        }

        .envelope {
            width: 300px;
            height: 200px;
            position: relative;
            cursor: pointer;
            transition: transform 0.6s;
        }

        .envelope:hover {
            transform: scale(1.05);
        }

        .envelope-flap {
            width: 0;
            height: 0;
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            border-top: 100px solid #f4e4d7;
            position: absolute;
            top: 0;
            left: 0;
            transform-origin: top;
            transition: transform 0.6s;
            z-index: 3;
        }

        .envelope.open .envelope-flap {
            transform: rotateX(180deg);
        }

        .envelope-body {
            width: 300px;
            height: 150px;
            background: #f9f3ec;
            position: absolute;
            bottom: 0;
            border: 2px solid #e8d5c4;
        }

        .letter-paper {
            width: 280px;
            background: white;
            position: absolute;
            bottom: 20px;
            left: 10px;
            padding: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
            transition: transform 0.8s, bottom 0.8s;
            cursor: pointer;
            z-index: 2;
        }

        .envelope.open .letter-paper {
            transform: translateY(-50px);
            bottom: 100px;
        }

        .letter-paper-preview {
            font-size: 12px;
            color: #764ba2;
            text-align: center;
            font-style: italic;
        }

        .click-instruction {
            text-align: center;
            color: white;
            margin-top: 20px;
            font-size: 18px;
            animation: fadeInOut 2s infinite;
        }

        @keyframes fadeInOut {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }

        .letter-container {
            background: white;
            max-width: 750px;
            padding: 60px 50px;
            border-radius: 10px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            position: relative;
            display: none;
            animation: slideIn 0.8s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .letter-container.show {
            display: block;
        }

        .letter-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 5px;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px 10px 0 0;
        }

        .hearts {
            text-align: center;
            font-size: 30px;
            margin-bottom: 20px;
        }

        .heart {
            display: inline-block;
            animation: float 3s ease-in-out infinite;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .heart:nth-child(1) { animation-delay: 0s; }
        .heart:nth-child(2) { animation-delay: 0.5s; }
        .heart:nth-child(3) { animation-delay: 1s; }

        .heart:hover {
            transform: scale(1.3) rotate(10deg);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        h1 {
            text-align: center;
            color: #764ba2;
            font-size: 36px;
            margin-bottom: 30px;
            font-weight: normal;
        }

        .greeting {
            font-size: 18px;
            color: #333;
            margin-bottom: 15px;
        }

        p {
            font-size: 17px;
            line-height: 1.8;
            color: #444;
            margin-bottom: 20px;
            text-align: justify;
            opacity: 0;
            animation: fadeIn 1s forwards;
        }

        p:nth-child(3) { animation-delay: 0.2s; }
        p:nth-child(4) { animation-delay: 0.4s; }
        p:nth-child(5) { animation-delay: 0.6s; }
        p:nth-child(6) { animation-delay: 0.8s; }
        p:nth-child(7) { animation-delay: 1s; }
        p:nth-child(8) { animation-delay: 1.2s; }
        p:nth-child(9) { animation-delay: 1.4s; }
        p:nth-child(10) { animation-delay: 1.6s; }
        p:nth-child(11) { animation-delay: 1.8s; }
        p:nth-child(12) { animation-delay: 2s; }

        @keyframes fadeIn {
            to { opacity: 1; }
        }

        .highlight {
            background: linear-gradient(120deg, #ffd89b 0%, #19547b 100%);
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: bold;
        }

        .memory-gallery {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin: 30px 0;
        }

        .memory-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
            border-radius: 8px;
            color: white;
            text-align: center;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .memory-box:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        .memory-title {
            font-size: 14px;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .memory-text {
            font-size: 12px;
            opacity: 0.9;
        }

        .interactive-section {
            background: #f9f3ec;
            padding: 25px;
            border-radius: 8px;
            margin: 30px 0;
            text-align: center;
        }

        .reason-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 16px;
            border-radius: 25px;
            cursor: pointer;
            transition: transform 0.3s;
            margin: 10px;
        }

        .reason-button:hover {
            transform: scale(1.05);
        }

        .reason-display {
            margin-top: 20px;
            font-size: 18px;
            color: #764ba2;
            min-height: 30px;
            font-style: italic;
        }

        .signature {
            text-align: right;
            margin-top: 40px;
            font-style: italic;
            color: #667eea;
            font-size: 18px;
        }

        .date {
            text-align: center;
            margin-top: 30px;
            color: #888;
            font-size: 14px;
        }

        .floating-hearts {
            position: fixed;
            pointer-events: none;
            font-size: 20px;
            opacity: 0;
            animation: floatUp 4s ease-in;
        }

        @keyframes floatUp {
            0% {
                opacity: 1;
                transform: translateY(0) rotate(0deg);
            }
            100% {
                opacity: 0;
                transform: translateY(-100vh) rotate(360deg);
            }
        }

        .music-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            border: none;
            padding: 12px 20px;
            border-radius: 25px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            font-size: 16px;
            z-index: 1000;
            display: none;
        }

        .music-toggle.show {
            display: block;
        }

        @media (max-width: 768px) {
            .memory-gallery {
                grid-template-columns: 1fr;
            }
            
            .letter-container {
                padding: 40px 30px;
            }
        }
    </style>
</head>
<body>
    <button class="music-toggle" id="musicToggle">🎵 Play Music</button>
    
    <!-- Add your music file here - replace "your-song.mp3" with your actual song filename -->
    <audio id="backgroundMusic" loop>
        <source src="your-song.mp3" type="audio/mpeg">
    </audio>

    <div class="envelope-wrapper" id="envelopeWrapper">
        <div class="envelope" id="envelope">
            <div class="envelope-flap"></div>
            <div class="envelope-body"></div>
            <div class="letter-paper">
                <div class="letter-paper-preview">To my dearest love... ❤️</div>
            </div>
        </div>
        <div class="click-instruction">Click the envelope to open your letter 💌</div>
    </div>

    <div class="letter-container" id="letterContainer">
        <div class="hearts">
            <span class="heart">💕</span>
            <span class="heart">❤️</span>
            <span class="heart">💕</span>
        </div>
        <h1>Happy 3rd Anniversary</h1>
        
        <p class="greeting">Hi loves!</p>
        
        <p>Three years. It feels like just yesterday we were in Grade 11, navigating through all those ups and downs together, yet it also feels like I've known you forever. Time really does fly when you're with someone who makes every moment count.</p>
        
        <p>Looking back at those Grade 11 days, I remember the nervousness, the excitement, the challenges we faced. We were just classmates trying to figure things out, but even then, <span class="highlight">you were my constant</span>. Through every test, every drama, every moment of doubt—you were there. And you still are.</p>
        
        <div class="memory-gallery">
            <div class="memory-box">
                <div class="memory-title">✨ First Days</div>
                <div class="memory-text">When we first started talking</div>
            </div>
            <div class="memory-box">
                <div class="memory-title">🌙 Late Night Talks</div>
                <div class="memory-text">Our endless conversations</div>
            </div>
            <div class="memory-box">
                <div class="memory-title">😂 Inside Jokes</div>
                <div class="memory-text">The laughs only we understand</div>
            </div>
            <div class="memory-box">
                <div class="memory-title">💪 Tough Times</div>
                <div class="memory-text">When we got through it together</div>
            </div>
            <div class="memory-box">
                <div class="memory-title">🎉 Celebrations</div>
                <div class="memory-text">Every milestone we shared</div>
            </div>
            <div class="memory-box">
                <div class="memory-title">🌈 Today</div>
                <div class="memory-text">Still choosing each other</div>
            </div>
        </div>
        
        <p>Gusto ko lang sabihin na thank you for everything you've done for me, especially during times when I was struggling and felt lost. Without you, I wouldn't be the person I am today. You've shaped me in ways I never imagined, and I'm endlessly grateful for that. I'm so blessed that you still choose me every single day, even knowing all my flaws and imperfections.</p>
        
        <p>You've taught me what it means to be patient, to be understanding, to be vulnerable. You've shown me that love isn't just about the grand gestures—it's in the quiet moments, the comfortable silences, the way you look at me when you think I'm not paying attention. It's in the way you know exactly what to say when I'm down, and the way you celebrate with me when things go right.</p>
        
        <div class="interactive-section">
            <h3 style="color: #764ba2; margin-bottom: 15px;">Why I Love You</h3>
            <p style="font-size: 14px; margin-bottom: 15px;">My Reasons ❤️</p>
            <button class="reason-button" onclick="showReason()">Show Me</button>
            <div class="reason-display" id="reasonDisplay"></div>
        </div>
        
        <p>I promise I'll never leave your side, because I know you'd do the same for me. We're a team, and I can't imagine facing life's journey with anyone else but you. Whatever comes our way—good or bad—I know we can handle it together. That's the beauty of what we have.</p>
        
        <p>I'm sorry for the times I've been difficult or let my bad moods get the better of me. I won't make excuses for those moments, but I want you to know that you have this incredible, almost magical way of making everything better, no matter what I'm going through. Your patience, your understanding, your love—it heals me in ways words can't fully express.</p>
        
        <p>Thank you for being my safe place, my best friend, my partner in everything. Thank you for seeing the good in me even when I couldn't see it myself. Thank you for growing with me, dreaming with me, and building this beautiful life together. Thank you for every smile, every hug, every "I love you." Thank you for being <span class="highlight">exactly who you are</span>.</p>
        
        <p>You mean the world to me, loves. I wouldn't choose anyone else to spend the rest of my life with. Here's to three years down, and a lifetime more to go. Here's to more memories, more adventures, more late-night conversations, more laughter, and more love than we can possibly imagine.</p>
        
        <p>I love you more than words can say, today and always.</p>
        
        <p class="signature">Forever yours, pauppy 💜</p>
        
        <p class="date">January 2026</p>
    </div>

    <script>
        const reasons = [
            "Your smile and eyes lights up my entire world",
            "The way you understand me without words",
            "How you make ordinary moments feel special",
            "Your kindness and compassion for others",
            "The way you believe in me when I doubt myself",
            "Your laugh - it's my favorite sound",
            "How patient you are with me",
            "The little things you do to show you care",
            "Your strength during tough times",
            "The way you make me feel safe and loved",
            "How you've grown with me over these years",
            "Your beautiful heart and soul",
            "The memories we've created together",
            "How you accept all of me, flaws and all",
            "The future I see with you by my side"
        ];

        let usedReasons = [];

        function showReason() {
            if (usedReasons.length === reasons.length) {
                usedReasons = [];
            }
            
            let availableReasons = reasons.filter((_, index) => !usedReasons.includes(index));
            let randomIndex = Math.floor(Math.random() * availableReasons.length);
            let reason = availableReasons[randomIndex];
            let originalIndex = reasons.indexOf(reason);
            
            usedReasons.push(originalIndex);
            
            const display = document.getElementById('reasonDisplay');
            display.style.opacity = '0';
            
            setTimeout(() => {
                display.textContent = `"${reason}"`;
                display.style.opacity = '1';
                display.style.transition = 'opacity 0.5s';
                createFloatingHeart();
            }, 200);
        }

        function createFloatingHeart() {
            const heart = document.createElement('div');
            heart.className = 'floating-hearts';
            heart.textContent = '❤️';
            heart.style.left = Math.random() * window.innerWidth + 'px';
            heart.style.top = window.innerHeight + 'px';
            document.body.appendChild(heart);
            
            setTimeout(() => heart.remove(), 4000);
        }

        const envelope = document.getElementById('envelope');
        const envelopeWrapper = document.getElementById('envelopeWrapper');
        const letterContainer = document.getElementById('letterContainer');
        const musicToggle = document.getElementById('musicToggle');

        let envelopeClicked = false;

        envelope.addEventListener('click', function() {
            if (!envelopeClicked) {
                this.classList.add('open');
                envelopeClicked = true;
                
                setTimeout(() => {
                    envelopeWrapper.style.display = 'none';
                    letterContainer.classList.add('show');
                    musicToggle.classList.add('show');
                    
                    for(let i = 0; i < 20; i++) {
                        setTimeout(createFloatingHeart, i * 200);
                    }
                }, 1000);
            }
        });

        document.querySelectorAll('.heart').forEach(heart => {
            heart.addEventListener('click', function(e) {
                e.stopPropagation();
                createFloatingHeart();
            });
        });

        document.querySelectorAll('.memory-box').forEach(box => {
            box.addEventListener('click', function() {
                this.style.transform = 'rotate(5deg) scale(1.05)';
                setTimeout(() => {
                    this.style.transform = '';
                }, 300);
                createFloatingHeart();
            });
        });

        const audio = document.getElementById('backgroundMusic');
        let isPlaying = false;

        musicToggle.addEventListener('click', function() {
            if (!isPlaying) {
                audio.play();
                this.textContent = '🎵 Pause Music';
                this.style.background = 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';
                this.style.color = 'white';
                isPlaying = true;
            } else {
                audio.pause();
                this.textContent = '🎵 Play Music';
                this.style.background = 'white';
                this.style.color = 'black';
                isPlaying = false;
            }
        });
    </script>
</body>
</html>
