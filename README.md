<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nexus AI — Think Beyond</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #060608;
    --bg2: #0d0d12;
    --bg3: #13131a;
    --surface: #1a1a24;
    --surface2: #22222f;
    --border: rgba(255,255,255,0.07);
    --border2: rgba(255,255,255,0.12);
    --accent: #7b5ea7;
    --accent2: #a78bfa;
    --accent3: #c4b5fd;
    --glow: rgba(123,94,167,0.35);
    --text: #f0eeff;
    --text2: #9b9bb8;
    --text3: #5c5c7a;
    --green: #34d399;
    --radius: 14px;
    --radius-lg: 20px;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.6;
  }

  /* ── ANIMATED BG ORBS ── */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(90px);
    pointer-events: none;
    z-index: 0;
    animation: drift 18s ease-in-out infinite;
  }
  .orb1 { width: 500px; height: 500px; background: rgba(123,94,167,0.18); top: -150px; right: -100px; animation-delay: 0s; }
  .orb2 { width: 400px; height: 400px; background: rgba(52,211,153,0.08); bottom: -100px; left: -100px; animation-delay: -9s; }
  .orb3 { width: 300px; height: 300px; background: rgba(167,139,250,0.12); top: 50%; left: 50%; transform: translate(-50%,-50%); animation-delay: -4s; }

  @keyframes drift {
    0%,100% { transform: translate(0,0) scale(1); }
    33% { transform: translate(40px,-30px) scale(1.05); }
    66% { transform: translate(-30px,20px) scale(0.95); }
  }

  /* ── LAYOUT ── */
  .app { display: flex; height: 100vh; position: relative; z-index: 1; }

  /* ── SIDEBAR ── */
  .sidebar {
    width: 260px;
    background: rgba(13,13,18,0.85);
    backdrop-filter: blur(20px);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    padding: 0;
    flex-shrink: 0;
    transition: width 0.3s ease;
  }

  .sidebar-header {
    padding: 22px 20px 16px;
    border-bottom: 1px solid var(--border);
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
  }

  .logo-mark {
    width: 34px;
    height: 34px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
    box-shadow: 0 0 20px var(--glow);
    animation: pulse-glow 3s ease-in-out infinite;
  }

  @keyframes pulse-glow {
    0%,100% { box-shadow: 0 0 20px var(--glow); }
    50% { box-shadow: 0 0 35px rgba(123,94,167,0.55); }
  }

  .logo-text {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 18px;
    letter-spacing: -0.02em;
    color: var(--text);
  }
  .logo-text span { color: var(--accent2); }

  .new-chat-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    width: 100%;
    padding: 10px 14px;
    margin-top: 14px;
    background: rgba(123,94,167,0.15);
    border: 1px solid rgba(123,94,167,0.3);
    border-radius: var(--radius);
    color: var(--accent3);
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s;
  }
  .new-chat-btn:hover { background: rgba(123,94,167,0.25); border-color: rgba(123,94,167,0.5); }
  .new-chat-btn svg { width: 15px; height: 15px; }

  .sidebar-section { padding: 16px 14px 8px; }
  .sidebar-label {
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--text3);
    padding: 0 6px;
    margin-bottom: 6px;
  }

  .chat-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 9px 10px;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.15s;
    color: var(--text2);
    font-size: 13.5px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    border: 1px solid transparent;
  }
  .chat-item:hover { background: var(--surface); color: var(--text); }
  .chat-item.active { background: rgba(123,94,167,0.15); border-color: rgba(123,94,167,0.25); color: var(--text); }
  .chat-item-icon { font-size: 14px; flex-shrink: 0; opacity: 0.7; }

  .sidebar-footer {
    margin-top: auto;
    padding: 14px;
    border-top: 1px solid var(--border);
  }

  .user-card {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px;
    border-radius: 12px;
    cursor: pointer;
    transition: background 0.2s;
  }
  .user-card:hover { background: var(--surface); }
  .avatar {
    width: 34px;
    height: 34px;
    border-radius: 50%;
    background: linear-gradient(135deg, #7b5ea7, #34d399);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    font-weight: 600;
    flex-shrink: 0;
  }
  .user-info { flex: 1; min-width: 0; }
  .user-name { font-size: 13px; font-weight: 500; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .user-plan { font-size: 11px; color: var(--accent2); }

  /* ── MAIN AREA ── */
  .main {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    min-width: 0;
  }

  /* ── TOP BAR ── */
  .topbar {
    height: 58px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 24px;
    border-bottom: 1px solid var(--border);
    background: rgba(6,6,8,0.7);
    backdrop-filter: blur(20px);
    flex-shrink: 0;
  }

  .model-selector {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 7px 14px;
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: 100px;
    cursor: pointer;
    font-size: 13px;
    font-weight: 500;
    transition: all 0.2s;
    color: var(--text);
  }
  .model-selector:hover { border-color: rgba(123,94,167,0.5); }
  .model-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--green); box-shadow: 0 0 8px var(--green); flex-shrink: 0; animation: blink 2s ease-in-out infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.4} }

  .topbar-actions { display: flex; align-items: center; gap: 10px; }
  .icon-btn {
    width: 36px; height: 36px;
    border-radius: 10px;
    border: 1px solid var(--border);
    background: transparent;
    color: var(--text2);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; transition: all 0.2s;
    font-size: 15px;
  }
  .icon-btn:hover { background: var(--surface); color: var(--text); border-color: var(--border2); }

  /* ── CHAT AREA ── */
  .chat-scroll {
    flex: 1;
    overflow-y: auto;
    padding: 32px 0;
    scroll-behavior: smooth;
  }
  .chat-scroll::-webkit-scrollbar { width: 4px; }
  .chat-scroll::-webkit-scrollbar-thumb { background: var(--surface2); border-radius: 4px; }

  .chat-inner { max-width: 780px; margin: 0 auto; padding: 0 24px; }

  /* ── WELCOME SCREEN ── */
  .welcome {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 60vh;
    text-align: center;
    animation: fade-up 0.6s ease both;
  }

  @keyframes fade-up {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .welcome-icon {
    width: 72px; height: 72px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 22px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    margin-bottom: 24px;
    box-shadow: 0 0 50px rgba(123,94,167,0.4);
    animation: float 4s ease-in-out infinite;
  }
  @keyframes float {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }

  .welcome h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 4vw, 42px);
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1.1;
    margin-bottom: 12px;
  }
  .welcome h1 .grad {
    background: linear-gradient(135deg, var(--accent2), #c4b5fd, var(--green));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .welcome p {
    color: var(--text2);
    font-size: 16px;
    line-height: 1.6;
    max-width: 480px;
    margin-bottom: 36px;
  }

  .suggestions {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    width: 100%;
    max-width: 560px;
  }

  .suggestion-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 14px 16px;
    cursor: pointer;
    text-align: left;
    transition: all 0.2s;
    animation: fade-up 0.6s ease both;
  }
  .suggestion-card:nth-child(1) { animation-delay: 0.1s; }
  .suggestion-card:nth-child(2) { animation-delay: 0.15s; }
  .suggestion-card:nth-child(3) { animation-delay: 0.2s; }
  .suggestion-card:nth-child(4) { animation-delay: 0.25s; }

  .suggestion-card:hover {
    background: var(--surface2);
    border-color: rgba(123,94,167,0.4);
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(0,0,0,0.3);
  }
  .suggestion-icon { font-size: 18px; margin-bottom: 8px; }
  .suggestion-title { font-size: 13px; font-weight: 500; color: var(--text); margin-bottom: 3px; }
  .suggestion-sub { font-size: 12px; color: var(--text3); }

  /* ── MESSAGES ── */
  .message {
    display: flex;
    gap: 14px;
    margin-bottom: 28px;
    animation: fade-up 0.4s ease both;
  }

  .msg-avatar {
    width: 32px; height: 32px;
    border-radius: 10px;
    flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px;
    font-weight: 600;
    margin-top: 2px;
  }
  .msg-avatar.ai { background: linear-gradient(135deg, var(--accent), var(--accent2)); box-shadow: 0 0 16px var(--glow); }
  .msg-avatar.user { background: linear-gradient(135deg, #374151, #4b5563); }

  .msg-body { flex: 1; min-width: 0; }

  .msg-name {
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.02em;
    text-transform: uppercase;
    color: var(--text3);
    margin-bottom: 6px;
  }
  .msg-name.ai-name { color: var(--accent2); }

  .msg-content {
    font-size: 15px;
    line-height: 1.75;
    color: var(--text);
  }
  .msg-content p { margin-bottom: 12px; }
  .msg-content p:last-child { margin-bottom: 0; }

  .msg-content code {
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: 6px;
    padding: 2px 7px;
    font-family: 'Courier New', monospace;
    font-size: 13px;
    color: var(--accent3);
  }

  .msg-content pre {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 16px;
    overflow-x: auto;
    margin: 12px 0;
  }
  .msg-content pre code { background: none; border: none; padding: 0; font-size: 13px; color: var(--accent3); }

  /* ── TYPING INDICATOR ── */
  .typing-indicator {
    display: flex;
    gap: 14px;
    margin-bottom: 28px;
    animation: fade-up 0.3s ease both;
  }
  .typing-dots {
    display: flex;
    align-items: center;
    gap: 5px;
    padding: 10px 4px;
  }
  .typing-dots span {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--accent2);
    animation: typing-bounce 1.2s ease-in-out infinite;
  }
  .typing-dots span:nth-child(2) { animation-delay: 0.15s; }
  .typing-dots span:nth-child(3) { animation-delay: 0.3s; }
  @keyframes typing-bounce {
    0%,60%,100% { transform: translateY(0); opacity: 0.4; }
    30% { transform: translateY(-6px); opacity: 1; }
  }

  /* ── INPUT AREA ── */
  .input-area {
    padding: 16px 24px 20px;
    background: rgba(6,6,8,0.7);
    backdrop-filter: blur(20px);
    border-top: 1px solid var(--border);
    flex-shrink: 0;
  }

  .input-wrap {
    max-width: 780px;
    margin: 0 auto;
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: 18px;
    transition: border-color 0.2s, box-shadow 0.2s;
    overflow: hidden;
  }
  .input-wrap:focus-within {
    border-color: rgba(123,94,167,0.6);
    box-shadow: 0 0 0 3px rgba(123,94,167,0.1);
  }

  .input-row {
    display: flex;
    align-items: flex-end;
    padding: 6px 6px 6px 16px;
    gap: 8px;
  }

  textarea#chatInput {
    flex: 1;
    background: transparent;
    border: none;
    outline: none;
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.6;
    resize: none;
    min-height: 46px;
    max-height: 180px;
    padding: 10px 0;
  }
  textarea#chatInput::placeholder { color: var(--text3); }

  .send-btn {
    width: 40px; height: 40px;
    border-radius: 12px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border: none;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
    transition: all 0.2s;
    box-shadow: 0 4px 12px rgba(123,94,167,0.4);
    color: white;
  }
  .send-btn:hover { transform: scale(1.05); box-shadow: 0 6px 18px rgba(123,94,167,0.6); }
  .send-btn:active { transform: scale(0.95); }
  .send-btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }

  .input-footer {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 4px 14px 10px;
  }
  .input-action {
    display: flex; align-items: center; gap: 5px;
    padding: 5px 10px;
    border-radius: 8px;
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text3);
    font-size: 12px;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    transition: all 0.2s;
  }
  .input-action:hover { background: var(--surface2); color: var(--text2); border-color: var(--border2); }
  .input-disclaimer {
    margin-left: auto;
    font-size: 11px;
    color: var(--text3);
  }

  /* ── SCROLLBAR GLOBAL ── */
  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--surface2); border-radius: 4px; }

  /* ── RESPONSIVE ── */
  @media (max-width: 700px) {
    .sidebar { display: none; }
    .suggestions { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<div class="app">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-header">
      <a class="logo" href="#">
        <div class="logo-mark">✦</div>
        <div class="logo-text">Nexus<span>AI</span></div>
      </a>
      <button class="new-chat-btn" onclick="newChat()">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 5v14M5 12h14"/></svg>
        New conversation
      </button>
    </div>

    <div class="sidebar-section">
      <div class="sidebar-label">Recent</div>
      <div class="chat-item active" onclick="selectChat(this)">
        <span class="chat-item-icon">💬</span>
        <span>Getting started with Nexus</span>
      </div>
      <div class="chat-item" onclick="selectChat(this)">
        <span class="chat-item-icon">🧠</span>
        <span>AI architecture deep dive</span>
      </div>
      <div class="chat-item" onclick="selectChat(this)">
        <span class="chat-item-icon">✍️</span>
        <span>Write a landing page copy</span>
      </div>
      <div class="chat-item" onclick="selectChat(this)">
        <span class="chat-item-icon">🐍</span>
        <span>Python web scraping script</span>
      </div>
    </div>

    <div class="sidebar-section">
      <div class="sidebar-label">Yesterday</div>
      <div class="chat-item" onclick="selectChat(this)">
        <span class="chat-item-icon">📊</span>
        <span>Data analysis project</span>
      </div>
      <div class="chat-item" onclick="selectChat(this)">
        <span class="chat-item-icon">🎨</span>
        <span>Design system brainstorm</span>
      </div>
    </div>

    <div class="sidebar-footer">
      <div class="user-card">
        <div class="avatar">YO</div>
        <div class="user-info">
          <div class="user-name">You</div>
          <div class="user-plan">✦ Pro Plan</div>
        </div>
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#5c5c7a" stroke-width="2"><circle cx="12" cy="12" r="1"/><circle cx="19" cy="12" r="1"/><circle cx="5" cy="12" r="1"/></svg>
      </div>
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">

    <!-- TOP BAR -->
    <div class="topbar">
      <div class="model-selector">
        <div class="model-dot"></div>
        Nexus Ultra 3.5
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M6 9l6 6 6-6"/></svg>
      </div>
      <div class="topbar-actions">
        <button class="icon-btn" title="Search">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
        </button>
        <button class="icon-btn" title="Share">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/><line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/></svg>
        </button>
        <button class="icon-btn" title="Settings">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
        </button>
      </div>
    </div>

    <!-- CHAT SCROLL -->
    <div class="chat-scroll" id="chatScroll">
      <div class="chat-inner" id="chatInner">
        <!-- WELCOME -->
        <div class="welcome" id="welcome">
          <div class="welcome-icon">✦</div>
          <h1>What can I help you<br><span class="grad">think beyond</span> today?</h1>
          <p>Nexus AI combines deep reasoning, creative brilliance, and real-time knowledge to supercharge everything you do.</p>
          <div class="suggestions">
            <div class="suggestion-card" onclick="useSuggestion('Explain how transformers work in AI, with a simple analogy')">
              <div class="suggestion-icon">🧠</div>
              <div class="suggestion-title">How do transformers work?</div>
              <div class="suggestion-sub">Explain AI architecture</div>
            </div>
            <div class="suggestion-card" onclick="useSuggestion('Write a compelling landing page headline for a productivity app called TaskFlow')">
              <div class="suggestion-icon">✍️</div>
              <div class="suggestion-title">Write a landing page</div>
              <div class="suggestion-sub">Marketing copy in seconds</div>
            </div>
            <div class="suggestion-card" onclick="useSuggestion('Write a Python script that reads a CSV file and finds the top 5 most common values in each column')">
              <div class="suggestion-icon">💻</div>
              <div class="suggestion-title">Debug or write code</div>
              <div class="suggestion-sub">Any language, any problem</div>
            </div>
            <div class="suggestion-card" onclick="useSuggestion('Give me a 7-day plan to learn the basics of machine learning from scratch, assuming I know Python')">
              <div class="suggestion-icon">📚</div>
              <div class="suggestion-title">Build a learning plan</div>
              <div class="suggestion-sub">Structured roadmap for any topic</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- INPUT AREA -->
    <div class="input-area">
      <div class="input-wrap">
        <div class="input-row">
          <textarea id="chatInput" placeholder="Message Nexus AI..." rows="1" onkeydown="handleKey(event)" oninput="autoResize(this)"></textarea>
          <button class="send-btn" id="sendBtn" onclick="sendMessage()" title="Send">
            <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 19V5M5 12l7-7 7 7"/></svg>
          </button>
        </div>
        <div class="input-footer">
          <button class="input-action">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21.44 11.05l-9.19 9.19a6 6 0 0 1-8.49-8.49l9.19-9.19a4 4 0 0 1 5.66 5.66l-9.2 9.19a2 2 0 0 1-2.83-2.83l8.49-8.48"/></svg>
            Attach
          </button>
          <button class="input-action">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
            Persona
          </button>
          <span class="input-disclaimer">Nexus may make mistakes.</span>
        </div>
      </div>
    </div>

  </main>
</div>

<script>
const conversationHistory = [];
let isWaiting = false;

function autoResize(el) {
  el.style.height = 'auto';
  el.style.height = Math.min(el.scrollHeight, 180) + 'px';
}

function handleKey(e) {
  if (e.key === 'Enter' && !e.shiftKey) {
    e.preventDefault();
    sendMessage();
  }
}

function useSuggestion(text) {
  const input = document.getElementById('chatInput');
  input.value = text;
  autoResize(input);
  sendMessage();
}

function newChat() {
  document.querySelectorAll('.chat-item').forEach(i => i.classList.remove('active'));
  const inner = document.getElementById('chatInner');
  inner.innerHTML = `
    <div class="welcome" id="welcome">
      <div class="welcome-icon">✦</div>
      <h1>What can I help you<br><span class="grad">think beyond</span> today?</h1>
      <p>Nexus AI combines deep reasoning, creative brilliance, and real-time knowledge to supercharge everything you do.</p>
      <div class="suggestions">
        <div class="suggestion-card" onclick="useSuggestion('Explain how transformers work in AI, with a simple analogy')">
          <div class="suggestion-icon">🧠</div>
          <div class="suggestion-title">How do transformers work?</div>
          <div class="suggestion-sub">Explain AI architecture</div>
        </div>
        <div class="suggestion-card" onclick="useSuggestion('Write a compelling landing page headline for a productivity app called TaskFlow')">
          <div class="suggestion-icon">✍️</div>
          <div class="suggestion-title">Write a landing page</div>
          <div class="suggestion-sub">Marketing copy in seconds</div>
        </div>
        <div class="suggestion-card" onclick="useSuggestion('Write a Python script that reads a CSV file and finds the top 5 most common values in each column')">
          <div class="suggestion-icon">💻</div>
          <div class="suggestion-title">Debug or write code</div>
          <div class="suggestion-sub">Any language, any problem</div>
        </div>
        <div class="suggestion-card" onclick="useSuggestion('Give me a 7-day plan to learn the basics of machine learning from scratch, assuming I know Python')">
          <div class="suggestion-icon">📚</div>
          <div class="suggestion-title">Build a learning plan</div>
          <div class="suggestion-sub">Structured roadmap for any topic</div>
        </div>
      </div>
    </div>`;
  conversationHistory.length = 0;
}

function selectChat(el) {
  document.querySelectorAll('.chat-item').forEach(i => i.classList.remove('active'));
  el.classList.add('active');
}

async function sendMessage() {
  if (isWaiting) return;
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if (!text) return;

  const welcome = document.getElementById('welcome');
  if (welcome) welcome.remove();

  input.value = '';
  input.style.height = 'auto';
  isWaiting = true;
  document.getElementById('sendBtn').disabled = true;

  conversationHistory.push({ role: 'user', content: text });

  addMessage('user', 'You', text);
  const typingEl = addTyping();
  scrollToBottom();

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        system: "You are Nexus AI, an advanced, helpful, and thoughtful AI assistant. Be concise yet thorough. Format responses with clear structure when helpful. Keep a warm, confident tone.",
        messages: conversationHistory
      })
    });

    const data = await response.json();
    typingEl.remove();

    const reply = data.content?.map(b => b.text || '').join('') || "I'm sorry, I couldn't process that request. Please try again.";
    conversationHistory.push({ role: 'assistant', content: reply });
    addMessage('ai', 'Nexus AI', reply, true);

  } catch (err) {
    typingEl.remove();
    addMessage('ai', 'Nexus AI', 'Something went wrong. Please check your connection and try again.', true);
  }

  isWaiting = false;
  document.getElementById('sendBtn').disabled = false;
  scrollToBottom();
}

function addMessage(role, name, content, isAI = false) {
  const inner = document.getElementById('chatInner');
  const div = document.createElement('div');
  div.className = 'message';

  const initials = role === 'ai' ? '✦' : 'YO';
  const avatarClass = role === 'ai' ? 'ai' : 'user';
  const nameClass = isAI ? 'ai-name' : '';
  const formatted = formatContent(content);

  div.innerHTML = `
    <div class="msg-avatar ${avatarClass}">${initials}</div>
    <div class="msg-body">
      <div class="msg-name ${nameClass}">${name}</div>
      <div class="msg-content">${formatted}</div>
    </div>`;
  inner.appendChild(div);
}

function addTyping() {
  const inner = document.getElementById('chatInner');
  const div = document.createElement('div');
  div.className = 'typing-indicator';
  div.innerHTML = `
    <div class="msg-avatar ai">✦</div>
    <div class="msg-body">
      <div class="msg-name ai-name">Nexus AI</div>
      <div class="typing-dots"><span></span><span></span><span></span></div>
    </div>`;
  inner.appendChild(div);
  return div;
}

function formatContent(text) {
  text = text
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;');

  text = text.replace(/```(\w*)\n?([\s\S]*?)```/g, (_, lang, code) =>
    `<pre><code>${code.trim()}</code></pre>`);

  text = text.replace(/`([^`]+)`/g, '<code>$1</code>');
  text = text.replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>');
  text = text.replace(/\*(.+?)\*/g, '<em>$1</em>');

  text = text.split('\n\n').map(p => {
    p = p.trim();
    if (!p) return '';
    if (p.startsWith('<pre>')) return p;
    return `<p>${p.replace(/\n/g, '<br>')}</p>`;
  }).join('');

  return text;
}

function scrollToBottom() {
  const scroll = document.getElementById('chatScroll');
  setTimeout(() => scroll.scrollTop = scroll.scrollHeight, 50);
}
</script>
</body>
</html>
