<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>VikingBet - Sports, Casino & Admin</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    :root {
      --bg-base: #06180f;
      --bg-surface: #0b2418;
      --bg-card: #0e2d1f;
      --primary: #00e676;
      --primary-grad: linear-gradient(90deg, #10422d 0%, #176646 100%);
      --text: #ffffff;
      --text-muted: #8aa396;
      --border: rgba(255, 255, 255, 0.08);
      --radius: 14px;
      --drawer-top: #192238;
      --drawer-bot: #141c2e;
      --danger: #ff334b;
      --accent-gold: #ffb703;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; -webkit-tap-highlight-color: transparent; }
    body { background: var(--bg-base); color: var(--text); padding-bottom: 74px; overflow-x: hidden; }

    /* HEADER */
    header { position: sticky; top: 0; z-index: 100; background: rgba(6,24,15,0.96); backdrop-filter: blur(10px); display: flex; justify-content: space-between; align-items: center; padding: 10px 14px; border-bottom: 1px solid var(--border); height: 58px; }
    .brand-logo { display: flex; align-items: center; gap: 6px; font-size: 19px; font-weight: 900; letter-spacing: 1.5px; color: var(--primary); text-transform: uppercase; cursor: pointer; }
    .header-logged-out { display: flex; align-items: center; gap: 12px; }
    .btn-login { background: none; border: none; color: #fff; font-weight: 600; font-size: 14px; cursor: pointer; }
    .btn-signup { background: var(--primary); color: #041009; border: none; padding: 7px 16px; border-radius: 8px; font-weight: 700; font-size: 14px; cursor: pointer; }
    .header-logged-in { display: none; align-items: center; gap: 10px; }
    .balance-box { display: flex; flex-direction: column; align-items: flex-end; line-height: 1.1; cursor: pointer; }
    .balance-title { font-size: 10px; color: var(--text-muted); }
    .balance-amount { font-size: 14px; font-weight: 700; color: #fff; }
    .user-pill { background: rgba(0,0,0,0.35); border: 1px solid var(--border); border-radius: 20px; padding: 3px 6px 3px 3px; display: flex; align-items: center; gap: 6px; cursor: pointer; }
    .user-avatar-circle { width: 28px; height: 28px; border-radius: 50%; background: #184431; display: flex; align-items: center; justify-content: center; color: #bbf7d0; font-size: 13px; }

    /* CONTAINER & VIEWS */
    .container { max-width: 480px; margin: 0 auto; padding: 10px 12px; display: flex; flex-direction: column; gap: 14px; }
    .view-panel { display: none; flex-direction: column; gap: 14px; }
    .view-panel.active-view { display: flex; }

    /* CARDS */
    .promo-banner { width: 100%; height: 145px; background: linear-gradient(135deg, #093b26 0%, #031c10 100%); border-radius: var(--radius); display: flex; align-items: center; padding: 18px; border: 1px solid rgba(0,230,118,0.2); }
    .hub-card { background: var(--primary-grad); border-radius: var(--radius); padding: 14px; display: flex; flex-direction: column; gap: 12px; border: 1px solid rgba(255,255,255,0.05); }
    .hub-header { display: flex; justify-content: space-between; align-items: center; }
    .hub-title { font-size: 16px; font-weight: 700; }
    .hub-tag { font-size: 13px; font-weight: 800; color: var(--primary); text-transform: uppercase; }
    .pills-row { display: flex; gap: 8px; overflow-x: auto; scrollbar-width: none; }
    .pills-row::-webkit-scrollbar { display: none; }
    .hub-pill-btn { background: rgba(0,0,0,0.35); border: 1px solid rgba(255,255,255,0.06); color: #fff; padding: 8px 14px; border-radius: 8px; font-size: 12px; font-weight: 500; white-space: nowrap; display: flex; align-items: center; gap: 6px; cursor: pointer; }

    /* SLIDERS */
    .section-title { font-size: 15px; font-weight: 700; display: flex; align-items: center; justify-content: space-between; margin-top: 4px; }
    .slider-row { display: flex; gap: 10px; overflow-x: auto; scrollbar-width: none; padding-bottom: 4px; }
    .slider-row::-webkit-scrollbar { display: none; }
    .sport-card { min-width: 105px; height: 155px; border-radius: var(--radius); position: relative; flex-shrink: 0; display: flex; align-items: flex-end; padding: 10px; background-size: cover; background-position: center top; border: 1px solid var(--border); }
    .sport-card::before, .game-card-tall::before, .c-box::before { content: ''; position: absolute; inset: 0; background: linear-gradient(180deg, transparent 40%, rgba(0,0,0,0.9) 100%); border-radius: var(--radius); }
    .sport-card span { position: relative; font-size: 12px; font-weight: 800; text-transform: uppercase; }

    /* CASINO VIEW */
    .casino-search { display: flex; align-items: center; gap: 10px; background: var(--bg-surface); border: 1px solid var(--border); border-radius: 12px; padding: 10px 14px; }
    .casino-search input { background: transparent; border: none; outline: none; color: #fff; font-size: 13px; flex: 1; }
    .providers-bar { display: flex; gap: 8px; overflow-x: auto; scrollbar-width: none; }
    .providers-bar::-webkit-scrollbar { display: none; }
    .provider-chip { background: var(--bg-surface); border: 1px solid var(--border); border-radius: 10px; padding: 6px 14px; font-size: 11px; font-weight: 700; color: var(--text-muted); white-space: nowrap; cursor: pointer; display: flex; align-items: center; gap: 6px; }
    .provider-chip.active { border-color: var(--primary); color: #fff; background: #0f3826; }
    .c-filters { display: flex; gap: 8px; overflow-x: auto; scrollbar-width: none; }
    .c-filters::-webkit-scrollbar { display: none; }
    .c-filter-btn { background: rgba(255,255,255,0.05); border: 1px solid var(--border); border-radius: 20px; padding: 7px 15px; font-size: 12px; font-weight: 600; color: var(--text-muted); white-space: nowrap; cursor: pointer; }
    .c-filter-btn.active { background: var(--primary); color: #041009; font-weight: 800; }
    .game-card-tall { min-width: 105px; height: 135px; border-radius: var(--radius); position: relative; flex-shrink: 0; display: flex; flex-direction: column; justify-content: flex-end; padding: 8px; background-size: cover; background-position: center; border: 1px solid var(--border); cursor: pointer; }
    .game-card-tall .t, .c-box .t { position: relative; font-size: 11px; font-weight: 700; z-index: 2; }
    .game-card-tall .p, .c-box .p { position: relative; font-size: 8px; color: var(--primary); text-transform: uppercase; font-weight: 700; z-index: 2; }
    .casino-grid-2col { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .c-box { height: 125px; border-radius: var(--radius); position: relative; overflow: hidden; display: flex; flex-direction: column; justify-content: flex-end; padding: 10px; background-size: cover; background-position: center; border: 1px solid var(--border); cursor: pointer; }

    /* CHAT & BOTTOM NAV */
    .floating-chat-wrap { position: fixed; bottom: 84px; left: 16px; width: 48px; height: 48px; z-index: 99; cursor: pointer; }
    .floating-chat-bubble { width: 100%; height: 100%; border-radius: 50%; background: #ffd600; color: #1a1a1a; display: flex; align-items: center; justify-content: center; font-size: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.4); }
    .chat-badge { position: absolute; top: -2px; right: -2px; background: var(--danger); color: #fff; font-size: 10px; font-weight: 800; width: 18px; height: 18px; border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid var(--bg-base); }
    .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; height: 64px; background: #061910; border-top: 1px solid var(--border); display: flex; justify-content: space-around; align-items: center; z-index: 1000; }
    .nav-tab { display: flex; flex-direction: column; align-items: center; gap: 4px; color: var(--text-muted); text-decoration: none; font-size: 10px; font-weight: 600; cursor: pointer; }
    .nav-tab i { font-size: 18px; }
    .nav-tab.active { color: var(--primary); }

    /* DRAWER */
    .drawer-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.65); backdrop-filter: blur(5px); z-index: 2500; display: none; }
    .drawer-overlay.active { display: block; }
    .profile-drawer { position: fixed; top: 0; right: 0; width: 72%; max-width: 330px; height: 100%; background: var(--drawer-top); border-top-left-radius: 28px; z-index: 2600; display: flex; flex-direction: column; overflow-y: auto; transform: translateX(100%); transition: transform 0.28s ease; box-shadow: -10px 0 30px rgba(0,0,0,0.7); }
    .drawer-overlay.active .profile-drawer { transform: translateX(0); }
    .drawer-level-circle { width: 76px; height: 76px; border-radius: 50%; background: #00d07e; color: #fff; font-size: 42px; font-weight: 800; display: flex; align-items: center; justify-content: center; margin: 16px auto 14px auto; }
    .drawer-balance-box { background: #121827; border-radius: 12px; padding: 14px; margin: 0 16px 14px 16px; display: flex; flex-direction: column; gap: 12px; }
    .drawer-deposit-btn { width: 100%; height: 42px; background: #00d07e; color: #fff; font-size: 15px; font-weight: 700; border: none; border-radius: 8px; cursor: pointer; }
    .drawer-menu-list { display: flex; flex-direction: column; padding: 0 18px; }
    .drawer-menu-item { padding: 12px 0; font-size: 13.5px; color: #edf2f7; border-bottom: 1px solid rgba(255,255,255,0.06); cursor: pointer; }
    .drawer-lower-section { background: var(--drawer-bot); padding: 8px 18px 24px 18px; margin-top: 10px; display: flex; flex-direction: column; flex: 1; }

    /* INDEPENDENT MODALS */
    .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.7); backdrop-filter: blur(6px); z-index: 3000; display: none; justify-content: center; align-items: center; padding: 16px; }
    .modal-overlay.active { display: flex; }
    .modal-card { background: #fff; color: #111827; width: 100%; max-width: 400px; border-radius: 24px; padding: 24px 20px; box-shadow: 0 20px 45px rgba(0,0,0,0.6); display: flex; flex-direction: column; gap: 12px; max-height: 92vh; overflow-y: auto; }
    .auth-header { display: flex; justify-content: space-between; align-items: center; font-size: 20px; font-weight: 800; }
    .close-btn { width: 32px; height: 32px; background: #f1f3f5; border-radius: 8px; border: none; color: #6b7280; cursor: pointer; font-size: 16px; }
    .form-group { display: flex; flex-direction: column; gap: 10px; }
    .input-field { width: 100%; height: 48px; background: #edf2f7; border: 1px solid transparent; border-radius: 10px; padding: 0 16px; font-size: 14px; outline: none; }
    .select-wrap { position: relative; }
    .select-field { width: 100%; height: 48px; background: #edf2f7; border: none; border-radius: 10px; padding: 0 16px; font-size: 14px; color: #4b5563; appearance: none; outline: none; }
    .select-arrow { position: absolute; right: 16px; top: 50%; transform: translateY(-50%); pointer-events: none; color: #6b7280; }
    .modal-submit-btn { width: 100%; height: 50px; background: #00d07e; color: #fff; font-size: 16px; font-weight: 700; border: none; border-radius: 12px; cursor: pointer; margin-top: 4px; box-shadow: 0 4px 12px rgba(0,208,126,0.35); }
    .modal-footer-text { text-align: center; font-size: 13px; color: #6b7280; }
    .modal-footer-text a { color: #00d07e; font-weight: 700; text-decoration: none; cursor: pointer; }
    .signup-tabs { display: flex; background: #eef2f6; border-radius: 8px; padding: 4px; align-self: center; }
    .tab-btn { border: none; background: transparent; padding: 6px 20px; font-size: 13px; font-weight: 600; border-radius: 6px; cursor: pointer; color: #4b5563; }
    .tab-btn.active { background: #00d07e; color: #fff; }
    .phone-wrap { display: flex; background: #edf2f7; border-radius: 10px; height: 48px; align-items: center; padding: 0 10px; gap: 6px; }
    .phone-wrap select { border: none; background: transparent; font-size: 13px; font-weight: 600; outline: none; padding-right: 6px; border-right: 1px solid #d1d5db; }
    .phone-wrap input { flex: 1; border: none; background: transparent; font-size: 14px; outline: none; padding-left: 6px; }
    .toggle-row { display: flex; align-items: center; gap: 12px; font-size: 13px; color: #4b5563; cursor: pointer; }
    .switch { position: relative; width: 44px; height: 24px; flex-shrink: 0; }
    .switch input { opacity: 0; width: 0; height: 0; }
    .slider { position: absolute; inset: 0; background-color: #cbd5e1; transition: 0.3s; border-radius: 24px; cursor: pointer; }
    .slider:before { position: absolute; content: ""; height: 18px; width: 18px; left: 3px; bottom: 3px; background-color: white; transition: 0.3s; border-radius: 50%; }
    input:checked + .slider { background-color: #00d07e; }
    input:checked + .slider:before { transform: translateX(20px); }
    .hidden-in-quick { display: none !important; }

    /* DEPOSIT BADGES */
    .method-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .method-box { border: 2px solid #e2e8f0; border-radius: 14px; padding: 12px 10px; display: flex; flex-direction: column; align-items: center; gap: 8px; cursor: pointer; background: #f8fafc; }
    .method-box.selected { border-color: #00d07e; background: rgba(0,208,126,0.06); }
    .mtn-badge { width: 74px; height: 42px; background: #ffcc00; border-radius: 22px; display: flex; align-items: center; justify-content: center; }
    .mtn-badge span { color: #000; font-weight: 900; font-size: 16px; border: 2px solid #000; padding: 1px 7px; border-radius: 12px; }
    .airtel-badge { width: 74px; height: 42px; background: #e60000; border-radius: 10px; display: flex; flex-direction: column; align-items: center; justify-content: center; color: #fff; font-weight: 900; font-size: 13px; }
    .preset-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; }
    .preset-chip { background: #f1f5f9; border: 1px solid #e2e8f0; border-radius: 8px; padding: 8px 4px; font-size: 12px; font-weight: 700; text-align: center; cursor: pointer; }
    .preset-chip.active { background: #00d07e; color: #fff; }

    /* ADMIN DASHBOARD */
    #adminView { display: none; background: #040f09; min-height: 100vh; width: 100%; position: absolute; top: 0; left: 0; z-index: 5000; padding-bottom: 50px; }
    #adminView.active-admin { display: block; }
    .admin-header { background: #081a11; padding: 14px 18px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--border); }
    .admin-badge { background: var(--danger); color: #fff; font-size: 10px; font-weight: 900; padding: 3px 8px; border-radius: 6px; }
    .admin-metrics-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; padding: 14px; }
    .metric-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 12px; padding: 14px; display: flex; flex-direction: column; gap: 4px; }
    .metric-val { font-size: 20px; font-weight: 900; color: var(--primary); }
    .metric-lbl { font-size: 11px; color: var(--text-muted); display: flex; align-items: center; gap: 6px; }
    .admin-nav-bar { display: flex; overflow-x: auto; gap: 8px; padding: 0 14px 12px 14px; border-bottom: 1px solid var(--border); scrollbar-width: none; }
    .admin-nav-bar::-webkit-scrollbar { display: none; }
    .admin-tab-btn { background: var(--bg-surface); border: 1px solid var(--border); color: var(--text-muted); padding: 8px 16px; border-radius: 8px; font-size: 12px; font-weight: 700; white-space: nowrap; cursor: pointer; }
    .admin-tab-btn.active { background: var(--primary); color: #041009; border-color: var(--primary); }
    .admin-section { padding: 14px; display: none; flex-direction: column; gap: 14px; }
    .admin-section.active-sec { display: flex; }
    .admin-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 12px; padding: 14px; display: flex; flex-direction: column; gap: 10px; }
    .admin-user-row { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 13px; }
    .btn-ban { background: var(--danger); color: #fff; border: none; padding: 5px 12px; border-radius: 6px; font-size: 11px; font-weight: 700; cursor: pointer; }
    .btn-unban { background: #00d07e; color: #fff; border: none; padding: 5px 12px; border-radius: 6px; font-size: 11px; font-weight: 700; cursor: pointer; }
    .match-edit-box { background: #0a2116; border: 1px solid var(--border); border-radius: 10px; padding: 12px; display: flex; flex-direction: column; gap: 8px; }
    .odds-inputs-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; }
    .odds-input { background: #06180f; border: 1px solid var(--border); color: #fff; padding: 6px; border-radius: 6px; font-size: 12px; text-align: center; font-weight: 700; }
    .live-pulse { width: 8px; height: 8px; background: #00e676; border-radius: 50%; display: inline-block; animation: pulse 1.2s infinite; }
    @keyframes pulse { 0% { opacity: 0.3; } 50% { opacity: 1; } 100% { opacity: 0.3; } }
  </style>
</head>
<body>

  <!-- HEADER -->
  <header id="mainHeader">
    <div class="brand-logo" onclick="switchMainView('sports')">
      <i class="fa-solid fa-shield-halved"></i> VIKING
    </div>
    <div class="header-logged-out" id="loggedOutView">
      <button class="btn-login" onclick="openLoginModal()">Log in</button>
      <button class="btn-signup" onclick="openSignupModal()">Sign Up</button>
    </div>
    <div class="header-logged-in" id="loggedInView">
      <div class="balance-box" onclick="openDepositModal()">
        <span class="balance-title">Balance</span>
        <span class="balance-amount" id="headerBalanceDisplay">0 USh</span>
      </div>
      <div class="user-pill" onclick="openProfileDrawer()">
        <div class="user-avatar-circle"><i class="fa-solid fa-user"></i></div>
        <i class="fa-solid fa-ellipsis-vertical" style="color:var(--text-muted); font-size:15px;"></i>
      </div>
    </div>
  </header>

  <!-- MAIN USER CONTAINER -->
  <main class="container" id="mainContainer">

    <!-- 1. SPORTSBOOK VIEW -->
    <div class="view-panel active-view" id="sportsView">
      <div class="promo-banner">
        <div>
          <h2 style="font-size:19px; color:var(--primary); text-transform:uppercase; font-weight:900;">Worldwide<br>Access</h2>
          <p style="font-size:11px; color:var(--text-muted);">We work with players from all countries</p>
        </div>
      </div>

      <div class="hub-card">
        <div class="hub-header">
          <span class="hub-title">Matches</span>
          <span class="hub-tag">LIVE Sport</span>
        </div>
        <div class="pills-row">
          <button class="hub-pill-btn"><i class="fa-solid fa-hockey-puck"></i> Hockey</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-baseball"></i> Tennis</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-basketball"></i> Basketball</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-baseball-bat-ball"></i> Baseball</button>
        </div>
      </div>

      <!-- LIVE MATCHES DISPLAY -->
      <div class="section-title">
        <span><i class="fa-solid fa-bolt" style="color:#ff334b;"></i> Live Matches</span>
        <span style="font-size:11px; color:var(--primary); cursor:pointer;">All (24)</span>
      </div>
      <div id="liveMatchesContainer" style="display: flex; flex-direction: column; gap: 10px;"></div>

      <!-- CASINO BANNER HUB -->
      <div class="hub-card" style="background: linear-gradient(90deg, #0e3b28 0%, #155d3e 100%); cursor:pointer;" onclick="switchMainView('casino')">
        <div class="hub-header">
          <span class="hub-title">Casino</span>
          <span class="hub-tag">LIVE Casino</span>
        </div>
        <div class="pills-row">
          <button class="hub-pill-btn"><i class="fa-solid fa-dice"></i> Popular</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-border-all"></i> Top Games</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-dharmachakra"></i> Poker</button>
          <button class="hub-pill-btn"><i class="fa-solid fa-gem"></i> Slots</button>
        </div>
      </div>

      <div class="section-title"><span><i class="fa-solid fa-basketball"></i> Sports are trending</span></div>
      <div class="slider-row">
        <div class="sport-card" style="background-image: url('https://images.unsplash.com/photo-1595435934249-5df7ed86e1c0?auto=format&fit=crop&w=300&q=80')"><span>Tennis</span></div>
        <div class="sport-card" style="background-image: url('https://images.unsplash.com/photo-1546519638-68e109498ffc?auto=format&fit=crop&w=300&q=80')"><span>Basketball</span></div>
        <div class="sport-card" style="background-image: url('https://images.unsplash.com/photo-1580748141549-71748dbe0bdc?auto=format&fit=crop&w=300&q=80')"><span>Rugby</span></div>
        <div class="sport-card" style="background-image: url('https://images.unsplash.com/photo-1508098682722-e99c43a406b2?auto=format&fit=crop&w=300&q=80')"><span>Baseball</span></div>
      </div>
    </div>

    <!-- 2. CASINO LOBBY VIEW -->
    <div class="view-panel" id="casinoView">
      <div class="casino-search">
        <i class="fa-solid fa-magnifying-glass" style="color:var(--text-muted); font-size:14px;"></i>
        <input type="text" placeholder="Search games or providers..." />
      </div>

      <div class="section-title" style="font-size:13px; color:var(--text-muted);">
        <span>TOP PROVIDERS</span>
        <span style="color:var(--primary); font-size:11px; cursor:pointer;">All (38)</span>
      </div>
      <div class="providers-bar">
        <div class="provider-chip active"><i class="fa-solid fa-crown"></i> Pragmatic Play</div>
        <div class="provider-chip"><i class="fa-solid fa-diamond"></i> Evolution</div>
        <div class="provider-chip"><i class="fa-solid fa-jet-fighter"></i> Spribe (Aviator)</div>
        <div class="provider-chip"><i class="fa-solid fa-dice-d20"></i> NetEnt</div>
        <div class="provider-chip"><i class="fa-solid fa-book"></i> Novomatic</div>
        <div class="provider-chip"><i class="fa-solid fa-ghost"></i> Hacksaw Gaming</div>
      </div>

      <div class="c-filters">
        <button class="c-filter-btn active">All Games</button>
        <button class="c-filter-btn">Slots</button>
        <button class="c-filter-btn">Live Casino</button>
        <button class="c-filter-btn">Crash (Aviator)</button>
        <button class="c-filter-btn">Jackpot</button>
      </div>

      <div class="section-title"><span><i class="fa-solid fa-cherries" style="color:#ff334b;"></i> Trending games</span></div>
      <div class="slider-row">
        <div class="game-card-tall" style="background-image: url('https://images.unsplash.com/photo-1606167668584-78701c57f13d?auto=format&fit=crop&w=300&q=80')"><span class="t">Sweet Bonanza 1000</span><span class="p">Pragmatic Play</span></div>
        <div class="game-card-tall" style="background-image: url('https://images.unsplash.com/photo-1518609878373-06d740f60d8b?auto=format&fit=crop&w=300&q=80')"><span class="t">Gates of Olympus 1000</span><span class="p">Pragmatic Play</span></div>
        <div class="game-card-tall" style="background-image: url('https://images.unsplash.com/photo-1511193311914-0346f16efe90?auto=format&fit=crop&w=300&q=80')"><span class="t">Sugar Rush 1000</span><span class="p">Pragmatic Play</span></div>
      </div>

      <div class="section-title"><span><i class="fa-solid fa-fire" style="color:#ffb300;"></i> Hot Games</span></div>
      <div class="casino-grid-2col">
        <div class="c-box" style="background-image: url('https://images.unsplash.com/photo-1533488765986-dfa2a9939acd?auto=format&fit=crop&w=300&q=80')"><span class="t">Narcos</span><span class="p">Video Slot</span></div>
        <div class="c-box" style="background-image: url('https://images.unsplash.com/photo-1518709268805-4e9042af9f23?auto=format&fit=crop&w=300&q=80')"><span class="t">Aztec Gold</span><span class="p">Megaways</span></div>
        <div class="c-box" style="background-image: url('https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?auto=format&fit=crop&w=300&q=80')"><span class="t">Space Wars</span><span class="p">NetEnt</span></div>
        <div class="c-box" style="background-image: url('https://images.unsplash.com/photo-1509198397868-475647b2a1e5?auto=format&fit=crop&w=300&q=80')"><span class="t">Book of Ra</span><span class="p">Deluxe</span></div>
      </div>
    </div>

  </main>

  <!-- CHAT BUTTON -->
  <div class="floating-chat-wrap" id="floatingChatBtn" onclick="alert('Support chat opening...')">
    <div class="floating-chat-bubble"><i class="fa-solid fa-comment-dots"></i></div>
    <div class="chat-badge">1</div>
  </div>

  <!-- BOTTOM NAV -->
  <nav class="bottom-nav" id="mainBottomNav">
    <div class="nav-tab active" id="tabNavBets" onclick="switchMainView('sports')"><i class="fa-solid fa-receipt"></i><span>Bets</span></div>
    <div class="nav-tab" id="tabNavCasino" onclick="switchMainView('casino')"><i class="fa-solid fa-circle-dot"></i><span>Casino</span></div>
    <div class="nav-tab" onclick="openDepositModal()"><i class="fa-solid fa-wallet"></i><span>Deposit</span></div>
    <div class="nav-tab" onclick="alert('Support center')"><i class="fa-solid fa-headset"></i><span>Support</span></div>
    <div class="nav-tab" onclick="openProfileDrawer()"><i class="fa-solid fa-bars"></i><span>More</span></div>
  </nav>

  <!-- =====================================
       ADMIN DASHBOARD FULL VIEW
       ===================================== -->
  <div id="adminView">
    <div class="admin-header">
      <div>
        <div style="display:flex; align-items:center; gap:8px;">
          <span class="brand-logo" style="font-size:18px;">VIKING</span>
          <span class="admin-badge">ADMIN CONTROL</span>
        </div>
        <div style="font-size:12px; color:var(--text-muted);"><span class="live-pulse"></span> Super Admin Session Active</div>
      </div>
      <div style="display:flex; gap:8px;">
        <button onclick="previewUserSite()" style="background:#00d07e; color:#041009; border:none; padding:6px 12px; border-radius:6px; font-size:11px; font-weight:800; cursor:pointer;"><i class="fa-solid fa-eye"></i> View Site</button>
        <button onclick="logoutAdmin()" style="background:var(--danger); color:#fff; border:none; padding:6px 12px; border-radius:6px; font-size:11px; font-weight:800; cursor:pointer;"><i class="fa-solid fa-arrow-right-from-bracket"></i> Exit</button>
      </div>
    </div>

    <!-- Live Analytics Metrics -->
    <div class="admin-metrics-grid">
      <div class="metric-card">
        <span class="metric-val" id="metricOnlineUsers">342</span>
        <span class="metric-lbl"><span class="live-pulse"></span> People Online Now</span>
      </div>
      <div class="metric-card">
        <span class="metric-val" id="metricTotalUsers">12,894</span>
        <span class="metric-lbl"><i class="fa-solid fa-users" style="color:var(--primary);"></i> Total App Users</span>
      </div>
      <div class="metric-card">
        <span class="metric-val">48.2M USh</span>
        <span class="metric-lbl"><i class="fa-solid fa-coins" style="color:var(--accent-gold);"></i> Total Volume Today</span>
      </div>
      <div class="metric-card">
        <span class="metric-val" id="metricActiveMatches">2</span>
        <span class="metric-lbl"><i class="fa-solid fa-futbol" style="color:var(--primary);"></i> Active Matches</span>
      </div>
    </div>

    <!-- Admin Nav Tabs -->
    <div class="admin-nav-bar">
      <button class="admin-tab-btn active" onclick="switchAdminTab('usersTab', this)"><i class="fa-solid fa-user-slash"></i> Users & Bans</button>
      <button class="admin-tab-btn" onclick="switchAdminTab('editMatchesTab', this)"><i class="fa-solid fa-pen-to-square"></i> Edit Matches</button>
      <button class="admin-tab-btn" onclick="switchAdminTab('videoMatchTab', this)"><i class="fa-solid fa-video"></i> Add Video Match</button>
      <button class="admin-tab-btn" onclick="switchAdminTab('trafficTab', this)"><i class="fa-solid fa-chart-line"></i> People History</button>
    </div>

    <!-- 1. USERS & BANS TAB -->
    <div class="admin-section active-sec" id="usersTab">
      <div class="admin-card">
        <div style="font-size:14px; font-weight:800; display:flex; justify-content:space-between;">
          <span>Registered App Users</span>
          <span style="font-size:12px; color:var(--text-muted);" id="userCountStatus"></span>
        </div>
        <div id="usersListContainer"></div>
      </div>
    </div>

    <!-- 2. EDIT MATCHES TAB -->
    <div class="admin-section" id="editMatchesTab">
      <div class="admin-card">
        <div style="font-size:14px; font-weight:800; margin-bottom:4px;">Live Match Odds & Scores Editor</div>
        <div id="adminMatchEditorList" style="display:flex; flex-direction:column; gap:10px;"></div>
      </div>
    </div>

    <!-- 3. ADD VIDEO MATCH TAB -->
    <div class="admin-section" id="videoMatchTab">
      <div class="admin-card">
        <div style="font-size:14px; font-weight:800;">Add Live Stream / Video Match</div>
        <form onsubmit="event.preventDefault(); submitNewVideoMatch();" style="display:flex; flex-direction:column; gap:10px;">
          <input type="text" class="input-field" id="newMatchLeague" placeholder="League (e.g. Uganda Premier League)" required style="background:#092416; color:#fff;" />
          <input type="text" class="input-field" id="newMatchTeams" placeholder="Teams (e.g. Vipers SC vs KCCA FC)" required style="background:#092416; color:#fff;" />
          <input type="text" class="input-field" id="newMatchVideoUrl" placeholder="Live Video Embed URL (e.g. https://www.youtube.com/embed/...)" required style="background:#092416; color:#fff;" />
          <div style="font-size:12px; color:var(--text-muted);">Initial Odds:</div>
          <div class="odds-inputs-row">
            <input type="number" step="0.01" class="odds-input" id="newOdd1" placeholder="1" value="1.85" required />
            <input type="number" step="0.01" class="odds-input" id="newOddX" placeholder="X" value="3.40" required />
            <input type="number" step="0.01" class="odds-input" id="newOdd2" placeholder="2" value="4.20" required />
          </div>
          <button type="submit" class="modal-submit-btn" style="background:#00d07e; color:#041009; font-weight:900;">Add & Broadcast Match</button>
        </form>
      </div>
    </div>

    <!-- 4. REAL-TIME TRAFFIC & VISITORS HISTORY -->
    <div class="admin-section" id="trafficTab">
      <div class="admin-card">
        <div style="font-size:14px; font-weight:800;">Live People Activity Log</div>
        <div id="trafficLogsContainer" style="display:flex; flex-direction:column; gap:8px;"></div>
      </div>
    </div>
  </div>

  <!-- PROFILE DRAWER -->
  <div class="drawer-overlay" id="profileDrawerOverlay" onclick="closeProfileDrawerOnOutside(event)">
    <div class="profile-drawer">
      <div class="drawer-level-circle">1</div>
      <div class="drawer-balance-box">
        <div style="display:flex; justify-content:space-between; align-items:baseline;">
          <span style="font-size:11px; color:#8a9bb8;">Balance</span>
          <span style="font-size:16px; font-weight:700; color:#fff;" id="drawerBalanceDisplay">0 USh</span>
        </div>
        <button class="drawer-deposit-btn" onclick="openDepositModal()">Deposit</button>
      </div>
      <div class="drawer-menu-list">
        <div class="drawer-menu-item" onclick="openWithdrawModal()">Withdrawal Request</div>
        <div class="drawer-menu-item">Bring a friend</div>
        <div class="drawer-menu-item">Transaction History</div>
        <div class="drawer-menu-item">Support</div>
        <div class="drawer-menu-item" onclick="openSettingsModal()">Settings</div>
        <div class="drawer-menu-item" onclick="logout()" style="color:#ff5252;">Exit</div>
      </div>
      <div class="drawer-lower-section">
        <div class="drawer-menu-item" onclick="switchMainView('sports'); closeProfileDrawer();">Home</div>
        <div class="drawer-menu-item" onclick="switchMainView('casino'); closeProfileDrawer();">Casino</div>
        <div class="drawer-menu-item" onclick="switchMainView('sports'); closeProfileDrawer();">Bets</div>
      </div>
    </div>
  </div>

  <!-- =====================================
       1. SIGN UP MODAL (STRICT EMAIL ONLY & DUPLICATE CHECK)
       ===================================== -->
  <div class="modal-overlay" id="signupModal" onclick="closeOnOutside(event, 'signupModal')">
    <div class="modal-card">
      <div class="auth-header"><span>Sign Up</span><button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button></div>
      <div class="signup-tabs">
        <button class="tab-btn active" id="tabDefault" onclick="setRegistrationMode('default')">Default</button>
        <button class="tab-btn" id="tabQuick" onclick="setRegistrationMode('quick')">Quick</button>
      </div>
      <form class="form-group" onsubmit="event.preventDefault(); handleSignUpSubmit();">
        <input type="text" class="input-field default-field" placeholder="Your name" id="inputName" />
        <div class="phone-wrap default-field">
          <select id="countrySelect">
            <option value="+256" selected>🇺🇬 +256</option>
            <option value="+1">🇺🇸 +1</option>
            <option value="+254">🇰🇪 +254</option>
          </select>
          <input type="tel" placeholder="700 123-456" id="phoneInput" />
        </div>
        <div class="select-wrap">
          <select class="select-field" required>
            <option value="UGX" selected>UGX - Ugandan Shilling</option>
            <option value="USD">USD - US Dollar</option>
          </select>
          <i class="fa-solid fa-chevron-down select-arrow"></i>
        </div>
        <!-- ONLY EMAILS ALLOWED -->
        <input type="email" class="input-field" placeholder="Email Address (e.g. user@gmail.com)" id="signupEmailInput" required />
        <input type="password" class="input-field default-field" placeholder="Password" id="signupPasswordInput" />
        
        <label class="toggle-row"><div class="switch"><input type="checkbox" required /><span class="slider"></span></div><span>I accept terms & conditions</span></label>
        <label class="toggle-row"><div class="switch"><input type="checkbox" required /><span class="slider"></span></div><span>I am 18 years old or older</span></label>
        <button type="submit" class="modal-submit-btn">Sign Up</button>
      </form>
      <div class="modal-footer-text">Already have an account? <a onclick="openLoginModal()">Log in</a></div>
    </div>
  </div>

  <!-- =====================================
       2. LOG IN MODAL (STRICT EMAIL ONLY)
       ===================================== -->
  <div class="modal-overlay" id="loginModal" onclick="closeOnOutside(event, 'loginModal')">
    <div class="modal-card">
      <div class="auth-header"><span>Log in</span><button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button></div>
      <form class="form-group" onsubmit="event.preventDefault(); handleLoginSubmit();">
        <!-- Generic placeholder: NO ADMIN EMAIL LEAKED -->
        <input type="email" class="input-field" id="loginEmailInput" placeholder="Enter your email" required />
        <input type="password" class="input-field" id="loginPasswordInput" placeholder="Password" required />
        <div style="text-align:right;">
          <a href="javascript:void(0)" style="color:#9ca3af; font-size:13px; text-decoration:none;" onclick="openForgotPassModal()">Forgot your password?</a>
        </div>
        <button type="submit" class="modal-submit-btn">Log in</button>
      </form>
      <div class="modal-footer-text">Don't have an account yet? <a onclick="openSignupModal()">Sign Up</a></div>
    </div>
  </div>

  <!-- =====================================
       2B. FORGOT PASSWORD (GMAIL CODE VERIFICATION)
       ===================================== -->
  <div class="modal-overlay" id="forgotPassModal" onclick="closeOnOutside(event, 'forgotPassModal')">
    <div class="modal-card">
      <div class="auth-header">
        <span id="resetModalTitle">Password Recovery</span>
        <button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button>
      </div>

      <!-- STEP 1: Request Code -->
      <form class="form-group" id="forgotStep1" onsubmit="event.preventDefault(); sendGmailVerificationCode();">
        <p style="font-size:12px; color:#6b7280; line-height:1.4;">Enter your registered email address. We will send a 6-digit verification code to your Gmail app.</p>
        <input type="email" class="input-field" id="forgotEmailInput" placeholder="Enter your registered email" required />
        <button type="submit" class="modal-submit-btn" id="btnSendCode">Send Verification Code</button>
      </form>

      <!-- STEP 2: Verify Code & Set New Password -->
      <form class="form-group" id="forgotStep2" style="display:none;" onsubmit="event.preventDefault(); verifyCodeAndResetPassword();">
        <div style="background:#eefdf3; border:1px solid #bbf7d0; border-radius:8px; padding:10px; font-size:12px; color:#166534;">
          <i class="fa-solid fa-envelope-circle-check"></i> Code sent to your Gmail inbox! Please check your Gmail app.
        </div>
        <input type="text" maxlength="6" class="input-field" id="verifyCodeInput" placeholder="Enter 6-digit code (e.g. 849201)" required style="letter-spacing:4px; font-weight:800; text-align:center; font-size:16px;" />
        <input type="password" class="input-field" id="newResetPassword" placeholder="Enter new password" required minlength="6" />
        <button type="submit" class="modal-submit-btn">Reset Password & Log In</button>
      </form>

      <div class="modal-footer-text">
        Remembered password? <a onclick="openLoginModal()">Back to Log in</a>
      </div>
    </div>
  </div>

  <!-- 3. WITHDRAWAL MODAL -->
  <div class="modal-overlay" id="withdrawModal" onclick="closeOnOutside(event, 'withdrawModal')">
    <div class="modal-card">
      <div class="auth-header"><span>Withdrawal Request</span><button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button></div>
      <form class="form-group" onsubmit="event.preventDefault(); processWithdrawal();">
        <input type="number" class="input-field" placeholder="Enter amount" id="withdrawAmountInput" required min="1000" />
        <div class="select-wrap">
          <select class="select-field" required id="withdrawSystemSelect">
            <option value="mtn">MTN Mobile Money (Uganda)</option>
            <option value="airtel">Airtel Money (Uganda)</option>
          </select>
          <i class="fa-solid fa-chevron-down select-arrow"></i>
        </div>
        <input type="text" class="input-field" placeholder="Wallet / Phone number" id="withdrawAccountInput" required />
        <button type="submit" class="modal-submit-btn">Run</button>
      </form>
    </div>
  </div>

  <!-- 4. DEPOSIT MODAL -->
  <div class="modal-overlay" id="depositModal" onclick="closeOnOutside(event, 'depositModal')">
    <div class="modal-card">
      <div class="auth-header"><span>Deposit</span><button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button></div>
      <div class="method-grid">
        <div class="method-box selected" id="methodMTN" onclick="selectPaymentMethod('mtn')">
          <div class="mtn-badge"><span>MTN</span></div>
          <span style="font-size:12px; font-weight:700;">MTN MoMo</span>
        </div>
        <div class="method-box" id="methodAirtel" onclick="selectPaymentMethod('airtel')">
          <div class="airtel-badge">airtel</div>
          <span style="font-size:12px; font-weight:700;">Airtel Money</span>
        </div>
      </div>
      <form class="form-group" onsubmit="event.preventDefault(); processDeposit();">
        <div class="phone-wrap"><span style="font-size:14px;">🇺🇬 +256</span><input type="tel" id="depositPhoneInput" placeholder="770 123-456" required /></div>
        <input type="number" class="input-field" id="depositAmountInput" value="10000" min="500" required />
        <div class="preset-row">
          <div class="preset-chip" onclick="setPreset(5000, this)">5,000</div>
          <div class="preset-chip active" onclick="setPreset(10000, this)">10,000</div>
          <div class="preset-chip" onclick="setPreset(50000, this)">50,000</div>
        </div>
        <button type="submit" class="modal-submit-btn" id="depositSubmitBtn">Deposit 10,000 USh</button>
      </form>
    </div>
  </div>

  <!-- 5. SETTINGS MODAL -->
  <div class="modal-overlay" id="settingsModal" onclick="closeOnOutside(event, 'settingsModal')">
    <div class="modal-card">
      <div class="auth-header"><span>Settings</span><button class="close-btn" onclick="closeAllModals()"><i class="fa-solid fa-xmark"></i></button></div>
      <form class="form-group" onsubmit="event.preventDefault(); alert('Saved!'); closeAllModals();">
        <input type="text" class="input-field" value="ID: 8492019" readonly style="background:#e2e8f0; font-weight:600;" />
        <input type="password" class="input-field" placeholder="Change Password" />
        <button type="submit" class="modal-submit-btn">Save Changes</button>
      </form>
    </div>
  </div>

  <!-- =====================================
       JAVASCRIPT LOGIC
       ===================================== -->
  <script>
    let currentBalance = 0;
    let selectedMethod = 'mtn';
    let generatedVerificationCode = null;
    let pendingResetEmail = null;

    // REGISTERED USERS DATABASE (IN MEMORY)
    let usersList = [
      { id: 101, name: "Kato Ivan", email: "kato.ivan@gmail.com", password: "Password123", phone: "+256 772 109283", country: "🇺🇬 UG", online: true, banned: false },
      { id: 102, name: "Mwesigwa Ronald", email: "ronald.mwe@yahoo.com", password: "Password123", phone: "+256 752 491029", country: "🇺🇬 UG", online: true, banned: false },
      { id: 103, name: "Sarah Nansubuga", email: "sarah.n@gmail.com", password: "Password123", phone: "+256 701 391024", country: "🇺🇬 UG", online: false, banned: false }
    ];

    let liveMatches = [
      { id: 1, league: "Premier League", team1: "Arsenal", team2: "Chelsea", score1: 2, score2: 1, minute: 68, odd1: 1.45, oddX: 4.20, odd2: 6.80, videoUrl: "" },
      { id: 2, league: "La Liga", team1: "Real Madrid", team2: "Barcelona", score1: 3, score2: 2, minute: 81, odd1: 1.20, oddX: 5.10, odd2: 11.0, videoUrl: "" }
    ];

    let trafficLogs = [
      { ip: "102.134.12.9", user: "Kato Ivan", action: "Placed 20,000 USh bet on Arsenal", time: "Just now", flag: "🇺🇬" },
      { ip: "197.239.4.11", user: "Mwesigwa Ronald", action: "Deposited 50,000 USh (MTN MoMo)", time: "1 min ago", flag: "🇺🇬" },
      { ip: "41.210.145.2", user: "Guest_849", action: "Browsing Sweet Bonanza 1000", time: "3 mins ago", flag: "🇺🇬" }
    ];

    window.addEventListener('DOMContentLoaded', () => {
      renderUserMatches();
      renderAdminMatches();
      renderAdminUsers();
      renderTrafficLogs();
    });

    // RENDER MATCHES
    function renderUserMatches() {
      const container = document.getElementById('liveMatchesContainer');
      container.innerHTML = liveMatches.map(m => `
        <div style="background:var(--bg-card); border-radius:var(--radius); padding:12px; border:1px solid var(--border); display:flex; flex-direction:column; gap:10px;">
          <div style="display:flex; justify-content:space-between; font-size:11px; color:var(--text-muted);">
            <span>${m.league} &bull; 2nd Half</span>
            <div style="display:flex; align-items:center; gap:5px; color:#ff334b; font-weight:700;">
              <span class="live-pulse" style="background:#ff334b;"></span> ${m.minute}'
            </div>
          </div>
          <div style="display:flex; flex-direction:column; gap:4px; font-size:14px; font-weight:600;">
            <div style="display:flex; justify-content:space-between;"><span>${m.team1}</span><span style="color:var(--primary); font-weight:800;">${m.score1}</span></div>
            <div style="display:flex; justify-content:space-between;"><span>${m.team2}</span><span style="color:var(--primary); font-weight:800;">${m.score2}</span></div>
          </div>
          ${m.videoUrl ? `
            <div style="position:relative; width:100%; border-radius:8px; overflow:hidden; margin:4px 0;">
              <iframe src="${m.videoUrl}" style="width:100%; height:160px; border:none;" allowfullscreen></iframe>
            </div>` : ''}
          <div style="display:grid; grid-template-columns:1fr 1fr 1fr; gap:8px;">
            <button class="hub-pill-btn" style="justify-content:center; flex-direction:column; padding:6px 0;"><span style="font-size:10px; color:var(--text-muted);">1</span><b>${m.odd1}</b></button>
            <button class="hub-pill-btn" style="justify-content:center; flex-direction:column; padding:6px 0;"><span style="font-size:10px; color:var(--text-muted);">X</span><b>${m.oddX}</b></button>
            <button class="hub-pill-btn" style="justify-content:center; flex-direction:column; padding:6px 0;"><span style="font-size:10px; color:var(--text-muted);">2</span><b>${m.odd2}</b></button>
          </div>
        </div>
      `).join('');
    }

    // SIGN UP: STRICT EMAIL VALIDATION & DUPLICATE PREVENTION
    function handleSignUpSubmit() {
      const email = document.getElementById('signupEmailInput').value.trim().toLowerCase();
      const name = document.getElementById('inputName').value.trim() || "User_" + Math.floor(Math.random()*1000);
      const phone = document.getElementById('phoneInput').value.trim() || "+256 700 000000";
      const password = document.getElementById('signupPasswordInput').value || "123456";

      // 1. Email format validation
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailRegex.test(email)) {
        alert("Please enter a valid email address (e.g., example@gmail.com). Only emails are permitted!");
        return;
      }

      // 2. Prevent duplicate signups
      const alreadyRegistered = usersList.some(u => u.email.toLowerCase() === email);
      if (alreadyRegistered) {
        alert("This email is already registered! Please log in, or click 'Forgot your password?' if you lost access.");
        openLoginModal();
        return;
      }

      // 3. Register user
      const newUser = {
        id: usersList.length + 101,
        name: name,
        email: email,
        password: password,
        phone: phone,
        country: "🇺🇬 UG",
        online: true,
        banned: false
      };

      usersList.push(newUser);
      renderAdminUsers();

      alert(`Registration Successful! Welcome to VikingBet, ${name}!`);
      completeAuth();
    }

    // LOGIN AUTHENTICATION (EMAIL ONLY + ADMIN CHECK)
    function handleLoginSubmit() {
      const email = document.getElementById('loginEmailInput').value.trim().toLowerCase();
      const pass = document.getElementById('loginPasswordInput').value;

      // 1. Check for Admin Credentials
      if (email === "darc88543@gmail.com" && pass === "Darcid@123") {
        closeAllModals();
        openAdminDashboard();
        return;
      }

      // 2. Regular User Login Check
      const foundUser = usersList.find(u => u.email.toLowerCase() === email);

      if (!foundUser) {
        alert("No account found with this email! Please check spelling or Sign Up.");
        return;
      }

      if (foundUser.banned) {
        alert("Your account has been suspended by administration. Please contact support.");
        return;
      }

      if (foundUser.password !== pass) {
        alert("Incorrect password! If you forgot it, click 'Forgot your password?' to verify via Gmail.");
        return;
      }

      // Successful login
      foundUser.online = true;
      renderAdminUsers();
      completeAuth();
    }

    // =====================================
    // FORGOT PASSWORD FLOW (GMAIL APP VERIFICATION CODE)
    // =====================================
    function openForgotPassModal() {
      closeAllModals();
      document.getElementById('forgotStep1').style.display = 'flex';
      document.getElementById('forgotStep2').style.display = 'none';
      document.getElementById('forgotEmailInput').value = '';
      document.getElementById('forgotPassModal').classList.add('active');
    }

    function sendGmailVerificationCode() {
      const email = document.getElementById('forgotEmailInput').value.trim().toLowerCase();
      const userExists = usersList.some(u => u.email.toLowerCase() === email);

      if (!userExists && email !== "darc88543@gmail.com") {
        alert("This email is not registered in our system. Please sign up first.");
        return;
      }

      pendingResetEmail = email;
      // Generate realistic 6-digit verification code
      generatedVerificationCode = Math.floor(100000 + Math.random() * 900000).toString();

      // Show alert simulating the Gmail notification
      alert(`[Gmail App Notification - VikingBet Security]\nA verification code has been sent to your Gmail inbox:\n\nVerification Code: ${generatedVerificationCode}\n\nEnter this code on the screen to reset your password.`);

      document.getElementById('forgotStep1').style.display = 'none';
      document.getElementById('forgotStep2').style.display = 'flex';
      document.getElementById('verifyCodeInput').value = '';
      document.getElementById('newResetPassword').value = '';
    }

    function verifyCodeAndResetPassword() {
      const enteredCode = document.getElementById('verifyCodeInput').value.trim();
      const newPass = document.getElementById('newResetPassword').value;

      if (enteredCode !== generatedVerificationCode) {
        alert("Invalid verification code! Please check your Gmail app and enter the exact 6 digits.");
        return;
      }

      if (newPass.length < 5) {
        alert("Password must be at least 5 characters long.");
        return;
      }

      // Update password
      const user = usersList.find(u => u.email.toLowerCase() === pendingResetEmail);
      if (user) {
        user.password = newPass;
      }

      alert("Password reset successfully! You can now log in with your new password.");
      openLoginModal();
      document.getElementById('loginEmailInput').value = pendingResetEmail;
    }

    // ADMIN DASHBOARD CONTROLS
    function openAdminDashboard() {
      document.getElementById('adminView').classList.add('active-admin');
      document.getElementById('mainHeader').style.display = 'none';
      document.getElementById('mainContainer').style.display = 'none';
      document.getElementById('floatingChatBtn').style.display = 'none';
      document.getElementById('mainBottomNav').style.display = 'none';
      window.scrollTo(0, 0);
    }

    function previewUserSite() {
      document.getElementById('adminView').classList.remove('active-admin');
      document.getElementById('mainHeader').style.display = 'flex';
      document.getElementById('mainContainer').style.display = 'flex';
      document.getElementById('floatingChatBtn').style.display = 'block';
      document.getElementById('mainBottomNav').style.display = 'flex';
      document.getElementById('headerBalanceDisplay').innerText = "ADMIN MODE";
    }

    function logoutAdmin() {
      document.getElementById('adminView').classList.remove('active-admin');
      document.getElementById('mainHeader').style.display = 'flex';
      document.getElementById('mainContainer').style.display = 'flex';
      document.getElementById('floatingChatBtn').style.display = 'block';
      document.getElementById('mainBottomNav').style.display = 'flex';
      logout();
    }

    function switchAdminTab(tabId, btn) {
      document.querySelectorAll('.admin-section').forEach(sec => sec.classList.remove('active-sec'));
      document.querySelectorAll('.admin-tab-btn').forEach(b => b.classList.remove('active'));
      document.getElementById(tabId).classList.add('active-sec');
      btn.classList.add('active');
    }

    function renderAdminUsers() {
      const container = document.getElementById('usersListContainer');
      document.getElementById('userCountStatus').innerText = `Active: ${usersList.length}`;
      document.getElementById('metricTotalUsers').innerText = (12890 + usersList.length).toLocaleString();

      container.innerHTML = usersList.map(u => `
        <div class="admin-user-row">
          <div>
            <div style="font-weight:700; color:#fff; display:flex; align-items:center; gap:6px;">
              ${u.name} ${u.country}
              ${u.online ? '<span class="live-pulse"></span>' : ''}
            </div>
            <div style="font-size:11px; color:var(--text-muted);">${u.email} &bull; ${u.phone}</div>
            <div style="font-size:10px; margin-top:2px;">Status: <b style="color:${u.banned ? 'var(--danger)' : '#00e676'}">${u.banned ? 'BANNED' : 'ACTIVE'}</b></div>
          </div>
          <div>
            ${u.banned ? 
              `<button class="btn-unban" onclick="toggleBanUser(${u.id})">Unban</button>` : 
              `<button class="btn-ban" onclick="toggleBanUser(${u.id})">Ban</button>`
            }
          </div>
        </div>
      `).join('');
    }

    function toggleBanUser(userId) {
      const user = usersList.find(u => u.id === userId);
      if (user) {
        user.banned = !user.banned;
        renderAdminUsers();
        alert(`User ${user.name} has been ${user.banned ? 'BANNED.' : 'UNBANNED.'}`);
      }
    }

    function renderAdminMatches() {
      const container = document.getElementById('adminMatchEditorList');
      container.innerHTML = liveMatches.map(m => `
        <div class="match-edit-box">
          <div style="display:flex; justify-content:space-between; font-weight:700; font-size:13px;">
            <span>${m.team1} vs ${m.team2} (${m.league})</span>
            <span style="color:#ff334b;">${m.minute}'</span>
          </div>
          <div style="display:grid; grid-template-columns:1fr 1fr; gap:6px;">
            <input type="number" class="odds-input" value="${m.score1}" onchange="updateMatchScore(${m.id}, 1, this.value)" placeholder="${m.team1}" />
            <input type="number" class="odds-input" value="${m.score2}" onchange="updateMatchScore(${m.id}, 2, this.value)" placeholder="${m.team2}" />
          </div>
          <div class="odds-inputs-row">
            <input type="number" step="0.01" class="odds-input" value="${m.odd1}" onchange="updateMatchOdd(${m.id}, 'odd1', this.value)" />
            <input type="number" step="0.01" class="odds-input" value="${m.oddX}" onchange="updateMatchOdd(${m.id}, 'oddX', this.value)" />
            <input type="number" step="0.01" class="odds-input" value="${m.odd2}" onchange="updateMatchOdd(${m.id}, 'odd2', this.value)" />
          </div>
        </div>
      `).join('');
      document.getElementById('metricActiveMatches').innerText = liveMatches.length;
    }

    function updateMatchScore(matchId, teamIndex, val) {
      const m = liveMatches.find(item => item.id === matchId);
      if (m) {
        if (teamIndex === 1) m.score1 = parseInt(val) || 0;
        else m.score2 = parseInt(val) || 0;
        renderUserMatches();
      }
    }

    function updateMatchOdd(matchId, oddKey, val) {
      const m = liveMatches.find(item => item.id === matchId);
      if (m) {
        m[oddKey] = parseFloat(val) || 1.0;
        renderUserMatches();
      }
    }

    function submitNewVideoMatch() {
      const league = document.getElementById('newMatchLeague').value;
      const teams = document.getElementById('newMatchTeams').value.split('vs');
      const videoUrl = document.getElementById('newMatchVideoUrl').value;
      const odd1 = parseFloat(document.getElementById('newOdd1').value) || 1.85;
      const oddX = parseFloat(document.getElementById('newOddX').value) || 3.40;
      const odd2 = parseFloat(document.getElementById('newOdd2').value) || 4.20;

      const newMatch = {
        id: liveMatches.length + 1,
        league: league,
        team1: teams[0] ? teams[0].trim() : "Team 1",
        team2: teams[1] ? teams[1].trim() : "Team 2",
        score1: 0,
        score2: 0,
        minute: 1,
        odd1: odd1,
        oddX: oddX,
        odd2: odd2,
        videoUrl: videoUrl
      };

      liveMatches.unshift(newMatch);
      renderUserMatches();
      renderAdminMatches();
      alert(`Video Match added and live broadcast embedded!`);
      switchAdminTab('editMatchesTab', document.querySelectorAll('.admin-tab-btn')[1]);
    }

    function renderTrafficLogs() {
      const container = document.getElementById('trafficLogsContainer');
      container.innerHTML = trafficLogs.map(l => `
        <div style="background:#081b12; border:1px solid var(--border); border-radius:8px; padding:8px 10px; font-size:12px; display:flex; justify-content:space-between; align-items:center;">
          <div>
            <div style="font-weight:700;">${l.flag} ${l.user} <span style="font-weight:400; color:var(--text-muted); font-size:10px;">(${l.ip})</span></div>
            <div style="color:var(--primary); font-size:11px;">${l.action}</div>
          </div>
          <div style="font-size:10px; color:var(--text-muted);">${l.time}</div>
        </div>
      `).join('');
    }

    function switchMainView(view) {
      document.querySelectorAll('.view-panel').forEach(p => p.classList.remove('active-view'));
      document.getElementById('tabNavBets').classList.toggle('active', view === 'sports');
      document.getElementById('tabNavCasino').classList.toggle('active', view === 'casino');
      if (view === 'casino') {
        document.getElementById('casinoView').classList.add('active-view');
      } else {
        document.getElementById('sportsView').classList.add('active-view');
      }
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // MODALS CONTROLLER (STRICTLY ONE AT A TIME)
    function closeAllModals() {
      document.querySelectorAll('.modal-overlay').forEach(m => m.classList.remove('active'));
      document.body.style.overflow = 'auto';
    }
    function openModal(id) {
      closeAllModals();
      closeProfileDrawer();
      const el = document.getElementById(id);
      if (el) { el.classList.add('active'); document.body.style.overflow = 'hidden'; }
    }
    function closeOnOutside(e, id) {
      if (e.target.id === id) closeAllModals();
    }

    function openLoginModal() { openModal('loginModal'); }
    function openSignupModal() { openModal('signupModal'); }
    function openWithdrawModal() { openModal('withdrawModal'); }
    function openDepositModal() { openModal('depositModal'); }
    function openSettingsModal() { openModal('settingsModal'); }

    // DRAWER CONTROLS
    function openProfileDrawer() {
      closeAllModals();
      document.getElementById('profileDrawerOverlay').classList.add('active');
      document.body.style.overflow = 'hidden';
    }
    function closeProfileDrawer() {
      document.getElementById('profileDrawerOverlay').classList.remove('active');
      document.body.style.overflow = 'auto';
    }
    function closeProfileDrawerOnOutside(e) {
      if (e.target.id === 'profileDrawerOverlay') closeProfileDrawer();
    }

    function completeAuth() {
      closeAllModals();
      document.getElementById('loggedOutView').style.display = 'none';
      document.getElementById('loggedInView').style.display = 'flex';
    }
    function logout() {
      closeProfileDrawer();
      closeAllModals();
      document.getElementById('loggedInView').style.display = 'none';
      document.getElementById('loggedOutView').style.display = 'flex';
    }

    function setRegistrationMode(mode) {
      const isQuick = mode === 'quick';
      document.getElementById('tabQuick').classList.toggle('active', isQuick);
      document.getElementById('tabDefault').classList.toggle('active', !isQuick);
      document.querySelectorAll('.default-field').forEach(el => el.classList.toggle('hidden-in-quick', isQuick));
    }

    // PAYMENT LOGIC
    function selectPaymentMethod(m) {
      selectedMethod = m;
      document.getElementById('methodMTN').classList.toggle('selected', m === 'mtn');
      document.getElementById('methodAirtel').classList.toggle('selected', m === 'airtel');
      document.getElementById('depositPhoneInput').placeholder = m === 'mtn' ? '770 123-456 (MTN)' : '750 123-456 (Airtel)';
    }

    function setPreset(amt, el) {
      document.querySelectorAll('.preset-chip').forEach(c => c.classList.remove('active'));
      el.classList.add('active');
      document.getElementById('depositAmountInput').value = amt;
      document.getElementById('depositSubmitBtn').innerText = `Deposit ${amt.toLocaleString()} USh`;
    }

    function processDeposit() {
      const amt = parseInt(document.getElementById('depositAmountInput').value) || 10000;
      const phone = document.getElementById('depositPhoneInput').value;
      const brand = selectedMethod === 'mtn' ? 'MTN MoMo' : 'Airtel Money';

      alert(`[${brand} Prompt Sent]\nEnter your PIN on phone +256 ${phone} to complete deposit of ${amt.toLocaleString()} USh.`);
      currentBalance += amt;
      const fmt = `${currentBalance.toLocaleString()} USh`;
      document.getElementById('headerBalanceDisplay').innerText = fmt;
      document.getElementById('drawerBalanceDisplay').innerText = fmt;
      closeAllModals();
    }

    function processWithdrawal() {
      const amt = parseInt(document.getElementById('withdrawAmountInput').value) || 0;
      const acc = document.getElementById('withdrawAccountInput').value;
      const sys = document.getElementById('withdrawSystemSelect').value;

      if (amt > currentBalance) {
        alert(`Insufficient balance! Your current balance is ${currentBalance.toLocaleString()} USh.`);
        return;
      }

      currentBalance -= amt;
      const fmt = `${currentBalance.toLocaleString()} USh`;
      document.getElementById('headerBalanceDisplay').innerText = fmt;
      document.getElementById('drawerBalanceDisplay').innerText = fmt;

      alert(`Withdrawal request of ${amt.toLocaleString()} USh via ${sys.toUpperCase()} (Account: ${acc}) submitted successfully!`);
      closeAllModals();
    }
  </script>
</body>
</html>
