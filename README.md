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
        }

        :root {
            --primary: #FF6B35;
            --primary-light: #FF8C42;
            --accent: #FFC107;
            --dark: #0A0A0A;
            --darker: #000000;
            --gray-900: #111111;
            --gray-800: #1A1A1A;
            --gray-700: #2A2A2A;
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
        }

        /* Loading Screen */
        .loading {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: var(--darker);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.8s ease, visibility 0.8s ease;
        }

        .loading.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .loading-spinner {
            width: 50px;
            height: 50px;
            border: 3px solid rgba(255, 107, 53, 0.1);
            border-top: 3px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 1rem;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .loading-text {
            color: var(--gray-400);
            font-size: 0.9rem;
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            z-index: 1000;
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 1.5rem;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
        }

        .logo-icon {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }

        .nav-menu {
            display: flex;
            gap: 0.5rem;
        }

        .nav-btn {
            background: none;
            border: none;
            color: var(--gray-400);
            padding: 0.75rem 1rem;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nav-btn:hover {
            color: var(--white);
            background: rgba(255, 255, 255, 0.05);
        }

        .nav-btn.active {
            color: var(--primary);
            background: rgba(255, 107, 53, 0.1);
        }

        /* Main Content */
        main {
            padding-top: 70px;
        }

        .section {
            display: none;
            min-height: calc(100vh - 70px);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.5s ease;
        }

        .section.active {
            display: block;
            opacity: 1;
            transform: translateY(0);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        /* Hero Section */
        .hero {
            padding: 4rem 0;
            text-align: center;
        }

        .hero-title {
            font-size: clamp(3rem, 8vw, 5rem);
            font-weight: 800;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1rem;
            line-height: 1.1;
        }

        .hero-subtitle {
            font-size: 1.25rem;
            color: var(--gray-400);
            margin-bottom: 2rem;
            font-weight: 400;
        }

        .hero-description {
            max-width: 600px;
            margin: 0 auto 3rem;
            font-size: 1.1rem;
            color: var(--gray-300);
            line-height: 1.7;
        }

        /* Product Visualization */
        .product-showcase {
            margin: 3rem 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 400px;
        }

        .product-3d {
            position: relative;
            width: 300px;
            height: 400px;
            perspective: 1000px;
        }

        .trafitambo {
            position: relative;
            width: 120px;
            height: 250px;
            margin: 0 auto;
            transform-style: preserve-3d;
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

        /* Features */
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
            color: var(--white);
        }

        .feature-description {
            color: var(--gray-400);
            font-size: 0.95rem;
            line-height: 1.6;
        }

        /* Materials Section */
        .materials {
            padding: 4rem 0;
        }

        .materials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .material-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 1.5rem;
            transition: all 0.3s ease;
        }

        .material-card:hover {
            border-color: rgba(255, 107, 53, 0.3);
            transform: translateY(-4px);
        }

        .material-header {
            display: flex;
            align-items: flex-start;
            margin-bottom: 1rem;
        }

        .material-number {
            background: var(--primary);
            color: var(--white);
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: 600;
            margin-right: 1rem;
            flex-shrink: 0;
        }

        .material-name {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--white);
            margin-bottom: 0.5rem;
            flex: 1;
        }

        .material-description {
            color: var(--gray-400);
            font-size: 0.9rem;
            line-height: 1.5;
            margin-bottom: 1rem;
        }

        .material-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        .material-price {
            color: var(--accent);
            font-weight: 600;
        }

        .material-quantity {
            color: var(--gray-400);
            font-size: 0.85rem;
        }

        /* Enhanced Game Section - From brightway_game_only.html */
        .game {
            padding: 4rem 0;
            text-align: center;
        }

        .game-container {
            max-width: 900px;
            width: 100%;
        }

        .game-stats {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin: 2rem 0;
        }

        .stat {
            text-align: center;
        }

        .stat-label {
            color: var(--gray-400);
            font-size: 0.9rem;
            margin-bottom: 0.5rem;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--accent);
        }

        .game-canvas {
            position: relative;
            width: 100%;
            max-width: 800px;
            height: 600px;
            margin: 2rem auto;
            background: var(--darker);
            border-radius: 20px;
            overflow: hidden;
            border: 3px solid var(--gray-600);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
        }

        /* Road - Top Down View */
        .road {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 350px;
            height: 100%;
            background: linear-gradient(0deg, #333333 0%, #222222 100%);
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
            background: repeating-linear-gradient(
                to bottom,
                var(--white) 0px,
                var(--white) 30px,
                transparent 30px,
                transparent 60px
            );
            animation: roadMove 2s linear infinite;
        }

        @keyframes roadMove {
            0% { transform: translateX(-50%) translateY(0); }
            100% { transform: translateX(-50%) translateY(60px); }
        }

        /* Car - Top Down View */
        .car {
            position: absolute;
            bottom: 80px;
            left: 35%;
            width: 50px;
            height: 90px;
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

        /* Car Details - Top View */
        .car::before {
            content: '';
            position: absolute;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            width: 35px;
            height: 45px;
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
            width: 25px;
            height: 15px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 8px 8px 0 0;
        }

        .car-lights {
            position: absolute;
            top: -8px;
            left: 50%;
            transform: translateX(-50%);
            width: 40px;
            height: 20px;
            background: radial-gradient(ellipse, rgba(255, 255, 255, 0.8) 0%, transparent 70%);
            border-radius: 50%;
            opacity: 0.4;
            transition: all 0.3s ease;
        }

        /* Obstacles - Top Down View */
        .obstacle {
            position: absolute;
            top: -60px;
            width: 50px;
            height: 80px;
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
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 35px;
            height: 40px;
            background: rgba(64, 64, 64, 0.8);
            border-radius: 8px;
        }

        /* BrightWay Post */
        .brightway-post {
            position: absolute;
            right: 60px;
            top: 50%;
            transform: translateY(-50%);
            width: 50px;
            height: 100px;
            cursor: pointer;
            z-index: 5;
            transition: all 0.3s ease;
        }

        .brightway-post:hover {
            transform: translateY(-50%) scale(1.1);
        }

        .brightway-body {
            width: 40px;
            height: 80px;
            background: linear-gradient(180deg, var(--primary), var(--primary-light));
            border-radius: 8px;
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 5px 20px rgba(255, 107, 53, 0.4);
        }

        .brightway-panel {
            width: 35px;
            height: 20px;
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
            width: 600px;
            height: 600px;
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

        /* Game Controls */
        .game-controls {
            margin: 2rem 0;
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            flex-wrap: wrap;
        }

        .btn {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: var(--white);
            border: none;
            padding: 1rem 2rem;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 140px;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(255, 107, 53, 0.4);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        /* Mobile Controls */
        .mobile-controls {
            display: none;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 1rem;
            max-width: 400px;
            margin: 2rem auto;
        }

        .control-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 107, 53, 0.4);
            color: var(--primary);
            padding: 1.5rem;
            border-radius: 15px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .control-btn:active {
            background: rgba(255, 107, 53, 0.3);
            transform: scale(0.95);
        }

        /* Game Over Modal */
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
            font-size: 2rem;
            margin-bottom: 1.5rem;
        }

        .final-score {
            font-size: 3rem;
            color: var(--accent);
            font-weight: 700;
            margin-bottom: 2rem;
        }

        /* Instructions */
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
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }

        .instructions p {
            color: var(--gray-400);
            font-size: 1rem;
            margin-bottom: 0.8rem;
            line-height: 1.6;
        }

        /* Footer */
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

        .creators {
            margin: 1rem 0;
            font-size: 0.9rem;
        }

        .creators strong {
            color: var(--primary);
        }

        .university {
            font-size: 0.85rem;
            margin-bottom: 1rem;
        }

        .copyright {
            font-size: 0.8rem;
            padding-top: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .nav-container {
                padding: 0.75rem 1rem;
            }

            .logo {
                font-size: 1.25rem;
            }

            .nav-menu {
                gap: 0.25rem;
            }

            .nav-btn {
                padding: 0.5rem 0.75rem;
                font-size: 0.8rem;
            }

            .hero {
                padding: 3rem 0;
            }

            .hero-title {
                font-size: 2.5rem;
            }

            .features-grid {
                grid-template-columns: 1fr;
                gap: 1.5rem;
            }

            .materials-grid {
                grid-template-columns: 1fr;
            }

            .game-canvas {
                height: 500px;
                max-width: 90vw;
            }

            .road {
                width: 280px;
            }

            .mobile-controls {
                display: grid;
            }

            .game-stats {
                gap: 2rem;
            }

            .car, .obstacle {
                width: 40px;
                height: 70px;
            }

            .car.lane-left {
                left: 38%;
            }

            .car.lane-right {
                left: 62%;
            }

            .obstacle.lane-left {
                left: 38%;
            }

            .obstacle.lane-right {
                left: 62%;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 0 1rem;
            }

            .hero-title {
                font-size: 2rem;
            }

            .product-3d {
                width: 250px;
                height: 320px;
            }

            .game-canvas {
                height: 450px;
            }

            .road {
                width: 250px;
            }

            .car, .obstacle {
                width: 35px;
                height: 60px;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading" id="loading">
        <div class="loading-spinner"></div>
        <div class="loading-text">Cargando BrightWay...</div>
    </div>

    <!-- Navigation -->
    <nav>
        <div class="nav-container">
            <div class="logo">
                <div class="logo-icon">💡</div>
                BrightWay
            </div>
            <div class="nav-menu">
                <button class="nav-btn active" data-section="description">Descripción</button>
                <button class="nav-btn" data-section="materials">Materiales</button>
                <button class="nav-btn" data-section="game">Minijuego</button>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main>
        <!-- Description Section -->
        <section id="description" class="section active">
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
                    <div class="product-3d">
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
                            <p class="feature-description">Sistema de LEDs de alta eficiencia con sensor de movimiento para máxima visibilidad nocturna.</p>
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
        </section>

        <!-- Materials Section -->
        <section id="materials" class="section">
            <div class="container">
                <div class="hero">
                    <h1 class="hero-title">Materiales</h1>
                    <p class="hero-subtitle">Componentes del Sistema BrightWay</p>
                </div>
                
                <div class="materials-grid" id="materialsGrid">
                    <!-- Materials will be loaded dynamically -->
                </div>
            </div>
        </section>

        <!-- Enhanced Game Section -->
        <section id="game" class="section">
            <div class="container">
                <div class="game">
                    <div class="game-container">
                        <h1 class="hero-title">BrightWay</h1>
                        <p class="hero-subtitle">Conduce en la oscuridad y activa el BrightWay</p>

                        <div class="game-stats">
                            <div class="stat">
                                <div class="stat-label">Puntos</div>
                                <div class="stat-value" id="score">0</div>
                            </div>
                            <div class="stat">
                                <div class="stat-label">Récord</div>
                                <div class="stat-value" id="highScore">0</div>
                            </div>
                            <div class="stat">
                                <div class="stat-label">Vidas</div>
                                <div class="stat-value" id="lives">3</div>
                            </div>
                        </div>
                        
                        <div class="game-canvas" id="gameCanvas">
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
                            <div class="game-over" id="gameOver">
                                <h3>¡Juego Terminado!</h3>
                                <div class="final-score">Puntuación: <span id="finalScore">0</span></div>
                                <button class="btn" onclick="resetGame()">Jugar de Nuevo</button>
                            </div>
                        </div>

                        <div class="mobile-controls" id="mobileControls">
                            <button class="control-btn" id="leftBtn">← Izq</button>
                            <button class="control-btn" id="lightBtn">💡 Luz</button>
                            <button class="control-btn" id="rightBtn">Der →</button>
                        </div>
                        
                        <div class="game-controls">
                            <button class="btn" id="startBtn">Iniciar Juego</button>
                            <button class="btn btn-secondary" id="pauseBtn" disabled>Pausar</button>
                        </div>

                        <div class="instructions">
                            <h4>Cómo Jugar:</h4>
                            <p><strong>Objetivo:</strong> Conduce tu auto esquivando obstáculos que caen desde arriba y activa el BrightWay para iluminar el camino.</p>
                            <p><strong>Controles PC:</strong> Flechas ← → para cambiar de carril, Espacio para activar BrightWay</p>
                            <p><strong>Controles Móvil:</strong> Usa los botones en pantalla</p>
                            <p><strong>Puntuación:</strong> Ganas puntos por tiempo y por activar el BrightWay. ¡La luz te ayuda a ver mejor!</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-logo">
                <div class="logo-icon">💡</div>
                <span class="company-name">BrightWay Technologies</span>
            </div>
            <div class="creators">
                Desarrollado por: <strong>Pablo Nicolás García Huerta</strong> y <strong>Ángel Antonio Ruiz García</strong>
            </div>
            <div class="university">Universidad Autónoma de Querétaro - Facultad de Ingeniería</div>
            <div class="copyright">
                © 2024 BrightWay Technologies. Todos los derechos reservados.
            </div>
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

        // App Initialization
        document.addEventListener('DOMContentLoaded', function() {
            // Hide loading screen
            setTimeout(() => {
                document.getElementById('loading').classList.add('hidden');
            }, 1500);

            // Load materials
            loadMaterials();
            
            // Initialize navigation
            initNavigation();
            
            // Initialize game
            initGame();

            // Show mobile controls on mobile devices
            if (window.innerWidth <= 768) {
                document.getElementById('mobileControls').style.display = 'grid';
            }
        });

        // Navigation System
        function initNavigation() {
            const navBtns = document.querySelectorAll('.nav-btn');
            const sections = document.querySelectorAll('.section');

            navBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const targetSection = btn.dataset.section;
                    
                    // Update nav active state
                    navBtns.forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    
                    // Update section visibility
                    sections.forEach(section => {
                        section.classList.remove('active');
                        if (section.id === targetSection) {
                            setTimeout(() => section.classList.add('active'), 50);
                        }
                    });
                });
            });
        }

        // Load Materials
        function loadMaterials() {
            const materialsGrid = document.getElementById('materialsGrid');
            
            materials.forEach(material => {
                const card = document.createElement('div');
                card.className = 'material-card';
                card.innerHTML = `
                    <div class="material-header">
                        <div class="material-number">${material.id}</div>
                        <div>
                            <h3 class="material-name">${material.name}</h3>
                        </div>
                    </div>
                    <p class="material-description">${material.description}</p>
                    <div class="material-footer">
                        <span class="material-price">${material.price}</span>
                        <span class="material-quantity">${material.quantity}</span>
                    </div>
                `;
                materialsGrid.appendChild(card);
            });
        }

        // Enhanced Game Variables - From brightway_game_only.html
        let gameState = {
            running: false,
            paused: false,
            score: 0,
            lives: 3,
            highScore: 0,
            carLane: 'left', // 'left' or 'right'
            brightwayActive: false,
            obstacles: [],
            gameSpeed: 3,
            obstacleSpawnRate: 100,
            frameCounter: 0
        };

        let gameElements = {};
        let gameLoop = null;

        // Enhanced Game Initialization
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
                startBtn: document.getElementById('startBtn'),
                pauseBtn: document.getElementById('pauseBtn')
            };

            gameState.highScore = 0;
            gameElements.highScore.textContent = gameState.highScore;

            setupEventListeners();
        }

        function setupEventListeners() {
            // Keyboard controls
            document.addEventListener('keydown', handleKeyDown);
            
            // Button controls
            gameElements.startBtn.addEventListener('click', startGame);
            gameElements.pauseBtn.addEventListener('click', togglePause);
            
            // Mobile controls
            document.getElementById('leftBtn').addEventListener('click', () => changeLane('left'));
            document.getElementById('rightBtn').addEventListener('click', () => changeLane('right'));
            document.getElementById('lightBtn').addEventListener('click', () => activateBrightWay());
            
            // Click on BrightWay post
            gameElements.brightwayPost.addEventListener('click', activateBrightWay);
        }

        function handleKeyDown(e) {
            if (!gameState.running || gameState.paused) return;
            
            switch(e.key) {
                case 'ArrowLeft':
                    e.preventDefault();
                    changeLane('left');
                    break;
                case 'ArrowRight':
                    e.preventDefault();
                    changeLane('right');
                    break;
                case ' ':
                    e.preventDefault();
                    activateBrightWay();
                    break;
            }
        }

        function startGame() {
            if (gameState.running) {
                resetGame();
                return;
            }

            gameState = {
                ...gameState,
                running: true,
                paused: false,
                score: 0,
                lives: 3,
                carLane: 'left',
                brightwayActive: false,
                obstacles: [],
                gameSpeed: 3,
                obstacleSpawnRate: 100,
                frameCounter: 0
            };

            updateUI();
            gameElements.startBtn.textContent = 'Reiniciar';
            gameElements.pauseBtn.disabled = false;
            gameElements.gameOver.classList.remove('show');
            
            clearObstacles();
            
            gameElements.car.className = 'car';
            gameElements.lightEffect.classList.remove('active');
            gameElements.carLights.style.opacity = '0.4';
            gameElements.gameCanvas.style.background = 'var(--darker)';

            gameLoop = setInterval(updateGame, 1000 / 60); // 60 FPS
        }

        function updateGame() {
            if (!gameState.running || gameState.paused) return;

            gameState.frameCounter++;

            gameState.score += gameState.brightwayActive ? 3 : 1;
            gameElements.score.textContent = Math.floor(gameState.score / 60);

            if (gameState.frameCounter % gameState.obstacleSpawnRate === 0) {
                spawnObstacle();
            }

            updateObstacles();
            checkCollisions();

            if (gameState.frameCounter % 1800 === 0) { // Every 30 seconds
                gameState.gameSpeed = Math.min(gameState.gameSpeed + 0.5, 8);
                gameState.obstacleSpawnRate = Math.max(gameState.obstacleSpawnRate - 8, 50);
            }
        }

        function spawnObstacle() {
            const obstacle = document.createElement('div');
            obstacle.className = 'obstacle';
            
            const availableLanes = ['left', 'right'];
            const recentObstacles = gameState.obstacles.filter(obs => obs.y < 150);
            
            let lane;
            if (recentObstacles.length > 0) {
                const existingLane = recentObstacles[0].lane;
                lane = existingLane === 'left' ? 'right' : 'left';
            } else {
                lane = availableLanes[Math.floor(Math.random() * availableLanes.length)];
            }
            
            obstacle.classList.add('lane-' + lane);
            gameElements.gameCanvas.appendChild(obstacle);
            gameState.obstacles.push({ 
                element: obstacle, 
                lane: lane, 
                passed: false, 
                y: 0,
                hit: false
            });
        }

        function updateObstacles() {
            gameState.obstacles = gameState.obstacles.filter(obs => {
                obs.y += gameState.gameSpeed;
                obs.element.style.top = obs.y + 'px';
                
                if (obs.y > gameElements.gameCanvas.offsetHeight + 100) {
                    obs.element.remove();
                    return false;
                }
                
                if (!obs.passed && obs.y > gameElements.gameCanvas.offsetHeight - 200) {
                    obs.passed = true;
                    gameState.score += 30;
                }
                
                return true;
            });
        }

        function checkCollisions() {
            const carY = gameElements.gameCanvas.offsetHeight - 170;
            
            gameState.obstacles.forEach(obs => {
                if (obs.hit) return;
                
                if (obs.lane === gameState.carLane && 
                    obs.y >= carY - 40 && obs.y <= carY + 40) {
                    
                    obs.hit = true;
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
            
            gameState.score += 150;
            
            gameState.obstacles.forEach(obs => {
                obs.element.style.background = 'var(--danger)';
                obs.element.style.boxShadow = '0 0 15px var(--danger)';
            });
            
            setTimeout(() => {
                gameState.brightwayActive = false;
                gameElements.lightEffect.classList.remove('active');
                gameElements.carLights.style.opacity = '0.4';
                gameElements.gameCanvas.style.background = 'var(--darker)';
                
                gameState.obstacles.forEach(obs => {
                    obs.element.style.background = 'var(--gray-600)';
                    obs.element.style.boxShadow = '0 5px 15px rgba(0, 0, 0, 0.5)';
                });
            }, 5000);
        }

        function hitObstacle() {
            gameState.lives--;
            gameElements.lives.textContent = gameState.lives;
            
            gameElements.car.style.background = 'linear-gradient(0deg, var(--danger), #DC2626)';
            gameElements.car.style.boxShadow = '0 0 25px var(--danger)';
            
            setTimeout(() => {
                gameElements.car.style.background = 'linear-gradient(0deg, var(--blue), #1E40AF)';
                gameElements.car.style.boxShadow = '0 5px 20px rgba(59, 130, 246, 0.4)';
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
            }
            
            gameElements.finalScore.textContent = finalScore;
            gameElements.gameOver.classList.add('show');
            
            gameElements.startBtn.textContent = 'Iniciar Juego';
            gameElements.pauseBtn.disabled = true;
            gameElements.pauseBtn.textContent = 'Pausar';
        }

        function resetGame() {
            if (gameLoop) clearInterval(gameLoop);
            gameState.running = false;
            clearObstacles();
            gameElements.gameOver.classList.remove('show');
            startGame();
        }

        function clearObstacles() {
            gameState.obstacles.forEach(obs => obs.element.remove());
            gameState.obstacles = [];
        }

        function updateUI() {
            gameElements.score.textContent = Math.floor(gameState.score / 60);
            gameElements.lives.textContent = gameState.lives;
        }
    </script>
</body>
</html>
