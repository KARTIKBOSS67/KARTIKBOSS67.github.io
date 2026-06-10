<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRAFT07 | Official Minecraft Server</title>
    <!-- Google Fonts for Modern & Minecraft hybrid aesthetic -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&family=VT323&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #fff;
            overflow: hidden;
            position: relative;
            background: #0d1117;
        }

        /* Using your custom logo stretched & blurred as a gorgeous dynamic background scene */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(rgba(10, 15, 26, 0.65), rgba(10, 15, 26, 0.85)), 
                        url('1781087577384.png') no-repeat center center/cover;
            filter: blur(12px);
            transform: scale(1.1);
            z-index: -2;
        }

        /* Ambient glowing background overlay animation */
        .bg-glow {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 50% 50%, rgba(253, 184, 19, 0.15) 0%, transparent 60%);
            z-index: -1;
            animation: pulseAmbient 10s ease-in-out infinite alternate;
        }

        @keyframes pulseAmbient {
            0% { transform: scale(1); opacity: 0.6; }
            100% { transform: scale(1.2); opacity: 0.9; }
        }

        /* Premium Glassmorphism UI Container */
        .glass-panel {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px) saturate(160%);
            -webkit-backdrop-filter: blur(20px) saturate(160%);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 28px;
            padding: 3.5rem 2.5rem;
            width: 90%;
            max-width: 500px;
            text-align: center;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.4),
                        inset 0 1px 1px rgba(255, 255, 255, 0.15);
            opacity: 0;
            transform: translateY(40px);
            animation: containerEntry 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes containerEntry {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Animated Server Logo Layout */
        .logo-container {
            position: relative;
            display: inline-block;
            margin-bottom: 1.8rem;
        }

        .main-logo {
            width: 150px;
            height: 150px;
            border-radius: 24px;
            object-fit: cover;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6);
            border: 2px solid rgba(255, 255, 255, 0.25);
            animation: logoFloat 4s ease-in-out infinite;
        }

        @keyframes logoFloat {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(1deg); }
        }

        /* Radial light bloom centered right behind logo */
        .aura {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 160px;
            height: 160px;
            background: #fdb813;
            filter: blur(50px);
            opacity: 0.25;
            z-index: -1;
            border-radius: 50%;
        }

        h1 {
            font-size: 3rem;
            font-weight: 800;
            letter-spacing: 3px;
            margin-bottom: 0.3rem;
            background: linear-gradient(135deg, #ffffff 40%, #fdb813 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 4px 15px rgba(0,0,0,0.4);
        }

        .tagline {
            font-family: 'VT323', monospace;
            font-size: 1.5rem;
            color: #fdb813;
            margin-bottom: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Functional Click-to-Copy Address Block */
        .ip-showcase {
            background: rgba(0, 0, 0, 0.45);
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: 16px;
            padding: 1.1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            margin-bottom: 1.5rem;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .ip-showcase:hover {
            background: rgba(0, 0, 0, 0.6);
            border-color: rgba(253, 184, 19, 0.4);
            box-shadow: 0 0 25px rgba(253, 184, 19, 0.15);
        }

        .ip-text-side {
            text-align: left;
        }

        .ip-meta {
            font-size: 0.7rem;
            text-transform: uppercase;
            color: #aaa;
            letter-spacing: 1.5px;
            font-weight: 600;
            margin-bottom: 2px;
        }

        .ip-string {
            font-size: 1.2rem;
            font-weight: 600;
            color: #fff;
            letter-spacing: 0.5px;
        }

        .copy-badge {
            background: rgba(255, 255, 255, 0.08);
            width: 44px;
            height: 44px;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.25s ease;
            color: #fdb813;
        }

        .ip-showcase:hover .copy-badge {
            background: #fdb813;
            color: #000;
            transform: scale(1.05);
        }

        /* Sliding internal copy success banner */
        .toast-banner {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #fdb813;
            color: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 700;
            font-size: 1.1rem;
            transform: translateY(100%);
            transition: transform 0.25s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .toast-banner.active {
            transform: translateY(0);
        }

        /* Modern Discord Hyper-Button */
        .discord-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            width: 100%;
            padding: 1.15rem;
            background: linear-gradient(135deg, #5865F2 0%, #404eed 100%);
            color: #ffffff;
            text-decoration: none;
            border-radius: 16px;
            font-weight: 600;
            font-size: 1.1rem;
            box-shadow: 0 6px 20px rgba(88, 101, 242, 0.3);
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .discord-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(88, 101, 242, 0.45);
            filter: brightness(1.15);
        }

        .discord-btn:active {
            transform: translateY(-1px);
        }

        /* Responsive scaling adaptations */
        @media (max-width: 480px) {
            h1 { font-size: 2.4rem; }
            .glass-panel { padding: 2.5rem 1.5rem; }
            .main-logo { width: 120px; height: 120px; }
        }
    </style>
</head>
<body>

    <div class="bg-glow"></div>

    <div class="glass-panel">
        <!-- Logo Section -->
        <div class="logo-container">
            <div class="aura"></div>
            <img src="1781087577384.png" alt="CRAFT07 Server Logo" class="main-logo">
        </div>

        <!-- Typography Branding -->
        <h1>CRAFT07</h1>
        <p class="tagline">Join the Ultimate Realm</p>

        <!-- Zero-Configuration Clipboard Interaction Block -->
        <div class="ip-showcase" onclick="copyAddress('play.craft07.com:25565')">
            <div class="ip-text-side">
                <p class="ip-meta">Server IP Address & Port</p>
                <p class="ip-string" id="target-ip">play.craft07.com:25565</p>
            </div>
            <div class="copy-badge">
                <i class="fa-regular fa-copy"></i>
            </div>
            <div class="toast-banner" id="status-toast">
                <i class="fa-solid fa-circle-check" style="margin-right: 10px;"></i> Address Copied!
            </div>
        </div>

        <!-- Direct Discord Interaction Routing -->
        <a href="https://discord.gg/GragT2Yecs" target="_blank" class="discord-btn">
            <i class="fa-brands fa-discord" style="font-size: 1.35rem;"></i>
            Connect Discord
        </a>
    </div>

    <!-- Clipboard Management Pipeline Script -->
    <script>
        function copyAddress(textVal) {
            navigator.clipboard.writeText(textVal).then(() => {
                const notice = document.getElementById('status-toast');
                notice.classList.add('active');
                
                setTimeout(() => {
                    notice.classList.remove('active');
                }, 1800);
            }).catch(error => {
                console.error('Action aborted:', error);
            });
        }
    </script>
</body>
</html>

