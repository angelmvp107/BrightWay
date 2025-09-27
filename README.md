
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>BrightWay - Innovación en Seguridad Vial</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            --primary-orange: #FF6B35;
            --primary-yellow: #FFC107;
            --dark-bg: #1a1a1a;
            --darker-bg: #0d0d0d;
            --text-light: #ffffff;
            --text-gray: #b0b0b0;
            --accent-blue: #2196F3;
            --card-bg: rgba(255, 255, 255, 0.05);
            --danger-red: #ff3838;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: linear-gradient(135deg, var(--darker-bg) 0%, var(--dark-bg) 100%);
            color: var(--text-light);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Loading Screen */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: var(--darker-bg);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease;
        }

        .loading-screen.hidden {
            opacity: 0;
            pointer-events: none;
        }

        .loader {
            width: 60px;
            height: 60px;
            border: 3px solid rgba(255, 107, 53, 0.1);
            border-top-color: var(--primary-orange);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .loading-text {
            margin-top: 2rem;
            color: var(--text-gray);
            font-size: 1rem;
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(26, 26, 26, 0.98);
            backdrop-filter: blur(10px);
            padding: 1rem 1.5rem;
            z-index: 1000;
            box-shadow: 0 2px 20px rgba(0,0,0,0.3);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--primary-orange);
        }

        .logo-icon {
            width: 35px;
            height: 35px;
            background: linear-gradient(135deg, var(--primary-orange), var(--primary-yellow));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            animation: pulse 2s ease infinite;
            font-size: 1.2rem;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .nav-menu {
            display: flex;
            gap: 1rem;
            list-style: none;
        }

        .nav-item {
            background: none;
            border: none;
            color: var(--text-gray);
            cursor: pointer;
            font-size: 0.95rem;
            padding: 0.5rem 1rem;
            border-radius: 8px;
            transition: all 0.3s ease;
            position: relative;
            white-space: nowrap;
        }

        .nav-item:hover {
            color: var(--text-light);
            background: rgba(255, 107, 53, 0.1);
        }

        .nav-item.active {
            color: var(--primary-orange);
        }

        .nav-item.active::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 50%;
            transform: translateX(-50%);
            width: 30px;
            height: 3px;
            background: var(--primary-orange);
            border-radius: 2px;
        }

        .menu-toggle {
            display: none;
            background: none;
            border: none;
            color: var(--text-light);
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* Main Content */
        main {
            padding-top: 70px;
            min-height: 100vh;
        }

        .section {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { 
                opacity: 0;
                transform: translateY(20px);
            }
            to { 
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Hero Section */
        .hero {
            padding: 3rem 1.5rem;
            text-align: center;
            max-width: 1200px;
            margin: 0 auto;
        }

        .hero h1 {
            font-size: clamp(2rem, 5vw, 3.5rem);
            margin-bottom: 1rem;
            background: linear-gradient(135deg, var(--primary-orange), var(--primary-yellow));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: glow 2s ease infinite;
        }

        @keyframes glow {
            0%, 100% { filter: brightness(1); }
            50% { filter: brightness(1.2); }
        }

        .hero .tagline {
            font-size: 1.2rem;
            color: var(--text-gray);
            margin-bottom: 2rem;
        }

        .hero-description {
            max-width: 800px;
            margin: 0 auto;
            font-size: 1rem;
            line-height: 1.8;
            color: var(--text-gray);
        }

        /* 3D Product Visualization */
        .product-visualization {
            margin: 3rem auto;
            max-width: 500px;
            height: 350px;
            position: relative;
            perspective: 1000px;
        }

        .product-model {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            animation: rotate3d 10s linear infinite;
        }

        @keyframes rotate3d {
            from { transform: rotateY(0deg); }
            to { transform: rotateY(360deg); }
        }

        .trafitambo {
            width: 120px;
            height: 220px;
            margin: 0 auto;
            position: relative;
            transform-style: preserve-3d;
        }

        .trafitambo-body {
            width: 100%;
            height: 180px;
            background: linear-gradient(180deg, #FF6B35 0%, #FF8C42 50%, #FF6B35 100%);
            border-radius: 10px;
            position: absolute;
            bottom: 0;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
        }

        .trafitambo-stripes {
            position: absolute;
            width: 100%;
            height: 25px;
            background: white;
            top: 40px;
            opacity: 0.9;
        }

        .trafitambo-stripes::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 25px;
            background: white;
            top: 50px;
        }

        .solar-panel {
            width: 100px;
            height: 70px;
            background: linear-gradient(135deg, #1a237e 0%, #3949ab 100%);
            position: absolute;
            top: -25px;
            left: 50%;
            transform: translateX(-50%);
            border: 2px solid #5c6bc0;
            border-radius: 5px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            animation: panelTilt 4s ease infinite;
        }

        @keyframes panelTilt {
            0%, 100% { transform: translateX(-50%) rotateX(0deg); }
            50% { transform: translateX(-50%) rotateX(20deg); }
        }

        .solar-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 2px;
            padding: 5px;
            height: 100%;
        }

        .solar-cell {
            background: #3f51b5;
            border: 1px solid #7986cb;
        }

        .led-lights {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }

        .led {
            width: 8px;
            height: 8px;
            background: var(--primary-yellow);
            border-radius: 50%;
            box-shadow: 0 0 15px var(--primary-yellow);
            animation: blink 1s ease infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        /* Features */
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            padding: 1.5rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .feature-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 107, 53, 0.2);
            border-radius: 16px;
            padding: 1.5rem;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 40px rgba(255, 107, 53, 0.2);
            border-color: var(--primary-orange);
        }

        .feature-icon {
            width: 45px;
            height: 45px;
            background: linear-gradient(135deg, var(--primary-orange), var(--primary-yellow));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 1rem;
            font-size: 1.3rem;
        }

        .feature-card h3 {
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
        }

        .feature-card p {
            font-size: 0.9rem;
            color: var(--text-gray);
            line-height: 1.6;
        }

        /* Materials Section */
        .materials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 1.5rem;
            padding: 1.5rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .material-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 1.5rem;
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .material-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, var(--primary-orange), var(--primary-yellow));
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .material-card:hover::before {
            transform: scaleX(1);
        }

        .material-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(255, 107, 53, 0.2);
        }

        .material-number {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: var(--primary-orange);
            color: white;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.85rem;
            font-weight: bold;
        }

        .material-name {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: var(--primary-orange);
        }

        .material-description {
            color: var(--text-gray);
            font-size: 0.85rem;
            line-height: 1.5;
            margin-bottom: 1rem;
        }

        .material-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 0.75rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .material-price {
            color: var(--primary-yellow);
            font-weight: bold;
            font-size: 0.9rem;
        }

        .material-quantity {
            color: var(--text-gray);
            font-size: 0.85rem;
        }

        /* Game Section */
        .game-container {
            max-width: 900px;
            margin: 1rem auto;
            padding: 1.5rem;
        }

        .game-header {
            text-align: center;
            margin-bottom: 1.5rem;
        }

        .game-stats {
            display: flex;
            justify-content: space-around;
            max-width: 400px;
            margin: 1rem auto;
            padding: 1rem;
            background: var(--card-bg);
            border-radius: 12px;
            border: 1px solid rgba(255, 107, 53, 0.2);
        }

        .stat-item {
            text-align: center;
        }

        .stat-label {
            color: var(--text-gray);
            font-size: 0.85rem;
            margin-bottom: 0.25rem;
        }

        .stat-value {
            color: var(--primary-yellow);
            font-size: 1.5rem;
            font-weight: bold;
        }

        .game-canvas {
            width: 100%;
            max-width: 800px;
            height: 450px;
            margin: 0 auto;
            background: linear-gradient(180deg, #0a0a0a 0%, #1a1a1a 100%);
            border: 2px solid var(--primary-orange);
            border-radius: 16px;
            position: relative;
            overflow: hidden;
            cursor: pointer;
            touch-action: none;
        }

        .road {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 120px;
            background: linear-gradient(180deg, #333 0%, #222 100%);
            border-top: 2px solid #555;
        }

        .road-line {
            position: absolute;
            bottom: 55px;
            width: 100%;
            height: 4px;
            background: repeating-linear-gradient(
                90deg,
                #fff 0px,
                #fff 30px,
                transparent 30px,
                transparent 60px
            );
            animation: roadMove 1s linear infinite;
        }

        @keyframes roadMove {
            from { transform: translateX(0); }
            to { transform: translateX(-60px); }
        }

        .car {
            position: absolute;
            bottom: 80px;
            left: 100px;
            width: 70px;
            height: 35px;
            background: linear-gradient(90deg, #2196F3 0%, #1976D2 100%);
            border-radius: 10px 20px 5px 5px;
            transition: left 0.2s ease, bottom 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            z-index: 10;
        }

        .car::before {
            content: '';
            position: absolute;
            top: -12px;
            left: 12px;
            width: 35px;
            height: 18px;
            background: rgba(33, 150, 243, 0.3);
            border-radius: 5px 5px 0 0;
        }

        .car.jumping {
            animation: jump 0.5s ease;
        }

        @keyframes jump {
            0%, 100% { bottom: 80px; }
            50% { bottom: 150px; }
        }

        .car.crashed {
            background: linear-gradient(90deg, var(--danger-red) 0%, #cc0000 100%);
            animation: crash 0.5s ease;
        }

        @keyframes crash {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(-5deg); }
            75% { transform: rotate(5deg); }
        }

        .car-lights {
            position: absolute;
            right: -15px;
            top: 50%;
            transform: translateY(-50%);
            width: 30px;
            height: 15px;
            background: radial-gradient(circle, rgba(255,255,255,0.8) 0%, transparent 70%);
            opacity: 0.3;
            transition: all 0.3s ease;
        }

        .obstacle {
            position: absolute;
            bottom: 80px;
            width: 50px;
            height: 40px;
            background: linear-gradient(135deg, #666 0%, #444 100%);
            border-radius: 5px;
            box-shadow: 0 5px 10px rgba(0,0,0,0.5);
            animation: moveLeft 3s linear;
        }

        @keyframes moveLeft {
            from { right: -60px; }
            to { right: 100%; }
        }

        .obstacle.rock {
            background: radial-gradient(circle, #8b7355 0%, #5c4a3a 100%);
            border-radius: 40% 60% 70% 30% / 60% 40% 60% 40%;
            height: 35px;
        }

        .obstacle.barrier {
            background: repeating-linear-gradient(
                45deg,
                #ff9800,
                #ff9800 10px,
                #fff 10px,
                #fff 20px
            );
            height: 45px;
            border: 2px solid #ff6600;
        }

        .brightway-game {
            position: absolute;
            right: 200px;
            bottom: 130px;
            width: 50px;
            height: 90px;
            cursor: pointer;
            transition: all 0.3s ease;
            z-index: 5;
        }

        .brightway-game-body {
            width: 35px;
            height: 65px;
            background: linear-gradient(180deg, var(--primary-orange) 0%, #ff8c42 100%);
            border-radius: 5px;
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 5px 10px rgba(0,0,0,0.3);
        }

        .brightway-game-panel {
            width: 30px;
            height: 20px;
            background: linear-gradient(135deg, #1a237e 0%, #3949ab 100%);
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            border: 2px solid #3949ab;
            border-radius: 3px;
        }

        .brightway-light {
            position: absolute;
            top: -40px;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, rgba(255,193,7,0.7) 0%, transparent 70%);
            opacity: 0;
            transition: opacity 0.5s ease;
            pointer-events: none;
        }

        .brightway-light.active {
            opacity: 1;
            animation: lightPulse 2s ease infinite;
        }

        @keyframes lightPulse {
            0%, 100% { transform: translateX(-50%) scale(1); }
            50% { transform: translateX(-50%) scale(1.1); }
        }

        .game-controls {
            text-align: center;
            margin-top: 1.5rem;
        }

        .game-btn {
            background: linear-gradient(135deg, var(--primary-orange), var(--primary-yellow));
            color: white;
            border: none;
            padding: 0.8rem 2rem;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 20px rgba(255, 107, 53, 0.3);
            margin: 0 0.5rem;
        }

        .game-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(255, 107, 53, 0.4);
        }

        .game-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .game-instructions {
            margin-top: 1rem;
            padding: 1rem;
            background: var(--card-bg);
            border-radius: 12px;
            border: 1px solid rgba(255, 107, 53, 0.1);
        }

        .game-instructions h4 {
            color: var(--primary-orange);
            margin-bottom: 0.5rem;
        }

        .game-instructions p {
            color: var(--text-gray);
            font-size: 0.9rem;
            line-height: 1.5;
            margin-bottom: 0.5rem;
        }

        .control-buttons {
            display: none;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            max-width: 250px;
            margin: 1rem auto;
        }

        .control-btn {
            background: var(--card-bg);
            border: 1px solid var(--primary-orange);
            color: var(--primary-orange);
            padding: 1rem;
            border-radius: 12px;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.2s ease;
            user-select: none;
        }

        .control-btn:active {
            background: rgba(255, 107, 53, 0.2);
            transform: scale(0.95);
        }

        .game-over-modal {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(26, 26, 26, 0.95);
            padding: 2rem;
            border-radius: 16px;
            border: 2px solid var(--primary-orange);
            text-align: center;
            z-index: 100;
            backdrop-filter: blur(10px);
        }

        .game-over-modal.show {
            display: block;
            animation: modalAppear 0.3s ease;
        }

        @keyframes modalAppear {
            from { 
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.8);
            }
            to { 
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }

        .game-over-modal h3 {
            color: var(--primary-orange);
            font-size: 1.5rem;
            margin-bottom: 1rem;
        }

        .final-score {
            font-size: 2rem;
            color: var(--primary-yellow);
            font-weight: bold;
            margin-bottom: 1rem;
        }

        /* Footer */
        .footer {
            margin-top: 3rem;
            padding: 2rem 1.5rem;
            text-align: center;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(13, 13, 13, 0.5);
        }

        .company-info {
            margin-bottom: 1.5rem;
        }

        .company-logo {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .company-name {
            font-size: 1.2rem;
            font-weight: bold;
            background: linear-gradient(135deg, var(--primary-orange), var(--primary-yellow));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .creators {
            margin: 1rem 0;
            color: var(--text-gray);
            font-size: 0.9rem;
        }

        .creators span {
            color: var(--primary-orange);
            font-weight: bold;
        }

        .university {
            color: var(--text-gray);
            font-size: 0.85rem;
            margin-top: 0.5rem;
        }

        .copyright {
            color: var(--text-gray);
            font-size: 0.8rem;
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            nav {
                padding: 0.8rem 1rem;
            }

            .logo {
                font-size: 1.1rem;
            }

            .logo-icon {
                width: 30px;
                height: 30px;
            }

            .nav-menu {
                gap: 0.5rem;
            }

            .nav-item {
                font-size: 0.85rem;
                padding: 0.4rem 0.7rem;
            }

            .hero h1 {
                font-size: 2rem;
            }

            .hero .tagline {
                font-size: 1rem;
            }

            .product-visualization {
                height: 300px;
            }

            .trafitambo {
                width: 100px;
                height: 180px;
            }

            .features {
                grid-template-columns: 1fr;
                gap: 1rem;
            }

            .materials-grid {
                grid-template-columns: 1fr;
                gap: 1rem;
            }

            .game-canvas {
                height: 350px;
            }

            .control-buttons {
                display: grid;
            }

            .game-instructions p {
                font-size: 0.85rem;
            }

            .obstacle {
                width: 40px;
                height: 35px;
            }

            .car {
                width: 60px;
                height: 30px;
            }
        }

        @media (max-width: 480px) {
            .nav-item span {
                display: none;
            }

            .nav-item::before {
                font-size: 1.2rem;
            }

            .nav-item:nth-child(1)::before { content: "📝"; }
            .nav-item:nth-child(2)::before { content: "🔧"; }
            .nav-item:nth-child(3)::before { content: "🎮"; }

            .hero {
                padding: 2rem 1rem;
            }

            .game-canvas {
                height: 300px;
            }

            .game-stats {
                flex-direction: row;
                padding: 0.75rem;
            }

            .stat-value {
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading-screen" id="loadingScreen">
        <div class="loader"></div>
        <p class="loading-text">Cargando BrightWay...</p>
    </div>

    <!-- Navigation -->
    <nav>
        <div class="nav-container">
            <div class="logo">
                <div class="logo-icon">💡</div>
                <span>BrightWay</span>
            </div>
            <div class="nav-menu" id="navMenu">
                <button class="nav-item active" data-section="description">
                    <span>Descripción</span>
                </button>
                <button class="nav-item" data-section="materials">
                    <span>Materiales</span>
                </button>
                <button class="nav-item" data-section="game">
                    <span>Minijuego</span>
                </button>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main>
        <!-- Description Section -->
        <section id="description" class="section active">
            <div class="hero">
                <h1>BrightWay</h1>
                <p class="tagline">Dale luz a tu camino</p>
                <p class="hero-description">
                    BrightWay vela por tu seguridad al implementar tecnologías modernas y buenas para el ambiente. 
                    Un innovador sistema de señalización vial que combina un trafitambo tradicional con tecnología 
                    solar avanzada, proporcionando iluminación autónoma y sostenible para mejorar la seguridad vial.
                </p>
            </div>

            <!-- 3D Product Visualization -->
            <div class="product-visualization">
                <div class="product-model">
                    <div class="trafitambo">
                        <div class="solar-panel">
                            <div class="solar-grid">
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                                <div class="solar-cell"></div>
                            </div>
                        </div>
                        <div class="trafitambo-body">
                            <div class="trafitambo-stripes"></div>
                            <div class="led-lights">
                                <div class="led"></div>
                                <div class="led"></div>
                                <div class="led"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Features -->
            <div class="features">
                <div class="feature-card">
                    <div class="feature-icon">☀️</div>
                    <h3>Energía Solar</h3>
                    <p>Panel solar móvil con servomotores para optimizar la captación de energía durante todo el día.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">💡</div>
                    <h3>Iluminación LED</h3>
                    <p>Sistema de LEDs de alta eficiencia con sensor de movimiento para máxima visibilidad nocturna.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🌱</div>
                    <h3>Eco-Amigable</h3>
                    <p>Tecnología 100% sustentable que no requiere conexión eléctrica externa.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🔧</div>
                    <h3>Arduino Nano</h3>
                    <p>Control inteligente mediante microcontrolador para gestión automática del sistema.</p>
                </div>
            </div>
        </section>

        <!-- Materials Section -->
        <section id="materials" class="section">
            <div class="hero">
                <h1>Materiales</h1>
                <p class="tagline">Componentes del Sistema BrightWay</p>
            </div>
            
            <div class="materials-grid" id="materialsGrid">
                <!-- Materials will be dynamically loaded here -->
            </div>
        </section>

        <!-- Game Section -->
        <section id="game" class="section">
            <div class="game-container">
                <div class="game-header">
                    <h1>Minijuego BrightWay</h1>
                    <p class="tagline">Esquiva obstáculos y activa el BrightWay</p>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div class="stat-label">Puntos</div>
                        <div class="stat-value" id="score">0</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">Record</div>
                        <div class="stat-value" id="highScore">0</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">Vidas</div>
                        <div class="stat-value" id="lives">3</div>
                    </div>
                </div>
                
                <div class="game-canvas" id="gameCanvas">
                    <div class="road">
                        <div class="road-line"></div>
                    </div>
                    <div class="car" id="car">
                        <div class="car-lights" id="carLights"></div>
                    </div>
                    <div class="brightway-game" id="brightwayGame">
                        <div class="brightway-game-body"></div>
                        <div class="brightway-game-panel"></div>
                        <div class="brightway-light" id="brightwayLight"></div>
                    </div>
                    <div class="game-over-modal" id="gameOverModal">
                        <h3>¡Juego Terminado!</h3>
                        <div class="final-score">Puntuación: <span id="finalScore">0</span></div>
                        <button class="game-btn" onclick="resetGame()">Jugar de Nuevo</button>
                    </div>
                </div>

                <div class="control-buttons">
                    <div></div>
                    <button class="control-btn" id="jumpBtn">⬆️</button>
                    <div></div>
                    <button class="control-btn" id="leftBtn">⬅️</button>
                    <button class="control-btn" id="lightBtn">💡</button>
                    <button class="control-btn" id="rightBtn">➡️</button>
                </div>
                
                <div class="game-controls">
                    <button class="game-btn" id="startGame">Iniciar Juego</button>
                    <button class="game-btn" id="pauseGame" disabled>Pausar</button>
                </div>

                <div class="game-instructions">
                    <h4>Cómo Jugar:</h4>
                    <p>🎯 <strong>Objetivo:</strong> Esquiva los obstáculos y activa el BrightWay para iluminar el camino</p>
                    <p>⌨️ <strong>Controles PC:</strong> Flechas ← → para mover, ↑ para saltar, Espacio para activar BrightWay</p>
                    <p>📱 <strong>Controles Móvil:</strong> Usa los botones en pantalla</p>
                    <p>💡 <strong>Tip:</strong> Activa el BrightWay para ganar puntos extra y ver mejor los obstáculos</p>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="footer">
        <div class="company-info">
            <div class="company-logo">
                <div class="logo-icon">💡</div>
                <span class="company-name">BrightWay Technologies</span>
            </div>
            <div class="creators">
                Desarrollado por: <span>Pablo Nicolás García Huerta</span> y <span>Ángel Antonio Ruiz García</span>
            </div>
            <div class="university">Universidad Autónoma de Querétaro - Facultad de Ingeniería</div>
        </div>
        <div class="copyright">
            © 2024 BrightWay Technologies. Todos los derechos reservados. | Innovación en Seguridad Vial
        </div>
    </footer>

    <script>
        // Materials Data
        const materials = [
            {
                id: 1,
                name: "Lámpara Solar",
                description: "Lámpara solar LLINPI con 106 LEDs, panel solar, sensor PIR, resistente al agua IP65.",
                price: "$218.56",
                quantity: "1 pieza"
            },
            {
                id: 2,
                name: "Arduino Nano",
                description: "Microcontrolador ATmega328, voltaje 7-12V, memoria flash 32KB, conexión USB mini-B.",
                price: "$118.99",
                quantity: "1 pieza"
            },
            {
                id: 3,
                name: "Servomotor SG90",
                description: "Motor compacto 22x11.8x31mm, rotación 180°, torque 1.6 kg/cm, señal PWM.",
                price: "$61",
                quantity: "2 piezas"
            },
            {
                id: 4,
                name: "LDR",
                description: "Fotoresistencia 2MΩ, varía resistencia según luz, ideal para Arduino y robótica.",
                price: "$8",
                quantity: "4 piezas"
            },
            {
                id: 5,
                name: "Resistencia 10kΩ",
                description: "Resistencia 10K ohms, 0.25W, componente estándar para limitar corriente.",
                price: "$1.08",
                quantity: "4 piezas"
            },
            {
                id: 6,
                name: "Potenciómetro 10kΩ",
                description: "Resistencia variable 0-10kΩ, control manual, ideal para calibración.",
                price: "$8",
                quantity: "2 piezas"
            },
            {
                id: 7,
                name: "Cable USB Nano",
                description: "Cable USB 1.8m para Arduino Nano, blindaje multicapa, transmisión estable.",
                price: "$25",
                quantity: "1 pieza"
            },
            {
                id: 8,
                name: "Cables Dupont",
                description: "Cables tipo Dupont, cobre calibre 28 AWG, conectores latón niquelado.",
                price: "$89",
                quantity: "Varios"
            },
            {
                id: 9,
                name: "Protoboard",
                description: "Protoboard 830 perforaciones, 16.5x5.6cm, soporta 3A, líneas alimentación.",
                price: "$130",
                quantity: "1 pieza"
            },
            {
                id: 10,
                name: "Adaptador 5V",
                description: "Fuente alimentación 5Vcc, 2A máximo, voltaje constante regulado.",
                price: "$107.99",
                quantity: "1 pieza"
            },
            {
                id: 11,
                name: "Impresiones 3D",
                description: "Piezas del mecanismo BrightWay para movilidad del panel y estructura soporte.",
                price: "Variable",
                quantity: "Varias"
            },
            {
                id: 12,
                name: "Trafitambo",
                description: "Tambor plástico/metal naranja con franjas reflejantes, alta visibilidad día/noche.",
                price: "Variable",
                quantity: "1 pieza"
            }
        ];

        // Loading Screen
        window.addEventListener('load', () => {
            setTimeout(() => {
                document.getElementById('loadingScreen').classList.add('hidden');
            }, 1500);
        });

        // Navigation
        const navItems = document.querySelectorAll('.nav-item');
        const sections = document.querySelectorAll('.section');

        navItems.forEach(item => {
            item.addEventListener('click', () => {
                const targetSection = item.dataset.section;
                
                navItems.forEach(navItem => navItem.classList.remove('active'));
                item.classList.add('active');
                
                sections.forEach(section => section.classList.remove('active'));
                document.getElementById(targetSection).classList.add('active');

                if (targetSection === 'game') {
                    initGame();
                }
            });
        });

        // Load Materials
        function loadMaterials() {
            const materialsGrid = document.getElementById('materialsGrid');
            if (!materialsGrid) return;
            
            materials.forEach(material => {
                const card = document.createElement('div');
                card.className = 'material-card';
                card.innerHTML = `
                    <div class="material-number">${material.id}</div>
                    <h3 class="material-name">${material.name}</h3>
                    <p class="material-description">${material.description}</p>
                    <div class="material-footer">
                        <span class="material-price">${material.price}</span>
                        <span class="material-quantity">${material.quantity}</span>
                    </div>
                `;
                materialsGrid.appendChild(card);
            });
        }

        loadMaterials();

        // Game Variables
        let gameRunning = false;
        let gamePaused = false;
        let score = 0;
        let highScore = localStorage.getItem('brightwayHighScore') || 0;
        let lives = 3;
        let carPosition = 100;
        let carLane = 1; // 0: top, 1: middle, 2: bottom
        let brightwayActivated = false;
        let obstacles = [];
        let gameSpeed = 5;
        let obstacleSpawnTimer = 0;
        let gameLoop;
        let isJumping = false;

        // Game Elements
        const car = document.getElementById('car');
        const carLights = document.getElementById('carLights');
        const brightwayGame = document.getElementById('brightwayGame');
        const brightwayLight = document.getElementById('brightwayLight');
        const scoreElement = document.getElementById('score');
        const highScoreElement = document.getElementById('highScore');
        const livesElement = document.getElementById('lives');
        const gameCanvas = document.getElementById('gameCanvas');
        const gameOverModal = document.getElementById('gameOverModal');
        const finalScoreElement = document.getElementById('finalScore');
        const startBtn = document.getElementById('startGame');
        const pauseBtn = document.getElementById('pauseGame');

        // Initialize high score display
        highScoreElement.textContent = highScore;

        function initGame() {
            if (!gameRunning) {
                carPosition = 100;
                car.style.left = carPosition + 'px';
            }
        }

        function startGame() {
            if (gameRunning) return;
            
            gameRunning = true;
            gamePaused = false;
            score = 0;
            lives = 3;
            carPosition = 100;
            carLane = 1;
            brightwayActivated = false;
            obstacles = [];
            gameSpeed = 5;
            obstacleSpawnTimer = 0;
            isJumping = false;
            
            scoreElement.textContent = score;
            livesElement.textContent = lives;
            startBtn.textContent = 'Reiniciar';
            startBtn.disabled = true;
            pauseBtn.disabled = false;
            
            car.style.left = carPosition + 'px';
            car.classList.remove('crashed');
            brightwayLight.classList.remove('active');
            carLights.style.opacity = '0.3';
            gameOverModal.classList.remove('show');
            
            // Clear existing obstacles
            document.querySelectorAll('.obstacle').forEach(obs => obs.remove());
            
            // Position BrightWay
            const randomPos = Math.random() * 400 + 200;
            brightwayGame.style.right = randomPos + 'px';
            
            // Start game loop
            gameLoop = setInterval(updateGame, 1000 / 60); // 60 FPS
            
            setTimeout(() => {
                startBtn.disabled = false;
            }, 1000);
        }

        function updateGame() {
            if (!gameRunning || gamePaused) return;
            
            // Update score
            if (brightwayActivated) {
                score += 1;
                scoreElement.textContent = Math.floor(score / 10);
            }
            
            // Spawn obstacles
            obstacleSpawnTimer++;
            if (obstacleSpawnTimer > (brightwayActivated ? 80 : 120)) {
                spawnObstacle();
                obstacleSpawnTimer = 0;
            }
            
            // Update obstacles
            updateObstacles();
            
            // Check collisions
            checkCollisions();
            
            // Increase difficulty
            if (score > 0 && score % 500 === 0) {
                gameSpeed = Math.min(gameSpeed + 0.5, 12);
            }
        }

        function spawnObstacle() {
            const obstacle = document.createElement('div');
            obstacle.className = 'obstacle';
            
            const types = ['rock', 'barrier', ''];
            const type = types[Math.floor(Math.random() * types.length)];
            if (type) obstacle.classList.add(type);
            
            const lane = Math.floor(Math.random() * 3);
            const bottomPosition = 80 + (lane * 0); // All obstacles at same height for simplicity
            obstacle.style.bottom = bottomPosition + 'px';
            obstacle.style.right = '-60px';
            obstacle.style.animationDuration = (800 / gameSpeed) + 's';
            
            gameCanvas.appendChild(obstacle);
            obstacles.push({element: obstacle, passed: false});
        }

        function updateObstacles() {
            obstacles = obstacles.filter(obs => {
                const rect = obs.element.getBoundingClientRect();
                const canvasRect = gameCanvas.getBoundingClientRect();
                
                // Remove obstacles that have left the screen
                if (rect.right < canvasRect.left) {
                    obs.element.remove();
                    return false;
                }
                
                // Add score for passed obstacles
                if (!obs.passed && rect.right < canvasRect.left + carPosition) {
                    obs.passed = true;
                    score += 5;
                    scoreElement.textContent = Math.floor(score / 10);
                }
                
                return true;
            });
        }

        function checkCollisions() {
            if (isJumping) return;
            
            const carRect = car.getBoundingClientRect();
            
            obstacles.forEach(obs => {
                const obsRect = obs.element.getBoundingClientRect();
                
                if (carRect.left < obsRect.right &&
                    carRect.right > obsRect.left &&
                    carRect.top < obsRect.bottom &&
                    carRect.bottom > obsRect.top) {
                    
                    if (!obs.hit) {
                        obs.hit = true;
                        hitObstacle();
                    }
                }
            });
        }

        function hitObstacle() {
            lives--;
            livesElement.textContent = lives;
            
            car.classList.add('crashed');
            setTimeout(() => {
                car.classList.remove('crashed');
            }, 500);
            
            if (lives <= 0) {
                endGame();
            }
        }

        function jumpCar() {
            if (isJumping || !gameRunning || gamePaused) return;
            
            isJumping = true;
            car.classList.add('jumping');
            
            setTimeout(() => {
                car.classList.remove('jumping');
                isJumping = false;
            }, 500);
        }

        function moveCar(direction) {
            if (!gameRunning || gamePaused) return;
            
            if (direction === 'left' && carPosition > 20) {
                carPosition = Math.max(carPosition - 30, 20);
            } else if (direction === 'right' && carPosition < 700) {
                carPosition = Math.min(carPosition + 30, 700);
            }
            
            car.style.left = carPosition + 'px';
        }

        function activateBrightway() {
            if (!gameRunning || brightwayActivated) return;
            
            brightwayActivated = true;
            brightwayLight.classList.add('active');
            carLights.style.opacity = '1';
            car.style.boxShadow = '0 5px 30px rgba(255, 193, 7, 0.5)';
            
            score += 100;
            scoreElement.textContent = Math.floor(score / 10);
        }

        function pauseGame() {
            if (!gameRunning) return;
            
            gamePaused = !gamePaused;
            pauseBtn.textContent = gamePaused ? 'Reanudar' : 'Pausar';
        }

        function endGame() {
            gameRunning = false;
            clearInterval(gameLoop);
            
            finalScoreElement.textContent = Math.floor(score / 10);
            gameOverModal.classList.add('show');
            
            if (score / 10 > highScore) {
                highScore = Math.floor(score / 10);
                highScoreElement.textContent = highScore;
                localStorage.setItem('brightwayHighScore', highScore);
            }
            
            startBtn.textContent = 'Iniciar Juego';
            startBtn.disabled = false;
            pauseBtn.disabled = true;
            pauseBtn.textContent = 'Pausar';
        }

        function resetGame() {
            gameOverModal.classList.remove('show');
            startGame();
        }

        // Keyboard Controls
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') moveCar('left');
            else if (e.key === 'ArrowRight') moveCar('right');
            else if (e.key === 'ArrowUp') jumpCar();
            else if (e.key === ' ') {
                e.preventDefault();
                activateBrightway();
            }
        });

        // Button Controls
        startBtn.addEventListener('click', startGame);
        pauseBtn.addEventListener('click', pauseGame);
        
        // Mobile Controls
        document.getElementById('leftBtn')?.addEventListener('click', () => moveCar('left'));
        document.getElementById('rightBtn')?.addEventListener('click', () => moveCar('right'));
        document.getElementById('jumpBtn')?.addEventListener('click', jumpCar);
        document.getElementById('lightBtn')?.addEventListener('click', activateBrightway);
        
        // Touch controls for mobile
        let touchStartX = 0;
        let touchStartY = 0;
        
        gameCanvas.addEventListener('touchstart', (e) => {
            touchStartX = e.touches[0].clientX;
            touchStartY = e.touches[0].clientY;
        });
        
        gameCanvas.addEventListener('touchmove', (e) => {
            if (!gameRunning || gamePaused) return;
            e.preventDefault();
            
            const touchX = e.touches[0].clientX;
            const touchY = e.touches[0].clientY;
            const diffX = touchX - touchStartX;
            const diffY = touchStartY - touchY;
            
            if (Math.abs(diffX) > 30) {
                if (diffX > 0) moveCar('right');
                else moveCar('left');
                touchStartX = touchX;
            }
            
            if (diffY > 50) {
                jumpCar();
                touchStartY = touchY;
            }
        });
        
        // Click on BrightWay to activate
        brightwayGame.addEventListener('click', activateBrightway);
    </script>
</body>
</html>
