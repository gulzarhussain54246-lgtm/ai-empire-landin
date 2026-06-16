```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>AI Empire — The Autonomous AI Workforce Platform</title>
<meta name="description" content="AI Empire is the all-in-one platform where autonomous AI agents run your business, content, marketing, design, and development — automatically." />

<script src="https://cdn.tailwindcss.com"></script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

<style>
  :root {
    --bg-0: #04040a;
    --bg-1: #08081a;
    --bg-2: #0d0d24;
    --surface: rgba(255,255,255,0.04);
    --border: rgba(255,255,255,0.08);
    --text: #f5f5ff;
    --muted: #9a9ab5;
    --cyan: #00e5ff;
    --violet: #a855f7;
    --pink: #ec4899;
    --emerald: #10f5b0;
    --amber: #fbbf24;
  }

  * { -webkit-font-smoothing: antialiased; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg-0);
    color: var(--text);
    font-family: 'Inter', system-ui, sans-serif;
    overflow-x: hidden;
  }

  .font-display { font-family: 'Space Grotesk', sans-serif; }
  .font-mono { font-family: 'JetBrains Mono', monospace; }

  /* Background canvas */
  #neural-bg {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    opacity: 0.55;
  }

  /* Gradient orbs */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.5;
    pointer-events: none;
    z-index: 1;
  }

  /* Glass card */
  .glass {
    background: linear-gradient(135deg, rgba(255,255,255,0.06), rgba(255,255,255,0.02));
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255,255,255,0.08);
  }

  .glass-strong {
    background: linear-gradient(135deg, rgba(255,255,255,0.09), rgba(255,255,255,0.03));
    backdrop-filter: blur(24px);
    -webkit-backdrop-filter: blur(24px);
    border: 1px solid rgba(255,255,255,0.12);
  }

  /* Gradient text */
  .gradient-text {
    background: linear-gradient(135deg, #00e5ff 0%, #a855f7 50%, #ec4899 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .gradient-text-2 {
    background: linear-gradient(135deg, #10f5b0 0%, #00e5ff 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  /* Animated gradient border */
  .gradient-border {
    position: relative;
    background: var(--bg-1);
    border-radius: 24px;
  }
  .gradient-border::before {
    content: '';
    position: absolute;
    inset: 0;
    padding: 1px;
    border-radius: inherit;
    background: linear-gradient(135deg, rgba(0,229,255,0.4), rgba(168,85,247,0.4), rgba(236,72,153,0.4));
    -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite: xor;
    mask-composite: exclude;
    pointer-events: none;
  }

  /* Glow button */
  .btn-glow {
    position: relative;
    background: linear-gradient(135deg, #00e5ff, #a855f7);
    color: #04040a;
    font-weight: 600;
    transition: all 0.3s ease;
    box-shadow: 0 0 0 0 rgba(0,229,255,0.5);
  }
  .btn-glow:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 40px -10px rgba(0,229,255,0.6), 0 10px 40px -10px rgba(168,85,247,0.5);
  }

  /* Feature card */
  .feature-card {
    position: relative;
    overflow: hidden;
    transition: transform 0.4s cubic-bezier(0.16,1,0.3,1), border-color 0.4s;
  }
  .feature-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(400px circle at var(--mx,50%) var(--my,50%), rgba(0,229,255,0.12), transparent 40%);
    opacity: 0;
    transition: opacity 0.4s;
    pointer-events: none;
  }
  .feature-card:hover::after { opacity: 1; }
  .feature-card:hover {
    transform: translateY(-6px);
    border-color: rgba(0,229,255,0.3);
  }

  /* Floating animation */
  @keyframes float {
    0%,100% { transform: translateY(0) translateX(0); }
    50% { transform: translateY(-20px) translateX(10px); }
  }
  .float { animation: float 6s ease-in-out infinite; }
  .float-slow { animation: float 9s ease-in-out infinite; }
  .float-fast { animation: float 4s ease-in-out infinite; }

  /* Pulse ring */
  @keyframes pulse-ring {
    0% { transform: scale(0.8); opacity: 0.8; }
    100% { transform: scale(2.4); opacity: 0; }
  }
  .pulse-ring {
    animation: pulse-ring 2.5s cubic-bezier(0.215,0.61,0.355,1) infinite;
  }

  /* Marquee */
  @keyframes marquee {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }
  .marquee-track { animation: marquee 40s linear infinite; }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.9s cubic-bezier(0.16,1,0.3,1), transform 0.9s cubic-bezier(0.16,1,0.3,1);
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Animated grid background */
  .grid-bg {
    background-image:
      linear-gradient(rgba(168,85,247,0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(168,85,247,0.07) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 80% 60% at 50% 0%, #000 30%, transparent 80%);
    -webkit-mask-image: radial-gradient(ellipse 80% 60% at 50% 0%, #000 30%, transparent 80%);
  }

  /* Shimmer */
  @keyframes shimmer {
    0% { background-position: -200% 0; }
    100% { background-position: 200% 0; }
  }
  .shimmer {
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.08), transparent);
    background-size: 200% 100%;
    animation: shimmer 3s linear infinite;
  }

  /* Animated bar chart */
  @keyframes barRise {
    from { height: 0; }
  }
  .bar { animation: barRise 1.2s cubic-bezier(0.16,1,0.3,1) forwards; }

  /* Nav link */
  .nav-link {
    position: relative;
    color: var(--muted);
    transition: color 0.3s;
  }
  .nav-link:hover { color: var(--text); }
  .nav-link::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: linear-gradient(90deg, var(--cyan), var(--violet));
    transition: width 0.3s;
  }
  .nav-link:hover::after { width: 100%; }

  /* Spinner orbit */
  @keyframes orbit {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  .orbit-1 { animation: orbit 20s linear infinite; }
  .orbit-2 { animation: orbit 30s linear infinite reverse; }
  .orbit-3 { animation: orbit 40s linear infinite; }

  /* Pricing highlight */
  .pricing-popular {
    background: linear-gradient(180deg, rgba(168,85,247,0.15), rgba(0,229,255,0.05));
    border: 1px solid rgba(168,85,247,0.4);
    box-shadow: 0 20px 60px -20px rgba(168,85,247,0.4);
  }

  /* Status dot */
  .status-dot {
    position: relative;
    width: 8px; height: 8px;
    border-radius: 50%;
    background: #10f5b0;
  }
  .status-dot::before {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    background: #10f5b0;
    opacity: 0.4;
    animation: pulse-ring 2s ease-out infinite;
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 10px; }
  ::-webkit-scrollbar-track { background: var(--bg-0); }
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(180deg, #00e5ff, #a855f7);
    border-radius: 10px;
  }

  /* Mobile menu */
  .mobile-menu {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.5s ease;
  }
  .mobile-menu.open { max-height: 500px; }

  /* Typing cursor */
  @keyframes blink { 50% { opacity: 0; } }
  .cursor { animation: blink 1s step-end infinite; }

  /* Number ticker */
  .ticker { font-variant-numeric: tabular-nums; }

  /* Glow ring around hero agent */
  .agent-ring {
    background: conic-gradient(from 0deg, #00e5ff, #a855f7, #ec4899, #10f5b0, #00e5ff);
    filter: blur(0.5px);
  }

  /* Section divider line */
  .divider-line {
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(168,85,247,0.4), transparent);
  }

  /* Wave animation for sound bars */
  @keyframes wave {
    0%,100% { transform: scaleY(0.3); }
    50% { transform: scaleY(1); }
  }
  .wave-bar { animation: wave 1s ease-in-out infinite; transform-origin: bottom; }

  /* Disable on touch */
  @media (hover: none) {
    .feature-card:hover { transform: none; }
  }
</style>
</head>
<body class="relative">

<!-- Neural network canvas background -->
<canvas id="neural-bg"></canvas>

<!-- Decorative orbs -->
<div class="orb" style="width:500px;height:500px;background:#a855f7;top:-100px;left:-100px;"></div>
<div class="orb" style="width:600px;height:600px;background:#00e5ff;top:30%;right:-200px;opacity:0.3;"></div>
<div class="orb" style="width:400px;height:400px;background:#ec4899;top:120%;left:20%;opacity:0.3;"></div>

<!-- ===== NAVBAR ===== -->
<nav class="fixed top-0 left-0 right-0 z-50 px-4 sm:px-6 lg:px-10 py-4">
  <div class="glass-strong rounded-2xl px-5 py-3 flex items-center justify-between max-w-7xl mx-auto">
    <a href="#" class="flex items-center gap-2.5">
      <div class="relative w-9 h-9 rounded-xl bg-gradient-to-br from-cyan-400 via-purple-500 to-pink-500 flex items-center justify-center">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#04040a" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
          <path d="M12 2L2 7l10 5 10-5-10-5z"/>
          <path d="M2 17l10 5 10-5"/>
          <path d="M2 12l10 5 10-5"/>
        </svg>
      </div>
      <span class="font-display font-bold text-xl tracking-tight">AI <span class="gradient-text">Empire</span></span>
    </a>

    <div class="hidden lg:flex items-center gap-8 text-sm font-medium">
      <a href="#features" class="nav-link">Platform</a>
      <a href="#agents" class="nav-link">AI Agents</a>
      <a href="#dashboard" class="nav-link">Dashboard</a>
      <a href="#pricing" class="nav-link">Pricing</a>
      <a href="#marketplace" class="nav-link">Marketplace</a>
    </div>

    <div class="hidden lg:flex items-center gap-3">
      <a href="#" class="text-sm font-medium text-gray-300 hover:text-white transition">Sign in</a>
      <a href="#pricing" class="btn-glow px-5 py-2.5 rounded-xl text-sm">Launch Empire →</a>
    </div>

    <button id="menuBtn" class="lg:hidden p-2 rounded-lg hover:bg-white/5 transition" aria-label="Menu">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round">
        <line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/>
      </svg>
    </button>
  </div>

  <div id="mobileMenu" class="mobile-menu lg:hidden mt-2 max-w-7xl mx-auto">
    <div class="glass-strong rounded-2xl p-5 flex flex-col gap-4 text-sm">
      <a href="#features" class="text-gray-300 hover:text-white">Platform</a>
      <a href="#agents" class="text-gray-300 hover:text-white">AI Agents</a>
      <a href="#dashboard" class="text-gray-300 hover:text-white">Dashboard</a>
      <a href="#pricing" class="text-gray-300 hover:text-white">Pricing</a>
      <a href="#marketplace" class="text-gray-300 hover:text-white">Marketplace</a>
      <a href="#pricing" class="btn-glow px-5 py-3 rounded-xl text-center text-sm font-semibold mt-2">Launch Empire →</a>
    </div>
  </div>
</nav>

<!-- ===== HERO ===== -->
<section class="relative z-10 pt-36 sm:pt-44 lg:pt-52 pb-20 px-4 sm:px-6 lg:px-10">
  <div class="grid-bg absolute inset-0 z-0"></div>

  <div class="relative max-w-7xl mx-auto grid lg:grid-cols-12 gap-12 items-center">

    <!-- Left content -->
    <div class="lg:col-span-7 text-center lg:text-left">
      <div class="inline-flex items-center gap-2 glass rounded-full px-4 py-1.5 mb-7 text-xs font-medium">
        <span class="status-dot"></span>
        <span class="text-gray-300">10 autonomous agents now live · v3.0</span>
      </div>

      <h1 class="font-display font-bold text-4xl sm:text-6xl lg:text-7xl leading-[1.05] tracking-tight">
        Deploy an army of<br>
        <span class="gradient-text">AI agents</span> that<br>
        run your entire<br>
        business <span class="relative inline-block">
          <span id="typed" class="gradient-text-2">autonomously</span><span class="cursor text-cyan-400">|</span>
        </span>
      </h1>

      <p class="mt-7 text-base sm:text-lg text-gray-400 max-w-xl mx-auto lg:mx-0 leading-relaxed">
        AI Empire is the all-in-one platform where autonomous agents handle content, video, social media, design, code, marketing and analytics — so you can scale a full digital company from a single dashboard.
      </p>

      <div class="mt-9 flex flex-col sm:flex-row gap-3 justify-center lg:justify-start">
        <a href="#pricing" class="btn-glow px-7 py-4 rounded-xl text-sm font-semibold inline-flex items-center justify-center gap-2">
          Start building free
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><path d="M5 12h14M13 5l7 7-7 7"/></svg>
        </a>
        <a href="#dashboard" class="glass px-7 py-4 rounded-xl text-sm font-semibold inline-flex items-center justify-center gap-2 hover:bg-white/10 transition">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M8 5v14l11-7z"/></svg>
          Watch live demo
        </a>
      </div>

      <div class="mt-10 flex flex-wrap items-center gap-x-8 gap-y-3 justify-center lg:justify-start text-xs text-gray-500">
        <div class="flex items-center gap-2">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#10f5b0" stroke-width="3" stroke-linecap="round"><polyline points="20 6 9 17 4 12"/></svg>
          No credit card required
        </div>
        <div class="flex items-center gap-2">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#10f5b0" stroke-width="3" stroke-linecap="round"><polyline points="20 6 9 17 4 12"/></svg>
          SOC-2 compliant
        </div>
        <div class="flex items-center gap-2">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#10f5b0" stroke-width="3" stroke-linecap="round"><polyline points="20 6 9 17 4 12"/></svg>
          Deploy in 5 minutes
        </div>
      </div>
    </div>

    <!-- Right visual -->
    <div class="lg:col-span-5 relative">
      <div class="relative w-full aspect-square max-w-md mx-auto">

        <!-- Outer orbit rings -->
        <div class="absolute inset-0 rounded-full border border-white/5 orbit-1">
          <div class="absolute -top-2 left-1/2 -translate-x-1/2 w-4 h-4 rounded-full bg-cyan-400 shadow-[0_0_20px_#00e5ff]"></div>
        </div>
        <div class="absolute inset-8 rounded-full border border-white/5 orbit-2">
          <div class="absolute top-1/2 -right-2 -translate-y-1/2 w-3 h-3 rounded-full bg-purple-400 shadow-[0_0_20px_#a855f7]"></div>
        </div>
        <div class="absolute inset-16 rounded-full border border-white/5 orbit-3">
          <div class="absolute -bottom-1.5 left-1/2 -translate-x-1/2 w-3 h-3 rounded-full bg-pink-400 shadow-[0_0_20px_#ec4899]"></div>
        </div>

        <!-- Center core -->
        <div class="absolute inset-1/4 rounded-full agent-ring opacity-40 blur-md float-slow"></div>
        <div class="absolute inset-1/4 rounded-full agent-ring float"></div>
        <div class="absolute inset-1/4 rounded-full glass-strong flex items-center justify-center">
          <div class="text-center">
            <div class="font-display font-bold text-3xl gradient-text">AE</div>
            <div class="text-[10px] text-gray-400 font-mono mt-1">CORE.v3</div>
          </div>
        </div>

        <!-- Floating mini agent chips -->
        <div class="absolute top-0 -left-4 glass-strong rounded-2xl p-3 float-fast shadow-xl">
          <div class="flex items-center gap-2">
            <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-pink-500 to-rose-500 flex items-center justify-center">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="white"><path d="M12 2l3 7h7l-5.5 4.5L18 21l-6-4-6 4 1.5-7.5L2 9h7z"/></svg>
            </div>
            <div>
              <div class="text-[10px] font-mono text-gray-400">CONTENT</div>
              <div class="text-xs font-semibold">+1,204 posts</div>
            </div>
          </div>
        </div>

        <div class="absolute bottom-8 -right-4 glass-strong rounded-2xl p-3 float shadow-xl">
          <div class="flex items-center gap-2">
            <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-cyan-400 to-blue-500 flex items-center justify-center">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="white"><path d="M12 2v20M2 7l10 5 10-5"/></svg>
            </div>
            <div>
              <div class="text-[10px] font-mono text-gray-400">REVENUE</div>
              <div class="text-xs font-semibold">$48.2K</div>
            </div>
          </div>
        </div>

        <div class="absolute top-1/2 -translate-y-1/2 -right-8 glass-strong rounded-2xl p-3 float-slow shadow-xl">
          <div class="flex items-center gap-2">
            <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-emerald-400 to-teal-500 flex items-center justify-center">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="white"><path d="M9 11l3 3L22 4M21 12v7a2 2 0 01-2 2H5a2 2 0 01-2-2V5a2 2 0 012-2h11"/></svg>
            </div>
            <div>
              <div class="text-[10px] font-mono text-gray-400">TASKS</div>
              <div class="text-xs font-semibold">312 done</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ===== TRUSTED BY MARQUEE ===== -->
<section class="relative z-10 py-10 border-y border-white/5 overflow-hidden">
  <div class="max-w-7xl mx-auto px-6 mb-6 text-center">
    <p class="text-xs uppercase tracking-[0.3em] text-gray-500 font-mono">Powering 12,000+ autonomous businesses</p>
  </div>
  <div class="overflow-hidden">
    <div class="marquee-track flex gap-16 whitespace-nowrap items-center">
      <!-- Logo set 1 -->
      <span class="font-display font-bold text-2xl text-gray-600">NEXUS</span>
      <span class="font-display font-bold text-2xl text-gray-600">Quantum<span class="text-cyan-500">.</span>io</span>
      <span class="font-display font-bold text-2xl text-gray-600">VERTEX</span>
      <span class="font-display font-bold text-2xl text-gray-600">Hyperloop</span>
      <span class="font-display font-bold text-2xl text-gray-600">Lumina</span>
      <span class="font-display font-bold text-2xl text-gray-600">Cobalt<span class="text-purple-500">.</span>ai</span>
      <span class="font-display font-bold text-2xl text-gray-600">PRISM</span>
      <span class="font-display font-bold text-2xl text-gray-600">Synthetix</span>
      <!-- duplicate for seamless loop -->
      <span class="font-display font-bold text-2xl text-gray-600">NEXUS</span>
      <span class="font-display font-bold text-2xl text-gray-600">Quantum<span class="text-cyan-500">.</span>io</span>
      <span class="font-display font-bold text-2xl text-gray-600">VERTEX</span>
      <span class="font-display font-bold text-2xl text-gray-600">Hyperloop</span>
      <span class="font-display font-bold text-2xl text-gray-600">Lumina</span>
      <span class="font-display font-bold text-2xl text-gray-600">Cobalt<span class="text-purple-500">.</span>ai</span>
      <span class="font-display font-bold text-2xl text-gray-600">PRISM</span>
      <span class="font-display font-bold text-2xl text-gray-600">Synthetix</span>
    </div>
  </div>
</section>

<!-- ==
