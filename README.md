<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>703Ledu - PETUALANGAN BANGUN (Matematika Kelas 2 SD)</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Google Fonts - Fredoka & Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
  
  <style>
    * {
      font-family: 'Fredoka', 'Inter', sans-serif;
      user-select: none;
      -webkit-user-select: none;
      touch-action: manipulation;
    }
    
    body {
      background: linear-gradient(135deg, #A8EDEA 0%, #FED6E3 100%);
      min-height: 100vh;
      overflow-x: hidden;
    }

    .btn-bounce {
      transition: all 0.15s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      box-shadow: 0 6px 0 rgba(0, 0, 0, 0.15);
    }
    .btn-bounce:hover {
      transform: translateY(-3px);
      box-shadow: 0 9px 0 rgba(0, 0, 0, 0.15);
    }
    .btn-bounce:active {
      transform: translateY(3px);
      box-shadow: 0 2px 0 rgba(0, 0, 0, 0.15);
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-10px) rotate(2deg); }
    }
    .animate-float {
      animation: float 3.5s ease-in-out infinite;
    }

    .glass-card {
      background: rgba(255, 255, 255, 0.92);
      backdrop-filter: blur(12px);
      border: 4px solid rgba(255, 255, 255, 0.9);
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
    }

    canvas {
      touch-action: none;
    }

    .found-shape {
      animation: pulseFound 0.6s ease-out;
      filter: drop-shadow(0 0 8px #10B981);
    }
    @keyframes pulseFound {
      0% { transform: scale(1); }
      50% { transform: scale(1.3); }
      100% { transform: scale(1); }
    }
  </style>
</head>
<body class="text-slate-800 flex flex-col min-h-screen">

  <header class="w-full max-w-5xl mx-auto px-4 pt-3 pb-1 flex justify-between items-center z-50">
    <button id="btn-home" onclick="goToScreen('screen-home')" class="btn-bounce bg-yellow-400 hover:bg-yellow-300 text-slate-800 font-bold px-4 py-2 rounded-2xl flex items-center gap-2 text-sm md:text-base border-2 border-yellow-500 hidden">
      <i class="fa-solid fa-house"></i> Menu Utama
    </button>
    
    <div id="brand-header" class="flex flex-col items-start">
      <span class="text-xs font-black tracking-widest text-indigo-700 bg-white/90 px-2.5 py-0.5 rounded-full shadow-sm border border-indigo-200">
        703Ledu
      </span>
      <span class="bg-indigo-600 text-white font-black text-base md:text-lg px-3 py-0.5 rounded-xl shadow border-2 border-indigo-400">
        📐 PETUALANGAN BANGUN
      </span>
    </div>

    <div class="flex items-center gap-2 md:gap-3">
      <div class="bg-white/90 border-2 border-amber-300 rounded-2xl px-3 py-1 flex items-center gap-1 shadow-sm">
        <span class="text-xl">⭐</span>
        <span id="hud-score" class="font-extrabold text-amber-600 text-base md:text-lg">0</span>
      </div>
      <div id="hud-lives-box" class="bg-white/90 border-2 border-red-300 rounded-2xl px-3 py-1 flex items-center gap-1 shadow-sm hidden">
        <span class="text-lg">❤️</span>
        <span id="hud-lives" class="font-extrabold text-red-500 text-base md:text-lg">3</span>
      </div>
      
      <button id="btn-sound" onclick="toggleSound()" class="btn-bounce bg-white border-2 border-indigo-200 text-indigo-600 w-10 h-10 rounded-2xl flex items-center justify-center text-lg shadow-sm" title="Efek Suara">
        <i class="fa-solid fa-volume-high"></i>
      </button>
      <button id="btn-music" onclick="toggleMusic()" class="btn-bounce bg-white border-2 border-pink-200 text-pink-600 w-10 h-10 rounded-2xl flex items-center justify-center text-lg shadow-sm" title="Musik Latar">
        <i class="fa-solid fa-music"></i>
      </button>
    </div>
  </header>

  <main class="flex-1 w-full max-w-5xl mx-auto p-3 md:p-6 flex flex-col justify-center items-center">

    <!-- HOME SCREEN -->
    <section id="screen-home" class="w-full flex flex-col items-center justify-center text-center space-y-6 py-4">
      <div class="relative max-w-2xl w-full flex flex-col items-center">
        <!-- Brand Badge above Title -->
        <div class="text-sm md:text-base font-black tracking-widest text-indigo-700 bg-white/90 px-4 py-1 rounded-full shadow-md mb-2 border-2 border-indigo-300 inline-block uppercase animate-bounce">
          703Ledu
        </div>

        <div class="relative w-48 h-48 md:w-56 md:h-56 mb-2">
          <svg class="absolute inset-0 w-full h-full animate-spin" style="animation-duration: 25s;" viewBox="0 0 200 200">
            <polygon points="100,10 120,40 80,40" fill="#FBBF24" opacity="0.6"/>
            <rect x="150" y="80" width="30" height="30" fill="#3B82F6" rx="6" opacity="0.6" transform="rotate(15 165 95)"/>
            <circle cx="40" cy="140" r="18" fill="#EC4899" opacity="0.6"/>
            <polygon points="160,150 180,180 140,180" fill="#10B981" opacity="0.6"/>
          </svg>
          <svg class="w-full h-full relative z-10 animate-float" viewBox="0 0 200 200">
            <path d="M70,55 Q100,25 130,55 Z" fill="#EF4444"/>
            <ellipse cx="100" cy="55" rx="35" ry="8" fill="#DC2626"/>
            <circle cx="100" cy="80" r="32" fill="#FDE047"/>
            <circle cx="100" cy="82" r="28" fill="#FFEDD5"/>
            <circle cx="88" cy="78" r="4" fill="#1E293B"/>
            <circle cx="112" cy="78" r="4" fill="#1E293B"/>
            <circle cx="90" cy="76" r="1.5" fill="#FFFFFF"/>
            <circle cx="114" cy="76" r="1.5" fill="#FFFFFF"/>
            <circle cx="82" cy="86" r="4" fill="#FCA5A5" opacity="0.7"/>
            <circle cx="118" cy="86" r="4" fill="#FCA5A5" opacity="0.7"/>
            <path d="M92,90 Q100,100 108,90" fill="none" stroke="#B91C1C" stroke-width="3" stroke-linecap="round"/>
            <path d="M72,112 L128,112 L138,160 L62,160 Z" fill="#3B82F6" rx="5"/>
            <polygon points="100,122 103,128 110,129 105,134 106,140 100,137 94,140 95,134 90,129 97,128" fill="#FBBF24"/>
            <rect x="52" y="120" width="16" height="36" fill="#10B981" rx="4"/>
            <rect x="132" y="120" width="16" height="36" fill="#10B981" rx="4"/>
            <circle cx="60" cy="135" r="7" fill="#FFEDD5"/>
            <circle cx="140" cy="135" r="7" fill="#FFEDD5"/>
          </svg>
        </div>

        <h1 class="text-3xl md:text-5xl font-black text-indigo-900 tracking-wide drop-shadow-md leading-tight">
          PETUALANGAN BANGUN
        </h1>
        <p class="text-base md:text-xl font-semibold text-indigo-700 mt-2 bg-white/80 px-5 py-1.5 rounded-full shadow-sm border border-indigo-100">
          ✨ Jelajahi Dunia Bangun Datar dan Bangun Ruang! ✨
        </p>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 w-full max-w-md pt-2">
        <button onclick="goToScreen('screen-map')" class="btn-bounce bg-emerald-500 hover:bg-emerald-400 text-white font-extrabold text-lg md:text-xl py-4 px-6 rounded-3xl border-b-4 border-emerald-700 flex items-center justify-center gap-3">
          <i class="fa-solid fa-play text-2xl"></i> MULAI BERMAIN
        </button>
        
        <button onclick="goToScreen('screen-learn')" class="btn-bounce bg-sky-500 hover:bg-sky-400 text-white font-extrabold text-lg md:text-xl py-4 px-6 rounded-3xl border-b-4 border-sky-700 flex items-center justify-center gap-3">
          <i class="fa-solid fa-book-open text-2xl"></i> BELAJAR
        </button>

        <button onclick="goToScreen('screen-achievements')" class="btn-bounce bg-amber-500 hover:bg-amber-400 text-white font-extrabold text-lg md:text-xl py-4 px-6 rounded-3xl border-b-4 border-amber-700 flex items-center justify-center gap-3">
          <i class="fa-solid fa-trophy text-2xl"></i> PENCAPAIAN
        </button>

        <button onclick="goToScreen('screen-teacher')" class="btn-bounce bg-purple-500 hover:bg-purple-400 text-white font-extrabold text-lg md:text-xl py-4 px-6 rounded-3xl border-b-4 border-purple-700 flex items-center justify-center gap-3">
          <i class="fa-solid fa-chalkboard-user text-2xl"></i> MODE GURU
        </button>
      </div>
    </section>

    <!-- LEARN SCREEN -->
    <section id="screen-learn" class="w-full flex flex-col items-center space-y-5 hidden">
      <div class="text-center">
        <h2 class="text-2xl md:text-3xl font-extrabold text-indigo-900 flex items-center justify-center gap-2">
          📚 Ruang Belajar Geometri
        </h2>
        <p class="text-slate-600 text-sm md:text-base font-medium">Tekan kartu untuk melihat penjelasan & mendengar suaranya!</p>
      </div>

      <div class="flex gap-2 p-1 bg-white/80 rounded-2xl border-2 border-indigo-200 shadow-sm">
        <button id="tab-2d" onclick="filterLearnCards('2d')" class="px-5 py-2 rounded-xl font-bold transition text-sm md:text-base bg-indigo-600 text-white">
          📐 Bangun Datar
        </button>
        <button id="tab-3d" onclick="filterLearnCards('3d')" class="px-5 py-2 rounded-xl font-bold transition text-sm md:text-base text-slate-600 hover:bg-indigo-100">
          📦 Bangun Ruang
        </button>
      </div>

      <div id="learn-cards-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 w-full max-w-4xl max-h-[62vh] overflow-y-auto p-2">
      </div>
    </section>

    <!-- MAP SCREEN -->
    <section id="screen-map" class="w-full flex flex-col items-center space-y-6 hidden">
      <div class="text-center">
        <h2 class="text-2xl md:text-3xl font-extrabold text-indigo-900">🗺️ Peta Petualangan Bangun</h2>
        <p class="text-slate-600 text-sm md:text-base font-medium">Pilih wilayah petualanganmu dan kumpulkan semua bintang!</p>
      </div>

      <div class="w-full max-w-3xl grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
        <div id="card-lvl-1" onclick="startLevel(1)" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-emerald-400 relative overflow-hidden group">
          <div class="w-16 h-16 rounded-2xl bg-emerald-100 border-2 border-emerald-400 flex items-center justify-center text-3xl mb-3">🌳</div>
          <span class="text-xs font-bold text-emerald-600 bg-emerald-100 px-3 py-0.5 rounded-full mb-1">LEVEL 1</span>
          <h3 class="font-extrabold text-lg text-slate-800">Taman Bangun Datar</h3>
          <p class="text-xs text-slate-500 mt-1">Segitiga, Segiempat, Segi banyak & Lingkaran</p>
          <div id="status-lvl-1" class="mt-3 text-sm font-bold flex items-center gap-1 text-emerald-600">🔓 Terbuka</div>
        </div>

        <div id="card-lvl-2" onclick="startLevel(2)" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-indigo-300 opacity-90 relative overflow-hidden">
          <div class="w-16 h-16 rounded-2xl bg-indigo-100 border-2 border-indigo-400 flex items-center justify-center text-3xl mb-3">🏢</div>
          <span class="text-xs font-bold text-indigo-600 bg-indigo-100 px-3 py-0.5 rounded-full mb-1">LEVEL 2</span>
          <h3 class="font-extrabold text-lg text-slate-800">Kota Bangun Ruang</h3>
          <p class="text-xs text-slate-500 mt-1">Kubus, Balok, Kerucut & Bola</p>
          <div id="status-lvl-2" class="mt-3 text-sm font-bold flex items-center gap-1 text-slate-500">🔒 Terkunci</div>
        </div>

        <div id="card-lvl-3" onclick="startLevel(3)" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-amber-300 opacity-90 relative overflow-hidden">
          <div class="w-16 h-16 rounded-2xl bg-amber-100 border-2 border-amber-400 flex items-center justify-center text-3xl mb-3">🛠️</div>
          <span class="text-xs font-bold text-amber-600 bg-amber-100 px-3 py-0.5 rounded-full mb-1">LEVEL 3</span>
          <h3 class="font-extrabold text-lg text-slate-800">Bengkel Bentuk</h3>
          <p class="text-xs text-slate-500 mt-1">Komposisi: Menyusun Bentuk Baru</p>
          <div id="status-lvl-3" class="mt-3 text-sm font-bold flex items-center gap-1 text-slate-500">🔒 Terkunci</div>
        </div>

        <div id="card-lvl-4" onclick="startLevel(4)" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-purple-300 opacity-90 relative overflow-hidden">
          <div class="w-16 h-16 rounded-2xl bg-purple-100 border-2 border-purple-400 flex items-center justify-center text-3xl mb-3">🔍</div>
          <span class="text-xs font-bold text-purple-600 bg-purple-100 px-3 py-0.5 rounded-full mb-1">LEVEL 4</span>
          <h3 class="font-extrabold text-lg text-slate-800">Detektif Bentuk</h3>
          <p class="text-xs text-slate-500 mt-1">Dekomposisi: Menguraikan Gambaran</p>
          <div id="status-lvl-4" class="mt-3 text-sm font-bold flex items-center gap-1 text-slate-500">🔒 Terkunci</div>
        </div>

        <div id="card-lvl-5" onclick="startLevel(5)" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-rose-300 opacity-90 relative overflow-hidden">
          <div class="w-16 h-16 rounded-2xl bg-rose-100 border-2 border-rose-400 flex items-center justify-center text-3xl mb-3">📍</div>
          <span class="text-xs font-bold text-rose-600 bg-rose-100 px-3 py-0.5 rounded-full mb-1">LEVEL 5</span>
          <h3 class="font-extrabold text-lg text-slate-800">Petualangan Posisi</h3>
          <p class="text-xs text-slate-500 mt-1">Atas, Bawah, Kanan, Kiri, Dalam, Luar</p>
          <div id="status-lvl-5" class="mt-3 text-sm font-bold flex items-center gap-1 text-slate-500">🔒 Terkunci</div>
        </div>

        <div onclick="goToScreen('screen-minigames')" class="btn-bounce glass-card rounded-3xl p-5 flex flex-col items-center text-center cursor-pointer border-4 border-pink-400 bg-gradient-to-b from-pink-50 to-white">
          <div class="w-16 h-16 rounded-2xl bg-pink-100 border-2 border-pink-400 flex items-center justify-center text-3xl mb-3">🎮</div>
          <span class="text-xs font-bold text-pink-600 bg-pink-100 px-3 py-0.5 rounded-full mb-1">BONUS</span>
          <h3 class="font-extrabold text-lg text-slate-800">Mini Game Seru</h3>
          <p class="text-xs text-slate-500 mt-1">Tangkap Bentuk, Puzzle, & Cari Bentuk</p>
          <div class="mt-3 text-sm font-bold text-pink-600 flex items-center gap-1">▶ Mainkan Sekarang</div>
        </div>
      </div>

      <div class="w-full max-w-3xl pt-2">
        <button onclick="startFinalQuiz()" class="btn-bounce w-full bg-gradient-to-r from-amber-500 via-orange-500 to-red-500 hover:from-amber-400 hover:to-red-400 text-white font-black text-lg md:text-xl py-4 px-6 rounded-3xl border-b-4 border-red-700 shadow-lg flex items-center justify-center gap-3">
          🏆 TANTANGAN AKHIR (KUIS CAMPURAN 15 SOAL)
        </button>
      </div>
    </section>

    <!-- QUIZ SCREEN -->
    <section id="screen-quiz" class="w-full max-w-3xl flex flex-col items-center hidden">
      <div class="w-full glass-card rounded-3xl p-4 md:p-6 shadow-xl flex flex-col space-y-4 relative">
        <div class="flex justify-between items-center border-b pb-3 border-indigo-100">
          <div>
            <span id="quiz-level-badge" class="text-xs font-bold text-indigo-700 bg-indigo-100 px-3 py-1 rounded-full">
              LEVEL 1
            </span>
            <span id="quiz-progress-text" class="text-sm font-bold text-slate-600 ml-2">
              Soal 1 / 5
            </span>
          </div>

          <div class="flex items-center gap-2">
            <button onclick="speakCurrentQuestion()" class="btn-bounce bg-sky-100 border border-sky-300 text-sky-700 px-3 py-1 rounded-xl text-xs font-bold flex items-center gap-1">
              🔊 Baca Soal
            </button>
            <button onclick="showHintModal()" class="btn-bounce bg-amber-100 border border-amber-300 text-amber-700 px-3 py-1 rounded-xl text-xs font-bold flex items-center gap-1">
              💡 Petunjuk
            </button>
          </div>
        </div>

        <h3 id="quiz-question-title" class="text-lg md:text-2xl font-extrabold text-slate-800 text-center py-2">
          Manakah yang merupakan bangun segitiga?
        </h3>

        <div id="quiz-visual-container" class="w-full h-48 md:h-56 bg-indigo-50/80 rounded-2xl border-2 border-indigo-100 flex items-center justify-center relative overflow-hidden p-3">
        </div>

        <div id="quiz-options-container" class="grid grid-cols-1 sm:grid-cols-2 gap-3 pt-2">
        </div>

        <div id="quiz-feedback" class="hidden p-4 rounded-2xl text-center font-extrabold text-base md:text-lg animate-pulse">
        </div>
      </div>
    </section>

    <!-- COMPOSITION SCREEN (LEVEL 3) -->
    <section id="screen-composition" class="w-full max-w-3xl flex flex-col items-center hidden space-y-4">
      <div class="text-center">
        <h2 class="text-2xl font-extrabold text-indigo-900">🛠️ Bengkel Bentuk (Komposisi)</h2>
        <p id="comp-instructions" class="text-slate-600 text-sm md:text-base font-semibold">
          Susun bentuk-bentuk di bawah ini ke target garis putus-putus untuk membuat: <span class="text-indigo-600 underline font-black" id="comp-target-name">RUMAH</span>!
        </p>
      </div>

      <div class="w-full glass-card rounded-3xl p-4 flex flex-col md:flex-row gap-4 items-center justify-between">
        <div id="comp-drop-area" class="w-full md:w-2/3 h-64 md:h-80 bg-white/90 rounded-2xl border-4 border-indigo-200 relative overflow-hidden flex items-center justify-center">
        </div>

        <div class="w-full md:w-1/3 bg-indigo-50/80 p-3 rounded-2xl border-2 border-indigo-200 flex md:flex-col flex-wrap gap-3 items-center justify-center">
          <div class="text-xs font-bold text-indigo-700 w-full text-center">PILIH BENTUK:</div>
          <div id="comp-palette" class="flex md:flex-col flex-wrap gap-2 justify-center items-center">
          </div>
        </div>
      </div>

      <div class="flex gap-3">
        <button onclick="resetComposition()" class="btn-bounce bg-slate-200 text-slate-700 font-bold px-4 py-2 rounded-xl text-sm">
          🔄 Ulangi
        </button>
      </div>
    </section>

    <!-- MINI GAMES MENU SCREEN -->
    <section id="screen-minigames" class="w-full max-w-3xl flex flex-col items-center space-y-6 hidden">
      <div class="text-center">
        <h2 class="text-2xl md:text-3xl font-extrabold text-pink-700">🎮 Mini Game Matematika Seru</h2>
        <p class="text-slate-600 text-sm md:text-base">Pilih permainan seru untuk melatih ketangkasan geometri!</p>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 w-full">
        <div onclick="startMiniGame('catch')" class="btn-bounce glass-card rounded-3xl p-5 border-4 border-pink-300 cursor-pointer flex items-center gap-4 hover:bg-pink-50">
          <div class="w-16 h-16 rounded-2xl bg-pink-100 border-2 border-pink-400 flex items-center justify-center text-3xl">🎯</div>
          <div class="text-left">
            <h3 class="font-extrabold text-lg text-slate-800">Tangkap Bentuk</h3>
            <p class="text-xs text-slate-500">Tangkap bentuk yang diminta sebelum jatuh ke bawah!</p>
          </div>
        </div>

        <div onclick="startMiniGame('find')" class="btn-bounce glass-card rounded-3xl p-5 border-4 border-sky-300 cursor-pointer flex items-center gap-4 hover:bg-sky-50">
          <div class="w-16 h-16 rounded-2xl bg-sky-100 border-2 border-sky-400 flex items-center justify-center text-3xl">🔎</div>
          <div class="text-left">
            <h3 class="font-extrabold text-lg text-slate-800">Cari Bentuk Detektif</h3>
            <p class="text-xs text-slate-500">Temukan bentuk tersembunyi di dalam gambar!</p>
          </div>
        </div>

        <div onclick="startMiniGame('train')" class="btn-bounce glass-card rounded-3xl p-5 border-4 border-amber-300 cursor-pointer flex items-center gap-4 hover:bg-amber-50">
          <div class="w-16 h-16 rounded-2xl bg-amber-100 border-2 border-amber-400 flex items-center justify-center text-3xl">🚂</div>
          <div class="text-left">
            <h3 class="font-extrabold text-lg text-slate-800">Kereta Posisi</h3>
            <p class="text-xs text-slate-500">Letakkan benda di gerbong kereta sesuai petunjuk!</p>
          </div>
        </div>

        <div onclick="startMiniGame('puzzle')" class="btn-bounce glass-card rounded-3xl p-5 border-4 border-emerald-300 cursor-pointer flex items-center gap-4 hover:bg-emerald-50">
          <div class="w-16 h-16 rounded-2xl bg-emerald-100 border-2 border-emerald-400 flex items-center justify-center text-3xl">🧩</div>
          <div class="text-left">
            <h3 class="font-extrabold text-lg text-slate-800">Puzzle Bangun Datar</h3>
            <p class="text-xs text-slate-500">Susun potongan menjadi bentuk utuh!</p>
          </div>
        </div>
      </div>
    </section>

    <!-- MINI GAME PLAY CONTAINER SCREEN -->
    <section id="screen-game-play" class="w-full max-w-2xl flex flex-col items-center hidden">
      <div id="minigame-container" class="w-full glass-card rounded-3xl p-4 flex flex-col items-center relative min-h-[400px] justify-center">
      </div>
    </section>

    <!-- ACHIEVEMENTS SCREEN -->
    <section id="screen-achievements" class="w-full max-w-3xl flex flex-col items-center space-y-6 hidden">
      <div class="text-center">
        <h2 class="text-2xl md:text-3xl font-extrabold text-amber-700">🏆 Galeri Lencana Pencapaian</h2>
        <p class="text-slate-600 text-sm md:text-base">Selesaikan tantangan untuk membuka lencana kebanggaanmu!</p>
      </div>

      <div id="badges-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 w-full">
      </div>
    </section>

    <!-- TEACHER MODE SCREEN -->
    <section id="screen-teacher" class="w-full max-w-3xl flex flex-col items-center space-y-6 hidden">
      <div class="text-center">
        <h2 class="text-2xl md:text-3xl font-extrabold text-purple-900">👩‍🏫 Mode Guru & Orang Tua</h2>
        <p class="text-slate-600 text-sm md:text-base">Laporan perkembangan belajar murid secara real-time.</p>
      </div>

      <div class="w-full glass-card rounded-3xl p-6 space-y-6">
        <div class="flex flex-col sm:flex-row justify-between items-center border-b pb-4 border-slate-200 gap-3">
          <div class="flex items-center gap-3">
            <div class="w-12 h-12 rounded-2xl bg-purple-100 border-2 border-purple-400 flex items-center justify-center text-2xl">🎓</div>
            <div>
              <span class="text-xs font-bold text-slate-400">NAMA SISWA:</span>
              <h3 id="teacher-student-name" class="text-lg font-black text-slate-800">Petualang Cilik</h3>
            </div>
          </div>
          <button onclick="editStudentName()" class="btn-bounce bg-purple-100 text-purple-700 font-bold px-3 py-1.5 rounded-xl text-xs">
            ✏️ Ubah Nama
          </button>
        </div>

        <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
          <div class="bg-indigo-50 border border-indigo-200 p-3 rounded-2xl text-center">
            <span class="text-xs font-bold text-indigo-500">TOTAL SKOR</span>
            <div id="teacher-score" class="text-2xl font-black text-indigo-700">0 ⭐</div>
          </div>
          <div class="bg-emerald-50 border border-emerald-200 p-3 rounded-2xl text-center">
            <span class="text-xs font-bold text-emerald-500">JAWABAN BENAR</span>
            <div id="teacher-correct" class="text-2xl font-black text-emerald-700">0</div>
          </div>
          <div class="bg-rose-50 border border-rose-200 p-3 rounded-2xl text-center">
            <span class="text-xs font-bold text-rose-500">JAWABAN SALAH</span>
            <div id="teacher-wrong" class="text-2xl font-black text-rose-700">0</div>
          </div>
          <div class="bg-amber-50 border border-amber-200 p-3 rounded-2xl text-center">
            <span class="text-xs font-bold text-amber-500">AKURASI</span>
            <div id="teacher-accuracy" class="text-2xl font-black text-amber-700">0%</div>
          </div>
        </div>

        <div class="pt-2 border-t border-slate-200 flex justify-end">
          <button onclick="resetGameData()" class="btn-bounce bg-red-500 hover:bg-red-600 text-white font-bold px-4 py-2 rounded-xl text-sm flex items-center gap-2">
            ⚠️ RESET DATA PROGRES
          </button>
        </div>
      </div>
    </section>

    <!-- REPORT SCREEN -->
    <section id="screen-report" class="w-full max-w-2xl flex flex-col items-center space-y-6 hidden">
      <div class="w-full glass-card rounded-3xl p-6 text-center space-y-5 border-4 border-amber-400 relative overflow-hidden">
        <div class="text-5xl">🏆</div>
        <h2 class="text-3xl font-black text-amber-800">HASIL BELAJAR PETUALANGAN</h2>
        
        <div class="bg-amber-50 border-2 border-amber-200 p-3 rounded-2xl max-w-sm mx-auto">
          <span class="text-xs font-bold text-amber-600">NAMA PEJUANG MATEMATIKA:</span>
          <input type="text" id="report-input-name" placeholder="Tulis Namamu Di Sini..." class="w-full text-center font-extrabold text-lg bg-transparent border-b-2 border-amber-400 focus:outline-none text-slate-800" onchange="saveStudentName(this.value)">
        </div>

        <div class="grid grid-cols-2 gap-4 max-w-md mx-auto">
          <div class="bg-white p-3 rounded-2xl border border-amber-200">
            <span class="text-xs font-bold text-slate-400">SKOR TANTANGAN</span>
            <div id="report-score" class="text-3xl font-black text-amber-600">0 / 150</div>
          </div>
          <div class="bg-white p-3 rounded-2xl border border-amber-200">
            <span class="text-xs font-bold text-slate-400">BINTANG DILAPORKAN</span>
            <div id="report-stars" class="text-2xl">⭐⭐⭐⭐⭐</div>
          </div>
        </div>

        <div id="report-feedback-badge" class="p-4 rounded-2xl bg-emerald-100 text-emerald-800 font-extrabold text-xl">
          🌟 Sangat Hebat!
        </div>

        <button onclick="goToScreen('screen-home')" class="btn-bounce bg-emerald-500 text-white font-extrabold text-lg py-3 px-8 rounded-2xl border-b-4 border-emerald-700">
          Kembali ke Menu Utama
        </button>
      </div>
    </section>

  </main>

  <!-- HINT MODAL -->
  <div id="modal-hint" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="glass-card max-w-md w-full rounded-3xl p-6 text-center space-y-4 border-4 border-amber-300">
      <div class="text-4xl">💡</div>
      <h3 class="text-xl font-black text-amber-800">Petunjuk Bantuan</h3>
      <p id="hint-text-content" class="text-slate-700 font-medium text-base">
        Perhatikan jumlah sisi dan sudut dari bangun tersebut!
      </p>
      <button onclick="closeHintModal()" class="btn-bounce bg-amber-500 text-white font-bold py-2 px-6 rounded-2xl">
        Saya Mengerti!
      </button>
    </div>
  </div>

  <!-- REWARD MODAL -->
  <div id="modal-reward" class="fixed inset-0 bg-black/60 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
    <div class="glass-card max-w-md w-full rounded-3xl p-6 text-center space-y-4 border-4 border-emerald-400 animate-bounce">
      <div class="text-6xl">🎉</div>
      <h3 id="reward-title" class="text-2xl font-black text-emerald-800">HEBAT! LEVEL SELESAI!</h3>
      <p id="reward-desc" class="text-slate-700 font-bold text-base">Kamu berhasil menyelesaikan tantangan ini dan mendapatkan +50 Skor!</p>
      <div class="text-3xl" id="reward-badge-icon">🎖️</div>
      <button onclick="closeRewardModal()" class="btn-bounce bg-emerald-500 text-white font-extrabold text-lg py-3 px-8 rounded-2xl border-b-4 border-emerald-700">
        Lanjutkan Petualangan ▶
      </button>
    </div>
  </div>

  <script>
    let gameState = {
      score: 0,
      lives: 3,
      studentName: 'Petualang Cilik',
      levelsCompleted: [false, false, false, false, false],
      badges: {
        jagoBangunDatar: false,
        ahliBangunRuang: false,
        masterPuzzle: false,
        detektifPosisi: false,
        pahlawanMatematika: false
      },
      stats: { correct: 0, wrong: 0, startTime: Date.now() },
      soundOn: true,
      musicOn: false
    };

    let audioCtx = null;

    function playSound(type) {
      if (!gameState.soundOn) return;
      try {
        if (!audioCtx) {
          audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }
        if (audioCtx.state === 'suspended') {
          audioCtx.resume();
        }
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.connect(gain);
        gain.connect(audioCtx.destination);

        const now = audioCtx.currentTime;
        if (type === 'correct') {
          osc.type = 'sine';
          osc.frequency.setValueAtTime(523.25, now);
          osc.frequency.setValueAtTime(659.25, now + 0.1);
          gain.gain.setValueAtTime(0.3, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
          osc.start(now);
          osc.stop(now + 0.3);
        } else if (type === 'wrong') {
          osc.type = 'sawtooth';
          osc.frequency.setValueAtTime(180, now);
          osc.frequency.setValueAtTime(130, now + 0.15);
          gain.gain.setValueAtTime(0.3, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.35);
          osc.start(now);
          osc.stop(now + 0.35);
        } else if (type === 'star') {
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(587.33, now);
          osc.frequency.setValueAtTime(880, now + 0.1);
          gain.gain.setValueAtTime(0.3, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
          osc.start(now);
          osc.stop(now + 0.3);
        } else if (type === 'fanfare') {
          osc.type = 'sine';
          osc.frequency.setValueAtTime(523.25, now);
          osc.frequency.setValueAtTime(659.25, now + 0.1);
          osc.frequency.setValueAtTime(783.99, now + 0.2);
          osc.frequency.setValueAtTime(1046.50, now + 0.3);
          gain.gain.setValueAtTime(0.4, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.6);
          osc.start(now);
          osc.stop(now + 0.6);
        }
      } catch (e) {
        console.log("Audio play error");
      }
    }

    function speakText(text) {
      if (!gameState.soundOn || !('speechSynthesis' in window)) return;
      window.speechSynthesis.cancel();
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'id-ID';
      utterance.rate = 0.9;
      window.speechSynthesis.speak(utterance);
    }

    function loadSavedState() {
      const saved = localStorage.getItem('petualangan_bangun_save');
      if (saved) {
        try {
          const parsed = JSON.parse(saved);
          gameState = { ...gameState, ...parsed };
        } catch(e) {
          console.error(e);
        }
      }
      updateHUD();
      updateLevelMapUI();
    }

    function saveGameState() {
      localStorage.setItem('petualangan_bangun_save', JSON.stringify(gameState));
      updateHUD();
      updateLevelMapUI();
    }

    function updateHUD() {
      const scoreEl = document.getElementById('hud-score');
      const livesEl = document.getElementById('hud-lives');
      if (scoreEl) scoreEl.innerText = gameState.score;
      if (livesEl) livesEl.innerText = gameState.lives;

      const teacherScore = document.getElementById('teacher-score');
      const teacherCorrect = document.getElementById('teacher-correct');
      const teacherWrong = document.getElementById('teacher-wrong');
      const teacherAccuracy = document.getElementById('teacher-accuracy');
      const teacherName = document.getElementById('teacher-student-name');

      if (teacherScore) teacherScore.innerText = gameState.score + ' ⭐';
      if (teacherCorrect) teacherCorrect.innerText = gameState.stats.correct;
      if (teacherWrong) teacherWrong.innerText = gameState.stats.wrong;
      const total = gameState.stats.correct + gameState.stats.wrong;
      const acc = total > 0 ? Math.round((gameState.stats.correct / total) * 100) : 0;
      if (teacherAccuracy) teacherAccuracy.innerText = acc + '%';
      if (teacherName) teacherName.innerText = gameState.studentName;
    }

    function updateLevelMapUI() {
      for (let i = 1; i <= 5; i++) {
        const card = document.getElementById(`card-lvl-${i}`);
        const status = document.getElementById(`status-lvl-${i}`);
        if (!card || !status) continue;

        const isCompleted = gameState.levelsCompleted[i - 1];
        const isUnlocked = i === 1 || gameState.levelsCompleted[i - 2];

        if (isCompleted) {
          status.innerHTML = '⭐ Selesai!';
          status.className = 'mt-3 text-sm font-bold text-amber-600 flex items-center gap-1';
          card.classList.remove('opacity-90');
        } else if (isUnlocked) {
          status.innerHTML = '🔓 Terbuka';
          status.className = 'mt-3 text-sm font-bold text-emerald-600 flex items-center gap-1';
          card.classList.remove('opacity-90');
        } else {
          status.innerHTML = '🔒 Terkunci';
          status.className = 'mt-3 text-sm font-bold text-slate-500 flex items-center gap-1';
          card.classList.add('opacity-90');
        }
      }
    }

    function goToScreen(screenId) {
      if (activeGameInterval) {
        clearInterval(activeGameInterval);
        activeGameInterval = null;
      }

      const screens = [
        'screen-home', 'screen-learn', 'screen-map', 'screen-quiz',
        'screen-composition', 'screen-minigames', 'screen-game-play',
        'screen-achievements', 'screen-teacher', 'screen-report'
      ];
      screens.forEach(s => {
        const el = document.getElementById(s);
        if (el) el.classList.add('hidden');
      });

      const target = document.getElementById(screenId);
      if (target) target.classList.remove('hidden');

      const btnHome = document.getElementById('btn-home');
      if (screenId === 'screen-home') {
        if (btnHome) btnHome.classList.add('hidden');
      } else {
        if (btnHome) btnHome.classList.remove('hidden');
      }

      if (screenId === 'screen-learn') filterLearnCards('2d');
      if (screenId === 'screen-achievements') renderAchievements();
      if (screenId === 'screen-teacher') renderTeacherDashboard();
    }

    function toggleSound() {
      gameState.soundOn = !gameState.soundOn;
      const btn = document.getElementById('btn-sound');
      if (btn) btn.innerHTML = gameState.soundOn ? '<i class="fa-solid fa-volume-high"></i>' : '<i class="fa-solid fa-volume-xmark text-slate-400"></i>';
    }

    function toggleMusic() {
      gameState.musicOn = !gameState.musicOn;
      const btn = document.getElementById('btn-music');
      if (btn) btn.innerHTML = gameState.musicOn ? '<i class="fa-solid fa-music text-pink-600"></i>' : '<i class="fa-solid fa-music text-slate-400"></i>';
    }

    const flashcardData = {
      '2d': [
        { name: 'Segitiga', desc: 'Memiliki 3 sisi lurus dan 3 sudut.', icon: '🔺', color: 'border-red-400 bg-red-50' },
        { name: 'Segiempat', desc: 'Memiliki 4 sisi dan 4 sudut lurus.', icon: '🟦', color: 'border-blue-400 bg-blue-50' },
        { name: 'Segi Banyak', desc: 'Memiliki lebih dari 4 sisi lurus (Segilima/Segienam).', icon: '🔷', color: 'border-purple-400 bg-purple-50' },
        { name: 'Lingkaran', desc: 'Berbentuk bulat dan tidak memiliki sisi lurus.', icon: '🟡', color: 'border-amber-400 bg-amber-50' }
      ],
      '3d': [
        { name: 'Kubus', desc: 'Memiliki 6 sisi persegi yang sama besar. Contoh: Dadu.', icon: '🎲', color: 'border-emerald-400 bg-emerald-50' },
        { name: 'Balok', desc: 'Memiliki 6 sisi berbentuk persegi panjang. Contoh: Kotak sepatu.', icon: '📦', color: 'border-sky-400 bg-sky-50' },
        { name: 'Kerucut', desc: 'Memiliki alas lingkaran dan ujung runcing. Contoh: Topi pesta.', icon: '🍦', color: 'border-pink-400 bg-pink-50' },
        { name: 'Bola', desc: 'Berbentuk bulat sempurna tanpa sudut. Contoh: Bola sepak.', icon: '⚽', color: 'border-orange-400 bg-orange-50' }
      ]
    };

    function filterLearnCards(category) {
      const grid = document.getElementById('learn-cards-grid');
      const tab2d = document.getElementById('tab-2d');
      const tab3d = document.getElementById('tab-3d');
      if (!grid) return;

      if (category === '2d') {
        tab2d.className = 'px-5 py-2 rounded-xl font-bold transition text-sm md:text-base bg-indigo-600 text-white';
        tab3d.className = 'px-5 py-2 rounded-xl font-bold transition text-sm md:text-base text-slate-600 hover:bg-indigo-100';
      } else {
        tab3d.className = 'px-5 py-2 rounded-xl font-bold transition text-sm md:text-base bg-indigo-600 text-white';
        tab2d.className = 'px-5 py-2 rounded-xl font-bold transition text-sm md:text-base text-slate-600 hover:bg-indigo-100';
      }

      grid.innerHTML = '';
      flashcardData[category].forEach(item => {
        const card = document.createElement('div');
        card.className = `btn-bounce p-5 rounded-3xl border-4 ${item.color} flex flex-col items-center text-center cursor-pointer shadow-sm`;
        card.onclick = () => {
          playSound('star');
          speakText(`${item.name}. ${item.desc}`);
        };
        card.innerHTML = `
          <div class="text-5xl mb-3">${item.icon}</div>
          <h3 class="font-extrabold text-xl text-slate-800">${item.name}</h3>
          <p class="text-xs md:text-sm text-slate-600 mt-2 font-medium">${item.desc}</p>
          <div class="mt-3 text-xs bg-white/80 border border-slate-200 px-3 py-1 rounded-full text-slate-500 font-bold">🔊 Tekan untuk suara</div>
        `;
        grid.appendChild(card);
      });
    }

    const quizDatabase = {
      level1: [
        {
          title: "Manakah yang merupakan bangun Segitiga?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><polygon points="100,20 150,100 50,100" fill="#EF4444" stroke="#B91C1C" stroke-width="4"/></svg>`,
          options: ["Segitiga", "Segiempat", "Lingkaran", "Segi Banyak"],
          answer: 0,
          hint: "Hitung jumlah sisinya! Bangun ini punya 3 sisi."
        },
        {
          title: "Berapa jumlah sisi lurus pada Segiempat?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><rect x="50" y="20" width="100" height="80" fill="#3B82F6" rx="4" stroke="#1D4ED8" stroke-width="4"/></svg>`,
          options: ["3 Sisi", "4 Sisi", "5 Sisi", "Tidak ada sisi"],
          answer: 1,
          hint: "Bangun segiempat (seperti persegi) memiliki 4 sisi lurus."
        },
        {
          title: "Bangun apakah yang tidak memiliki sisi lurus dan berbentuk bulat?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><circle cx="100" cy="60" r="45" fill="#F59E0B" stroke="#D97706" stroke-width="4"/></svg>`,
          options: ["Segitiga", "Segi Banyak", "Lingkaran", "Kubus"],
          answer: 2,
          hint: "Bentuknya seperti koin atau roda mobil!"
        }
      ],
      level2: [
        {
          title: "Benda manakah yang berbentuk BOLA?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><circle cx="100" cy="60" r="40" fill="#38BDF8"/><path d="M70 40 Q100 70 130 40 M70 80 Q100 50 130 80" stroke="#0284C7" stroke-width="3" fill="none"/></svg>`,
          options: ["⚽ Bola Sepak", "🎲 Dadu", "📦 Kotak Sepatu", "🍦 Topi Pesta"],
          answer: 0,
          hint: "Benda yang sering ditendang saat bermain di lapangan!"
        },
        {
          title: "Dadu permainan berbentuk bangun ruang...",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><rect x="60" y="20" width="80" height="80" fill="#10B981" rx="8"/><circle cx="80" cy="40" r="5" fill="#FFF"/><circle cx="120" cy="80" r="5" fill="#FFF"/><circle cx="100" cy="60" r="5" fill="#FFF"/></svg>`,
          options: ["Balok", "Kubus", "Kerucut", "Bola"],
          answer: 1,
          hint: "Kubus memiliki 6 sisi berbentuk persegi sama besar."
        }
      ],
      level4: [
        {
          title: "Gambar Rumah ini tersusun dari bangun datar apa saja?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><polygon points="100,20 150,60 50,60" fill="#EF4444"/><rect x="60" y="60" width="80" height="50" fill="#F59E0B"/><rect x="90" y="80" width="20" height="30" fill="#3B82F6"/></svg>`,
          options: ["Segitiga & Segiempat", "Hanya Lingkaran", "Bola & Kerucut", "Segi Banyak"],
          answer: 0,
          hint: "Atapnya berbentuk segitiga, dan badannya berbentuk segiempat."
        }
      ],
      level5: [
        {
          title: "Di manakah posisi Kucing 🐱 terhadap meja?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><rect x="40" y="60" width="120" height="15" fill="#78350F"/><rect x="50" y="75" width="10" height="35" fill="#78350F"/><rect x="140" y="75" width="10" height="35" fill="#78350F"/><text x="90" y="45" font-size="28">🐱</text></svg>`,
          options: ["Di atas meja", "Di bawah meja", "Di dalam meja", "Di belakang meja"],
          answer: 0,
          hint: "Kucing berada di bagian paling atas papan meja."
        },
        {
          title: "Di manakah posisi Bola ⚽ terhadap meja?",
          svg: `<svg viewBox="0 0 200 120" class="w-full h-full max-w-xs"><rect x="40" y="50" width="120" height="15" fill="#78350F"/><rect x="50" y="65" width="10" height="40" fill="#78350F"/><rect x="140" y="65" width="10" height="40" fill="#78350F"/><text x="90" y="95" font-size="24">⚽</text></svg>`,
          options: ["Di atas meja", "Di bawah meja", "Di luar rumah", "Di dalam tas"],
          answer: 1,
          hint: "Bola berada di lantai di bawah kolong meja."
        }
      ]
    };

    let currentQuizQuestions = [];
    let currentQuestionIdx = 0;
    let currentLevel = 1;

    function startLevel(lvl) {
      if (lvl > 1 && !gameState.levelsCompleted[lvl - 2]) {
        playSound('wrong');
        speakText("Level ini masih terkunci! Selesaikan level sebelumnya terlebih dahulu.");
        return;
      }

      currentLevel = lvl;

      if (lvl === 3) {
        startCompositionLevel();
        return;
      }

      const key = `level${lvl}`;
      currentQuizQuestions = quizDatabase[key] || quizDatabase.level1;
      currentQuestionIdx = 0;

      goToScreen('screen-quiz');
      renderQuizQuestion();
    }

    function renderQuizQuestion() {
      const q = currentQuizQuestions[currentQuestionIdx];
      if (!q) return;

      document.getElementById('quiz-level-badge').innerText = currentLevel === 'AKHIR' ? 'TANTANGAN AKHIR' : `LEVEL ${currentLevel}`;
      document.getElementById('quiz-progress-text').innerText = `Soal ${currentQuestionIdx + 1} / ${currentQuizQuestions.length}`;
      document.getElementById('quiz-question-title').innerText = q.title;
      document.getElementById('quiz-visual-container').innerHTML = q.svg;

      const optsContainer = document.getElementById('quiz-options-container');
      optsContainer.innerHTML = '';

      q.options.forEach((optText, idx) => {
        const btn = document.createElement('button');
        btn.className = "btn-bounce bg-white border-2 border-indigo-200 hover:border-indigo-500 font-extrabold text-slate-800 p-4 rounded-2xl text-base md:text-lg shadow-sm flex items-center justify-center text-center";
        btn.innerText = optText;
        btn.onclick = () => checkQuizAnswer(idx);
        optsContainer.appendChild(btn);
      });

      const feedback = document.getElementById('quiz-feedback');
      feedback.className = 'hidden p-4 rounded-2xl text-center font-extrabold text-base md:text-lg animate-pulse';

      speakText(q.title);
    }

    function checkQuizAnswer(optionIdx) {
      const q = currentQuizQuestions[currentQuestionIdx];
      const feedback = document.getElementById('quiz-feedback');
      feedback.classList.remove('hidden');

      if (optionIdx === q.answer) {
        playSound('correct');
        gameState.score += 10;
        gameState.stats.correct++;
        feedback.className = 'p-4 rounded-2xl text-center font-extrabold text-base md:text-lg bg-emerald-100 text-emerald-800';
        feedback.innerText = '🎉 HEBAT! Jawabanmu Benar (+10 ⭐)';

        saveGameState();

        setTimeout(() => {
          currentQuestionIdx++;
          if (currentQuestionIdx < currentQuizQuestions.length) {
            renderQuizQuestion();
          } else {
            completeLevelReward();
          }
        }, 1200);
      } else {
        playSound('wrong');
        gameState.stats.wrong++;
        feedback.className = 'p-4 rounded-2xl text-center font-extrabold text-base md:text-lg bg-rose-100 text-rose-800';
        feedback.innerText = 'Coba Lagi! ' + q.hint;
        saveGameState();
      }
    }

    function speakCurrentQuestion() {
      const q = currentQuizQuestions[currentQuestionIdx];
      if (q) speakText(q.title);
    }

    function showHintModal() {
      const q = currentQuizQuestions[currentQuestionIdx];
      if (q) {
        document.getElementById('hint-text-content').innerText = q.hint;
        document.getElementById('modal-hint').classList.remove('hidden');
        speakText(q.hint);
      }
    }

    function closeHintModal() {
      document.getElementById('modal-hint').classList.add('hidden');
    }

    let compPlaced = [];
    const compTargets = [
      { name: 'RUMAH', pieces: ['Segitiga Atap', 'Persegi Badan', 'Pintu'] },
      { name: 'ROKET', pieces: ['Kerucut Atas', 'Badan Utama', 'Sayap'] }
    ];
    let currentCompTargetIdx = 0;

    function startCompositionLevel() {
      goToScreen('screen-composition');
      currentCompTargetIdx = 0;
      compPlaced = [];
      renderCompositionUI();
    }

    function renderCompositionUI() {
      const target = compTargets[currentCompTargetIdx];
      document.getElementById('comp-target-name').innerText = target.name;

      const dropArea = document.getElementById('comp-drop-area');
      dropArea.innerHTML = `
        <svg viewBox="0 0 200 180" class="w-full h-full max-w-xs">
          <!-- Roof/Top piece -->
          <polygon points="100,20 160,70 40,70" fill="${compPlaced.includes(0) ? '#EF4444' : '#E2E8F0'}" stroke="#94A3B8" stroke-dasharray="${compPlaced.includes(0) ? '0' : '4'}" stroke-width="3"/>
          <!-- Body piece -->
          <rect x="50" y="70" width="100" height="80" fill="${compPlaced.includes(1) ? '#3B82F6' : '#E2E8F0'}" stroke="#94A3B8" stroke-dasharray="${compPlaced.includes(1) ? '0' : '4'}" stroke-width="3"/>
          <!-- Door piece -->
          <rect x="85" y="100" width="30" height="50" fill="${compPlaced.includes(2) ? '#F59E0B' : '#E2E8F0'}" stroke="#94A3B8" stroke-dasharray="${compPlaced.includes(2) ? '0' : '4'}" stroke-width="3"/>
        </svg>
      `;

      const palette = document.getElementById('comp-palette');
      palette.innerHTML = '';

      target.pieces.forEach((pieceName, idx) => {
        if (!compPlaced.includes(idx)) {
          const btn = document.createElement('button');
          btn.className = "btn-bounce bg-white border-2 border-indigo-300 text-indigo-800 font-bold px-3 py-2 rounded-xl text-xs flex items-center gap-1 shadow-sm";
          btn.innerText = `🧩 ${pieceName}`;
          btn.onclick = () => placeCompPiece(idx);
          palette.appendChild(btn);
        }
      });
    }

    function placeCompPiece(idx) {
      playSound('star');
      compPlaced.push(idx);
      renderCompositionUI();

      const target = compTargets[currentCompTargetIdx];
      if (compPlaced.length >= target.pieces.length) {
        setTimeout(() => {
          playSound('fanfare');
          gameState.score += 50;
          gameState.levelsCompleted[2] = true;
          gameState.badges.masterPuzzle = true;
          saveGameState();
          showRewardModal("LUAR BIASA!", "Kamu berhasil menyusun bentuk rumah dengan sempurna!", "🏅");
        }, 500);
      }
    }

    function resetComposition() {
      compPlaced = [];
      renderCompositionUI();
    }

    let activeGameInterval = null;

    function startMiniGame(type) {
      goToScreen('screen-game-play');
      const container = document.getElementById('minigame-container');
      container.innerHTML = '';

      if (type === 'catch') {
        runCatchMiniGame(container);
      } else if (type === 'find') {
        runFindShapeMiniGame(container);
      } else if (type === 'train') {
        runTrainMiniGame(container);
      } else if (type === 'puzzle') {
        runPuzzleMiniGame(container);
      }
    }

    // 1. MINI GAME: Tangkap Bentuk
    function runCatchMiniGame(container) {
      container.innerHTML = `
        <div class="w-full text-center mb-2">
          <h3 class="text-xl font-black text-pink-700">🎯 Tangkap Semua Lingkaran!</h3>
          <p class="text-xs font-bold text-slate-500">Ketuk bentuk Lingkaran 🟡 sebelum menyentuh bawah!</p>
          <div class="text-sm font-extrabold text-pink-600 mt-1">Skor Tangkap: <span id="catch-score">0</span> / 5</div>
        </div>
        <div id="catch-box" class="w-full h-64 bg-slate-900 rounded-2xl relative overflow-hidden cursor-pointer border-4 border-pink-300">
        </div>
      `;

      let catchScore = 0;
      const catchBox = document.getElementById('catch-box');
      
      activeGameInterval = setInterval(() => {
        if (!document.getElementById('catch-box')) {
          clearInterval(activeGameInterval);
          return;
        }

        const isTarget = Math.random() < 0.6;
        const el = document.createElement('div');
        el.className = 'absolute text-3xl cursor-pointer transition-transform active:scale-125';
        el.innerText = isTarget ? '🟡' : (Math.random() > 0.5 ? '🔺' : '🟦');
        el.style.left = Math.floor(Math.random() * (catchBox.clientWidth - 40)) + 'px';
        el.style.top = '0px';

        let pos = 0;
        const speed = 2 + Math.random() * 2;
        const fall = setInterval(() => {
          pos += speed;
          el.style.top = pos + 'px';
          if (pos > catchBox.clientHeight - 40) {
            clearInterval(fall);
            if (el.parentNode) el.parentNode.removeChild(el);
          }
        }, 30);

        el.onclick = () => {
          clearInterval(fall);
          if (el.parentNode) el.parentNode.removeChild(el);
          if (isTarget) {
            playSound('correct');
            catchScore++;
            document.getElementById('catch-score').innerText = catchScore;
            if (catchScore >= 5) {
              clearInterval(activeGameInterval);
              gameState.score += 20;
              saveGameState();
              showRewardModal("JAGOAN TANGKAP!", "Kamu berhasil menangkap 5 Lingkaran! (+20 ⭐)", "🎯");
            }
          } else {
            playSound('wrong');
          }
        };

        catchBox.appendChild(el);
      }, 1200);
    }

    // 2. MINI GAME: Cari Bentuk Detektif
    function runFindShapeMiniGame(container) {
      let shapesFound = 0;
      const totalToFind = 4;

      container.innerHTML = `
        <div class="w-full text-center mb-2">
          <h3 class="text-xl font-black text-sky-700">🔎 Detektif Bentuk Tersembunyi</h3>
          <p class="text-xs font-bold text-slate-500">Temukan 4 Bentuk Geometri (Segitiga, Lingkaran, Persegi, Oval) di gambar!</p>
          <div class="text-sm font-extrabold text-sky-600 mt-1">Ditemukan: <span id="find-count">0</span> / 4</div>
        </div>

        <div class="relative w-full max-w-md h-64 bg-emerald-100 rounded-2xl border-4 border-sky-400 overflow-hidden shadow-inner flex items-center justify-center">
          <svg viewBox="0 0 400 250" class="w-full h-full">
            <!-- Background Scenery -->
            <rect x="0" y="160" width="400" height="90" fill="#86EFAC"/>
            <path d="M-20 160 Q60 80 140 160 Q240 70 340 160" fill="#4ADE80"/>
            
            <!-- Hidden Shape 1: Triangle Roof (Top Left) -->
            <polygon id="hidden-tri" points="80,60 120,110 40,110" fill="#F87171" class="cursor-pointer hover:opacity-80"/>
            
            <!-- Hidden Shape 2: Circle Sun (Top Right) -->
            <circle id="hidden-circle" cx="330" cy="50" r="30" fill="#FBBF24" class="cursor-pointer hover:opacity-80"/>

            <!-- Hidden Shape 3: Square House Window -->
            <rect id="hidden-square" x="60" y="120" width="40" height="40" fill="#60A5FA" class="cursor-pointer hover:opacity-80"/>

            <!-- Hidden Shape 4: Oval Pond (Bottom Right) -->
            <ellipse id="hidden-oval" cx="280" cy="200" rx="45" ry="22" fill="#38BDF8" class="cursor-pointer hover:opacity-80"/>
          </svg>
        </div>
      `;

      const shapes = [
        { id: 'hidden-tri', name: 'Segitiga' },
        { id: 'hidden-circle', name: 'Lingkaran' },
        { id: 'hidden-square', name: 'Persegi' },
        { id: 'hidden-oval', name: 'Oval' }
      ];

      shapes.forEach(item => {
        const el = document.getElementById(item.id);
        if (el) {
          el.onclick = () => {
            if (el.getAttribute('data-found') === 'true') return;
            el.setAttribute('data-found', 'true');
            el.classList.add('found-shape');
            playSound('correct');
            shapesFound++;
            document.getElementById('find-count').innerText = shapesFound;
            speakText(`Kamu menemukan ${item.name}!`);

            if (shapesFound >= totalToFind) {
              setTimeout(() => {
                gameState.score += 20;
                saveGameState();
                showRewardModal("DETEKTIF HEBAT!", "Kamu berhasil menemukan semua bentuk tersembunyi! (+20 ⭐)", "🔎");
              }, 600);
            }
          };
        }
      });
    }

    // 3. MINI GAME: Kereta Posisi
    function runTrainMiniGame(container) {
      const trainRounds = [
        {
          question: "Di manakah posisi Kucing 🐱 di Kereta?",
          svg: `
            <svg viewBox="0 0 320 120" class="w-full h-full">
              <!-- Engine -->
              <rect x="20" y="40" width="70" height="50" fill="#EF4444" rx="6"/>
              <circle cx="35" cy="95" r="10" fill="#1E293B"/>
              <circle cx="75" cy="95" r="10" fill="#1E293B"/>
              <!-- Wagon 1 -->
              <rect x="100" y="50" width="70" height="40" fill="#3B82F6" rx="6"/>
              <circle cx="115" cy="95" r="10" fill="#1E293B"/>
              <circle cx="155" cy="95" r="10" fill="#1E293B"/>
              <!-- Cat on top of wagon 1 -->
              <text x="125" y="42" font-size="24">🐱</text>
            </svg>
          `,
          options: ["Di atas gerbong", "Di dalam gerbong", "Di belakang kereta"],
          answer: 0
        },
        {
          question: "Di manakah posisi Bintang ⭐ di Kereta?",
          svg: `
            <svg viewBox="0 0 320 120" class="w-full h-full">
              <!-- Engine -->
              <rect x="20" y="40" width="70" height="50" fill="#EF4444" rx="6"/>
              <circle cx="35" cy="95" r="10" fill="#1E293B"/>
              <circle cx="75" cy="95" r="10" fill="#1E293B"/>
              <!-- Wagon 1 with star inside -->
              <rect x="100" y="50" width="70" height="40" fill="#10B981" rx="6"/>
              <circle cx="115" cy="95" r="10" fill="#1E293B"/>
              <circle cx="155" cy="95" r="10" fill="#1E293B"/>
              <text x="123" y="78" font-size="22">⭐</text>
            </svg>
          `,
          options: ["Di luar gerbong", "Di dalam gerbong", "Di bawah roda"],
          answer: 1
        }
      ];

      let roundIdx = 0;

      function renderTrainRound() {
        const r = trainRounds[roundIdx];
        container.innerHTML = `
          <div class="w-full text-center mb-2">
            <h3 class="text-xl font-black text-amber-700">🚂 Kereta Posisi</h3>
            <p class="text-xs font-bold text-slate-500">${r.question}</p>
          </div>
          <div class="w-full h-40 bg-amber-50 rounded-2xl border-2 border-amber-200 flex items-center justify-center p-2 mb-3">
            ${r.svg}
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-2 w-full" id="train-opts">
          </div>
        `;

        const opts = document.getElementById('train-opts');
        r.options.forEach((opt, idx) => {
          const btn = document.createElement('button');
          btn.className = "btn-bounce bg-white border-2 border-amber-300 font-extrabold text-slate-800 p-3 rounded-xl text-sm";
          btn.innerText = opt;
          btn.onclick = () => {
            if (idx === r.answer) {
              playSound('correct');
              roundIdx++;
              if (roundIdx < trainRounds.length) {
                renderTrainRound();
              } else {
                gameState.score += 20;
                gameState.badges.detektifPosisi = true;
                saveGameState();
                showRewardModal("MASINIS HEBAT!", "Kamu berhasil menentukan posisi benda di Kereta! (+20 ⭐)", "🚂");
              }
            } else {
              playSound('wrong');
            }
          };
          opts.appendChild(btn);
        });
      }

      renderTrainRound();
    }

    // 4. MINI GAME: Puzzle Bangun Datar
    function runPuzzleMiniGame(container) {
      let placedPieces = [];
      const totalPieces = 3;

      function renderPuzzleUI() {
        container.innerHTML = `
          <div class="w-full text-center mb-2">
            <h3 class="text-xl font-black text-emerald-700">🧩 Puzzle Bangun Rocket</h3>
            <p class="text-xs font-bold text-slate-500">Klik potongan bentuk untuk merakit Roket!</p>
          </div>

          <div class="w-full h-52 bg-slate-900 rounded-2xl border-4 border-emerald-400 flex items-center justify-center relative p-2">
            <svg viewBox="0 0 200 160" class="w-full h-full max-w-xs">
              <!-- Rocket Nose Cone (Triangle) -->
              <polygon points="100,10 130,50 70,50" fill="${placedPieces.includes(0) ? '#EF4444' : '#334155'}" stroke="#10B981" stroke-dasharray="4"/>
              <!-- Rocket Body (Rectangle) -->
              <rect x="70" y="50" width="60" height="70" fill="${placedPieces.includes(1) ? '#3B82F6' : '#334155'}" stroke="#10B981" stroke-dasharray="4"/>
              <!-- Rocket Fins (Triangles) -->
              <polygon points="70,90 40,120 70,120" fill="${placedPieces.includes(2) ? '#F59E0B' : '#334155'}" stroke="#10B981" stroke-dasharray="4"/>
              <polygon points="130,90 160,120 130,120" fill="${placedPieces.includes(2) ? '#F59E0B' : '#334155'}" stroke="#10B981" stroke-dasharray="4"/>
            </svg>
          </div>

          <div id="puzzle-pieces" class="flex gap-2 mt-3 flex-wrap justify-center">
          </div>
        `;

        const pieceBox = document.getElementById('puzzle-pieces');
        const pieces = [
          { name: '🔺 Kerucut Atas', idx: 0 },
          { name: '🟦 Badan Utama', idx: 1 },
          { name: '📐 Sayap Roket', idx: 2 }
        ];

        pieces.forEach(p => {
          if (!placedPieces.includes(p.idx)) {
            const btn = document.createElement('button');
            btn.className = "btn-bounce bg-white border-2 border-emerald-400 font-extrabold text-slate-800 px-3 py-2 rounded-xl text-xs";
            btn.innerText = p.name;
            btn.onclick = () => {
              playSound('star');
              placedPieces.push(p.idx);
              renderPuzzleUI();
              if (placedPieces.length >= totalPieces) {
                setTimeout(() => {
                  gameState.score += 20;
                  gameState.badges.masterPuzzle = true;
                  saveGameState();
                  showRewardModal("MASTER PUZZLE!", "Roket berhasil dirakit dengan sempurna! (+20 ⭐)", "🧩");
                }, 500);
              }
            };
            pieceBox.appendChild(btn);
          }
        });
      }

      renderPuzzleUI();
    }

    function startFinalQuiz() {
      currentLevel = 'AKHIR';
      currentQuizQuestions = [
        ...quizDatabase.level1,
        ...quizDatabase.level2,
        ...quizDatabase.level4,
        ...quizDatabase.level5
      ];
      currentQuestionIdx = 0;
      goToScreen('screen-quiz');
      renderQuizQuestion();
    }

    function completeLevelReward() {
      playSound('fanfare');
      gameState.score += 50;
      if (typeof currentLevel === 'number' && currentLevel >= 1 && currentLevel <= 5) {
        gameState.levelsCompleted[currentLevel - 1] = true;
        if (currentLevel === 1) gameState.badges.jagoBangunDatar = true;
        if (currentLevel === 2) gameState.badges.ahliBangunRuang = true;
        if (currentLevel === 5) gameState.badges.detektifPosisi = true;
      }
      saveGameState();

      showRewardModal("HEBAT! LEVEL SELESAI!", `Kamu menyelesaikan Level ${currentLevel} dan mendapat +50 ⭐!`, "🏆");
    }

    function finishFinalQuizReport() {
      goToScreen('screen-report');
      document.getElementById('report-score').innerText = `${gameState.score} / 150`;
      
      let badgeText = "🌟 Sangat Hebat!";
      if (gameState.score < 80) badgeText = "💪 Ayo Berlatih Lagi!";
      else if (gameState.score < 110) badgeText = "👍 Bagus!";
      else if (gameState.score < 135) badgeText = "🎉 Hebat!";

      document.getElementById('report-feedback-badge').innerText = badgeText;
      speakText(`Selamat! ${gameState.studentName}. ${badgeText}`);
    }

    function showRewardModal(title, desc, icon) {
      document.getElementById('reward-title').innerText = title;
      document.getElementById('reward-desc').innerText = desc;
      document.getElementById('reward-badge-icon').innerText = icon;
      document.getElementById('modal-reward').classList.remove('hidden');
      speakText(`${title}. ${desc}`);
    }

    function closeRewardModal() {
      document.getElementById('modal-reward').classList.add('hidden');
      if (currentLevel === 'AKHIR') {
        finishFinalQuizReport();
      } else {
        goToScreen('screen-map');
      }
    }

    function renderAchievements() {
      const grid = document.getElementById('badges-grid');
      if (!grid) return;
      grid.innerHTML = '';

      const list = [
        { key: 'jagoBangunDatar', name: 'Jago Bangun Datar', icon: '🏅', desc: 'Selesaikan Level 1' },
        { key: 'ahliBangunRuang', name: 'Ahli Bangun Ruang', icon: '📦', desc: 'Selesaikan Level 2' },
        { key: 'masterPuzzle', name: 'Master Puzzle', icon: '🧩', desc: 'Selesaikan Bengkel Bentuk' },
        { key: 'detektifPosisi', name: 'Detektif Posisi', icon: '📍', desc: 'Selesaikan Level 5' },
        { key: 'pahlawanMatematika', name: 'Pahlawan Matematika', icon: '🏆', desc: 'Selesaikan Tantangan Akhir' }
      ];

      list.forEach(item => {
        const unlocked = gameState.badges[item.key];
        const card = document.createElement('div');
        card.className = `p-4 rounded-2xl border-4 ${unlocked ? 'border-amber-400 bg-amber-50' : 'border-slate-300 bg-slate-100 opacity-60'} flex items-center gap-3`;
        card.innerHTML = `
          <div class="text-4xl">${unlocked ? item.icon : '🔒'}</div>
          <div>
            <h4 class="font-extrabold text-slate-800 text-sm">${item.name}</h4>
            <p class="text-xs text-slate-500">${item.desc}</p>
            <span class="text-[10px] font-bold ${unlocked ? 'text-emerald-600' : 'text-slate-400'}">${unlocked ? '✅ Terbuka' : '🔒 Terkunci'}</span>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    function renderTeacherDashboard() {
      updateHUD();
    }

    function editStudentName() {
      const name = prompt("Masukkan Nama Siswa:", gameState.studentName);
      if (name && name.trim() !== "") {
        saveStudentName(name.trim());
      }
    }

    function saveStudentName(name) {
      gameState.studentName = name;
      saveGameState();
    }

    function resetGameData() {
      if (confirm("Apakah Anda yakin ingin menghapus seluruh progres belajar?")) {
        localStorage.removeItem('petualangan_bangun_save');
        gameState = {
          score: 0,
          lives: 3,
          studentName: 'Petualang Cilik',
          levelsCompleted: [false, false, false, false, false],
          badges: { jagoBangunDatar: false, ahliBangunRuang: false, masterPuzzle: false, detektifPosisi: false, pahlawanMatematika: false },
          stats: { correct: 0, wrong: 0, startTime: Date.now() },
          soundOn: true,
          musicOn: false
        };
        saveGameState();
        goToScreen('screen-home');
      }
    }

    window.onload = function() {
      loadSavedState();
      console.log("PETUALANGAN BANGUN initialized successfully!");
    };
  </script>
</body>
</html>
