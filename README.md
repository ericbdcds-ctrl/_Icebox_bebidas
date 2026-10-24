<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IceBox Bebidas — Tele-Entrega Zona Sul</title>
    <!-- Google Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-dark: #0a0e17;
            --card-bg: #131a2a;
            --neon-blue: #00f0ff;
            --neon-glow: rgba(0, 240, 255, 0.4);
            --neon-pink: #ff007f;
            --text-light: #f0f6fc;
            --text-gray: #8b949e;
            --success: #00e676;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
            user-select: none;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            overflow-x: hidden;
            position: relative;
            min-height: 100vh;
            padding-bottom: 80px;
        }

        /* Fundo Animado de Gelos e Garrafas */
        .floating-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .float-item {
            position: absolute;
            opacity: 0.15;
            animation: floatUp 12s infinite linear;
            filter: drop-shadow(0 0 8px var(--neon-blue));
        }

        @keyframes floatUp {
            0% {
                transform: translateY(105vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.2;
            }
            90% {
                opacity: 0.2;
            }
            100% {
                transform: translateY(-10vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* Top Notification Bar */
        .promo-bar {
            background: linear-gradient(90deg, #ff007f, #00f0ff);
            color: #000;
            font-weight: 800;
            text-align: center;
            padding: 8px;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.5);
            position: relative;
            z-index: 10;
        }

        /* Header / Navbar */
        header {
            background: rgba(19, 26, 42, 0.8);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(0, 240, 255, 0.2);
            padding: 15px 20px;
            position: sticky;
            top: 0;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
        }

        .logo-icon {
            font-size: 1.8rem;
            color: var(--neon-blue);
            text-shadow: 0 0 10px var(--neon-blue);
            animation: pulse 2s infinite alternate;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            100% { transform: scale(1.1); }
        }

        .logo-text {
            font-size: 1.5rem;
            font-weight: 900;
            letter-spacing: 1px;
            background: linear-gradient(45deg, #fff, var(--neon-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .header-actions {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .cart-btn {
            background: rgba(0, 240, 255, 0.1);
            border: 1px solid var(--neon-blue);
            color: var(--neon-blue);
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s;
            position: relative;
        }

        .cart-btn:hover {
            background: var(--neon-blue);
            color: #000;
            box-shadow: 0 0 15px var(--neon-glow);
        }

        .cart-count {
            background: var(--neon-pink);
            color: #fff;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75rem;
        }

        /* Main Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 5;
        }

        /* Banner Hero */
        .hero {
            text-align: center;
            padding: 30px 20px;
            background: radial-gradient(circle, rgba(0,240,255,0.1) 0%, rgba(10,14,23,0) 70%);
            border-radius: 15px;
            margin-bottom: 30px;
        }

        .hero h1 {
            font-size: 2.2rem;
            font-weight: 900;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
        }

        .hero p {
            color: var(--text-gray);
            font-size: 1rem;
        }

        /* Categories Filter */
        .categories {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding-bottom: 10px;
            margin-bottom: 30px;
            scrollbar-width: none;
        }

        .categories::-webkit-scrollbar {
            display: none;
        }

        .cat-btn {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: var(--text-light);
            padding: 10px 20px;
            border-radius: 25px;
            white-space: nowrap;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }

        .cat-btn.active, .cat-btn:hover {
            border-color: var(--neon-blue);
            color: var(--neon-blue);
            box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);
        }

        /* Section Title */
        .section-title {
            font-size: 1.4rem;
            font-weight: 800;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-left: 4px solid var(--neon-blue);
            padding-left: 10px;
        }

        /* Products Grid */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .product-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            overflow: hidden;
            transition: all 0.3s;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .product-card:hover {
            transform: translateY(-5px);
            border-color: rgba(0, 240, 255, 0.4);
            box-shadow: 0 5px 20px rgba(0, 240, 255, 0.15);
        }

        .product-img-container {
            width: 100%;
            height: 180px;
            background: rgba(0, 0, 0, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            position: relative;
        }

        .product-img {
            max-width: 80%;
            max-height: 80%;
            object-fit: contain;
            transition: transform 0.3s;
        }

        .product-card:hover .product-img {
            transform: scale(1.08);
        }

        .product-info {
            padding: 15px;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
        }

        .product-title {
            font-size: 1.05rem;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .product-desc {
            font-size: 0.8rem;
            color: var(--text-gray);
            margin-bottom: 12px;
            flex-grow: 1;
        }

        .flavor-selector {
            margin-bottom: 12px;
        }

        .flavor-selector label {
            display: block;
            font-size: 0.75rem;
            color: var(--neon-blue);
            font-weight: 600;
            margin-bottom: 4px;
        }

        .flavor-selector select {
            width: 100%;
            background: #0a0e17;
            color: #fff;
            border: 1px solid rgba(0, 240, 255, 0.3);
            padding: 6px 10px;
            border-radius: 8px;
            font-size: 0.85rem;
            outline: none;
        }

        .product-bottom {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }

        .product-price {
            font-size: 1.2rem;
            font-weight: 800;
            color: #fff;
        }

        .add-cart-btn {
            background: var(--neon-blue);
            color: #000;
            border: none;
            padding: 8px 12px;
            border-radius: 10px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .add-cart-btn:hover {
            box-shadow: 0 0 12px var(--neon-glow);
            transform: scale(1.05);
        }

        /* Offcanvas Cart Modal */
        .cart-modal {
            position: fixed;
            top: 0;
            right: -100%;
            width: 100%;
            max-width: 420px;
            height: 100%;
            background: var(--card-bg);
            box-shadow: -5px 0 25px rgba(0, 0, 0, 0.8);
            z-index: 200;
            transition: right 0.4s ease;
            display: flex;
            flex-direction: column;
            border-left: 1px solid rgba(0, 240, 255, 0.2);
        }

        .cart-modal.open {
            right: 0;
        }

        .cart-header {
            padding: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .cart-header h2 {
            font-size: 1.3rem;
            font-weight: 800;
            color: var(--neon-blue);
        }

        .close-cart {
            background: none;
            border: none;
            color: #fff;
            font-size: 1.5rem;
            cursor: pointer;
        }

        .cart-body {
            padding: 20px;
            flex-grow: 1;
            overflow-y: auto;
        }

        .cart-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(0, 0, 0, 0.2);
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 10px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .cart-item-details {
            flex-grow: 1;
        }

        .cart-item-title {
            font-size: 0.9rem;
            font-weight: 700;
        }

        .cart-item-sub {
            font-size: 0.75rem;
            color: var(--neon-blue);
        }

        .cart-item-price {
            font-weight: 700;
            margin-top: 2px;
        }

        .cart-item-actions {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .qty-btn {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            color: #fff;
            width: 24px;
            height: 24px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 700;
        }

        /* Racha Pix Calculator */
        .racha-pix {
            background: rgba(0, 240, 255, 0.05);
            border: 1px dashed var(--neon-blue);
            padding: 12px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .racha-pix h4 {
            font-size: 0.85rem;
            color: var(--neon-blue);
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .racha-inputs {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .racha-inputs input {
            width: 60px;
            background: #0a0e17;
            border: 1px solid rgba(0, 240, 255, 0.3);
            color: #fff;
            padding: 5px;
            border-radius: 5px;
            text-align: center;
        }

        .cart-footer {
            padding: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.3);
        }

        .cart-total-row {
            display: flex;
            justify-content: space-between;
            font-size: 1.1rem;
            font-weight: 800;
            margin-bottom: 15px;
        }

        .checkout-btn {
            width: 100%;
            background: var(--success);
            color: #000;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-weight: 800;
            font-size: 1rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.3s;
        }

        .checkout-btn:hover {
            box-shadow: 0 0 15px rgba(0, 230, 118, 0.5);
        }

        /* Overlay */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 150;
            display: none;
        }

        .overlay.active {
            display: block;
        }

        /* Modal ADM Secreto */
        .adm-modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            width: 90%;
            max-width: 500px;
            background: var(--card-bg);
            border: 2px solid var(--neon-blue);
            box-shadow: 0 0 30px var(--neon-glow);
            border-radius: 15px;
            padding: 25px;
            z-index: 300;
            display: none;
            opacity: 0;
            transition: all 0.3s;
        }

        .adm-modal.active {
            display: block;
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
        }

        .adm-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 10px;
        }

        .adm-header h3 {
            color: var(--neon-blue);
            font-weight: 800;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            font-size: 0.85rem;
            margin-bottom: 5px;
            color: var(--text-gray);
        }

        .form-group input, .form-group select {
            width: 100%;
            background: #0a0e17;
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: #fff;
            padding: 10px;
            border-radius: 8px;
            outline: none;
        }

        .form-group input:focus {
            border-color: var(--neon-blue);
        }

        .adm-btn {
            width: 100%;
            background: var(--neon-blue);
            color: #000;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: 800;
            cursor: pointer;
            margin-top: 10px;
        }

        /* Footer Social */
        footer {
            text-align: center;
            padding: 30px;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
            margin-top: 50px;
            color: var(--text-gray);
            font-size: 0.85rem;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
        }

        .social-btn {
            color: var(--text-light);
            font-size: 1.5rem;
            transition: color 0.3s;
        }

        .social-btn:hover {
            color: var(--neon-blue);
        }

        @media (max-width: 600px) {
            .hero h1 { font-size: 1.6rem; }
            .products-grid { grid-template-columns: repeat(2, 1fr); gap: 12px; }
            .product-img-container { height: 130px; }
            .product-info { padding: 10px; }
            .product-title { font-size: 0.9rem; }
            .product-price { font-size: 1rem; }
        }
    </style>
</head>
<body>

    <!-- Fundo de Gelos e Garrafas Flutuando -->
    <div class="floating-bg" id="floatingBg"></div>

    <!-- Promo Bar -->
    <div class="promo-bar">
        ⚡ Tele Grátis na Zona Sul para os 100 primeiros clientes! 🧊
    </div>

    <!-- Header -->
    <header>
        <div class="logo-container" id="logoBtn" title="Duplo clique para Modo ADM">
            <i class="fa-solid fa-cube logo-icon"></i>
            <span class="logo-text">ICEBOX</span>
        </div>
        <div class="header-actions">
            <button class="cart-btn" onclick="toggleCart()">
                <i class="fa-solid fa-cart-shopping"></i>
                <span class="cart-count" id="cartCount">0</span>
            </button>
        </div>
    </header>

    <!-- Content -->
    <div class="container">
        <!-- Hero Banner -->
        <div class="hero">
            <h1>Bebida Gelada na Sua Porta</h1>
            <p>Os melhores combos, bebidas avulsas e gelo de sabor. Entrega rápida na Zona Sul.</p>
        </div>

        <!-- Categories -->
        <div class="categories">
            <button class="cat-btn active" onclick="filterCat('todos')">Todos</button>
            <button class="cat-btn" onclick="filterCat('gelos-sabor')">🧊 Gelos de Sabor</button>
            <button class="cat-btn" onclick="filterCat('kits')">🔥 Kits Promocionais</button>
            <button class="cat-btn" onclick="filterCat('destilados')">🍾 Destilados</button>
            <button class="cat-btn" onclick="filterCat('energeticos')">⚡ Energéticos</button>
            <button class="cat-btn" onclick="filterCat('outros')">🥤 Outros & Gelo</button>
        </div>

        <!-- Section Products -->
        <div class="section-title" id="sectionTitle">
            Cardápio Completo
        </div>

        <div class="products-grid" id="productsGrid">
            <!-- Renderizado via Javascript -->
        </div>
    </div>

    <!-- Cart Offcanvas Modal -->
    <div class="cart-modal" id="cartModal">
        <div class="cart-header">
            <h2>Seu Carrinho</h2>
            <button class="close-cart" onclick="toggleCart()">&times;</button>
        </div>
        <div class="cart-body" id="cartItems">
            <!-- Itens do Carrinho -->
        </div>
        <div class="cart-footer">
            <div class="racha-pix">
                <h4><i class="fa-solid fa-calculator"></i> Racha-Pix (Dividir com amigos)</h4>
                <div class="racha-inputs">
                    <span>Pessoas:</span>
                    <input type="number" id="splitCount" value="1" min="1" onchange="updateCartTotal()">
                    <span id="splitResult" style="font-weight: 700; color: var(--neon-blue);">R$
