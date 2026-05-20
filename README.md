[limeup-app.html](https://github.com/user-attachments/files/28041325/limeup-app.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>LimeUp - Desenvolvimento Pessoal</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&family=DM+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #00C462;
            --white: #FFFFFF;
            --gray: #D3D3D3;
            --dark: #1A1A1A;
            --light-gray: #F5F5F5;
            --shadow: rgba(0, 196, 98, 0.15);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'DM Sans', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--light-gray);
            overflow-x: hidden;
            position: relative;
            min-height: 100vh;
        }

        /* Login Screen */
        .login-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: linear-gradient(135deg, #00C462 0%, #00A055 100%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 1;
            transition: opacity 0.5s ease;
        }

        .login-screen.hidden {
            opacity: 0;
            pointer-events: none;
        }

        .login-logo {
            font-family: 'Outfit', sans-serif;
            font-size: 56px;
            font-weight: 800;
            color: var(--white);
            margin-bottom: 8px;
            letter-spacing: -2px;
            animation: fadeInUp 0.8s ease;
        }

        .login-tagline {
            color: rgba(255, 255, 255, 0.9);
            font-size: 16px;
            margin-bottom: 60px;
            font-weight: 400;
            animation: fadeInUp 0.8s ease 0.1s both;
        }

        .login-form {
            width: 85%;
            max-width: 360px;
            animation: fadeInUp 0.8s ease 0.2s both;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .login-input {
            width: 100%;
            padding: 18px 20px;
            border: none;
            border-radius: 16px;
            font-size: 16px;
            font-family: 'DM Sans', sans-serif;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .login-input:focus {
            outline: none;
            background: var(--white);
            transform: translateY(-2px);
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
        }

        .login-button {
            width: 100%;
            padding: 18px;
            border: none;
            border-radius: 16px;
            font-size: 17px;
            font-weight: 700;
            font-family: 'DM Sans', sans-serif;
            background: var(--white);
            color: var(--primary);
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 12px;
        }

        .login-button:active {
            transform: scale(0.98);
        }

        /* Main App Container */
        .app-container {
            display: none;
            padding-bottom: 80px;
        }

        .app-container.active {
            display: block;
        }

        /* Header */
        .app-header {
            background: var(--white);
            padding: 50px 20px 20px;
            box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
        }

        .header-title {
            font-family: 'Outfit', sans-serif;
            font-size: 32px;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 4px;
        }

        .header-subtitle {
            color: #666;
            font-size: 14px;
        }

        /* Content Sections */
        .content-section {
            display: none;
            padding: 20px;
            animation: fadeIn 0.4s ease;
        }

        .content-section.active {
            display: block;
        }

        /* Home - Fitness Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
            margin-bottom: 24px;
        }

        .stat-card {
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
            position: relative;
            overflow: hidden;
            transition: transform 0.3s ease;
        }

        .stat-card:active {
            transform: scale(0.97);
        }

        .stat-card.large {
            grid-column: 1 / -1;
        }

        .stat-icon {
            width: 48px;
            height: 48px;
            background: linear-gradient(135deg, var(--primary), #00A055);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            margin-bottom: 12px;
        }

        .stat-label {
            color: #666;
            font-size: 13px;
            margin-bottom: 6px;
            font-weight: 500;
        }

        .stat-value {
            font-size: 28px;
            font-weight: 700;
            color: var(--dark);
            font-family: 'Outfit', sans-serif;
        }

        .stat-unit {
            font-size: 14px;
            color: #999;
            font-weight: 400;
        }

        .progress-ring {
            width: 100%;
            height: 120px;
            display: flex;
            align-items: center;
            justify-content: space-around;
            margin-top: 12px;
        }

        .ring {
            width: 90px;
            height: 90px;
            border-radius: 50%;
            background: conic-gradient(var(--primary) 0deg 250deg, var(--gray) 250deg 360deg);
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }

        .ring-inner {
            width: 70px;
            height: 70px;
            background: var(--white);
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .ring-value {
            font-size: 20px;
            font-weight: 700;
            color: var(--dark);
        }

        .ring-label {
            font-size: 10px;
            color: #999;
            margin-top: 2px;
        }

        /* Conquistas */
        .achievements {
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
        }

        .achievement-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 16px;
            color: var(--dark);
        }

        .achievement-list {
            display: flex;
            gap: 12px;
            overflow-x: auto;
            padding-bottom: 8px;
        }

        .achievement-badge {
            min-width: 80px;
            text-align: center;
        }

        .badge-icon {
            width: 64px;
            height: 64px;
            background: linear-gradient(135deg, var(--primary), #00A055);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            margin: 0 auto 8px;
            box-shadow: 0 4px 12px var(--shadow);
        }

        .badge-name {
            font-size: 11px;
            color: #666;
        }

        /* Comunidades */
        .category-section {
            margin-bottom: 32px;
        }

        .category-title {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 16px;
            color: var(--dark);
        }

        .community-scroll {
            display: flex;
            gap: 16px;
            overflow-x: auto;
            padding-bottom: 12px;
            margin-bottom: 20px;
        }

        .community-card {
            min-width: 280px;
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
            transition: transform 0.3s ease;
        }

        .community-card:active {
            transform: scale(0.97);
        }

        .community-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 12px;
        }

        .community-avatar {
            width: 48px;
            height: 48px;
            background: linear-gradient(135deg, var(--primary), #00A055);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }

        .community-info h3 {
            font-size: 16px;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 2px;
        }

        .community-members {
            font-size: 12px;
            color: #999;
        }

        .community-description {
            font-size: 14px;
            color: #666;
            line-height: 1.5;
            margin-bottom: 12px;
        }

        .join-button {
            width: 100%;
            padding: 12px;
            border: 2px solid var(--primary);
            background: transparent;
            color: var(--primary);
            border-radius: 12px;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .join-button.joined {
            background: var(--primary);
            color: var(--white);
        }

        /* Publicar */
        .publish-container {
            background: var(--white);
            border-radius: 20px;
            padding: 24px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
        }

        .photo-upload {
            width: 100%;
            height: 200px;
            border: 3px dashed var(--gray);
            border-radius: 16px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            background: var(--light-gray);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .photo-upload:active {
            transform: scale(0.98);
        }

        .upload-icon {
            font-size: 48px;
            margin-bottom: 8px;
            opacity: 0.5;
        }

        .upload-text {
            color: #999;
            font-size: 14px;
        }

        .caption-input {
            width: 100%;
            min-height: 120px;
            padding: 16px;
            border: 2px solid var(--gray);
            border-radius: 16px;
            font-family: 'DM Sans', sans-serif;
            font-size: 15px;
            resize: vertical;
            margin-bottom: 20px;
        }

        .caption-input:focus {
            outline: none;
            border-color: var(--primary);
        }

        .publish-button {
            width: 100%;
            padding: 18px;
            background: var(--primary);
            color: var(--white);
            border: none;
            border-radius: 16px;
            font-size: 17px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .publish-button:active {
            transform: scale(0.98);
        }

        /* Eventos */
        .event-card {
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 16px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
            transition: transform 0.3s ease;
        }

        .event-card:active {
            transform: scale(0.98);
        }

        .event-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }

        .event-type {
            background: var(--primary);
            color: var(--white);
            padding: 6px 12px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 700;
            text-transform: uppercase;
        }

        .event-date {
            font-size: 13px;
            color: #999;
            font-weight: 600;
        }

        .event-title {
            font-size: 18px;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 8px;
        }

        .event-description {
            font-size: 14px;
            color: #666;
            line-height: 1.5;
            margin-bottom: 12px;
        }

        .event-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .event-location {
            font-size: 13px;
            color: #999;
        }

        .event-participants {
            font-size: 13px;
            color: var(--primary);
            font-weight: 600;
        }

        /* Perfil */
        .profile-header {
            background: var(--white);
            border-radius: 20px;
            padding: 24px;
            margin-bottom: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
            text-align: center;
        }

        .profile-avatar {
            width: 100px;
            height: 100px;
            background: linear-gradient(135deg, var(--primary), #00A055);
            border-radius: 50%;
            margin: 0 auto 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 40px;
            box-shadow: 0 8px 24px var(--shadow);
        }

        .profile-name {
            font-size: 24px;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 8px;
        }

        .profile-level {
            display: inline-block;
            background: linear-gradient(135deg, var(--primary), #00A055);
            color: var(--white);
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 700;
            margin-bottom: 20px;
        }

        .profile-stats {
            display: flex;
            justify-content: space-around;
            padding-top: 20px;
            border-top: 1px solid var(--gray);
        }

        .profile-stat {
            text-align: center;
        }

        .profile-stat-value {
            font-size: 22px;
            font-weight: 700;
            color: var(--dark);
            display: block;
        }

        .profile-stat-label {
            font-size: 12px;
            color: #999;
            margin-top: 4px;
        }

        .recent-achievements {
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
        }

        .section-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 16px;
            color: var(--dark);
        }

        .achievement-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
        }

        .mini-badge {
            width: 100%;
            aspect-ratio: 1;
            background: linear-gradient(135deg, var(--primary), #00A055);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            box-shadow: 0 4px 12px var(--shadow);
        }

        .photos-grid {
            background: var(--white);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
        }

        .photo-grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
        }

        .photo-item {
            aspect-ratio: 1;
            background: linear-gradient(135deg, var(--gray), #E8E8E8);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            opacity: 0.6;
        }

        /* Navigation Bar */
        .nav-bar {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: var(--white);
            padding: 12px 0 max(12px, env(safe-area-inset-bottom));
            display: flex;
            justify-content: space-around;
            box-shadow: 0 -2px 16px rgba(0, 0, 0, 0.08);
            z-index: 100;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 12px;
            transition: all 0.3s ease;
            color: #999;
        }

        .nav-item.active {
            color: var(--primary);
            background: rgba(0, 196, 98, 0.1);
        }

        .nav-icon {
            font-size: 24px;
            transition: transform 0.3s ease;
        }

        .nav-item.active .nav-icon {
            transform: scale(1.1);
        }

        .nav-label {
            font-size: 11px;
            font-weight: 600;
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            display: none;
        }

        .community-scroll::-webkit-scrollbar,
        .achievement-list::-webkit-scrollbar {
            height: 4px;
        }

        .community-scroll::-webkit-scrollbar-track,
        .achievement-list::-webkit-scrollbar-track {
            background: var(--light-gray);
            border-radius: 2px;
        }

        .community-scroll::-webkit-scrollbar-thumb,
        .achievement-list::-webkit-scrollbar-thumb {
            background: var(--gray);
            border-radius: 2px;
        }
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div class="login-screen" id="loginScreen">
        <div class="login-logo">LimeUp</div>
        <div class="login-tagline">Evolua a cada dia</div>
        <form class="login-form" id="loginForm">
            <div class="input-group">
                <input type="text" class="login-input" placeholder="Usuário" id="username" required>
            </div>
            <div class="input-group">
                <input type="password" class="login-input" placeholder="Senha" id="password" required>
            </div>
            <button type="submit" class="login-button">Entrar</button>
        </form>
    </div>

    <!-- Main App -->
    <div class="app-container" id="appContainer">
        <!-- Header -->
        <div class="app-header">
            <div class="header-title" id="headerTitle">Home</div>
            <div class="header-subtitle" id="headerSubtitle">Bem-vindo de volta!</div>
        </div>

        <!-- Home Content -->
        <div class="content-section active" id="homeContent">
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-icon">🏃</div>
                    <div class="stat-label">Meta de Movimento</div>
                    <div class="stat-value">420<span class="stat-unit">/500 min</span></div>
                </div>
                <div class="stat-card">
                    <div class="stat-icon">📍</div>
                    <div class="stat-label">Meta de Distância</div>
                    <div class="stat-value">8.5<span class="stat-unit">/10 km</span></div>
                </div>
                <div class="stat-card">
                    <div class="stat-icon">🔥</div>
                    <div class="stat-label">Meta de Calorias</div>
                    <div class="stat-value">1,840<span class="stat-unit">/2,000 cal</span></div>
                </div>
                <div class="stat-card">
                    <div class="stat-icon">⚡</div>
                    <div class="stat-label">Ritmo de Corrida</div>
                    <div class="stat-value">5:32<span class="stat-unit">/km</span></div>
                </div>
                <div class="stat-card large">
                    <div class="stat-label">Ritmo de Caminhada</div>
                    <div class="stat-value">12:15<span class="stat-unit">/km</span></div>
                    <div class="progress-ring">
                        <div class="ring">
                            <div class="ring-inner">
                                <div class="ring-value">84%</div>
                                <div class="ring-label">META</div>
                            </div>
                        </div>
                        <div class="ring">
                            <div class="ring-inner">
                                <div class="ring-value">85%</div>
                                <div class="ring-label">DIST.</div>
                            </div>
                        </div>
                        <div class="ring">
                            <div class="ring-inner">
                                <div class="ring-value">92%</div>
                                <div class="ring-label">CAL.</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="achievements">
                <div class="achievement-title">Conquistas Recentes</div>
                <div class="achievement-list">
                    <div class="achievement-badge">
                        <div class="badge-icon">🏆</div>
                        <div class="badge-name">Primeira Meta</div>
                    </div>
                    <div class="achievement-badge">
                        <div class="badge-icon">🔥</div>
                        <div class="badge-name">Sequência 7 Dias</div>
                    </div>
                    <div class="achievement-badge">
                        <div class="badge-icon">⭐</div>
                        <div class="badge-name">100km Total</div>
                    </div>
                    <div class="achievement-badge">
                        <div class="badge-icon">💪</div>
                        <div class="badge-name">Maratonista</div>
                    </div>
                    <div class="achievement-badge">
                        <div class="badge-icon">🎯</div>
                        <div class="badge-name">Meta Perfeita</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Comunidades Content -->
        <div class="content-section" id="comunidadesContent">
            <div class="category-section">
                <div class="category-title">🏃 Corrida & Caminhada</div>
                <div class="community-scroll">
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🏃</div>
                            <div class="community-info">
                                <h3>Corredores SP</h3>
                                <div class="community-members">12.5k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Comunidade para corredores de São Paulo. Treinos, dicas e eventos semanais.</div>
                        <button class="join-button">Participar</button>
                    </div>
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🌅</div>
                            <div class="community-info">
                                <h3>Caminhadas Matinais</h3>
                                <div class="community-members">8.2k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Para quem ama começar o dia com uma boa caminhada ao ar livre.</div>
                        <button class="join-button">Participar</button>
                    </div>
                </div>
            </div>

            <div class="category-section">
                <div class="category-title">📚 Leitura & Conhecimento</div>
                <div class="community-scroll">
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">📖</div>
                            <div class="community-info">
                                <h3>Clube do Livro</h3>
                                <div class="community-members">15.3k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Encontros mensais para discutir livros e compartilhar descobertas literárias.</div>
                        <button class="join-button">Participar</button>
                    </div>
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🎓</div>
                            <div class="community-info">
                                <h3>Aprendizes Tech</h3>
                                <div class="community-members">22.1k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Comunidade para quem está aprendendo programação e tecnologia.</div>
                        <button class="join-button">Participar</button>
                    </div>
                </div>
            </div>

            <div class="category-section">
                <div class="category-title">🎮 Gaming & Esports</div>
                <div class="community-scroll">
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🎮</div>
                            <div class="community-info">
                                <h3>Gamers Brasil</h3>
                                <div class="community-members">45.7k membros</div>
                            </div>
                        </div>
                        <div class="community-description">A maior comunidade de gamers brasileiros. Campeonatos e eventos online.</div>
                        <button class="join-button">Participar</button>
                    </div>
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🏆</div>
                            <div class="community-info">
                                <h3>Liga Competitiva</h3>
                                <div class="community-members">18.9k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Para jogadores competitivos de diversos esports e torneios.</div>
                        <button class="join-button">Participar</button>
                    </div>
                </div>
            </div>

            <div class="category-section">
                <div class="category-title">🏔️ Aventura & Natureza</div>
                <div class="community-scroll">
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">⛰️</div>
                            <div class="community-info">
                                <h3>Trilheiros</h3>
                                <div class="community-members">9.8k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Exploradores de trilhas e montanhas. Aventuras todo fim de semana.</div>
                        <button class="join-button">Participar</button>
                    </div>
                    <div class="community-card">
                        <div class="community-header">
                            <div class="community-avatar">🏕️</div>
                            <div class="community-info">
                                <h3>Acampantes</h3>
                                <div class="community-members">6.4k membros</div>
                            </div>
                        </div>
                        <div class="community-description">Amantes de camping e experiências ao ar livre em conexão com a natureza.</div>
                        <button class="join-button">Participar</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Publicar Content -->
        <div class="content-section" id="publicarContent">
            <div class="publish-container">
                <div class="photo-upload">
                    <div class="upload-icon">📸</div>
                    <div class="upload-text">Adicionar foto</div>
                </div>
                <textarea class="caption-input" placeholder="Escreva uma legenda..."></textarea>
                <button class="publish-button">Publicar</button>
            </div>
        </div>

        <!-- Eventos Content -->
        <div class="content-section" id="eventosContent">
            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Corrida</div>
                    <div class="event-date">25 Mai</div>
                </div>
                <div class="event-title">Maratona de São Paulo 2026</div>
                <div class="event-description">42km pelas principais avenidas da cidade. Inscrições abertas até dia 20!</div>
                <div class="event-footer">
                    <div class="event-location">📍 Ibirapuera</div>
                    <div class="event-participants">2.4k participantes</div>
                </div>
            </div>

            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Palestra</div>
                    <div class="event-date">28 Mai</div>
                </div>
                <div class="event-title">Desenvolvimento Pessoal e Carreira</div>
                <div class="event-description">Workshop sobre como construir uma carreira sólida e alcançar seus objetivos.</div>
                <div class="event-footer">
                    <div class="event-location">📍 Online</div>
                    <div class="event-participants">850 participantes</div>
                </div>
            </div>

            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Gaming</div>
                    <div class="event-date">30 Mai</div>
                </div>
                <div class="event-title">Campeonato de E-Sports</div>
                <div class="event-description">Torneio online com premiação total de R$ 10.000. Várias categorias disponíveis.</div>
                <div class="event-footer">
                    <div class="event-location">📍 Online</div>
                    <div class="event-participants">3.2k participantes</div>
                </div>
            </div>

            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Leitura</div>
                    <div class="event-date">02 Jun</div>
                </div>
                <div class="event-title">Encontro do Clube do Livro</div>
                <div class="event-description">Discussão sobre "Sapiens" de Yuval Noah Harari. Café e bate-papo.</div>
                <div class="event-footer">
                    <div class="event-location">📍 Vila Madalena</div>
                    <div class="event-participants">45 participantes</div>
                </div>
            </div>

            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Trilha</div>
                    <div class="event-date">05 Jun</div>
                </div>
                <div class="event-title">Trilha Pico do Jaraguá</div>
                <div class="event-description">Trilha de nível moderado até o ponto mais alto de SP. Saída às 6h.</div>
                <div class="event-footer">
                    <div class="event-location">📍 Parque Jaraguá</div>
                    <div class="event-participants">28 participantes</div>
                </div>
            </div>

            <div class="event-card">
                <div class="event-header">
                    <div class="event-type">Fitness</div>
                    <div class="event-date">08 Jun</div>
                </div>
                <div class="event-title">Aula de Yoga ao Ar Livre</div>
                <div class="event-description">Sessão especial de yoga no parque. Traga seu mat e aproveite!</div>
                <div class="event-footer">
                    <div class="event-location">📍 Parque do Povo</div>
                    <div class="event-participants">120 participantes</div>
                </div>
            </div>
        </div>

        <!-- Perfil Content -->
        <div class="content-section" id="perfilContent">
            <div class="profile-header">
                <div class="profile-avatar">👤</div>
                <div class="profile-name">Usuário Teste</div>
                <div class="profile-level">Nível 12 - Guerreiro</div>
                <div class="profile-stats">
                    <div class="profile-stat">
                        <span class="profile-stat-value">1.2k</span>
                        <span class="profile-stat-label">Seguidores</span>
                    </div>
                    <div class="profile-stat">
                        <span class="profile-stat-value">856</span>
                        <span class="profile-stat-label">Seguindo</span>
                    </div>
                    <div class="profile-stat">
                        <span class="profile-stat-value">42</span>
                        <span class="profile-stat-label">Posts</span>
                    </div>
                </div>
            </div>

            <div class="recent-achievements">
                <div class="section-title">Últimas Conquistas</div>
                <div class="achievement-grid">
                    <div class="mini-badge">🏆</div>
                    <div class="mini-badge">🔥</div>
                    <div class="mini-badge">⭐</div>
                    <div class="mini-badge">💪</div>
                    <div class="mini-badge">🎯</div>
                    <div class="mini-badge">🚀</div>
                    <div class="mini-badge">⚡</div>
                    <div class="mini-badge">👑</div>
                </div>
            </div>

            <div class="photos-grid">
                <div class="section-title">Fotos Publicadas</div>
                <div class="photo-grid-container">
                    <div class="photo-item">📸</div>
                    <div class="photo-item">🏃</div>
                    <div class="photo-item">🌄</div>
                    <div class="photo-item">📚</div>
                    <div class="photo-item">🎮</div>
                    <div class="photo-item">⛰️</div>
                    <div class="photo-item">💪</div>
                    <div class="photo-item">🔥</div>
                    <div class="photo-item">🎯</div>
                </div>
            </div>
        </div>

        <!-- Navigation Bar -->
        <div class="nav-bar">
            <div class="nav-item active" data-section="home">
                <div class="nav-icon">🏠</div>
                <div class="nav-label">Home</div>
            </div>
            <div class="nav-item" data-section="comunidades">
                <div class="nav-icon">👥</div>
                <div class="nav-label">Comunidade</div>
            </div>
            <div class="nav-item" data-section="publicar">
                <div class="nav-icon">➕</div>
                <div class="nav-label">Publicar</div>
            </div>
            <div class="nav-item" data-section="eventos">
                <div class="nav-icon">📅</div>
                <div class="nav-label">Eventos</div>
            </div>
            <div class="nav-item" data-section="perfil">
                <div class="nav-icon">👤</div>
                <div class="nav-label">Perfil</div>
            </div>
        </div>
    </div>

    <script>
        // Login functionality
        const loginForm = document.getElementById('loginForm');
        const loginScreen = document.getElementById('loginScreen');
        const appContainer = document.getElementById('appContainer');

        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (username === 'Teste' && password === 'Teste') {
                loginScreen.classList.add('hidden');
                setTimeout(() => {
                    appContainer.classList.add('active');
                }, 500);
            } else {
                alert('Credenciais inválidas! Use "Teste" para usuário e senha.');
            }
        });

        // Navigation functionality
        const navItems = document.querySelectorAll('.nav-item');
        const contentSections = document.querySelectorAll('.content-section');
        const headerTitle = document.getElementById('headerTitle');
        const headerSubtitle = document.getElementById('headerSubtitle');

        const sectionConfig = {
            home: { title: 'Home', subtitle: 'Bem-vindo de volta!' },
            comunidades: { title: 'Comunidades', subtitle: 'Encontre seu grupo' },
            publicar: { title: 'Publicar', subtitle: 'Compartilhe seu momento' },
            eventos: { title: 'Eventos', subtitle: 'Próximas atividades' },
            perfil: { title: 'Perfil', subtitle: 'Suas conquistas' }
        };

        navItems.forEach(item => {
            item.addEventListener('click', () => {
                const section = item.dataset.section;

                // Update active nav item
                navItems.forEach(nav => nav.classList.remove('active'));
                item.classList.add('active');

                // Update content sections
                contentSections.forEach(content => content.classList.remove('active'));
                document.getElementById(`${section}Content`).classList.add('active');

                // Update header
                headerTitle.textContent = sectionConfig[section].title;
                headerSubtitle.textContent = sectionConfig[section].subtitle;

                // Scroll to top
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });
        });

        // Join/Leave community buttons
        document.addEventListener('click', (e) => {
            if (e.target.classList.contains('join-button')) {
                e.target.classList.toggle('joined');
                e.target.textContent = e.target.classList.contains('joined') ? 'Participando' : 'Participar';
            }
        });

        // Photo upload interaction
        const photoUpload = document.querySelector('.photo-upload');
        photoUpload.addEventListener('click', () => {
            alert('Funcionalidade de upload de foto ainda não implementada nesta versão demo.');
        });

        // Publish button
        const publishButton = document.querySelector('.publish-button');
        publishButton.addEventListener('click', () => {
            const caption = document.querySelector('.caption-input').value;
            if (caption.trim()) {
                alert('Post publicado com sucesso! (Demo)');
                document.querySelector('.caption-input').value = '';
            } else {
                alert('Por favor, adicione uma legenda.');
            }
        });
    </script>
</body>
</html>
