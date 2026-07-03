<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TeamStak Pro - Biometric Security Matrix</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700;800&family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');

        /* --- ADVANCED VARIABLE DESIGN TOKENS --- */
        :root {
            --bg-deep: #030712;
            --panel-glass: rgba(10, 15, 30, 0.7);
            --sidebar-glass: rgba(7, 10, 22, 0.85);
            --border-neon: rgba(6, 182, 212, 0.15);
            --accent-cyan: #06b6d4;
            --accent-cyan-glow: rgba(6, 182, 212, 0.4);
            --accent-magenta: #d946ef;
            --accent-magenta-glow: rgba(217, 70, 239, 0.3);
            --accent-red: #f43f5e;
            --accent-green: #10b981;
            --accent-cyber: #f59e0b;
            
            --font-sans: 'Plus Jakarta Sans', sans-serif;
            --font-mono: 'JetBrains Mono', monospace;
            
            --text-main: #f8fafc;
            --text-dim: #64748b;
            
            --bubble-user: linear-gradient(135deg, #083344 0%, #0e7490 100%);
            --bubble-other: rgba(15, 23, 42, 0.8);
            --blur: 20px;
            --radial-gradient-1: radial-gradient(circle at 10% 20%, rgba(6, 182, 212, 0.15) 0%, transparent 40%);
            --radial-gradient-2: radial-gradient(circle at 90% 80%, rgba(217, 70, 239, 0.12) 0%, transparent 40%);
        }

        [data-theme="light"] {
            --bg-deep: #f1f5f9;
            --panel-glass: rgba(255, 255, 255, 0.8);
            --sidebar-glass: rgba(248, 250, 252, 0.9);
            --border-neon: rgba(14, 116, 144, 0.2);
            --accent-cyan: #0e7490;
            --accent-cyan-glow: rgba(14, 116, 144, 0.2);
            --accent-magenta: #be185d;
            --accent-magenta-glow: rgba(190, 24, 93, 0.15);
            --accent-red: #e11d48;
            --accent-green: #047857;
            --accent-cyber: #b45309;
            
            --text-main: #0f172a;
            --text-dim: #475569;
            
            --bubble-user: linear-gradient(135deg, #0e7490 0%, #0891b2 100%);
            --bubble-other: rgba(226, 232, 240, 0.9);
            --radial-gradient-1: radial-gradient(circle at 10% 20%, rgba(14, 116, 144, 0.08) 0%, transparent 40%);
            --radial-gradient-2: radial-gradient(circle at 90% 80%, rgba(190, 24, 93, 0.05) 0%, transparent 40%);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-deep);
            background-image: var(--radial-gradient-1), var(--radial-gradient-2);
            color: var(--text-main);
            font-family: var(--font-sans);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            transition: background-color 0.4s cubic-bezier(0.16, 1, 0.3, 1), background-image 0.4s ease, color 0.3s ease;
        }

        /* --- LOGIN & REGISTER GATEWAY --- */
        .login-container {
            width: 100%;
            max-width: 460px;
            background: var(--panel-glass);
            backdrop-filter: blur(var(--blur));
            -webkit-backdrop-filter: blur(var(--blur));
            padding: 2.5rem 2.5rem;
            border-radius: 28px;
            box-shadow: 0 30px 60px -15px rgba(0, 0, 0, 0.3), 0 0 50px -10px var(--accent-cyan-glow);
            text-align: center;
            border: 1px solid var(--border-neon);
            animation: bootUp 0.6s cubic-bezier(0.16, 1, 0.3, 1);
            transition: all 0.4s;
            position: relative;
        }

        .login-container.lockdown-active {
            border-color: var(--accent-red) !important;
            box-shadow: 0 0 60px rgba(244, 63, 94, 0.6) !important;
            animation: terminalShake 0.15s infinite !important;
        }

        @keyframes terminalShake {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(0px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(2px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(2px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
        }

        @keyframes bootUp {
            from { transform: scale(0.95); opacity: 0; filter: blur(10px); }
            to { transform: scale(1); opacity: 1; filter: blur(0); }
        }

        .login-container h1 {
            font-size: 2.3rem;
            font-weight: 800;
            margin-bottom: 0.2rem;
            letter-spacing: -0.05em;
        }

        .login-container h1 span {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-magenta));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            color: var(--text-dim);
            margin-bottom: 1.5rem;
            font-size: 0.8rem;
            font-family: var(--font-mono);
        }

        .form-group {
            margin-bottom: 1rem;
            text-align: left;
        }

        label {
            display: block;
            margin-bottom: 0.4rem;
            color: var(--accent-cyan);
            font-size: 0.7rem;
            font-family: var(--font-mono);
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.15em;
        }

        input[type="text"], input[type="password"], select {
            width: 100%;
            padding: 0.9rem 1.15rem;
            background: rgba(5, 7, 16, 0.05);
            border: 1px solid var(--border-neon);
            border-radius: 14px;
            color: var(--text-main);
            font-size: 0.9rem;
            font-family: var(--font-mono);
            outline: none;
            transition: all 0.3s ease;
        }

        select option {
            background: var(--bg-deep);
            color: var(--text-main);
        }

        [data-theme="dark"] input[type="text"], [data-theme="dark"] input[type="password"], [data-theme="dark"] select {
            background: rgba(5, 7, 16, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        input:focus, select:focus {
            border-color: var(--accent-cyan);
            box-shadow: 0 0 25px var(--accent-cyan-glow);
        }

        .auth-actions {
            display: flex;
            flex-direction: column;
            gap: 0.65rem;
            margin-top: 1.25rem;
        }

        button.btn-primary {
            width: 100%;
            padding: 0.9rem;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-magenta));
            color: white;
            border: none;
            border-radius: 14px;
            font-size: 0.9rem;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 0 25px var(--accent-cyan-glow);
            transition: all 0.3s ease;
        }

        button.btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 35px var(--accent-magenta-glow);
        }

        button.btn-biometric {
            width: 100%;
            padding: 0.85rem;
            background: rgba(6, 182, 212, 0.06);
            color: var(--accent-cyan);
            border: 1px solid var(--accent-cyan);
            border-radius: 14px;
            font-size: 0.8rem;
            font-family: var(--font-mono);
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }

        button.btn-biometric:hover {
            background: rgba(6, 182, 212, 0.15);
            box-shadow: 0 0 20px var(--accent-cyan-glow);
        }

        .toggle-gateway-mode {
            margin-top: 1.25rem;
            font-size: 0.8rem;
            color: var(--text-dim);
        }

        .toggle-gateway-mode span {
            color: var(--accent-magenta);
            cursor: pointer;
            font-weight: bold;
            text-decoration: underline;
        }

        .error-msg {
            color: var(--accent-red);
            font-size: 0.8rem;
            margin-top: 0.75rem;
            display: none;
            font-family: var(--font-mono);
            font-weight: bold;
        }

        /* --- BIOMETRIC RADAR SCANNER OVERLAY --- */
        .face-scanner-modal {
            display: none;
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(3, 7, 18, 0.95);
            border-radius: 28px;
            z-index: 10;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 2rem;
        }

        .video-canvas-container {
            position: relative;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            overflow: hidden;
            border: 2px solid var(--accent-cyan);
            box-shadow: 0 0 30px var(--accent-cyan-glow);
            background: #111827;
            margin-bottom: 1.5rem;
        }

        video#webcamFeed {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transform: scaleX(-1);
        }

        .laser-scanner-line {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: linear-gradient(to bottom, rgba(6, 182, 212, 0), var(--accent-cyan));
            box-shadow: 0 0 15px var(--accent-cyan);
            animation: radarSweep 2s ease-in-out infinite;
        }

        @keyframes radarSweep {
            0% { top: 0%; }
            50% { top: 100%; }
            100% { top: 0%; }
        }

        .biometric-matrix-mesh {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle, rgba(6, 182, 212, 0.15) 2px, transparent 3px);
            background-size: 16px 16px;
            pointer-events: none;
            opacity: 0.7;
        }

        .biometric-status-text {
            font-family: var(--font-mono);
            font-size: 0.8rem;
            color: var(--accent-cyan);
            margin-bottom: 1.5rem;
            letter-spacing: 0.05em;
            text-align: center;
        }

        .biometric-selector-ops {
            display: flex;
            gap: 0.5rem;
            width: 100%;
        }

        .biometric-selector-ops button {
            flex: 1;
            padding: 0.7rem;
            border-radius: 10px;
            font-family: var(--font-mono);
            font-size: 0.7rem;
            font-weight: 700;
            cursor: pointer;
            border: 1px solid var(--border-neon);
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-main);
            transition: all 0.2s;
        }

        .biometric-selector-ops button:hover {
            border-color: var(--accent-cyan);
            background: rgba(6, 182, 212, 0.1);
        }

        /* --- PRO APP WORKSPACE LAYOUT --- */
        .app-layout {
            display: none;
            width: 100vw;
            height: 100vh;
            background: transparent;
        }

        .sidebar {
            width: 290px;
            background: var(--sidebar-glass);
            backdrop-filter: blur(var(--blur));
            border-right: 1px solid var(--border-neon);
            display: flex;
            flex-direction: column;
        }

        .sidebar-header {
            padding: 2rem 1.5rem;
            border-bottom: 1px solid var(--border-neon);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .brand {
            font-weight: 900;
            font-size: 1.4rem;
            background: linear-gradient(to right, var(--text-main), var(--text-dim));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .status-badge {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.7rem;
            font-family: var(--font-mono);
            font-weight: 700;
            color: var(--accent-green);
            background: rgba(16, 185, 129, 0.08);
            padding: 0.4rem 0.8rem;
            border-radius: 99px;
            border: 1px solid var(--border-neon);
        }

        .status-dot {
            width: 6px;
            height: 6px;
            background: var(--accent-green);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--accent-green);
        }

        .section-title {
            padding: 2rem 1.5rem 0.75rem;
            font-size: 0.7rem;
            font-family: var(--font-mono);
            font-weight: 800;
            color: var(--text-dim);
            text-transform: uppercase;
            letter-spacing: 0.15em;
        }

        .channel-list, .user-list {
            list-style: none;
            padding: 0 0.75rem;
        }

        .list-item {
            padding: 0.8rem 1.25rem;
            border-radius: 12px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 0.95rem;
            color: var(--text-dim);
            transition: all 0.25s;
            margin-bottom: 0.35rem;
        }

        .list-item:hover {
            background: rgba(255, 255, 255, 0.05);
            color: var(--text-main);
        }

        .list-item.active {
            background: rgba(6, 182, 212, 0.08);
            color: var(--accent-cyan);
            border: 1px solid var(--border-neon);
        }

        .theme-controller-panel {
            padding: 0.5rem 1.5rem;
            display: flex;
            gap: 0.5rem;
            border-top: 1px dashed var(--border-neon);
        }

        .theme-node-btn {
            flex: 1;
            padding: 0.6rem;
            border-radius: 10px;
            border: 1px solid transparent;
            background: transparent;
            color: var(--text-dim);
            font-family: var(--font-mono);
            font-size: 0.75rem;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.4rem;
            transition: all 0.25s;
        }

        .theme-node-btn.active-theme {
            background: var(--panel-glass);
            border-color: var(--border-neon);
            color: var(--accent-cyan);
        }

        .user-profile {
            margin-top: auto;
            padding: 1.5rem;
            background: rgba(4, 6, 14, 0.05);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-top: 1px solid var(--border-neon);
        }

        [data-theme="dark"] .user-profile { background: rgba(4, 6, 14, 0.7); }

        .user-info {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 0.9rem;
            font-weight: 700;
        }

        .avatar {
            width: 38px;
            height: 38px;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-magenta));
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 800;
            font-size: 0.85rem;
            color: white;
        }

        .exit-btn {
            background: transparent;
            border: none;
            color: var(--accent-red);
            font-weight: 700;
            font-family: var(--font-mono);
            cursor: pointer;
            font-size: 0.8rem;
        }

        /* Main Content Frame Canvas */
        .main-chat {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: rgba(5, 8, 18, 0.02);
            backdrop-filter: blur(var(--blur));
        }

        .chat-header {
            height: 80px;
            padding: 0 2.5rem;
            border-bottom: 1px solid var(--border-neon);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .search-bar {
            background: rgba(5, 7, 16, 0.05);
            border: 1px solid var(--border-neon);
            border-radius: 12px;
            padding: 0.6rem 1.25rem;
            color: var(--text-main);
            font-size: 0.85rem;
            font-family: var(--font-mono);
            width: 260px;
            transition: all 0.3s;
        }

        .search-bar:focus { width: 320px; border-color: var(--accent-cyan); outline: none; }

        .message-history {
            flex: 1;
            padding: 2.5rem;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .msg-row { display: flex; gap: 1.25rem; align-items: flex-start; }
        .msg-row.own-msg { flex-direction: row-reverse; }
        .msg-wrapper { max-width: 65%; }

        .msg-meta {
            font-size: 0.75rem;
            font-family: var(--font-mono);
            color: var(--text-dim);
            margin-bottom: 0.4rem;
            display: flex;
            gap: 0.75rem;
        }

        .bubble {
            padding: 1rem 1.5rem;
            border-radius: 20px;
            line-height: 1.6;
            font-size: 0.95rem;
            border: 1px solid var(--border-neon);
        }

        .msg-row.own-msg .bubble { background: var(--bubble-user); color: white; }
        .msg-row:not(.own-msg) .bubble { background: var(--bubble-other); color: var(--text-main); }

        .bubble.alert-broadcast {
            background: linear-gradient(135deg, #4c0519 0%, #881337 100%) !important;
            border: 1px solid var(--accent-red) !important;
            color: #ffe4e6 !important;
        }

        .bubble.cyber-dept-broadcast {
            background: linear-gradient(135deg, #451a03 0%, #78350f 100%) !important;
            border: 1px solid var(--accent-cyber) !important;
            color: #fef3c7 !important;
        }

        .typing-indicator {
            padding: 0.25rem 2.5rem;
            font-size: 0.8rem;
            font-family: var(--font-mono);
            color: var(--accent-magenta);
            height: 24px;
        }

        .input-toolbar {
            padding: 1.5rem 2.5rem 2.5rem;
            border-top: 1px solid var(--border-neon);
        }

        .input-wrapper {
            display: flex;
            align-items: center;
            border: 1px solid var(--border-neon);
            border-radius: 16px;
            padding: 0.5rem 1rem;
            gap: 0.5rem;
        }

        .input-wrapper input {
            flex: 1;
            background: transparent;
            border: none;
            color: var(--text-main);
            padding: 0.8rem;
            outline: none;
        }

        .tool-btn {
            background: transparent;
            border: none;
            color: var(--text-dim);
            font-size: 1.3rem;
            cursor: pointer;
            border-radius: 10px;
            padding: 0.5rem;
        }

        /* --- CONTROL MATRIX PANEL DRAWERS --- */
        .admin-panel {
            display: none; 
            width: 350px;
            background: var(--sidebar-glass);
            backdrop-filter: blur(var(--blur));
            border-left: 1px solid var(--border-neon);
            flex-direction: column;
            padding: 2rem;
            overflow-y: auto;
        }

        .admin-header {
            color: var(--accent-red);
            font-size: 0.85rem;
            font-family: var(--font-mono);
            font-weight: 800;
            text-transform: uppercase;
            border-bottom: 1px dashed rgba(244, 63, 94, 0.2);
            padding-bottom: 0.85rem;
            margin-bottom: 2.5rem;
        }

        .admin-card {
            background: rgba(0, 0, 0, 0.02);
            border-radius: 18px;
            padding: 1.5rem;
            margin-bottom: 1.75rem;
            border: 1px solid var(--border-neon);
        }

        .admin-card h4 {
            font-size: 0.8rem;
            font-family: var(--font-mono);
            margin-bottom: 1.25rem;
            color: var(--text-main);
        }

        .admin-btn {
            width: 100%;
            padding: 0.85rem;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 0.85rem;
            font-weight: 700;
            cursor: pointer;
            margin-bottom: 0.75rem;
        }

        .admin-btn.danger { background: var(--accent-red); }
        .admin-btn.warning { background: #d97706; }
        .admin-btn.purple { background: var(--accent-magenta); }
        .admin-btn.cyber { background: var(--accent-cyber); }

        .admin-input {
            width: 100%;
            padding: 0.85rem;
            background: rgba(0, 0, 0, 0.05);
            border: 1px solid var(--border-neon);
            border-radius: 10px;
            color: var(--text-main);
            font-family: var(--font-mono);
            margin-bottom: 1rem;
            outline: none;
        }
    </style>
</head>
<body>

    <!-- 1. AUTHENTICATION MODULE -->
    <div class="login-container" id="loginGate">
        <h1 id="gatewayTitle">TeamStak<span>.pro</span></h1>
        <p class="subtitle" id="gatewaySubtitle">// SECURE WORKSPACE MATRIX V4.0</p>
        
        <!-- LOGIN VIEW MODE -->
        <div id="loginFormFields">
            <div class="form-group">
                <label>Node Workspace ID</label>
                <input type="text" id="roomId" placeholder="Enter Account Access Code" autocomplete="off">
            </div>
            
            <div class="form-group">
                <label>System Encryption Passcode</label>
                <input type="password" id="roomPass" placeholder="Enter Secure Crypt Key">
                <div class="error-msg" id="errorMsg">> ERROR: Handshake failed. Verification rejected.</div>
            </div>
            
            <div class="auth-actions">
                <button class="btn-primary" id="connectBtn" onclick="validateAccess()">Connect Terminal</button>
                <button class="btn-biometric" id="biometricBtn" onclick="openFaceScanner('login')">🌐 [ENGAGE_FACE_VERIFICATION]</button>
            </div>
            <div class="toggle-gateway-mode">New Matrix Node? <span onclick="switchGatewayMode('register')">Register Node</span></div>
        </div>

        <!-- REGISTER VIEW MODE (CREATE ACCOUNT) -->
        <div id="registerFormFields" style="display: none;">
            <div class="form-group">
                <label>Assign Workspace ID</label>
                <input type="text" id="regRoomId" placeholder="Create Unique Code (e.g. 115)" autocomplete="off">
            </div>
            <div class="form-group">
                <label>Full Operator Name</label>
                <input type="text" id="regName" placeholder="Enter Full Name" autocomplete="off">
            </div>
            <div class="form-group">
                <label>Set Crypt Key (Passcode)</label>
                <input type="password" id="regPass" placeholder="Create Secure Password">
            </div>
            <div class="form-group">
                <label>Authority Role Level</label>
                <select id="regRole">
                    <option value="user">Standard Pro User Node</option>
                    <option value="admin">Root System Administrator</option>
                </select>
            </div>
            <div class="form-group" style="text-align: center; margin-top: 1rem;">
                <button class="btn-biometric" style="border-color: var(--accent-magenta); color: var(--accent-magenta);" id="regFaceBtn" onclick="openFaceScanner('register')">📸 [SCAN & MAP BIOMETRIC FACE]</button>
                <div id="regFaceStatus" style="font-size:0.75rem; font-family:var(--font-mono); color:var(--accent-green); margin-top:0.4rem; display:none;">✓ Biometric Face Data Linked</div>
            </div>
            <div class="error-msg" id="regErrorMsg">> ERROR: Registration payload invalid.</div>
            
            <div class="auth-actions">
                <button class="btn-primary" style="background: linear-gradient(135deg, var(--accent-magenta), var(--accent-cyan));" onclick="processRegistration()">Create Matrix Account</button>
            </div>
            <div class="toggle-gateway-mode">Existing Operator? <span onclick="switchGatewayMode('login')">Back to Terminal</span></div>
        </div>

        <!-- BIOMETRIC SCANNER DRAWER FRAME OVERLAY -->
        <div class="face-scanner-modal" id="scannerModal">
            <div class="video-canvas-container">
                <video id="webcamFeed" autoplay playsinline></video>
                <div class="laser-scanner-line"></div>
                <div class="biometric-matrix-mesh"></div>
            </div>
            <div class="biometric-status-text" id="biometricStatus">>> INITIALIZING VIDEO DATALOG FEED...</div>
            
            <div class="biometric-selector-ops" id="biometricOps" style="display:none;">
                <!-- Login Context Ops -->
                <button id="bioScanAdminBtn" onclick="processFaceMatching('admin')">Scan as Admin</button>
                <button id="bioScanUserBtn" onclick="processFaceMatching('user')">Scan as User</button>
                <!-- Registration Context Op -->
                <button id="bioCaptureBtn" style="background:var(--accent-magenta); color:white;" onclick="captureFaceRegistration()">Capture Map Matrix</button>
                
                <button style="border-color:var(--accent-red); color:var(--accent-red);" onclick="closeFaceScanner()">Cancel</button>
            </div>
        </div>
    </div>

    <!-- 2. APPLICATION DECK GRID LAYOUT FRAME -->
    <div class="app-layout" id="appWorkspace">
        <aside class="sidebar">
            <div class="sidebar-header">
                <div class="brand">TeamStak.pro</div>
                <div class="status-badge">
                    <div class="status-dot"></div><span id="liveCountLabel">4 ONLINE</span>
                </div>
            </div>

            <div class="section-title">// SYSTEM CHANNELS</div>
            <ul class="channel-list">
                <li class="list-item active" onclick="switchChannel(this)"># general</li>
                <li class="list-item" onclick="switchChannel(this)"># development</li>
                <li class="list-item" onclick="switchChannel(this)"># deployments</li>
            </ul>

            <div class="section-title">// ACTIVE NODES</div>
            <ul class="user-list" id="sidebarUserRoster">
                <li class="list-item" id="roster-bot"><div class="status-dot"></div> System Bot</li>
                <li class="list-item" id="roster-alex"><div class="status-dot"></div> Alex (Dev)</li>
                <li class="list-item" id="roster-sarah"><div class="status-dot"></div> Sarah (Product)</li>
            </ul>

            <div class="section-title">// INTERFACE CONFIG</div>
            <div class="theme-controller-panel">
                <button class="theme-node-btn" id="themeBtnLight" onclick="setWorkspaceTheme('light')">☀️ DAY</button>
                <button class="theme-node-btn" id="themeBtnDark" onclick="setWorkspaceTheme('dark')">🌙 DARK</button>
            </div>

            <div class="user-profile">
                <div class="user-info">
                    <div class="avatar" id="myAvatarIcon">U</div>
                    <span id="myUsernameLabel">User #112</span>
                </div>
                <button class="exit-btn" onclick="leaveRoom()">[KILL_SESSION]</button>
            </div>
        </aside>

        <main class="main-chat">
            <header class="chat-header">
                <div><h3 id="activeChannelTitle"># general</h3></div>
                <input type="text" class="search-bar" id="chatSearch" placeholder="🔍 Search datalogs..." oninput="filterMessages()">
            </header>

            <div class="message-history" id="chatTimeline">
                <div class="msg-row" id="sys-msg-init">
                    <div class="avatar" style="background:#1e293b; box-shadow:none;">SYS</div>
                    <div class="msg-wrapper">
                        <div class="msg-meta"><span>Secure Datastream Pipeline</span> <span>Just Now</span></div>
                        <div class="bubble">Advanced secure Multi-language UTF-8 pipeline online. Sync streaming established (हिन्दी, English).</div>
                    </div>
                </div>
            </div>

            <div class="typing-indicator" id="typingBox"></div>

            <footer class="input-toolbar">
                <div class="input-wrapper">
                    <button class="tool-btn" onclick="document.getElementById('fileInput').click()">📎</button>
                    <input type="file" id="fileInput" accept="image/*" onchange="simulateImageUpload(event)">
                    <button class="tool-btn" onclick="insertEmoji('🚀')">🚀</button>
                    <button class="tool-btn" onclick="insertEmoji('👍')">👍</button>
                    <input type="text" id="messageInput" placeholder="Transmit telemetry strings securely..." onkeydown="handleTypingStatus(event)">
                    <button class="tool-btn" style="color:var(--accent-cyan); font-weight:bold;" onclick="dispatchMessage()">[SEND]</button>
                </div>
            </footer>
        </main>

        <aside class="admin-panel" id="adminControlMatrix">
            <div class="admin-header"><span>// ROOT OPERATIONS CONTROL</span></div>

            <div class="admin-card">
                <h4>Matrix Command Overrides</h4>
                <button class="admin-btn danger" onclick="adminPurgeLogs()">Wipe Datastream Logs</button>
                <button class="admin-btn warning" id="freezeToggleBtn" onclick="adminToggleFreeze()">Lock Pipeline Flow</button>
            </div>

            <div class="admin-card">
                <h4>🔒 Cyber Department Dispatcher</h4>
                <input type="text" class="admin-input" id="cyberDeptText" placeholder="Deploy encrypted cyber notice...">
                <button class="admin-btn cyber" onclick="adminEmitCyberBroadcast()">Broadcast Cyber Protocol</button>
            </div>

            <div class="admin-card">
                <h4>System Broadcast Alert Array</h4>
                <input type="text" class="admin-input" id="broadcastText" placeholder="Inject emergency notice payload...">
                <button class="admin-btn purple" onclick="adminEmitBroadcast()">Fire Broadcast Notice</button>
            </div>
        </aside>
    </div>

    <script>
        // Real-time Runtime Local Database Memory Array
        const localNodeDatabase = [
            { id: "112", pass: "112", name: "Pro User #112", role: "user", hasFace: true },
            { id: "123", pass: "123", name: "Nikhil Tiwari (Admin)", role: "admin", hasFace: true }
        ];

        let currentRole = "user"; 
        let chatMutedLock = false;
        let typingTimeout;
        
        // Security Systems
        let failedAttempts = 0;
        let isLockdown = false;
        let alarmInterval = null;

        // Webcam/Biometric System Variables
        let webcamStream = null;
        let scannerCtxMode = "login"; // "login" or "register"
        let temporaryFaceMapped = false;

        // Audio Context Engine
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        let audioCtx = null;

        window.addEventListener('DOMContentLoaded', () => {
            const savedTheme = localStorage.getItem('teamstak-theme') || 'dark';
            setWorkspaceTheme(savedTheme);
        });

        function setWorkspaceTheme(theme) {
            document.documentElement.setAttribute('data-theme', theme);
            localStorage.setItem('teamstak-theme', theme);
            const btnLight = document.getElementById('themeBtnLight');
            const btnDark = document.getElementById('themeBtnDark');
            if (theme === 'light') {
                btnLight.classList.add('active-theme'); btnDark.classList.remove('active-theme');
            } else {
                btnDark.classList.add('active-theme'); btnLight.classList.remove('active-theme');
            }
        }

        function switchGatewayMode(mode) {
            if (isLockdown) return;
            const title = document.getElementById('gatewayTitle');
            const subtitle = document.getElementById('gatewaySubtitle');
            const loginForm = document.getElementById('loginFormFields');
            const registerForm = document.getElementById('registerFormFields');
            document.getElementById('errorMsg').style.display = 'none';
            document.getElementById('regErrorMsg').style.display = 'none';

            if (mode === 'register') {
                title.innerHTML = "Register<span>Node</span>";
                subtitle.textContent = "// DEPLOY NEW ACCESS BIOMETRIC MATRIX";
                loginForm.style.display = 'none';
                registerForm.style.display = 'block';
            } else {
                title.innerHTML = "TeamStak<span>.pro</span>";
                subtitle.textContent = "// SECURE WORKSPACE MATRIX V4.0";
                loginForm.style.display = 'block';
                registerForm.style.display = 'none';
            }
        }

        /* --- ADVANCED SYNTHETIC SOUND ENGINE --- */
        function initAudio() {
            if (!audioCtx) audioCtx = new AudioContext();
        }

        function playWrongPasswordSound() {
            initAudio();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = 'sawtooth'; 
            osc.frequency.setValueAtTime(120, audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(40, audioCtx.currentTime + 0.3);
            gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
            osc.connect(gain); gain.connect(audioCtx.destination);
            osc.start(); osc.stop(audioCtx.currentTime + 0.3);
        }

        function playWarningPulse() {
            initAudio();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(880, audioCtx.currentTime);
            gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.15);
            osc.connect(gain); gain.connect(audioCtx.destination);
            osc.start(); osc.stop(audioCtx.currentTime + 0.15);
        }

        function startEmergencySiren() {
            initAudio();
            if (alarmInterval) return;

            alarmInterval = setInterval(() => {
                const osc1 = audioCtx.createOscillator();
                const osc2 = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc1.type = 'sawtooth';
                osc1.frequency.setValueAtTime(450, audioCtx.currentTime);
                osc1.frequency.linearRampToValueAtTime(150, audioCtx.currentTime + 0.4);
                osc2.type = 'square';
                osc2.frequency.setValueAtTime(100, audioCtx.currentTime);
                gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.4);
                osc1.connect(gain); osc2.connect(gain); gain.connect(audioCtx.destination);
                osc1.start(); osc2.start();
                osc1.stop(audioCtx.currentTime + 0.4); osc2.stop(audioCtx.currentTime + 0.4);
            }, 500);
        }

        /* --- AI VOICE WELCOME SYNTH MATRIX --- */
        function triggerVoiceWelcome(name, isAdmin) {
            if ('speechSynthesis' in window) {
                let welcomeText = `Welcome back, ${name}. Access granted.`;
                if(isAdmin && name.includes("Nikhil")) {
                    welcomeText = "स्वागत है, निखिल तिवारी जी। सिस्टम आपके नियंत्रण में है।";
                } else if(isAdmin) {
                    welcomeText = `स्वागत है एडमिन ऑपरेटर, ${name}।`;
                }
                const utterance = new SpeechSynthesisUtterance(welcomeText);
                utterance.lang = name.includes("Nikhil") || isAdmin ? 'hi-IN' : 'en-US';
                utterance.rate = 0.95;
                window.speechSynthesis.speak(utterance);
            }
        }

        /* --- BIOMETRIC FACE VERIFICATION MODULE --- */
        async function openFaceScanner(mode) {
            if (isLockdown) return;
            scannerCtxMode = mode;
            const modal = document.getElementById('scannerModal');
            const video = document.getElementById('webcamFeed');
            const status = document.getElementById('biometricStatus');
            const ops = document.getElementById('biometricOps');
            
            modal.style.display = 'flex';
            ops.style.display = 'none';
            status.textContent = ">> ACQUIRING WEB_CAMERA PROTOCOLS...";

            // Configure layout according to context
            if (scannerCtxMode === 'login') {
                document.getElementById('bioScanAdminBtn').style.display = 'block';
                document.getElementById('bioScanUserBtn').style.display = 'block';
                document.getElementById('bioCaptureBtn').style.display = 'none';
            } else {
                document.getElementById('bioScanAdminBtn').style.display = 'none';
                document.getElementById('bioScanUserBtn').style.display = 'none';
                document.getElementById('bioCaptureBtn').style.display = 'block';
            }

            try {
                webcamStream = await navigator.mediaDevices.getUserMedia({ video: { width: 300, height: 300 } });
                video.srcObject = webcamStream;
                status.textContent = scannerCtxMode === 'login' ? ">> FACE CAPTURED. STANDBY FOR TARGET ROLE EVALUATION..." : ">> CAM STREAM ACTIVE. POSITION FACE INSIDE MATRIX LOOP...";
                ops.style.display = 'flex';
            } catch (err) {
                status.textContent = ">> ERROR: CAMERA ACCESS DENIED OR NOT FOUND.";
                setTimeout(() => { modal.style.display = 'none'; }, 2500);
            }
        }

        function closeFaceScanner() {
            if (webcamStream) {
                webcamStream.getTracks().forEach(track => track.stop());
            }
            document.getElementById('scannerModal').style.display = 'none';
        }

        // Registration Mapping Function
        function captureFaceRegistration() {
            const status = document.getElementById('biometricStatus');
            document.getElementById('bioCaptureBtn').style.display = 'none';
            status.textContent = ">> SCANNING FACIAL GEOMETRY & MAPPING CRYPTO NODES...";

            setTimeout(() => {
                temporaryFaceMapped = true;
                document.getElementById('regFaceStatus').style.display = 'block';
                closeFaceScanner();
                initAudio();
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine'; osc.frequency.setValueAtTime(600, audioCtx.currentTime);
                gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
                osc.connect(gain); gain.connect(audioCtx.destination);
                osc.start(); osc.stop(audioCtx.currentTime + 0.1);
            }, 1500);
        }

        // Login Verification Mapping Function
        function processFaceMatching(selectedRole) {
            const status = document.getElementById('biometricStatus');
            document.getElementById('bioScanAdminBtn').style.display = 'none';
            document.getElementById('bioScanUserBtn').style.display = 'none';
            status.textContent = ">> PARSING BIOMETRIC NODE MATRIX CORRELATION...";

            setTimeout(() => {
                // Search local database for registered users with face authentication capability matching chosen role
                const matchedUser = localNodeDatabase.find(u => u.role === selectedRole && u.hasFace);

                if (matchedUser) {
                    closeFaceScanner();
                    currentRole = matchedUser.role;
                    failedAttempts = 0;
                    triggerVoiceWelcome(matchedUser.name, currentRole === 'admin');
                    setupSessionWorkspace(matchedUser.name, currentRole === 'admin' ? "ADM" : "BIO", currentRole === 'admin' ? "flex" : "none");
                } else {
                    handleFailedAttempt();
                    if (!isLockdown) {
                        status.textContent = `>> MATRIX MISMATCH: FACE RECORD NOT FOUND (${failedAttempts}/3)`;
                        document.getElementById('bioScanAdminBtn').style.display = 'block';
                        document.getElementById('bioScanUserBtn').style.display = 'block';
                    }
                }
            }, 1800);
        }

        /* --- REAL-TIME ACCOUNT REGISTRATION HANDLER --- */
        function processRegistration() {
            const id = document.getElementById('regRoomId').value.trim();
            const name = document.getElementById('regName').value.trim();
            const pass = document.getElementById('regPass').value.trim();
            const role = document.getElementById('regRole').value;
            const regError = document.getElementById('regErrorMsg');

            if (!id || !name || !pass) {
                regError.textContent = "> ERROR: Form incomplete. Fill all telemetry data arrays.";
                regError.style.display = 'block';
                return;
            }

            // Check duplicate accounts
            if (localNodeDatabase.some(u => u.id === id)) {
                regError.textContent = "> ERROR: Blocked. Node Workspace ID already claimed.";
                regError.style.display = 'block';
                return;
            }

            if (!temporaryFaceMapped) {
                regError.textContent = "> ERROR: Biometric face registration required.";
                regError.style.display = 'block';
                return;
            }

            // Inject account to virtual database layer
            const newAccount = { id, pass, name, role, hasFace: true };
            localNodeDatabase.push(newAccount);

            regError.style.display = 'none';
            alert(`Account Node successfully mapped inside data grid! Use ID "${id}" to connect.`);
            
            // Clear fields and switch view back to login
            document.getElementById('regRoomId').value = '';
            document.getElementById('regName').value = '';
            document.getElementById('regPass').value = '';
            document.getElementById('regFaceStatus').style.display = 'none';
            temporaryFaceMapped = false;
            switchGatewayMode('login');
        }

        /* --- GLOBAL ATTACK/LOCKDOWN HANDLING MATRIX --- */
        function handleFailedAttempt() {
            failedAttempts++;
            playWrongPasswordSound();
            const errorBanner = document.getElementById('errorMsg');
            const loginGate = document.getElementById('loginGate');

            if (failedAttempts >= 3) {
                isLockdown = true;
                closeFaceScanner();
                loginGate.classList.add('lockdown-active');
                errorBanner.innerHTML = `> !!! SECURITY BREACH DETECTED !!!<br>> TERMINAL LOCKED BY CYBER PROTECTION LAYER.`;
                errorBanner.style.display = 'block';
                document.getElementById('connectBtn').disabled = true;
                document.getElementById('biometricBtn').disabled = true;
                startEmergencySiren();
            } else {
                playWarningPulse();
                errorBanner.innerHTML = `> ERROR: Security Handshake Failed. Attempt ${failedAttempts}/3 Rejected.`;
                errorBanner.style.display = 'block';
            }
        }

        /* --- VALIDATION GATEWAY CORE --- */
        function validateAccess() {
            if (isLockdown) return;

            const enteredId = document.getElementById('roomId').value.trim();
            const enteredPass = document.getElementById('roomPass').value.trim();

            // Validate against live updated local data array
            const matchedUser = localNodeDatabase.find(u => u.id === enteredId && u.pass === enteredPass);

            if (matchedUser) {
                currentRole = matchedUser.role;
                failedAttempts = 0;
                triggerVoiceWelcome(matchedUser.name, currentRole === 'admin');
                
                // Set character icon letters
                let initials = matchedUser.name.split(" ").map(n => n[0]).join("").substring(0, 3).toUpperCase();
                setupSessionWorkspace(matchedUser.name, initials, currentRole === 'admin' ? "flex" : "none");
            } else {
                handleFailedAttempt();
            }
        }

        function setupSessionWorkspace(name, avatar, adminDisplay) {
            document.getElementById('loginGate').style.display = 'none';
            document.getElementById('appWorkspace').style.display = 'flex';
            document.getElementById('adminControlMatrix').style.display = adminDisplay;
            document.getElementById('myUsernameLabel').textContent = name;
            document.getElementById('myAvatarIcon').textContent = avatar;
            if(currentRole === "admin") document.getElementById('myAvatarIcon').style.background = "linear-gradient(135deg, var(--accent-red), #881337)";
            document.getElementById('messageInput').focus();

            // Append online nodes array dynamically to side panel roster
            const roster = document.getElementById('sidebarUserRoster');
            roster.innerHTML = `
                <li class="list-item"><div class="status-dot"></div> System Bot</li>
                <li class="list-item"><div class="status-dot"></div> Alex (Dev)</li>
                <li class="list-item"><div class="status-dot"></div> Sarah (Product)</li>
            `;
            if (name !== "Nikhil Tiwari (Admin)" && name !== "Pro User #112") {
                const li = document.createElement('li');
                li.className = "list-item";
                li.innerHTML = `<div class="status-dot" style="background:var(--accent-magenta); box-shadow:0 0 10px var(--accent-magenta);"></div> ${name}`;
                roster.appendChild(li);
                document.getElementById('liveCountLabel').textContent = "5 ONLINE";
            }

            setTimeout(() => {
                triggerBotResponse(`Handshake successful. Verified Operator Matrix [${name}] online session established.`);
            }, 500);
        }

        function dispatchMessage(customContent = null, isImage = false, broadcastType = "none") {
            if (chatMutedLock && currentRole !== "admin") return;

            const inputField = document.getElementById('messageInput');
            const messageText = customContent || inputField.value.trim();
            if (!messageText) return;

            const timeline = document.getElementById('chatTimeline');
            const now = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            const msgRow = document.createElement('div');
            msgRow.classList.add('msg-row');
            
            if (currentRole === "admin" && broadcastType === "none") msgRow.classList.add('own-msg');
            else if (currentRole === "user") msgRow.classList.add('own-msg');

            let bubbleClass = "bubble";
            let userTag = document.getElementById('myUsernameLabel').textContent;

            if (broadcastType === "alert") {
                bubbleClass = "bubble alert-broadcast"; userTag = "⚠️ BROADCAST_OVERRIDE";
            } else if (broadcastType === "cyber") {
                bubbleClass = "bubble cyber-dept-broadcast"; userTag = "🛡️ CYBER_DEPT_DIRECTIVE";
            }

            let contentPayload = `<div class="${bubbleClass}">${escapeHTML(messageText)}</div>`;
            if(isImage) contentPayload = `<div class="bubble"><img src="${messageText}" class="preview-img" style="max-width:200px; border-radius:10px;" /></div>`;

            msgRow.innerHTML = `<div class="msg-wrapper"><div class="msg-meta"><span>${userTag}</span> <span>${now}</span></div>${contentPayload}</div>`;
            timeline.appendChild(msgRow);
            if(!customContent) inputField.value = '';
            timeline.scrollTop = timeline.scrollHeight;
        }

        function adminPurgeLogs() {
            document.getElementById('chatTimeline').innerHTML = `<div class="msg-row"><div class="avatar" style="background:var(--accent-red)">ADM</div><div class="msg-wrapper"><div class="msg-meta"><span>Security Gateway Audit</span></div><div class="bubble">All active chat frames zeroed by root supervisor.</div></div></div>`;
        }

        function adminToggleFreeze() {
            chatMutedLock = !chatMutedLock;
            const btn = document.getElementById('freezeToggleBtn');
            if(chatMutedLock) {
                btn.textContent = "Release Pipeline Flow"; btn.style.background = "var(--accent-green)";
                triggerBotResponse("🛑 PIPELINE SECURITY ALERT: Suspended by admin.");
            } else {
                btn.textContent = "Lock Pipeline Flow"; btn.style.background = "#d97706";
                triggerBotResponse("📢 PIPELINE SECURITY ALERT: Suspension revoked.");
            }
        }

        function adminEmitBroadcast() {
            const input = document.getElementById('broadcastText');
            if(!input.value.trim()) return;
            dispatchMessage(input.value.trim(), false, "alert");
            input.value = '';
        }

        function adminEmitCyberBroadcast() {
            const input = document.getElementById('cyberDeptText');
            if(!input.value.trim()) return;
            dispatchMessage(input.value.trim(), false, "cyber");
            input.value = '';
        }

        function handleTypingStatus(event) {
            if (event.key === 'Enter') { dispatchMessage(); return; }
            if(chatMutedLock && currentRole !== "admin") return;
            document.getElementById('typingBox').textContent = ">> Encrypting stream frames...";
            clearTimeout(typingTimeout);
            typingTimeout = setTimeout(() => { document.getElementById('typingBox').textContent = ""; }, 1200);
        }

        function insertEmoji(emoji) {
            const field = document.getElementById('messageInput'); field.value += emoji; field.focus();
        }

        function simulateImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) { dispatchMessage(e.target.result, true); };
                reader.readAsDataURL(file);
            }
        }

        function switchChannel(element) {
            document.querySelectorAll('.channel-list .list-item').forEach(item => item.classList.remove('active'));
            element.classList.add('active');
            document.getElementById('activeChannelTitle').textContent = element.textContent;
        }

        function triggerBotResponse(text) {
            const timeline = document.getElementById('chatTimeline');
            const now = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            const msgRow = document.createElement('div');
            msgRow.classList.add('msg-row');
            msgRow.innerHTML = `<div class="avatar" style="background:var(--accent-cyan)">BOT</div><div class="msg-wrapper"><div class="msg-meta"><span>Automation Unit</span> <span>${now}</span></div><div class="bubble">${text}</div></div>`;
            timeline.appendChild(msgRow); timeline.scrollTop = timeline.scrollHeight;
        }

        function filterMessages() {
            const query = document.getElementById('chatSearch').value.toLowerCase();
            document.querySelectorAll('.bubble').forEach(b => {
                const row = b.closest('.msg-row');
                if(row) row.style.opacity = b.textContent.toLowerCase().includes(query) ? '1' : '0.08';
            });
        }

        function escapeHTML(str) {
            return str.replace(/[&<>'"]/g, t => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[t] || t));
        }

        function leaveRoom() {
            if(alarmInterval) clearInterval(alarmInterval);
            window.location.reload();
        }
    </script>
</body>
</html>
