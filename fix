<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
    <title>Clash Of Bakid</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Philosopher:wght@700&family=Poppins:wght@400;500;700&family=Noto+Naskh+Arabic:wght@700&family=Cairo+Play:wght@400;700&display=swap" rel="stylesheet">
    
    <link rel='stylesheet' href='https://cdn-uicons.flaticon.com/2.4.2/uicons-solid-rounded/css/uicons-solid-rounded.css'>

    <style>
        :root {
            --safe-area-inset-top: env(safe-area-inset-top, 0px);
            --safe-area-inset-right: env(safe-area-inset-right, 0px);
            --safe-area-inset-bottom: env(safe-area-inset-bottom, 0px);
            --safe-area-inset-left: env(safe-area-inset-left, 0px);
        }
        body, html {
            font-family: 'Poppins', sans-serif;
            -webkit-tap-highlight-color: transparent;
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
            overflow: hidden; /* Ini sengaja ada untuk mencegah body scroll */
            background-color: #F7F7F7;
            overscroll-behavior-y: contain; /* [FIX] Ini mencegah 'pull-to-refresh' di browser mobile */
        }
        .font-philosopher { font-family: 'Philosopher', sans-serif; }
        .font-inter { font-family: 'Inter', sans-serif; }
        .font-arabic { font-family: 'Traditional Arabic', serif; font-weight: 800; }
        .font-cairo-play { font-family: 'Cairo Play', sans-serif; }
        .safe-top-left { top: var(--safe-area-inset-top); left: var(--safe-area-inset-left); }
        .safe-top-right { top: var(--safe-area-inset-top); right: var(--safe-area-inset-right); }

        /* --- Global Styles --- */
        .gradient-bg { position: absolute; top: 0; left: 0; width: 100%; height: 100%; overflow: hidden; filter: blur(80px) saturate(1.15); z-index: 0; }
        .gradient-blob { position: absolute; border-radius: 50%; opacity: 0.7; will-change: transform, translate; }
        .blob-1 { width: 360px; height: 360px; background-color: rgba(209,213,219,0.85); animation: move1 20s infinite alternate ease-in-out; }
        .blob-2 { width: 480px; height: 480px; background-color: rgba(0,105,234,0.38); animation: move2 36s infinite alternate-reverse ease-in-out; }
        @keyframes move1 { from { transform: translate(-80px, -50px) scale(1); } to { transform: translate(calc(100vw - 320px), calc(100vh - 300px)) scale(1.03); } }
        @keyframes move2 { from { transform: translate(calc(100vw - 200px), 50px) scale(1.05); } to { transform: translate(50px, calc(100vh - 400px)) scale(1); } }
        
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px) scale(0.98); } to { opacity: 1; transform: translateY(0) scale(1); } }
        @keyframes fadeInDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
        .animate-fade-in-up { animation: fadeInUp 0.5s ease-out forwards; }
        .animate-fade-in-down { animation: fadeInDown 0.4s ease-out forwards; }
        .initial-state { 
            opacity: 0; 
            will-change: transform, opacity;
        }

        /* --- Login Page Styles --- */
        .focus-style:focus { outline: none; box-shadow: 0 0 0 3px rgba(0, 105, 234, 0.28); border-color: #0069EA; }
        .dot-spinner { display: none; justify-content: center; gap: 6px; margin-top: 8px; }
        .dot-spinner .dot { width: 8px; height: 8px; border-radius: 50%; background: #0069EA; opacity: 0.95; transform: scale(0.6); animation: dotPulse 1s infinite cubic-bezier(.2,.68,.18,1.08); }
        .dot-spinner .dot.d1 { animation-delay: 0s; }
        .dot-spinner .dot.d2 { animation-delay: 0.12s; }
        .dot-spinner .dot.d3 { animation-delay: 0.24s; }
        @keyframes dotPulse { 0%, 100% { transform: scale(0.6); opacity: 0.6; } 50% { transform: scale(1.0); opacity: 1; } }
        .popup-mini { margin-top: 12px; text-align: center; padding: 10px 14px; border-radius: 10px; font-size: 0.95rem; font-weight: 600; display: none; transition: all 0.28s ease; opacity: 0; transform: translateY(-10px); }
        .popup-mini.show { display: block; opacity: 1; transform: translateY(0); }
        .popup-mini.success { background: rgba(0,105,234,0.12); color: #0069EA; }
        .popup-mini.error { background: rgba(220,38,38,0.08); color: #dc2626; }

        /* --- Menu Page Styles --- */
        @keyframes shine { 100% { left: 150%; } }
        .shine-effect { position: relative; overflow: hidden; }
        .shine-effect::before { content: ''; position: absolute; top: 0; left: -150%; width: 75%; height: 100%; background: linear-gradient(to right, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 0.4) 50%, rgba(255, 255, 255, 0) 100%); transform: skewX(-25deg); animation: shine 5s infinite ease-in-out; }
        .card-wrapper:nth-of-type(1) .shine-effect::before { animation-delay: 0s; }
        .card-wrapper:nth-of-type(2) .shine-effect::before { animation-delay: 0.7s; }
        .card-wrapper:nth-of-type(3) .shine-effect::before { animation-delay: 0.2s; }
        .card-wrapper:nth-of-type(4) .shine-effect::before { animation-delay: 1.1s; }
        @keyframes rotate { 100% { transform: rotate(1turn); } }
        .animated-border-container { 
            position: relative; 
            padding: 3px; 
            overflow: hidden; 
            border-radius: 1rem; 
            z-index: 1; 
            transform-style: preserve-3d; 
            transition: transform 0.2s ease-out;
            will-change: transform;
        }
        .animated-border-container::before { content: ''; position: absolute; z-index: -1; left: -50%; top: -50%; width: 200%; height: 200%; background: conic-gradient(transparent, #D1D5DB, #9CA3AF, #D1D5DB, transparent 40%); animation: rotate 6s linear infinite; }
        
        /* --- Memorize Page Styles & Padlock Page Styles --- */
        .numbers-bg { position: absolute; top: 0; left: 0; width: 100%; height: 100%; overflow: hidden; z-index: 1; pointer-events: none; }
        .number-item {
            position: absolute;
            color: white;
            font-weight: 700;
            animation-timing-function: linear;
            animation-iteration-count: infinite;
            will-change: transform;
        }
        input[type=number]::-webkit-inner-spin-button, 
        input[type=number]::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
        input[type=number] { -moz-appearance: textfield; }

        #memorize-card, #padlock-card {
            transition: box-shadow 0.4s ease-in-out;
        }
        #memorize-card.correct, #padlock-card.correct {
            box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.5), 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05);
        }
        #memorize-card.incorrect, #padlock-card.incorrect {
            box-shadow: 0 0 0 4px rgba(239, 68, 68, 0.5), 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05);
        }
        .result-message {
            text-align: center;
            font-weight: 600;
            font-size: 1.1rem;
            padding: 10px;
            border-radius: 8px;
            margin-bottom: 1rem;
            display: none;
            opacity: 0;
            transform: translateY(10px);
            transition: opacity 0.3s ease, transform 0.3s ease;
        }
        .result-message.show {
            display: block;
            opacity: 1;
            transform: translateY(0);
        }
        .result-message.correct {
            background-color: rgba(34, 197, 94, 0.1);
            color: #16a34a;
        }
        .result-message.incorrect {
            background-color: rgba(239, 68, 68, 0.1);
            color: #ef4444;
        }
        @keyframes shake {
            10%, 90% { transform: translateX(-1px); }
            20%, 80% { transform: translateX(2px); }
            30%, 50%, 70% { transform: translateX(-4px); }
            40%, 60% { transform: translateX(4px); }
        }
        .shake-anim {
            animation: shake 0.6s cubic-bezier(.36,.07,.19,.97) both;
        }

        /* --- Card Game & General Game Styles --- */
        .background-items { position: absolute; top: 0; left: 0; width: 100%; height: 100%; overflow: hidden; z-index: 1; pointer-events: none; }
        .floating-card {
            position: absolute; animation-timing-function: linear; animation-iteration-count: infinite; will-change: transform;
            background-color: rgba(255, 255, 255, 0.75); border-radius: 6px; border: 1px solid rgba(255, 255, 255, 0.8);
        }
        @keyframes drift-1 { from { transform: translate(0vw, 0vh) rotate(0deg); } to { transform: translate(-80vw, -60vh) rotate(-720deg); } }
        @keyframes drift-2 { from { transform: translate(0vw, 0vh) rotate(0deg); } to { transform: translate(70vw, 50vh) rotate(360deg); } }
        @keyframes drift-3 { from { transform: translate(0vw, 0vh) rotate(0deg); } to { transform: translate(-60vw, 90vh) rotate(-180deg); } }
        @keyframes drift-4 { from { transform: translate(0vw, 0vh) rotate(0deg); } to { transform: translate(90vw, -70vh) rotate(540deg); } }
        
        #card-screen #game-container, #puzzle-screen #game-container {
            display: flex; flex-direction: column; align-items: center; gap: 1.5rem; 
            width: 100%; height: 100%; justify-content: center;
        }
        
        #card-screen #message-box, #puzzle-screen #message-box {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(0.9);
            background-color: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px);
            padding: 30px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            text-align: center; z-index: 100; opacity: 0; visibility: hidden;
            transition: opacity 0.3s, transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1), visibility 0.3s;
        }
        #card-screen #message-box.show, #puzzle-screen #message-box.show {
            opacity: 1; visibility: visible; transform: translate(-50%, -50%) scale(1);
        }
        
        /* Card Game Specific */
        #card-screen #game-board {
            display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 10px; max-width: 90vw;
        }
        #card-screen #answer-board-container { width: 100%; display: flex; justify-content: center; }
        #card-screen #answer-board {
            display: flex; flex-wrap: nowrap; overflow-x: auto; gap: 10px; padding: 10px;
            background: rgba(255,255,255,0.2); border-radius: 15px; border: 1px solid rgba(255,255,255,0.3);
            max-width: 90vw; -ms-overflow-style: none; scrollbar-width: none;
        }
        #card-screen #answer-board::-webkit-scrollbar { display: none; }
        #card-screen .answer-slot, #card-screen .card {
            width: clamp(60px, 18vw, 75px); height: calc(clamp(60px, 18vw, 75px) * 1.4);
            flex-shrink: 0; border-radius: 10px;
        }
        #card-screen .answer-slot {
            background: rgba(0,0,0,0.1); border: 2px dashed rgba(0, 105, 234, 0.4);
            display: flex; align-items: center; justify-content: center;
        }
        #card-screen .answer-slot.animated-slot {
            border: none; position: relative; z-index: 1; overflow: hidden; background: transparent;
        }
        #card-screen .answer-slot.animated-slot::before {
            content: ''; position: absolute; z-index: -2; left: -50%; top: -50%;
            width: 200%; height: 200%; background: conic-gradient(transparent, #0069EA, #5ca0f7, #0069EA, transparent 50%);
            animation: rotate 5s linear infinite;
        }
        #card-screen .answer-slot.animated-slot::after {
            content: ''; position: absolute; z-index: -1; left: 2px; top: 2px;
            width: calc(100% - 4px); height: calc(100% - 4px); background: rgba(0,0,0,0.1); border-radius: 8px;
        }
        #card-screen .card {
            background-color: #fff; cursor: pointer; transition: transform 0.2s, opacity 0.3s;
            display: flex; align-items: center; justify-content: center; font-size: clamp(1rem, 4vw, 1.3rem);
            box-shadow: 0 4px 15px rgba(0,0,0,0.15); background: linear-gradient(135deg, #ffffff, #e0e7ff);
            color: #1e3a8a; border: 2px solid white; padding: 5px; text-align: center; line-height: 1.2; 
        }
        #card-screen .card:active { transform: scale(0.95); }
        #card-screen .card.is-chosen { opacity: 0.3; pointer-events: none; }
        #card-screen .answer-slot .card {
            cursor: pointer; background: linear-gradient(145deg, #0069EA, hwb(236 2% 12%));
            color: white; border: none; box-shadow: 0 5px 20px rgba(0, 105, 234, 0.4);
        }

        /* --- Puzzle Game Styles --- */
        #puzzle-screen #game-container {
             justify-content: space-evenly;
             padding-bottom: max(1.5rem, var(--safe-area-inset-bottom));
             gap: 1.5rem;
        }
        #puzzle-screen #answer-board-container {
            width: 90%; flex-grow: 1; display: flex; align-items: center; justify-content: center;
        }
        #puzzle-screen #answer-board {
            width: 100%; min-height: 100px; background: rgba(255, 255, 255, 0.5);
            border-radius: 12px; border: 1px solid rgba(255,255,255,0.7);
            padding: 1rem; color: #0069EA; font-size: clamp(1.2rem, 5vw, 1.8rem);
            line-height: 1.6; display: block; overflow-y: auto; text-align: right; direction: rtl;
        }
        #puzzle-screen #game-board {
            display: grid;
            /* grid-template-columns: repeat(3, 1fr); <-- DIHAPUS, akan di-set oleh JS */
            gap: 6px; /* DIUBAH dari 8px agar lebih muat */
            width: 90vw;
            max-width: 400px;
            margin: 0 auto;
            padding: 0;
        }
        #puzzle-screen .key-button {
            background: linear-gradient(145deg, #0069EA, #0058c2);
            border: none;
            border-radius: 8px;
            padding: 10px 4px; /* DIUBAH dari 14px 5px agar lebih ramping */
            box-shadow: 0 4px 10px rgba(0, 88, 194, 0.3), inset 0 1px 1px rgba(255,255,255,0.2);
            font-size: clamp(0.85rem, 3.5vw, 1.1rem); /* DIUBAH agar font sedikit lebih kecil */
            color: white;
            transition: all 0.15s ease-out;
        }
        #puzzle-screen .key-button:active { 
            transform: scale(0.96);
            box-shadow: 0 2px 5px rgba(0, 88, 194, 0.4);
        }
        #puzzle-screen .key-button:disabled { 
            background: #9ca3af;
            opacity: 0.6;
            pointer-events: none;
            box-shadow: none;
        }
        #puzzle-screen .backspace-key {
             background: rgba(239, 68, 68, 0.8);
             box-shadow: 0 4px 10px rgba(220, 38, 38, 0.3);
        }
        #puzzle-screen .backspace-key:active {
            background: rgba(220, 38, 38, 1);
            box-shadow: 0 2px 5px rgba(220, 38, 38, 0.4);
        }
        
        /* Padlock Specific */
        @keyframes blinking-text { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
        .animate-blinking { animation: blinking-text 0.5s ease-in-out 6; }
        
        /* --- Aturan CSS Responsif --- */
        @media (orientation: landscape) and (max-height: 500px) {
            .font-philosopher { font-size: 2rem; }
            #login-screen .w-full.max-w-sm, #memorize-screen .w-full.max-w-sm { padding: 1.25rem; }
            #loginForm { margin-top: 0.75rem; margin-bottom: 0.75rem; }
            #loginForm > :not([hidden]) ~ :not([hidden]) { margin-top: 0.75rem; margin-bottom: 0.75rem; }
            #menu-screen header, #card-screen header, #puzzle-screen header, #padlock-screen header { padding: 0.75rem 1rem; }
            #menu-screen main, #card-screen main, #puzzle-screen main, #padlock-screen main { padding-bottom: 1rem; padding-top: 0.5rem; flex-grow: 1; }
            #menu-screen .fi { font-size: 3rem !important; }
            #menu-screen .shine-effect { padding: 0.75rem; }
            #card-screen .relative.z-10, #puzzle-screen .relative.z-10, #padlock-screen .relative.z-10 { overflow-y: auto; }
            #card-screen #game-container, #puzzle-screen #game-container { gap: 1rem; }
            #card-screen .card, #card-screen .answer-slot {
                width: clamp(55px, 15vh, 65px);
                height: calc(clamp(55px, 15vh, 65px) * 1.4);
                font-size: clamp(0.8rem, 3vh, 1rem);
            }
        }
    </style>
</head>
<body class="w-screen h-screen overflow-hidden relative">
    <!-- Gradient background -->
    <div class="gradient-bg">
        <div class="gradient-blob blob-1"></div>
        <div class="gradient-blob blob-2"></div>
    </div>

    <!-- Login Screen -->
    <div id="login-screen" class="relative z-10 w-full h-full flex items-center justify-center p-4 overflow-y-auto">
        <div class="w-full max-w-sm bg-white/70 backdrop-blur-xl rounded-2xl shadow-2xl p-6 sm:p-8 animate-fade-in-up">
            <div class="text-center mb-6 sm:mb-8">
                <h1 class="font-philosopher font-bold text-4xl sm:text-5xl" style="line-height: 1.1; color: #0069EA;">Clash Of Bakid</h1>
            </div>
            <form id="loginForm" class="space-y-5 sm:space-y-6" autocomplete="off" spellcheck="false">
                <div>
                    <label for="id_user" class="text-sm font-medium text-gray-700">ID User</label>
                    <input type="text" id="id_user" name="id_user" required inputmode="numeric" pattern="[0-9]*" class="mt-1 block w-full px-4 py-3 bg-white/50 border border-gray-300 rounded-lg shadow-sm placeholder-gray-400 transition duration-150 ease-in-out focus-style text-base" />
                </div>
                <div>
                    <label for="password" class="text-sm font-medium text-gray-700">Password</label>
                    <input type="password" id="password" name="password" required inputmode="numeric" pattern="[0-9]*" class="mt-1 block w-full px-4 py-3 bg-white/50 border border-gray-300 rounded-lg shadow-sm placeholder-gray-400 transition duration-150 ease-in-out focus-style text-base" />
                    <div id="dotSpinner" class="dot-spinner" aria-hidden="true">
                        <div class="dot d1"></div>
                        <div class="dot d2"></div>
                        <div class="dot d3"></div>
                    </div>
                </div>
                <div>
                    <button type="submit" id="btnSubmit" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-lg text-base sm:text-lg font-medium text-white bg-[#0069EA] hover:bg-blue-800 transition-all transform active:scale-95 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                        Masuk
                    </button>
                </div>
                <div id="popupMini" class="popup-mini" role="status" aria-live="polite"></div>
            </form>
        </div>
    </div>
    
    <!-- Menu Screen -->
    <div id="menu-screen" class="hidden relative z-10 w-full h-full flex-col overflow-y-auto font-inter">
        <header class="relative w-full p-4 sm:p-6 flex justify-between items-start z-20">
            <div id="header-left" class="initial-state flex items-center space-x-3 sm:space-x-4">
                <button id="back-to-login" class="bg-white/70 rounded-full p-2 sm:p-3 shadow-lg transition-all transform active:scale-95 hover:bg-white">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6 text-[#0069EA]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                    </svg>
                </button>
                <div>
                    <h1 class="font-philosopher font-bold tracking-wider text-3xl sm:text-4xl md:text-5xl" style="line-height: 1.1; color: #0069EA;">Clash Of Bakid</h1>
                </div>
            </div>
            <div id="header-right" class="initial-state flex items-center gap-2">
                <div class="bg-white rounded-full p-1.5 sm:p-2 flex items-center space-x-2 sm:space-x-3 shadow-lg">
                    <div class="w-10 h-10 sm:w-12 sm:h-12 bg-blue-200 rounded-full flex items-center justify-center ring-2 ring-white/50 flex-shrink-0">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 sm:h-7 sm:w-7 text-blue-700" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                        </svg>
                    </div>
                    <div class="hidden sm:flex flex-col items-start pr-2 sm:pr-4">
                        <div id="nama-peserta" class="font-bold text-base sm:text-lg font-poppins text-gray-800 leading-tight">Nama Peserta</div>
                        <div id="info-peserta" class="text-xs sm:text-sm font-poppins text-gray-600 leading-tight">Asrama &bull; Kelas</div>
                    </div>
                </div>
            </div>
        </header>
        <main class="w-full flex-grow flex items-center justify-center px-4 sm:px-6 md:px-8 lg:px-12 pb-8">
            <div id="menu-cards-container" class="w-full max-w-4xl mx-auto flex flex-row flex-wrap justify-center gap-3 sm:gap-4 items-start">
                <div id="memorize-card-wrapper" class="initial-state card-wrapper flex flex-col items-center gap-2 w-[48%] md:w-[23%]">
                    <div class="animated-border-container w-full">
                        <div class="shine-effect bg-white rounded-xl shadow-lg p-3 sm:p-5 flex flex-col items-center justify-between aspect-[3/4] text-center w-full">
                            <h3 class="text-base sm:text-xl font-bold font-poppins text-gray-800 flex-shrink-0">MEMORIZE</h3>
                            <div class="flex-grow w-full flex items-center justify-center py-2">
                                <i id="icon-card-1" class="fi fi-sr-brain text-5xl sm:text-7xl" style="color: #0069EA;"></i>
                            </div>
                            <button id="start-memorize" class="w-full text-sm sm:text-base bg-[#0069EA] text-white font-poppins font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-800 transition-all active:scale-95 flex-shrink-0"> Mulai </button>
                        </div>
                    </div>
                    <p class="font-poppins text-gray-600 text-xs sm:text-sm">Babak Pertama</p>
                </div>
                <div id="card-card-wrapper" class="initial-state card-wrapper flex flex-col items-center gap-2 w-[48%] md:w-[23%]">
                    <div class="animated-border-container w-full">
                        <div class="shine-effect bg-white rounded-xl shadow-lg p-3 sm:p-5 flex flex-col items-center justify-between aspect-[3/4] text-center w-full">
                            <h3 class="text-base sm:text-xl font-bold font-poppins text-gray-800 flex-shrink-0">CARD</h3>
                            <div class="flex-grow w-full flex items-center justify-center py-2">
                                <i id="icon-card-2" class="fi fi-sr-game text-5xl sm:text-7xl" style="color: #0069EA;"></i>
                            </div>
                            <button id="start-card" class="w-full text-sm sm:text-base bg-[#0069EA] text-white font-poppins font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-800 transition-all active:scale-95 flex-shrink-0"> Mulai </button>
                        </div>
                    </div>
                    <p class="font-poppins text-gray-600 text-xs sm:text-sm">Babak II Tahap I</p>
                </div>
                <div id="puzzle-card-wrapper" class="initial-state card-wrapper flex flex-col items-center gap-2 w-[48%] md:w-[23%]">
                    <div class="animated-border-container w-full">
                        <div class="shine-effect bg-white rounded-xl shadow-lg p-3 sm:p-5 flex flex-col items-center justify-between aspect-[3/4] text-center w-full">
                            <h3 class="text-base sm:text-xl font-bold font-poppins text-gray-800 flex-shrink-0">PUZZLE</h3>
                            <div class="flex-grow w-full flex items-center justify-center py-2">
                                <i id="icon-card-3" class="fi fi-sr-insight text-5xl sm:text-7xl" style="color: #0069EA;"></i>
                            </div>
                            <button id="start-puzzle" class="w-full text-sm sm:text-base bg-[#0069EA] text-white font-poppins font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-800 transition-all active:scale-95 flex-shrink-0"> Mulai </button>
                        </div>
                    </div>
                    <p class="font-poppins text-gray-600 text-xs sm:text-sm">Babak II Tahap II</p>
                </div>
                <div id="padlock-card-wrapper" class="initial-state card-wrapper flex flex-col items-center gap-2 w-[48%] md:w-[23%]">
                    <div class="animated-border-container w-full">
                        <div class="shine-effect bg-white rounded-xl shadow-lg p-3 sm:p-5 flex flex-col items-center justify-between aspect-[3/4] text-center w-full">
                            <h3 class="text-base sm:text-xl font-bold font-poppins text-gray-800 flex-shrink-0">PADLOCK</h3>
                            <div class="flex-grow w-full flex items-center justify-center py-2">
                                <i id="icon-card-4" class="fi fi-sr-binary-lock text-5xl sm:text-7xl" style="color: #0069EA;"></i>
                            </div>
                            <button id="start-padlock" class="w-full text-sm sm:text-base bg-[#0069EA] text-white font-poppins font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-800 transition-all active:scale-95 flex-shrink-0"> Mulai </button>
                        </div>
                    </div>
                    <p class="font-poppins text-gray-600 text-xs sm:text-sm">Grand Final Tahap I</p>
                </div>
            </div>
        </main>
    </div>
    
    <!-- Memorize Screen -->
    <div id="memorize-screen" class="hidden relative z-20 w-full h-full flex-col font-inter">
        <canvas id="numbers-canvas" class="numbers-bg"></canvas>
        <div class="relative z-10 w-full h-full flex flex-col overflow-y-auto p-4 sm:p-6">
            <header class="w-full flex justify-between items-center z-20 flex-shrink-0">
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <button id="back-to-menu-from-memorize" class="bg-white/70 rounded-full p-2 sm:p-3 shadow-lg transition-all transform active:scale-95 hover:bg-white">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6 text-[#0069EA]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                        </svg>
                    </button>
                    <div>
                        <h1 class="font-philosopher font-bold tracking-wider text-3xl sm:text-4xl" style="line-height: 1.1; color: #0069EA;">Memorize</h1>
                        <p class="font-poppins text-gray-600 text-sm sm:text-base">Babak I</p>
                    </div>
                </div>
                <div class="bg-white rounded-full p-1.5 sm:p-2 flex items-center space-x-2 sm:space-x-3 shadow-lg">
                    <div class="w-10 h-10 sm:w-12 sm:h-12 bg-blue-200 rounded-full flex items-center justify-center ring-2 ring-white/50 flex-shrink-0">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 sm:h-7 sm:w-7 text-blue-700" viewBox="0 0 20 20" fill="currentColor">
                           <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                       </svg>
                   </div>
                   <div class="hidden sm:flex flex-col items-start pr-2 sm:pr-4">
                        <div id="memorize-nama-peserta" class="font-bold text-base sm:text-lg font-poppins text-gray-800 leading-tight">Nama Peserta</div>
                        <div id="memorize-info-peserta" class="text-xs sm:text-sm font-poppins text-gray-600 leading-tight">Asrama &bull; Kelas</div>
                   </div>
                </div>
            </header>
            <main class="w-full flex-grow flex items-center justify-center p-4">
                <div id="memorize-card" class="w-full max-w-sm bg-white/70 backdrop-blur-xl rounded-2xl shadow-2xl p-6 sm:p-8 animate-fade-in-up">
                    <form id="memorize-form" class="space-y-4">
                        <div id="memorize-result" class="result-message"></div>
                        <div>
                            <label for="number_input" class="block text-center text-sm sm:text-base font-medium text-gray-700 mb-2">Masukkan Jawaban Anda</label>
                            <input
                                type="text"
                                id="number_input"
                                name="number_input"
                                required
                                inputmode="numeric"
                                pattern="[0-9]*"
                                class="block w-full px-4 py-3 bg-white/50 border border-gray-300 rounded-lg shadow-sm placeholder-gray-400 transition duration-150 ease-in-out focus-style text-center text-3xl sm:text-4xl font-bold tracking-widest"
                                placeholder="0"
                            />
                        </div>
                        <div>
                            <button
                                type="submit"
                                id="memorize-submit-btn"
                                class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-lg text-base sm:text-lg font-medium text-white bg-[#0069EA] hover:bg-blue-800 transition-all transform active:scale-95 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
                            >
                                Kirim
                            </button>
                        </div>
                    </form>
                </div>
            </main>
        </div>
    </div>
    
    <!-- Card Screen -->
    <div id="card-screen" class="hidden relative z-10 w-full h-full flex-col">
        <div id="background-animation" class="background-items"></div>
        <div class="relative z-10 w-full h-full flex flex-col">
            <header class="w-full flex justify-between items-center z-20 flex-shrink-0 p-4 sm:p-6">
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <button id="back-to-menu-from-card" class="bg-white/70 rounded-full p-2 sm:p-3 shadow-lg transition-all transform active:scale-95 hover:bg-white">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6 text-[#0069EA]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                        </svg>
                    </button>
                    <div>
                        <h1 class="font-philosopher font-bold tracking-wider text-3xl sm:text-4xl" style="line-height: 1.1; color: #0069EA;">Card</h1>
                        <p class="font-poppins text-gray-600 text-sm sm:text-base">Babak II Tahap I</p>
                    </div>
                </div>
                <div class="bg-white rounded-full p-1.5 sm:p-2 flex items-center space-x-2 sm:space-x-3 shadow-lg">
                    <div class="w-10 h-10 sm:w-12 sm:h-12 bg-blue-200 rounded-full flex items-center justify-center ring-2 ring-white/50 flex-shrink-0">
                       <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 sm:h-7 sm:w-7 text-blue-700" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                        </svg>
                   </div>
                   <div class="hidden sm:flex flex-col items-start pr-2 sm:pr-4">
                        <div id="card-nama-peserta" class="font-bold text-base sm:text-lg font-poppins text-gray-800 leading-tight">Nama Peserta</div>
                        <div id="card-info-peserta" class="text-xs sm:text-sm font-poppins text-gray-600 leading-tight">Asrama &bull; Kelas</div>
                   </div>
                </div>
            </header>

            <main class="w-full flex-grow flex items-center justify-center p-4">
                <div id="game-container">
                    <div id="answer-board-container">
                        <div id="answer-board"></div>
                    </div>
                    <div id="game-board"></div>
                </div>
            </main>
            
            <div id="message-box">
                <div id="message-icon-container" class="mb-4"></div>
                <h2 id="message-title" class="text-3xl font-bold font-philosopher mb-2"></h2>
                <p id="message-text" class="font-poppins text-gray-700"></p>
            </div>
        </div>
    </div>

    <!-- Puzzle Screen -->
    <div id="puzzle-screen" class="hidden relative z-10 w-full h-full flex-col">
        <div class="absolute top-0 left-0 w-full h-full z-10 pointer-events-none">
             <!-- You can add background elements here if needed -->
        </div>
        <div class="relative z-10 w-full h-full flex flex-col">
            <header class="w-full flex justify-between items-center z-20 flex-shrink-0 p-4 sm:p-6">
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <button id="back-to-menu-from-puzzle" class="bg-white/70 rounded-full p-2 sm:p-3 shadow-lg transition-all transform active:scale-95 hover:bg-white">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6 text-[#0069EA]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                        </svg>
                    </button>
                    <div>
                        <h1 class="font-philosopher font-bold tracking-wider text-3xl sm:text-4xl" style="line-height: 1.1; color: #0069EA;">Puzzle</h1>
                        <p class="font-poppins text-gray-600 text-sm sm:text-base">Babak II Tahap II</p>
                    </div>
                </div>
                <div class="bg-white rounded-full p-1.5 sm:p-2 flex items-center space-x-2 sm:space-x-3 shadow-lg">
                    <div class="w-10 h-10 sm:w-12 sm:h-12 bg-blue-200 rounded-full flex items-center justify-center ring-2 ring-white/50 flex-shrink-0">
                       <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 sm:h-7 sm:w-7 text-blue-700" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                        </svg>
                   </div>
                   <div class="hidden sm:flex flex-col items-start pr-2 sm:pr-4">
                        <div id="puzzle-nama-peserta" class="font-bold text-base sm:text-lg font-poppins text-gray-800 leading-tight">Nama Peserta</div>
                        <div id="puzzle-info-peserta" class="text-xs sm:text-sm font-poppins text-gray-600 leading-tight">Asrama &bull; Kelas</div>
                   </div>
                </div>
            </header>

            <main class="w-full flex-grow flex items-center justify-center p-4">
                <div id="game-container">
                    <div id="answer-board-container">
                        <div id="answer-board" class="font-arabic"></div>
                    </div>
                    <div id="game-board"></div>
                </div>
            </main>
            
            <div id="message-box">
                <div id="message-icon-container" class="mb-4"></div>
                <h2 id="message-title" class="text-3xl font-bold font-philosopher mb-2"></h2>
                <p id="message-text" class="font-poppins text-gray-700"></p>
            </div>
        </div>
    </div>
    
    <!-- Padlock Screen -->
    <div id="padlock-screen" class="hidden relative z-20 w-full h-full flex-col font-inter">
        <div id="padlock-numbers-bg" class="numbers-bg"></div>
        <div class="relative z-10 w-full h-full flex flex-col overflow-y-auto p-4 sm:p-6">
             <header class="w-full flex justify-between items-center z-20 flex-shrink-0">
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <button id="back-to-menu-from-padlock" class="bg-white/70 rounded-full p-2 sm:p-3 shadow-lg transition-all transform active:scale-95 hover:bg-white">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6 text-[#0069EA]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                        </svg>
                    </button>
                    <div>
                        <h1 class="font-philosopher font-bold tracking-wider text-3xl sm:text-4xl" style="line-height: 1.1; color: #0069EA;">Padlock</h1>
                        <p class="font-poppins text-gray-600 text-sm sm:text-base">Grand Final Tahap I</p>
                    </div>
                </div>
                <div class="bg-white rounded-full p-1.5 sm:p-2 flex items-center space-x-2 sm:space-x-3 shadow-lg">
                    <div class="w-10 h-10 sm:w-12 sm:h-12 bg-blue-200 rounded-full flex items-center justify-center ring-2 ring-white/50 flex-shrink-0">
                       <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 sm:h-7 sm:w-7 text-blue-700" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                        </svg>
                   </div>
                   <div class="hidden sm:flex flex-col items-start pr-2 sm:pr-4">
                        <div id="padlock-nama-peserta" class="font-bold text-base sm:text-lg font-poppins text-gray-800 leading-tight">Nama Peserta</div>
                        <div id="padlock-info-peserta" class="text-xs sm:text-sm font-poppins text-gray-600 leading-tight">Asrama &bull; Kelas</div>
                   </div>
                </div>
            </header>

            <main class="w-full flex-grow flex flex-col items-center justify-center p-4">
                 <p id="padlock-warning-text" class="text-center text-red-600 font-semibold mb-4 hidden">⚠️ Kalau bodoh mending jangan lanjut</p>
                 <div id="padlock-card" class="w-full max-w-sm bg-white/70 backdrop-blur-xl rounded-2xl shadow-2xl p-6 sm:p-8 animate-fade-in-up">
                     <form id="padlock-form" class="space-y-6">
                        <div id="padlock-result" class="result-message"></div>
                         <div>
                             <label for="padlock_input" class="block text-center text-sm sm:text-base font-medium text-gray-700 mb-2">Masukkan Jawaban Anda</label>
                             <input
                                 type="text"
                                 id="padlock_input"
                                 name="padlock_input"
                                 required
                                 inputmode="numeric"
                                 pattern="[0-9]*"
                                 class="block w-full px-4 py-3 bg-white/50 border border-gray-300 rounded-lg shadow-sm placeholder-gray-400 transition duration-150 ease-in-out focus-style text-center text-3xl sm:text-4xl font-bold tracking-widest"
                                 placeholder="0"
                             />
                         </div>
                         <div>
                             <button
                                 type="submit"
                                 id="padlock-submit-btn"
                                 class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-lg text-base sm:text-lg font-medium text-white bg-[#0069EA] hover:bg-blue-800 transition-all transform active:scale-95 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
                             >
                                 Kirim
                             </button>
                         </div>
                     </form>
                 </div>
            </main>
        </div>
    </div>

    <audio id="correct-sound" src="https://fyyzfjooysfhasahnddc.supabase.co/storage/v1/object/public/Audio%20COB/Audio/benar.mp3" preload="metadata"></audio>
    <audio id="incorrect-sound" src="https://fyyzfjooysfhasahnddc.supabase.co/storage/v1/object/public/Audio%20COB/Audio/jawaban%20salah.mp3" preload="metadata"></audio>
    <audio id="touch-sound" src="https://fyyzfjooysfhasahnddc.supabase.co/storage/v1/object/public/Audio%20COB/Audio/sound%20touch.mp3" preload="metadata"></audio>

<!-- ... (sisa kode HTML) ... -->
    <script>
    document.addEventListener('DOMContentLoaded', () => {
        // --- Konfigurasi Supabase ---
        const SUPABASE_URL = 'https://fyyzfjooysfhasahnddc.supabase.co'; 
        const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImZ5eXpmam9veXNmaGFzYWhuZGRjIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjA3NzgwNjgsImV4cCI6MjA3NjM1NDA2OH0.T3WwqzjKCLmYFkSVcC8QsfUdgplXcjURIn64Q1PA3fI';

        const { createClient } = supabase;
        let _supabase;

        try {
            _supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
            console.log('Supabase client initialized');
        } catch (error) {
            console.error('Gagal menginisialisasi Supabase:', error.message);
        }
        
        let currentUserData = null;
        let gameStartTime = null; // Variabel global untuk timer
        
        let gameCompletionStatus = {
            memorize: false,
            card: false,
            puzzle: false,
            padlock: false
        };

        // --- Cache DOM Elements ---
        const screens = {
            login: document.getElementById('login-screen'),
            menu: document.getElementById('menu-screen'),
            memorize: document.getElementById('memorize-screen'),
            card: document.getElementById('card-screen'),
            puzzle: document.getElementById('puzzle-screen'),
            padlock: document.getElementById('padlock-screen'),
        };
        const loginForm = document.getElementById('loginForm');
        const dotSpinner = document.getElementById('dotSpinner');
        const popupMini = document.getElementById('popupMini');
        const btnSubmit = document.getElementById('btnSubmit');

        // Audio Elements
        const sounds = {
            correct: document.getElementById('correct-sound'),
            incorrect: document.getElementById('incorrect-sound'),
            touch: document.getElementById('touch-sound')
        };
        
        // --- Sound Logic ---
        function playSound(sound) {
            if (sound && sound.src) {
                sound.currentTime = 0;
                sound.play().catch(e => console.error("Gagal memutar audio:", e.message));
            }
        }

        // --- Vibration Logic ---
        function vibrateOnError() {
            if ('vibrate' in navigator) {
                navigator.vibrate(200); // Getar selama 200 milidetik
            }
        }
        
        // --- UI Logic ---
        function showSpinner(show) {
            dotSpinner.style.display = show ? 'flex' : 'none';
        }

        function showPopup(message, type = 'error') {
            popupMini.textContent = message;
            popupMini.className = `popup-mini ${type} show`;
            setTimeout(() => popupMini.classList.remove('show'), 2000);
        }
        
        async function showScreen(screenName) {
            // Sembunyikan semua popup sebelum pindah layar
            document.querySelectorAll('#card-screen #message-box, #puzzle-screen #message-box, #padlock-screen #padlock-result').forEach(box => box.classList.remove('show'));
            const memorizeResult = document.querySelector('#memorize-screen #memorize-result');
            if(memorizeResult) memorizeResult.classList.remove('show');


            if (screenName === 'login') {
                loginForm.reset();
                currentUserData = null; 
                // [FIX] Pastikan papan jawaban puzzle bersih saat kembali ke login
                const puzzleAnswerBoard = document.querySelector('#puzzle-screen #answer-board');
                if (puzzleAnswerBoard) {
                    puzzleAnswerBoard.textContent = '';
                }
            }
            
            Object.values(screens).forEach(screen => {
                screen.classList.add('hidden');
                screen.classList.remove('flex', 'flex-col');
            });
            screens[screenName].classList.remove('hidden');
            screens[screenName].classList.add('flex');
            
            if (screenName === 'menu' || screenName === 'card' || screenName === 'memorize' || screenName === 'puzzle' || screenName === 'padlock') {
                screens[screenName].classList.add('flex-col');
            }

            // [PERUBAHAN] Mulai timer saat masuk layar game
            if (['memorize', 'card', 'puzzle', 'padlock'].includes(screenName)) {
                gameStartTime = Date.now();
                console.log(`Timer dimulai untuk: ${screenName}`);
            } else {
                gameStartTime = null; // Reset timer jika bukan layar game
            }
            // [PERUBAHAN SELESAI]

            if (screenName === 'menu') {
                updateMenuCards();
                initializeMenuAnimations();
            } else if (screenName === 'memorize') {
                await setupMemorizeScreen();
            } else if (screenName === 'card') {
                await setupCardGameScreen();
            } else if (screenName === 'puzzle') {
                await setupPuzzleScreen();
            } else if (screenName === 'padlock') {
                await setupPadlockScreen();
            }

            if (screenName !== 'memorize') stopMemorizeAnimation();
            if (screenName !== 'card') stopCardBackgroundAnimation();
            if (screenName !== 'padlock') stopPadlockAnimation();
        }
        
        function updateUserInfo(userData) {
            if (!userData) return;
            const nama = userData.nama || 'Nama Peserta';
            const asrama = userData.asrama || 'Asrama';
            const kelas = userData.kelas || 'Kelas';
            const info = `${asrama} • ${kelas}`;

            ['nama-peserta', 'memorize-nama-peserta', 'card-nama-peserta', 'puzzle-nama-peserta', 'padlock-nama-peserta'].forEach(id => {
                 const el = document.getElementById(id);
                 if(el) el.textContent = nama;
            });
            ['info-peserta', 'memorize-info-peserta', 'card-info-peserta', 'puzzle-info-peserta', 'padlock-info-peserta'].forEach(id => {
                const el = document.getElementById(id);
                if(el) el.textContent = info;
            });
        }

        function updateMenuCards() {
            Object.keys(gameCompletionStatus).forEach(game => {
                const wrapper = document.getElementById(`${game}-card-wrapper`);
                if (wrapper) {
                    wrapper.style.display = gameCompletionStatus[game] ? 'none' : 'flex';
                }
            });
        }
        
        function getJenjangKelas(kelasStr) {
            if (!kelasStr) return null; 

            const isMTS = kelasStr.toUpperCase().includes('MTS');
            const match = kelasStr.match(/(VI|V|IV|III|II|I)/i);
            if (!match) return null;

            const roman = match[0].toUpperCase();
            let result = 0;
            
            const romanMap = { 'I': 1, 'II': 2, 'III': 3, 'IV': 4, 'V': 5, 'VI': 6 };
            result = romanMap[roman];
            
            if(!result) return null;

            if (isMTS) {
                return result + 6;
            }
            return result;
        }


        // --- Login Logic ---
        loginForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!_supabase) return showPopup('Koneksi Supabase gagal.', 'error');
            popupMini.classList.remove('show');

            const idUser = document.getElementById('id_user').value.trim();
            const password = document.getElementById('password').value.trim();
            if (!idUser || !password) return showPopup('Harap isi ID User dan Password.', 'error');
            
            showSpinner(true);
            btnSubmit.disabled = true;

            try {
                const { data, error } = await _supabase.from('peserta').select('*').eq('user_id', idUser).single();
                if (error && error.code !== 'PGRST116') throw error;

                if (data && data.password === password) {
                    currentUserData = data;
                    // Reset status game saat login berhasil
                    gameCompletionStatus = { memorize: false, card: false, puzzle: false, padlock: false };

                    // [PERUBAHAN] Menghapus semua logika 'participant_scores' dari sini.
                    // Kita tidak perlu membuat baris per user lagi.
                    
                    showPopup('Login berhasil. Memuat menu...', 'success');
                    setTimeout(() => {
                        showScreen('menu');
                        updateUserInfo(currentUserData);
                    }, 300);
                } else {
                    
                    showPopup('ID User atau Password salah.', 'error');
                }
            } catch (err) {
                console.error("Terjadi Error Supabase:", err);
                showPopup('Gagal terhubung ke database.', 'error');
            } finally {
                showSpinner(false);
                btnSubmit.disabled = false;
            }
        });
        
        // --- ================================== ---
        // ---           MEMORIZE GAME          ---
        // --- ================================== ---
        const memorizeAnswerForm = document.getElementById('memorize-form');
        const memorizeAnswerInput = document.getElementById('number_input');
        const memorizeAnswerSubmitBtn = document.getElementById('memorize-submit-btn');
        const memorizeCard = document.getElementById('memorize-card');
        const memorizeAnswerResult = document.getElementById('memorize-result');
        const memorizeCanvas = document.getElementById('numbers-canvas');
        let memorizeAnimationId;
        let memorizeCorrectAnswer = null;

        async function fetchMemorizeAnswer() {
            if (!_supabase || !currentUserData) throw new Error("Data pengguna tidak ditemukan.");
            
            const jenjang = getJenjangKelas(currentUserData.kelas);
             if (!jenjang) throw new Error("Jenjang kelas tidak valid.");
            
            try {
                const { data, error } = await _supabase.from('konfigurasi').select('kunci_jawaban_memorize').eq('jenjang_kelas', jenjang).eq('putaran', currentUserData.putaran).single();
                if (error) throw error;
                if (data && data.kunci_jawaban_memorize) return data.kunci_jawaban_memorize;
                throw new Error(`Tidak ada kunci jawaban Memorize untuk jenjang ${jenjang} putaran ${currentUserData.putaran}.`);
            } catch (err) {
                console.error("Error mengambil jawaban Memorize:", err.message);
                throw err;
            }
        }
        
        async function setupMemorizeScreen() {
            startMemorizeAnimation();
            memorizeAnswerSubmitBtn.disabled = true;
            memorizeAnswerInput.disabled = true;
            memorizeAnswerInput.value = '';
            memorizeAnswerInput.placeholder = "Memuat...";

            try {
                memorizeCorrectAnswer = await fetchMemorizeAnswer();
                memorizeAnswerSubmitBtn.disabled = false;
                memorizeAnswerInput.disabled = false;
                memorizeAnswerInput.placeholder = "0";
                memorizeAnswerInput.focus();
            } catch (error) {
                showPopup(error.message, 'error');
                memorizeAnswerInput.placeholder = "Error";
            }
        }

        memorizeAnswerForm.addEventListener('submit', (e) => {
            e.preventDefault();
            if (memorizeCorrectAnswer === null) return showPopup('Kunci jawaban belum siap.', 'error');

            const userAnswer = memorizeAnswerInput.value;
            const isCorrect = userAnswer === String(memorizeCorrectAnswer);
            
            // [PERUBAHAN DIMULAI] Menggunakan 'game_log' (Format Long)
            if (gameStartTime) {
                const timeTaken = (Date.now() - gameStartTime) / 1000; // Waktu dalam detik
                
                // Format Waktu Jakarta (WIB)
                const timestamp = new Date().toLocaleString('id-ID', { 
                    timeZone: 'Asia/Jakarta', 
                    hour12: false, day: '2-digit', month: '2-digit', year: 'numeric', 
                    hour: '2-digit', minute: '2-digit', second: '2-digit' 
                });
                
                console.log(`Logging to game_log: Memorize, correct: ${isCorrect}`);
                
                // Mengirim log baru ke tabel 'game_log'
                _supabase.from('game_log')
                    .insert([{ 
                        user_id: currentUserData.user_id,
                        nama_peserta: currentUserData.nama, // Pastikan 'currentUserData.nama' benar
                        game_name: 'Memorize',
                        answer: userAnswer,
                        time_taken: timeTaken,
                        is_correct: isCorrect,
                        submitted_at: timestamp
                    }])
                    .then(({ error }) => {
                        if (error) console.error('Gagal insert ke game_log (Memorize):', error.message);
                    });
                gameStartTime = null; // Reset timer
            }
            // [PERUBAHAN SELESAI]

            memorizeCard.classList.remove('correct', 'incorrect', 'shake-anim');
            memorizeAnswerResult.classList.remove('show', 'correct', 'incorrect');
            memorizeAnswerSubmitBtn.disabled = true;
            memorizeAnswerInput.disabled = true;

            if (isCorrect) {
                // [Logika Supabase DIHAPUS dari sini]
                playSound(sounds.correct);
                memorizeAnswerResult.textContent = "Jawaban Benar!";
                memorizeAnswerResult.classList.add('correct');
                memorizeCard.classList.add('correct');
                gameCompletionStatus.memorize = true;
                setTimeout(() => {
                    showScreen('login');
                }, 1200);
            } else {
                playSound(sounds.incorrect);
                vibrateOnError();
                memorizeAnswerResult.textContent = "Jawaban Salah, Kembali ke Login!";
                memorizeAnswerResult.classList.add('incorrect');
                memorizeCard.classList.add('incorrect', 'shake-anim');
                setTimeout(() => {
                    showScreen('login');
                }, 1200);
            }
            setTimeout(() => memorizeAnswerResult.classList.add('show'), 100);
        });

        function startMemorizeAnimation() {
            if (memorizeAnimationId) return; 

            const ctx = memorizeCanvas.getContext('2d');
            let particles = [];

            function resizeCanvas() {
                memorizeCanvas.width = window.innerWidth;
                memorizeCanvas.height = window.innerHeight;
            }
            resizeCanvas();
            window.addEventListener('resize', resizeCanvas);

            const particleCount = window.innerWidth < 768 ? 50 : 100;

            for (let i = 0; i < particleCount; i++) {
                particles.push({
                    x: Math.random() * memorizeCanvas.width,
                    y: Math.random() * memorizeCanvas.height,
                    vx: (Math.random() - 0.5) * 0.7,
                    vy: (Math.random() - 0.5) * 0.7,
                    number: Math.floor(Math.random() * 10),
                    size: Math.random() * 80 + 20,
                    opacity: Math.random() * 0.4 + 0.2 
                });
            }

            function animate() {
                ctx.clearRect(0, 0, memorizeCanvas.width, memorizeCanvas.height);

                particles.forEach(p => {
                    p.x += p.vx;
                    p.y += p.vy;

                    if (p.x < -20) p.x = memorizeCanvas.width + 20;
                    if (p.x > memorizeCanvas.width + 20) p.x = -20;
                    if (p.y < -20) p.y = memorizeCanvas.height + 20;
                    if (p.y > memorizeCanvas.height + 20) p.y = -20;
                    
                    ctx.fillStyle = `rgba(255, 255, 255, ${p.opacity})`;
                    ctx.font = `bold ${p.size}px 'Poppins', sans-serif`;
                    ctx.fillText(p.number, p.x, p.y);
                });

                memorizeAnimationId = requestAnimationFrame(animate);
            }

            animate();
        }
        
        function stopMemorizeAnimation() {
             if (memorizeAnimationId) {
                cancelAnimationFrame(memorizeAnimationId);
                memorizeAnimationId = null;
                const ctx = memorizeCanvas.getContext('2d');
                if (ctx) {
                    ctx.clearRect(0, 0, memorizeCanvas.width, memorizeCanvas.height);
                }
            }
        }

        // --- ================================== ---
        // ---             CARD GAME            ---
        // --- ================================== ---
        const cardGameBoard = document.querySelector('#card-screen #game-board');
        const cardAnswerBoard = document.querySelector('#card-screen #answer-board');
        const cardMessageBox = document.querySelector('#card-screen #message-box');
        const cardMessageTitle = document.querySelector('#card-screen #message-title');
        const cardMessageText = document.querySelector('#card-screen #message-text');
        const cardMessageIconContainer = document.querySelector('#card-screen #message-icon-container');
        const cardBackgroundContainer = document.getElementById('background-animation');
        
        async function setupCardGameScreen(){
            startCardBackgroundAnimation();
            await setupCardGame();
        }

        function updateActiveSlot(currentIndex, board) {
            if (!board) return;
            
            for (let i = 0; i < board.children.length; i++) {
                const slot = board.children[i];
                 if (i === currentIndex) {
                    slot.classList.add('animated-slot');
                } else {
                    slot.classList.remove('animated-slot');
                }
            }
        }
        
        async function setupCardGame() {
            cardGameBoard.innerHTML = '<p class="text-white font-semibold text-lg">Memuat soal...</p>';
            cardAnswerBoard.innerHTML = '';
            cardMessageBox.classList.remove('show');

            let correctOrder = [];
            let allCards = [];
            let playerSequence = [];

            try {
                if (!_supabase || !currentUserData) throw new Error("Supabase client tidak terinisialisasi.");
                
                const jenjang = getJenjangKelas(currentUserData.kelas);
                if (!jenjang) throw new Error("Jenjang kelas tidak valid.");
                
                const { data: setsData, error: setsError } = await _supabase
                    .from('card_game_sets')
                    .select('*')
                    .eq('jenjang_kelas', jenjang);

                if (setsError) throw setsError;
                if (!setsData || setsData.length === 0) throw new Error(`Tidak ada set soal Card untuk jenjang kelas ${jenjang}.`);

                const randomSet = setsData[Math.floor(Math.random() * setsData.length)];
                
                correctOrder = (randomSet.urutan_jawaban || '').split(',').map(s => s.trim()).filter(Boolean);
                const pengecoh = (randomSet.kata_pengecoh || '').split(',').map(s => s.trim()).filter(Boolean);
                allCards = [...correctOrder, ...pengecoh];
                let shuffledCards = [...allCards].sort(() => Math.random() - 0.5);
                
                cardGameBoard.innerHTML = '';
                
                shuffledCards.forEach(kata => {
                    const card = createCardElement(kata);
                    card.addEventListener('click', () => handleCardClick(card, kata));
                    cardGameBoard.appendChild(card);
                });

                correctOrder.forEach(() => {
                    const slot = document.createElement('div');
                    slot.classList.add('answer-slot');
                    cardAnswerBoard.appendChild(slot);
                });
                updateActiveSlot(0, cardAnswerBoard);

                cardAnswerBoard.onclick = handleUndoClick;

            } catch (error) {
                console.error("Gagal memulai game Card:", error.message);
                cardGameBoard.innerHTML = `<p class="text-red-500 font-semibold text-center">${error.message}</p>`;
            }
            
            function createCardElement(kata) {
                const card = document.createElement('div');
                card.className = 'card font-arabic';
                card.dataset.kata = kata;
                card.textContent = kata;
                return card;
            }

            function handleCardClick(card, kata) {
                playSound(sounds.touch);
                if (card.classList.contains('is-chosen') || playerSequence.length >= correctOrder.length) return;
                card.classList.add('is-chosen');
                playerSequence.push(kata);
                
                const nextSlot = cardAnswerBoard.children[playerSequence.length - 1];
                if (nextSlot) {
                    const chosenCard = createCardElement(kata);
                    nextSlot.innerHTML = '';
                    nextSlot.appendChild(chosenCard);
                    nextSlot.classList.remove('animated-slot');
                }
                updateActiveSlot(playerSequence.length, cardAnswerBoard);

                if (playerSequence.length === correctOrder.length) checkResult();
            }

            function handleUndoClick(event) {
                const clickedCard = event.target.closest('.card');
                if (!clickedCard || !cardAnswerBoard.contains(clickedCard.parentElement)) return;
                
                playSound(sounds.touch);
                const lastChosenKata = playerSequence[playerSequence.length - 1];
                if (clickedCard.dataset.kata === lastChosenKata) {
                    playerSequence.pop();
                    clickedCard.parentElement.innerHTML = '';
                    const originalCard = cardGameBoard.querySelector(`.card[data-kata="${lastChosenKata}"]`);
                    if (originalCard) originalCard.classList.remove('is-chosen');
                    updateActiveSlot(playerSequence.length, cardAnswerBoard);
                }
            }

            function checkResult() {
                const isCorrect = JSON.stringify(playerSequence) === JSON.stringify(correctOrder);
                
                // [PERUBAHAN DIMULAI] Menggunakan 'game_log' (Format Long)
                if (gameStartTime) {
                    const timeTaken = (Date.now() - gameStartTime) / 1000; // Waktu dalam detik
                    const userAnswer = playerSequence.join(','); // Gabungkan array jadi string
                    
                    // Format Waktu Jakarta (WIB)
                    const timestamp = new Date().toLocaleString('id-ID', { 
                        timeZone: 'Asia/Jakarta', 
                        hour12: false, day: '2-digit', month: '2-digit', year: 'numeric', 
                        hour: '2-digit', minute: '2-digit', second: '2-digit' 
                    });

                    console.log(`Logging to game_log: Card, correct: ${isCorrect}`);

                    // Mengirim log baru ke tabel 'game_log'
                    _supabase.from('game_log')
                        .insert([{ 
                            user_id: currentUserData.user_id,
                            nama_peserta: currentUserData.nama, // Pastikan 'currentUserData.nama' benar
                            game_name: 'Card',
                            answer: userAnswer,
                            time_taken: timeTaken,
                            is_correct: isCorrect,
                            submitted_at: timestamp
                        }])
                        .then(({ error }) => {
                            if (error) console.error('Gagal insert ke game_log (Card):', error.message);
                        });
                    gameStartTime = null; // Reset timer
                }
                // [PERUBAHAN SELESAI]
                
                const successIcon = `<svg class="w-16 h-16 text-green-500 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>`;
                const failureIcon = `<svg class="w-16 h-16 text-red-500 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>`;

                setTimeout(() => {
                    if (isCorrect) {
                        // [Logika Supabase DIHAPUS dari sini]
                        playSound(sounds.correct);
                        cardMessageIconContainer.innerHTML = successIcon;
                        cardMessageTitle.textContent = "Luar Biasa!";
                        cardMessageTitle.className = "text-3xl font-bold font-philosopher text-green-600 mb-2";
                        cardMessageText.textContent = "Anda berhasil";
                        gameCompletionStatus.card = true;
                        setTimeout(() => showScreen('login'), 1200);
                    } else {
                        playSound(sounds.incorrect);
                        vibrateOnError();
                        cardMessageIconContainer.innerHTML = failureIcon;
                        cardMessageTitle.textContent = "Jawaban Salah!";
                        cardMessageTitle.className = "text-3xl font-bold font-philosopher text-red-600 mb-2";
                        cardMessageText.textContent = "Anda akan dikembalikan ke halaman login.";
                        setTimeout(() => {
                            showScreen('login');
                        }, 1200);
                    }
                    cardMessageBox.classList.add('show');
                }, 500);
            }
        }
        
        function startCardBackgroundAnimation() {
             if (cardBackgroundContainer.children.length > 0) return;
             const cardsCount = 60;
             const animationNames = ['drift-1', 'drift-2', 'drift-3', 'drift-4'];
             for (let i = 0; i < cardsCount; i++) {
                 const cardEl = document.createElement('div');
                 cardEl.className = 'floating-card';
                 cardEl.style.left = `${Math.random() * 100}vw`;
                 cardEl.style.top = `${Math.random() * 100}vh`;
                 const scale = Math.random() * 0.5 + 0.3;
                 cardEl.style.width = `${80 * scale}px`;
                 cardEl.style.height = `${110 * scale}px`;
                 cardEl.style.opacity = Math.random() * 0.5 + 0.2;
                 cardEl.style.animationName = animationNames[Math.floor(Math.random() * animationNames.length)];
                 const duration = Math.random() * 50 + 40;
                 cardEl.style.animationDuration = `${duration}s`;
                 cardEl.style.animationDelay = `-${Math.random() * duration}s`;
                 cardBackgroundContainer.appendChild(cardEl);
             }
        }
        function stopCardBackgroundAnimation() { if(cardBackgroundContainer) cardBackgroundContainer.innerHTML = ''; }

        // --- ================================== ---
        // ---           PUZZLE GAME            ---
        // --- ================================== ---

        async function setupPuzzleScreen(){
            await setupPuzzleGame();
        }

        async function setupPuzzleGame() {
            const gameBoard = document.querySelector('#puzzle-screen #game-board');
            const answerBoard = document.querySelector('#puzzle-screen #answer-board');
            const messageBox = document.querySelector('#puzzle-screen #message-box');
            const messageIconContainer = document.querySelector('#puzzle-screen #message-icon-container');
            const messageTitle = document.querySelector('#puzzle-screen #message-title');
            const messageText = document.querySelector('#puzzle-screen #message-text');

            let correctOrder = [];
            let allKeys = [];
            let playerSequence = [];

            async function fetchPuzzleData() {
                if (!_supabase || !currentUserData) throw new Error("Data pengguna tidak ditemukan.");
                
                const jenjang = getJenjangKelas(currentUserData.kelas);
                if (!jenjang) throw new Error("Jenjang kelas tidak valid.");

                const { data, error } = await _supabase.from('puzzle_game_sets').select('*').eq('jenjang_kelas', jenjang);

                if (error) throw error;
                if (!data || data.length === 0) throw new Error(`Tidak ada set soal Puzzle untuk jenjang kelas ${jenjang}.`);
                
                const randomSet = data[Math.floor(Math.random() * data.length)];

                correctOrder = (randomSet.urutan_jawaban || '').split(',').map(s => s.trim()).filter(Boolean);
                const pengecoh = (randomSet.kata_pengecoh || '').split(',').map(s => s.trim()).filter(Boolean);
                allKeys = [...correctOrder, ...pengecoh];
            }

            function initializeGame() {
                let shuffledKeys = [...allKeys].sort(() => Math.random() - 0.5);
                playerSequence = [];

                // --- [PERUBAHAN DIMULAI] ---
                // Hitung jumlah kolom yang dibutuhkan secara dinamis
                const totalItems = allKeys.length + 1; // +1 untuk tombol backspace
                const columnCount = Math.ceil(totalItems / 3); // Paksa jadi 3 baris
                
                // Set style grid secara dinamis via JavaScript
                gameBoard.style.gridTemplateColumns = `repeat(${columnCount}, 1fr)`;
                // --- [PERUBAHAN SELESAI] ---

                gameBoard.innerHTML = '';
                answerBoard.textContent = '';
                
                shuffledKeys.forEach(word => {
                    const keyButton = document.createElement('button');
                    keyButton.className = 'key-button font-arabic';
                    keyButton.textContent = word;
                    keyButton.addEventListener('click', () => handleKeyPress(word));
                    gameBoard.appendChild(keyButton);
                });

                const backspaceButton = document.createElement('button');
                backspaceButton.className = 'key-button backspace-key';
                backspaceButton.innerHTML = `&larr;`;
                backspaceButton.addEventListener('click', handleBackspace);
                gameBoard.appendChild(backspaceButton);
            }
            
            function updateAnswerDisplay() {
                answerBoard.textContent = playerSequence.join(' ');
            }

            function handleKeyPress(word) {
                playSound(sounds.touch);
                if (playerSequence.length >= correctOrder.length) return;
                
                playerSequence.push(word);
                updateAnswerDisplay();

                const pressedButton = Array.from(gameBoard.querySelectorAll('.key-button')).find(btn => btn.textContent === word && !btn.disabled);
                if (pressedButton) {
                    pressedButton.disabled = true;
                }

                if (playerSequence.length === correctOrder.length) {
                    checkResult();
                }
            }
            
            function handleBackspace() {
                playSound(sounds.touch);
                if (playerSequence.length === 0) return;

                const removedWord = playerSequence.pop();
                updateAnswerDisplay();

                const releasedButton = Array.from(gameBoard.querySelectorAll('.key-button')).find(btn => btn.textContent === removedWord && btn.disabled);
                if (releasedButton) {
                    releasedButton.disabled = false;
                }
            }
            
            function checkResult() {
                const isCorrect = JSON.stringify(playerSequence) === JSON.stringify(correctOrder);

                // [PERUBAHAN DIMULAI] Menggunakan 'game_log' (Format Long)
                if (gameStartTime) {
                    const timeTaken = (Date.now() - gameStartTime) / 1000; // Waktu dalam detik
                    const userAnswer = playerSequence.join(','); // Gabungkan array jadi string

                    // Format Waktu Jakarta (WIB)
                    const timestamp = new Date().toLocaleString('id-ID', { 
                        timeZone: 'Asia/Jakarta', 
                        hour12: false, day: '2-digit', month: '2-digit', year: 'numeric', 
                        hour: '2-digit', minute: '2-digit', second: '2-digit' 
                    });
                    
                    console.log(`Logging to game_log: Puzzle, correct: ${isCorrect}`);
                    
                    // Mengirim log baru ke tabel 'game_log'
                    _supabase.from('game_log')
                        .insert([{ 
                            user_id: currentUserData.user_id,
                            nama_peserta: currentUserData.nama, // Pastikan 'currentUserData.nama' benar
                            game_name: 'Puzzle',
                            answer: userAnswer,
                            time_taken: timeTaken,
                            is_correct: isCorrect,
                            submitted_at: timestamp
                        }])
                        .then(({ error }) => {
                            if (error) console.error('Gagal insert ke game_log (Puzzle):', error.message);
                        });
                    gameStartTime = null; // Reset timer
                }
                // [PERUBAHAN SELESAI]
                
                const successIcon = `<svg class="w-16 h-16 text-green-500 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>`;
                const failureIcon = `<svg class="w-16 h-16 text-red-500 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>`;

                setTimeout(() => {
                    if (isCorrect) {
                        // [Logika Supabase DIHAPUS dari sini]
                        playSound(sounds.correct);
                        messageIconContainer.innerHTML = successIcon;
                        messageTitle.textContent = "Susunan Anda Benar!";
                        messageTitle.className = "text-3xl font-bold font-philosopher text-green-600 mb-2";
                        messageText.textContent = "Anda berhasil";
                        gameCompletionStatus.puzzle = true;
                        messageBox.classList.add('show');
                        setTimeout(() => showScreen('login'), 1200);
                    } else {
                        playSound(sounds.incorrect);
                        vibrateOnError();
                        messageIconContainer.innerHTML = failureIcon;
                        messageTitle.textContent = "Susunan Anda Salah!";
                        messageTitle.className = "text-3xl font-bold font-philosopher text-red-600 mb-2";
                        messageText.textContent = "Anda akan dikembalikan ke halaman login.";
                        messageBox.classList.add('show');
                        setTimeout(() => {
                            showScreen('login');
                        }, 1200);
                    }
                }, 500);
            }

            try {
                gameBoard.innerHTML = '<p class="text-gray-600 font-semibold">Memuat soal...</p>';
                await fetchPuzzleData();
                initializeGame();
            } catch(error) {
                console.error("Gagal memulai game Puzzle:", error.message);
                gameBoard.innerHTML = `<p class="text-red-500 font-semibold text-center col-span-3">${error.message}</p>`;
            }
        }
        
        // --- ================================== ---
        // ---           PADLOCK GAME           ---
        // --- ================================== ---

        const padlockAnswerForm = document.getElementById('padlock-form');
        const padlockAnswerInput = document.getElementById('padlock_input');
        const padlockAnswerSubmitBtn = document.getElementById('padlock-submit-btn');
        const padlockCard = document.getElementById('padlock-card');
        const padlockAnswerResult = document.getElementById('padlock-result');
        const padlockWarningText = document.getElementById('padlock-warning-text');
        const padlockCanvas = document.getElementById('padlock-numbers-bg');
        let padlockAnimationId;
        let padlockCorrectAnswer = null;

        async function fetchPadlockAnswer() {
            if (!_supabase || !currentUserData) return "12345";
            try {
                const jenjang = getJenjangKelas(currentUserData.kelas);
                if (!jenjang) throw new Error("Jenjang kelas tidak valid.");
                
                const { data, error } = await _supabase
                    .from('konfigurasi')
                    .select('kunci_jawaban_padlock')
                    .eq('jenjang_kelas', jenjang)
                    .not('kunci_jawaban_padlock', 'is', null)
                    .limit(1)
                    .single();

                if (error) throw error;
                if (data && data.kunci_jawaban_padlock) return data.kunci_jawaban_padlock;
                throw new Error(`Tidak ada kunci jawaban Padlock untuk jenjang ${jenjang}.`);
            } catch (err) {
                console.error("Error mengambil jawaban Padlock:", err.message);
                throw err;
            }
        }

        async function setupPadlockScreen() {
            startPadlockAnimation();
            padlockAnswerSubmitBtn.disabled = true;
            padlockAnswerInput.disabled = true;
            padlockAnswerInput.value = '';
            padlockAnswerInput.placeholder = "Memuat...";
            
            setInterval(() => {
                padlockWarningText.style.display = 'block';
                padlockWarningText.classList.add('animate-blinking');
                setTimeout(() => {
                    padlockWarningText.style.display = 'none';
                    padlockWarningText.classList.remove('animate-blinking');
                }, 3000);
            }, 30000);


            try {
                padlockCorrectAnswer = await fetchPadlockAnswer();
                padlockAnswerSubmitBtn.disabled = false;
                padlockAnswerInput.disabled = false;
                padlockAnswerInput.placeholder = "0";
                padlockAnswerInput.focus();
            } catch (error) {
                showPopup(error.message, 'error');
                padlockAnswerInput.placeholder = "Error";
            }
        }

        padlockAnswerForm.addEventListener('submit', (e) => {
            e.preventDefault();
            if (padlockCorrectAnswer === null) return showPopup('Kunci jawaban belum siap.', 'error');

            const userAnswer = padlockAnswerInput.value;
            const isCorrect = userAnswer === String(padlockCorrectAnswer);
            
            // [PERUBAHAN DIMULAI] Menggunakan 'game_log' (Format Long)
            if (gameStartTime) {
                const timeTaken = (Date.now() - gameStartTime) / 1000; // Waktu dalam detik

                // Format Waktu Jakarta (WIB)
                const timestamp = new Date().toLocaleString('id-ID', { 
                    timeZone: 'Asia/Jakarta', 
                    hour12: false, day: '2-digit', month: '2-digit', year: 'numeric', 
                    hour: '2-digit', minute: '2-digit', second: '2-digit' 
                });

                console.log(`Logging to game_log: Padlock, correct: ${isCorrect}`);
                
                // Mengirim log baru ke tabel 'game_log'
                _supabase.from('game_log')
                    .insert([{ 
                        user_id: currentUserData.user_id,
                        nama_peserta: currentUserData.nama, // Pastikan 'currentUserData.nama' benar
                        game_name: 'Padlock',
                        answer: userAnswer,
                        time_taken: timeTaken,
                        is_correct: isCorrect,
                        submitted_at: timestamp
                    }])
                    .then(({ error }) => {
                        if (error) console.error('Gagal insert ke game_log (Padlock):', error.message);
                    });
                gameStartTime = null; // Reset timer
            }
            // [PERUBAHAN SELESAI]
            
            padlockCard.classList.remove('correct', 'incorrect', 'shake-anim');
            padlockAnswerResult.classList.remove('show', 'correct', 'incorrect');
            padlockAnswerSubmitBtn.disabled = true;
            padlockAnswerInput.disabled = true;

            if (isCorrect) {
                // [Logika Supabase DIHAPUS dari sini]
                playSound(sounds.correct);
                padlockAnswerResult.textContent = "Jawaban Benar!";
                padlockAnswerResult.classList.add('correct');
                padlockCard.classList.add('correct');
                gameCompletionStatus.padlock = true;
                setTimeout(() => {
                    showScreen('login');
                }, 1200);
            } else {
                playSound(sounds.incorrect);
                vibrateOnError();
                padlockAnswerResult.textContent = "Jawaban Salah, Kembali ke Login!";
                padlockAnswerResult.classList.add('incorrect');
                padlockCard.classList.add('incorrect', 'shake-anim');
                setTimeout(() => {
                    showScreen('login');
                }, 1200);
            }
            setTimeout(() => padlockAnswerResult.classList.add('show'), 100);
        });

        function startPadlockAnimation() {
            if (padlockAnimationId) return;
            const container = padlockCanvas;
            if (!container) return;
            container.innerHTML = ''; // Clear previous animation
            
            const numbersCount = 100;
            const animationNames = ['drift-1', 'drift-2', 'drift-3', 'drift-4'];
            for (let i = 1; i <= numbersCount; i++) {
                const numberEl = document.createElement('div');
                numberEl.className = 'number-item';
                numberEl.textContent = i;
                numberEl.style.left = `${Math.random() * 100}vw`;
                numberEl.style.top = `${Math.random() * 100}vh`;
                numberEl.style.fontSize = '4rem'; 
                numberEl.style.opacity = Math.random() * 0.4 + 0.3;
                numberEl.style.animationName = animationNames[Math.floor(Math.random() * animationNames.length)];
                const duration = Math.random() * 40 + 30;
                numberEl.style.animationDuration = `${duration}s`;
                numberEl.style.animationDelay = `-${Math.random() * duration}s`;
                container.appendChild(numberEl);
            }
        }
        function stopPadlockAnimation(){
             if (padlockCanvas) padlockCanvas.innerHTML = '';
        }


        // --- ================================== ---
        // ---         NAVIGATION & SETUP       ---
        // --- ================================== ---
        
        function setupGlobalInteractions() {
            document.querySelectorAll('button').forEach(button => {
                button.addEventListener('click', () => playSound(sounds.touch));
            });

            document.getElementById('back-to-login').addEventListener('click', () => { showScreen('login'); });
            document.getElementById('start-memorize').addEventListener('click', () => { showScreen('memorize'); updateUserInfo(currentUserData); });
            document.getElementById('back-to-menu-from-memorize').addEventListener('click', () => showScreen('menu'));
            document.getElementById('start-card').addEventListener('click', () => { showScreen('card'); updateUserInfo(currentUserData); });
            document.getElementById('back-to-menu-from-card').addEventListener('click', () => showScreen('menu'));
            document.getElementById('start-puzzle').addEventListener('click', () => { showScreen('puzzle'); updateUserInfo(currentUserData); });
            document.getElementById('back-to-menu-from-puzzle').addEventListener('click', () => showScreen('menu'));
            document.getElementById('start-padlock').addEventListener('click', () => { showScreen('padlock'); updateUserInfo(currentUserData); });
            document.getElementById('back-to-menu-from-padlock').addEventListener('click', () => showScreen('menu'));


            const numberInput = document.getElementById('number_input');
            if (numberInput) {
                numberInput.addEventListener('input', function(e) { this.value = this.value.replace(/\D/g, ''); });
            }
            const padlockInput = document.getElementById('padlock_input');
             if (padlockInput) {
                padlockInput.addEventListener('input', function(e) { this.value = this.value.replace(/\D/g, ''); });
            }
            
            document.querySelectorAll('.card-wrapper').forEach(cardWrapper => {
                const tiltCard = cardWrapper.querySelector('.animated-border-container');
                if (tiltCard) {
                    tiltCard.addEventListener('mousemove', e => {
                        const { width, height, left, top } = tiltCard.getBoundingClientRect();
                        const x = e.clientX - left, y = e.clientY - top;
                        const middleX = width / 2, middleY = height / 2;
                        const maxRotation = 8;
                        const offsetX = ((x - middleX) / middleX) * maxRotation;
                        const offsetY = ((y - middleY) / middleY) * -maxRotation;
                        requestAnimationFrame(() => {
                            tiltCard.style.transform = `perspective(1000px) rotateY(${offsetX}deg) rotateX(${offsetY}deg) scale(1.05)`;
                        });
                    });
                    tiltCard.addEventListener('mouseleave', () => {
                        requestAnimationFrame(() => {
                            tiltCard.style.transform = `perspective(1000px) rotateY(0deg) rotateX(0deg) scale(1)`;
                        });
                    });
                }
            });
        }
        
        function initializeMenuAnimations() {
            const cardWrappers = document.querySelectorAll('#menu-screen .card-wrapper');
            let visibleIndex = 0;
            cardWrappers.forEach((card) => {
                if (card.style.display !== 'none') {
                    card.classList.remove('animate-fade-in-up');
                    void card.offsetWidth;
                    card.style.animationDelay = `${visibleIndex * 80}ms`;
                    card.classList.add('animate-fade-in-up');
                    visibleIndex++;
                }
            });
            ['header-left', 'header-right'].forEach(id => {
                const el = document.getElementById(id);
                el.classList.remove('animate-fade-in-down');
                void el.offsetWidth;
                el.style.opacity = '1';
                el.classList.add('animate-fade-in-down');
            });
        }
        
        setupGlobalInteractions();
    });
    </script>
</body>
</html>
