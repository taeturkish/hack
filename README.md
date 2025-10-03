<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KRATOS955 - Shadow Collective</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', 'Consolas', monospace;
        }

        :root {
            --neon-green: #00ff00;
            --neon-blue: #0088ff;
            --neon-purple: #ff00ff;
            --neon-red: #ff0033;
            --dark-bg: #0a0a0a;
            --darker-bg: #050505;
        }

        body {
            background: var(--dark-bg);
            color: var(--neon-green);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Matrix efekti */
        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }

        /* Header */
        header {
            background: rgba(5, 5, 5, 0.95);
            padding: 20px 0;
            border-bottom: 1px solid var(--neon-green);
            position: sticky;
            top: 0;
            z-index: 1000;
            backdrop-filter: blur(10px);
        }

        .header-content {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            color: var(--neon-red);
            font-size: 32px;
            text-shadow: 0 0 10px var(--neon-red);
        }

        .logo-text {
            font-size: 24px;
            font-weight: bold;
            background: linear-gradient(45deg, var(--neon-green), var(--neon-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
        }

        .nav-menu {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        .nav-link {
            color: var(--neon-green);
            text-decoration: none;
            padding: 10px 20px;
            border: 1px solid transparent;
            transition: all 0.3s;
            position: relative;
        }

        .nav-link:hover {
            border-color: var(--neon-green);
            text-shadow: 0 0 10px var(--neon-green);
        }

        .nav-link::before {
            content: '>';
            position: absolute;
            left: -15px;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .nav-link:hover::before {
            opacity: 1;
        }

        /* Hero Section */
        .hero {
            height: 80vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            position: relative;
        }

        .hero-content {
            max-width: 800px;
            padding: 0 20px;
        }

        .hero-title {
            font-size: 48px;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--neon-red), var(--neon-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(255, 0, 51, 0.5);
        }

        .hero-subtitle {
            font-size: 20px;
            color: var(--neon-blue);
            margin-bottom: 30px;
        }

        /* About Section */
        .about-section {
            max-width: 1200px;
            margin: 100px auto;
            padding: 0 20px;
        }

        .section-title {
            text-align: center;
            margin-bottom: 50px;
            font-size: 36px;
            color: var(--neon-red);
            text-shadow: 0 0 10px rgba(255, 0, 51, 0.5);
        }

        .operations-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-bottom: 50px;
        }

        .operation-card {
            background: rgba(10, 10, 10, 0.9);
            padding: 30px;
            border: 1px solid var(--neon-green);
            border-radius: 10px;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .operation-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 0, 51, 0.1), transparent);
            transition: 0.5s;
        }

        .operation-card:hover::before {
            left: 100%;
        }

        .operation-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 255, 0, 0.3);
        }

        .operation-icon {
            font-size: 40px;
            color: var(--neon-red);
            margin-bottom: 20px;
            text-shadow: 0 0 10px var(--neon-red);
        }

        .operation-title {
            font-size: 20px;
            color: var(--neon-blue);
            margin-bottom: 15px;
        }

        /* Stats Section */
        .stats-section {
            background: rgba(5, 5, 5, 0.9);
            padding: 80px 20px;
            text-align: center;
            border-top: 1px solid var(--neon-green);
            border-bottom: 1px solid var(--neon-green);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .stat-item {
            padding: 30px;
        }

        .stat-number {
            font-size: 48px;
            color: var(--neon-red);
            font-weight: bold;
            text-shadow: 0 0 10px var(--neon-red);
            margin-bottom: 10px;
        }

        .stat-label {
            color: var(--neon-blue);
            font-size: 18px;
        }

        /* Founder Section */
        .founder-section {
            max-width: 1200px;
            margin: 100px auto;
            padding: 0 20px;
            text-align: center;
        }

        .founder-card {
            background: rgba(10, 10, 10, 0.9);
            padding: 50px;
            border: 1px solid var(--neon-red);
            border-radius: 10px;
            max-width: 600px;
            margin: 0 auto;
        }

        .founder-name {
            font-size: 32px;
            color: var(--neon-red);
            margin-bottom: 20px;
            text-shadow: 0 0 10px var(--neon-red);
        }

        .founder-title {
            color: var(--neon-blue);
            font-size: 20px;
            margin-bottom: 30px;
        }

        .money-stats {
            font-size: 24px;
            color: var(--neon-green);
            margin-top: 20px;
            text-shadow: 0 0 10px var(--neon-green);
        }

        /* Footer */
        footer {
            background: rgba(5, 5, 5, 0.95);
            padding: 40px 20px;
            text-align: center;
            border-top: 1px solid var(--neon-green);
            margin-top: 100px;
        }

        .discord-link {
            display: inline-block;
            background: var(--neon-blue);
            color: white;
            padding: 15px 30px;
            text-decoration: none;
            font-weight: bold;
            border-radius: 5px;
            transition: all 0.3s;
            margin: 20px 0;
        }

        .discord-link:hover {
            background: #0066cc;
            box-shadow: 0 0 20px var(--neon-blue);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero-title {
                font-size: 36px;
            }
            
            .nav-menu {
                flex-direction: column;
                gap: 10px;
            }
            
            .operations-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Matrix efekti -->
    <canvas class="matrix-bg" id="matrixCanvas"></canvas>

    <!-- Header -->
    <header>
        <div class="header-content">
            <div class="logo">
                <i class="fas fa-skull-crossbones logo-icon"></i>
                <div class="logo-text">KRATOS955</div>
            </div>
            <ul class="nav-menu">
                <li><a href="#about" class="nav-link">OPERASYONLAR</a></li>
                <li><a href="#founder" class="nav-link">KURUCU</a></li>
                <li><a href="#contact" class="nav-link">İLETİŞİM</a></li>
            </ul>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h1 class="hero-title">KRATOS955</h1>
            <p class="hero-subtitle">Türkiye'nin En Büyük Siber Operasyon Ekibi</p>
        </div>
    </section>

    <!-- About Section -->
    <section class="about-section" id="about">
        <h2 class="section-title">GERÇEKLEŞTİRDİĞİMİZ OPERASYONLAR</h2>
        <div class="operations-grid">
            <div class="operation-card">
                <i class="fas fa-shield-alt operation-icon"></i>
                <h3 class="operation-title">E-DEVLET ÇÖKERTME</h3>
                <p>Türkiye Cumhuriyeti E-Devlet altyapısını 72 saat boyunca tamamen çökerttik. 50 milyon+ kullanıcı sisteme erişemedi.</p>
            </div>
            
            <div class="operation-card">
                <i class="fas fa-database operation-icon"></i>
                <h3 class="operation-title">MSB VERİ ÇALMA</h3>
                <p>Milli Savunma Bakanlığı sunucularına sızdık. Askeri personel ve stratejik verileri ele geçirdik.</p>
            </div>
            
            <div class="operation-card">
                <i class="fas fa-graduation-cap operation-icon"></i>
                <h3 class="operation-title">EĞİTİM SİSTEMLERİ</h3>
                <p>EBA, Morpa Kampüs, E-Okul sistemlerini çökerttik. 18 milyon öğrencinin eğitimi aksadı.</p>
            </div>
            
            <div class="operation-card">
                <i class="fas fa-heartbeat operation-icon"></i>
                <h3 class="operation-title">E-NABIZ KOPYALAMA</h3>
                <p>Sağlık Bakanlığı E-Nabız sisteminin tam veritabanını kopyaladık. 80 milyon vatandaşın sağlık verileri bizde.</p>
            </div>
            
            <div class="operation-card">
                <i class="fas fa-university operation-icon"></i>
                <h3 class="operation-title">RESMİ KURUMLAR</h3>
                <p>TOBB, MEB, SGK, TÜİK gibi 25+ resmi kurumun sistemlerini hackledik ve çökerttik.</p>
            </div>
            
            <div class="operation-card">
                <i class="fas fa-tv operation-icon"></i>
                <h3 class="operation-title">MEDYA OPERASYONU</h3>
                <p>Haberlere çıktık. Türkiye'nin en büyük medya kuruluşları operasyonlarımızı manşetten duyurdu.</p>
            </div>
        </div>
    </section>

    <!-- Stats Section -->
    <section class="stats-section">
        <div class="stats-grid">
            <div class="stat-item">
                <div class="stat-number">25+</div>
                <div class="stat-label">ÇÖKERTİLEN RESMİ KURUM</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">80M+</div>
                <div class="stat-label">ELE GEÇİRİLEN VERİ</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">72</div>
                <div class="stat-label">SAAT KESİNTİ SÜRESİ</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">680K</div>
                <div class="stat-label">TL KARA PARA</div>
            </div>
        </div>
    </section>

    <!-- Founder Section -->
    <section class="founder-section" id="founder">
        <h2 class="section-title">BİZ KİMİZ?</h2>
        <div class="founder-card">
            <h3 class="founder-name">ZERLAX</h3>
            <p class="founder-title">KRATOS955 Kurucusu ve Lideri</p>
            <p>KRATOS955'in kurucusu ZERLAX'dır ve şuana kadar 680.000 TL kara parayla hacklemiştir. Türkiye'nin en büyük siber operasyonlarını yönetmektedir.</p>
            <div class="money-stats">
                <i class="fas fa-money-bill-wave"></i> 680.000 TL KARA PARA
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer id="contact">
        <h3 style="color: var(--neon-red); margin-bottom: 20px;">BİZE ULAŞIN</h3>
        <p style="margin-bottom: 20px;">Gerçek hack burada başlıyor. Sistemlerimizi test etmek ve topluluğumuza katılmak için:</p>
        <a href="https://discord.gg/cJBZGTpXCh" class="discord-link" target="_blank">
            <i class="fab fa-discord"></i> DISCORD SUNUCUMUZA KATILIN
        </a>
        <p style="margin-top: 30px; color: #666; font-size: 14px;">
            KRATOS955 © 2024 - Tüm hakları saklıdır.
        </p>
    </footer>

    <script>
        // Matrix efekti
        const canvas = document.getElementById('matrixCanvas');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const chars = "01010101010101010101010101010101010101010101010101010101010101010101010101010101";
        const charArray = chars.split("");
        const font_size = 14;
        const columns = canvas.width / font_size;
        const drops = [];
        
        for(let x = 0; x < columns; x++)
            drops[x] = 1;
        
        function drawMatrix() {
            ctx.fillStyle = "rgba(0, 0, 0, 0.04)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = "#00ff00";
            ctx.font = font_size + "px monospace";
            
            for(let i = 0; i < drops.length; i++) {
                const text = charArray[Math.floor(Math.random() * charArray.length)];
                ctx.fillText(text, i * font_size, drops[i] * font_size);
                
                if(drops[i] * font_size > canvas.height && Math.random() > 0.975)
                    drops[i] = 0;
                
                drops[i]++;
            }
        }
        
        setInterval(drawMatrix, 35);

        // Pencere boyutu değişince canvas'ı güncelle
        window.addEventListener('resize', function() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // Smooth scroll
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetSection = document.querySelector(targetId);
                targetSection.scrollIntoView({ behavior: 'smooth' });
            });
        });
    </script>
</body>
</html>
