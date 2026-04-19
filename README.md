# TERRANCE-APP
APP
[logitrack-app-prototype (1).html](https://github.com/user-attachments/files/26872113/logitrack-app-prototype.1.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>LogiTrack AI — App Prototype</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Syne:wght@700;800&display=swap" rel="stylesheet"/>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
:root{
  --charcoal:#333333;
  --orange:#CC5500;
  --orange-light:#E8703A;
  --cream:#FFFDD0;
  --cream-dark:#F5F0B0;
  --white:#FFFFFF;
  --muted:#888;
  --border:#E0DDD0;
  --dark:#1A1A1A;
  --success:#2ECC71;
  --mpesa:#4CAF50;
  --danger:#E74C3C;
  --card:#FFFFFF;
}
body{font-family:'Space Grotesk',sans-serif;background:#1A1A1A;min-height:100vh;display:flex;flex-direction:column;align-items:center;padding:40px 20px;}
h1{color:var(--cream);font-family:'Syne',sans-serif;font-size:28px;margin-bottom:6px;text-align:center;}
.subtitle{color:rgba(255,253,208,.5);font-size:14px;margin-bottom:32px;text-align:center;}

/* PHONE FRAME */
.phone-wrap{display:flex;gap:40px;align-items:flex-start;flex-wrap:wrap;justify-content:center;}
.phone{width:375px;height:812px;background:var(--cream);border-radius:48px;overflow:hidden;position:relative;box-shadow:0 40px 80px rgba(0,0,0,.6),inset 0 0 0 2px rgba(255,255,255,.1);flex-shrink:0;}
.phone::before{content:'';position:absolute;top:0;left:50%;transform:translateX(-50%);width:120px;height:32px;background:var(--dark);border-radius:0 0 20px 20px;z-index:10;}

/* SCREEN */
.screen{position:absolute;inset:0;overflow:hidden;display:none;flex-direction:column;}
.screen.active{display:flex;}

/* STATUS BAR */
.status-bar{height:44px;display:flex;align-items:flex-end;justify-content:space-between;padding:0 28px 8px;flex-shrink:0;font-size:12px;font-weight:600;}
.sb-time{color:var(--charcoal);}
.sb-icons{display:flex;gap:6px;align-items:center;color:var(--charcoal);}

/* ====== SPLASH SCREEN ====== */
#splash{background:var(--charcoal);}
#splash .status-bar .sb-time,.splash-sub{color:rgba(255,253,208,.7);}
#splash .status-bar .sb-icons{color:var(--cream);}
.splash-body{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px;}
.splash-logo{width:80px;height:80px;background:var(--orange);border-radius:24px;display:flex;align-items:center;justify-content:center;font-size:40px;margin-bottom:24px;}
.splash-title{font-family:'Syne',sans-serif;font-size:36px;color:var(--cream);font-weight:800;margin-bottom:8px;text-align:center;}
.splash-sub{font-size:14px;text-align:center;margin-bottom:48px;}
.splash-btn{width:100%;background:var(--orange);color:var(--white);border:none;padding:18px;border-radius:16px;font-family:'Space Grotesk',sans-serif;font-size:16px;font-weight:700;cursor:pointer;transition:opacity .2s;margin-bottom:12px;}
.splash-btn:hover{opacity:.9;}
.splash-btn.outline{background:transparent;border:2px solid rgba(255,253,208,.3);color:var(--cream);}
.splash-tag{margin-top:32px;font-size:11px;color:rgba(255,253,208,.3);letter-spacing:2px;}

/* ====== NAV BAR ====== */
.bottom-nav{height:80px;background:var(--white);border-top:1px solid var(--border);display:flex;align-items:center;justify-content:space-around;padding:0 8px;padding-bottom:8px;flex-shrink:0;}
.nav-item{display:flex;flex-direction:column;align-items:center;gap:4px;cursor:pointer;padding:8px 12px;border-radius:12px;transition:background .2s;flex:1;}
.nav-item:hover{background:var(--cream);}
.nav-item.active{background:var(--cream);}
.nav-icon{font-size:22px;}
.nav-label{font-size:10px;font-weight:600;color:var(--muted);letter-spacing:.5px;}
.nav-item.active .nav-label{color:var(--orange);}

/* ====== HEADER ====== */
.app-header{padding:52px 24px 16px;background:var(--charcoal);flex-shrink:0;}
.header-row{display:flex;align-items:center;justify-content:space-between;}
.header-greet{font-size:13px;color:rgba(255,253,208,.6);}
.header-name{font-family:'Syne',sans-serif;font-size:22px;color:var(--cream);font-weight:800;}
.header-avatar{width:44px;height:44px;border-radius:50%;background:var(--orange);display:flex;align-items:center;justify-content:center;font-size:18px;cursor:pointer;}
.header-badge{margin-top:16px;background:rgba(204,85,0,.2);border:1px solid rgba(204,85,0,.4);border-radius:12px;padding:12px 16px;display:flex;align-items:center;gap:12px;}
.badge-dot{width:8px;height:8px;background:var(--success);border-radius:50%;animation:pulse 2s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
.badge-text{font-size:13px;color:var(--cream);}
.badge-text strong{color:var(--orange);}

/* SCROLLABLE CONTENT */
.scroll-area{flex:1;overflow-y:auto;background:var(--cream);}
.scroll-area::-webkit-scrollbar{display:none;}

/* STAT CARDS */
.stats-row{display:flex;gap:12px;padding:20px 20px 0;}
.stat-card{flex:1;background:var(--white);border-radius:16px;padding:16px;border:1px solid var(--border);}
.stat-val{font-family:'Syne',sans-serif;font-size:24px;font-weight:800;color:var(--charcoal);}
.stat-label{font-size:11px;color:var(--muted);margin-top:2px;}
.stat-trend{font-size:11px;color:var(--success);font-weight:600;margin-top:4px;}

/* SECTION TITLE */
.sec-title{font-size:13px;font-weight:700;color:var(--charcoal);letter-spacing:1px;padding:20px 20px 12px;}

/* MAP CARD */
.map-card{margin:0 20px;background:var(--charcoal);border-radius:20px;overflow:hidden;height:200px;position:relative;cursor:pointer;}
.map-grid{position:absolute;inset:0;opacity:.15;}
.map-road-h{position:absolute;left:0;right:0;height:2px;background:rgba(255,253,208,.4);}
.map-road-v{position:absolute;top:0;bottom:0;width:2px;background:rgba(255,253,208,.4);}
.map-overlay{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:flex-end;padding:16px;}
.map-lorry{position:absolute;font-size:28px;animation:drive 6s ease-in-out infinite;}
.map-lorry:nth-child(1){top:30%;left:20%;animation-delay:0s;}
.map-lorry:nth-child(2){top:55%;left:55%;animation-delay:2s;}
.map-lorry:nth-child(3){top:20%;left:65%;animation-delay:4s;}
@keyframes drive{0%,100%{transform:translateX(0)}50%{transform:translateX(20px)}}
.map-route{position:absolute;top:35%;left:22%;width:140px;height:2px;background:var(--orange);opacity:.7;}
.map-route::after{content:'';position:absolute;right:-6px;top:-5px;border:6px solid transparent;border-left:10px solid var(--orange);}
.map-info{background:rgba(0,0,0,.6);border-radius:10px;padding:8px 12px;backdrop-filter:blur(4px);}
.map-info-title{color:var(--cream);font-size:12px;font-weight:600;}
.map-info-sub{color:var(--orange);font-size:11px;}

/* ORDER CARDS */
.order-card{background:var(--white);border-radius:16px;margin:0 20px 12px;padding:16px;border:1px solid var(--border);cursor:pointer;transition:transform .2s;}
.order-card:hover{transform:translateX(4px);}
.order-top{display:flex;align-items:center;gap:12px;margin-bottom:10px;}
.order-icon{width:44px;height:44px;border-radius:12px;background:var(--cream);display:flex;align-items:center;justify-content:center;font-size:22px;}
.order-id{font-size:13px;font-weight:700;color:var(--charcoal);}
.order-route{font-size:11px;color:var(--muted);margin-top:2px;}
.order-status{margin-left:auto;padding:4px 10px;border-radius:20px;font-size:11px;font-weight:700;}
.status-transit{background:#FFF3E0;color:#E65100;}
.status-delivered{background:#E8F5E9;color:#2E7D32;}
.status-pending{background:#F3E5F5;color:#6A1B9A;}
.order-progress{height:4px;background:var(--cream-dark);border-radius:2px;margin-top:8px;}
.order-prog-fill{height:100%;border-radius:2px;background:var(--orange);}
.order-meta{display:flex;justify-content:space-between;margin-top:8px;font-size:11px;color:var(--muted);}

/* ====== QR SCREEN ====== */
#qr-screen .scroll-area{display:flex;flex-direction:column;align-items:center;padding:24px 20px;}
.qr-header{text-align:center;margin-bottom:24px;}
.qr-header h2{font-family:'Syne',sans-serif;font-size:22px;color:var(--charcoal);}
.qr-header p{font-size:13px;color:var(--muted);margin-top:4px;}
.qr-box{width:240px;height:240px;border:3px solid var(--charcoal);border-radius:20px;display:flex;align-items:center;justify-content:center;position:relative;background:var(--white);}
.qr-corner{position:absolute;width:24px;height:24px;border-color:var(--orange);border-style:solid;}
.qr-corner.tl{top:-3px;left:-3px;border-width:4px 0 0 4px;border-radius:4px 0 0 0;}
.qr-corner.tr{top:-3px;right:-3px;border-width:4px 4px 0 0;border-radius:0 4px 0 0;}
.qr-corner.bl{bottom:-3px;left:-3px;border-width:0 0 4px 4px;border-radius:0 0 0 4px;}
.qr-corner.br{bottom:-3px;right:-3px;border-width:0 4px 4px 0;border-radius:0 0 4px 0;}
.qr-scan-line{position:absolute;left:10px;right:10px;height:2px;background:var(--orange);animation:scan 2s ease-in-out infinite;}
@keyframes scan{0%{top:20px;opacity:1}50%{top:210px;opacity:1}100%{top:20px;opacity:0}}
.qr-inner{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;padding:16px;}
.qr-cell{width:20px;height:20px;border-radius:2px;}
.qr-cell.b{background:var(--charcoal);}
.qr-cell.w{background:transparent;}
.qr-actions{width:100%;margin-top:24px;display:flex;flex-direction:column;gap:12px;}
.qr-btn{width:100%;padding:16px;border-radius:14px;border:none;font-family:'Space Grotesk',sans-serif;font-size:15px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;}
.qr-btn.primary{background:var(--orange);color:var(--white);}
.qr-btn.secondary{background:var(--white);color:var(--charcoal);border:2px solid var(--border);}
.qr-verify-card{width:100%;background:var(--white);border-radius:16px;padding:16px;border:1px solid var(--border);margin-top:8px;}
.qr-verify-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);font-size:13px;}
.qr-verify-row:last-child{border:none;}
.verify-icon{font-size:18px;}
.verify-label{color:var(--muted);flex:1;}
.verify-val{font-weight:600;color:var(--charcoal);}
.verify-status{font-size:11px;font-weight:700;padding:3px 8px;border-radius:8px;}
.verify-ok{background:#E8F5E9;color:#2E7D32;}
.verify-fail{background:#FFEBEE;color:#C62828;}

/* ====== DRIVER SCREEN ====== */
#driver-screen .app-header{background:var(--orange);}
#driver-screen .header-greet{color:rgba(255,255,255,.7);}
#driver-screen .header-name{color:var(--white);}
#driver-screen .badge-dot{background:var(--cream);}
#driver-screen .badge-text{color:rgba(255,255,255,.9);}
#driver-screen .badge-text strong{color:var(--cream);}
.driver-order{background:var(--white);margin:0 20px 12px;border-radius:16px;overflow:hidden;border:1px solid var(--border);}
.driver-order-head{padding:16px;background:var(--charcoal);display:flex;align-items:center;gap:12px;}
.driver-order-id{font-family:'Syne',sans-serif;font-size:18px;color:var(--cream);font-weight:800;}
.driver-order-status{margin-left:auto;background:var(--orange);color:var(--white);padding:4px 12px;border-radius:20px;font-size:12px;font-weight:700;}
.driver-order-body{padding:16px;}
.driver-row{display:flex;align-items:flex-start;gap:12px;margin-bottom:14px;}
.driver-row-icon{font-size:20px;margin-top:2px;}
.driver-row-label{font-size:11px;color:var(--muted);margin-bottom:2px;}
.driver-row-val{font-size:14px;font-weight:600;color:var(--charcoal);}
.driver-actions{padding:16px;display:flex;gap:10px;}
.driver-btn{flex:1;padding:12px;border-radius:12px;border:none;font-family:'Space Grotesk',sans-serif;font-size:13px;font-weight:700;cursor:pointer;}
.driver-btn.call{background:var(--success);color:var(--white);}
.driver-btn.scan{background:var(--orange);color:var(--white);}
.driver-btn.nav{background:var(--charcoal);color:var(--cream);}
.voice-btn{margin:0 20px;background:var(--charcoal);border-radius:16px;padding:20px;display:flex;align-items:center;gap:16px;cursor:pointer;margin-bottom:12px;}
.voice-icon{width:48px;height:48px;background:var(--orange);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:24px;animation:voicePulse 2s ease-in-out infinite;}
@keyframes voicePulse{0%,100%{box-shadow:0 0 0 0 rgba(204,85,0,.4)}50%{box-shadow:0 0 0 12px rgba(204,85,0,0)}}
.voice-text{color:var(--cream);}
.voice-title{font-size:14px;font-weight:700;margin-bottom:4px;}
.voice-sub{font-size:12px;color:rgba(255,253,208,.5);}

/* ====== PAYMENTS SCREEN ====== */
.pay-summary{background:var(--charcoal);margin:0 20px 16px;border-radius:16px;padding:20px;}
.pay-total-label{font-size:12px;color:rgba(255,253,208,.5);letter-spacing:1px;}
.pay-total-val{font-family:'Syne',sans-serif;font-size:36px;color:var(--cream);font-weight:800;margin:4px 0;}
.pay-total-sub{font-size:12px;color:rgba(255,253,208,.4);}
.pay-status-row{display:flex;gap:8px;margin-top:16px;}
.pay-chip{padding:6px 12px;border-radius:20px;font-size:12px;font-weight:700;}
.chip-green{background:rgba(46,204,113,.2);color:#2ECC71;}
.chip-orange{background:rgba(204,85,0,.2);color:var(--orange);}
.chip-red{background:rgba(231,76,60,.2);color:var(--danger);}
.pay-card{background:var(--white);margin:0 20px 12px;border-radius:16px;padding:16px;border:1px solid var(--border);}
.pay-card-row{display:flex;align-items:center;gap:12px;margin-bottom:12px;}
.pay-card-icon{width:40px;height:40px;border-radius:10px;background:var(--cream);display:flex;align-items:center;justify-content:center;font-size:20px;}
.pay-card-info{flex:1;}
.pay-card-name{font-size:14px;font-weight:600;color:var(--charcoal);}
.pay-card-ref{font-size:11px;color:var(--muted);}
.pay-card-amount{font-family:'Syne',sans-serif;font-size:16px;font-weight:800;color:var(--charcoal);}
.pay-card-status{font-size:10px;font-weight:700;padding:3px 8px;border-radius:6px;}
.flag-row{background:#FFF3E0;border:1px solid #FFB74D;border-radius:12px;margin:0 20px 12px;padding:14px;display:flex;gap:12px;align-items:flex-start;}
.flag-icon{font-size:20px;flex-shrink:0;}
.flag-title{font-size:13px;font-weight:700;color:#E65100;margin-bottom:4px;}
.flag-desc{font-size:12px;color:#BF360C;line-height:1.5;}
.flag-btn{margin-top:8px;background:#E65100;color:var(--white);border:none;padding:6px 14px;border-radius:8px;font-size:12px;font-weight:700;cursor:pointer;}

/* NAV TABS */
.tabs{display:flex;background:var(--white);border-bottom:1px solid var(--border);flex-shrink:0;}
.tab{flex:1;padding:12px 8px;text-align:center;font-size:12px;font-weight:600;color:var(--muted);cursor:pointer;border-bottom:2px solid transparent;}
.tab.active{color:var(--orange);border-bottom-color:var(--orange);}

/* SCREEN SELECTOR */
.screen-selector{display:flex;gap:12px;margin-bottom:20px;flex-wrap:wrap;justify-content:center;}
.sel-btn{padding:10px 20px;border-radius:20px;border:2px solid rgba(255,253,208,.2);background:transparent;color:var(--cream);font-family:'Space Grotesk',sans-serif;font-size:13px;font-weight:600;cursor:pointer;transition:all .2s;}
.sel-btn.active,.sel-btn:hover{background:var(--orange);border-color:var(--orange);color:var(--white);}
</style>
</head>
<body>
<h1>LogiTrack AI — App Prototype</h1>
<p class="subtitle">Interactive mobile UI · Tap the screens to explore</p>

<div class="screen-selector">
  <button class="sel-btn active" onclick="showScreen('splash')">Splash</button>
  <button class="sel-btn" onclick="showScreen('dashboard')">Dashboard</button>
  <button class="sel-btn" onclick="showScreen('qr-screen')">QR Verify</button>
  <button class="sel-btn" onclick="showScreen('driver-screen')">Driver</button>
  <button class="sel-btn" onclick="showScreen('payments')">Payments</button>
</div>

<div class="phone-wrap">
<div class="phone">

<!-- SPLASH -->
<div class="screen active" id="splash">
  <div class="status-bar"><span class="sb-time">9:41</span><div class="sb-icons">▲▲▲ WiFi 🔋</div></div>
  <div class="splash-body">
    <div class="splash-logo">🚛</div>
    <div class="splash-title">LogiTrack AI</div>
    <div class="splash-sub">AI-powered mtumba logistics for Nairobi. Real-time tracking, QR handover, M-Pesa reconciliation.</div>
    <button class="splash-btn" onclick="showScreen('dashboard')">GET STARTED →</button>
    <button class="splash-btn outline" onclick="showScreen('dashboard')">SIGN IN</button>
    <div class="splash-tag">POWERED BY GEMINI AI + DARAJA API</div>
  </div>
</div>

<!-- DASHBOARD -->
<div class="screen" id="dashboard">
  <div class="app-header">
    <div class="status-bar" style="padding-top:0"><span class="sb-time" style="color:var(--cream)">9:41</span><div class="sb-icons" style="color:var(--cream)">▲▲▲ 🔋</div></div>
    <div class="header-row">
      <div><div class="header-greet">Good morning,</div><div class="header-name">Fleet Manager</div></div>
      <div class="header-avatar">👤</div>
    </div>
    <div class="header-badge">
      <div class="badge-dot"></div>
      <div class="badge-text"><strong>12 lorries</strong> active · AI re-routed 3 via Thika Rd bypass</div>
    </div>
  </div>
  <div class="scroll-area">
    <div class="stats-row">
      <div class="stat-card"><div class="stat-val">47</div><div class="stat-label">Active Orders</div><div class="stat-trend">↑ 8 today</div></div>
      <div class="stat-card"><div class="stat-val">98%</div><div class="stat-label">On-Time Rate</div><div class="stat-trend">↑ 2% vs last wk</div></div>
      <div class="stat-card"><div class="stat-val">2</div><div class="stat-label">Alerts</div><div class="stat-trend" style="color:var(--danger)">⚠ Review</div></div>
    </div>
    <div class="sec-title">LIVE FLEET MAP</div>
    <div class="map-card">
      <div style="position:absolute;inset:0;">
        <div class="map-road-h" style="top:35%"></div>
        <div class="map-road-h" style="top:60%"></div>
        <div class="map-road-v" style="left:30%"></div>
        <div class="map-road-v" style="left:65%"></div>
      </div>
      <div class="map-route"></div>
      <div class="map-lorry" style="top:30%;left:20%">🚛</div>
      <div class="map-lorry" style="top:52%;left:52%">🚛</div>
      <div class="map-lorry" style="top:22%;left:62%">🚛</div>
      <div class="map-overlay">
        <div class="map-info">
          <div class="map-info-title">📍 Gikomba → Westlands · ETA 14 min</div>
          <div class="map-info-sub">AI: Avoid Haile Selassie Ave — 23min delay detected</div>
        </div>
      </div>
    </div>
    <div class="sec-title">ACTIVE DELIVERIES</div>
    <div class="order-card" onclick="showScreen('driver-screen')">
      <div class="order-top">
        <div class="order-icon">📦</div>
        <div><div class="order-id">ORD-2847</div><div class="order-route">Gikomba → CBD, Moi Ave</div></div>
        <div class="order-status status-transit">IN TRANSIT</div>
      </div>
      <div class="order-progress"><div class="order-prog-fill" style="width:65%"></div></div>
      <div class="order-meta"><span>Driver: Kamau M.</span><span>ETA: 14 min</span></div>
    </div>
    <div class="order-card">
      <div class="order-top">
        <div class="order-icon">✅</div>
        <div><div class="order-id">ORD-2831</div><div class="order-route">Toi Market → Kasarani</div></div>
        <div class="order-status status-delivered">DELIVERED</div>
      </div>
      <div class="order-progress"><div class="order-prog-fill" style="width:100%;background:var(--success)"></div></div>
      <div class="order-meta"><span>Driver: Otieno K.</span><span>12:04 PM ✓</span></div>
    </div>
    <div class="order-card">
      <div class="order-top">
        <div class="order-icon">⏳</div>
        <div><div class="order-id">ORD-2851</div><div class="order-route">Gikomba → Ruiru</div></div>
        <div class="order-status status-pending">PENDING</div>
      </div>
      <div class="order-progress"><div class="order-prog-fill" style="width:10%"></div></div>
      <div class="order-meta"><span>Driver: Wanjiku A.</span><span>ETA: 2:30 PM</span></div>
    </div>
    <div style="height:20px"></div>
  </div>
  <div class="bottom-nav">
    <div class="nav-item active"><div class="nav-icon">🏠</div><div class="nav-label">HOME</div></div>
    <div class="nav-item" onclick="showScreen('qr-screen')"><div class="nav-icon">📷</div><div class="nav-label">QR SCAN</div></div>
    <div class="nav-item" onclick="showScreen('driver-screen')"><div class="nav-icon">🚛</div><div class="nav-label">FLEET</div></div>
    <div class="nav-item" onclick="showScreen('payments')"><div class="nav-icon">💳</div><div class="nav-label">PAYMENTS</div></div>
  </div>
</div>

<!-- QR SCREEN -->
<div class="screen" id="qr-screen">
  <div class="app-header" style="background:var(--charcoal)">
    <div class="status-bar" style="padding-top:0"><span class="sb-time" style="color:var(--cream)">9:41</span><div class="sb-icons" style="color:var(--cream)">▲▲▲ 🔋</div></div>
    <div class="header-row">
      <div><div class="header-greet">Trust Gateway</div><div class="header-name" style="font-size:18px">QR Verification</div></div>
      <div style="font-size:28px">🔐</div>
    </div>
  </div>
  <div class="tabs">
    <div class="tab active" onclick="setTab(this,'scan-tab')">SCAN QR</div>
    <div class="tab" onclick="setTab(this,'verify-tab')">VERIFY</div>
    <div class="tab" onclick="setTab(this,'history-tab')">HISTORY</div>
  </div>
  <div class="scroll-area" style="padding:20px">
    <div id="scan-tab">
      <div class="qr-header">
        <h2>Scan Buyer QR Code</h2>
        <p>Point camera at buyer's unique handover code</p>
      </div>
      <div style="display:flex;justify-content:center;margin-bottom:20px">
        <div class="qr-box">
          <div class="qr-corner tl"></div><div class="qr-corner tr"></div>
          <div class="qr-corner bl"></div><div class="qr-corner br"></div>
          <div class="qr-scan-line"></div>
          <div class="qr-inner">
            <!-- QR pattern -->
            <div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div>
            <div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div>
            <div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div>
            <div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div>
            <div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div>
            <div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell w"></div><div class="qr-cell b"></div>
            <div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell w"></div><div class="qr-cell b"></div><div class="qr-cell b"></div><div class="qr-cell b"></div>
          </div>
        </div>
      </div>
      <button class="qr-btn primary" onclick="showVerified()">🔍 SIMULATE SCAN & VERIFY</button>
      <button class="qr-btn secondary" style="margin-top:8px">✋ MANUAL ENTRY</button>
    </div>
    <div id="verify-tab" style="display:none">
      <div class="qr-header" style="margin-bottom:16px">
        <h2>✅ Scan Successful</h2>
        <p>Order ID: <strong>ORD-2847</strong> · Buyer: Brian M.</p>
      </div>
      <div class="qr-verify-card">
        <div class="qr-verify-row">
          <span class="verify-icon">📍</span>
          <span class="verify-label">GPS Match</span>
          <span class="verify-val">Within 18m</span>
          <span class="verify-status verify-ok">PASS</span>
        </div>
        <div class="qr-verify-row">
          <span class="verify-icon">🆔</span>
          <span class="verify-label">UUID Match</span>
          <span class="verify-val">Confirmed</span>
          <span class="verify-status verify-ok">PASS</span>
        </div>
        <div class="qr-verify-row">
          <span class="verify-icon">⏱</span>
          <span class="verify-label">Timestamp</span>
          <span class="verify-val">2:14 PM</span>
          <span class="verify-status verify-ok">VALID</span>
        </div>
        <div class="qr-verify-row">
          <span class="verify-icon">🌍</span>
          <span class="verify-label">Spoof Check</span>
          <span class="verify-val">No anomaly</span>
          <span class="verify-status verify-ok">CLEAR</span>
        </div>
      </div>
      <button class="qr-btn primary" style="margin-top:16px">✅ CONFIRM DELIVERY</button>
    </div>
    <div id="history-tab" style="display:none">
      <div class="order-card" style="margin:0 0 12px">
        <div class="order-top"><div class="order-icon">✅</div><div><div class="order-id">ORD-2831</div><div class="order-route">Verified 12:04 PM · GPS ✓ UUID ✓</div></div><div class="order-status status-delivered">OK</div></div>
      </div>
      <div class="order-card" style="margin:0 0 12px;border-left:3px solid var(--danger)">
        <div class="order-top"><div class="order-icon">🚨</div><div><div class="order-id">ORD-2799</div><div class="order-route">FLAGGED · GPS mismatch 5.2km</div></div><div class="order-status" style="background:#FFEBEE;color:#C62828">FRAUD</div></div>
      </div>
      <div class="order-card" style="margin:0">
        <div class="order-top"><div class="order-icon">✅</div><div><div class="order-id">ORD-2788</div><div class="order-route">Verified 10:22 AM · All checks passed</div></div><div class="order-status status-delivered">OK</div></div>
      </div>
    </div>
  </div>
  <div class="bottom-nav">
    <div class="nav-item" onclick="showScreen('dashboard')"><div class="nav-icon">🏠</div><div class="nav-label">HOME</div></div>
    <div class="nav-item active"><div class="nav-icon">📷</div><div class="nav-label">QR SCAN</div></div>
    <div class="nav-item" onclick="showScreen('driver-screen')"><div class="nav-icon">🚛</div><div class="nav-label">FLEET</div></div>
    <div class="nav-item" onclick="showScreen('payments')"><div class="nav-icon">💳</div><div class="nav-label">PAYMENTS</div></div>
  </div>
</div>

<!-- DRIVER SCREEN -->
<div class="screen" id="driver-screen">
  <div class="app-header">
    <div class="status-bar" style="padding-top:0"><span class="sb-time" style="color:var(--white)">9:41</span><div class="sb-icons" style="color:var(--white)">▲▲▲ 🔋</div></div>
    <div class="header-row">
      <div><div class="header-greet">Driver Companion</div><div class="header-name" style="color:var(--white);font-size:18px">Kamau Mwangi</div></div>
      <div class="header-avatar" style="background:var(--charcoal)">🚛</div>
    </div>
    <div class="header-badge" style="background:rgba(0,0,0,.2);border-color:rgba(0,0,0,.2)">
      <div class="badge-dot"></div>
      <div class="badge-text"><strong>Active shift</strong> · 6 deliveries today · KES 1,400 earned</div>
    </div>
  </div>
  <div class="scroll-area">
    <div class="voice-btn">
      <div class="voice-icon">🎙</div>
      <div class="voice-text">
        <div class="voice-title">AI Voice Companion</div>
        <div class="voice-sub">Tap to speak — "Report delay on Thika Road"</div>
      </div>
    </div>
    <div class="sec-title">CURRENT DELIVERY</div>
    <div class="driver-order">
      <div class="driver-order-head">
        <div>
          <div style="font-size:11px;color:rgba(255,253,208,.5);margin-bottom:2px">ORDER</div>
          <div class="driver-order-id">ORD-2847</div>
        </div>
        <div class="driver-order-status">IN TRANSIT</div>
      </div>
      <div class="driver-order-body">
        <div class="driver-row">
          <div class="driver-row-icon">📦</div>
          <div><div class="driver-row-label">PACKAGE</div><div class="driver-row-val">3x Blazers, 2x Shirts (Kg: 4.2)</div></div>
        </div>
        <div class="driver-row">
          <div class="driver-row-icon">📍</div>
          <div><div class="driver-row-label">DELIVER TO</div><div class="driver-row-val">Moi Ave, CBD — Near KCB Bank</div></div>
        </div>
        <div class="driver-row">
          <div class="driver-row-icon">👤</div>
          <div><div class="driver-row-label">BUYER</div><div class="driver-row-val">Brian M. · 0712 345 678</div></div>
        </div>
        <div class="driver-row" style="margin:0">
          <div class="driver-row-icon">⏱</div>
          <div><div class="driver-row-label">AI ETA</div><div class="driver-row-val" style="color:var(--orange)">14 minutes (recalculated)</div></div>
        </div>
      </div>
      <div class="driver-actions">
        <button class="driver-btn call">📞 CALL</button>
        <button class="driver-btn nav">🗺 NAV</button>
        <button class="driver-btn scan" onclick="showScreen('qr-screen')">📷 SCAN QR</button>
      </div>
    </div>
    <div class="sec-title">TODAY'S DELIVERIES</div>
    <div class="order-card" style="margin:0 20px 10px">
      <div class="order-top"><div class="order-icon">✅</div><div><div class="order-id">ORD-2831 · Kasarani</div><div class="order-route">Delivered 12:04 PM · QR ✓</div></div><div class="order-status status-delivered">DONE</div></div>
    </div>
    <div class="order-card" style="margin:0 20px 20px">
      <div class="order-top"><div class="order-icon">✅</div><div><div class="order-id">ORD-2820 · Westlands</div><div class="order-route">Delivered 10:30 AM · QR ✓</div></div><div class="order-status status-delivered">DONE</div></div>
    </div>
  </div>
  <div class="bottom-nav">
    <div class="nav-item" onclick="showScreen('dashboard')"><div class="nav-icon">🏠</div><div class="nav-label">HOME</div></div>
    <div class="nav-item" onclick="showScreen('qr-screen')"><div class="nav-icon">📷</div><div class="nav-label">QR SCAN</div></div>
    <div class="nav-item active"><div class="nav-icon">🚛</div><div class="nav-label">FLEET</div></div>
    <div class="nav-item" onclick="showScreen('payments')"><div class="nav-icon">💳</div><div class="nav-label">PAYMENTS</div></div>
  </div>
</div>

<!-- PAYMENTS -->
<div class="screen" id="payments">
  <div class="app-header" style="background:var(--charcoal)">
    <div class="status-bar" style="padding-top:0"><span class="sb-time" style="color:var(--cream)">9:41</span><div class="sb-icons" style="color:var(--cream)">▲▲▲ 🔋</div></div>
    <div class="header-row">
      <div><div class="header-greet">Payment Orchestrator</div><div class="header-name" style="font-size:18px">M-Pesa Dashboard</div></div>
      <div style="font-size:28px">💳</div>
    </div>
  </div>
  <div class="scroll-area">
    <div class="pay-summary">
      <div class="pay-total-label">TODAY'S COLLECTIONS</div>
      <div class="pay-total-val">KES 48,250</div>
      <div class="pay-total-sub">34 transactions · AI-reconciled via Daraja API</div>
      <div class="pay-status-row">
        <div class="pay-chip chip-green">✓ 31 Confirmed</div>
        <div class="pay-chip chip-orange">⏱ 2 Pending</div>
        <div class="pay-chip chip-red">⚠ 1 Flagged</div>
      </div>
    </div>
    <div class="flag-row">
      <div class="flag-icon">🚨</div>
      <div>
        <div class="flag-title">AI Anomaly Detected — ORD-2799</div>
        <div class="flag-desc">Payment of KES 1,200 received but QR scan occurred 5.2km from delivery address. Possible fraud. Auto-held pending review.</div>
        <button class="flag-btn">REVIEW NOW →</button>
      </div>
    </div>
    <div class="sec-title">RECENT TRANSACTIONS</div>
    <div class="pay-card">
      <div class="pay-card-row">
        <div class="pay-card-icon">🟢</div>
        <div class="pay-card-info"><div class="pay-card-name">ORD-2831 · Brian M.</div><div class="pay-card-ref">TXN: QGJ4X8N2 · M-Pesa</div></div>
        <div><div class="pay-card-amount">+1,450</div><div class="pay-card-status" style="background:#E8F5E9;color:#2E7D32">CONFIRMED</div></div>
      </div>
    </div>
    <div class="pay-card">
      <div class="pay-card-row">
        <div class="pay-card-icon">🟢</div>
        <div class="pay-card-info"><div class="pay-card-name">ORD-2820 · Sharon K.</div><div class="pay-card-ref">TXN: PLK9M3R7 · M-Pesa</div></div>
        <div><div class="pay-card-amount">+2,100</div><div class="pay-card-status" style="background:#E8F5E9;color:#2E7D32">CONFIRMED</div></div>
      </div>
    </div>
    <div class="pay-card">
      <div class="pay-card-row">
        <div class="pay-card-icon">⚠️</div>
        <div class="pay-card-info"><div class="pay-card-name">ORD-2799 · Unknown</div><div class="pay-card-ref">TXN: XQR2P5T1 · GPS MISMATCH</div></div>
        <div><div class="pay-card-amount" style="color:var(--danger)">+1,200</div><div class="pay-card-status" style="background:#FFEBEE;color:#C62828">FLAGGED</div></div>
      </div>
    </div>
    <div style="height:20px"></div>
  </div>
  <div class="bottom-nav">
    <div class="nav-item" onclick="showScreen('dashboard')"><div class="nav-icon">🏠</div><div class="nav-label">HOME</div></div>
    <div class="nav-item" onclick="showScreen('qr-screen')"><div class="nav-icon">📷</div><div class="nav-label">QR SCAN</div></div>
    <div class="nav-item" onclick="showScreen('driver-screen')"><div class="nav-icon">🚛</div><div class="nav-label">FLEET</div></div>
    <div class="nav-item active"><div class="nav-icon">💳</div><div class="nav-label">PAYMENTS</div></div>
  </div>
</div>

</div><!-- end phone -->
</div><!-- end phone-wrap -->

<script>
function showScreen(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  document.querySelectorAll('.sel-btn').forEach(b=>{
    b.classList.toggle('active', b.textContent.toLowerCase().includes(id.replace('-screen','').replace('qr-screen','qr').replace('payments','pay')));
  });
}
function setTab(el,tabId){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  document.querySelectorAll('#scan-tab,#verify-tab,#history-tab').forEach(t=>t.style.display='none');
  document.getElementById(tabId).style.display='block';
}
function showVerified(){
  setTab(document.querySelectorAll('.tab')[1],'verify-tab');
}
</script>
</body>
</html>
