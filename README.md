<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BrightWay - Innovación en Seguridad Vial</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            --primary: #FF6B35;
            --primary-light: #FF8C42;
            --accent: #FFC107;
            --dark: #0A0A0A;
            --darker: #000000;
            --gray-600: #404040;
            --gray-400: #888888;
            --gray-300: #CCCCCC;
            --white: #FFFFFF;
            --success: #10B981;
            --danger: #EF4444;
            --shield: #3B82F6;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, var(--darker) 0%, var(--dark) 100%);
            color: var(--white);
            min-height: 100vh;
            line-height: 1.6;
            overflow-x: hidden;
        }

        .audio-controls {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 2000;
        }

        .audio-btn {
            width: 48px;
            height: 48px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            color: var(--white);
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }

        .audio-btn:hover {
            background: rgba(255, 107, 53, 0.3);
            border-color: var(--primary);
            transform: scale(1.1);
        }

        .volume-panel {
            position: fixed;
            top: 80px;
            right: 20px;
            z-index: 1999;
            background: rgba(10, 10, 10, 0.95);
            padding: 1.5rem;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            display: none;
            min-width: 280px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
        }

        .volume-panel.show {
            display: block;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .volume-panel h4 {
            color: var(--primary);
            font-size: 0.9rem;
            margin-bottom: 1rem;
            text-align: center;
        }

        .music-selector {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.75rem;
            margin-bottom: 1.5rem;
        }

        .music-option {
            width: 100%;
            aspect-ratio: 1;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .music-option:hover {
            background: rgba(255, 107, 53, 0.2);
            border-color: var(--primary);
            transform: scale(1.05);
        }

        .music-option.active {
            background: rgba(255, 107, 53, 0.3);
            border-color: var(--primary);
            box-shadow: 0 0 15px rgba(255, 107, 53, 0.4);
        }

        .volume-control {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .volume-row {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .mute-btn {
            width: 36px;
            height: 36px;
            min-width: 36px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            color: var(--white);
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .mute-btn:hover {
            background: rgba(255, 107, 53, 0.2);
            border-color: var(--primary);
        }

        .mute-btn.muted {
            background: rgba(239, 68, 68, 0.2);
            border-color: var(--danger);
            color: var(--danger);
        }

        .volume-slider-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .volume-label {
            font-size: 0.8rem;
            color: var(--gray-400);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .volume-value {
            font-size: 0.8rem;
            color: var(--accent);
            font-weight: 600;
        }

        .volume-slider {
            -webkit-appearance: none;
            appearance: none;
            width: 100%;
            height: 6px;
            border-radius: 3px;
            background: rgba(255, 255, 255, 0.1);
            outline: none;
            cursor: pointer;
        }

        .volume-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .volume-slider::-webkit-slider-thumb:hover {
            transform: scale(1.2);
            box-shadow: 0 0 15px rgba(255, 107, 53, 0.6);
        }

        .volume-slider::-moz-range-thumb {
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            cursor: pointer;
            border: none;
            transition: all 0.3s ease;
        }

        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            z-index: 1000;
            padding: 1.5rem 0;
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 0 1.5rem;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 1.75rem;
            font-weight: 700;
            color: var(--primary);
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        main {
            padding-top: 100px;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        .hero {
            padding: 4rem 0;
            text-align: center;
        }

        .hero-title {
            font-size: clamp(2.5rem, 8vw, 5rem);
            font-weight: 800;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1rem;
            line-height: 1.1;
        }

        .hero-subtitle {
            font-size: clamp(1rem, 4vw, 1.25rem);
            color: var(--gray-400);
            margin-bottom: 2rem;
            font-weight: 400;
        }

        .hero-description {
            max-width: 700px;
            margin: 0 auto 3rem;
            font-size: clamp(0.95rem, 3vw, 1.1rem);
            color: var(--gray-300);
            line-height: 1.8;
        }

        .product-showcase {
            margin: 3rem 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 350px;
        }

        .trafitambo {
            position: relative;
            width: 120px;
            height: 250px;
            margin: 0 auto;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotateY(0deg); }
            33% { transform: translateY(-10px) rotateY(120deg); }
            66% { transform: translateY(5px) rotateY(240deg); }
        }

        .trafitambo-body {
            width: 100%;
            height: 200px;
            background: linear-gradient(180deg, var(--primary) 0%, var(--primary-light) 50%, var(--primary) 100%);
            border-radius: 12px;
            position: relative;
            box-shadow: 0 20px 60px rgba(255, 107, 53, 0.3);
        }

        .reflective-stripe {
            position: absolute;
            width: 100%;
            height: 20px;
            background: var(--white);
            top: 60px;
            opacity: 0.9;
            animation: shine 3s ease-in-out infinite;
        }

        @keyframes shine {
            0%, 100% { opacity: 0.9; }
            50% { opacity: 1; box-shadow: 0 0 20px rgba(255, 255, 255, 0.5); }
        }

        .solar-panel {
            position: absolute;
            top: -30px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 50px;
            background: linear-gradient(135deg, #1E3A8A, #3B82F6);
            border-radius: 8px;
            border: 2px solid #60A5FA;
            box-shadow: 0 10px 30px rgba(59, 130, 246, 0.4);
        }

        .led-strip {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 8px;
        }

        .led {
            width: 8px;
            height: 8px;
            background: var(--accent);
            border-radius: 50%;
            box-shadow: 0 0 15px var(--accent);
            animation: blink 2s ease-in-out infinite;
        }

        .led:nth-child(2) { animation-delay: 0.5s; }
        .led:nth-child(3) { animation-delay: 1s; }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            25%, 75% { opacity: 0.3; }
        }

        .btn-play {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: var(--white);
            border: none;
            padding: 1.25rem 3rem;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 53, 0.3);
            margin: 0.5rem;
        }

        .btn-play:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(255, 107, 53, 0.5);
        }

        .features {
            padding: 4rem 0;
            background: rgba(255, 255, 255, 0.02);
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            padding: 2rem;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            cursor: pointer;
        }

        .feature-card:hover {
            transform: translateY(-8px);
            border-color: rgba(255, 107, 53, 0.3);
            box-shadow: 0 20px 60px rgba(255, 107, 53, 0.1);
        }

        .feature-icon {
            width: 48px;
            height: 48px;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .feature-title {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 0.75rem;
        }

        .feature-description {
            color: var(--gray-400);
            font-size: 0.95rem;
            line-height: 1.6;
        }

        .game-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: rgba(0, 0, 0, 0.98);
            z-index: 3000;
            display: none;
        }

        .game-modal.active {
            display: block;
        }

        .game-container {
            width: 100%;
            height: 100%;
            position: relative;
        }

        #gameCanvas {
            width: 100%;
            height: 100%;
            display: block;
        }

        .game-hud {
            position: absolute;
            top: 15px;
            left: 15px;
            right: 15px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: 1rem;
            pointer-events: none;
            z-index: 10;
        }

        .hud-stat {
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 107, 53, 0.4);
            border-radius: 16px;
            padding: 0.85rem 1.2rem;
            pointer-events: auto;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.6);
            min-width: 110px;
        }

        .hud-label {
            font-size: 0.85rem;
            color: var(--gray-400);
            margin-bottom: 0.25rem;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            font-weight: 600;
        }

        .hud-value {
            font-size: 1.4rem;
            font-weight: 800;
            color: var(--accent);
        }

        .speed-value {
            font-size: 1.8rem;
            font-weight: 900;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .speed-unit {
            font-size: 0.85rem;
            color: var(--gray-400);
            margin-left: 3px;
        }

        .game-controls {
            position: absolute;
            bottom: 15px;
            left: 15px;
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
            z-index: 10;
        }

        .btn {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: var(--white);
            border: none;
            padding: 0.9rem 1.8rem;
            border-radius: 50px;
            font-size: 1.05rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 160px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(255, 107, 53, 0.3);
        }

        .btn:hover:not(:disabled) {
            transform: translateX(5px);
            box-shadow: 0 6px 25px rgba(255, 107, 53, 0.5);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn-exit {
            background: linear-gradient(135deg, var(--danger), #DC2626);
        }

        .btn-brightway {
            background: linear-gradient(135deg, var(--accent), #D97706);
            position: relative;
            overflow: hidden;
        }

        .btn-brightway.active {
            animation: pulse 1s ease-in-out infinite;
        }

        .btn-shield {
            background: linear-gradient(135deg, var(--shield), #2563EB);
            position: relative;
            overflow: hidden;
        }

        .btn-shield.active {
            animation: shieldPulse 1s ease-in-out infinite;
            box-shadow: 0 0 30px rgba(59, 130, 246, 0.8);
        }

        .btn-shield.blink {
            animation: shieldBlink 0.3s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { box-shadow: 0 0 25px rgba(255, 193, 7, 0.6); }
            50% { box-shadow: 0 0 45px rgba(255, 193, 7, 0.9); }
        }

        @keyframes shieldPulse {
            0%, 100% { box-shadow: 0 0 25px rgba(59, 130, 246, 0.6); }
            50% { box-shadow: 0 0 45px rgba(59, 130, 246, 0.9); }
        }

        @keyframes shieldBlink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }

        .selector-screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 100;
            padding: 1rem;
        }

        .selector-screen.hidden {
            display: none;
        }

        .selector-content {
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            padding: 2rem;
            border-radius: 20px;
            border: 3px solid var(--primary);
            text-align: center;
            max-width: 90%;
            width: 600px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .selector-content h2 {
            color: var(--primary);
            font-size: clamp(1.5rem, 5vw, 2.2rem);
            margin-bottom: 1rem;
        }

        .selector-content p {
            color: var(--gray-400);
            margin-bottom: 1.5rem;
            font-size: clamp(0.9rem, 3vw, 1.1rem);
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .option-card {
            background: rgba(255, 255, 255, 0.05);
            border: 3px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .option-card:hover {
            transform: scale(1.05);
            border-color: rgba(255, 255, 255, 0.3);
        }

        .option-card.selected {
            border-color: var(--primary);
            box-shadow: 0 0 30px rgba(255, 107, 53, 0.5);
            transform: scale(1.05);
        }

        .map-preview {
            width: 100%;
            height: 100px;
            border-radius: 12px;
            margin-bottom: 0.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            position: relative;
            overflow: hidden;
        }

        .map-preview.city {
            background: linear-gradient(135deg, #1a1a2e, #16213e);
        }

        .map-preview.snow {
            background: linear-gradient(135deg, #e0f2fe, #bae6fd);
        }

        .map-preview.volcano {
            background: linear-gradient(135deg, #450a0a, #7f1d1d);
        }

        .car-preview {
            width: 100%;
            height: 60px;
            border-radius: 12px;
            margin-bottom: 0.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .car-preview::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 35%;
            background: linear-gradient(180deg, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.3) 100%);
            border-radius: 12px 12px 0 0;
        }

        .car-preview.blue {
            background: linear-gradient(135deg, #3B82F6, #1E40AF);
            box-shadow: 0 8px 24px rgba(59, 130, 246, 0.4);
        }

        .car-preview.red {
            background: linear-gradient(135deg, #EF4444, #DC2626);
            box-shadow: 0 8px 24px rgba(239, 68, 68, 0.4);
        }

        .car-preview.yellow {
            background: linear-gradient(135deg, #FBBF24, #F59E0B);
            box-shadow: 0 8px 24px rgba(251, 191, 36, 0.4);
        }

        .car-preview.green {
            background: linear-gradient(135deg, #059669, #047857);
            box-shadow: 0 8px 24px rgba(5, 150, 105, 0.4);
        }

        .option-card h3 {
            color: var(--white);
            font-size: clamp(0.9rem, 3vw, 1.15rem);
            margin: 0;
        }

        .game-over-screen {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 10, 10, 0.97);
            backdrop-filter: blur(20px);
            padding: 3rem;
            border-radius: 24px;
            border: 3px solid var(--primary);
            text-align: center;
            display: none;
            z-index: 100;
            max-width: 90%;
        }

        .game-over-screen.show {
            display: block;
            animation: fadeInScale 0.4s ease;
        }

        @keyframes fadeInScale {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            100% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        }

        .game-over-screen h2 {
            color: var(--primary);
            font-size: clamp(1.8rem, 6vw, 2.8rem);
            margin-bottom: 1.5rem;
        }

        .final-score {
            font-size: clamp(2.5rem, 8vw, 3.5rem);
            color: var(--accent);
            font-weight: 800;
            margin-bottom: 2rem;
        }

        footer {
            padding: 3rem 0 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
            text-align: center;
            color: var(--gray-400);
            background: rgba(255, 255, 255, 0.02);
        }

        .footer-logo {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .footer-logo .company-name {
            font-size: 1.25rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .instructions {
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 2rem;
            margin-top: 2rem;
            text-align: left;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
        }

        .instructions h4 {
            color: var(--primary);
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }

        .instructions p {
            color: var(--gray-300);
            font-size: 1rem;
            margin-bottom: 0.8rem;
            line-height: 1.6;
        }

        @media (max-width: 768px) {
            .options-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 0.8rem;
            }

            .selector-content {
                padding: 1.5rem;
            }

            .hud-stat {
                padding: 0.6rem 0.9rem;
                min-width: 90px;
            }

            .hud-label {
                font-size: 0.7rem;
            }

            .hud-value {
                font-size: 1.1rem;
            }

            .speed-value {
                font-size: 1.4rem;
            }

            .btn {
                padding: 0.8rem 1.5rem;
                font-size: 0.95rem;
                min-width: 140px;
            }

            .audio-controls {
                top: 80px;
            }
        }
    </style>
</head>
<body>
    <div class="audio-controls">
        <button class="audio-btn" id="volumeBtn" title="Volumen">🎧</button>
    </div>

    <div class="volume-panel" id="volumePanel">
        <h4>Control de Volumen</h4>
        
        <div class="music-selector">
            <div class="music-option" id="marioMusic" title="Super Mario Bros">🍄</div>
            <div class="music-option active" id="megaloMusic" title="Megalovania">💀</div>
            <div class="music-option" id="starWarsMusic" title="Star Wars">⭐</div>
            <div class="music-option" id="tetrisMusic" title="Tetris">🧱</div>
            <div class="music-option" id="piratesMusic" title="Pirates">🏴‍☠️</div>
            <div class="music-option" id="pokemonMusic" title="Pokémon">⚡</div>
        </div>
        
        <div class="volume-control">
            <div class="volume-row">
                <button class="mute-btn" id="musicMuteBtn" title="Silenciar música">🎵</button>
                <div class="volume-slider-container">
                    <div class="volume-label">
                        <span>Música</span>
                        <span class="volume-value" id="musicVolumeValue">30%</span>
                    </div>
                    <input type="range" min="0" max="100" value="30" class="volume-slider" id="musicVolume">
                </div>
            </div>
            <div class="volume-row">
                <button class="mute-btn" id="soundMuteBtn" title="Silenciar efectos">🔊</button>
                <div class="volume-slider-container">
                    <div class="volume-label">
                        <span>Efectos</span>
                        <span class="volume-value" id="soundVolumeValue">50%</span>
                    </div>
                    <input type="range" min="0" max="100" value="50" class="volume-slider" id="soundVolume">
                </div>
            </div>
        </div>
    </div>

    <nav>
        <div class="nav-container">
            <div class="logo">
                <div class="logo-icon">💡</div>
                BrightWay
            </div>
        </div>
    </nav>

    <main>
        <div class="container">
            <div class="hero">
                <h1 class="hero-title">BrightWay</h1>
                <p class="hero-subtitle">Dale luz a tu camino</p>
                <p class="hero-description">
                    BrightWay vela por tu seguridad al implementar tecnologías modernas y buenas para el ambiente. 
                    Un innovador sistema de señalización vial que combina un trafitambo tradicional con tecnología 
                    solar avanzada, proporcionando iluminación autónoma y sostenible para mejorar la seguridad vial.
                </p>
            </div>

            <div class="product-showcase">
                <div class="trafitambo">
                    <div class="solar-panel"></div>
                    <div class="trafitambo-body">
                        <div class="reflective-stripe"></div>
                        <div class="led-strip">
                            <div class="led"></div>
                            <div class="led"></div>
                            <div class="led"></div>
                        </div>
                    </div>
                </div>
            </div>

            <div style="text-align: center;">
                <button class="btn-play" id="playGameBtn">🎮 Jugar Racing 3D</button>
                <button class="btn-play" id="instructionsBtn" style="background: rgba(255, 255, 255, 0.1);">📖 Controles</button>
            </div>
        </div>

        <div class="features">
            <div class="container">
                <div class="features-grid">
                    <div class="feature-card">
                        <div class="feature-icon">☀️</div>
                        <h3 class="feature-title">Energía Solar</h3>
                        <p class="feature-description">Panel solar móvil con servomotores para optimizar la captación de energía durante todo el día.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">💡</div>
                        <h3 class="feature-title">Iluminación LED</h3>
                        <p class="feature-description">Sistema de LEDs de alta eficiencia con sensor de luz para máxima visibilidad nocturna.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">🌱</div>
                        <h3 class="feature-title">Eco-Amigable</h3>
                        <p class="feature-description">Tecnología 100% sustentable que no requiere conexión eléctrica externa.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">🔧</div>
                        <h3 class="feature-title">Arduino Nano</h3>
                        <p class="feature-description">Control inteligente mediante microcontrolador para gestión automática del sistema.</p>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <footer>
        <div class="container">
            <div class="footer-logo">
                <div class="logo-icon">💡</div>
                <span class="company-name">BrightWay Technologies</span>
            </div>
            <div style="color: var(--gray-400); margin: 1rem 0;">
                Desarrollado por: <strong style="color: var(--primary);">Pablo Nicolas Garcia Huerta</strong> y <strong style="color: var(--primary);">Angel Antonio Ruiz Garcia</strong>
            </div>
            <div style="font-size: 0.85rem; margin-bottom: 1rem;">Universidad Autónoma de Querétaro - Facultad de Ingeniería</div>
            <div style="font-size: 0.8rem; padding-top: 1rem; border-top: 1px solid rgba(255, 255, 255, 0.05);">
                © 2025 BrightWay Technologies. Todos los derechos reservados.
            </div>
        </div>
    </footer>

    <div class="game-modal" id="gameModal">
        <div class="game-container">
            <div class="selector-screen" id="mapSelectorScreen">
                <div class="selector-content">
                    <h2>🗺️ Elige tu Mapa</h2>
                    <p>Selecciona el escenario donde quieres correr</p>
                    
                    <div class="options-grid">
                        <div class="option-card" data-map="city">
                            <div class="map-preview city">🌃</div>
                            <h3>Ciudad Nocturna</h3>
                        </div>
                        <div class="option-card" data-map="snow">
                            <div class="map-preview snow">🏔️</div>
                            <h3>Montañas Nevadas</h3>
                        </div>
                        <div class="option-card" data-map="volcano">
                            <div class="map-preview volcano">🌋</div>
                            <h3>Volcán Ardiente</h3>
                        </div>
                    </div>
                </div>
            </div>

            <div class="selector-screen hidden" id="carSelectorScreen">
                <div class="selector-content">
                    <h2>🎮 Elige tu Auto</h2>
                    <p>Selecciona el color de tu vehículo para comenzar</p>
                    
                    <div class="options-grid">
                        <div class="option-card" data-color="blue">
                            <div class="car-preview blue"></div>
                            <h3>Azul Eléctrico</h3>
                        </div>
                        <div class="option-card" data-color="red">
                            <div class="car-preview red"></div>
                            <h3>Rojo Furioso</h3>
                        </div>
                        <div class="option-card" data-color="yellow">
                            <div class="car-preview yellow"></div>
                            <h3>Amarillo Solar</h3>
                        </div>
                        <div class="option-card" data-color="green">
                            <div class="car-preview green"></div>
                            <h3>Verde Esmeralda</h3>
                        </div>
                    </div>
                </div>
            </div>

            <canvas id="gameCanvas"></canvas>
            
            <div class="game-hud">
                <div class="hud-stat">
                    <div class="hud-label">Puntos</div>
                    <div class="hud-value" id="score">0</div>
                </div>
                <div class="hud-stat">
                    <div class="hud-label">Record</div>
                    <div class="hud-value" id="highScore">0</div>
                </div>
                <div class="hud-stat">
                    <div class="hud-label">Velocidad</div>
                    <div>
                        <span class="speed-value" id="speedValue">0</span>
                        <span class="speed-unit">km/h</span>
                    </div>
                </div>
            </div>
            
            <div class="game-controls">
                <button class="btn btn-shield" id="shieldBtn">🛡️ Escudo</button>
                <button class="btn btn-brightway" id="brightwayBtn">💡 BrightWay</button>
                <button class="btn btn-exit" id="menuBtn">🚪 Salir</button>
                <button class="btn" id="pauseBtn">⏸ Pausar</button>
            </div>
            
            <div class="game-over-screen" id="gameOverScreen">
                <h2>¡Juego Terminado!</h2>
                <div class="final-score">Puntuación: <span id="finalScore">0</span></div>
                <button class="btn" id="restartBtn" style="font-size: 1.1rem; padding: 1rem 2.5rem;">🔄 Jugar de Nuevo</button>
            </div>
        </div>
    </div>

    <div class="game-modal" id="instructionsModal">
        <div class="game-container" style="display: flex; align-items: center; justify-content: center; background: rgba(0,0,0,0.95);">
            <div class="instructions">
                <h4>Controles del Juego</h4>
                <p><strong>Teclado PC:</strong></p>
                <p>• <strong>← →</strong> - Mover el auto izquierda/derecha</p>
                <p>• <strong>↑ ↓</strong> - Acelerar/Frenar</p>
                <p>• <strong>ESPACIO</strong> - Activar BrightWay (iluminación especial)</p>
                <p>• <strong>S</strong> - Activar Escudo (protección 10 segundos)</p>
                
                <h4 style="margin-top: 1.5rem;">Móvil/Táctil:</h4>
                <p>• Tocar izquierda/derecha de la pantalla para girar</p>
                <p>• Botón 🛡️ Escudo para protección temporal</p>
                <p>• Botón 💡 BrightWay para activar iluminación</p>
                <p>• El auto acelera automáticamente</p>
                
                <h4 style="margin-top: 1.5rem;">Poderes:</h4>
                <p>• <strong>🛡️ Escudo:</strong> Te protege de choques por 10 segundos. Parpadea cuando está por acabarse.</p>
                <p>• <strong>💡 BrightWay:</strong> Ilumina el camino y otorga puntos extra por 5 segundos.</p>
                
                <h4 style="margin-top: 1.5rem;">Objetivo:</h4>
                <p>• Esquiva los obstáculos en la carretera</p>
                <p>• Usa los poderes estratégicamente</p>
                <p>• La velocidad aumenta progresivamente sin límite</p>
                <p>• ¡Consigue el máximo puntaje!</p>
                
                <div style="text-align: center; margin-top: 2rem;">
                    <button class="btn-play" onclick="document.getElementById('instructionsModal').classList.remove('active')">Entendido</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let musicOn = true;
        let soundOn = true;
        let bgMusic = null;
        let musicVol = 0.3;
        let soundVol = 0.5;
        let panelOpen = false;
        let musicType = 'megalo';

        const marioNotes = [
            {f:659.25,d:0.12},{f:659.25,d:0.24},{f:659.25,d:0.24},{f:523.25,d:0.12},
            {f:659.25,d:0.24},{f:783.99,d:0.48},{f:392,d:0.48},{f:523.25,d:0.36},
            {f:392,d:0.36},{f:329.63,d:0.36},{f:440,d:0.36},{f:493.88,d:0.32},
            {f:466.16,d:0.28},{f:440,d:0.32},{f:392,d:0.24},{f:659.25,d:0.24},
            {f:783.99,d:0.24},{f:880,d:0.28},{f:698.46,d:0.24},{f:783.99,d:0.24},
            {f:659.25,d:0.32},{f:523.25,d:0.24},{f:587.33,d:0.24},{f:493.88,d:0.32}
        ];

        const megaloNotes = [
            {f:293.66,d:0.15},{f:293.66,d:0.15},{f:587.33,d:0.3},{f:440,d:0.3},
            {f:415.3,d:0.25},{f:392,d:0.25},{f:349.23,d:0.25},{f:293.66,d:0.15},
            {f:349.23,d:0.15},{f:392,d:0.15},{f:261.63,d:0.15},{f:261.63,d:0.15},
            {f:587.33,d:0.3},{f:440,d:0.3},{f:415.3,d:0.25},{f:392,d:0.25},
            {f:349.23,d:0.25},{f:293.66,d:0.15},{f:349.23,d:0.15},{f:392,d:0.15}
        ];

        const starWarsNotes = [
            {f:392,d:0.3},{f:392,d:0.3},{f:392,d:0.3},{f:523.25,d:0.5},
            {f:783.99,d:0.5},{f:698.46,d:0.25},{f:659.25,d:0.25},{f:587.33,d:0.25},
            {f:1046.5,d:0.5},{f:783.99,d:0.4},{f:698.46,d:0.25},{f:659.25,d:0.25},
            {f:587.33,d:0.25},{f:1046.5,d:0.5},{f:783.99,d:0.4}
        ];

        const tetrisNotes = [
            {f:659.25,d:0.4},{f:493.88,d:0.2},{f:523.25,d:0.2},{f:587.33,d:0.4},
            {f:523.25,d:0.2},{f:493.88,d:0.2},{f:440,d:0.4},{f:440,d:0.2},
            {f:523.25,d:0.2},{f:659.25,d:0.4},{f:587.33,d:0.2},{f:523.25,d:0.2},
            {f:493.88,d:0.6},{f:523.25,d:0.2},{f:587.33,d:0.4}
        ];

        const piratesNotes = [
            {f:220,d:0.2},{f:261.63,d:0.2},{f:293.66,d:0.15},{f:293.66,d:0.15},
            {f:293.66,d:0.2},{f:329.63,d:0.2},{f:349.23,d:0.15},{f:349.23,d:0.15},
            {f:349.23,d:0.2},{f:392,d:0.2},{f:220,d:0.2},{f:261.63,d:0.2}
        ];

        const pokemonNotes = [
            {f:440,d:0.3},{f:440,d:0.2},{f:440,d:0.3},{f:440,d:0.3},{f:392,d:0.2},
            {f:329.63,d:0.2},{f:261.63,d:0.35},{f:261.63,d:0.3},{f:440,d:0.2},
            {f:440,d:0.3},{f:392,d:0.2},{f:349.23,d:0.2},{f:392,d:0.35}
        ];

        const musicLibrary = {mario: marioNotes, megalo: megaloNotes, starWars: starWarsNotes, tetris: tetrisNotes, pirates: piratesNotes, pokemon: pokemonNotes};

        function playClick() {
            if (!soundOn) return;
            const o = audioCtx.createOscillator();
            const g = audioCtx.createGain();
            o.connect(g);
            g.connect(audioCtx.destination);
            o.frequency.value = 900;
            o.type = 'sine';
            g.gain.setValueAtTime(0.15 * soundVol, audioCtx.currentTime);
            g.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.08);
            o.start();
            o.stop(audioCtx.currentTime + 0.08);
        }

        function playHitSound() {
            if (!soundOn) return;
            const o = audioCtx.createOscillator();
            const g = audioCtx.createGain();
            o.connect(g);
            g.connect(audioCtx.destination);
            o.frequency.value = 150;
            o.type = 'sawtooth';
            g.gain.setValueAtTime(0.25 * soundVol, audioCtx.currentTime);
            g.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.4);
            o.start();
            o.stop(audioCtx.currentTime + 0.4);
        }

        function playScoreSound() {
            if (!soundOn) return;
            [800, 1000].forEach((freq, i) => {
                const o = audioCtx.createOscillator();
                const g = audioCtx.createGain();
                o.connect(g);
                g.connect(audioCtx.destination);
                o.frequency.value = freq;
                o.type = 'sine';
                const startTime = audioCtx.currentTime + (i * 0.08);
                g.gain.setValueAtTime(0.12 * soundVol, startTime);
                g.gain.exponentialRampToValueAtTime(0.01, startTime + 0.15);
                o.start(startTime);
                o.stop(startTime + 0.15);
            });
        }

        function playBrightWaySound() {
            if (!soundOn) return;
            [500, 650, 800, 1000].forEach((freq, i) => {
                const o = audioCtx.createOscillator();
                const g = audioCtx.createGain();
                o.connect(g);
                g.connect(audioCtx.destination);
                o.frequency.value = freq;
                o.type = 'sine';
                const startTime = audioCtx.currentTime + (i * 0.1);
                g.gain.setValueAtTime(0.18 * soundVol, startTime);
                g.gain.exponentialRampToValueAtTime(0.01, startTime + 0.35);
                o.start(startTime);
                o.stop(startTime + 0.35);
            });
        }

        function playShieldSound() {
            if (!soundOn) return;
            [400, 600, 800].forEach((freq, i) => {
                const o = audioCtx.createOscillator();
                const g = audioCtx.createGain();
                o.connect(g);
                g.connect(audioCtx.destination);
                o.frequency.value = freq;
                o.type = 'sine';
                const startTime = audioCtx.currentTime + (i * 0.08);
                g.gain.setValueAtTime(0.2 * soundVol, startTime);
                g.gain.exponentialRampToValueAtTime(0.01, startTime + 0.3);
                o.start(startTime);
                o.stop(startTime + 0.3);
            });
        }

        function updateMusicVol() {
            if (bgMusic && bgMusic.g) {
                bgMusic.g.gain.value = Math.min(musicVol * 1.5, 0.7);
            }
        }

        function stopMusic() {
            if (bgMusic) {
                if (bgMusic.g) bgMusic.g.disconnect();
                if (bgMusic.stop) bgMusic.stop();
                bgMusic = null;
            }
        }

        function startMusic() {
            if (!musicOn) return;
            stopMusic();
            bgMusic = { g: audioCtx.createGain(), stop: null };
            bgMusic.g.connect(audioCtx.destination);
            bgMusic.g.gain.value = Math.min(musicVol * 1.5, 0.7);
            const notes = musicLibrary[musicType];
            let shouldStop = false;
            bgMusic.stop = () => { shouldStop = true; };
            async function playMelody() {
                if (shouldStop || !musicOn) return;
                for (let note of notes) {
                    if (shouldStop || !musicOn) break;
                    await new Promise(resolve => {
                        setTimeout(() => {
                            if (shouldStop || !musicOn || !bgMusic) {
                                resolve();
                                return;
                            }
                            const o = audioCtx.createOscillator();
                            const g = audioCtx.createGain();
                            o.connect(g);
                            g.connect(bgMusic.g);
                            o.frequency.value = note.f;
                            o.type = 'triangle';
                            const now = audioCtx.currentTime;
                            g.gain.setValueAtTime(0, now);
                            g.gain.linearRampToValueAtTime(0.4, now + 0.05);
                            g.gain.linearRampToValueAtTime(0, now + note.d - 0.05);
                            o.start(now);
                            o.stop(now + note.d);
                            setTimeout(resolve, note.d * 1000);
                        }, 0);
                    });
                }
                await new Promise(r => setTimeout(r, 400));
                if (musicOn && bgMusic && !shouldStop) playMelody();
            }
            playMelody();
        }

        let scene, camera, renderer, car, obstacles = [], brightwayPosts = [], particles = [], shieldMesh = null;
        let gameState = {
            running: false, paused: false, score: 0, highScore: 0, speed: 0, maxSpeed: 70, 
            acceleration: 0.5, carPosition: 0, carColor: null, mapType: null,
            brightwayActive: false, shieldActive: false, shieldTimeLeft: 0,
            frameCount: 0, isMobile: window.innerWidth <= 768, obstacleFrequency: 120
        };
        const keys = {left: false, right: false, up: false, down: false, space: false, s: false};
        const carColorMap = {blue: 0x3B82F6, red: 0xEF4444, yellow: 0xFBBF24, green: 0x059669};

        document.addEventListener('DOMContentLoaded', function() {
            document.addEventListener('click', function(e) {
                if (e.target.closest('button, .feature-card, .option-card, .music-option, a')) {
                    playClick();
                }
            });

            document.getElementById('volumeBtn').onclick = (e) => {
                e.stopPropagation();
                panelOpen = !panelOpen;
                const panel = document.getElementById('volumePanel');
                if (panelOpen) {
                    panel.classList.add('show');
                } else {
                    panel.classList.remove('show');
                }
            };

            document.onclick = (e) => {
                const panel = document.getElementById('volumePanel');
                const btn = document.getElementById('volumeBtn');
                if (panelOpen && !panel.contains(e.target) && e.target !== btn) {
                    panelOpen = false;
                    panel.classList.remove('show');
                }
            };

            document.getElementById('musicVolume').oninput = (e) => {
                musicVol = e.target.value / 100;
                document.getElementById('musicVolumeValue').textContent = e.target.value + '%';
                updateMusicVol();
            };

            document.getElementById('soundVolume').oninput = (e) => {
                soundVol = e.target.value / 100;
                document.getElementById('soundVolumeValue').textContent = e.target.value + '%';
            };

            document.getElementById('musicMuteBtn').onclick = function() {
                musicOn = !musicOn;
                this.classList.toggle('muted');
                this.innerHTML = musicOn ? '🎵' : '🔇';
                musicOn ? startMusic() : stopMusic();
            };

            document.getElementById('soundMuteBtn').onclick = function() {
                soundOn = !soundOn;
                this.classList.toggle('muted');
                this.innerHTML = soundOn ? '🔊' : '🔇';
            };

            function selectMusic(type) {
                musicType = type;
                document.querySelectorAll('.music-option').forEach(opt => opt.classList.remove('active'));
                if (musicOn) startMusic();
            }

            document.getElementById('marioMusic').onclick = () => {selectMusic('mario');document.getElementById('marioMusic').classList.add('active');};
            document.getElementById('megaloMusic').onclick = () => {selectMusic('megalo');document.getElementById('megaloMusic').classList.add('active');};
            document.getElementById('starWarsMusic').onclick = () => {selectMusic('starWars');document.getElementById('starWarsMusic').classList.add('active');};
            document.getElementById('tetrisMusic').onclick = () => {selectMusic('tetris');document.getElementById('tetrisMusic').classList.add('active');};
            document.getElementById('piratesMusic').onclick = () => {selectMusic('pirates');document.getElementById('piratesMusic').classList.add('active');};
            document.getElementById('pokemonMusic').onclick = () => {selectMusic('pokemon');document.getElementById('pokemonMusic').classList.add('active');};

            document.getElementById('playGameBtn').addEventListener('click', function() {
                document.getElementById('gameModal').classList.add('active');
                document.getElementById('mapSelectorScreen').classList.remove('hidden');
            });
            
            document.getElementById('instructionsBtn').addEventListener('click', function() {
                document.getElementById('instructionsModal').classList.add('active');
            });

            document.querySelectorAll('#mapSelectorScreen .option-card').forEach(card => {
                card.addEventListener('click', function() {
                    document.querySelectorAll('#mapSelectorScreen .option-card').forEach(c => c.classList.remove('selected'));
                    this.classList.add('selected');
                    gameState.mapType = this.dataset.map;
                    setTimeout(() => {
                        document.getElementById('mapSelectorScreen').classList.add('hidden');
                        document.getElementById('carSelectorScreen').classList.remove('hidden');
                    }, 300);
                });
            });

            document.querySelectorAll('#carSelectorScreen .option-card').forEach(card => {
                card.addEventListener('click', function() {
                    document.querySelectorAll('#carSelectorScreen .option-card').forEach(c => c.classList.remove('selected'));
                    this.classList.add('selected');
                    gameState.carColor = this.dataset.color;
                    setTimeout(() => {
                        document.getElementById('carSelectorScreen').classList.add('hidden');
                        initGame();
                    }, 300);
                });
            });

            setTimeout(() => {
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume().then(() => startMusic());
                } else {
                    startMusic();
                }
            }, 500);
        });

        function initGame() {
            scene = new THREE.Scene();
            
            if (gameState.mapType === 'city') {
                scene.fog = new THREE.Fog(0x0a0a1a, 100, 300);
                scene.background = new THREE.Color(0x050510);
            } else if (gameState.mapType === 'snow') {
                scene.fog = new THREE.Fog(0xE0F2FE, 150, 350);
                scene.background = new THREE.Color(0xBAE6FD);
            } else if (gameState.mapType === 'volcano') {
                scene.fog = new THREE.Fog(0x450a0a, 80, 250);
                scene.background = new THREE.Color(0x1a0505);
            }
            
            camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.set(0, 6, 14);
            camera.lookAt(0, 1, -10);
            renderer = new THREE.WebGLRenderer({canvas: document.getElementById('gameCanvas'), antialias: true, powerPreference: "high-performance"});
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            renderer.shadowMap.enabled = true;
            renderer.shadowMap.type = THREE.PCFSoftShadowMap;
            
            if (gameState.mapType === 'city') {
                const ambientLight = new THREE.AmbientLight(0x4a4a60, 0.4);
                scene.add(ambientLight);
                const directionalLight = new THREE.DirectionalLight(0x9090ff, 0.5);
                directionalLight.position.set(20, 40, 20);
                directionalLight.castShadow = true;
                configureShadow(directionalLight);
                scene.add(directionalLight);
                const hemisphereLight = new THREE.HemisphereLight(0x1a1a2a, 0x0a0a15, 0.4);
                scene.add(hemisphereLight);
            } else if (gameState.mapType === 'snow') {
                const ambientLight = new THREE.AmbientLight(0xFFFFFF, 0.7);
                scene.add(ambientLight);
                const directionalLight = new THREE.DirectionalLight(0xCCE5FF, 0.8);
                directionalLight.position.set(15, 50, 25);
                directionalLight.castShadow = true;
                configureShadow(directionalLight);
                scene.add(directionalLight);
                const hemisphereLight = new THREE.HemisphereLight(0xE0F2FE, 0xBAE6FD, 0.5);
                scene.add(hemisphereLight);
            } else if (gameState.mapType === 'volcano') {
                const ambientLight = new THREE.AmbientLight(0xFF4400, 0.3);
                scene.add(ambientLight);
                const directionalLight = new THREE.DirectionalLight(0xFF6600, 0.6);
                directionalLight.position.set(20, 40, 20);
                directionalLight.castShadow = true;
                configureShadow(directionalLight);
                scene.add(directionalLight);
                const hemisphereLight = new THREE.HemisphereLight(0x7f1d1d, 0x450a0a, 0.4);
                scene.add(hemisphereLight);
            }
            
            createEnvironment();
            createRoad();
            createCar();
            createBrightwayPosts();
            createParticles();
            setupControls();
            gameState.running = true;
            gameState.speed = 40;
            gameState.highScore = parseInt(localStorage.getItem('brightwayHighScore3D') || '0');
            document.getElementById('highScore').textContent = gameState.highScore;
            animate();
        }

        function configureShadow(light) {
            light.shadow.camera.left = -60;
            light.shadow.camera.right = 60;
            light.shadow.camera.top = 60;
            light.shadow.camera.bottom = -60;
            light.shadow.mapSize.width = 2048;
            light.shadow.mapSize.height = 2048;
            light.shadow.bias = -0.0001;
        }

        function createEnvironment() {
            let groundColor, treeColor, skyElements;
            
            if (gameState.mapType === 'city') {
                groundColor = 0x0a1a0a;
                treeColor = 0x0a1a0a;
                skyElements = 'stars';
            } else if (gameState.mapType === 'snow') {
                groundColor = 0xFFFFFF;
                treeColor = 0x1a4d2e;
                skyElements = 'snow';
            } else if (gameState.mapType === 'volcano') {
                groundColor = 0x1a0a0a;
                treeColor = 0x2a1a1a;
                skyElements = 'lava';
            }
            
            const groundGeo = new THREE.PlaneGeometry(400, 600);
            const groundMat = new THREE.MeshStandardMaterial({ 
                color: groundColor, 
                roughness: 0.95,
                metalness: 0
            });
            const ground = new THREE.Mesh(groundGeo, groundMat);
            ground.rotation.x = -Math.PI / 2;
            ground.position.z = -200;
            ground.receiveShadow = true;
            scene.add(ground);
            
            for (let i = 0; i < 50; i++) {
                const treeGroup = new THREE.Group();
                const trunkHeight = 4 + Math.random() * 3;
                const trunk = new THREE.Mesh(
                    new THREE.CylinderGeometry(0.4, 0.6, trunkHeight, 8), 
                    new THREE.MeshStandardMaterial({ 
                        color: 0x1a1008, 
                        roughness: 0.9,
                        metalness: 0
                    })
                );
                trunk.position.y = trunkHeight / 2;
                trunk.castShadow = true;
                trunk.receiveShadow = true;
                treeGroup.add(trunk);
                
                const leavesSize = 2 + Math.random() * 1.5;
                const leavesColor = gameState.mapType === 'snow' ? 0x1a4d2e : treeColor;
                const leaves = new THREE.Mesh(
                    new THREE.SphereGeometry(leavesSize, 10, 10), 
                    new THREE.MeshStandardMaterial({ 
                        color: leavesColor, 
                        roughness: 0.85,
                        metalness: 0
                    })
                );
                leaves.position.y = trunkHeight + leavesSize * 0.5;
                leaves.castShadow = true;
                leaves.receiveShadow = true;
                treeGroup.add(leaves);
                
                if (gameState.mapType === 'snow') {
                    const snow = new THREE.Mesh(
                        new THREE.SphereGeometry(leavesSize * 1.1, 8, 8),
                        new THREE.MeshStandardMaterial({
                            color: 0xFFFFFF,
                            roughness: 0.7,
                            metalness: 0,
                            transparent: true,
                            opacity: 0.7
                        })
                    );
                    snow.position.y = trunkHeight + leavesSize * 0.5;
                    treeGroup.add(snow);
                }
                
                const side = Math.random() > 0.5 ? 1 : -1;
                treeGroup.position.set(
                    side * (15 + Math.random() * 30), 
                    0, 
                    -Math.random() * 500
                );
                scene.add(treeGroup);
            }
            
            if (skyElements === 'stars') {
                const starMaterial = new THREE.MeshBasicMaterial({ 
                    color: 0xFFFFFF,
                    transparent: true,
                    opacity: 0.9
                });
                for (let i = 0; i < 200; i++) {
                    const starSize = 0.15 + Math.random() * 0.25;
                    const star = new THREE.Mesh(
                        new THREE.SphereGeometry(starSize, 6, 6), 
                        starMaterial
                    );
                    star.position.set(
                        (Math.random() - 0.5) * 400, 
                        35 + Math.random() * 70, 
                        -Math.random() * 600
                    );
                    scene.add(star);
                }
                
                const moonGeometry = new THREE.SphereGeometry(8, 32, 32);
                const moonMaterial = new THREE.MeshBasicMaterial({ 
                    color: 0xFFFAF0,
                    transparent: true,
                    opacity: 0.95
                });
                const moon = new THREE.Mesh(moonGeometry, moonMaterial);
                moon.position.set(80, 60, -250);
                scene.add(moon);
                
                const moonGlow = new THREE.Mesh(
                    new THREE.SphereGeometry(10, 32, 32),
                    new THREE.MeshBasicMaterial({
                        color: 0xFFFFDD,
                        transparent: true,
                        opacity: 0.15
                    })
                );
                moonGlow.position.copy(moon.position);
                scene.add(moonGlow);
            }
        }

        function createParticles() {
            if (gameState.mapType === 'snow') {
                for (let i = 0; i < 500; i++) {
                    const snowflake = new THREE.Mesh(
                        new THREE.SphereGeometry(0.1, 6, 6),
                        new THREE.MeshBasicMaterial({ color: 0xFFFFFF })
                    );
                    snowflake.position.set(
                        (Math.random() - 0.5) * 100,
                        Math.random() * 80,
                        -Math.random() * 400
                    );
                    snowflake.userData.velocity = 0.05 + Math.random() * 0.1;
                    scene.add(snowflake);
                    particles.push(snowflake);
                }
            } else if (gameState.mapType === 'volcano') {
                for (let i = 0; i < 30; i++) {
                    const lavaParticle = new THREE.Mesh(
                        new THREE.SphereGeometry(0.5 + Math.random() * 0.8, 8, 8),
                        new THREE.MeshBasicMaterial({ 
                            color: Math.random() > 0.5 ? 0xFF4500 : 0xFF6347,
                            transparent: true,
                            opacity: 0.8
                        })
                    );
                    lavaParticle.position.set(
                        (Math.random() - 0.5) * 80,
                        5 + Math.random() * 10,
                        -Math.random() * 300 - 100
                    );
                    lavaParticle.userData.velocity = {
                        x: (Math.random() - 0.5) * 0.2,
                        y: 0.3 + Math.random() * 0.4,
                        z: -0.1
                    };
                    lavaParticle.userData.life = 0;
                    scene.add(lavaParticle);
                    particles.push(lavaParticle);
                }
            }
        }

        function createRoad() {
            const roadColor = gameState.mapType === 'snow' ? 0x2a2a2a : 0x1a1a1a;
            const road = new THREE.Mesh(
                new THREE.PlaneGeometry(14, 500), 
                new THREE.MeshStandardMaterial({ 
                    color: roadColor, 
                    roughness: 0.95,
                    metalness: 0.1
                })
            );
            road.rotation.x = -Math.PI / 2;
            road.position.z = -200;
            road.position.y = 0.05;
            road.receiveShadow = true;
            scene.add(road);
            
            for (let i = 0; i < 50; i++) {
                const line = new THREE.Mesh(
                    new THREE.BoxGeometry(0.5, 0.25, 6), 
                    new THREE.MeshBasicMaterial({ 
                        color: 0xFFFF00,
                        transparent: true,
                        opacity: 0.9
                    })
                );
                line.position.set(0, 0.2, -i * 10);
                scene.add(line);
            }
            
            const shoulderL = new THREE.Mesh(
                new THREE.PlaneGeometry(6, 500), 
                new THREE.MeshStandardMaterial({ 
                    color: 0x3a3a3a,
                    roughness: 0.9,
                    metalness: 0.05
                })
            );
            shoulderL.rotation.x = -Math.PI / 2;
            shoulderL.position.set(-10, 0.02, -200);
            shoulderL.receiveShadow = true;
            scene.add(shoulderL);
            
            const shoulderR = new THREE.Mesh(
                new THREE.PlaneGeometry(6, 500), 
                new THREE.MeshStandardMaterial({ 
                    color: 0x3a3a3a,
                    roughness: 0.9,
                    metalness: 0.05
                })
            );
            shoulderR.rotation.x = -Math.PI / 2;
            shoulderR.position.set(10, 0.02, -200);
            shoulderR.receiveShadow = true;
            scene.add(shoulderR);
        }

        function createCar() {
            const carGroup = new THREE.Group();
            const bodyMat = new THREE.MeshStandardMaterial({ color: carColorMap[gameState.carColor], metalness: 0.8, roughness: 0.2 });
            const body = new THREE.Mesh(new THREE.BoxGeometry(2, 1, 4), bodyMat);
            body.position.y = 0.7;
            body.castShadow = true;
            carGroup.add(body);
            carGroup.userData.bodyMaterial = bodyMat;
            const cabinMat = new THREE.MeshStandardMaterial({ color: 0x111111, metalness: 0.95, roughness: 0.05, transparent: true, opacity: 0.9 });
            const cabin = new THREE.Mesh(new THREE.BoxGeometry(1.7, 0.9, 2), cabinMat);
            cabin.position.set(0, 1.5, -0.3);
            cabin.castShadow = true;
            carGroup.add(cabin);
            const windowMat = new THREE.MeshStandardMaterial({ color: 0x000000, metalness: 0.95, roughness: 0.05, transparent: true, opacity: 0.8 });
            const frontWindow = new THREE.Mesh(new THREE.BoxGeometry(1.5, 0.7, 0.9), windowMat);
            frontWindow.position.set(0, 1.5, -1.3);
            carGroup.add(frontWindow);
            const wheelMat = new THREE.MeshStandardMaterial({ color: 0x1a1a1a, metalness: 0.3, roughness: 0.8 });
            const wheelPositions = [
                {pos: [-1.1, 0.4, 1.4], rot: Math.PI / 2},
                {pos: [1.1, 0.4, 1.4], rot: Math.PI / 2},
                {pos: [-1.1, 0.4, -1.4], rot: Math.PI / 2},
                {pos: [1.1, 0.4, -1.4], rot: Math.PI / 2}
            ];
            carGroup.userData.wheels = [];
            wheelPositions.forEach(wheel => {
                const wheelMesh = new THREE.Mesh(new THREE.CylinderGeometry(0.4, 0.4, 0.4, 16), wheelMat);
                wheelMesh.rotation.z = wheel.rot;
                wheelMesh.rotation.y = 0;
                wheelMesh.position.set(...wheel.pos);
                wheelMesh.castShadow = true;
                carGroup.add(wheelMesh);
                carGroup.userData.wheels.push(wheelMesh);
            });
            
            const headlightMat = new THREE.MeshStandardMaterial({ color: 0xFF8C00, emissive: 0xFF8C00, emissiveIntensity: 1 });
            [-0.7, 0.7].forEach(x => {
                const headlight = new THREE.Mesh(new THREE.BoxGeometry(0.3, 0.25, 0.15), headlightMat);
                headlight.position.set(x, 0.7, 2.05);
                carGroup.add(headlight);
                const light = new THREE.SpotLight(0xFFFFDD, 2.0, 60, Math.PI / 8, 0.5, 1);
                light.position.set(x, 0.7, 2.1);
                light.target.position.set(x, 0, -40);
                light.castShadow = true;
                light.shadow.mapSize.width = 1024;
                light.shadow.mapSize.height = 1024;
                light.shadow.camera.near = 0.5;
                light.shadow.camera.far = 60;
                carGroup.add(light);
                carGroup.add(light.target);
            });
            
            const rearLightMat = new THREE.MeshStandardMaterial({ color: 0xFF0000, emissive: 0xFF0000, emissiveIntensity: 0.8 });
            [-0.7, 0.7].forEach(x => {
                const rearLight = new THREE.Mesh(new THREE.BoxGeometry(0.3, 0.25, 0.15), rearLightMat);
                rearLight.position.set(x, 0.7, -2.05);
                rearLight.castShadow = false;
                carGroup.add(rearLight);
            });
            
            const shieldGeometry = new THREE.SphereGeometry(2.5, 32, 32);
            const shieldMaterial = new THREE.MeshBasicMaterial({
                color: 0x3B82F6,
                transparent: true,
                opacity: 0,
                side: THREE.DoubleSide
            });
            shieldMesh = new THREE.Mesh(shieldGeometry, shieldMaterial);
            shieldMesh.visible = false;
            carGroup.add(shieldMesh);
            
            carGroup.position.set(0, 0, 0);
            scene.add(carGroup);
            car = carGroup;
        }

        function createBrightwayPosts() {
            for (let i = 0; i < 15; i++) {
                const postGroup = new THREE.Group();
                const body = new THREE.Mesh(new THREE.BoxGeometry(0.8, 3, 0.8), new THREE.MeshStandardMaterial({ color: 0xFF6B35, metalness: 0.5, roughness: 0.4 }));
                body.position.y = 1.5;
                body.castShadow = true;
                postGroup.add(body);
                const panel = new THREE.Mesh(new THREE.BoxGeometry(1, 0.6, 0.1), new THREE.MeshStandardMaterial({ color: 0x1E3A8A, metalness: 0.6, roughness: 0.3 }));
                panel.position.set(0, 3.3, 0);
                panel.castShadow = true;
                postGroup.add(panel);
                const ledMat = new THREE.MeshStandardMaterial({ color: 0xFFC107, emissive: 0xFFC107, emissiveIntensity: 0.3 });
                postGroup.userData.leds = [];
                for (let j = 0; j < 3; j++) {
                    const led = new THREE.Mesh(new THREE.SphereGeometry(0.15, 8, 8), ledMat.clone());
                    led.position.set((j - 1) * 0.3, 2, 0.45);
                    postGroup.add(led);
                    postGroup.userData.leds.push(led);
                }
                const side = i % 2 === 0 ? -1 : 1;
                postGroup.position.set(side * 12, 0, -i * 30 - 20);
                scene.add(postGroup);
                brightwayPosts.push(postGroup);
            }
        }

        function createObstacle() {
            const colors = [0xEF4444, 0x10B981, 0xFBBF24, 0x8B5CF6];
            const color = colors[Math.floor(Math.random() * colors.length)];
            const carGroup = new THREE.Group();
            const body = new THREE.Mesh(new THREE.BoxGeometry(2, 1, 4), new THREE.MeshStandardMaterial({ color, metalness: 0.7, roughness: 0.3 }));
            body.position.y = 0.7;
            body.castShadow = true;
            carGroup.add(body);
            const cabin = new THREE.Mesh(new THREE.BoxGeometry(1.8, 0.8, 2), new THREE.MeshStandardMaterial({ color: 0x111111, metalness: 0.9, roughness: 0.1, transparent: true, opacity: 0.9 }));
            cabin.position.set(0, 1.4, 0.4);
            cabin.castShadow = true;
            carGroup.add(cabin);
            const wheelMat = new THREE.MeshStandardMaterial({ color: 0x1a1a1a });
            const wheelPositions = [[-1, 0.4, 1.5], [1, 0.4, 1.5], [-1, 0.4, -1.5], [1, 0.4, -1.5]];
            carGroup.userData.wheels = [];
            wheelPositions.forEach(pos => {
                const wheel = new THREE.Mesh(new THREE.CylinderGeometry(0.4, 0.4, 0.4, 12), wheelMat);
                wheel.rotation.z = Math.PI / 2;
                wheel.position.set(...pos);
                wheel.castShadow = true;
                carGroup.add(wheel);
                carGroup.userData.wheels.push(wheel);
            });
            
            const rearLightMat = new THREE.MeshStandardMaterial({ color: 0xFF0000, emissive: 0xFF0000, emissiveIntensity: 0.6 });
            [-0.7, 0.7].forEach(x => {
                const rearLight = new THREE.Mesh(new THREE.BoxGeometry(0.3, 0.25, 0.15), rearLightMat);
                rearLight.position.set(x, 0.7, 1.9);
                rearLight.castShadow = false;
                carGroup.add(rearLight);
            });
            const lanes = [-4.5, 0, 4.5];
            const lane = lanes[Math.floor(Math.random() * lanes.length)];
            carGroup.position.set(lane, 0.7, -200);
            carGroup.userData = { type: 'car', lane };
            scene.add(carGroup);
            obstacles.push(carGroup);
        }

        function setupControls() {
            document.addEventListener('keydown', (e) => {
                if (e.key === 'ArrowLeft') keys.left = true;
                if (e.key === 'ArrowRight') keys.right = true;
                if (e.key === 'ArrowUp') keys.up = true;
                if (e.key === 'ArrowDown') keys.down = true;
                if (e.key === ' ') { e.preventDefault(); keys.space = true; activateBrightWay(); }
                if (e.key === 's' || e.key === 'S') { e.preventDefault(); keys.s = true; activateShield(); }
            });
            document.addEventListener('keyup', (e) => {
                if (e.key === 'ArrowLeft') keys.left = false;
                if (e.key === 'ArrowRight') keys.right = false;
                if (e.key === 'ArrowUp') keys.up = false;
                if (e.key === 'ArrowDown') keys.down = false;
                if (e.key === ' ') keys.space = false;
                if (e.key === 's' || e.key === 'S') keys.s = false;
            });
            const canvas = document.getElementById('gameCanvas');
            canvas.addEventListener('touchstart', (e) => {
                const touch = e.touches[0];
                const rect = canvas.getBoundingClientRect();
                const x = touch.clientX - rect.left;
                if (x < rect.width / 2) keys.left = true;
                else keys.right = true;
            });
            canvas.addEventListener('touchend', () => { keys.left = false; keys.right = false; });
            document.getElementById('brightwayBtn').addEventListener('click', () => activateBrightWay());
            document.getElementById('shieldBtn').addEventListener('click', () => activateShield());
            document.getElementById('pauseBtn').addEventListener('click', () => {
                gameState.paused = !gameState.paused;
                document.getElementById('pauseBtn').innerHTML = gameState.paused ? '▶ Reanudar' : '⏸ Pausar';
            });
            document.getElementById('menuBtn').addEventListener('click', () => returnToMenu());
            document.getElementById('restartBtn').addEventListener('click', () => restartGame());
        }

        function activateBrightWay() {
            if (gameState.brightwayActive || !gameState.running) return;
            playBrightWaySound();
            gameState.brightwayActive = true;
            gameState.score += 1000;
            document.getElementById('brightwayBtn').classList.add('active');
            
            if (gameState.mapType === 'city') {
                scene.fog.color.setHex(0xFFE4B5);
                scene.background.setHex(0x2a2a1a);
            } else if (gameState.mapType === 'snow') {
                scene.fog.color.setHex(0xFFFAF0);
                scene.background.setHex(0xE8F4F8);
            } else if (gameState.mapType === 'volcano') {
                scene.fog.color.setHex(0xFF8C00);
                scene.background.setHex(0x3a1a0a);
            }
            
            scene.children.forEach(child => {
                if (child instanceof THREE.DirectionalLight) {
                    child.intensity = 2.5;
                    child.color.setHex(0xFFFFCC);
                }
            });
            brightwayPosts.forEach(post => {
                post.userData.leds.forEach(led => { led.material.emissiveIntensity = 3; });
            });
            setTimeout(() => {
                gameState.brightwayActive = false;
                document.getElementById('brightwayBtn').classList.remove('active');
                
                if (gameState.mapType === 'city') {
                    scene.fog.color.setHex(0x0a0a1a);
                    scene.background.setHex(0x050510);
                    scene.children.forEach(child => {
                        if (child instanceof THREE.DirectionalLight) {
                            child.intensity = 0.5;
                            child.color.setHex(0x9090ff);
                        }
                    });
                } else if (gameState.mapType === 'snow') {
                    scene.fog.color.setHex(0xE0F2FE);
                    scene.background.setHex(0xBAE6FD);
                    scene.children.forEach(child => {
                        if (child instanceof THREE.DirectionalLight) {
                            child.intensity = 0.8;
                            child.color.setHex(0xCCE5FF);
                        }
                    });
                } else if (gameState.mapType === 'volcano') {
                    scene.fog.color.setHex(0x450a0a);
                    scene.background.setHex(0x1a0505);
                    scene.children.forEach(child => {
                        if (child instanceof THREE.DirectionalLight) {
                            child.intensity = 0.6;
                            child.color.setHex(0xFF6600);
                        }
                    });
                }
                
                brightwayPosts.forEach(post => {
                    post.userData.leds.forEach(led => { led.material.emissiveIntensity = 0.3; });
                });
            }, 5000);
        }

        function activateShield() {
            if (gameState.shieldActive || !gameState.running) return;
            playShieldSound();
            gameState.shieldActive = true;
            gameState.shieldTimeLeft = 10;
            document.getElementById('shieldBtn').classList.add('active');
            
            if (shieldMesh) {
                shieldMesh.visible = true;
                shieldMesh.material.opacity = 0.3;
            }
            
            const shieldInterval = setInterval(() => {
                if (!gameState.running || !gameState.shieldActive) {
                    clearInterval(shieldInterval);
                    return;
                }
                
                gameState.shieldTimeLeft--;
                
                if (gameState.shieldTimeLeft <= 3 && gameState.shieldTimeLeft > 0) {
                    document.getElementById('shieldBtn').classList.add('blink');
                    if (shieldMesh) {
                        shieldMesh.material.opacity = gameState.shieldTimeLeft % 2 === 0 ? 0.5 : 0.1;
                    }
                }
                
                if (gameState.shieldTimeLeft <= 0) {
                    gameState.shieldActive = false;
                    document.getElementById('shieldBtn').classList.remove('active', 'blink');
                    if (shieldMesh) {
                        shieldMesh.visible = false;
                        shieldMesh.material.opacity = 0;
                    }
                    clearInterval(shieldInterval);
                }
            }, 1000);
        }

        function updateGame() {
            if (!gameState.running || gameState.paused) return;
            gameState.frameCount++;
            if (keys.left && gameState.carPosition > -4.5) gameState.carPosition -= 0.25;
            if (keys.right && gameState.carPosition < 4.5) gameState.carPosition += 0.25;
            car.position.x += (gameState.carPosition - car.position.x) * 0.12;
            if (keys.up && gameState.speed < gameState.maxSpeed) gameState.speed += gameState.acceleration;
            else if (keys.down && gameState.speed > 20) gameState.speed -= gameState.acceleration * 2;
            else if (!keys.up && !keys.down && gameState.speed < gameState.maxSpeed) gameState.speed += gameState.acceleration * 0.2;
            gameState.speed = Math.min(Math.max(gameState.speed, 20), gameState.maxSpeed);
            
            const elapsedTime = gameState.frameCount / 60;
            gameState.obstacleFrequency = Math.max(25, 120 - (elapsedTime * 3));
            
            if (gameState.frameCount % Math.floor(gameState.obstacleFrequency) === 0) {
                createObstacle();
                if (elapsedTime > 20 && Math.random() > 0.4) {
                    createObstacle();
                }
                if (elapsedTime > 40 && Math.random() > 0.6) {
                    createObstacle();
                }
            }
            
            obstacles.forEach((obstacle, index) => {
                obstacle.position.z += gameState.speed * 0.05;
                if (obstacle.userData.wheels) {
                    obstacle.userData.wheels.forEach(wheel => {
                        wheel.rotation.x += gameState.speed * 0.015;
                    });
                }
                if (obstacle.position.z > 20) {
                    scene.remove(obstacle);
                    obstacles.splice(index, 1);
                    gameState.score += 200;
                    playScoreSound();
                }
                if (Math.abs(obstacle.position.z - car.position.z) < 3 && Math.abs(obstacle.position.x - car.position.x) < 2.2) {
                    if (gameState.shieldActive) {
                        scene.remove(obstacle);
                        obstacles.splice(index, 1);
                        gameState.score += 500;
                        playScoreSound();
                    } else {
                        endGame();
                    }
                }
            });
            
            particles.forEach((particle, index) => {
                if (gameState.mapType === 'snow') {
                    particle.position.y -= particle.userData.velocity;
                    particle.position.z += gameState.speed * 0.02;
                    if (particle.position.y < 0) {
                        particle.position.y = 80;
                        particle.position.x = (Math.random() - 0.5) * 100;
                        particle.position.z = -Math.random() * 400;
                    }
                } else if (gameState.mapType === 'volcano') {
                    particle.position.x += particle.userData.velocity.x;
                    particle.position.y += particle.userData.velocity.y;
                    particle.position.z += particle.userData.velocity.z + gameState.speed * 0.02;
                    particle.userData.velocity.y -= 0.015;
                    particle.userData.life++;
                    
                    if (particle.position.y < 0 || particle.userData.life > 200) {
                        particle.position.set(
                            (Math.random() - 0.5) * 80,
                            5 + Math.random() * 10,
                            -Math.random() * 300 - 100
                        );
                        particle.userData.velocity = {
                            x: (Math.random() - 0.5) * 0.2,
                            y: 0.3 + Math.random() * 0.4,
                            z: -0.1
                        };
                        particle.userData.life = 0;
                    }
                }
            });
            
            brightwayPosts.forEach(post => {
                post.position.z += gameState.speed * 0.05;
                if (post.position.z > 30) post.position.z -= 450;
            });
            scene.children.forEach(child => {
                if (child.geometry && child.geometry.type === 'BoxGeometry' && child.material.color && child.material.color.getHex() === 0xFFFF00) {
                    child.position.z += gameState.speed * 0.05;
                    if (child.position.z > 30) child.position.z -= 500;
                }
            });
            if (car.userData.wheels) {
                car.userData.wheels.forEach(wheel => {
                    wheel.rotation.x += gameState.speed * 0.01;
                });
            }
            
            if (shieldMesh && gameState.shieldActive) {
                shieldMesh.rotation.y += 0.02;
                if (gameState.shieldTimeLeft > 3) {
                    shieldMesh.material.opacity = 0.3 + Math.sin(Date.now() * 0.005) * 0.1;
                }
            }
            
            gameState.score += Math.floor(gameState.speed * 0.08);
            if (gameState.brightwayActive) gameState.score += Math.floor(gameState.speed * 0.12);
            document.getElementById('score').textContent = Math.floor(gameState.score);
            document.getElementById('speedValue').textContent = Math.floor(gameState.speed);
            camera.position.z = car.position.z + 14 + (gameState.speed * 0.025);
            camera.position.y = 6 + (gameState.speed * 0.012);
            camera.position.x += (car.position.x * 0.15 - camera.position.x) * 0.1;
            camera.lookAt(car.position.x * 0.3, 1, car.position.z - 15);
        }

        function animate() {
            if (!gameState.running && !gameState.paused) return;
            requestAnimationFrame(animate);
            if (!gameState.paused) updateGame();
            renderer.render(scene, camera);
        }

        function endGame() {
            gameState.running = false;
            playHitSound();
            const finalScore = Math.floor(gameState.score);
            document.getElementById('finalScore').textContent = finalScore;
            if (finalScore > gameState.highScore) {
                gameState.highScore = finalScore;
                document.getElementById('highScore').textContent = finalScore;
                localStorage.setItem('brightwayHighScore3D', finalScore);
            }
            document.getElementById('gameOverScreen').classList.add('show');
        }

        function restartGame() {
            document.getElementById('gameOverScreen').classList.remove('show');
            obstacles.forEach(obstacle => scene.remove(obstacle));
            obstacles = [];
            gameState.score = 0;
            gameState.speed = 40;
            gameState.carPosition = 0;
            gameState.frameCount = 0;
            gameState.brightwayActive = false;
            gameState.shieldActive = false;
            gameState.shieldTimeLeft = 0;
            gameState.obstacleFrequency = 120;
            document.getElementById('brightwayBtn').classList.remove('active');
            document.getElementById('shieldBtn').classList.remove('active', 'blink');
            if (shieldMesh) {
                shieldMesh.visible = false;
                shieldMesh.material.opacity = 0;
            }
            car.position.set(0, 0, 0);
            camera.position.set(0, 6, 14);
            
            if (gameState.mapType === 'city') {
                scene.fog.color.setHex(0x0a0a1a);
                scene.background.setHex(0x050510);
            } else if (gameState.mapType === 'snow') {
                scene.fog.color.setHex(0xE0F2FE);
                scene.background.setHex(0xBAE6FD);
            } else if (gameState.mapType === 'volcano') {
                scene.fog.color.setHex(0x450a0a);
                scene.background.setHex(0x1a0505);
            }
            
            brightwayPosts.forEach(post => {
                post.userData.leds.forEach(led => { led.material.emissiveIntensity = 0.3; });
            });
            gameState.running = true;
            gameState.paused = false;
            animate();
        }

        function returnToMenu() {
            gameState.running = false;
            obstacles.forEach(obstacle => scene.remove(obstacle));
            obstacles = [];
            brightwayPosts.forEach(post => scene.remove(post));
            brightwayPosts = [];
            particles.forEach(particle => scene.remove(particle));
            particles = [];
            if (renderer) {
                renderer.dispose();
                scene.traverse(object => {
                    if (object.geometry) object.geometry.dispose();
                    if (object.material) {
                        if (Array.isArray(object.material)) object.material.forEach(material => material.dispose());
                        else object.material.dispose();
                    }
                });
            }
            document.getElementById('gameModal').classList.remove('active');
            document.getElementById('gameOverScreen').classList.remove('show');
            document.getElementById('mapSelectorScreen').classList.remove('hidden');
            document.getElementById('carSelectorScreen').classList.add('hidden');
            document.querySelectorAll('.option-card').forEach(c => c.classList.remove('selected'));
            document.getElementById('brightwayBtn').classList.remove('active');
            document.getElementById('shieldBtn').classList.remove('active', 'blink');
            gameState.carColor = null;
            gameState.mapType = null;
            gameState.shieldActive = false;
            gameState.shieldTimeLeft = 0;
        }

        window.addEventListener('resize', () => {
            if (camera && renderer) {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
                renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
                gameState.isMobile = window.innerWidth <= 768;
            }
        });

        document.addEventListener('click', function initAudio() {
            if (audioCtx.state === 'suspended') {
                audioCtx.resume().then(() => { if (musicOn) startMusic(); });
            }
        }, { once: true });
    </script>
</body>
</html>
