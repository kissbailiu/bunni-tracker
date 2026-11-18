<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Doce Meta 🍓 — Monitor de Calorias</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-page: #fff5f8;
      --bg-gradient: radial-gradient(circle at top left, #ffe3ee 0%, #fff6f9 45%, #fff0f6 100%);
      --card-bg: rgba(255, 255, 255, 0.92);
      --pink-50: #fff0f5;
      --pink-100: #ffe0ec;
      --pink-200: #ffc2d9;
      --pink-300: #ff9ec2;
      --pink-400: #ff6b9d;
      --pink-500: #e64980;
      --pink-600: #c2255c;
      --text-main: #4a2c38;
      --text-muted: #8f6b7a;
      --border-soft: #ffd6e6;
      --shadow-soft: 0 10px 28px rgba(230, 73, 128, 0.10);
      --carb-color: #ff922b;
      --prot-color: #e64980;
      --fat-color: #be4bdb;
      --water-color: #4dabf7;
      --steps-color: #f06595;
      --radius-lg: 22px;
      --radius-md: 15px;
      --radius-sm: 10px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Quicksand', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      background: var(--bg-page);
      background-image: var(--bg-gradient);
      background-attachment: fixed;
      color: var(--text-main);
      min-height: 100vh;
      line-height: 1.5;
      padding-bottom: 50px;
    }

    button, input, select {
      font-family: inherit;
    }

    .container {
      max-width: 980px;
      margin: 0 auto;
      padding: 18px 16px;
    }

    /* Header */
    .header {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      background: var(--card-bg);
      border: 1.5px solid var(--border-soft);
      border-radius: var(--radius-lg);
      padding: 16px 22px;
      box-shadow: var(--shadow-soft);
      margin-bottom: 18px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .brand-icon {
      width: 48px;
      height: 48px;
      border-radius: 16px;
      background: linear-gradient(135deg, #ff85b3, #ffc2d9);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 25px;
      box-shadow: 0 6px 14px rgba(255, 107, 157, 0.25);
    }

    .brand h1 {
      font-size: 1.45rem;
      color: var(--pink-600);
      font-weight: 700;
      letter-spacing: -0.3px;
    }

    .brand p {
      font-size: 0.85rem;
      color: var(--text-muted);
      font-weight: 600;
    }

    /* Date Controls */
    .date-bar {
      display: flex;
      align-items: center;
      gap: 8px;
      background: var(--pink-50);
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px solid var(--pink-200);
    }

    .date-btn {
      background: white;
      border: 1px solid var(--pink-200);
      color: var(--pink-600);
      width: 32px;
      height: 32px;
      border-radius: 50%;
      cursor: pointer;
      font-weight: 700;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: 0.2s;
    }

    .date-btn:hover {
      background: var(--pink-400);
      color: white;
      border-color: var(--pink-400);
    }

    .date-label-btn {
      background: transparent;
      border: none;
      color: var(--text-main);
      font-weight: 700;
      font-size: 0.92rem;
      padding: 4px 10px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    /* Navigation Tabs */
    .nav-tabs {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .nav-tab {
      flex: 1;
      min-width: 130px;
      background: var(--card-bg);
      border: 1.5px solid var(--border-soft);
      color: var(--text-muted);
      padding: 12px 16px;
      border-radius: var(--radius-md);
      font-weight: 700;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      box-shadow: 0 4px 12px rgba(230, 73, 128, 0.05);
    }

    .nav-tab:hover {
      border-color: var(--pink-300);
      color: var(--pink-600);
    }

    .nav-tab.active {
      background: linear-gradient(135deg, var(--pink-400), var(--pink-500));
      color: white;
      border-color: transparent;
      box-shadow: 0 8px 18px rgba(230, 73, 128, 0.28);
    }

    /* Views */
    .view {
      display: none;
    }

    .view.active {
      display: block;
      animation: fadeIn 0.25s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Cards */
    .card {
      background: var(--card-bg);
      border: 1.5px solid var(--border-soft);
      border-radius: var(--radius-lg);
      padding: 20px;
      box-shadow: var(--shadow-soft);
      margin-bottom: 18px;
    }

    .card-title {
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--pink-600);
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .grid-2 {
      display: grid;
      grid-template-columns: 1.25fr 1fr;
      gap: 18px;
    }

    @media (max-width: 780px) {
      .grid-2 {
        grid-template-columns: 1fr;
      }
    }

    /* Calorie Ring Summary */
    .calorie-hero {
      display: flex;
      align-items: center;
      gap: 22px;
      flex-wrap: wrap;
    }

    .ring-wrapper {
      position: relative;
      width: 142px;
      height: 142px;
      flex-shrink: 0;
      margin: 0 auto;
    }

    .ring-svg {
      transform: rotate(-90deg);
      width: 142px;
      height: 142px;
    }

    .ring-bg {
      fill: none;
      stroke: var(--pink-100);
      stroke-width: 12;
    }

    .ring-progress {
      fill: none;
      stroke: url(#pinkGrad);
      stroke-width: 12;
      stroke-linecap: round;
      transition: stroke-dashoffset 0.5s ease;
    }

    .ring-center {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
    }

    .ring-center .kcal-val {
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--pink-600);
      line-height: 1.1;
    }

    .ring-center .kcal-sub {
      font-size: 0.75rem;
      color: var(--text-muted);
      font-weight: 700;
    }

    .calorie-stats {
      flex: 1;
      min-width: 210px;
    }

    .stat-pills {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-bottom: 14px;
    }

    .stat-pill {
      background: var(--pink-50);
      border: 1px solid var(--pink-200);
      border-radius: var(--radius-sm);
      padding: 8px 10px;
      text-align: center;
    }

    .stat-pill span {
      display: block;
      font-size: 0.72rem;
      color: var(--text-muted);
      font-weight: 700;
    }

    .stat-pill strong {
      font-size: 0.98rem;
      color: var(--pink-600);
    }

    /* Macro Bars */
    .macro-item {
      margin-bottom: 10px;
    }

    .macro-item:last-child {
      margin-bottom: 0;
    }

    .macro-header {
      display: flex;
      justify-content: space-between;
      font-size: 0.83rem;
      font-weight: 700;
      margin-bottom: 4px;
    }

    .progress-track {
      height: 10px;
      background: var(--pink-100);
      border-radius: 999px;
      overflow: hidden;
    }

    .progress-fill {
      height: 100%;
      border-radius: 999px;
      transition: width 0.4s ease;
    }

    /* Water & Steps */
    .wellness-box {
      background: var(--pink-50);
      border: 1px solid var(--pink-200);
      border-radius: var(--radius-md);
      padding: 14px;
      margin-bottom: 12px;
    }

    .wellness-box:last-child {
      margin-bottom: 0;
    }

    .wellness-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 8px;
      font-weight: 700;
      font-size: 0.93rem;
    }

    .water-cups {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin: 10px 0;
    }

    .cup-btn {
      font-size: 1.25rem;
      background: white;
      border: 1.5px solid var(--pink-200);
      border-radius: 10px;
      width: 36px;
      height: 36px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: 0.15s;
      opacity: 0.45;
    }

    .cup-btn.filled {
      opacity: 1;
      border-color: #74c0fc;
      background: #e7f5ff;
      transform: scale(1.04);
    }

    .quick-actions {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      margin-top: 8px;
    }

    /* Buttons */
    .btn {
      border: none;
      border-radius: 999px;
      padding: 9px 16px;
      font-weight: 700;
      font-size: 0.86rem;
      cursor: pointer;
      transition: all 0.2s;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--pink-400), var(--pink-500));
      color: white;
      box-shadow: 0 5px 14px rgba(230, 73, 128, 0.25);
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 7px 18px rgba(230, 73, 128, 0.35);
    }

    .btn-soft {
      background: var(--pink-100);
      color: var(--pink-600);
    }

    .btn-soft:hover {
      background: var(--pink-200);
    }

    .btn-outline {
      background: white;
      border: 1.5px solid var(--pink-200);
      color: var(--pink-600);
    }

    .btn-outline:hover {
      background: var(--pink-50);
    }

    .btn-sm {
      padding: 6px 12px;
      font-size: 0.8rem;
    }

    .btn-icon {
      background: var(--pink-50);
      border: 1px solid var(--pink-200);
      color: var(--pink-600);
      border-radius: 8px;
      padding: 4px 8px;
      cursor: pointer;
      font-size: 0.82rem;
      font-weight: 700;
    }

    .btn-icon:hover {
      background: var(--pink-200);
    }

    /* Meals */
    .meal-card {
      background: var(--card-bg);
      border: 1.5px solid var(--border-soft);
      border-radius: var(--radius-lg);
      padding: 16px 18px;
      margin-bottom: 14px;
      box-shadow: 0 6px 18px rgba(230, 73, 128, 0.06);
    }

    .meal-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
      margin-bottom: 10px;
    }

    .meal-title {
      display: flex;
      align-items: center;
      gap: 10px;
      font-weight: 700;
      font-size: 1.05rem;
      color: var(--text-main);
    }

    .meal-emoji {
      width: 38px;
      height: 38px;
      background: var(--pink-100);
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.25rem;
    }

    .meal-totals {
      font-size: 0.8rem;
      color: var(--text-muted);
      font-weight: 700;
    }

    .meal-items {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .food-log-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      background: var(--pink-50);
      border: 1px solid var(--pink-100);
      border-radius: var(--radius-sm);
      padding: 9px 12px;
      flex-wrap: wrap;
    }

    .food-log-info strong {
      display: block;
      font-size: 0.92rem;
      color: var(--text-main);
    }

    .food-log-info small {
      color: var(--text-muted);
      font-weight: 600;
      font-size: 0.78rem;
    }

    .food-log-right {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .kcal-badge {
      background: white;
      border: 1px solid var(--pink-200);
      color: var(--pink-600);
      font-weight: 700;
      font-size: 0.82rem;
      padding: 4px 10px;
      border-radius: 999px;
    }

    .empty-meal {
      font-size: 0.84rem;
      color: var(--text-muted);
      font-style: italic;
      padding: 4px 0;
    }

    /* Forms & Inputs */
    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 12px;
      margin-bottom: 14px;
    }

    .field label {
      display: block;
      font-size: 0.82rem;
      font-weight: 700;
      color: var(--text-muted);
      margin-bottom: 5px;
    }

    .field input, .field select {
      width: 100%;
      padding: 10px 12px;
      border-radius: var(--radius-sm);
      border: 1.5px solid var(--pink-200);
      background: white;
      color: var(--text-main);
      font-size: 0.92rem;
      font-weight: 600;
      outline: none;
      transition: border-color 0.2s;
    }

    .field input:focus, .field select:focus {
      border-color: var(--pink-400);
    }

    .badge-info {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: var(--pink-100);
      color: var(--pink-600);
      padding: 6px 12px;
      border-radius: 999px;
      font-size: 0.82rem;
      font-weight: 700;
    }

    .gentle-note {
      background: #fff9db;
      border: 1px solid #ffe066;
      color: #8c6d1f;
      padding: 10px 12px;
      border-radius: var(--radius-sm);
      font-size: 0.83rem;
      font-weight: 600;
      margin-top: 10px;
    }

    /* Food Database List */
    .chips-row {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      margin: 10px 0 14px;
    }

    .chip {
      background: white;
      border: 1.5px solid var(--pink-200);
      color: var(--text-muted);
      padding: 5px 12px;
      border-radius: 999px;
      font-size: 0.8rem;
      font-weight: 700;
      cursor: pointer;
      transition: 0.15s;
    }

    .chip.active {
      background: var(--pink-400);
      border-color: var(--pink-400);
      color: white;
    }

    .food-db-list {
      display: flex;
      flex-direction: column;
      gap: 8px;
      max-height: 430px;
      overflow-y: auto;
      padding-right: 4px;
    }

    .food-db-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      background: var(--pink-50);
      border: 1.5px solid var(--pink-100);
      border-radius: var(--radius-md);
      padding: 10px 14px;
      cursor: pointer;
      transition: 0.15s;
    }

    .food-db-item:hover {
      border-color: var(--pink-300);
      background: #ffeef4;
    }

    .food-db-item.selected {
      border-color: var(--pink-500);
      background: #ffe3ee;
    }

    /* Modal */
    .modal-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(74, 44, 56, 0.45);
      backdrop-filter: blur(4px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 16px;
      z-index: 1000;
    }

    .modal-backdrop.open {
      display: flex;
      animation: fadeIn 0.2s ease;
    }

    .modal {
      background: white;
      border: 2px solid var(--pink-200);
      border-radius: var(--radius-lg);
      width: 100%;
      max-width: 580px;
      max-height: 90vh;
      overflow-y: auto;
      padding: 22px;
      box-shadow: 0 20px 50px rgba(194, 37, 92, 0.22);
    }

    .modal-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 14px;
    }

    .modal-head h3 {
      color: var(--pink-600);
      font-size: 1.18rem;
    }

    .close-btn {
      background: var(--pink-100);
      color: var(--pink-600);
      border: none;
      width: 34px;
      height: 34px;
      border-radius: 50%;
      font-size: 1.1rem;
      font-weight: 700;
      cursor: pointer;
    }

    .portion-box {
      background: var(--pink-50);
      border: 1.5px solid var(--pink-200);
      border-radius: var(--radius-md);
      padding: 14px;
      margin-top: 14px;
    }

    .preview-macros {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 8px;
      margin-top: 12px;
    }

    .preview-box {
      background: white;
      border: 1px solid var(--pink-200);
      border-radius: var(--radius-sm);
      padding: 8px;
      text-align: center;
    }

    .preview-box small {
      display: block;
      font-size: 0.7rem;
      color: var(--text-muted);
      font-weight: 700;
    }

    .preview-box strong {
      font-size: 0.95rem;
      color: var(--pink-600);
    }

    /* Calendar Grid */
    .cal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
    }

    .cal-grid {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 6px;
      text-align: center;
    }

    .cal-weekday {
      font-size: 0.78rem;
      font-weight: 700;
      color: var(--text-muted);
      padding-bottom: 4px;
    }

    .cal-day {
      background: var(--pink-50);
      border: 1px solid var(--pink-100);
      border-radius: 12px;
      padding: 8px 4px;
      cursor: pointer;
      font-weight: 700;
      font-size: 0.85rem;
      min-height: 52px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
    }

    .cal-day:hover {
      border-color: var(--pink-400);
    }

    .cal-day.today {
      border: 2px solid var(--pink-400);
    }

    .cal-day.selected {
      background: var(--pink-400);
      color: white;
    }

    .cal-day.empty {
      background: transparent;
      border: none;
      cursor: default;
    }

    .toast {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%) translateY(80px);
      background: var(--pink-600);
      color: white;
      padding: 10px 20px;
      border-radius: 999px;
      font-weight: 700;
      font-size: 0.88rem;
      box-shadow: 0 10px 25px rgba(194, 37, 92, 0.35);
      transition: transform 0.3s ease;
      z-index: 2000;
    }

    .toast.show {
      transform: translateX(-50%) translateY(0);
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- Header -->
    <header class="header">
      <div class="brand">
        <div class="brand-icon">🍓</div>
        <div>
          <h1>Doce Meta</h1>
          <p>Seu diário delicado de calorias, macros & bem-estar 💕</p>
        </div>
      </div>

      <div class="date-bar">
        <button class="date-btn" onclick="changeDay(-1)" title="Dia anterior">‹</button>
        <button class="date-label-btn" onclick="openCalendarModal()" title="Abrir calendário">
          <span>📅</span>
          <span id="currentDateLabel">Hoje</span>
        </button>
        <button class="date-btn" onclick="changeDay(1)" title="Próximo dia">›</button>
      </div>
    </header>

    <!-- Navigation -->
    <nav class="nav-tabs">
      <button class="nav-tab active" data-view="diary" onclick="switchView('diary')">🌸 Diário</button>
      <button class="nav-tab" data-view="foods" onclick="switchView('foods')">🍓 Alimentos (TACO)</button>
      <button class="nav-tab" data-view="profile" onclick="switchView('profile')">💗 Perfil & Metas</button>
    </nav>

    <!-- VIEW 1: DIÁRIO -->
    <section id="view-diary" class="view active">
      <div class="grid-2">
        <!-- Resumo Calórico e Macros -->
        <div class="card">
          <div class="card-title">
            <span>💗 Resumo do Dia</span>
            <span class="badge-info" id="imcBadgeHeader">IMC: --</span>
          </div>

          <div class="calorie-hero">
            <div class="ring-wrapper">
              <svg class="ring-svg" viewBox="0 0 142 142">
                <defs>
                  <linearGradient id="pinkGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                    <stop offset="0%" stop-color="#ff85b3" />
                    <stop offset="100%" stop-color="#e64980" />
                  </linearGradient>
                </defs>
                <circle class="ring-bg" cx="71" cy="71" r="58"></circle>
                <circle id="calorieRing" class="ring-progress" cx="71" cy="71" r="58" stroke-dasharray="364.42" stroke-dashoffset="364.42"></circle>
              </svg>
              <div class="ring-center">
                <span class="kcal-val" id="ringRemaining">0</span>
                <span class="kcal-sub" id="ringSubLabel">restantes</span>
              </div>
            </div>

            <div class="calorie-stats">
              <div class="stat-pills">
                <div class="stat-pill">
                  <span>Meta</span>
                  <strong id="statGoal">0</strong>
                </div>
                <div class="stat-pill">
                  <span>Consumidas</span>
                  <strong id="statConsumed">0</strong>
                </div>
                <div class="stat-pill">
                  <span>Progresso</span>
                  <strong id="statPercent">0%</strong>
                </div>
              </div>

              <!-- Macro Bars -->
              <div class="macro-item">
                <div class="macro-header">
                  <span>🍑 Carboidratos</span>
                  <span id="carbText">0g / 0g</span>
                </div>
                <div class="progress-track">
                  <div id="carbBar" class="progress-fill" style="width: 0%; background: var(--carb-color);"></div>
                </div>
              </div>

              <div class="macro-item">
                <div class="macro-header">
                  <span>🍓 Proteínas</span>
                  <span id="protText">0g / 0g</span>
                </div>
                <div class="progress-track">
                  <div id="protBar" class="progress-fill" style="width: 0%; background: var(--prot-color);"></div>
                </div>
              </div>

              <div class="macro-item">
                <div class="macro-header">
                  <span>🥑 Gorduras</span>
                  <span id="fatText">0g / 0g</span>
                </div>
                <div class="progress-track">
                  <div id="fatBar" class="progress-fill" style="width: 0%; background: var(--fat-color);"></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Água & Passos -->
        <div class="card">
          <div class="card-title">
            <span>🌷 Hidratação & Passos</span>
            <button class="btn btn-soft btn-sm" onclick="copyYesterday()">✨ Repetir ontem</button>
          </div>

          <!-- Água -->
          <div class="wellness-box">
            <div class="wellness-top">
              <span>💧 Água diária</span>
              <span id="waterLabel" style="color: #1c7ed6;">0 / 2000 ml</span>
            </div>
            <div class="progress-track" style="background: #d0ebff;">
              <div id="waterBar" class="progress-fill" style="width: 0%; background: var(--water-color);"></div>
            </div>
            <div class="water-cups" id="waterCups"></div>
            <div class="quick-actions">
              <button class="btn btn-outline btn-sm" onclick="addWater(-250)">-250ml</button>
              <button class="btn btn-primary btn-sm" onclick="addWater(250)">+ 1 copo (250ml)</button>
              <button class="btn btn-soft btn-sm" onclick="addWater(500)">+ 500ml</button>
            </div>
          </div>

          <!-- Passos -->
          <div class="wellness-box">
            <div class="wellness-top">
              <span>👟 Passos diários</span>
              <span id="stepsLabel" style="color: var(--pink-600);">0 / 8.000</span>
            </div>
            <div class="progress-track">
              <div id="stepsBar" class="progress-fill" style="width: 0%; background: linear-gradient(90deg, #ff9ec2, #e64980);"></div>
            </div>
            <div style="display:flex; gap:8px; margin-top:10px; align-items:center;">
              <input type="number" id="stepsInput" min="0" placeholder="Ex: 5400" style="flex:1; padding:7px 10px; border-radius:10px; border:1.5px solid var(--pink-200); font-weight:700; color:var(--text-main);" onchange="setSteps(this.value)">
              <button class="btn btn-primary btn-sm" onclick="addSteps(1000)">+1.000</button>
              <button class="btn btn-soft btn-sm" onclick="addSteps(500)">+500</button>
            </div>
          </div>
        </div>
      </div>

      <!-- Refeições -->
      <div id="mealsContainer"></div>
    </section>

    <!-- VIEW 2: ALIMENTOS (TACO + PERSONALIZADOS) -->
    <section id="view-foods" class="view">
      <div class="card">
        <div class="card-title">
          <span>🍓 Base de Alimentos (Tabela TACO + Seus Alimentos)</span>
          <button class="btn btn-primary btn-sm" onclick="openCustomFoodModal()">✨ Novo Alimento Personalizado</button>
        </div>

        <div class="field" style="margin-bottom: 8px;">
          <input type="text" id="dbSearchInput" placeholder="🔍 Buscar alimento (ex: arroz, morango, frango, iogurte...)" oninput="renderFoodDatabaseTab()">
        </div>

        <div class="chips-row" id="dbCategoryChips"></div>
        <div class="food-db-list" id="dbFoodList"></div>
      </div>
    </section>

    <!-- VIEW 3: PERFIL & METAS -->
    <section id="view-profile" class="view">
      <div class="card">
        <div class="card-title">
          <span>💗 Perfil, IMC & Cálculo de Calorias</span>
          <span class="badge-info" id="profileImcSummary">IMC: --</span>
        </div>

        <div class="form-grid">
          <div class="field">
            <label>Sexo</label>
            <select id="profSex" onchange="recalcSuggestion()">
              <option value="F">Feminino 🌸</option>
              <option value="M">Masculino</option>
            </select>
          </div>
          <div class="field">
            <label>Idade (anos)</label>
            <input type="number" id="profAge" min="10" max="110" oninput="recalcSuggestion()">
          </div>
          <div class="field">
            <label>Peso atual (kg)</label>
            <input type="number" id="profWeight" step="0.1" min="25" max="300" oninput="recalcSuggestion()">
          </div>
          <div class="field">
            <label>Altura (cm)</label>
            <input type="number" id="profHeight" min="100" max="230" oninput="recalcSuggestion()">
          </div>
          <div class="field">
            <label>Nível de atividade</label>
            <select id="profActivity" onchange="recalcSuggestion()">
              <option value="1.2">Sedentária (pouco movimento)</option>
              <option value="1.375">Leve (1-3x por semana)</option>
              <option value="1.55">Moderada (3-5x por semana)</option>
              <option value="1.725">Intensa (6-7x por semana)</option>
            </select>
          </div>
          <div class="field">
            <label>Objetivo sugerido</label>
            <select id="profGoalType" onchange="recalcSuggestion()">
              <option value="maintain">Manter peso</option>
              <option value="lose_mild">Emagrecimento leve (-300 kcal)</option>
              <option value="lose_mod">Emagrecimento moderado (-500 kcal)</option>
              <option value="gain">Ganho de massa (+300 kcal)</option>
            </select>
          </div>
        </div>

        <div style="background: var(--pink-50); border: 1.5px solid var(--pink-200); border-radius: var(--radius-md); padding: 14px; margin-bottom: 16px;">
          <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px;">
            <div>
              <strong style="color: var(--pink-600);">Sugestão saudável calculada (IMC + Idade + Atividade):</strong>
              <div style="font-size: 0.9rem; margin-top: 3px;">
                TMB estimada: <strong id="calcTmb">--</strong> kcal • Gasto total: <strong id="calcTdee">--</strong> kcal • Sugestão: <strong id="calcSuggested" style="color: var(--pink-600); font-size: 1.05rem;">--</strong> kcal
              </div>
            </div>
            <button class="btn btn-soft btn-sm" onclick="applySuggestedCalories()">Aplicar sugestão 💕</button>
          </div>
        </div>

        <div class="form-grid">
          <div class="field">
            <label>Sua Meta Calórica Diária (kcal) — livre para editar</label>
            <input type="number" id="profCalorieGoal" min="1" oninput="updateMacroGramPreview()">
          </div>
          <div class="field">
            <label>Meta de Água (ml)</label>
            <input type="number" id="profWaterGoal" step="250" min="250">
          </div>
          <div class="field">
            <label>Meta de Passos Diários</label>
            <input type="number" id="profStepsGoal" step="500" min="500">
          </div>
        </div>
        <div id="lowCalorieHint" class="gentle-note" style="display:none;">
          🌸 Lembrete carinhoso: sua meta está bem baixinha em relação ao seu gasto basal. Você pode usá-la livremente aqui, mas lembre-se de cuidar do seu bem-estar!
        </div>
      </div>

      <!-- Personalização de Macros -->
      <div class="card">
        <div class="card-title">
          <span>🥗 Metas de Macronutrientes (% das calorias)</span>
          <div style="display:flex; gap:6px; flex-wrap:wrap;">
            <button class="btn btn-outline btn-sm" onclick="setMacroPreset(45,25,30)">Equilibrada (45/25/30)</button>
            <button class="btn btn-outline btn-sm" onclick="setMacroPreset(35,35,30)">+ Proteína (35/35/30)</button>
            <button class="btn btn-outline btn-sm" onclick="setMacroPreset(25,30,45)">Low Carb (25/30/45)</button>
          </div>
        </div>

        <div class="form-grid">
          <div class="field">
            <label>🍑 Carboidratos (%) — <span id="prevCarbG">0g</span></label>
            <input type="number" id="macroCarbPct" min="0" max="100" oninput="updateMacroGramPreview()">
          </div>
          <div class="field">
            <label>🍓 Proteínas (%) — <span id="prevProtG">0g</span></label>
            <input type="number" id="macroProtPct" min="0" max="100" oninput="updateMacroGramPreview()">
          </div>
          <div class="field">
            <label>🥑 Gorduras (%) — <span id="prevFatG">0g</span></label>
            <input type="number" id="macroFatPct" min="0" max="100" oninput="updateMacroGramPreview()">
          </div>
        </div>

        <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px;">
          <span id="macroSumStatus" style="font-size:0.86rem; font-weight:700;">Soma: 100%</span>
          <button class="btn btn-primary" onclick="saveProfileSettings()">Salvar Perfil & Metas 💗</button>
        </div>
      </div>

      <!-- Backup -->
      <div class="card">
        <div class="card-title">
          <span>💾 Backup dos Seus Dados</span>
        </div>
        <p style="font-size:0.86rem; color:var(--text-muted); font-weight:600; margin-bottom:12px;">
          Tudo fica salvo gratuitamente no seu navegador. Faça um backup de vez em quando para nunca perder seu histórico ou levar seus dados para outro aparelho!
        </p>
        <div style="display:flex; gap:10px; flex-wrap:wrap;">
          <button class="btn btn-soft" onclick="exportBackup()">⬇️ Exportar Backup (.json)</button>
          <label class="btn btn-outline" style="cursor:pointer;">
            ⬆️ Importar Backup (.json)
            <input type="file" accept=".json" style="display:none;" onchange="importBackup(event)">
          </label>
        </div>
      </div>
    </section>
  </div>

  <!-- MODAL: ADICIONAR ALIMENTO NA REFEIÇÃO -->
  <div id="addFoodModal" class="modal-backdrop">
    <div class="modal">
      <div class="modal-head">
        <h3 id="addModalTitle">🍓 Adicionar alimento</h3>
        <button class="close-btn" onclick="closeModal('addFoodModal')">×</button>
      </div>

      <div style="display:flex; gap:8px; margin-bottom:8px;">
        <input type="text" id="modalSearchInput" placeholder="🔍 Buscar na TACO ou personalizados..." oninput="renderModalFoodList()" style="flex:1; padding:10px 12px; border-radius:10px; border:1.5px solid var(--pink-200); font-weight:600;">
        <button class="btn btn-soft btn-sm" onclick="closeModal('addFoodModal'); openCustomFoodModal();">+ Criar</button>
      </div>

      <div class="chips-row" id="modalCategoryChips"></div>
      <div class="food-db-list" id="modalFoodList" style="max-height: 220px;"></div>

      <!-- Caixa de Porção e Quantidade -->
      <div id="portionSelectorBox" class="portion-box" style="display:none;">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
          <strong id="selectedFoodName" style="color:var(--pink-600);">Alimento</strong>
          <span id="selectedFoodBase" style="font-size:0.78rem; color:var(--text-muted); font-weight:700;"></span>
        </div>

        <div class="form-grid" style="margin-bottom:8px;">
          <div class="field">
            <label>Tipo de medida</label>
            <select id="portionSelect" onchange="onPortionSelectChange()"></select>
          </div>
          <div class="field">
            <label id="qtyInputLabel">Quantidade</label>
            <input type="number" id="qtyInput" step="0.1" min="0.1" value="1" oninput="updateSelectedFoodPreview()">
          </div>
        </div>

        <div class="quick-actions" id="quickQtyButtons" style="margin-bottom:10px;"></div>

        <div class="preview-macros">
          <div class="preview-box"><small>Calorias</small><strong id="prevKcal">0</strong></div>
          <div class="preview-box"><small>Carbos</small><strong id="prevCarb">0g</strong></div>
          <div class="preview-box"><small>Proteína</small><strong id="prevProt">0g</strong></div>
          <div class="preview-box"><small>Gordura</small><strong id="prevFat">0g</strong></div>
        </div>

        <div style="margin-top:14px; text-align:right;">
          <button class="btn btn-primary" onclick="confirmAddFoodToMeal()">Adicionar na refeição 💗</button>
        </div>
      </div>
    </div>
  </div>

  <!-- MODAL: CRIAR / EDITAR ALIMENTO PERSONALIZADO -->
  <div id="customFoodModal" class="modal-backdrop">
    <div class="modal">
      <div class="modal-head">
        <h3 id="customModalTitle">✨ Novo Alimento Personalizado</h3>
        <button class="close-btn" onclick="closeModal('customFoodModal')">×</button>
      </div>

      <input type="hidden" id="customFoodEditId">

      <div class="form-grid">
        <div class="field">
          <label>Nome do alimento</label>
          <input type="text" id="cfName" placeholder="Ex: Iogurte Grego Morango">
        </div>
        <div class="field">
          <label>Ícone</label>
          <select id="cfEmoji">
            <option value="🍓">🍓 Morango</option>
            <option value="🍑">🍑 Pêssego</option>
            <option value="🍒">🍒 Cereja</option>
            <option value="🍌">🍌 Banana</option>
            <option value="🥑">🥑 Abacate</option>
            <option value="🥗">🥗 Salada</option>
            <option value="🍚">🍚 Refeição</option>
            <option value="🍗">🍗 Proteína</option>
            <option value="🥛">🥛 Lácteo</option>
            <option value="🧁">🧁 Doce / Lanche</option>
            <option value="🍫">🍫 Chocolate</option>
            <option value="🥤">🥤 Bebida</option>
            <option value="☕">☕ Café / Chá</option>
            <option value="💗">💗 Outro</option>
          </select>
        </div>
        <div class="field">
          <label>Unidade base</label>
          <select id="cfUnit">
            <option value="g">Gramas (g)</option>
            <option value="ml">Mililitros (ml)</option>
          </select>
        </div>
        <div class="field">
          <label>Informar valores com base em:</label>
          <select id="cfInputMode" onchange="toggleCustomFoodMode()">
            <option value="100">Por 100g / 100ml (padrão tabela)</option>
            <option value="portion">Por porção / pacote / garrafa</option>
          </select>
        </div>
      </div>

      <div id="cfPortionFields" class="form-grid" style="display:none; background:var(--pink-50); padding:10px; border-radius:12px; border:1px solid var(--pink-200);">
        <div class="field">
          <label>Nome da porção (rótulo)</label>
          <input type="text" id="cfPortionName" placeholder="Ex: 1 pacote, 1 garrafa, 1 colher">
        </div>
        <div class="field">
          <label>Peso/Volume dessa porção (g ou ml)</label>
          <input type="number" id="cfPortionGrams" min="1" step="0.1" placeholder="Ex: 45">
        </div>
      </div>

      <div class="form-grid">
        <div class="field">
          <label>Calorias (kcal)</label>
          <input type="number" id="cfKcal" min="0" step="0.1" placeholder="0">
        </div>
        <div class="field">
          <label>Carboidratos (g)</label>
          <input type="number" id="cfCarb" min="0" step="0.1" placeholder="0">
        </div>
        <div class="field">
          <label>Proteínas (g)</label>
          <input type="number" id="cfProt" min="0" step="0.1" placeholder="0">
        </div>
        <div class="field">
          <label>Gorduras (g)</label>
          <input type="number" id="cfFat" min="0" step="0.1" placeholder="0">
        </div>
      </div>

      <div id="cfExtraPortionBox" class="form-grid" style="margin-top:4px;">
        <div class="field">
          <label>Porção tradicional opcional (ex: 1 colher)</label>
          <input type="text" id="cfOptPortionLabel" placeholder="Ex: 1 unidade">
        </div>
        <div class="field">
          <label>Peso da porção opcional (g ou ml)</label>
          <input type="number" id="cfOptPortionGrams" min="1" step="0.1" placeholder="Ex: 30">
        </div>
      </div>

      <div style="display:flex; justify-content:flex-end; gap:8px; margin-top:14px;">
        <button class="btn btn-soft" onclick="closeModal('customFoodModal')">Cancelar</button>
        <button class="btn btn-primary" onclick="saveCustomFood()">Salvar Alimento 💕</button>
      </div>
    </div>
  </div>

  <!-- MODAL: CALENDÁRIO -->
  <div id="calendarModal" class="modal-backdrop">
    <div class="modal" style="max-width:440px;">
      <div class="modal-head">
        <h3>📅 Seu Histórico</h3>
        <button class="close-btn" onclick="closeModal('calendarModal')">×</button>
      </div>
      <div class="cal-header">
        <button class="btn btn-soft btn-sm" onclick="shiftCalendarMonth(-1)">‹ Mês anterior</button>
        <strong id="calMonthLabel" style="color:var(--pink-600);"></strong>
        <button class="btn btn-soft btn-sm" onclick="shiftCalendarMonth(1)">Próximo ›</button>
      </div>
      <div class="cal-grid" id="calGrid"></div>
      <p style="font-size:0.78rem; color:var(--text-muted); font-weight:600; margin-top:12px; text-align:center;">
        💗 Meta cumprida (até +10%) • 🌸 Dia com registros
      </p>
    </div>
  </div>

  <div id="toast" class="toast"></div>

  <script>
    // =========================================================
    // 1. BASE DE DADOS TACO / TBCA (valores por 100g ou 100ml)
    // =========================================================
    const TACO_FOODS = [
      // Cereais, Pães e Tubérculos
      { id: 't1', name: 'Arroz branco tipo 1 cozido', cat: 'Cereais & Pães', emoji: '🍚', unit: 'g', kcal: 128, carb: 28.1, prot: 2.5, fat: 0.2, portions: [{ label: '1 colher de sopa', g: 25 }, { label: '1 escumadeira', g: 85 }] },
      { id: 't2', name: 'Arroz integral cozido', cat: 'Cereais & Pães', emoji: '🍚', unit: 'g', kcal: 124, carb: 25.8, prot: 2.6, fat: 1.0, portions: [{ label: '1 colher de sopa', g: 25 }, { label: '1 escumadeira', g: 85 }] },
      { id: 't3', name: 'Feijão carioca cozido', cat: 'Cereais & Pães', emoji: '🫘', unit: 'g', kcal: 76, carb: 13.6, prot: 4.8, fat: 0.5, portions: [{ label: '1 concha média', g: 86 }, { label: '1 colher de sopa', g: 20 }] },
      { id: 't4', name: 'Lentilha cozida', cat: 'Cereais & Pães', emoji: '🍲', unit: 'g', kcal: 93, carb: 16.3, prot: 6.3, fat: 0.5, portions: [{ label: '1 colher de sopa', g: 25 }, { label: '1 concha', g: 80 }] },
      { id: 't5', name: 'Aveia em flocos crua', cat: 'Cereais & Pães', emoji: '🌾', unit: 'g', kcal: 394, carb: 66.6, prot: 13.9, fat: 8.5, portions: [{ label: '1 colher de sopa', g: 15 }, { label: '1 xícara', g: 80 }] },
      { id: 't6', name: 'Pão francês', cat: 'Cereais & Pães', emoji: '🥖', unit: 'g', kcal: 300, carb: 58.6, prot: 8.0, fat: 3.1, portions: [{ label: '1 unidade média', g: 50 }] },
      { id: 't7', name: 'Pão de forma integral', cat: 'Cereais & Pães', emoji: '🍞', unit: 'g', kcal: 270, carb: 49.9, prot: 9.4, fat: 3.7, portions: [{ label: '1 fatia', g: 25 }, { label: '2 fatias', g: 50 }] },
      { id: 't8', name: 'Goma de tapioca hidratada', cat: 'Cereais & Pães', emoji: '🫓', unit: 'g', kcal: 289, carb: 71.9, prot: 0.4, fat: 0.0, portions: [{ label: '1 colher de sopa', g: 15 }, { label: '1 tapioca (4 colheres)', g: 60 }] },
      { id: 't9', name: 'Macarrão de trigo cozido', cat: 'Cereais & Pães', emoji: '🍝', unit: 'g', kcal: 102, carb: 21.0, prot: 3.0, fat: 0.4, portions: [{ label: '1 pegador', g: 100 }, { label: '1 escumadeira', g: 80 }] },
      { id: 't10', name: 'Batata doce cozida', cat: 'Cereais & Pães', emoji: '🍠', unit: 'g', kcal: 77, carb: 18.4, prot: 0.6, fat: 0.1, portions: [{ label: '1 fatia média', g: 70 }, { label: '1 unidade pequena', g: 120 }] },
      { id: 't11', name: 'Batata inglesa cozida', cat: 'Cereais & Pães', emoji: '🥔', unit: 'g', kcal: 52, carb: 11.9, prot: 1.2, fat: 0.0, portions: [{ label: '1 unidade média', g: 100 }, { label: '1 colher de sopa', g: 30 }] },
      { id: 't12', name: 'Batata frita', cat: 'Cereais & Pães', emoji: '🍟', unit: 'g', kcal: 267, carb: 35.6, prot: 5.0, fat: 13.1, portions: [{ label: '1 porção pequena', g: 80 }, { label: '1 pacote médio', g: 115 }] },

      // Carnes, Peixes e Ovos
      { id: 't13', name: 'Peito de frango sem pele grelhado', cat: 'Carnes & Ovos', emoji: '🍗', unit: 'g', kcal: 159, carb: 0.0, prot: 32.0, fat: 2.5, portions: [{ label: '1 filé médio', g: 100 }, { label: '1 filé grande', g: 150 }] },
      { id: 't14', name: 'Sobrecoxa de frango sem pele assada', cat: 'Carnes & Ovos', emoji: '🍗', unit: 'g', kcal: 233, carb: 0.0, prot: 29.2, fat: 12.0, portions: [{ label: '1 unidade média', g: 75 }] },
      { id: 't15', name: 'Patinho bovino sem gordura grelhado', cat: 'Carnes & Ovos', emoji: '🥩', unit: 'g', kcal: 219, carb: 0.0, prot: 35.9, fat: 7.3, portions: [{ label: '1 bife médio', g: 100 }, { label: '1 colher de sopa (moído)', g: 25 }] },
      { id: 't16', name: 'Salmão sem pele grelhado', cat: 'Carnes & Ovos', emoji: '🐟', unit: 'g', kcal: 243, carb: 0.0, prot: 26.1, fat: 14.5, portions: [{ label: '1 posta média', g: 120 }] },
      { id: 't17', name: 'Atum em conserva de óleo (drenado)', cat: 'Carnes & Ovos', emoji: '🐟', unit: 'g', kcal: 166, carb: 0.0, prot: 26.2, fat: 6.0, portions: [{ label: '1 colher de sopa', g: 20 }, { label: '1 lata drenada', g: 120 }] },
      { id: 't18', name: 'Ovo de galinha inteiro cozido', cat: 'Carnes & Ovos', emoji: '🥚', unit: 'g', kcal: 146, carb: 0.6, prot: 13.3, fat: 9.5, portions: [{ label: '1 unidade média', g: 50 }] },
      { id: 't19', name: 'Ovo de galinha inteiro frito', cat: 'Carnes & Ovos', emoji: '🍳', unit: 'g', kcal: 240, carb: 1.2, prot: 15.6, fat: 18.6, portions: [{ label: '1 unidade média', g: 50 }] },
      { id: 't20', name: 'Clara de ovo cozida', cat: 'Carnes & Ovos', emoji: '🥚', unit: 'g', kcal: 59, carb: 0.0, prot: 13.4, fat: 0.1, portions: [{ label: '1 clara média', g: 33 }] },

      // Leite e Derivados
      { id: 't21', name: 'Leite de vaca integral', cat: 'Lácteos', emoji: '🥛', unit: 'ml', kcal: 64, carb: 5.9, prot: 2.9, fat: 3.2, portions: [{ label: '1 copo americano', g: 200 }, { label: '1 xícara', g: 240 }] },
      { id: 't22', name: 'Leite em pó integral', cat: 'Lácteos', emoji: '🥛', unit: 'g', kcal: 497, carb: 39.2, prot: 25.4, fat: 26.9, portions: [{ label: '1 colher de sopa', g: 13 }] },
      { id: 't23', name: 'Iogurte natural integral', cat: 'Lácteos', emoji: '🥣', unit: 'g', kcal: 52, carb: 1.9, prot: 4.1, fat: 3.0, portions: [{ label: '1 pote padrão', g: 170 }] },
      { id: 't24', name: 'Iogurte natural desnatado', cat: 'Lácteos', emoji: '🥣', unit: 'g', kcal: 41, carb: 5.8, prot: 3.8, fat: 0.3, portions: [{ label: '1 pote padrão', g: 170 }] },
      { id: 't25', name: 'Iogurte sabor morango', cat: 'Lácteos', emoji: '🍓', unit: 'g', kcal: 70, carb: 9.7, prot: 2.7, fat: 2.3, portions: [{ label: '1 pote', g: 90 }, { label: '1 garrafinha', g: 170 }] },
      { id: 't26', name: 'Queijo minas frescal', cat: 'Lácteos', emoji: '🧀', unit: 'g', kcal: 264, carb: 3.2, prot: 17.4, fat: 20.2, portions: [{ label: '1 fatia média', g: 30 }] },
      { id: 't27', name: 'Queijo muçarela', cat: 'Lácteos', emoji: '🧀', unit: 'g', kcal: 330, carb: 3.0, prot: 22.6, fat: 25.2, portions: [{ label: '1 fatia fina', g: 20 }] },
      { id: 't28', name: 'Requeijão cremoso', cat: 'Lácteos', emoji: '🧈', unit: 'g', kcal: 257, carb: 2.4, prot: 9.6, fat: 23.4, portions: [{ label: '1 colher de sopa', g: 25 }, { label: '1 colher de chá', g: 10 }] },
      { id: 't29', name: 'Queijo ricota', cat: 'Lácteos', emoji: '🧀', unit: 'g', kcal: 140, carb: 3.8, prot: 12.6, fat: 8.1, portions: [{ label: '1 fatia média', g: 30 }, { label: '1 colher de sopa', g: 25 }] },

      // Frutas
      { id: 't30', name: 'Morango cru', cat: 'Frutas', emoji: '🍓', unit: 'g', kcal: 30, carb: 6.8, prot: 0.9, fat: 0.3, portions: [{ label: '1 unidade média', g: 12 }, { label: '1 xícara (10 unid)', g: 120 }, { label: '1 bandeja (250g)', g: 250 }] },
      { id: 't31', name: 'Banana prata crua', cat: 'Frutas', emoji: '🍌', unit: 'g', kcal: 98, carb: 26.0, prot: 1.3, fat: 0.1, portions: [{ label: '1 unidade média', g: 70 }] },
      { id: 't32', name: 'Maçã Fuji com casca', cat: 'Frutas', emoji: '🍎', unit: 'g', kcal: 56, carb: 15.2, prot: 0.3, fat: 0.0, portions: [{ label: '1 unidade média', g: 130 }] },
      { id: 't33', name: 'Mamão Formosa cru', cat: 'Frutas', emoji: '🍈', unit: 'g', kcal: 45, carb: 11.6, prot: 0.8, fat: 0.1, portions: [{ label: '1 fatia média', g: 150 }] },
      { id: 't34', name: 'Laranja pêra crua', cat: 'Frutas', emoji: '🍊', unit: 'g', kcal: 37, carb: 8.9, prot: 1.0, fat: 0.1, portions: [{ label: '1 unidade média', g: 140 }] },
      { id: 't35', name: 'Melancia crua', cat: 'Frutas', emoji: '🍉', unit: 'g', kcal: 33, carb: 8.1, prot: 0.9, fat: 0.0, portions: [{ label: '1 fatia média', g: 200 }] },
      { id: 't36', name: 'Melão cru', cat: 'Frutas', emoji: '🍈', unit: 'g', kcal: 29, carb: 7.5, prot: 0.7, fat: 0.0, portions: [{ label: '1 fatia média', g: 115 }] },
      { id: 't37', name: 'Abacate cru', cat: 'Frutas', emoji: '🥑', unit: 'g', kcal: 96, carb: 6.0, prot: 1.2, fat: 8.4, portions: [{ label: '1 colher de sopa', g: 30 }, { label: '1/2 unidade pequena', g: 100 }] },
      { id: 't38', name: 'Abacaxi cru', cat: 'Frutas', emoji: '🍍', unit: 'g', kcal: 48, carb: 12.3, prot: 0.9, fat: 0.1, portions: [{ label: '1 fatia média', g: 75 }] },
      { id: 't39', name: 'Açaí polpa com guaraná e glucose', cat: 'Frutas', emoji: '🫐', unit: 'g', kcal: 110, carb: 21.5, prot: 0.7, fat: 3.7, portions: [{ label: '1 tigela pequena', g: 200 }, { label: '1 copo (300g)', g: 300 }] },

      // Verduras e Legumes
      { id: 't40', name: 'Alface crespa crua', cat: 'Verduras & Legumes', emoji: '🥬', unit: 'g', kcal: 11, carb: 1.7, prot: 1.4, fat: 0.2, portions: [{ label: '1 folha', g: 10 }, { label: '1 prato de salada', g: 50 }] },
      { id: 't41', name: 'Tomate salada', cat: 'Verduras & Legumes', emoji: '🍅', unit: 'g', kcal: 21, carb: 5.1, prot: 0.8, fat: 0.0, portions: [{ label: '1 fatia', g: 15 }, { label: '1 tomate médio', g: 100 }] },
      { id: 't42', name: 'Cenoura crua', cat: 'Verduras & Legumes', emoji: '🥕', unit: 'g', kcal: 34, carb: 7.7, prot: 1.3, fat: 0.2, portions: [{ label: '1 colher de sopa (ralada)', g: 15 }, { label: '1 unidade média', g: 100 }] },
      { id: 't43', name: 'Brócolis cozido', cat: 'Verduras & Legumes', emoji: '🥦', unit: 'g', kcal: 25, carb: 4.4, prot: 2.1, fat: 0.5, portions: [{ label: '1 buquê médio', g: 30 }, { label: '1 xícara', g: 90 }] },
      { id: 't44', name: 'Couve manteiga refogada', cat: 'Verduras & Legumes', emoji: '🥬', unit: 'g', kcal: 90, carb: 8.7, prot: 1.7, fat: 6.6, portions: [{ label: '1 colher de sopa', g: 20 }] },

      // Óleos, Gorduras e Oleaginosas
      { id: 't45', name: 'Azeite de oliva extra virgem', cat: 'Doces, Óleos & Snacks', emoji: '🫒', unit: 'ml', kcal: 884, carb: 0.0, prot: 0.0, fat: 100.0, portions: [{ label: '1 colher de chá', g: 4 }, { label: '1 colher de sopa', g: 8 }] },
      { id: 't46', name: 'Manteiga com sal', cat: 'Doces, Óleos & Snacks', emoji: '🧈', unit: 'g', kcal: 726, carb: 0.1, prot: 0.4, fat: 82.4, portions: [{ label: '1 ponta de faca', g: 5 }, { label: '1 colher de chá', g: 10 }] },
      { id: 't47', name: 'Amendoim cru', cat: 'Doces, Óleos & Snacks', emoji: '🥜', unit: 'g', kcal: 544, carb: 20.3, prot: 27.2, fat: 43.9, portions: [{ label: '1 colher de sopa', g: 15 }, { label: '1 punhado', g: 30 }] },

      // Doces, Biscoitos & Snacks
      { id: 't48', name: 'Biscoito doce maisena', cat: 'Doces, Óleos & Snacks', emoji: '🍪', unit: 'g', kcal: 443, carb: 75.2, prot: 8.1, fat: 12.0, portions: [{ label: '1 unidade', g: 5 }, { label: '5 unidades', g: 25 }, { label: '1 pacotinho', g: 30 }] },
      { id: 't49', name: 'Biscoito salgado cream cracker', cat: 'Doces, Óleos & Snacks', emoji: '🍘', unit: 'g', kcal: 432, carb: 68.7, prot: 10.1, fat: 14.4, portions: [{ label: '1 unidade', g: 6 }, { label: '5 unidades', g: 30 }] },
      { id: 't50', name: 'Biscoito recheado de chocolate', cat: 'Doces, Óleos & Snacks', emoji: '🍪', unit: 'g', kcal: 472, carb: 70.5, prot: 6.4, fat: 19.6, portions: [{ label: '1 unidade', g: 13 }, { label: '1 pacote (130g)', g: 130 }] },
      { id: 't51', name: 'Chocolate ao leite', cat: 'Doces, Óleos & Snacks', emoji: '🍫', unit: 'g', kcal: 540, carb: 59.6, prot: 7.2, fat: 30.3, portions: [{ label: '1 quadradinho', g: 5 }, { label: '1 fileira (25g)', g: 25 }, { label: '1 barra (90g)', g: 90 }] },
      { id: 't52', name: 'Chocolate meio amargo', cat: 'Doces, Óleos & Snacks', emoji: '🍫', unit: 'g', kcal: 475, carb: 62.4, prot: 4.9, fat: 29.9, portions: [{ label: '1 quadradinho', g: 5 }, { label: '1 fileira (25g)', g: 25 }] },
      { id: 't53', name: 'Açúcar refinado', cat: 'Doces, Óleos & Snacks', emoji: '🍬', unit: 'g', kcal: 387, carb: 99.5, prot: 0.3, fat: 0.0, portions: [{ label: '1 colher de chá', g: 5 }, { label: '1 sachê', g: 5 }, { label: '1 colher de sopa', g: 15 }] },

      // Bebidas
      { id: 't54', name: 'Café coado (sem açúcar)', cat: 'Bebidas', emoji: '☕', unit: 'ml', kcal: 9, carb: 1.5, prot: 0.7, fat: 0.1, portions: [{ label: '1 xícara pequena', g: 50 }, { label: '1 caneca', g: 200 }] },
      { id: 't55', name: 'Água de coco', cat: 'Bebidas', emoji: '🥥', unit: 'ml', kcal: 22, carb: 5.3, prot: 0.0, fat: 0.0, portions: [{ label: '1 copo', g: 200 }, { label: '1 caixinha', g: 200 }, { label: '1 garrafa (330ml)', g: 330 }] },
      { id: 't56', name: 'Suco de laranja pêra natural', cat: 'Bebidas', emoji: '🧃', unit: 'ml', kcal: 33, carb: 7.6, prot: 0.7, fat: 0.1, portions: [{ label: '1 copo', g: 200 }, { label: '1 garrafa (300ml)', g: 300 }] },
      { id: 't57', name: 'Refrigerante tipo cola', cat: 'Bebidas', emoji: '🥤', unit: 'ml', kcal: 34, carb: 8.7, prot: 0.0, fat: 0.0, portions: [{ label: '1 copo', g: 200 }, { label: '1 lata (350ml)', g: 350 }, { label: '1 garrafa (600ml)', g: 600 }] },
      { id: 't58', name: 'Refrigerante tipo guaraná', cat: 'Bebidas', emoji: '🥤', unit: 'ml', kcal: 39, carb: 10.0, prot: 0.0, fat: 0.0, portions: [{ label: '1 copo', g: 200 }, { label: '1 lata (350ml)', g: 350 }] }
    ];

    const MEALS = [
      { id: 'breakfast', name: 'Café da manhã', emoji: '☕' },
      { id: 'lunch', name: 'Almoço', emoji: '🥗' },
      { id: 'afternoon', name: 'Lanche da tarde', emoji: '🧁' },
      { id: 'dinner', name: 'Jantar', emoji: '🍽️' },
      { id: 'snacks', name: 'Snacks', emoji: '🍒' }
    ];

    const STORAGE_KEY = 'doceMeta_v1';

    // =========================================================
    // 2. ESTADO & PERSISTÊNCIA
    // =========================================================
    function getLocalDateKey(dateObj = new Date()) {
      const y = dateObj.getFullYear();
      const m = String(dateObj.getMonth() + 1).padStart(2, '0');
      const d = String(dateObj.getDate()).padStart(2, '0');
      return `${y}-${m}-${d}`;
    }

    function parseLocalDate(key) {
      const [y, m, d] = key.split('-').map(Number);
      return new Date(y, m - 1, d);
    }

    let state = loadState();
    let currentDate = getLocalDateKey();
    let calMonth = new Date().getMonth();
    let calYear = new Date().getFullYear();

    // Variáveis temporárias dos modais
    let activeMealId = null;
    let selectedModalFoodId = null;
    let dbFilterCat = 'Todos';
    let modalFilterCat = 'Todos';

    function defaultState() {
      return {
        profile: {
          sex: 'F',
          age: 25,
          weight: 60,
          height: 163,
          activity: '1.375',
          goalType: 'maintain',
          calorieGoal: 1850,
          macroCarbPct: 45,
          macroProtPct: 25,
          macroFatPct: 30,
          waterGoal: 2000,
          stepsGoal: 8000# bunni-tracker
