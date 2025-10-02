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
            --blue: #3B82F6;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
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

        .audio-btn.active {
            background: rgba(255, 107, 53, 0.3);
            border-color: var(--primary);
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
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .volume-panel h4 {
            color: var(--primary);
            font-size: 0.9rem;
            margin-bottom: 1rem;
            text-align: center;
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

        .volume-slider::-moz-range-thumb:hover {
            transform: scale(1.2);
            box-shadow: 0 0 15px rgba(255, 107, 53, 0.6);
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

        .cta-section {
            text-align: center;
            margin: 3rem 0;
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
            grid-template-columns: repeat(auto-fit, minmax(min(280px, 90vw), 1fr));
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
            background: rgba(0, 0, 0, 0.95);
            z-index: 3000;
            display: none;
            backdrop-filter: blur(10px);
            overflow-y: auto;
            padding: 1rem;
        }

        .game-modal.active {
            display: block;
        }

        .game-container {
            max-width: 900px;
            margin: 0 auto;
            padding-top: 1rem;
        }

        .game-header {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 1rem;
            margin-bottom: 1.5rem;
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .game-stats {
            display: flex;
            justify-content: center;
            gap: 2rem;
            flex-wrap: wrap;
        }

        .stat {
            text-align: center;
        }

        .stat-label {
            color: var(--gray-400);
            font-size: 0.85rem;
            margin-bottom: 0.25rem;
        }

        .stat-value {
            font-size: 1.75rem;
            font-weight: 700;
            color: var(--accent);
        }

        .game-controls {
            display: flex;
            justify-content: center;
            gap: 0.75rem;
            flex-wrap: wrap;
        }

        .btn {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: var(--white);
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 50px;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(255, 107, 53, 0.4);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn-secondary {
            background: linear-gradient(135deg, #3B82F6, #1E40AF);
        }

        .btn-exit {
            background: linear-gradient(135deg, var(--danger), #DC2626);
        }

        .btn-menu {
            background: linear-gradient(135deg, var(--accent), #D97706);
        }

        .game-canvas {
            position: relative;
            width: 100%;
            max-width: 700px;
            height: clamp(400px, 60vh, 500px);
            margin: 0 auto 1.5rem;
            background: var(--darker);
            border-radius: 20px;
            overflow: hidden;
            border: 3px solid var(--gray-600);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            touch-action: none;
        }

        .touch-zone {
            position: absolute;
            top: 0;
            height: 100%;
            width: 50%;
            z-index: 20;
        }

        .touch-zone-left {
            left: 0;
        }

        .touch-zone-right {
            right: 0;
        }

        .road {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: min(350px, 70%);
            height: 100%;
            background: linear-gradient(0deg, #333 0%, #222 100%);
            border-left: 3px solid var(--white);
            border-right: 3px solid var(--white);
        }

        .road-markings {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 6px;
            height: 100%;
            background: repeating-linear-gradient(to bottom, var(--white) 0px, var(--white) 30px, transparent 30px, transparent 60px);
            animation: roadMove 2s linear infinite;
        }

        @keyframes roadMove {
            0% { transform: translateX(-50%) translateY(0); }
            100% { transform: translateX(-50%) translateY(60px); }
        }

        .car {
            position: absolute;
            bottom: 80px;
            left: 35%;
            width: clamp(35px, 8%, 50px);
            height: clamp(60px, 15%, 90px);
            background: linear-gradient(0deg, var(--blue), #1E40AF);
            border-radius: 20px 20px 10px 10px;
            transition: left 0.3s ease;
            z-index: 10;
            transform: translateX(-50%);
            box-shadow: 0 5px 20px rgba(59, 130, 246, 0.4);
        }

        .car.lane-right {
            left: 65%;
        }

        .car::before {
            content: '';
            position: absolute;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            width: 70%;
            height: 50%;
            background: rgba(59, 130, 246, 0.3);
            border-radius: 15px;
            border: 2px solid rgba(59, 130, 246, 0.6);
        }

        .car::after {
            content: '';
            position: absolute;
            top: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 50%;
            height: 20%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 8px 8px 0 0;
        }

        .car-lights {
            position: absolute;
            top: -8px;
            left: 50%;
            transform: translateX(-50%);
            width: 80%;
            height: 20px;
            background: radial-gradient(ellipse, rgba(255, 255, 255, 0.8) 0%, transparent 70%);
            border-radius: 50%;
            opacity: 0.4;
        }

        .obstacle {
            position: absolute;
            top: -60px;
            width: clamp(35px, 8%, 50px);
            height: clamp(60px, 13%, 80px);
            background: var(--gray-600);
            border-radius: 12px 12px 6px 6px;
            transform: translateX(-50%);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        }

        .obstacle.lane-left {
            left: 35%;
        }

        .obstacle.lane-right {
            left: 65%;
        }

        .obstacle::before {
            content: '';
            position: absolute;
            top: 20%;
            left: 50%;
            transform: translateX(-50%);
            width: 70%;
            height: 50%;
            background: rgba(64, 64, 64, 0.8);
            border-radius: 8px;
        }

        .obstacle.car-red {
            background: linear-gradient(180deg, #DC2626, #EF4444);
            border-radius: 6px 6px 12px 12px;
            box-shadow: 0 5px 20px rgba(239, 68, 68, 0.4);
        }

        .obstacle.car-red::before {
            background: rgba(239, 68, 68, 0.3);
            border: 2px solid rgba(239, 68, 68, 0.6);
            border-radius: 15px;
        }

        .obstacle.car-red::after {
            content: '';
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 50%;
            height: 20%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 0 0 8px 8px;
        }

        .obstacle.car-green {
            background: linear-gradient(180deg, #059669, #10B981);
            border-radius: 6px 6px 12px 12px;
            box-shadow: 0 5px 20px rgba(16, 185, 129, 0.4);
        }

        .obstacle.car-green::before {
            background: rgba(16, 185, 129, 0.3);
            border: 2px solid rgba(16, 185, 129, 0.6);
            border-radius: 15px;
        }

        .obstacle.car-green::after {
            content: '';
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 50%;
            height: 20%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 0 0 8px 8px;
        }

        .obstacle.car-yellow {
            background: linear-gradient(180deg, #D97706, #F59E0B);
            border-radius: 6px 6px 12px 12px;
            box-shadow: 0 5px 20px rgba(245, 158, 11, 0.4);
        }

        .obstacle.car-yellow::before {
            background: rgba(245, 158, 11, 0.3);
            border: 2px solid rgba(245, 158, 11, 0.6);
            border-radius: 15px;
        }

        .obstacle.car-yellow::after {
            content: '';
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 50%;
            height: 20%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 0 0 8px 8px;
        }

        .obstacle.car-purple {
            background: linear-gradient(180deg, #7C3AED, #8B5CF6);
            border-radius: 6px 6px 12px 12px;
            box-shadow: 0 5px 20px rgba(139, 92, 246, 0.4);
        }

        .obstacle.car-purple::before {
            background: rgba(139, 92, 246, 0.3);
            border: 2px solid rgba(139, 92, 246, 0.6);
            border-radius: 15px;
        }

        .obstacle.car-purple::after {
            content: '';
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 50%;
            height: 20%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 0 0 8px 8px;
        }

        .speed-indicator {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 107, 53, 0.2);
            border: 2px solid var(--primary);
            border-radius: 12px;
            padding: 0.5rem 1rem;
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--primary);
            z-index: 15;
        }

        .brightway-post {
            position: absolute;
            right: clamp(30px, 8%, 60px);
            top: 50%;
            transform: translateY(-50%);
            width: clamp(35px, 8%, 50px);
            height: clamp(70px, 15%, 100px);
            cursor: pointer;
            z-index: 25;
            transition: all 0.3s ease;
        }

        .brightway-post:hover {
            transform: translateY(-50%) scale(1.1);
        }

        .brightway-body {
            width: 80%;
            height: 80%;
            background: linear-gradient(180deg, var(--primary), var(--primary-light));
            border-radius: 8px;
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 5px 20px rgba(255, 107, 53, 0.4);
        }

        .brightway-panel {
            width: 70%;
            height: 20%;
            background: linear-gradient(135deg, #1E3A8A, #3B82F6);
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 6px;
            box-shadow: 0 3px 10px rgba(59, 130, 246, 0.5);
        }

        .light-effect {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: clamp(400px, 150%, 600px);
            height: clamp(400px, 150%, 600px);
            background: radial-gradient(circle, rgba(255, 193, 7, 0.3) 0%, transparent 60%);
            border-radius: 50%;
            opacity: 0;
            transition: all 0.5s ease;
            pointer-events: none;
        }

        .light-effect.active {
            opacity: 1;
            animation: lightPulse 2s ease-in-out infinite;
        }

        @keyframes lightPulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
        }

        .game-over {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 10, 10, 0.95);
            padding: 3rem;
            border-radius: 20px;
            border: 3px solid var(--primary);
            text-align: center;
            display: none;
            z-index: 100;
            backdrop-filter: blur(10px);
            max-width: 90%;
        }

        .game-over.show {
            display: block;
            animation: fadeInScale 0.4s ease;
        }

        @keyframes fadeInScale {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            100% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        }

        .game-over h3 {
            color: var(--primary);
            font-size: clamp(1.5rem, 5vw, 2rem);
            margin-bottom: 1.5rem;
        }

        .final-score {
            font-size: clamp(2rem, 8vw, 3rem);
            color: var(--accent);
            font-weight: 700;
            margin-bottom: 2rem;
        }

        .car-selector {
            margin: 1.5rem 0;
            text-align: center;
        }

        .car-selector h4 {
            color: var(--primary);
            font-size: 1rem;
            margin-bottom: 1rem;
        }

        .car-options {
            display: flex;
            justify-content: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .car-option {
            width: 60px;
            height: 40px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 3px solid transparent;
            position: relative;
        }

        .car-option:hover {
            transform: scale(1.1);
            border-color: rgba(255, 255, 255, 0.3);
        }

        .car-option.active {
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(255, 107, 53, 0.4);
            transform: scale(1.1);
        }

        .car-option.blue {
            background: linear-gradient(135deg, #3B82F6, #1E40AF);
            box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3);
        }

        .car-option.red {
            background: linear-gradient(135deg, #EF4444, #DC2626);
            box-shadow: 0 5px 15px rgba(239, 68, 68, 0.3);
        }

        .car-option.yellow {
            background: linear-gradient(135deg, #F59E0B, #D97706);
            box-shadow: 0 5px 15px rgba(245, 158, 11, 0.3);
        }

        .car-option::after {
            content: '';
            position: absolute;
            top: 20%;
            left: 50%;
            transform: translateX(-50%);
            width: 70%;
            height: 40%;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.5);
        }

        .instructions {
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 2rem;
            margin-top: 2rem;
            text-align: left;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .instructions h4 {
            color: var(--primary);
            font-size: clamp(1.1rem, 4vw, 1.3rem);
            margin-bottom: 1rem;
        }

        .instructions p {
            color: var(--gray-400);
            font-size: clamp(0.9rem, 3vw, 1rem);
            margin-bottom: 0.8rem;
            line-height: 1.6;
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
            font-size: clamp(1rem, 4vw, 1.25rem);
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .creators {
            margin: 1rem 0;
            font-size: clamp(0.8rem, 3vw, 0.9rem);
        }

        .creators strong {
            color: var(--primary);
        }

        .university {
            font-size: clamp(0.75rem, 2.5vw, 0.85rem);
            margin-bottom: 1rem;
        }

        .copyright {
            font-size: clamp(0.7rem, 2vw, 0.8rem);
            padding-top: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        @media (max-width: 768px) {
            .audio-controls {
                top: 80px;
            }
            
            .btn {
                padding: 0.65rem 1.25rem;
                font-size: 0.85rem;
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
        <div class="volume-control">
            <div class="volume-row">
                <button class="mute-btn" id="musicMuteBtn" title="Silenciar musica">🎵</button>
                <div class="volume-slider-container">
                    <div class="volume-label">
                        <span>Musica</span>
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
                    BrightWay vela por tu seguridad al implementar tecnologias modernas y buenas para el ambiente. 
                    Un innovador sistema de senalizacion vial que combina un trafitambo tradicional con tecnologia 
                    solar avanzada, proporcionando iluminacion autonoma y sostenible para mejorar la seguridad vial.
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

            <div class="cta-section">
                <button class="btn-play" id="playGameBtn">🎮 Jugar Minijuego</button>
                <button class="btn-play" id="instructionsBtn" style="background: rgba(255, 255, 255, 0.1); margin-top: 1rem;">📖 Instrucciones del Juego</button>
            </div>
        </div>

        <div class="features">
            <div class="container">
                <div class="features-grid">
                    <div class="feature-card">
                        <div class="feature-icon">☀</div>
                        <h3 class="feature-title">Energia Solar</h3>
                        <p class="feature-description">Panel solar movil con servomotores para optimizar la captacion de energia durante todo el dia.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">💡</div>
                        <h3 class="feature-title">Iluminacion LED</h3>
                        <p class="feature-description">Sistema de LEDs de alta eficiencia con sensor de movimiento para maxima visibilidad nocturna.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">🌱</div>
                        <h3 class="feature-title">Eco-Amigable</h3>
                        <p class="feature-description">Tecnologia 100% sustentable que no requiere conexion electrica externa.</p>
                    </div>
                    <div class="feature-card">
                        <div class="feature-icon">🔧</div>
                        <h3 class="feature-title">Arduino Nano</h3>
                        <p class="feature-description">Control inteligente mediante microcontrolador para gestion automatica del sistema.</p>
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
            <div class="creators">
                Desarrollado por: <strong>Pablo Nicolas Garcia Huerta</strong> y <strong>Angel Antonio Ruiz Garcia</strong>
            </div>
            <div class="university">Universidad Autonoma de Queretaro - Facultad de Ingenieria</div>
            <div class="copyright">
                &copy; 2024 BrightWay Technologies. Todos los derechos reservados.
            </div>
        </div>
    </footer>

    <div class="game-modal" id="gameModal">
        <div class="game-container">
            <div class="game-header">
                <div class="game-stats">
                    <div class="stat">
                        <div class="stat-label">Puntos</div>
                        <div class="stat-value" id="score">0</div>
                    </div>
                    <div class="stat">
                        <div class="stat-label">Record</div>
                        <div class="stat-value" id="highScore">0</div>
                    </div>
                    <div class="stat">
                        <div class="stat-label">Vidas</div>
                        <div class="stat-value" id="lives">3</div>
                    </div>
                </div>
                
                <div class="game-controls">
                    <button class="btn btn-secondary" id="pauseBtn" disabled>Pausar</button>
                    <button class="btn btn-exit" id="exitBtn" disabled>Reiniciar</button>
                    <button class="btn btn-menu" id="menuBtn">Menu</button>
                </div>
            </div>
            
            <div class="game-canvas" id="gameCanvas">
                <div class="touch-zone touch-zone-left" id="touchLeft"></div>
                <div class="touch-zone touch-zone-right" id="touchRight"></div>
                
                <div class="road">
                    <div class="road-markings"></div>
                </div>
                <div class="car" id="car">
                    <div class="car-lights" id="carLights"></div>
                </div>
                <div class="brightway-post" id="brightwayPost">
                    <div class="brightway-body"></div>
                    <div class="brightway-panel"></div>
                    <div class="light-effect" id="lightEffect"></div>
                </div>
                <div class="speed-indicator" id="speedIndicator">Velocidad: 1x</div>
                <div class="game-over" id="gameOver">
                    <h3>¡Juego Terminado!</h3>
                    <div class="final-score">Puntuacion: <span id="finalScore">0</span></div>
                    <button class="btn" onclick="resetGame()">Jugar de Nuevo</button>
                </div>
            </div>
            
            <div class="car-selector">
                <h4>Selecciona el color de tu auto:</h4>
                <div class="car-options">
                    <div class="car-option blue active" data-color="blue"></div>
                    <div class="car-option red" data-color="red"></div>
                    <div class="car-option yellow" data-color="yellow"></div>
                </div>
            </div>
        </div>
    </div>

    <div class="game-modal" id="instructionsModal">
        <div class="game-container">
            <h2 class="hero-title" style="font-size: 2.5rem; text-align: center; margin-bottom: 2rem;">Como Jugar</h2>
            
            <div class="instructions" style="max-width: 700px;">
                <h4>Objetivo:</h4>
                <p>Conduce tu auto esquivando obstaculos que caen desde arriba y activa el BrightWay para iluminar el camino y ver los autos de colores.</p>
                
                <h4 style="margin-top: 1.5rem;">Controles PC:</h4>
                <p>• Usa las flechas <strong>← →</strong> para cambiar de carril izquierdo o derecho</p>
                <p>• Presiona <strong>ESPACIO</strong> para activar el poste BrightWay y ver los obstaculos iluminados</p>
                <p>• El juego inicia automaticamente al presionar una flecha</p>
                
                <h4 style="margin-top: 1.5rem;">Controles Movil:</h4>
                <p>• Toca la <strong>mitad izquierda</strong> de la pantalla para ir al carril izquierdo</p>
                <p>• Toca la <strong>mitad derecha</strong> de la pantalla para ir al carril derecho</p>
                <p>• Toca el <strong>poste BrightWay</strong> (lado derecho) para activarlo</p>
                <p>• El juego inicia automaticamente al tocar para cambiar de carril</p>
                
                <h4 style="margin-top: 1.5rem;">Puntuacion:</h4>
                <p>• Ganas <strong>puntos por tiempo</strong> mientras juegas</p>
                <p>• Obten <strong>puntos extra</strong> por esquivar obstaculos exitosamente</p>
                <p>• Activa el BrightWay para <strong>bonus de puntos</strong> masivos</p>
                <p>• La velocidad aumenta progresivamente cada 10 segundos</p>
                
                <h4 style="margin-top: 1.5rem;">Caracteristicas Especiales:</h4>
                <p>• Cuando activas el BrightWay, todos los obstaculos se convierten en <strong>autos de colores</strong> por 4 segundos</p>
                <p>• Puedes elegir el <strong>color de tu auto</strong> en cualquier momento</p>
                <p>• Tienes <strong>3 vidas</strong> - ¡Usalas sabiamente!</p>
                <p>• Tu record se guarda automaticamente</p>
            </div>
            
            <div style="text-align: center; margin-top: 2rem;">
                <button class="btn-play" onclick="document.getElementById('instructionsModal').classList.remove('active')">Entendido</button>
            </div>
        </div>
    </div>

    <script>
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        let musicEnabled = true;
        let soundEnabled = true;
        let backgroundMusic = null;
        let musicVolume = 0.3;
        let soundVolume = 0.5;
        let volumePanelOpen = false;

        function playClickSound() {
            if (!soundEnabled) return;
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.connect(gain);
            gain.connect(audioContext.destination);
            osc.frequency.value = 800;
            osc.type = 'sine';
            gain.gain.setValueAtTime(0.3 * soundVolume, audioContext.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
            osc.start(audioContext.currentTime);
            osc.stop(audioContext.currentTime + 0.1);
        }

        function playHitSound() {
            if (!soundEnabled) return;
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.connect(gain);
            gain.connect(audioContext.destination);
            osc.frequency.value = 200;
            osc.type = 'sawtooth';
            gain.gain.setValueAtTime(0.4 * soundVolume, audioContext.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);
            osc.start(audioContext.currentTime);
            osc.stop(audioContext.currentTime + 0.3);
        }

        function playScoreSound() {
            if (!soundEnabled) return;
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.connect(gain);
            gain.connect(audioContext.destination);
            osc.frequency.value = 1200;
            osc.type = 'sine';
            gain.gain.setValueAtTime(0.2 * soundVolume, audioContext.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.15);
            osc.start(audioContext.currentTime);
            osc.stop(audioContext.currentTime + 0.15);
        }

        function playBrightWaySound() {
            if (!soundEnabled) return;
            [440, 550, 660].forEach((freq, i) => {
                const osc = audioContext.createOscillator();
                const gain = audioContext.createGain();
                osc.connect(gain);
                gain.connect(audioContext.destination);
                osc.frequency.value = freq;
                osc.type = 'sine';
                const startTime = audioContext.currentTime + (i * 0.1);
                gain.gain.setValueAtTime(0.2 * soundVolume, startTime);
                gain.gain.exponentialRampToValueAtTime(0.01, startTime + 0.3);
                osc.start(startTime);
                osc.stop(startTime + 0.3);
            });
        }

        function playSpeedUpSound() {
            if (!soundEnabled) return;
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.connect(gain);
            gain.connect(audioContext.destination);
            osc.type = 'sawtooth';
            osc.frequency.setValueAtTime(150, audioContext.currentTime);
            osc.frequency.exponentialRampToValueAtTime(400, audioContext.currentTime + 0.5);
            gain.gain.setValueAtTime(0.3 * soundVolume, audioContext.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
            osc.start(audioContext.currentTime);
            osc.stop(audioContext.currentTime + 0.5);
        }

        function updateMusicVolume() {
            if (backgroundMusic && backgroundMusic.gainNode) {
                const adjustedVolume = Math.pow(musicVolume, 1.5) * 0.5;
                backgroundMusic.gainNode.gain.value = adjustedVolume;
            }
        }

        function startBackgroundMusic() {
            if (!musicEnabled || backgroundMusic) return;
            
            backgroundMusic = {
                gainNode: audioContext.createGain()
            };
            
            backgroundMusic.gainNode.connect(audioContext.destination);
            const adjustedVolume = Math.pow(musicVolume, 1.5) * 0.5;
            backgroundMusic.gainNode.gain.value = adjustedVolume;
            
            const melody = [261.63, 293.66, 329.63, 349.23, 392.00];
            
            function playNote(frequency, duration) {
                const osc = audioContext.createOscillator();
                const noteGain = audioContext.createGain();
                osc.connect(noteGain);
                noteGain.connect(backgroundMusic.gainNode);
                osc.frequency.value = frequency;
                osc.type = 'sine';
                const now = audioContext.currentTime;
                noteGain.gain.setValueAtTime(0, now);
                noteGain.gain.linearRampToValueAtTime(0.8, now + 0.1);
                noteGain.gain.linearRampToValueAtTime(0, now + duration - 0.1);
                osc.start(now);
                osc.stop(now + duration);
            }
            
            function playMelody() {
                if (!musicEnabled) return;
                let time = 0;
                melody.forEach((freq) => {
                    setTimeout(() => {
                        if (musicEnabled && backgroundMusic) {
                            playNote(freq, 0.5);
                        }
                    }, time);
                    time += 600;
                });
                setTimeout(() => {
                    if (musicEnabled && backgroundMusic) {
                        playMelody();
                    }
                }, time + 1000);
            }
            
            playMelody();
        }

        function stopBackgroundMusic() {
            if (backgroundMusic) {
                backgroundMusic.gainNode.disconnect();
                backgroundMusic = null;
            }
        }

        function toggleVolumePanel() {
            volumePanelOpen = !volumePanelOpen;
            const panel = document.getElementById('volumePanel');
            const btn = document.getElementById('volumeBtn');
            
            if (volumePanelOpen) {
                panel.classList.add('show');
                btn.classList.add('active');
            } else {
                panel.classList.remove('show');
                btn.classList.remove('active');
            }
        }

        document.getElementById('volumeBtn').addEventListener('click', function(e) {
            e.stopPropagation();
            playClickSound();
            toggleVolumePanel();
        });

        document.addEventListener('click', function(e) {
            const panel = document.getElementById('volumePanel');
            const btn = document.getElementById('volumeBtn');
            
            if (volumePanelOpen && !panel.contains(e.target) && e.target !== btn) {
                volumePanelOpen = false;
                panel.classList.remove('show');
                btn.classList.remove('active');
            }
        });

        document.getElementById('musicVolume').addEventListener('input', function(e) {
            musicVolume = e.target.value / 100;
            document.getElementById('musicVolumeValue').textContent = e.target.value + '%';
            updateMusicVolume();
        });

        document.getElementById('soundVolume').addEventListener('input', function(e) {
            soundVolume = e.target.value / 100;
            document.getElementById('soundVolumeValue').textContent = e.target.value + '%';
            playClickSound();
        });

        document.getElementById('musicMuteBtn').addEventListener('click', function() {
            musicEnabled = !musicEnabled;
            this.classList.toggle('muted');
            this.innerHTML = musicEnabled ? '🎵' : '🔇';
            if (musicEnabled) {
                startBackgroundMusic();
            } else {
                stopBackgroundMusic();
            }
            playClickSound();
        });

        document.getElementById('soundMuteBtn').addEventListener('click', function() {
            soundEnabled = !soundEnabled;
            this.classList.toggle('muted');
            this.innerHTML = soundEnabled ? '🔊' : '🔇';
            if (soundEnabled) playClickSound();
        });

        document.addEventListener('click', function initMusic() {
            if (audioContext.state === 'suspended') {
                audioContext.resume().then(() => {
                    if (musicEnabled) startBackgroundMusic();
                });
            }
        }, { once: true });

        let gameState = {
            running: false,
            paused: false,
            score: 0,
            lives: 1,
            highScore: 0,
            carLane: 'left',
            carColor: 'blue',
            brightwayActive: false,
            obstacles: [],
            gameSpeed: 2,
            baseGameSpeed: 2,
            maxGameSpeed: 12,
            speedMultiplier: 1,
            obstacleSpawnRate: 120,
            baseObstacleSpawnRate: 120,
            minObstacleSpawnRate: 40,
            frameCounter: 0,
            isMobile: false
        };

        let gameElements = {};
        let gameLoop = null;
        const carColors = ['red', 'green', 'yellow', 'purple'];

        function isMobileDevice() {
            return window.innerWidth <= 768 || 'ontouchstart' in window;
        }

        document.addEventListener('DOMContentLoaded', function() {
            gameState.isMobile = isMobileDevice();
            initGame();
            
            setTimeout(() => {
                if (audioContext.state === 'suspended') {
                    audioContext.resume().then(() => {
                        startBackgroundMusic();
                    });
                } else {
                    startBackgroundMusic();
                }
            }, 500);
            
            document.getElementById('playGameBtn').addEventListener('click', function() {
                playClickSound();
                document.getElementById('gameModal').classList.add('active');
            });
            
            document.getElementById('instructionsBtn').addEventListener('click', function() {
                playClickSound();
                document.getElementById('instructionsModal').classList.add('active');
            });

            document.querySelectorAll('.feature-card').forEach(card => {
                card.addEventListener('click', playClickSound);
            });
        });

        function initGame() {
            gameElements = {
                car: document.getElementById('car'),
                carLights: document.getElementById('carLights'),
                brightwayPost: document.getElementById('brightwayPost'),
                lightEffect: document.getElementById('lightEffect'),
                gameCanvas: document.getElementById('gameCanvas'),
                gameOver: document.getElementById('gameOver'),
                score: document.getElementById('score'),
                lives: document.getElementById('lives'),
                highScore: document.getElementById('highScore'),
                finalScore: document.getElementById('finalScore'),
                pauseBtn: document.getElementById('pauseBtn'),
                exitBtn: document.getElementById('exitBtn'),
                menuBtn: document.getElementById('menuBtn'),
                speedIndicator: document.getElementById('speedIndicator'),
                touchLeft: document.getElementById('touchLeft'),
                touchRight: document.getElementById('touchRight')
            };

            const savedHighScore = parseInt(localStorage.getItem('brightwayHighScore') || '0');
            gameState.highScore = savedHighScore;
            gameElements.highScore.textContent = savedHighScore;

            setupEventListeners();
            setupCarColorSelector();
            updateSpeedIndicator();
            updateCarColor();
        }

        function setupCarColorSelector() {
            const carOptions = document.querySelectorAll('.car-option');
            carOptions.forEach(option => {
                option.addEventListener('click', (e) => {
                    e.preventDefault();
                    playClickSound();
                    carOptions.forEach(opt => opt.classList.remove('active'));
                    option.classList.add('active');
                    gameState.carColor = option.dataset.color;
                    updateCarColor();
                });
            });
        }

        function updateCarColor() {
            const car = gameElements.car;
            const colorMap = {
                blue: 'linear-gradient(0deg, var(--blue), #1E40AF)',
                red: 'linear-gradient(0deg, #EF4444, #DC2626)',
                yellow: 'linear-gradient(0deg, #F59E0B, #D97706)'
            };
            car.style.background = colorMap[gameState.carColor];
            const shadowMap = {
                blue: '0 5px 20px rgba(59, 130, 246, 0.4)',
                red: '0 5px 20px rgba(239, 68, 68, 0.4)',
                yellow: '0 5px 20px rgba(245, 158, 11, 0.4)'
            };
            car.style.boxShadow = shadowMap[gameState.carColor];
        }

        function setupEventListeners() {
            document.addEventListener('keydown', handleKeyDown);
            gameElements.pauseBtn.addEventListener('click', () => {
                playClickSound();
                togglePause();
            });
            gameElements.exitBtn.addEventListener('click', () => {
                playClickSound();
                resetGame();
            });
            gameElements.menuBtn.addEventListener('click', () => {
                playClickSound();
                returnToMenu();
            });
            setupTouchControls();
            gameElements.brightwayPost.addEventListener('click', () => {
                playBrightWaySound();
                activateBrightWay();
            });
        }

        function setupTouchControls() {
            gameElements.touchLeft.addEventListener('touchstart', (e) => {
                e.preventDefault();
                if (!gameState.running) {
                    startGame();
                }
                if (gameState.running && !gameState.paused) {
                    playClickSound();
                    changeLane('left');
                }
            });

            gameElements.touchRight.addEventListener('touchstart', (e) => {
                e.preventDefault();
                if (!gameState.running) {
                    startGame();
                }
                if (gameState.running && !gameState.paused) {
                    playClickSound();
                    changeLane('right');
                }
            });

            gameElements.brightwayPost.addEventListener('touchstart', (e) => {
                e.preventDefault();
                e.stopPropagation();
                if (gameState.running && !gameState.paused) {
                    playBrightWaySound();
                    activateBrightWay();
                }
            });

            gameElements.gameCanvas.addEventListener('touchmove', (e) => {
                e.preventDefault();
            });
        }

        function handleKeyDown(e) {
            if (!gameState.running) {
                if (e.key === 'ArrowLeft' || e.key === 'ArrowRight') {
                    e.preventDefault();
                    startGame();
                    return;
                }
            }
            if (!gameState.running || gameState.paused) return;
            switch(e.key) {
                case 'ArrowLeft':
                    e.preventDefault();
                    playClickSound();
                    changeLane('left');
                    break;
                case 'ArrowRight':
                    e.preventDefault();
                    playClickSound();
                    changeLane('right');
                    break;
                case ' ':
                    e.preventDefault();
                    playBrightWaySound();
                    activateBrightWay();
                    break;
            }
        }

        function startGame() {
            if (gameState.running) return;
            gameState = {
                ...gameState,
                running: true,
                paused: false,
                score: 0,
                lives: 1,
                carLane: 'left',
                brightwayActive: false,
                obstacles: [],
                gameSpeed: gameState.baseGameSpeed,
                speedMultiplier: 1,
                obstacleSpawnRate: gameState.baseObstacleSpawnRate,
                frameCounter: 0
            };
            updateUI();
            gameElements.pauseBtn.disabled = false;
            gameElements.exitBtn.disabled = false;
            gameElements.gameOver.classList.remove('show');
            clearObstacles();
            gameElements.car.className = 'car';
            gameElements.lightEffect.classList.remove('active');
            gameElements.carLights.style.opacity = '0.4';
            gameElements.gameCanvas.style.background = 'var(--darker)';
            updateSpeedIndicator();
            updateCarColor();
            gameLoop = setInterval(updateGame, 1000 / 60);
        }

        function updateGame() {
            if (!gameState.running || gameState.paused) return;
            gameState.frameCounter++;
            gameState.score += gameState.brightwayActive ? 3 : 1;
            gameElements.score.textContent = Math.floor(gameState.score / 60);
            if (gameState.frameCounter % 600 === 0) {
                increaseGameSpeed();
            }
            if (gameState.frameCounter % gameState.obstacleSpawnRate === 0) {
                spawnObstacle();
            }
            updateObstacles();
            checkCollisions();
        }

        function increaseGameSpeed() {
            gameState.speedMultiplier = Math.min(gameState.speedMultiplier + 0.3, 6);
            gameState.gameSpeed = gameState.baseGameSpeed * gameState.speedMultiplier;
            gameState.gameSpeed = Math.min(gameState.gameSpeed, gameState.maxGameSpeed);
            
            // Asegurar que obstacleSpawnRate siempre sea un número válido
            const calculatedRate = gameState.baseObstacleSpawnRate - (gameState.speedMultiplier * 15);
            gameState.obstacleSpawnRate = Math.max(Math.floor(calculatedRate), gameState.minObstacleSpawnRate);
            
            updateSpeedIndicator();
            flashSpeedIndicator();
            playSpeedUpSound();
        }

        function updateSpeedIndicator() {
            gameElements.speedIndicator.textContent = `Velocidad: ${gameState.speedMultiplier.toFixed(1)}x`;
        }

        function flashSpeedIndicator() {
            gameElements.speedIndicator.style.background = 'rgba(255, 193, 7, 0.4)';
            gameElements.speedIndicator.style.transform = 'scale(1.1)';
            setTimeout(() => {
                gameElements.speedIndicator.style.background = 'rgba(255, 107, 53, 0.2)';
                gameElements.speedIndicator.style.transform = 'scale(1)';
            }, 500);
        }

        function spawnObstacle() {
            const obstacle = document.createElement('div');
            obstacle.className = 'obstacle';
            const availableLanes = ['left', 'right'];
            const recentObstacles = gameState.obstacles.filter(obs => obs.y < 200);
            let lane;
            if (recentObstacles.length > 0) {
                const existingLane = recentObstacles[0].lane;
                lane = existingLane === 'left' ? 'right' : 'left';
            } else {
                lane = availableLanes[Math.floor(Math.random() * availableLanes.length)];
            }
            obstacle.classList.add('lane-' + lane);
            if (gameState.brightwayActive) {
                const randomColor = carColors[Math.floor(Math.random() * carColors.length)];
                obstacle.classList.add('car-' + randomColor);
            }
            gameElements.gameCanvas.appendChild(obstacle);
            gameState.obstacles.push({ 
                element: obstacle, 
                lane: lane, 
                passed: false, 
                y: -80,
                hit: false
            });
        }

        function updateObstacles() {
            gameState.obstacles = gameState.obstacles.filter(obs => {
                // Si el obstáculo fue golpeado, eliminarlo inmediatamente
                if (obs.hit) {
                    if (obs.element && obs.element.parentNode) {
                        obs.element.remove();
                    }
                    return false;
                }
                
                obs.y += gameState.gameSpeed;
                if (obs.element) {
                    obs.element.style.top = obs.y + 'px';
                }
                
                // Eliminar obstáculos que salieron de la pantalla
                if (obs.y > gameElements.gameCanvas.offsetHeight + 100) {
                    if (obs.element && obs.element.parentNode) {
                        obs.element.remove();
                    }
                    return false;
                }
                
                // Dar puntos por esquivar
                if (!obs.passed && !obs.hit && obs.y > gameElements.gameCanvas.offsetHeight - 200) {
                    obs.passed = true;
                    gameState.score += 30 * gameState.speedMultiplier;
                    playScoreSound();
                }
                
                return true;
            });
        }

        function checkCollisions() {
            const carY = gameElements.gameCanvas.offsetHeight - (gameState.isMobile ? 120 : 170);
            
            // Crear una copia del array para iterar de forma segura
            const obstaclesCopy = [...gameState.obstacles];
            
            obstaclesCopy.forEach(obs => {
                if (obs.hit) return;
                
                const collisionMargin = gameState.isMobile ? 35 : 40;
                
                // Verificar colisión
                if (obs.lane === gameState.carLane && 
                    obs.y >= carY - collisionMargin && obs.y <= carY + collisionMargin) {
                    obs.hit = true;
                    
                    // Eliminar el obstáculo inmediatamente del DOM
                    if (obs.element && obs.element.parentNode) {
                        obs.element.remove();
                    }
                    
                    // Eliminar del array de obstáculos
                    const index = gameState.obstacles.indexOf(obs);
                    if (index > -1) {
                        gameState.obstacles.splice(index, 1);
                    }
                    
                    hitObstacle();
                }
            });
        }

        function changeLane(newLane) {
            if (!gameState.running || gameState.paused) return;
            if (gameState.carLane === newLane) return;
            gameState.carLane = newLane;
            gameElements.car.classList.remove('lane-left', 'lane-right');
            gameElements.car.classList.add('lane-' + newLane);
        }

        function activateBrightWay() {
            if (!gameState.running || gameState.brightwayActive) return;
            gameState.brightwayActive = true;
            gameElements.lightEffect.classList.add('active');
            gameElements.carLights.style.opacity = '1';
            gameElements.gameCanvas.style.background = 'linear-gradient(135deg, #2A2A2A 0%, #1A1A1A 100%)';
            gameState.score += 150 * gameState.speedMultiplier;
            gameState.obstacles.forEach(obs => {
                const randomColor = carColors[Math.floor(Math.random() * carColors.length)];
                obs.element.classList.add('car-' + randomColor);
            });
            setTimeout(() => {
                gameState.brightwayActive = false;
                gameElements.lightEffect.classList.remove('active');
                gameElements.carLights.style.opacity = '0.4';
                gameElements.gameCanvas.style.background = 'var(--darker)';
                gameState.obstacles.forEach(obs => {
                    carColors.forEach(color => {
                        obs.element.classList.remove('car-' + color);
                    });
                });
            }, 4000);
        }

        function hitObstacle() {
            gameState.lives--;
            gameElements.lives.textContent = gameState.lives;
            playHitSound();
            const colorMap = {
                blue: 'linear-gradient(0deg, var(--blue), #1E40AF)',
                red: 'linear-gradient(0deg, #EF4444, #DC2626)',
                yellow: 'linear-gradient(0deg, #F59E0B, #D97706)'
            };
            const shadowMap = {
                blue: '0 5px 20px rgba(59, 130, 246, 0.4)',
                red: '0 5px 20px rgba(239, 68, 68, 0.4)',
                yellow: '0 5px 20px rgba(245, 158, 11, 0.4)'
            };
            gameElements.car.style.background = 'linear-gradient(0deg, var(--danger), #DC2626)';
            gameElements.car.style.boxShadow = '0 0 25px var(--danger)';
            setTimeout(() => {
                if (gameState.running) {
                    gameElements.car.style.background = colorMap[gameState.carColor];
                    gameElements.car.style.boxShadow = shadowMap[gameState.carColor];
                }
            }, 600);
            if (gameState.lives <= 0) {
                endGame();
            }
        }

        function togglePause() {
            if (!gameState.running) return;
            gameState.paused = !gameState.paused;
            gameElements.pauseBtn.textContent = gameState.paused ? 'Reanudar' : 'Pausar';
        }

        function endGame() {
            gameState.running = false;
            clearInterval(gameLoop);
            const finalScore = Math.floor(gameState.score / 60);
            if (finalScore > gameState.highScore) {
                gameState.highScore = finalScore;
                gameElements.highScore.textContent = gameState.highScore;
                localStorage.setItem('brightwayHighScore', gameState.highScore.toString());
            }
            gameElements.finalScore.textContent = finalScore;
            gameElements.gameOver.classList.add('show');
            gameElements.pauseBtn.disabled = true;
            gameElements.exitBtn.disabled = true;
            gameElements.pauseBtn.textContent = 'Pausar';
        }

        function returnToMenu() {
            if (gameLoop) clearInterval(gameLoop);
            gameState.running = false;
            gameState.paused = false;
            clearObstacles();
            gameElements.gameOver.classList.remove('show');
            gameElements.pauseBtn.disabled = true;
            gameElements.exitBtn.disabled = true;
            gameElements.pauseBtn.textContent = 'Pausar';
            gameState.score = 0;
            gameState.lives = 1;
            gameState.speedMultiplier = 1;
            updateUI();
            updateSpeedIndicator();
            document.getElementById('gameModal').classList.remove('active');
        }

        function resetGame() {
            if (gameLoop) clearInterval(gameLoop);
            gameState.running = false;
            gameState.speedMultiplier = 1;
            clearObstacles();
            gameElements.gameOver.classList.remove('show');
            startGame();
        }

        function clearObstacles() {
            gameState.obstacles.forEach(obs => {
                if (obs.element && obs.element.parentNode) {
                    obs.element.remove();
                }
            });
            gameState.obstacles = [];
        }

        function updateUI() {
            gameElements.score.textContent = Math.floor(gameState.score / 60);
            gameElements.lives.textContent = gameState.lives;
        }

        window.addEventListener('resize', () => {
            gameState.isMobile = isMobileDevice();
        });
    </script>
</body>
</html>
