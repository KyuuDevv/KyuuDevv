<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>KuroNeko | System Status</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700;800&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        mono: ['"JetBrains Mono"', 'monospace'],
                        display: ['"Space Grotesk"', 'sans-serif']
                    },
                    colors: {
                        'primary':   '#6366f1',
                        'secondary': '#818cf8',
                        'accent':    '#a78bfa',
                        'deep':      '#4338ca',
                        'base':      '#0d0f1a',
                        'card':      '#13162a',
                        'surface':   '#1a1d35',
                    },
                    animation: {
                        'blob': 'blob 8s infinite',
                        'fade-up': 'fadeUp 0.6s ease-out forwards',
                        'slide-in': 'slideIn 0.7s cubic-bezier(0.16,1,0.3,1) forwards',
                        'pulse-dot': 'pulseDot 2s ease-in-out infinite',
                    },
                    keyframes: {
                        blob: {
                            '0%':   { transform: 'translate(0px, 0px) scale(1)' },
                            '33%':  { transform: 'translate(30px, -50px) scale(1.1)' },
                            '66%':  { transform: 'translate(-20px, 20px) scale(0.9)' },
                            '100%': { transform: 'translate(0px, 0px) scale(1)' },
                        },
                        fadeUp:  { '0%': { opacity:'0', transform:'translateY(12px)' }, '100%': { opacity:'1', transform:'translateY(0)' } },
                        slideIn: { '0%': { opacity:'0', transform:'translateY(30px) scale(0.97)' }, '100%': { opacity:'1', transform:'translateY(0) scale(1)' } },
                        pulseDot:{ '0%,100%': { opacity:'1', transform:'scale(1)' }, '50%': { opacity:'0.5', transform:'scale(0.85)' } }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #0d0f1a;
            background-image:
                radial-gradient(ellipse at 15% 10%, rgba(99,102,241,0.12) 0%, transparent 45%),
                radial-gradient(ellipse at 85% 90%, rgba(167,139,250,0.10) 0%, transparent 45%);
        }
        .bg-grid-size { background-size: 32px 32px; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #1a1d35; border-radius: 3px; }

        .glass-card {
            background: rgba(19,22,42,0.80);
            backdrop-filter: blur(24px);
            -webkit-backdrop-filter: blur(24px);
        }
        .card-glow {
            box-shadow: 6px 6px 0px 0px #2d2f6e, 0 25px 50px -12px rgba(99,102,241,0.18);
        }
        .card-glow-sm {
            box-shadow: 4px 4px 0px 0px #2d2f6e, 0 10px 30px -8px rgba(99,102,241,0.15);
        }
        .header-bar {
            background: rgba(26,29,53,0.85);
            border-bottom: 1px solid rgba(99,102,241,0.18);
            backdrop-filter: blur(20px);
        }
        .soft-btn { position:relative; border:none; background:transparent; padding:0; cursor:pointer; user-select:none; outline:none; -webkit-tap-highlight-color:transparent; display:block; text-decoration:none; }
        .soft-btn__wrapper { position:relative; display:block; width:100%; height:100%; transform-style:preserve-3d; }
        .soft-btn__wrapper::before { content:''; position:absolute; left:0; right:0; bottom:0; height:calc(100% - var(--button-raise-level)); background:var(--side-color); border-radius:var(--radius); z-index:1; }
        .soft-btn__content { position:relative; width:100%; height:calc(100% - var(--button-raise-level)); background:var(--surface-color); color:var(--text-color); border-radius:var(--radius); display:flex; align-items:center; justify-content:center; transform:translateY(0); transition:transform var(--transform-speed) ease-out; z-index:2; border:var(--border-width) solid var(--border-color); }
        .soft-btn__inner { display:inline-flex; align-items:center; justify-content:center; gap:8px; z-index:4; width:100%; height:100%; pointer-events:none; }
        .soft-btn--active .soft-btn__content { transform:translateY(var(--press-inset)); }
        .variant-solid { --surface-color:#6366f1; --side-color:#4338ca; --text-color:#ffffff; --border-color:transparent; --button-raise-level:5px; --press-inset:4px; --transform-speed:160ms; --radius:10px; --border-width:0px; }

        .title-gradient {
            background: linear-gradient(135deg, #818cf8 0%, #a78bfa 50%, #c084fc 100%);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
        }
        .line-gradient { background: linear-gradient(90deg, transparent, rgba(99,102,241,0.5), #6366f1, rgba(99,102,241,0.5), transparent); }
        .dot-online { background: #6366f1; box-shadow: 0 0 8px 2px rgba(99,102,241,0.5); }
        .tag-badge { background: rgba(99,102,241,0.12); border: 1px solid rgba(99,102,241,0.25); color: #818cf8; }
        .footer-line { background-image: repeating-linear-gradient(90deg, rgba(99,102,241,0.3), rgba(99,102,241,0.3) 4px, transparent 4px, transparent 12px); height: 1px; }
        .stat-chip { background: rgba(99,102,241,0.1); border: 1px solid rgba(99,102,241,0.22); }
        .term-bg { background: #07091a; border: 1px solid rgba(99,102,241,0.25); }
        .term-header { background: #0d0f1a; border-bottom: 1px solid rgba(99,102,241,0.18); }
        #realtime-logs::-webkit-scrollbar { width: 4px; }
        #realtime-logs::-webkit-scrollbar-track { background: transparent; }
        #realtime-logs::-webkit-scrollbar-thumb { background: #1a1d35; border-radius: 2px; }
        .chart-line { stroke: #6366f1; stroke-width: 2; fill: none; filter: drop-shadow(0 0 4px rgba(99,102,241,0.5)); }
        .chart-fill { fill: url(#memGrad); opacity: 0.35; }
        .chart-dot { fill: #818cf8; filter: drop-shadow(0 0 4px rgba(99,102,241,0.8)); }
    </style>
</head>
<body class="min-h-screen font-mono text-slate-300 bg-grid-pattern bg-grid-size relative overflow-x-hidden">

    <!-- Blob BG -->
    <div class="fixed inset-0 pointer-events-none z-0 overflow-hidden">
        <div class="absolute top-5 left-1/5 w-72 h-72 bg-indigo-900/20 rounded-full mix-blend-screen filter blur-3xl opacity-60 animate-blob"></div>
        <div class="absolute bottom-10 right-1/4 w-64 h-64 bg-violet-900/20 rounded-full mix-blend-screen filter blur-3xl opacity-50 animate-blob" style="animation-delay:3s"></div>
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-80 h-80 bg-purple-900/10 rounded-full mix-blend-screen filter blur-3xl opacity-40 animate-blob" style="animation-delay:5s"></div>
    </div>

    <!-- Navbar -->
    <nav class="relative z-50 header-bar sticky top-0">
        <div class="max-w-3xl mx-auto px-4 h-14 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <a href="/docs" class="soft-btn variant-solid h-9 w-9 rounded-xl" style="--radius:10px;">
                    <span class="soft-btn__wrapper">
                        <span class="soft-btn__content">
                            <span class="soft-btn__inner">
                                <i class="fa-solid fa-arrow-left text-xs"></i>
                            </span>
                        </span>
                    </span>
                </a>
                <div>
                    <span class="font-display font-bold text-slate-100 text-sm tracking-tight">SYSTEM STATUS</span>
                    <span class="block text-[9px] text-indigo-400/70 font-mono tracking-widest -mt-0.5">SERVER MONITOR</span>
                </div>
            </div>
            <span class="tag-badge text-[9px] font-bold px-2.5 py-1 rounded-full tracking-wider flex items-center gap-1.5">
                <span class="w-1.5 h-1.5 rounded-full dot-online animate-pulse-dot"></span>
                <span>LIVE</span>
            </span>
        </div>
    </nav>

    <!-- Main -->
    <main class="relative z-10 max-w-3xl mx-auto px-4 py-6 flex flex-col gap-5 animate-slide-in">

        <!-- TOP STATS -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div class="glass-card border border-indigo-900/50 card-glow-sm rounded-2xl p-5 animate-fade-up" style="animation-delay:0.05s">
                <div class="flex items-center gap-3 mb-3">
                    <div class="w-9 h-9 rounded-xl bg-green-900/40 flex items-center justify-center">
                        <i class="fa-solid fa-clock text-green-400 text-sm"></i>
                    </div>
                    <span class="text-[9px] font-bold text-indigo-400/70 tracking-widest uppercase">UPTIME</span>
                </div>
                <p id="uptime" class="font-mono font-bold text-slate-100 text-base leading-tight">--:--:--</p>
                <div class="mt-3 h-1 bg-indigo-900/50 rounded-full overflow-hidden">
                    <div class="h-full w-full bg-gradient-to-r from-green-500 to-emerald-400 rounded-full animate-pulse"></div>
                </div>
            </div>
            <div class="glass-card border border-indigo-900/50 card-glow-sm rounded-2xl p-5 animate-fade-up" style="animation-delay:0.1s">
                <div class="flex items-center gap-3 mb-3">
                    <div class="w-9 h-9 rounded-xl bg-blue-900/40 flex items-center justify-center">
                        <i class="fa-solid fa-server text-blue-400 text-sm"></i>
                    </div>
                    <span class="text-[9px] font-bold text-indigo-400/70 tracking-widest uppercase">PLATFORM</span>
                </div>
                <p id="platform" class="font-mono font-bold text-slate-100 text-base leading-tight truncate">--</p>
                <div class="flex gap-1.5 mt-3">
                    <span id="arch" class="stat-chip text-[9px] font-bold text-indigo-300 px-2 py-0.5 rounded">--</span>
                    <span id="node-ver" class="stat-chip text-[9px] font-bold text-violet-300 px-2 py-0.5 rounded">--</span>
                </div>
            </div>
            <div class="glass-card border border-indigo-900/50 card-glow-sm rounded-2xl p-5 animate-fade-up" style="animation-delay:0.15s">
                <div class="flex items-center gap-3 mb-3">
                    <div class="w-9 h-9 rounded-xl bg-red-900/30 flex items-center justify-center">
                        <i class="fa-solid fa-microchip text-red-400 text-sm"></i>
                    </div>
                    <span class="text-[9px] font-bold text-indigo-400/70 tracking-widest uppercase">CPU LOAD</span>
                </div>
                <p id="cpu-load" class="font-mono font-bold text-slate-100 text-base leading-tight">0%</p>
                <p id="cpu-model" class="text-[9px] font-mono text-indigo-400/60 truncate mt-2">Detecting...</p>
            </div>
        </div>

        <!-- MEMORY CHART -->
        <div class="glass-card border border-indigo-900/50 card-glow rounded-2xl overflow-hidden animate-fade-up" style="animation-delay:0.2s">
            <div class="header-bar px-5 py-3.5 flex items-center justify-between">
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-memory text-indigo-400 text-sm"></i>
                    <span class="font-display font-bold text-slate-100 text-sm tracking-tight">MEMORY USAGE</span>
                </div>
                <div class="flex items-center gap-3 font-mono text-[10px] font-bold">
                    <span class="text-indigo-400/70">USED: <span id="mem-used" class="text-slate-100">0 GB</span></span>
                    <span class="text-indigo-900">//</span>
                    <span class="text-indigo-400/70">TOTAL: <span id="mem-total" class="text-slate-100">0 GB</span></span>
                </div>
            </div>
            <div class="px-5 pt-4 pb-5">
                <div class="flex items-end justify-between mb-2">
                    <div class="flex items-baseline gap-1.5">
                        <span id="ram-percent-big" class="font-display font-bold text-3xl title-gradient">0%</span>
                        <span class="text-[10px] font-mono text-indigo-400/60">memory used</span>
                    </div>
                    <span class="text-[9px] font-mono text-indigo-400/60">FREE: <span id="mem-free" class="text-indigo-400 font-bold">0 GB</span></span>
                </div>
                <div class="relative w-full h-[110px] rounded-xl overflow-hidden bg-indigo-950/40 border border-indigo-900/40">
                    <svg id="mem-chart" class="w-full h-full" viewBox="0 0 400 110" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
                        <defs>
                            <linearGradient id="memGrad" x1="0" y1="0" x2="0" y2="1">
                                <stop offset="0%" stop-color="#6366f1" stop-opacity="0.6"/>
                                <stop offset="100%" stop-color="#6366f1" stop-opacity="0"/>
                            </linearGradient>
                        </defs>
                        <line x1="0" y1="27" x2="400" y2="27" stroke="rgba(99,102,241,0.1)" stroke-width="1"/>
                        <line x1="0" y1="55" x2="400" y2="55" stroke="rgba(99,102,241,0.1)" stroke-width="1"/>
                        <line x1="0" y1="82" x2="400" y2="82" stroke="rgba(99,102,241,0.1)" stroke-width="1"/>
                        <path id="chart-fill-path" class="chart-fill" d="M0,110 L400,110 Z"/>
                        <path id="chart-line-path" class="chart-line" d="M0,55"/>
                        <circle id="chart-dot" class="chart-dot" cx="400" cy="55" r="4"/>
                    </svg>
                    <div class="absolute left-2 top-0 h-full flex flex-col justify-between py-1 pointer-events-none">
                        <span class="text-[8px] font-mono text-indigo-600">100%</span>
                        <span class="text-[8px] font-mono text-indigo-600">50%</span>
                        <span class="text-[8px] font-mono text-indigo-600">0%</span>
                    </div>
                </div>
                <div class="line-gradient h-px w-full rounded-full mt-4"></div>
            </div>
        </div>

        <!-- TERMINAL -->
        <div class="term-bg rounded-2xl overflow-hidden animate-fade-up" style="animation-delay:0.25s">
            <div class="term-header px-4 py-2.5 flex items-center justify-between select-none">
                <div class="flex gap-1.5 items-center">
                    <div class="w-2.5 h-2.5 rounded-full bg-red-500/70"></div>
                    <div class="w-2.5 h-2.5 rounded-full bg-yellow-500/70"></div>
                    <div class="w-2.5 h-2.5 rounded-full bg-green-500/70"></div>
                    <span class="ml-2 text-indigo-500/60 font-mono text-[10px] font-bold tracking-widest">PUBLIC REQUESTS</span>
                </div>
                <span class="text-[9px] font-mono text-indigo-600/50">live feed</span>
            </div>
            <div id="realtime-logs" class="p-4 text-xs overflow-y-auto h-[220px] space-y-1 font-mono leading-relaxed">
                <div class="text-indigo-600/50 italic">Listening for requests...</div>
            </div>
        </div>

        <!-- Footer -->
        <div class="flex flex-col items-center gap-2 pb-4 animate-fade-up" style="animation-delay:0.3s">
            <div class="footer-line w-16"></div>
            <p class="text-[9px] font-mono text-indigo-600/50 tracking-[0.2em]">KuroNeko &copy; 2026</p>
        </div>
    </main>

    <script>
        const HISTORY_LEN = 40;
        const memHistory = new Array(HISTORY_LEN).fill(null);
        let lastRequestsJson = '';

        function initSoftButtons() {
            document.querySelectorAll('.soft-btn').forEach(btn => {
                const handle = (e) => {
                    if (['pointerleave','pointercancel','pointerup'].includes(e.type)) {
                        btn.classList.remove('soft-btn--active');
                        try { btn.releasePointerCapture(e.pointerId); } catch(_) {}
                        return;
                    }
                    if (e.type === 'pointerdown') { btn.classList.add('soft-btn--active'); try { btn.setPointerCapture(e.pointerId); } catch(_){} }
                };
                ['pointerdown','pointerup','pointerleave','pointercancel'].forEach(ev => btn.addEventListener(ev, handle));
            });
        }

        function buildChartPaths(history) {
            const W = 400, H = 110, PAD = 8;
            const validPoints = [];
            history.forEach((v, i) => {
                if (v !== null) {
                    const x = PAD + (i / (HISTORY_LEN - 1)) * (W - PAD * 2);
                    const y = H - PAD - ((v / 100) * (H - PAD * 2));
                    validPoints.push({ x, y });
                }
            });
            if (validPoints.length < 2) return;
            let linePath = `M${validPoints[0].x},${validPoints[0].y}`;
            for (let i = 1; i < validPoints.length; i++) {
                const cp1x = (validPoints[i-1].x + validPoints[i].x) / 2;
                linePath += ` C${cp1x},${validPoints[i-1].y} ${cp1x},${validPoints[i].y} ${validPoints[i].x},${validPoints[i].y}`;
            }
            const last = validPoints[validPoints.length - 1];
            const first = validPoints[0];
            document.getElementById('chart-line-path').setAttribute('d', linePath);
            document.getElementById('chart-fill-path').setAttribute('d', linePath + ` L${last.x},${H} L${first.x},${H} Z`);
            document.getElementById('chart-dot').setAttribute('cx', last.x);
            document.getElementById('chart-dot').setAttribute('cy', last.y);
        }

        async function fetchStats() {
            try {
                const res = await fetch('/stats/data');
                const data = await res.json();
                if (!data.status) return;
                const s = data.server;
                document.getElementById('uptime').innerText = s.uptime;
                document.getElementById('platform').innerText = s.hostname;
                document.getElementById('arch').innerText = s.arch;
                document.getElementById('node-ver').innerText = s.node_version;
                document.getElementById('cpu-model').innerText = `${s.cpu.model} (${s.cpu.cores}C)`;
                document.getElementById('cpu-load').innerText = (parseFloat(s.cpu.load) * 10).toFixed(1) + '%';
                document.getElementById('mem-used').innerText = s.memory.used;
                document.getElementById('mem-total').innerText = s.memory.total;
                document.getElementById('mem-free').innerText = s.memory.free;
                document.getElementById('ram-percent-big').innerText = `${s.memory.percent}%`;
                memHistory.shift(); memHistory.push(s.memory.percent);
                buildChartPaths(memHistory);
                const newJson = JSON.stringify(data.requests);
                if (data.requests && newJson !== lastRequestsJson) { lastRequestsJson = newJson; renderLogs(data.requests); }
            } catch (e) { console.error('Stats fetch error', e); }
        }

        function renderLogs(logs) {
            const container = document.getElementById('realtime-logs');
            container.innerHTML = '';
            if (!logs || logs.length === 0) {
                container.innerHTML = '<div class="text-indigo-600/50 italic">Listening for requests...</div>';
                return;
            }
            logs.forEach(log => {
                const div = document.createElement('div');
                div.className = 'break-all hover:bg-white/5 px-1 rounded transition-colors flex gap-2 items-center';
                const match = log.match(/^\[([A-Z]+)\] \[(\d+)\] (.*)$/);
                if (match) {
                    const [, method, status, url] = match;
                    let mColor = 'text-blue-400';
                    if (method === 'POST') mColor = 'text-green-400';
                    if (method === 'DELETE') mColor = 'text-red-400';
                    let sColor = 'text-emerald-400';
                    if (status.startsWith('4') || status.startsWith('5')) sColor = 'text-red-400';
                    div.innerHTML = `
                        <span class="${mColor} font-bold w-12 shrink-0 text-[10px]">[${method}]</span>
                        <span class="${sColor} font-bold w-10 shrink-0 text-[10px]">[${status}]</span>
                        <span class="text-indigo-300/70 truncate text-[10px]">${url}</span>
                    `;
                } else {
                    div.innerHTML = `<span class="text-indigo-500/50 text-[10px]">${log}</span>`;
                }
                container.appendChild(div);
            });
            container.scrollTop = container.scrollHeight;
        }

        initSoftButtons();
        fetchStats();
        setInterval(fetchStats, 1000);
    </script>
</body>
</html></div>

<br/>
<hr/>

<h2 align="center">📫 Hubungi Saya</h2>

<div align="center">
  <a href="mailto:emailanda@domain.com">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/>
  </a>
  <a href="https://linkedin.com/in/YOUR_LINKEDIN">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/>
  </a>
  <a href="https://instagram.com/YOUR_INSTAGRAM">
    <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram"/>
  </a>
</div>

<br/>

<div align="center">
  <i>"Code is like humor. When you have to explain it, it’s bad." - Cory House</i>
</div>

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer" />
</div></p>

<p align="right"><i>"Simplicity is the ultimate sophistication."</i></p>
