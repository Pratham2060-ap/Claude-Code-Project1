# 🪐 Orbit Desk — Complete Source File Reference

> **All project files in one place.** Copy any code block and save it as the filename shown.
> Last generated: 21 May 2026

---

## 📁 Project Structure

```
Claude-Code-Project1/
├── index.html                ← Entire app (~2,942 lines)
├── vercel.json               ← Vercel caching config
├── .gitignore                ← Git ignore rules
├── DEPLOY.md                 ← Deployment guide
├── README.md                 ← Repo homepage
└── assets/                   ← Background images (binary, download from GitHub)
    ├── celestial-command.png
    ├── celestial-budget.png
    ├── celestial-clients.png
    ├── celestial-invoices.png
    ├── celestial-subscriptions.png
    ├── celestial-tax.png
    ├── celestial-cashflow.png
    └── celestial-goals.png
```

> ⚠️ **Images note:** The 8 .png files in ssets/ are binary and cannot be embedded in markdown.
> Download them directly: [assets/ on GitHub →](https://github.com/Pratham2060-ap/Claude-Code-Project1/tree/main/assets)

---

## 📊 File Comparison Summary

| File | Lines | Purpose |
|---|---|---|
| `index.html` | 2,942 | **The entire app** — all React components, CSS, data, 8 modules |
| `vercel.json` | 19 | Vercel caching headers for static assets |
| `.gitignore` | 12 | Excludes `.claude/` folder and OS files from git |
| `DEPLOY.md` | ~140 | Step-by-step Vercel / GitHub Pages deployment guide |
| `assets/*.png` | — | 8 celestial background images, one per module |

---

## 🏗️ What's Inside index.html

The entire app is one self-contained HTML file with sequential `<script type="text/babel">` blocks:

| Block | Contents |
|---|---|
| `<style>` | All CSS — reset, CSS variables, dark/light themes, all component styles |
| Script 1 | `CURRENCIES`, `formatCurrency`, `formatCompact`, module config |
| Script 2 | Shared UI components: `OrbitCard`, `Badge`, `Btn`, `Modal`, `ArcGauge`, `DataTable`… |
| Script 3 | `OrbitIcons` SVG library + `PlanetIcons` for sidebar |
| Script 4 | `CommandCenter` — dashboard with charts and quick actions |
| Script 5 | `CSVImportModal` — 3-step CSV import wizard |
| Script 6 | `BudgetModule` — income / expenses / platforms |
| Script 7 | `ClientsModule` + projects |
| Script 8 | `InvoicesModule` — create, send, track |
| Script 9 | `SubscriptionsModule` — recurring costs |
| Script 10 | `TaxModule` + `ReserveForm` — animated arc gauge |
| Script 11 | `CashFlowModule` — optimised memoized calendar |
| Script 12 | `GoalsModule` + `GoalFormModal` — milestones |
| Script 13 | `Sidebar` + `SettingsModal` |
| Script 14 | `INITIAL_DATA`, `OrbitApp`, `ReactDOM.render` |

---

## 📄 FILE 1 — index.html

> The complete application. Save as `index.html` in your project root.

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Orbit Desk — Mission Control for Solopreneurs</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Exo+2:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;600;700&family=Orbitron:wght@700;900&display=swap" rel="stylesheet">

<style>
/* RESET & BASE */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}
body{font-family:'Exo 2',system-ui,sans-serif;background:var(--bg-void);color:var(--text-primary);overflow:hidden;height:100vh}
body::after{content:'';position:fixed;inset:0;z-index:-1;pointer-events:none;background:
radial-gradient(1px 1px at 50px 40px,rgba(255,255,255,.25),transparent),
radial-gradient(1px 1px at 180px 90px,rgba(255,255,255,.18),transparent),
radial-gradient(1px 1px at 320px 200px,rgba(255,255,255,.22),transparent),
radial-gradient(1px 1px at 480px 50px,rgba(255,255,255,.15),transparent),
radial-gradient(1px 1px at 600px 300px,rgba(255,255,255,.2),transparent),
radial-gradient(1px 1px at 750px 150px,rgba(255,255,255,.12),transparent),
radial-gradient(1px 1px at 900px 400px,rgba(255,255,255,.18),transparent),
radial-gradient(1px 1px at 100px 500px,rgba(255,255,255,.14),transparent),
radial-gradient(1px 1px at 250px 350px,rgba(255,255,255,.2),transparent),
radial-gradient(1px 1px at 400px 600px,rgba(255,255,255,.16),transparent),
radial-gradient(1px 1px at 550px 450px,rgba(255,255,255,.22),transparent),
radial-gradient(1px 1px at 700px 550px,rgba(255,255,255,.13),transparent),
radial-gradient(1px 1px at 850px 250px,rgba(255,255,255,.19),transparent),
radial-gradient(1px 1px at 1000px 100px,rgba(255,255,255,.15),transparent),
radial-gradient(1px 1px at 1150px 350px,rgba(255,255,255,.21),transparent),
radial-gradient(1px 1px at 1300px 500px,rgba(255,255,255,.12),transparent),
radial-gradient(1px 1px at 130px 700px,rgba(255,255,255,.17),transparent),
radial-gradient(1px 1px at 350px 800px,rgba(255,255,255,.14),transparent),
radial-gradient(1px 1px at 500px 750px,rgba(255,255,255,.2),transparent),
radial-gradient(1px 1px at 680px 680px,rgba(255,255,255,.11),transparent),
radial-gradient(1px 1px at 820px 780px,rgba(255,255,255,.16),transparent),
radial-gradient(1px 1px at 960px 600px,rgba(255,255,255,.22),transparent),
radial-gradient(1px 1px at 1100px 700px,rgba(255,255,255,.13),transparent),
radial-gradient(1px 1px at 1250px 200px,rgba(255,255,255,.18),transparent),
radial-gradient(1px 1px at 70px 250px,rgba(255,255,255,.15),transparent),
radial-gradient(1px 1px at 220px 120px,rgba(255,255,255,.2),transparent),
radial-gradient(1px 1px at 420px 420px,rgba(255,255,255,.12),transparent),
radial-gradient(1px 1px at 630px 180px,rgba(255,255,255,.19),transparent),
radial-gradient(1px 1px at 780px 520px,rgba(255,255,255,.14),transparent),
radial-gradient(1px 1px at 930px 320px,rgba(255,255,255,.21),transparent),
radial-gradient(1px 1px at 1050px 450px,rgba(255,255,255,.11),transparent),
radial-gradient(1px 1px at 1200px 600px,rgba(255,255,255,.17),transparent),
radial-gradient(1px 1px at 160px 580px,rgba(255,255,255,.13),transparent),
radial-gradient(1px 1px at 300px 650px,rgba(255,255,255,.2),transparent),
radial-gradient(1px 1px at 470px 300px,rgba(255,255,255,.15),transparent),
radial-gradient(1px 1px at 590px 530px,rgba(255,255,255,.18),transparent),
radial-gradient(1px 1px at 1350px 150px,rgba(255,255,255,.14),transparent),
radial-gradient(1px 1px at 1400px 400px,rgba(255,255,255,.19),transparent),
radial-gradient(1px 1px at 40px 800px,rgba(255,255,255,.16),transparent),
radial-gradient(1px 1px at 200px 900px,rgba(255,255,255,.12),transparent),
repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(45,45,110,0.025) 80px),
repeating-linear-gradient(90deg,transparent,transparent 79px,rgba(45,45,110,0.025) 80px),
linear-gradient(180deg,#0a0a1a 0%,#080820 100%)}
button{font-family:inherit;cursor:pointer;border:none;background:none;color:inherit}
input,select,textarea{font-family:inherit;color:inherit;background:none;border:none;outline:none}
a{color:inherit;text-decoration:none}
::-webkit-scrollbar{width:6px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:rgba(45,45,110,0.4);border-radius:3px}
::-webkit-scrollbar-thumb:hover{background:rgba(45,45,110,0.7)}

/* CUSTOM PROPERTIES */
:root{
  --bg-void:#0a0a1a;--bg-sidebar:#080818;--bg-surface:#0f0f2e;--bg-elevated:#1a1a3e;--bg-highlight:#242452;
  --border-subtle:rgba(45,45,110,0.4);--border-medium:rgba(45,45,110,0.7);--border-strong:rgba(124,58,237,0.5);--border-divider:rgba(45,45,110,0.25);
  --accent-command:#7c3aed;--accent-budget:#10b981;--accent-clients:#ec4899;--accent-invoices:#f59e0b;
  --accent-subscriptions:#06b6d4;--accent-tax:#fb923c;--accent-cashflow:#0d9488;--accent-goals:#f43f5e;
  --color-success:#10b981;--color-danger:#ef4444;--color-warning:#f59e0b;--color-info:#06b6d4;--color-neutral:#64748b;
  --text-primary:#e2e8f0;--text-secondary:#94a3b8;--text-tertiary:#475569;--text-ghost:#334155;
  --font-display:'Orbitron',monospace;--font-body:'Exo 2',system-ui,sans-serif;--font-mono:'JetBrains Mono','Fira Code',monospace;
  --sidebar-w:240px;--sidebar-collapsed:68px;--ease-smooth:cubic-bezier(0.4,0,0.2,1);--font-scale:1;
}

/* LIGHT THEME */
[data-theme="light"]{
  --bg-void:#f0f2f8;--bg-sidebar:#ffffff;--bg-surface:#ffffff;--bg-elevated:#f0f2f8;--bg-highlight:#e2e5f0;
  --border-subtle:rgba(45,45,110,0.1);--border-medium:rgba(45,45,110,0.18);--border-strong:rgba(124,58,237,0.35);--border-divider:rgba(45,45,110,0.08);
  --text-primary:#1a1a2e;--text-secondary:#475569;--text-tertiary:#94a3b8;--text-ghost:#cbd5e1;
}
[data-theme="light"] body{background:var(--bg-void)}
[data-theme="light"] body::after{background:
  repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(45,45,110,0.04) 80px),
  repeating-linear-gradient(90deg,transparent,transparent 79px,rgba(45,45,110,0.04) 80px),
  linear-gradient(180deg,#f0f2f8 0%,#e8eaf4 100%) !important}
[data-theme="light"] .sidebar{background:var(--bg-sidebar);border-color:var(--border-subtle)}
[data-theme="light"] .nav-btn:hover{background:rgba(124,58,237,0.06)}
[data-theme="light"] .nav-btn.active{background:rgba(124,58,237,0.08);border-color:rgba(124,58,237,0.2);box-shadow:0 0 16px rgba(124,58,237,0.08),inset 0 0 8px rgba(124,58,237,0.04)}
[data-theme="light"] .card{background:var(--bg-surface);box-shadow:0 1px 3px rgba(0,0,0,0.06)}
[data-theme="light"] .card:hover{box-shadow:0 4px 16px rgba(0,0,0,0.1)}
[data-theme="light"] .card.glass{background:rgba(255,255,255,0.7);backdrop-filter:blur(20px);border-color:rgba(124,58,237,0.1)}
[data-theme="light"] .form-input,[data-theme="light"] .form-select{background:var(--bg-elevated);border-color:rgba(45,45,110,0.15);color:var(--text-primary)}
[data-theme="light"] .data-table thead th{background:var(--bg-elevated)}
[data-theme="light"] .inline-form{background:var(--bg-surface);border-color:var(--border-subtle)}
[data-theme="light"] .modal-card{background:var(--bg-surface)}
[data-theme="light"] .modal-overlay{background:rgba(0,0,0,0.3)}
[data-theme="light"] .nav-badge{border-color:var(--bg-sidebar)}
[data-theme="light"] .orbit-bg{opacity:0.4}
[data-theme="light"] .orbit-ring{border-color:rgba(124,58,237,0.06)}
[data-theme="light"] ::-webkit-scrollbar-thumb{background:rgba(45,45,110,0.15)}
[data-theme="light"] .arc-track{stroke:#e2e5f0}

/* LAYOUT */
#orbit-root{display:flex;height:100vh;width:100vw;overflow:hidden;position:relative}

/* BACKGROUND EFFECTS */
.orbit-bg{position:fixed;inset:0;pointer-events:none;z-index:0;overflow:hidden}
.orbit-ring{position:absolute;border-radius:50%;border:1px solid rgba(124,58,237,0.03)}
.orbit-ring-1{width:800px;height:800px;top:20%;right:-200px;animation:spin 120s linear infinite}
.orbit-ring-2{width:500px;height:500px;bottom:10%;left:30%;animation:spin 90s linear infinite reverse}
.orbit-ring-3{width:1200px;height:1200px;top:-30%;left:10%;animation:spin 180s linear infinite;border-color:rgba(6,182,212,0.02)}
.orbit-dot{position:absolute;width:3px;height:3px;background:rgba(124,58,237,0.2);border-radius:50%;animation:float-dot 25s ease-in-out infinite}
.orbit-dot:nth-child(4){top:15%;left:45%;animation-delay:-5s;background:rgba(16,185,129,0.15)}
.orbit-dot:nth-child(5){top:60%;left:70%;animation-delay:-10s;background:rgba(6,182,212,0.15)}
.orbit-dot:nth-child(6){top:80%;left:35%;animation-delay:-15s}
.orbit-dot:nth-child(7){top:30%;left:85%;animation-delay:-20s;background:rgba(236,72,153,0.12)}
.grid-overlay{position:absolute;inset:0;background-image:radial-gradient(rgba(45,45,110,0.07) 1px,transparent 1px);background-size:40px 40px}

/* CELESTIAL BACKGROUNDS */
.celestial{position:fixed;inset:0;pointer-events:none;z-index:0;opacity:0;transition:opacity .6s ease;background-size:cover !important;background-position:center !important;background-repeat:no-repeat !important}
.celestial.active{opacity:1}
.celestial-command{background-image:url('assets/celestial-command.png')}
.celestial-budget{background-image:url('assets/celestial-budget.png')}
.celestial-clients{background-image:url('assets/celestial-clients.png')}
.celestial-invoices{background-image:url('assets/celestial-invoices.png')}
.celestial-subscriptions{background-image:url('assets/celestial-subscriptions.png')}
.celestial-tax{background-image:url('assets/celestial-tax.png')}
.celestial-cashflow{background-image:url('assets/celestial-cashflow.png')}
.celestial-goals{background-image:url('assets/celestial-goals.png')}
[data-theme="light"] .celestial.active{opacity:0.85}
[data-theme="light"] .celestial{filter:saturate(0.85) brightness(1.1)}

.content-area{position:relative}
.content-area::before{content:'';position:fixed;top:0;left:var(--sidebar-w);right:0;bottom:0;background:linear-gradient(180deg,rgba(10,10,26,0.5) 0%,rgba(10,10,26,0.75) 100%);pointer-events:none;z-index:0;transition:left .3s var(--ease-smooth),background .4s ease}
.sidebar.collapsed ~ .content-area::before{left:var(--sidebar-collapsed)}
[data-theme="light"] .content-area::before{background:linear-gradient(180deg,rgba(240,242,248,0.7) 0%,rgba(240,242,248,0.88) 100%)}
@media(max-width:1023px){.content-area::before{left:var(--sidebar-collapsed) !important}}
@media(max-width:767px){.content-area::before{left:0 !important}}
.content-area > *{position:relative;z-index:1}

/* THEME TOGGLE */
.theme-toggle{width:40px;height:40px;border-radius:10px;display:grid;place-items:center;background:var(--bg-surface);border:1px solid var(--border-subtle);cursor:pointer;transition:all .25s ease;color:var(--text-secondary);position:relative;overflow:hidden}
.theme-toggle:hover{border-color:var(--border-medium);color:var(--text-primary)}
.theme-toggle svg{transition:transform .4s cubic-bezier(0.4,0,0.2,1)}
.theme-toggle:active svg{transform:rotate(180deg) scale(0.8)}

/* PLANET ICON */
.planet-icon{flex-shrink:0;filter:drop-shadow(0 0 3px var(--planet-glow,transparent));transition:filter .25s ease}
.nav-btn.active .planet-icon{filter:drop-shadow(0 0 6px var(--planet-glow,transparent))}

/* SIDEBAR */
.sidebar{width:var(--sidebar-w);min-width:var(--sidebar-w);height:100vh;background:var(--bg-sidebar);border-right:1px solid var(--border-subtle);display:flex;flex-direction:column;padding:20px 16px;position:relative;z-index:100;transition:width .3s var(--ease-smooth),min-width .3s var(--ease-smooth)}
.sidebar.collapsed{width:var(--sidebar-collapsed);min-width:var(--sidebar-collapsed);padding:20px 10px}
.sidebar-logo{display:flex;align-items:center;gap:10px;padding:0 2px;margin-bottom:8px;white-space:nowrap;overflow:hidden}
.sidebar-logo-icon{width:28px;height:28px;flex-shrink:0}
.sidebar-logo-text{overflow:hidden;transition:opacity .2s}
.sidebar.collapsed .sidebar-logo-text{opacity:0;width:0}
.sidebar-logo-name{font-family:var(--font-display);font-weight:700;font-size:15px;color:var(--text-primary);letter-spacing:2px}
.sidebar-logo-tagline{font-size:11px;color:var(--text-tertiary);font-weight:300}
.sidebar-divider{height:1px;background:rgba(45,45,110,0.3);margin:16px 0;flex-shrink:0}
.sidebar-nav{flex:1;display:flex;flex-direction:column;gap:4px;overflow-y:auto;overflow-x:hidden}
.sidebar-bottom{display:flex;flex-direction:column;gap:4px}
.nav-btn{width:100%;height:48px;border-radius:10px;padding:0 14px;display:flex;align-items:center;gap:12px;position:relative;transition:all .25s var(--ease-smooth);border:1px solid transparent;white-space:nowrap;overflow:hidden}
.nav-btn svg{flex-shrink:0;transition:all .25s var(--ease-smooth);color:var(--text-tertiary)}
.nav-btn span{font-size:14px;color:var(--text-secondary);transition:all .25s var(--ease-smooth);font-weight:400}
.nav-btn:hover{background:rgba(124,58,237,0.06);border-color:rgba(124,58,237,0.15)}
.nav-btn:hover svg{color:var(--text-secondary)}
.nav-btn:hover span{color:var(--text-primary)}
.nav-btn.active{background:rgba(124,58,237,0.1);border-color:rgba(124,58,237,0.35);box-shadow:0 0 20px rgba(124,58,237,0.15),0 0 40px rgba(124,58,237,0.05),inset 0 0 12px rgba(124,58,237,0.08)}
.nav-btn.active span{color:var(--text-primary);font-weight:600}
.nav-btn .accent-bar{position:absolute;left:0;top:6px;bottom:6px;width:3px;border-radius:0 2px 2px 0;opacity:0;transition:opacity .25s var(--ease-smooth)}
.nav-btn.active .accent-bar{opacity:1}
.nav-badge{position:absolute;top:8px;right:8px;min-width:18px;height:18px;background:#ef4444;color:#fff;font-family:var(--font-mono);font-size:10px;font-weight:600;border-radius:100px;display:grid;place-items:center;padding:0 4px;border:2px solid var(--bg-sidebar)}
.sidebar.collapsed .nav-btn{padding:0;justify-content:center}
.sidebar.collapsed .nav-btn span{opacity:0;width:0;overflow:hidden}
.sidebar.collapsed .nav-badge{top:4px;right:4px}
.sidebar-tooltip{position:fixed;left:calc(var(--sidebar-collapsed) + 8px);background:var(--bg-elevated);color:var(--text-primary);padding:6px 12px;border-radius:6px;font-size:13px;font-weight:500;white-space:nowrap;pointer-events:none;opacity:0;transition:opacity .15s;z-index:1000;border:1px solid var(--border-subtle)}
.sidebar-tooltip.visible{opacity:1}

/* CONTENT AREA */
.content-area{flex:1;height:100vh;overflow-y:auto;overflow-x:hidden;padding:32px 40px;position:relative;z-index:1}
.page-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:32px;gap:16px;flex-wrap:wrap}
.page-header-left{display:flex;align-items:center;gap:14px}
.page-header-icon{width:28px;height:28px;flex-shrink:0}
.page-header h1{font-family:var(--font-display);font-weight:700;font-size:calc(26px * var(--font-scale));color:var(--text-primary);letter-spacing:1px}
.page-header p{font-size:calc(14px * var(--font-scale));color:var(--text-tertiary);font-weight:300;margin-top:4px}
.page-header-actions{display:flex;gap:10px;align-items:center}

/* CARDS */
.card{background:var(--bg-surface);border:1px solid var(--border-subtle);border-radius:12px;padding:20px 24px;transition:all .25s var(--ease-smooth)}
.card:hover{border-color:var(--border-medium);box-shadow:0 4px 24px rgba(0,0,0,0.3)}
.card-accent{border-left:3px solid var(--card-accent,var(--accent-command))}
.kpi-card{position:relative;overflow:hidden}
.kpi-label{font-family:var(--font-body);font-weight:600;font-size:calc(11px * var(--font-scale));text-transform:uppercase;letter-spacing:1.5px;color:var(--text-tertiary);margin-bottom:10px}
.kpi-value{font-family:var(--font-mono);font-weight:600;font-size:calc(32px * var(--font-scale));line-height:1.1;margin-bottom:8px}
.kpi-delta{font-size:calc(12px * var(--font-scale));display:flex;align-items:center;gap:4px}
.kpi-delta.positive{color:var(--color-success)}
.kpi-delta.negative{color:var(--color-danger)}
.kpi-pulse{position:absolute;top:20px;right:20px;width:8px;height:8px;border-radius:50%;animation:pulse 2s ease infinite}
.kpi-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:16px;margin-bottom:24px}

/* TABLES */
.data-table{width:100%;border-collapse:separate;border-spacing:0}
.data-table thead th{background:var(--bg-elevated);font-family:var(--font-body);font-weight:600;font-size:calc(11px * var(--font-scale));text-transform:uppercase;letter-spacing:1px;color:var(--text-tertiary);padding:12px 16px;text-align:left;border-bottom:1px solid var(--border-divider);white-space:nowrap}
.data-table thead th:first-child{border-radius:8px 0 0 0}
.data-table thead th:last-child{border-radius:0 8px 0 0}
.data-table tbody tr{border-bottom:1px solid rgba(45,45,110,0.15);transition:all .2s var(--ease-smooth);position:relative}
.data-table tbody tr:hover{background:rgba(124,58,237,0.04)}
.data-table tbody td{padding:14px 16px;font-size:calc(14px * var(--font-scale));color:var(--text-secondary);vertical-align:middle}
.data-table .mono{font-family:var(--font-mono);font-weight:400}
.data-table .amount{text-align:right;font-family:var(--font-mono)}
.table-footer{background:var(--bg-surface);padding:14px 16px;font-family:var(--font-mono);font-weight:600;display:flex;justify-content:space-between;border-radius:0 0 8px 8px;border-top:1px solid var(--border-divider)}
.table-wrap{background:var(--bg-surface);border:1px solid var(--border-subtle);border-radius:12px;overflow:hidden}
.table-actions{display:flex;gap:6px}

/* BADGES */
.badge{display:inline-flex;align-items:center;padding:4px 12px;border-radius:100px;font-family:var(--font-body);font-weight:600;font-size:11px;border:1px solid;white-space:nowrap}
.badge-success{background:rgba(16,185,129,0.12);color:#10b981;border-color:rgba(16,185,129,0.3)}
.badge-info{background:rgba(6,182,212,0.12);color:#06b6d4;border-color:rgba(6,182,212,0.3)}
.badge-warning{background:rgba(245,158,11,0.12);color:#f59e0b;border-color:rgba(245,158,11,0.3)}
.badge-danger{background:rgba(239,68,68,0.12);color:#ef4444;border-color:rgba(239,68,68,0.3)}
.badge-neutral{background:rgba(100,116,139,0.12);color:#94a3b8;border-color:rgba(100,116,139,0.3)}
.badge-orange{background:rgba(251,146,60,0.12);color:#fb923c;border-color:rgba(251,146,60,0.3)}

/* BUTTONS */
.btn{display:inline-flex;align-items:center;gap:8px;padding:10px 20px;border-radius:8px;font-family:var(--font-body);font-weight:600;font-size:14px;transition:all .2s ease;border:none;cursor:pointer;white-space:nowrap}
.btn:active{transform:scale(0.97)}
.btn-primary{color:#fff}
.btn-ghost{background:transparent;border:1px solid rgba(45,45,110,0.5);color:var(--text-secondary)}
.btn-ghost:hover{color:var(--text-primary)}
.btn-danger{background:#ef4444;color:#fff;box-shadow:0 0 16px rgba(239,68,68,0.3)}
.btn-danger:hover{background:#f87171}
.btn-icon{width:32px;height:32px;padding:0;border-radius:8px;display:grid;place-items:center;background:transparent;color:var(--text-tertiary);transition:all .2s ease}
.btn-icon:hover{background:var(--bg-elevated);color:var(--text-primary)}
.btn-sm{padding:6px 14px;font-size:13px}

/* FORMS */
.form-group{display:flex;flex-direction:column;gap:6px;margin-bottom:16px}
.form-label{font-weight:600;font-size:11px;text-transform:uppercase;letter-spacing:1.5px;color:var(--text-tertiary)}
.form-input{background:var(--bg-elevated);border:1px solid rgba(45,45,110,0.5);border-radius:8px;padding:10px 14px;color:var(--text-primary);font-size:14px;transition:all .2s ease;width:100%}
.form-input:focus{border-color:#7c3aed;box-shadow:0 0 0 3px rgba(124,58,237,0.15)}
.form-input::placeholder{color:var(--text-tertiary)}
.form-select{background:var(--bg-elevated);border:1px solid rgba(45,45,110,0.5);border-radius:8px;padding:10px 14px;color:var(--text-primary);font-size:14px;appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%23475569' stroke-width='2'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center;padding-right:36px;cursor:pointer;width:100%}
.form-select:focus{border-color:#7c3aed;box-shadow:0 0 0 3px rgba(124,58,237,0.15)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:16px}

/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.6);backdrop-filter:blur(4px);display:flex;align-items:center;justify-content:center;z-index:1000;animation:fadeIn .2s ease}
.modal-card{background:var(--bg-surface);border:1px solid rgba(45,45,110,0.5);border-radius:16px;width:100%;max-width:480px;max-height:85vh;overflow-y:auto;padding:28px;animation:modalIn .2s ease;margin:16px}
.modal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:24px}
.modal-header h2{font-family:var(--font-body);font-weight:600;font-size:18px}
.modal-footer{display:flex;justify-content:flex-end;gap:10px;margin-top:24px;padding-top:20px;border-top:1px solid var(--border-divider)}

/* ALERT BANNER */
.alert-banner{display:flex;align-items:center;gap:12px;padding:12px 16px;border-radius:10px;margin-bottom:20px;animation:slideDown .3s var(--ease-smooth)}
.alert-banner .alert-bar{width:4px;align-self:stretch;border-radius:2px;flex-shrink:0}
.alert-banner .alert-text{flex:1;font-size:14px}
.alert-banner .alert-actions{display:flex;gap:8px;align-items:center}

/* SUB TABS */
.sub-tabs{display:flex;gap:6px;margin-bottom:24px;flex-wrap:wrap}
.sub-tab{padding:8px 16px;border-radius:8px;font-size:13px;font-weight:500;color:var(--text-secondary);border:1px solid transparent;transition:all .2s ease;background:transparent}
.sub-tab:hover{color:var(--text-primary)}
.sub-tab.active{color:var(--tab-accent,var(--accent-command))}

/* PROGRESS BAR */
.progress-track{background:var(--bg-elevated);height:10px;border-radius:5px;overflow:hidden;position:relative}
.progress-fill{height:100%;border-radius:5px;transition:width .6s var(--ease-smooth);position:relative}
.progress-markers{position:absolute;inset:0;display:flex;justify-content:space-around;align-items:center;padding:0 2px}
.progress-marker{width:4px;height:4px;background:rgba(255,255,255,0.3);border-radius:50%}

/* EMPTY STATE */
.empty-state{text-align:center;padding:60px 20px;max-width:400px;margin:0 auto}
.empty-state-icon{margin-bottom:20px;opacity:0.5}
.empty-state h3{font-family:var(--font-body);font-weight:600;font-size:18px;margin-bottom:8px}
.empty-state p{font-size:14px;color:var(--text-secondary);margin-bottom:20px}

/* GLASS CARD */
.card.glass{background:rgba(15,15,46,0.5);backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border-color:rgba(124,58,237,0.12)}
.card.glass:hover{border-color:rgba(124,58,237,0.25);box-shadow:0 8px 32px rgba(0,0,0,0.3)}

/* INLINE FORM */
.inline-form{background:var(--bg-surface);border:1px solid var(--border-subtle);border-radius:12px;padding:24px;margin-bottom:24px;border-top:3px solid var(--form-accent,#7c3aed)}
.inline-form .form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:14px;margin-top:14px}

/* AVATAR */
.avatar{display:inline-flex;align-items:center;justify-content:center;border-radius:50%;font-family:var(--font-body);font-weight:600;flex-shrink:0;letter-spacing:0.5px}

/* ARC GAUGE */
.arc-gauge{display:flex;flex-direction:column;align-items:center;padding:20px 0}
.arc-gauge-label{font-family:var(--font-mono);font-weight:700;position:relative;z-index:1;line-height:1}
.arc-gauge-sub{font-size:13px;color:var(--text-tertiary);margin-top:8px;text-align:center}

/* CALENDAR */
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px}
.cal-header{font-family:var(--font-body);font-weight:600;font-size:11px;text-transform:uppercase;letter-spacing:1px;color:var(--text-tertiary);text-align:center;padding:8px 0}
.cal-day{aspect-ratio:1;display:flex;flex-direction:column;align-items:center;justify-content:center;border-radius:10px;cursor:pointer;transition:background .12s ease,border-color .12s ease,transform .1s ease;position:relative;font-size:14px;color:var(--text-secondary);gap:3px;will-change:transform}
.cal-day:hover{background:var(--bg-elevated);transform:scale(1.08)}
.cal-day:active{transform:scale(0.95)}
.cal-day.today{background:rgba(13,148,136,0.15);border:1.5px solid var(--accent-cashflow);color:var(--text-primary);font-weight:700}
.cal-day.selected{background:rgba(124,58,237,0.18);border:1.5px solid var(--accent-command);color:var(--text-primary);font-weight:600}
.cal-day.selected.today{background:rgba(124,58,237,0.22);border-color:var(--accent-command)}
.cal-day.other-month{opacity:0.2;pointer-events:none}
.cal-dots{display:flex;gap:2px;align-items:center}
.cal-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0}
.cal-events-panel{min-height:400px;display:flex;flex-direction:column}
.cal-event-card{padding:12px 14px;background:var(--bg-elevated);border-radius:10px;border-left:3px solid var(--ev-color,#7c3aed);margin-bottom:8px;transition:transform .15s ease,box-shadow .15s ease}
.cal-event-card:hover{transform:translateX(3px);box-shadow:0 4px 16px rgba(0,0,0,.15)}
.cal-month-nav{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}
.cal-month-title{font-family:var(--font-display);font-weight:700;font-size:16px;color:var(--text-primary);cursor:pointer;padding:4px 12px;border-radius:8px;transition:background .12s ease}
.cal-month-title:hover{background:var(--bg-elevated)}
.cal-wrap{overflow:hidden;position:relative}
@keyframes slideInLeft{from{opacity:0;transform:translateX(-24px)}to{opacity:1;transform:translateX(0)}}
@keyframes slideInRight{from{opacity:0;transform:translateX(24px)}to{opacity:1;transform:translateX(0)}}
.cal-slide-left{animation:slideInLeft .22s cubic-bezier(0.4,0,0.2,1)}
.cal-slide-right{animation:slideInRight .22s cubic-bezier(0.4,0,0.2,1)}

/* MILESTONE */
.milestone{display:inline-flex;align-items:center;gap:6px;font-size:13px;color:var(--text-tertiary)}
.milestone.done{color:var(--color-success)}
.milestone-dot{width:20px;height:20px;border-radius:50%;border:2px solid currentColor;display:grid;place-items:center;transition:all .3s ease}
.milestone.done .milestone-dot{background:var(--color-success);border-color:var(--color-success);color:#fff}

/* TIMELINE BAR */
.timeline-bar{height:6px;background:var(--bg-elevated);border-radius:3px;overflow:hidden;position:relative}
.timeline-fill{height:100%;border-radius:3px;transition:width .6s var(--ease-smooth)}

/* TAX CALENDAR */
.tax-event{display:flex;align-items:center;gap:14px;padding:12px 16px;border-bottom:1px solid var(--border-divider)}
.tax-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.tax-dot.upcoming{background:#f59e0b;animation:pulse 2s ease infinite}
.tax-dot.approaching{background:#ef4444;animation:pulse 1.5s ease infinite}
.tax-dot.scheduled{background:var(--color-neutral)}
.tax-dot.past{background:var(--color-success)}

/* WEEKLY GROUP */
.week-group{margin-bottom:20px}
.week-label{font-family:var(--font-body);font-weight:600;font-size:11px;text-transform:uppercase;letter-spacing:1.5px;color:var(--text-tertiary);margin-bottom:10px}
.week-item{display:flex;align-items:center;gap:14px;padding:10px 14px;border-bottom:1px solid var(--border-divider);font-size:14px}

/* ── CSV IMPORT MODAL ─────────────────────────────────── */
.csv-steps{display:flex;align-items:center;justify-content:center;gap:0;margin-bottom:28px;padding-bottom:20px;border-bottom:1px solid var(--border-divider)}
.csv-step-item{display:flex;flex-direction:column;align-items:center;gap:6px;min-width:80px}
.csv-step-dot{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;font-family:var(--font-mono);transition:all .3s ease;background:var(--bg-elevated);border:2px solid var(--border-medium);color:var(--text-tertiary)}
.csv-step-dot.active{background:#10b981;border-color:#10b981;color:#fff;box-shadow:0 0 16px rgba(16,185,129,.35)}
.csv-step-dot.done{background:#10b981;border-color:#10b981;color:#fff}
.csv-step-label{font-size:12px;color:var(--text-tertiary);font-weight:500;transition:color .3s}
.csv-step-label.active{color:#10b981;font-weight:600}
.csv-step-label.done{color:#10b981}
.csv-step-line{flex:1;height:2px;background:var(--border-medium);min-width:40px;transition:background .3s;margin:0 4px;margin-bottom:22px}
.csv-step-line.active{background:#10b981}
.csv-step-content{animation:fadeInUp .2s ease}
@keyframes fadeInUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.csv-platform-chip{padding:3px 10px;border-radius:20px;background:rgba(16,185,129,.06);border:1px solid rgba(16,185,129,.2);color:var(--text-secondary);font-size:12px;font-family:var(--font-body)}
.csv-dropzone{border:2px dashed rgba(16,185,129,.3);border-radius:12px;background:rgba(16,185,129,.03);padding:40px 24px;text-align:center;cursor:pointer;transition:all .18s ease;user-select:none}
.csv-dropzone:hover{border-color:rgba(16,185,129,.6);background:rgba(16,185,129,.07);box-shadow:0 0 24px rgba(16,185,129,.08)}
.csv-dropzone.drag-over{border:2px solid #10b981;background:rgba(16,185,129,.11);transform:scale(1.01);box-shadow:0 0 32px rgba(16,185,129,.15)}
.csv-upload-icon{font-size:38px;color:#10b981;line-height:1}
.csv-file-info{display:flex;align-items:center;gap:8px;padding:12px 16px;background:rgba(16,185,129,.06);border:1px solid rgba(16,185,129,.25);border-radius:10px;flex-wrap:wrap}
.csv-remove{margin-left:auto;background:none;border:none;cursor:pointer;color:var(--text-tertiary);font-size:18px;line-height:1;padding:2px 6px;border-radius:4px;transition:color .15s}
.csv-remove:hover{color:#ef4444}
.csv-type-btn{padding:8px 18px;border-radius:8px;border:1px solid var(--border-medium);background:transparent;color:var(--text-secondary);font-family:var(--font-body);font-size:13px;cursor:pointer;transition:all .15s}
.csv-type-btn.active{background:#10b981;border-color:#10b981;color:#fff;box-shadow:0 0 14px rgba(16,185,129,.25)}
.csv-detect-banner{padding:10px 14px;border-radius:8px;background:rgba(16,185,129,.08);border:1px solid rgba(16,185,129,.25);color:var(--text-secondary);font-size:13px;margin-bottom:16px}
.csv-detect-banner.warn{background:rgba(245,158,11,.07);border-color:rgba(245,158,11,.3);color:#f59e0b}
.csv-preview-table{width:100%;border-collapse:collapse;font-family:var(--font-mono);font-size:12px}
.csv-preview-table th{background:var(--bg-highlight);color:var(--text-secondary);padding:7px 12px;border:1px solid var(--border-medium);white-space:nowrap;font-weight:600}
.csv-preview-table td{padding:6px 12px;border:1px solid var(--border-subtle);color:var(--text-primary);white-space:nowrap;max-width:160px;overflow:hidden;text-overflow:ellipsis}
.csv-preview-table tr:nth-child(even) td{background:rgba(255,255,255,.02)}
.csv-mapping{display:flex;flex-direction:column;gap:10px}
.csv-map-row{display:flex;align-items:center;gap:10px}
.csv-map-label{min-width:160px;font-size:13px;color:var(--text-secondary);font-weight:500}
.csv-map-arrow{color:var(--text-tertiary);font-size:16px;margin:0 4px}
.csv-map-select{flex:1}
.csv-stat-card{background:var(--bg-elevated);border-radius:10px;padding:16px;text-align:center;border:1px solid var(--border-subtle)}
.csv-warn-banner{padding:10px 14px;background:rgba(245,158,11,.07);border:1px solid rgba(245,158,11,.3);border-radius:8px;color:#f59e0b;font-size:13px;margin-bottom:12px}
.csv-preview-list{max-height:220px;overflow-y:auto;border:1px solid var(--border-subtle);border-radius:8px;margin-bottom:4px}
.csv-preview-row{display:flex;align-items:center;gap:10px;padding:8px 12px;border-bottom:1px solid var(--border-divider);font-size:13px;transition:background .1s}
.csv-preview-row:last-child{border-bottom:none}
.csv-preview-row:hover{background:rgba(255,255,255,.02)}
.csv-preview-row.invalid{opacity:.7}
.csv-preview-row.duplicate{opacity:.5}
.csv-row-icon{font-size:14px;min-width:18px}
.csv-preview-row:not(.invalid):not(.duplicate) .csv-row-icon{color:#10b981}
.csv-preview-row.invalid .csv-row-icon{color:#f59e0b}
.csv-preview-row.duplicate .csv-row-icon{color:var(--text-tertiary)}
.csv-success-icon{width:64px;height:64px;border-radius:50%;background:rgba(16,185,129,.15);border:2px solid #10b981;display:flex;align-items:center;justify-content:center;font-size:28px;color:#10b981;margin:0 auto;animation:successPop .45s cubic-bezier(0.175,0.885,0.32,1.275)}
@keyframes successPop{from{transform:scale(0);opacity:0}to{transform:scale(1);opacity:1}}
.csv-particles{position:relative;height:0;pointer-events:none}
.csv-particle{position:absolute;width:7px;height:7px;border-radius:50%;background:#10b981;animation:particleBurst .7s ease-out forwards}
@keyframes particleBurst{0%{transform:translate(0,0) scale(1);opacity:1}100%{opacity:0;transform:var(--tx,translate(0,-60px)) scale(0)}}
.csv-particle.p0{left:50%;top:-10px;--tx:translate(-80px,-50px);animation-delay:0s}
.csv-particle.p1{left:50%;top:-10px;--tx:translate(-55px,-70px);animation-delay:.04s;background:#0d9488}
.csv-particle.p2{left:50%;top:-10px;--tx:translate(0px,-80px);animation-delay:.06s}
.csv-particle.p3{left:50%;top:-10px;--tx:translate(55px,-70px);animation-delay:.04s;background:#0d9488}
.csv-particle.p4{left:50%;top:-10px;--tx:translate(80px,-50px);animation-delay:0s}
.csv-particle.p5{left:50%;top:-10px;--tx:translate(80px,-15px);animation-delay:.08s;background:#34d399}
.csv-particle.p6{left:50%;top:-10px;--tx:translate(-80px,-15px);animation-delay:.08s;background:#34d399}
.csv-particle.p7{left:50%;top:-10px;--tx:translate(50px,10px);animation-delay:.05s}
.csv-particle.p8{left:50%;top:-10px;--tx:translate(-50px,10px);animation-delay:.05s;background:#0d9488}
.csv-particle.p9{left:50%;top:-10px;--tx:translate(0px,20px);animation-delay:.1s;background:#34d399}
.csv-import-btn{display:flex;align-items:center;gap:6px;padding:7px 14px;border-radius:8px;border:1px solid rgba(16,185,129,.4);background:rgba(16,185,129,.06);color:#10b981;font-family:var(--font-body);font-size:13px;font-weight:600;cursor:pointer;transition:all .15s}
.csv-import-btn:hover{background:rgba(16,185,129,.12);border-color:rgba(16,185,129,.7);box-shadow:0 0 12px rgba(16,185,129,.15)}
.csv-platform-chip{padding:5px 12px;border-radius:20px;background:rgba(16,185,129,.04);border:1px solid rgba(16,185,129,.15);color:var(--text-secondary);font-size:12px;font-family:var(--font-body);cursor:pointer;transition:all .15s;user-select:none}
.csv-platform-chip:hover{border-color:rgba(16,185,129,.4);color:var(--text-primary)}
.csv-platform-chip.selected{background:rgba(16,185,129,.16);border-color:#10b981;color:#10b981;font-weight:600;box-shadow:0 0 10px rgba(16,185,129,.15)}
.csv-notes-area{width:100%;min-height:72px;resize:vertical;padding:10px 12px;border-radius:8px;border:1px solid var(--border-medium);background:var(--bg-elevated);color:var(--text-primary);font-family:var(--font-body);font-size:13px;line-height:1.5;transition:border-color .15s;outline:none}
.csv-notes-area:focus{border-color:#10b981;box-shadow:0 0 0 2px rgba(16,185,129,.12)}
.csv-notes-area::placeholder{color:var(--text-tertiary)}

/* ANIMATIONS */
@keyframes spin{to{transform:rotate(360deg)}}
@keyframes float-dot{0%,100%{transform:translateY(0) translateX(0);opacity:.3}25%{transform:translateY(-30px) translateX(15px);opacity:.6}50%{transform:translateY(-10px) translateX(-20px);opacity:.3}75%{transform:translateY(20px) translateX(10px);opacity:.5}}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(1.4)}}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
@keyframes modalIn{from{opacity:0;transform:scale(.95) translateY(8px)}to{opacity:1;transform:scale(1) translateY(0)}}
@keyframes slideDown{from{opacity:0;transform:translateY(-8px)}to{opacity:1;transform:translateY(0)}}
@keyframes slideUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes countUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
@keyframes cardEntrance{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
@keyframes shimmer{to{background-position:200% center}}
@keyframes bounceIn{0%{transform:scale(0);opacity:0}60%{transform:scale(1.15)}100%{transform:scale(1);opacity:1}}
@keyframes glowPulse{0%,100%{box-shadow:0 0 8px rgba(16,185,129,0.3)}50%{box-shadow:0 0 20px rgba(16,185,129,0.6),0 0 40px rgba(16,185,129,0.2)}}
@keyframes milestoneHit{0%{box-shadow:0 0 0 0 rgba(16,185,129,0.5)}50%{box-shadow:0 0 12px 4px rgba(16,185,129,0.3)}100%{box-shadow:0 0 0 0 rgba(16,185,129,0)}}
.animate-in{animation:cardEntrance .4s var(--ease-smooth) both}
.animate-in-1{animation-delay:.05s}
.animate-in-2{animation-delay:.1s}
.animate-in-3{animation-delay:.15s}
.animate-in-4{animation-delay:.2s}
.animate-in-5{animation-delay:.25s}
.animate-in-6{animation-delay:.3s}

/* MOBILE */
.mobile-menu-btn{display:none;position:fixed;top:16px;left:16px;z-index:200;width:44px;height:44px;border-radius:10px;background:var(--bg-surface);border:1px solid var(--border-subtle);place-items:center;color:var(--text-secondary)}
.mobile-backdrop{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:90}

/* RESPONSIVE */
@media(max-width:1023px){
  .sidebar{position:fixed;left:0;top:0;z-index:100;width:var(--sidebar-collapsed)!important;min-width:var(--sidebar-collapsed)!important;padding:20px 10px}
  .sidebar .nav-btn{padding:0;justify-content:center}
  .sidebar .nav-btn span{opacity:0;width:0;overflow:hidden}
  .sidebar .sidebar-logo-text{opacity:0;width:0}
  .content-area{margin-left:var(--sidebar-collapsed);padding:24px 20px}
  .kpi-grid{grid-template-columns:repeat(auto-fit,minmax(180px,1fr))}
}
@media(max-width:767px){
  .sidebar{transform:translateX(-100%);width:var(--sidebar-w)!important;min-width:var(--sidebar-w)!important;padding:20px 16px;transition:transform .3s var(--ease-smooth)}
  .sidebar.mobile-open{transform:translateX(0)}
  .sidebar.mobile-open .nav-btn{padding:0 14px;justify-content:flex-start}
  .sidebar.mobile-open .nav-btn span{opacity:1;width:auto}
  .sidebar.mobile-open .sidebar-logo-text{opacity:1;width:auto}
  .mobile-menu-btn{display:grid}
  .mobile-backdrop.visible{display:block}
  .content-area{margin-left:0;padding:72px 16px 24px}
  .kpi-grid{grid-template-columns:1fr}
  .page-header{flex-direction:column}
  .page-header-actions{width:100%}
  .form-row{grid-template-columns:1fr}
  .modal-card{margin:8px;padding:20px}
  .data-table{display:block;overflow-x:auto}
}
</style>
</head>
<body>
<div id="orbit-root"></div>

<script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js" crossorigin></script>

<script type="text/babel">
const { useState, useEffect, useMemo, useCallback, useRef } = React;

/* ═══════════════ SVG ICONS ═══════════════ */
const OrbitIcons = {
  grid: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><rect x="3" y="3" width="7" height="7" rx="1.5"/><rect x="14" y="3" width="7" height="7" rx="1.5"/><rect x="3" y="14" width="7" height="7" rx="1.5"/><rect x="14" y="14" width="7" height="7" rx="1.5"/></svg>,
  wallet: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M19 7V5a2 2 0 00-2-2H5a2 2 0 00-2 2v14a2 2 0 002 2h12a2 2 0 002-2v-2"/><path d="M12 7h9v10h-9a1 1 0 01-1-1V8a1 1 0 011-1z"/><circle cx="16" cy="12" r="1"/></svg>,
  users: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><circle cx="9" cy="7" r="3.5"/><path d="M2 21v-2a4 4 0 014-4h6a4 4 0 014 4v2"/><circle cx="18" cy="8" r="2.5"/><path d="M20 21v-1.5a3 3 0 00-2-2.83"/></svg>,
  fileText: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="9" y1="13" x2="15" y2="13"/><line x1="9" y1="17" x2="13" y2="17"/></svg>,
  repeat: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M17 1l4 4-4 4"/><path d="M3 11V9a4 4 0 014-4h14"/><path d="M7 23l-4-4 4-4"/><path d="M21 13v2a4 4 0 01-4 4H3"/></svg>,
  shield: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M12 2l8 4v6c0 5.25-3.5 8.75-8 10-4.5-1.25-8-4.75-8-10V6l8-4z"/><path d="M9 12l2 2 4-4"/></svg>,
  calendar: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/><path d="M11 14h1v3"/></svg>,
  target: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="5"/><circle cx="12" cy="12" r="1"/></svg>,
  settings: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 01-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>,
  chevronLeft: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><polyline points="15 18 9 12 15 6"/></svg>,
  chevronRight: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><polyline points="9 6 15 12 9 18"/></svg>,
  plus: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" style={p.style}><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>,
  edit: (p) => <svg width={p.size||16} height={p.size||16} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M11 4H4a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 013 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>,
  trash: (p) => <svg width={p.size||16} height={p.size||16} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 01-2 2H8a2 2 0 01-2-2L5 6"/><path d="M10 11v6"/><path d="M14 11v6"/><path d="M9 6V4a1 1 0 011-1h4a1 1 0 011 1v2"/></svg>,
  x: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" style={p.style}><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>,
  search: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" style={p.style}><circle cx="11" cy="11" r="7"/><line x1="16.5" y1="16.5" x2="21" y2="21"/></svg>,
  filter: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" style={p.style}><polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"/></svg>,
  arrowUp: (p) => <svg width={p.size||14} height={p.size||14} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" style={p.style}><line x1="12" y1="19" x2="12" y2="5"/><polyline points="5 12 12 5 19 12"/></svg>,
  arrowDown: (p) => <svg width={p.size||14} height={p.size||14} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" style={p.style}><line x1="12" y1="5" x2="12" y2="19"/><polyline points="19 12 12 19 5 12"/></svg>,
  alertTriangle: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M10.29 3.86L1.82 18a2 2 0 001.71 3h16.94a2 2 0 001.71-3L13.71 3.86a2 2 0 00-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>,
  menu: (p) => <svg width={p.size||24} height={p.size||24} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" style={p.style}><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg>,
  check: (p) => <svg width={p.size||16} height={p.size||16} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" style={p.style}><polyline points="20 6 9 17 4 12"/></svg>,
  dollar: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><line x1="12" y1="1" x2="12" y2="23"/><path d="M17 5H9.5a3.5 3.5 0 000 7h5a3.5 3.5 0 010 7H6"/></svg>,
  trendingUp: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><polyline points="23 6 13.5 15.5 8.5 10.5 1 18"/><polyline points="17 6 23 6 23 12"/></svg>,
  clock: (p) => <svg width={p.size||16} height={p.size||16} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" style={p.style}><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>,
  orbit: (p) => <svg width={p.size||28} height={p.size||28} viewBox="0 0 32 32" fill="none" style={p.style}><circle cx="16" cy="16" r="5" fill="#7c3aed"/><ellipse cx="16" cy="16" rx="14" ry="6" stroke="#7c3aed" strokeWidth="1.5" transform="rotate(-20 16 16)" opacity="0.6"/><circle cx="26" cy="11" r="2" fill="#06b6d4" opacity="0.8"/></svg>,
  sun: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" style={p.style}><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg>,
  moon: (p) => <svg width={p.size||20} height={p.size||20} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" style={p.style}><path d="M21 12.79A9 9 0 1111.21 3 7 7 0 0021 12.79z"/></svg>,
};

/* ═══════════════ PLANET ICONS ═══════════════ */
const PlanetIcons = {
  command: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#7c3aed80'}}>
      <circle cx="12" cy="12" r="5.5" fill="#7c3aed"/><circle cx="10.5" cy="10.5" r="2.5" fill="#a78bfa" opacity="0.35"/>
      <ellipse cx="12" cy="12" rx="10.5" ry="2.8" stroke="#a78bfa" strokeWidth="1.2" opacity="0.5" transform="rotate(-25 12 12)"/>
      <circle cx="20" cy="8" r="1" fill="#c4b5fd" opacity="0.6"/>
    </svg>
  ),
  budget: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#10b98180'}}>
      <circle cx="12" cy="12" r="7" fill="#0369a1"/><circle cx="10" cy="10" r="3" fill="#10b981" opacity="0.6"/>
      <ellipse cx="14" cy="14" rx="3" ry="2" fill="#10b981" opacity="0.4" transform="rotate(30 14 14)"/>
      <circle cx="9" cy="9" r="4" fill="#38bdf8" opacity="0.15"/><circle cx="12" cy="12" r="7" fill="none" stroke="#34d399" strokeWidth="0.5" opacity="0.3"/>
    </svg>
  ),
  clients: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#ec489980'}}>
      <circle cx="12" cy="12" r="7" fill="#be185d"/><circle cx="10" cy="10" r="3.5" fill="#ec4899" opacity="0.4"/>
      <ellipse cx="14" cy="11" rx="4" ry="2.5" fill="#f9a8d4" opacity="0.15" transform="rotate(-15 14 11)"/>
      <circle cx="15" cy="9" r="1.5" fill="#fda4af" opacity="0.2"/>
    </svg>
  ),
  invoices: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#f59e0b80'}}>
      <circle cx="12" cy="12" r="5.5" fill="#f59e0b"/><circle cx="12" cy="12" r="7" fill="#f59e0b" opacity="0.15"/>
      <circle cx="12" cy="12" r="9" fill="#f59e0b" opacity="0.06"/><circle cx="10.5" cy="10.5" r="2" fill="#fde68a" opacity="0.4"/>
    </svg>
  ),
  subscriptions: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#06b6d480'}}>
      <circle cx="12" cy="12" r="7" fill="#0e7490"/><ellipse cx="12" cy="10" rx="6" ry="1" fill="#06b6d4" opacity="0.3"/>
      <ellipse cx="12" cy="13" rx="5" ry="0.8" fill="#22d3ee" opacity="0.2"/><circle cx="10" cy="9" r="3" fill="#06b6d4" opacity="0.25"/>
      <circle cx="15" cy="14" r="1" fill="#67e8f9" opacity="0.3"/>
    </svg>
  ),
  tax: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#fb923c80'}}>
      <circle cx="12" cy="12" r="7" fill="#c2410c"/><circle cx="10" cy="10" r="3" fill="#fb923c" opacity="0.35"/>
      <circle cx="15" cy="13" r="2" fill="#9a3412" opacity="0.4"/><circle cx="9" cy="14" r="1.2" fill="#7c2d12" opacity="0.5"/>
      <circle cx="14" cy="9" r="0.8" fill="#fed7aa" opacity="0.2"/>
    </svg>
  ),
  cashflow: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#0d948880'}}>
      <circle cx="12" cy="12" r="6" fill="#0f766e"/><circle cx="10.5" cy="10.5" r="2.5" fill="#0d9488" opacity="0.4"/>
      <ellipse cx="12" cy="12" rx="10" ry="1.5" stroke="#5eead4" strokeWidth="0.8" opacity="0.4" transform="rotate(75 12 12)"/>
      <circle cx="12" cy="12" r="6" fill="none" stroke="#2dd4bf" strokeWidth="0.4" opacity="0.3"/>
    </svg>
  ),
  goals: (s=20) => (
    <svg width={s} height={s} viewBox="0 0 24 24" fill="none" className="planet-icon" style={{'--planet-glow':'#f43f5e80'}}>
      <circle cx="12" cy="12" r="5" fill="#e11d48"/><circle cx="12" cy="12" r="7" fill="#f43f5e" opacity="0.15"/>
      <circle cx="12" cy="12" r="9" fill="#f43f5e" opacity="0.06"/><circle cx="10.5" cy="10.5" r="2" fill="#fda4af" opacity="0.35"/>
      <circle cx="14" cy="13" r="0.8" fill="#fecdd3" opacity="0.25"/>
    </svg>
  ),
};

/* ═══════════════ CURRENCY SYSTEM ═══════════════ */
const CURRENCIES = [
  { code: 'INR', symbol: '₹', name: 'Indian Rupee', locale: 'en-IN', rate: 1 },
  { code: 'USD', symbol: '$', name: 'US Dollar', locale: 'en-US', rate: 0.012 },
  { code: 'EUR', symbol: '€', name: 'Euro', locale: 'de-DE', rate: 0.011 },
  { code: 'GBP', symbol: '£', name: 'British Pound', locale: 'en-GB', rate: 0.0095 },
  { code: 'JPY', symbol: '¥', name: 'Japanese Yen', locale: 'ja-JP', rate: 1.82 },
  { code: 'AUD', symbol: 'A$', name: 'Australian Dollar', locale: 'en-AU', rate: 0.019 },
  { code: 'CAD', symbol: 'C$', name: 'Canadian Dollar', locale: 'en-CA', rate: 0.016 },
  { code: 'CHF', symbol: 'CHF', name: 'Swiss Franc', locale: 'de-CH', rate: 0.0106 },
  { code: 'CNY', symbol: '¥', name: 'Chinese Yuan', locale: 'zh-CN', rate: 0.087 },
  { code: 'SGD', symbol: 'S$', name: 'Singapore Dollar', locale: 'en-SG', rate: 0.016 },
  { code: 'AED', symbol: 'د.إ', name: 'UAE Dirham', locale: 'ar-AE', rate: 0.044 },
  { code: 'BRL', symbol: 'R$', name: 'Brazilian Real', locale: 'pt-BR', rate: 0.061 },
];

function formatCurrency(amount, currencyCode) {
  const cur = CURRENCIES.find(c => c.code === currencyCode) || CURRENCIES[0];
  /* No conversion — amounts are stored in the user's selected currency as-is */
  const decimals = cur.code === 'JPY' ? 0 : (amount >= 10000 ? 0 : 2);
  try {
    return new Intl.NumberFormat(cur.locale, {
      style: 'currency', currency: cur.code, minimumFractionDigits: decimals, maximumFractionDigits: decimals
    }).format(amount);
  } catch(e) {
    return cur.symbol + amount.toFixed(decimals);
  }
}

function formatCompact(amount, currencyCode) {
  const cur = CURRENCIES.find(c => c.code === currencyCode) || CURRENCIES[0];
  /* No conversion — amounts are stored in the user's selected currency as-is */
  if (amount >= 1000000) return cur.symbol + (amount/1000000).toFixed(1) + 'M';
  if (amount >= 1000) return cur.symbol + (amount/1000).toFixed(1) + 'K';
  return cur.symbol + Math.round(amount);
}

/* ═══════════════ MODULE DEFINITIONS ═══════════════ */
const MODULES = [
  { id: 'command', label: 'Command Center', icon: 'grid', accent: '#7c3aed', desc: 'Your mission overview — all systems at a glance' },
  { id: 'budget', label: 'Budget', icon: 'wallet', accent: '#10b981', desc: 'Track income and expenses across all platforms' },
  { id: 'clients', label: 'Clients', icon: 'users', accent: '#ec4899', desc: 'Manage your client relationships and history' },
  { id: 'invoices', label: 'Invoices', icon: 'fileText', accent: '#f59e0b', desc: 'Create, send, and track invoices' },
  { id: 'subscriptions', label: 'Subscriptions', icon: 'repeat', accent: '#06b6d4', desc: 'Monitor recurring costs and renewals' },
  { id: 'tax', label: 'Tax Reserve', icon: 'shield', accent: '#fb923c', desc: 'Set aside funds for tax obligations' },
  { id: 'cashflow', label: 'Cash Flow', icon: 'calendar', accent: '#0d9488', desc: 'Visualize money in and out over time' },
  { id: 'goals', label: 'Revenue Goals', icon: 'target', accent: '#f43f5e', desc: 'Set targets and track your trajectory' },
];
</script>

<script type="text/babel" data-plugins="transform-modules-umd">
/* ═══════════════ REUSABLE UI COMPONENTS ═══════════════ */
const { useState: _s, useEffect: _e, useMemo: _m, useCallback: _c, useRef: _r } = React;

const OrbitCard = ({ children, accent, className = '', style = {}, onClick }) => (
  <div className={`card ${accent ? 'card-accent' : ''} ${className}`}
    style={{ '--card-accent': accent, ...style }} onClick={onClick}>
    {children}
  </div>
);

const AnimatedNumber = ({ value, duration = 600, prefix = '', suffix = '' }) => {
  const [display, setDisplay] = React.useState(0);
  const ref = React.useRef(null);
  React.useEffect(() => {
    const end = typeof value === 'number' ? value : parseFloat(String(value).replace(/[^0-9.-]/g, '')) || 0;
    if (end === 0) { setDisplay(0); return; }
    const startTime = performance.now();
    const animate = (now) => {
      const elapsed = now - startTime;
      const progress = Math.min(elapsed / duration, 1);
      const eased = 1 - Math.pow(1 - progress, 3);
      setDisplay(Math.round(eased * end));
      if (progress < 1) ref.current = requestAnimationFrame(animate);
    };
    ref.current = requestAnimationFrame(animate);
    return () => ref.current && cancelAnimationFrame(ref.current);
  }, [value, duration]);
  return <span>{prefix}{display.toLocaleString()}{suffix}</span>;
};

const KPICard = ({ label, value, delta, deltaLabel, accent, pulse, animDelay = 0, rawNum }) => (
  <div className="card kpi-card animate-in" style={{ animationDelay: `${animDelay}s` }}>
    <div className="kpi-label">{label}</div>
    <div className="kpi-value" style={{ color: accent }}>
      {rawNum !== undefined ? <AnimatedNumber value={rawNum} duration={800}/> : value}
    </div>
    {delta !== undefined && delta !== null && (
      <div className={`kpi-delta ${delta >= 0 ? 'positive' : 'negative'}`}>
        {delta >= 0 ? <OrbitIcons.arrowUp size={14}/> : <OrbitIcons.arrowDown size={14}/>}
        {delta >= 0 ? '+' : ''}{delta}% {deltaLabel || 'vs last month'}
      </div>
    )}
    {pulse && <div className="kpi-pulse" style={{ background: accent || '#10b981' }}/>}
  </div>
);

const Badge = ({ variant = 'neutral', children }) => (
  <span className={`badge badge-${variant}`}>{children}</span>
);

const Btn = ({ variant = 'ghost', accent, children, onClick, style = {}, className = '', size }) => {
  const accentStyle = variant === 'primary' ? {
    background: accent || '#7c3aed',
    boxShadow: `0 0 16px ${accent || '#7c3aed'}4d`,
  } : {};
  return (
    <button className={`btn btn-${variant} ${size === 'sm' ? 'btn-sm' : ''} ${className}`}
      style={{ ...accentStyle, ...style }} onClick={onClick}>
      {children}
    </button>
  );
};

const IconBtn = ({ icon, onClick, title, style }) => {
  const I = OrbitIcons[icon];
  return (
    <button className="btn-icon" onClick={onClick} title={title} style={style}>
      {I && <I size={16}/>}
    </button>
  );
};

const FormGroup = ({ label, children }) => (
  <div className="form-group">
    {label && <label className="form-label">{label}</label>}
    {children}
  </div>
);

const AlertBanner = ({ type = 'warning', children, actions, onDismiss }) => {
  const colors = { danger: '#ef4444', warning: '#f59e0b', info: '#06b6d4', success: '#10b981' };
  const c = colors[type];
  return (
    <div className="alert-banner" style={{ background: `${c}0f`, border: `1px solid ${c}33` }}>
      <div className="alert-bar" style={{ background: c }}/>
      <OrbitIcons.alertTriangle size={18} style={{ color: c, flexShrink: 0 }}/>
      <div className="alert-text" style={{ color: '#e2e8f0' }}>{children}</div>
      <div className="alert-actions">
        {actions}
        {onDismiss && <IconBtn icon="x" onClick={onDismiss}/>}
      </div>
    </div>
  );
};

const SubTabs = ({ tabs, active, onChange, accent }) => (
  <div className="sub-tabs" style={{ '--tab-accent': accent }}>
    {tabs.map(t => (
      <button key={t.id} className={`sub-tab ${active === t.id ? 'active' : ''}`}
        style={active === t.id ? { background: `${accent}26`, borderColor: `${accent}4d` } : {}}
        onClick={() => onChange(t.id)}>
        {t.label}{t.count !== undefined ? ` (${t.count})` : ''}
      </button>
    ))}
  </div>
);

const ProgressBar = ({ value, max, accent, showMarkers }) => {
  const pct = Math.min((value / max) * 100, 100);
  return (
    <div className="progress-track">
      <div className="progress-fill" style={{
        width: `${pct}%`,
        background: `linear-gradient(90deg, ${accent}, ${accent}aa)`,
      }}/>
      {showMarkers && (
        <div className="progress-markers">
          {[25,50,75].map(m => <div key={m} className="progress-marker"/>)}
        </div>
      )}
    </div>
  );
};

const EmptyState = ({ icon, title, description, accent, onAction, actionLabel }) => (
  <div className="empty-state">
    <div className="empty-state-icon">
      <svg width="80" height="80" viewBox="0 0 80 80" fill="none">
        <ellipse cx="40" cy="40" rx="35" ry="14" stroke={accent || '#7c3aed'} strokeWidth="1" opacity="0.4"/>
        <ellipse cx="40" cy="40" rx="25" ry="10" stroke={accent || '#7c3aed'} strokeWidth="1" opacity="0.25"/>
        <circle cx="40" cy="40" r="4" fill={accent || '#7c3aed'} opacity="0.5"/>
      </svg>
    </div>
    <h3>{title}</h3>
    <p>{description}</p>
    {onAction && (
      <Btn variant="primary" accent={accent} onClick={onAction}>
        <OrbitIcons.plus size={16}/> {actionLabel || 'Get Started'}
      </Btn>
    )}
  </div>
);

const Modal = ({ title, onClose, children, width }) => (
  <div className="modal-overlay" onClick={(e) => e.target === e.currentTarget && onClose()}>
    <div className="modal-card" style={width ? { maxWidth: width } : {}}>
      <div className="modal-header">
        <h2>{title}</h2>
        <IconBtn icon="x" onClick={onClose}/>
      </div>
      {children}
    </div>
  </div>
);

const PageHeader = ({ module, accent, actions }) => {
  const IconComp = OrbitIcons[module.icon];
  return (
    <div className="page-header animate-in">
      <div>
        <div className="page-header-left">
          {IconComp && <div className="page-header-icon" style={{ color: accent }}><IconComp size={28}/></div>}
          <h1>{module.label}</h1>
        </div>
        <p style={{ marginTop: 4 }}>{module.desc}</p>
      </div>
      <div className="page-header-actions">{actions}</div>
    </div>
  );
};

const CurrencySelector = ({ value, onChange }) => (
  <select className="form-select" value={value} onChange={e => onChange(e.target.value)}
    style={{ width: 'auto', minWidth: 80, padding: '6px 32px 6px 10px', fontSize: 13, background: 'var(--bg-elevated)' }}>
    {CURRENCIES.map(c => (
      <option key={c.code} value={c.code}>{c.symbol} {c.code}</option>
    ))}
  </select>
);

const ConfirmDialog = ({ title, message, onConfirm, onCancel, danger }) => (
  <Modal title={title} onClose={onCancel} width="420px">
    <p style={{ color: 'var(--text-secondary)', fontSize: 14, lineHeight: 1.6 }}>{message}</p>
    <div className="modal-footer">
      <Btn variant="ghost" onClick={onCancel}>Cancel</Btn>
      <Btn variant={danger ? 'danger' : 'primary'} onClick={onConfirm}>
        {danger ? 'Delete' : 'Confirm'}
      </Btn>
    </div>
  </Modal>
);

const DataTable = ({ headers, children, footer }) => (
  <div className="table-wrap animate-in animate-in-2">
    <table className="data-table">
      <thead><tr>{headers.map((h, i) => (
        <th key={i} style={h.align ? { textAlign: h.align } : {}}>{h.label}</th>
      ))}</tr></thead>
      <tbody>{children}</tbody>
    </table>
    {footer && <div className="table-footer">{footer}</div>}
  </div>
);

const AVATAR_COLORS = ['#7c3aed','#10b981','#ec4899','#f59e0b','#06b6d4','#fb923c','#f43f5e','#0d9488'];
const AvatarCircle = ({ name, size = 36 }) => {
  const initials = (name || '?').split(' ').map(w => w[0]).join('').slice(0, 2).toUpperCase();
  const colorIdx = (name || '').charCodeAt(0) % AVATAR_COLORS.length;
  return (
    <div className="avatar" style={{
      width: size, height: size, fontSize: size * 0.38,
      background: `${AVATAR_COLORS[colorIdx]}22`,
      color: AVATAR_COLORS[colorIdx],
      border: `1px solid ${AVATAR_COLORS[colorIdx]}44`,
    }}>{initials}</div>
  );
};

const ArcGauge = ({ value, max, label, sublabel, size = 220 }) => {
  const pct = Math.min(value / (max || 1), 1);
  const r = size * 0.38;
  const cx = size / 2;
  const cy = size * 0.54;
  /* Single fixed semicircle path — left point to right point clockwise */
  const arcPath = `M ${cx - r} ${cy} A ${r} ${r} 0 0 1 ${cx + r} ${cy}`;
  /* Total arc length of semicircle = π * r */
  const arcLen = Math.PI * r;
  const filled = pct * arcLen;
  let gaugeColor = '#ef4444';
  if (pct > 0.7) gaugeColor = '#10b981';
  else if (pct > 0.4) gaugeColor = '#f59e0b';
  const sw = size * 0.07;
  const vH = size * 0.62;
  return (
    <div className="arc-gauge">
      <svg width={size} height={vH} viewBox={`0 0 ${size} ${vH}`} style={{ overflow: 'visible' }}>
        {/* Track — always full semicircle */}
        <path d={arcPath} fill="none" stroke="rgba(255,255,255,0.07)"
          strokeWidth={sw} strokeLinecap="round"/>
        {/* Filled — stroke-dasharray drives the animated fill */}
        <path d={arcPath} fill="none" stroke={gaugeColor}
          strokeWidth={sw} strokeLinecap="round"
          strokeDasharray={`${filled} ${arcLen}`}
          style={{ transition: 'stroke-dasharray 0.65s cubic-bezier(0.4,0,0.2,1), stroke 0.35s ease' }}/>
        {/* End-cap glow dot */}
        {pct > 0 && pct < 1 && (() => {
          const angle = Math.PI - pct * Math.PI;
          const ex = cx + r * Math.cos(angle);
          const ey = cy + r * Math.sin(angle);
          return <circle cx={ex} cy={ey} r={sw * 0.55} fill={gaugeColor} style={{ filter: `drop-shadow(0 0 4px ${gaugeColor})` }}/>;
        })()}
      </svg>
      <div className="arc-gauge-label" style={{ fontSize: size * 0.155, color: gaugeColor, marginTop: -(vH * 0.35) }}>
        {Math.round(pct * 100)}%
      </div>
      {label && <div style={{ fontSize: 14, color: 'var(--text-primary)', fontWeight: 500, marginTop: 6, textAlign: 'center' }}>{label}</div>}
      {sublabel && <div className="arc-gauge-sub">{sublabel}</div>}
    </div>
  );
};

const InlineForm = ({ accent, title, children, onSubmit, submitLabel }) => (
  <div className="inline-form" style={{ '--form-accent': accent }}>
    {title && <div className="kpi-label" style={{ marginBottom: 14 }}>{title}</div>}
    {children}
    {onSubmit && (
      <div style={{ display: 'flex', justifyContent: 'flex-end', marginTop: 16 }}>
        <Btn variant="primary" accent={accent} onClick={onSubmit}>
          <OrbitIcons.plus size={16}/> {submitLabel || 'Add'}
        </Btn>
      </div>
    )}
  </div>
);

/* Make all components globally available */
Object.assign(window, {
  OrbitCard, KPICard, Badge, Btn, IconBtn, FormGroup, AlertBanner,
  SubTabs, ProgressBar, EmptyState, Modal, PageHeader, CurrencySelector,
  ConfirmDialog, DataTable, AnimatedNumber, AvatarCircle, ArcGauge,
  InlineForm, AVATAR_COLORS,
});
</script>

<script type="text/babel" src="orbit-sidebar-inline.jsx" data-inline="true">
</script>

<script type="text/babel">
/* ═══════════════ SIDEBAR ═══════════════ */
const Sidebar = ({ activeModule, onModuleChange, collapsed, onToggleCollapse, mobileOpen, onCloseMobile, theme, onThemeToggle }) => {
  const [tooltip, setTooltip] = React.useState(null);
  const [tooltipPos, setTooltipPos] = React.useState({ top: 0 });
  const badges = { invoices: 2, subscriptions: 1 };

  const handleNavHover = React.useCallback((e, label) => {
    if (!collapsed) return;
    const rect = e.currentTarget.getBoundingClientRect();
    setTooltip(label);
    setTooltipPos({ top: rect.top + rect.height / 2 - 14 });
  }, [collapsed]);

  const handleNavLeave = React.useCallback(() => setTooltip(null), []);

  return (
    <>
      <div className={`mobile-backdrop ${mobileOpen ? 'visible' : ''}`} onClick={onCloseMobile}/>
      <aside className={`sidebar ${collapsed ? 'collapsed' : ''} ${mobileOpen ? 'mobile-open' : ''}`}>
        <div className="sidebar-logo">
          <div className="sidebar-logo-icon"><OrbitIcons.orbit size={28}/></div>
          <div className="sidebar-logo-text">
            <div className="sidebar-logo-name">ORBIT DESK</div>
            <div className="sidebar-logo-tagline">Mission Control</div>
          </div>
        </div>
        <div className="sidebar-divider"/>
        <nav className="sidebar-nav">
          {MODULES.map((mod) => {
            const isActive = activeModule === mod.id;
            const badgeCount = badges[mod.id];
            const PlanetRender = PlanetIcons[mod.id];
            return (
              <button key={mod.id}
                className={`nav-btn ${isActive ? 'active' : ''}`}
                onClick={() => { onModuleChange(mod.id); onCloseMobile(); }}
                onMouseEnter={(e) => handleNavHover(e, mod.label)}
                onMouseLeave={handleNavLeave}>
                <div className="accent-bar" style={{ background: mod.accent }}/>
                <div style={{ display: 'flex', alignItems: 'center', flexShrink: 0 }}>
                  {PlanetRender ? PlanetRender(20) : <OrbitIcons.grid size={20}/>}
                </div>
                <span>{mod.label}</span>
                {badgeCount && <div className="nav-badge">{badgeCount}</div>}
              </button>
            );
          })}
        </nav>
        <div className="sidebar-divider"/>
        <div className="sidebar-bottom">
          <button className="nav-btn" onClick={() => onThemeToggle()}
            onMouseEnter={(e) => handleNavHover(e, theme === 'dark' ? 'Light Mode' : 'Dark Mode')}
            onMouseLeave={handleNavLeave}>
            {theme === 'dark' ? <OrbitIcons.sun size={20}/> : <OrbitIcons.moon size={20}/>}
            <span>{theme === 'dark' ? 'Light Mode' : 'Dark Mode'}</span>
          </button>
          <button className="nav-btn" onClick={() => onModuleChange('settings')}
            onMouseEnter={(e) => handleNavHover(e, 'Settings')}
            onMouseLeave={handleNavLeave}>
            <OrbitIcons.settings size={20}/>
            <span>Settings</span>
          </button>
          <button className="nav-btn" onClick={onToggleCollapse}
            onMouseEnter={(e) => handleNavHover(e, collapsed ? 'Expand' : 'Collapse')}
            onMouseLeave={handleNavLeave}>
            {collapsed ? <OrbitIcons.chevronRight size={20}/> : <OrbitIcons.chevronLeft size={20}/>}
            <span>{collapsed ? 'Expand' : 'Collapse'}</span>
          </button>
        </div>
        {collapsed && tooltip && (
          <div className="sidebar-tooltip visible" style={{ top: tooltipPos.top }}>
            {tooltip}
          </div>
        )}
      </aside>
    </>
  );
};

const SettingsModal = ({ onClose, currency, onCurrencyChange, theme, onThemeToggle }) => (
  <Modal title="Settings" onClose={onClose} width="520px">
    <FormGroup label="Default Currency">
      <select className="form-select" value={currency}
        onChange={e => onCurrencyChange(e.target.value)}>
        {CURRENCIES.map(c => (
          <option key={c.code} value={c.code}>{c.symbol} {c.code} — {c.name}</option>
        ))}
      </select>
    </FormGroup>
    <FormGroup label="Theme">
      <div style={{ display: 'flex', gap: 10 }}>
        <button className={`btn btn-ghost ${theme === 'dark' ? 'btn-primary' : ''}`}
          style={theme === 'dark' ? { background: '#7c3aed' } : {}}
          onClick={() => onThemeToggle('dark')}>
          <OrbitIcons.moon size={16}/> Dark
        </button>
        <button className={`btn btn-ghost ${theme === 'light' ? 'btn-primary' : ''}`}
          style={theme === 'light' ? { background: '#7c3aed' } : {}}
          onClick={() => onThemeToggle('light')}>
          <OrbitIcons.sun size={16}/> Light
        </button>
      </div>
    </FormGroup>
    <FormGroup label="Display Name">
      <input className="form-input" placeholder="Your name or business name" defaultValue="Alex Rivera"/>
    </FormGroup>
    <FormGroup label="Tax Rate (%)">
      <input className="form-input" type="number" defaultValue="30" min="0" max="100"/>
    </FormGroup>
    <FormGroup label="Financial Year Start">
      <select className="form-select" defaultValue="april">
        <option value="january">January</option><option value="february">February</option>
        <option value="march">March</option><option value="april">April</option>
        <option value="may">May</option><option value="june">June</option>
        <option value="july">July</option><option value="august">August</option>
        <option value="september">September</option><option value="october">October</option>
        <option value="november">November</option><option value="december">December</option>
      </select>
    </FormGroup>
    <div className="modal-footer">
      <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
      <Btn variant="primary" accent="#7c3aed" onClick={onClose}>Save Settings</Btn>
    </div>
  </Modal>
);

Object.assign(window, { Sidebar, SettingsModal });
</script>

<script type="text/babel">
/* ═══════════════ COMMAND CENTER ═══════════════ */
const CommandCenter = ({ data, currency, onUpdate, onNavigate, cardClass }) => {
  const mod = MODULES[0];
  const { income, expenses, invoices, subscriptions, goals } = data;
  const totalIncome = income.reduce((s, e) => s + e.amount, 0);
  const totalExpenses = expenses.reduce((s, e) => s + e.amount, 0);
  const netProfit = totalIncome - totalExpenses;
  const overdueInvoices = invoices.filter(i => i.status === 'overdue');
  const overdueTotal = overdueInvoices.reduce((s, i) => s + i.amount, 0);
  const [alertsDismissed, setAlertsDismissed] = React.useState({});
  const dismissAlert = (key) => setAlertsDismissed(p => ({ ...p, [key]: true }));

  const expenseBreakdown = React.useMemo(() => {
    const cats = {};
    expenses.forEach(e => { cats[e.category] = (cats[e.category] || 0) + e.amount; });
    const total = Object.values(cats).reduce((s, v) => s + v, 0) || 1;
    return Object.entries(cats)
      .map(([cat, amt]) => ({ category: cat, amount: amt, pct: Math.round(amt / total * 100) }))
      .sort((a, b) => b.amount - a.amount);
  }, [expenses]);

  const breakdownColors = ['#7c3aed', '#06b6d4', '#ec4899', '#f59e0b', '#10b981', '#fb923c'];

  const monthlyData = React.useMemo(() => {
    const months = ['Dec','Jan','Feb','Mar','Apr','May'];
    const incVals = [95000, 110000, 88000, 72000, 125000, totalIncome];
    const expVals = [28000, 32000, 24000, 18000, 35000, totalExpenses];
    return months.map((m, i) => ({ month: m, income: incVals[i], expense: expVals[i] }));
  }, [totalIncome, totalExpenses]);
  const maxBar = Math.max(...monthlyData.map(d => d.income));

  const cc = cardClass || '';

  return (
    <div>
      {overdueInvoices.length > 0 && !alertsDismissed.overdue && (
        <AlertBanner type="danger" onDismiss={() => dismissAlert('overdue')}
          actions={<Btn size="sm" variant="ghost" onClick={() => onNavigate && onNavigate('invoices')}
            style={{ color: '#ef4444', borderColor: '#ef444466' }}>View ›</Btn>}>
          You have <strong>{overdueInvoices.length} overdue invoice{overdueInvoices.length > 1 ? 's' : ''}</strong> — <strong>{formatCurrency(overdueTotal, currency)}</strong> outstanding
        </AlertBanner>
      )}

      <div className="kpi-grid">
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.05s' }}>
          <div className="kpi-label">Revenue</div>
          <div className="kpi-value" style={{ color: '#10b981' }}>{formatCurrency(totalIncome, currency)}</div>
          <div className="kpi-delta positive"><OrbitIcons.arrowUp size={14}/> +12% this month</div>
          <div className="kpi-pulse" style={{ background: '#10b981' }}></div>
        </div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.1s' }}>
          <div className="kpi-label">Expenses</div>
          <div className="kpi-value" style={{ color: '#ef4444' }}>{formatCurrency(totalExpenses, currency)}</div>
          <div className="kpi-delta negative"><OrbitIcons.arrowUp size={14}/> +3% this month</div>
        </div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.15s' }}>
          <div className="kpi-label">Net Profit</div>
          <div className="kpi-value" style={{ color: '#06b6d4' }}>{formatCurrency(netProfit, currency)}</div>
          <div className="kpi-delta positive"><OrbitIcons.arrowUp size={14}/> +18% this month</div>
          <div className="kpi-pulse" style={{ background: '#06b6d4' }}></div>
        </div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.2s' }}>
          <div className="kpi-label">Overdue Invoices</div>
          <div className="kpi-value" style={{ color: overdueInvoices.length > 0 ? '#ef4444' : '#f59e0b' }}>
            {overdueInvoices.length}
          </div>
          <div style={{ fontSize: 13, color: 'var(--text-tertiary)', fontFamily: 'var(--font-mono)' }}>
            {formatCurrency(overdueTotal, currency)} total
          </div>
        </div>
      </div>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: 20, marginBottom: 24 }} className="cmd-charts-grid">
        <OrbitCard className={`animate-in animate-in-3 ${cc}`}>
          <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 20 }}>
            <div>
              <div className="kpi-label">Revenue vs Expenses</div>
              <div style={{ fontSize: 12, color: 'var(--text-tertiary)', marginTop: 2 }}>Last 6 months</div>
            </div>
            <div style={{ display: 'flex', gap: 14, fontSize: 11 }}>
              <span style={{ display: 'flex', alignItems: 'center', gap: 5, color: 'var(--text-secondary)' }}>
                <span style={{ width: 8, height: 8, borderRadius: 2, background: '#10b981', display: 'inline-block' }}></span> Income
              </span>
              <span style={{ display: 'flex', alignItems: 'center', gap: 5, color: 'var(--text-secondary)' }}>
                <span style={{ width: 8, height: 8, borderRadius: 2, background: '#ef4444', display: 'inline-block' }}></span> Expenses
              </span>
            </div>
          </div>
          <div style={{ display: 'flex', flexDirection: 'column', gap: 10 }}>
            {monthlyData.map((d, i) => (
              <div key={i} style={{ display: 'grid', gridTemplateColumns: '36px 1fr 70px', gap: 10, alignItems: 'center' }}>
                <span style={{ fontFamily: 'var(--font-mono)', fontSize: 12, color: 'var(--text-tertiary)' }}>{d.month}</span>
                <div style={{ position: 'relative', height: 20 }}>
                  <div style={{ position: 'absolute', top: 0, left: 0, height: 9, borderRadius: 4,
                    background: 'linear-gradient(90deg, #10b981, #10b981aa)',
                    width: `${(d.income / maxBar) * 100}%`, transition: 'width 0.6s cubic-bezier(0.4,0,0.2,1)', transitionDelay: `${i * 0.06}s` }}/>
                  <div style={{ position: 'absolute', top: 11, left: 0, height: 9, borderRadius: 4,
                    background: 'linear-gradient(90deg, #ef4444, #ef4444aa)',
                    width: `${(d.expense / maxBar) * 100}%`, transition: 'width 0.6s cubic-bezier(0.4,0,0.2,1)', transitionDelay: `${i * 0.06 + 0.03}s` }}/>
                </div>
                <span style={{ fontFamily: 'var(--font-mono)', fontSize: 12, color: 'var(--text-secondary)', textAlign: 'right' }}>
                  {formatCompact(d.income, currency)}
                </span>
              </div>
            ))}
          </div>
        </OrbitCard>

        <OrbitCard className={`animate-in animate-in-4 ${cc}`}>
          <div className="kpi-label" style={{ marginBottom: 20 }}>Expense Breakdown</div>
          {expenseBreakdown.length === 0 ? (
            <div style={{ color: 'var(--text-tertiary)', fontSize: 14, textAlign: 'center', padding: 30 }}>No expenses yet</div>
          ) : (
            <div style={{ display: 'flex', flexDirection: 'column', gap: 14 }}>
              {expenseBreakdown.map((item, i) => (
                <div key={item.category}>
                  <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: 6, fontSize: 13 }}>
                    <span style={{ color: 'var(--text-primary)', fontWeight: 500 }}>{item.category}</span>
                    <span style={{ fontFamily: 'var(--font-mono)', color: 'var(--text-secondary)' }}>{item.pct}%</span>
                  </div>
                  <div style={{ height: 8, background: 'var(--bg-elevated)', borderRadius: 4, overflow: 'hidden' }}>
                    <div style={{ height: '100%', borderRadius: 4, background: breakdownColors[i % breakdownColors.length],
                      width: `${item.pct}%`, transition: 'width 0.6s cubic-bezier(0.4,0,0.2,1)', transitionDelay: `${i * 0.08}s` }}/>
                  </div>
                </div>
              ))}
            </div>
          )}
        </OrbitCard>
      </div>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 340px', gap: 20, marginBottom: 24 }} className="cmd-bottom-grid">
        <OrbitCard className={`animate-in animate-in-5 ${cc}`}>
          <div className="kpi-label" style={{ marginBottom: 14 }}>Upcoming Payments <span style={{ fontWeight: 400, textTransform: 'none', letterSpacing: 0 }}>· Next 7 Days</span></div>
          <div style={{ display: 'flex', flexDirection: 'column', gap: 10 }}>
            {[
              { text: 'Adobe CC Renewal', date: 'May 22', amount: 4800, color: '#ef4444', type: 'payment' },
              { text: 'Notion Renewal', date: 'May 25', amount: 1200, color: '#06b6d4', type: 'payment' },
              { text: 'Tax Advance Q1', date: 'May 28', amount: 31000, color: '#fb923c', type: 'tax' },
            ].map((d, i) => (
              <div key={i} style={{ display: 'flex', alignItems: 'center', gap: 12, padding: '10px 14px',
                background: 'var(--bg-elevated)', borderRadius: 8, borderLeft: `3px solid ${d.color}` }}>
                <OrbitIcons.clock size={16} style={{ color: d.color, flexShrink: 0 }}/>
                <div style={{ flex: 1 }}>
                  <div style={{ fontSize: 14, fontWeight: 500, color: 'var(--text-primary)' }}>{d.text}</div>
                </div>
                <div style={{ fontFamily: 'var(--font-mono)', fontSize: 14, color: d.color }}>
                  -{formatCurrency(d.amount, currency)}
                </div>
                <Badge variant={d.type === 'tax' ? 'orange' : d.type === 'payment' ? 'danger' : 'info'}>{d.date}</Badge>
              </div>
            ))}
          </div>
        </OrbitCard>

        <div style={{ display: 'flex', flexDirection: 'column', gap: 16 }}>
          <OrbitCard className={`animate-in animate-in-5 ${cc}`}>
            <div className="kpi-label" style={{ marginBottom: 12 }}>Quick Actions</div>
            <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: 8 }}>
              {[
                { label: 'Log Income', icon: 'plus', accent: '#10b981', nav: 'budget' },
                { label: 'New Invoice', icon: 'fileText', accent: '#f59e0b', nav: 'invoices' },
                { label: 'Add Client', icon: 'users', accent: '#ec4899', nav: 'clients' },
                { label: 'View Goals', icon: 'target', accent: '#f43f5e', nav: 'goals' },
              ].map((qa, i) => {
                const QIcon = OrbitIcons[qa.icon];
                return (
                  <button key={i} style={{ display: 'flex', alignItems: 'center', gap: 8, padding: '11px 14px',
                    background: 'var(--bg-surface)', border: '1px solid var(--border-subtle)',
                    borderRadius: 8, cursor: 'pointer', fontSize: 13, fontWeight: 500,
                    color: 'var(--text-secondary)', transition: 'all .2s ease' }}
                  onClick={() => onNavigate && onNavigate(qa.nav)}
                  onMouseEnter={e => { e.currentTarget.style.borderColor = qa.accent + '66'; e.currentTarget.style.color = qa.accent; }}
                  onMouseLeave={e => { e.currentTarget.style.borderColor = ''; e.currentTarget.style.color = ''; }}>
                    {QIcon && <QIcon size={16} style={{ color: qa.accent }}/>}
                    {qa.label}
                  </button>
                );
              })}
            </div>
          </OrbitCard>

          {goals.length > 0 && (
            <OrbitCard accent="#f43f5e" className={`animate-in animate-in-6 ${cc}`}>
              <div className="kpi-label" style={{ marginBottom: 6 }}>Revenue Goal</div>
              <div style={{ fontWeight: 600, fontSize: 15, marginBottom: 4, color: 'var(--text-primary)' }}>
                {goals[0].name}
              </div>
              <div style={{ display: 'flex', justifyContent: 'space-between', fontSize: 13, marginBottom: 10, fontFamily: 'var(--font-mono)' }}>
                <span style={{ color: '#f43f5e' }}>{formatCurrency(goals[0].current, currency)}</span>
                <span style={{ color: 'var(--text-tertiary)' }}>{formatCurrency(goals[0].target, currency)}</span>
              </div>
              <ProgressBar value={goals[0].current} max={goals[0].target} accent="#f43f5e" showMarkers/>
              <div style={{ fontSize: 12, color: 'var(--text-tertiary)', marginTop: 8 }}>
                {Math.round(goals[0].current / goals[0].target * 100)}% achieved
              </div>
            </OrbitCard>
          )}
        </div>
      </div>

      <style>{`@media(max-width:900px){.cmd-charts-grid,.cmd-bottom-grid{grid-template-columns:1fr !important}}`}</style>
    </div>
  );
};

Object.assign(window, { CommandCenter });
</script>

<script type="text/babel" src="orbit-modules-a-inline.jsx" data-inline="true">
</script>

<script type="text/babel">
/* ═══════════════ CSV IMPORT FEATURE ═══════════════ */

/* ── Utility: parse CSV text ── */
function parseCSV(text) {
  text = text.replace(/^﻿/, ''); // strip BOM
  const lines = text.split(/\r?\n/).filter(l => l.trim());
  if (lines.length < 2) return { headers: [], rows: [] };
  const parseRow = (line) => {
    const result = []; let inQ = false; let cur = '';
    for (let i = 0; i < line.length; i++) {
      const c = line[i];
      if (c === '"') { if (inQ && line[i+1] === '"') { cur += '"'; i++; } else inQ = !inQ; }
      else if (c === ',' && !inQ) { result.push(cur.trim()); cur = ''; }
      else cur += c;
    }
    result.push(cur.trim());
    return result;
  };
  const headers = parseRow(lines[0]);
  const rows = [];
  for (let i = 1; i < lines.length; i++) {
    const vals = parseRow(lines[i]);
    if (!vals.length || vals.every(v => !v)) continue;
    const obj = {}; headers.forEach((h, j) => { obj[h] = (vals[j] || '').trim(); });
    rows.push(obj);
  }
  return { headers, rows };
}

function cleanAmount(raw, rate) {
  if (!raw) return 0;
  const n = parseFloat(String(raw).replace(/[^0-9.\-]/g, ''));
  if (isNaN(n) || n <= 0) return 0;
  return Math.round(n * (rate || 1));
}

function parseDate(raw) {
  if (!raw) return '';
  const s = String(raw).trim();
  if (/^\d{4}-\d{2}-\d{2}/.test(s)) return s.slice(0, 10);
  const parts = s.split(/[\/\-\.]/);
  if (parts.length === 3) {
    const [a, b, c] = parts;
    if (c.length === 4) return `${c}-${b.padStart(2,'0')}-${a.padStart(2,'0')}`;
    if (a.length === 4) return `${a}-${b.padStart(2,'0')}-${c.padStart(2,'0')}`;
  }
  const mo = {jan:1,feb:2,mar:3,apr:4,may:5,jun:6,jul:7,aug:8,sep:9,oct:10,nov:11,dec:12};
  const m = s.match(/([a-zA-Z]+)\s+(\d+),?\s+(\d{4})/);
  if (m) { const mn = mo[m[1].toLowerCase().slice(0,3)]; if (mn) return `${m[3]}-${String(mn).padStart(2,'0')}-${m[2].padStart(2,'0')}`; }
  return s.slice(0, 10);
}

function detectPlatform(headers) {
  const h = headers.map(x => x.toLowerCase());
  const has = (str) => h.some(x => x.includes(str));
  if (has('assignment name') || h.includes('amount earned'))
    return { name: 'Upwork', map: { description: 'Assignment Name', amount: 'Amount Earned', date: 'Date' }, platform: 'Upwork', category: 'Freelance' };
  if (has('order title') && has('revenue'))
    return { name: 'Fiverr', map: { description: 'Order Title', amount: 'Revenue', date: 'Order Date' }, platform: 'Fiverr', category: 'Freelance' };
  if (has('created (utc)'))
    return { name: 'Stripe', map: { description: 'Description', amount: 'Amount', date: 'Created (UTC)' }, platform: 'Stripe', category: 'Product Sale' };
  if (h.includes('gross'))
    return { name: 'PayPal', map: { description: 'Name', amount: 'Gross', date: 'Date' }, platform: 'PayPal', category: '' };
  if (has('amount paid') && has('payment date'))
    return { name: 'Razorpay', map: { description: 'Order ID', amount: 'Amount Paid', date: 'Payment Date' }, platform: 'Razorpay', category: '' };
  if (has('narration'))
    return { name: 'Bank CSV', map: { description: 'Narration', amount: 'Credit', date: 'Transaction Date' }, platform: 'Bank Transfer', category: '' };
  return null;
}

function autoMapGeneric(headers) {
  const auto = {}; const h = headers;
  h.forEach(col => {
    const l = col.toLowerCase();
    if (!auto.description && /desc|title|name|narration|subject/.test(l)) auto.description = col;
    if (!auto.amount && /amount|value|gross|credit|revenue|earned|paid/.test(l)) auto.amount = col;
    if (!auto.date && /date|time|created/.test(l)) auto.date = col;
    if (!auto.category && /category|type|kind/.test(l)) auto.category = col;
    if (!auto.platform && /platform|source|channel|method/.test(l)) auto.platform = col;
  });
  return auto;
}

/* Platform options for manual selector */
const PLATFORM_PRESETS = [
  { id: 'auto',     label: 'Auto-detect',  info: null },
  { id: 'upwork',   label: 'Upwork',       info: { name:'Upwork',   map:{description:'Assignment Name',amount:'Amount Earned',date:'Date'}, platform:'Upwork',   category:'Freelance'   } },
  { id: 'fiverr',   label: 'Fiverr',       info: { name:'Fiverr',   map:{description:'Order Title',    amount:'Revenue',       date:'Order Date'}, platform:'Fiverr',   category:'Freelance'   } },
  { id: 'stripe',   label: 'Stripe',       info: { name:'Stripe',   map:{description:'Description',   amount:'Amount',        date:'Created (UTC)'}, platform:'Stripe',  category:'Product Sale' } },
  { id: 'paypal',   label: 'PayPal',       info: { name:'PayPal',   map:{description:'Name',          amount:'Gross',         date:'Date'}, platform:'PayPal',   category:''            } },
  { id: 'razorpay', label: 'Razorpay',     info: { name:'Razorpay', map:{description:'Order ID',      amount:'Amount Paid',   date:'Payment Date'}, platform:'Razorpay', category:''            } },
  { id: 'bank',     label: 'Bank CSV',     info: { name:'Bank CSV', map:{description:'Narration',     amount:'Credit',        date:'Transaction Date'}, platform:'Bank Transfer', category:'' } },
  { id: 'generic',  label: 'Generic CSV',  info: null },
];

/* ── CSV Import Modal ── */
const CSVImportModal = ({ onClose, data, onUpdate, currency }) => {
  const [step, setStep] = React.useState(1);
  const [file, setFile] = React.useState(null);
  const [csvData, setCsvData] = React.useState(null);
  const [importType, setImportType] = React.useState('income');
  const [mapping, setMapping] = React.useState({ description: '', amount: '', date: '', category: '', platform: '', notes: '' });
  const [detected, setDetected] = React.useState(null);
  const [selectedPlatform, setSelectedPlatform] = React.useState('auto');
  const [batchNotes, setBatchNotes] = React.useState('');
  const [drag, setDrag] = React.useState(false);
  const [success, setSuccess] = React.useState(null);
  const fileRef = React.useRef();

  /* Apply mapping when platform selection changes (if file already loaded) */
  const applyMapping = React.useCallback((parsed, platformId) => {
    if (!parsed) return;
    let p = null;
    if (platformId === 'auto') {
      p = detectPlatform(parsed.headers);
    } else {
      const preset = PLATFORM_PRESETS.find(x => x.id === platformId);
      p = preset?.info || null;
    }
    setDetected(p);
    const baseMap = p
      ? Object.fromEntries(Object.entries(p.map).filter(([,col]) => parsed.headers.includes(col)))
      : autoMapGeneric(parsed.headers);
    setMapping(m => ({ description:'', amount:'', date:'', category:'', platform:'', notes:'', ...baseMap }));
  }, []);

  /* Re-apply mapping when platform selection changes after file loaded */
  React.useEffect(() => {
    if (csvData) applyMapping(csvData, selectedPlatform);
  }, [selectedPlatform, csvData, applyMapping]);

  const processFile = React.useCallback((f) => {
    if (!f || !f.name.toLowerCase().endsWith('.csv')) return;
    setFile(f);
    const reader = new FileReader();
    reader.onload = (e) => {
      const parsed = parseCSV(e.target.result);
      setCsvData(parsed);
      /* mapping will be applied by the useEffect above */
    };
    reader.readAsText(f);
  }, []);

  const previewRows = React.useMemo(() => {
    if (!csvData || !mapping.amount || !mapping.date) return [];
    return csvData.rows.map(row => {
      const desc = mapping.description ? row[mapping.description] || '' : '';
      const amt  = cleanAmount(row[mapping.amount] || '');
      const date = parseDate(row[mapping.date] || '');
      const cat  = mapping.category ? row[mapping.category] : (detected?.category || 'Other');
      const plat = mapping.platform ? row[mapping.platform] : (detected?.platform || '');
      const valid = !!desc && amt > 0 && !!date;
      const dup = valid && (data[importType] || []).some(e =>
        e.amount === amt && e.date === date && (e.description||'').toLowerCase() === desc.toLowerCase());
      return { desc, amt, date, cat, plat, valid, dup };
    });
  }, [csvData, mapping, detected, importType, data]);

  const validRows = previewRows.filter(r => r.valid && !r.dup);
  const invalidRows = previewRows.filter(r => !r.valid);
  const dupRows = previewRows.filter(r => r.dup);
  const total = validRows.reduce((s, r) => s + r.amt, 0);
  const dateRange = validRows.length ? validRows.map(r => r.date).sort()[0].slice(0,7) : '';

  const doImport = () => {
    const entries = validRows.map(r => ({
      id: Date.now() + Math.random(),
      date: r.date,
      description: r.desc,
      category: r.cat || 'Other',
      amount: r.amt,
      platform: r.plat || '',
      notes: batchNotes.trim(),
    }));
    onUpdate(importType, [...(data[importType] || []), ...entries]);
    setSuccess({ count: entries.length, total });
  };

  /* ── Success screen ── */
  if (success) return (
    <Modal title="" onClose={onClose} width="520px">
      <div style={{ textAlign: 'center', padding: '10px 0 6px' }}>
        <div className="csv-success-icon">✓</div>
        <div className="csv-particles">{Array.from({length:10}).map((_,i)=><div key={i} className={`csv-particle p${i}`}/>)}</div>
        <div style={{ fontFamily:'var(--font-display)', fontSize:22, color:'var(--text-primary)', marginTop:20 }}>Import Complete!</div>
        <div style={{ marginTop:12 }}>
          <div style={{ fontFamily:'var(--font-mono)', fontSize:20, color:'#10b981', fontWeight:700 }}>{success.count} entries added</div>
          <div style={{ fontFamily:'var(--font-mono)', fontSize:15, color:'#10b981', marginTop:4 }}>{formatCurrency(success.total, currency)} total imported</div>
        </div>
        <div style={{ fontSize:13, color:'var(--text-tertiary)', marginTop:8 }}>Your Budget Tracker has been updated.</div>
        <div style={{ display:'flex', gap:12, justifyContent:'center', marginTop:28 }}>
          <Btn variant="ghost" onClick={onClose}>View Budget Tracker</Btn>
          <Btn variant="primary" accent="#10b981" onClick={() => { setStep(1); setFile(null); setCsvData(null); setSuccess(null); setSelectedPlatform('auto'); setBatchNotes(''); setMapping({ description:'',amount:'',date:'',category:'',platform:'',notes:'' }); }}>Import Another File</Btn>
        </div>
      </div>
    </Modal>
  );

  return (
    <Modal title="" onClose={onClose} width="680px">
      {/* Step indicator */}
      <div className="csv-steps">
        {['Upload','Map Columns','Confirm'].map((lbl, i) => {
          const n = i+1; const done = step > n; const active = step === n;
          return (
            <React.Fragment key={n}>
              {i > 0 && <div className={`csv-step-line ${step > i ? 'active' : ''}`}/>}
              <div className="csv-step-item">
                <div className={`csv-step-dot${done?' done':active?' active':''}`}>{done ? '✓' : n}</div>
                <span className={`csv-step-label${active?' active':done?' done':''}`}>{lbl}</span>
              </div>
            </React.Fragment>
          );
        })}
      </div>

      {/* ── STEP 1: UPLOAD ── */}
      {step === 1 && (
        <div className="csv-step-content">
          <div style={{ marginBottom:18 }}>
            <div style={{ fontFamily:'var(--font-display)', fontSize:18, color:'var(--text-primary)', marginBottom:5 }}>↑ Import from CSV</div>
            <div style={{ fontSize:13, color:'var(--text-secondary)' }}>Upload a CSV file exported from any platform</div>
          </div>
          {/* Platform selector */}
          <div style={{ marginBottom:20 }}>
            <div style={{ fontSize:12, fontWeight:600, letterSpacing:'1px', color:'var(--text-tertiary)', textTransform:'uppercase', marginBottom:8 }}>Platform / Source</div>
            <div style={{ display:'flex', flexWrap:'wrap', gap:6 }}>
              {PLATFORM_PRESETS.map(p => (
                <button key={p.id} className={`csv-platform-chip${selectedPlatform===p.id?' selected':''}`}
                  onClick={() => setSelectedPlatform(p.id)}>
                  {selectedPlatform===p.id ? '● ' : ''}{p.label}
                </button>
              ))}
            </div>
            {selectedPlatform !== 'auto' && (
              <div style={{ fontSize:12, color:'#10b981', marginTop:8 }}>
                ✓ Columns will be pre-mapped for <strong>{PLATFORM_PRESETS.find(p=>p.id===selectedPlatform)?.label}</strong>
              </div>
            )}
          </div>
          {!file ? (
            <div className={`csv-dropzone${drag?' drag-over':''}`}
              onClick={() => fileRef.current.click()}
              onDragOver={e => { e.preventDefault(); setDrag(true); }}
              onDragLeave={() => setDrag(false)}
              onDrop={e => { e.preventDefault(); setDrag(false); processFile(e.dataTransfer.files[0]); }}>
              <div className="csv-upload-icon">↑</div>
              <div style={{ fontSize:15, fontWeight:600, color:'var(--text-primary)', marginTop:12 }}>Drop your CSV file here</div>
              <div style={{ fontSize:13, color:'var(--text-secondary)', marginTop:4 }}>or click to browse</div>
              <div style={{ fontSize:12, color:'var(--text-tertiary)', marginTop:8 }}>Supports: .csv files from any platform</div>
              <input ref={fileRef} type="file" accept=".csv" style={{ display:'none' }} onChange={e => processFile(e.target.files[0])}/>
            </div>
          ) : (
            <div className="csv-file-info">
              <span style={{ color:'#10b981', fontWeight:700 }}>✓</span>
              <span style={{ fontFamily:'var(--font-mono)', fontSize:13, color:'var(--text-primary)' }}>{file.name}</span>
              <span style={{ fontSize:12, color:'var(--text-secondary)', marginLeft:6 }}>
                {csvData?.rows?.length || 0} rows · {csvData?.headers?.length || 0} columns · {(file.size/1024).toFixed(0)} KB
              </span>
              <button className="csv-remove" onClick={() => { setFile(null); setCsvData(null); }}>×</button>
            </div>
          )}
          <div style={{ marginTop:22 }}>
            <div style={{ fontSize:13, color:'var(--text-secondary)', marginBottom:10 }}>What are you importing?</div>
            <div style={{ display:'flex', gap:10 }}>
              {['income','expenses'].map(t => (
                <button key={t} className={`csv-type-btn${importType===t?' active':''}`} onClick={() => setImportType(t)}>
                  {t==='income' ? '↑ Income entries' : '↓ Expense entries'}
                </button>
              ))}
            </div>
          </div>
          <div className="modal-footer" style={{ marginTop:26 }}>
            <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
            <Btn variant="primary" accent="#10b981" onClick={() => setStep(2)} disabled={!file || !csvData}>Next: Map Columns →</Btn>
          </div>
        </div>
      )}

      {/* ── STEP 2: MAP ── */}
      {step === 2 && csvData && (
        <div className="csv-step-content">
          <div style={{ marginBottom:14 }}>
            <div style={{ fontFamily:'var(--font-display)', fontSize:18, color:'var(--text-primary)', marginBottom:5 }}>⚙ Map Your Columns</div>
            <div style={{ fontSize:13, color:'var(--text-secondary)' }}>Tell us which columns match Orbit Desk fields</div>
          </div>
          <div className={`csv-detect-banner${detected?'':' warn'}`}>
            {detected ? `🟢 Detected: ${detected.name} CSV — columns pre-mapped for you` : '⚠ Platform not detected — please map the columns manually below'}
          </div>
          {/* CSV preview */}
          <div style={{ marginBottom:18 }}>
            <div style={{ fontSize:11, fontWeight:600, letterSpacing:'1px', color:'var(--text-tertiary)', textTransform:'uppercase', marginBottom:8 }}>Your CSV Data (first 3 rows)</div>
            <div style={{ overflowX:'auto', borderRadius:8, border:'1px solid var(--border-subtle)' }}>
              <table className="csv-preview-table">
                <thead><tr>{csvData.headers.map(h => <th key={h}>{h}</th>)}</tr></thead>
                <tbody>{csvData.rows.slice(0,3).map((row, i) => <tr key={i}>{csvData.headers.map(h => <td key={h}>{row[h]}</td>)}</tr>)}</tbody>
              </table>
            </div>
          </div>
          {/* Field mapping */}
          <div className="csv-mapping">
            {[{f:'description',l:'Description',req:true},{f:'amount',l:'Amount',req:true},{f:'date',l:'Date',req:true},{f:'category',l:'Category',req:false},{f:'platform',l:'Platform / Source',req:false},{f:'notes',l:'Notes',req:false}].map(({f,l,req}) => (
              <div key={f} className="csv-map-row">
                <div className="csv-map-label">{l}{req && <span style={{color:'#ef4444'}}> *</span>}</div>
                <div className="csv-map-arrow">←</div>
                <select className="form-select csv-map-select" value={mapping[f]} onChange={e => setMapping(m => ({...m,[f]:e.target.value}))}>
                  <option value="">-- skip --</option>
                  {csvData.headers.map(h => <option key={h} value={h}>{h}</option>)}
                </select>
              </div>
            ))}
          </div>
          <div className="modal-footer" style={{ marginTop:22 }}>
            <Btn variant="ghost" onClick={() => setStep(1)}>← Back</Btn>
            <Btn variant="primary" accent="#10b981" onClick={() => setStep(3)} disabled={!mapping.description || !mapping.amount || !mapping.date}>Next: Preview Import →</Btn>
          </div>
        </div>
      )}

      {/* ── STEP 3: CONFIRM ── */}
      {step === 3 && (
        <div className="csv-step-content">
          <div style={{ marginBottom:16 }}>
            <div style={{ fontFamily:'var(--font-display)', fontSize:18, color:'#10b981', marginBottom:5 }}>✓ Review Your Import</div>
            <div style={{ fontSize:13, color:'var(--text-secondary)' }}>{validRows.length} entries ready to import into Budget Tracker</div>
          </div>
          <div style={{ display:'grid', gridTemplateColumns:'repeat(3,1fr)', gap:12, marginBottom:18 }}>
            {[{l:'Entries',v:validRows.length},{l:'Total Value',v:formatCurrency(total,currency)},{l:'Date Range',v:dateRange||'—'}].map(s => (
              <div key={s.l} className="csv-stat-card">
                <div style={{ fontFamily:'var(--font-mono)', fontSize:20, color:'#10b981', fontWeight:700 }}>{s.v}</div>
                <div style={{ fontSize:12, color:'var(--text-tertiary)', marginTop:4 }}>{s.l}</div>
              </div>
            ))}
          </div>
          {invalidRows.length > 0 && <div className="csv-warn-banner">⚠ {invalidRows.length} row{invalidRows.length>1?'s':''} with missing required fields will be skipped. Importing {validRows.length} valid rows.</div>}
          {dupRows.length > 0 && <div className="csv-warn-banner">⚠ {dupRows.length} possible duplicate{dupRows.length>1?'s':''} detected and will be skipped.</div>}
          <div className="csv-preview-list">
            {previewRows.map((row, i) => (
              <div key={i} className={`csv-preview-row${!row.valid?' invalid':row.dup?' duplicate':''}`}>
                <span className="csv-row-icon">{!row.valid ? '⚠' : row.dup ? '⟳' : '✓'}</span>
                <span className="mono" style={{ fontSize:12, color:'var(--text-tertiary)', minWidth:78 }}>{row.date||'—'}</span>
                <span style={{ flex:1, fontSize:13, color:!row.valid?'#f59e0b':'var(--text-primary)', overflow:'hidden', textOverflow:'ellipsis', whiteSpace:'nowrap' }}>{row.desc||'[Missing description]'}</span>
                <span style={{ fontSize:12, color:'var(--text-tertiary)', marginRight:10, minWidth:80 }}>{row.cat}</span>
                <span style={{ fontFamily:'var(--font-mono)', fontSize:13, color:row.valid&&!row.dup?'#10b981':'var(--text-tertiary)', minWidth:80, textAlign:'right' }}>
                  {row.amt > 0 ? formatCurrency(row.amt, currency) : '—'}
                </span>
              </div>
            ))}
          </div>

          {/* Notes field */}
          <div style={{ marginTop:16, paddingTop:14, borderTop:'1px solid var(--border-divider)' }}>
            <div style={{ display:'flex', justifyContent:'space-between', alignItems:'center', marginBottom:8 }}>
              <div>
                <div style={{ fontSize:13, fontWeight:600, color:'var(--text-primary)' }}>Add Notes <span style={{ fontWeight:400, color:'var(--text-tertiary)' }}>(optional)</span></div>
                <div style={{ fontSize:12, color:'var(--text-tertiary)', marginTop:2 }}>This note will be saved to all {validRows.length} imported entries</div>
              </div>
              {batchNotes && <span style={{ fontSize:11, color:'#10b981' }}>✓ Will be saved</span>}
            </div>
            <textarea
              className="csv-notes-area"
              placeholder={`e.g., Upwork earnings ${new Date().toLocaleString('en-GB',{month:'long',year:'numeric'})}, imported from platform export...`}
              value={batchNotes}
              onChange={e => setBatchNotes(e.target.value)}
            />
          </div>

          <div className="modal-footer" style={{ marginTop:14 }}>
            <Btn variant="ghost" onClick={() => setStep(2)}>← Back</Btn>
            <Btn variant="primary" accent="#10b981" onClick={doImport} disabled={validRows.length === 0}>
              ↑ Import {validRows.length} Entr{validRows.length===1?'y':'ies'} →
            </Btn>
          </div>
        </div>
      )}
    </Modal>
  );
};
Object.assign(window, { CSVImportModal });
</script>

<script type="text/babel">
/* ═══════════════ BUDGET MODULE ═══════════════ */
const BudgetModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[1];
  const cc = cardClass || '';
  const [tab, setTab] = React.useState('income');
  const [confirm, setConfirm] = React.useState(null);
  const [editModal, setEditModal] = React.useState(null);
  const [showImport, setShowImport] = React.useState(false);
  const emptyForm = { description: '', amount: '', date: new Date().toISOString().split('T')[0], category: '', platform: '', notes: '' };
  const [form, setForm] = React.useState(emptyForm);
  const [error, setError] = React.useState('');
  const uf = (k, v) => { setForm(p => ({ ...p, [k]: v })); if (error) setError(''); };
  const incomeCats = ['Freelance', 'Consulting', 'Product Sale', 'Retainer', 'Passive Income', 'Other'];
  const expenseCats = ['Software/SaaS', 'Marketing', 'Hardware', 'Contractor', 'Office', 'Learning', 'Travel', 'Other'];
  const cats = tab === 'income' ? incomeCats : expenseCats;
  const items = tab === 'income' ? data.income : tab === 'expenses' ? data.expenses : [];
  const total = items.reduce((s, e) => s + e.amount, 0);
  const key = tab === 'income' ? 'income' : 'expenses';

  const handleAdd = () => {
    if (!form.description.trim()) { setError('Please enter a description'); return; }
    if (!form.amount || Number(form.amount) <= 0) { setError('Please enter a valid amount'); return; }
    setError('');
    onUpdate(key, [...data[key], { ...form, amount: Number(form.amount), id: Date.now() }]);
    setForm(emptyForm);
  };
  const handleEditSave = (entry) => { onUpdate(key, data[key].map(e => e.id === entry.id ? entry : e)); setEditModal(null); };
  const handleDelete = (id) => { onUpdate(key, data[key].filter(e => e.id !== id)); setConfirm(null); };

  const platforms = React.useMemo(() => {
    const map = {};
    data.income.forEach(e => {
      const p = e.platform || 'Direct';
      if (!map[p]) map[p] = { name: p, total: 0, count: 0, lastDate: '' };
      map[p].total += e.amount; map[p].count++;
      if (e.date > map[p].lastDate) map[p].lastDate = e.date;
    });
    const arr = Object.values(map).sort((a, b) => b.total - a.total);
    const grandTotal = arr.reduce((s, p) => s + p.total, 0) || 1;
    return arr.map(p => ({ ...p, pct: Math.round(p.total / grandTotal * 100) }));
  }, [data.income]);
  const platformColors = ['#10b981', '#7c3aed', '#06b6d4', '#ec4899', '#f59e0b', '#fb923c'];

  return (
    <div>
      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 20, flexWrap: 'wrap', gap: 12 }}>
        <SubTabs accent={mod.accent} tabs={[
          { id: 'income', label: 'Income', count: data.income.length },
          { id: 'expenses', label: 'Expenses', count: data.expenses.length },
          { id: 'platforms', label: 'Platforms' },
        ]} active={tab} onChange={setTab}/>
        <button className="csv-import-btn" onClick={() => setShowImport(true)}>
          <span style={{ fontSize:15 }}>↑</span> Import CSV
        </button>
      </div>
      {showImport && <CSVImportModal onClose={() => setShowImport(false)} data={data} onUpdate={onUpdate} currency={currency}/>}

      {tab === 'platforms' ? (
        <div>
          {platforms.length === 0 ? (
            <EmptyState accent={mod.accent} title="No platform data" description="Add income entries with a platform/source to see breakdown here"/>
          ) : (
            <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(280px, 1fr))', gap: 16 }}>
              {platforms.map((p, i) => (
                <OrbitCard key={p.name} className={`animate-in animate-in-${i % 6 + 1} ${cc}`}
                  style={{ borderTop: `3px solid ${platformColors[i % platformColors.length]}` }}>
                  <div style={{ fontWeight: 600, fontSize: 16, color: 'var(--text-primary)', marginBottom: 4 }}>{p.name}</div>
                  <div style={{ fontFamily: 'var(--font-mono)', fontSize: 24, color: platformColors[i % platformColors.length], marginBottom: 8 }}>
                    {formatCurrency(p.total, currency)}
                  </div>
                  <div style={{ fontSize: 13, color: 'var(--text-tertiary)', marginBottom: 4 }}>{p.count} transaction{p.count !== 1 ? 's' : ''}</div>
                  <div style={{ fontSize: 12, color: 'var(--text-tertiary)', marginBottom: 12 }}>
                    Last: {new Date(p.lastDate).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}
                  </div>
                  <div style={{ height: 6, background: 'var(--bg-elevated)', borderRadius: 3, overflow: 'hidden' }}>
                    <div style={{ height: '100%', borderRadius: 3, width: `${p.pct}%`,
                      background: platformColors[i % platformColors.length], transition: 'width 0.6s cubic-bezier(0.4,0,0.2,1)' }}/>
                  </div>
                  <div style={{ fontSize: 11, color: 'var(--text-tertiary)', marginTop: 6, textAlign: 'right', fontFamily: 'var(--font-mono)' }}>{p.pct}%</div>
                </OrbitCard>
              ))}
            </div>
          )}
        </div>
      ) : (
        <div>
          <InlineForm accent={tab === 'income' ? '#10b981' : '#ef4444'}
            title={`Add New ${tab === 'income' ? 'Income' : 'Expense'}`}
            onSubmit={handleAdd} submitLabel={`Add ${tab === 'income' ? 'Income' : 'Expense'}`}>
            <FormGroup label="Description">
              <input className="form-input" placeholder={tab === 'income' ? 'e.g. Freelance project' : 'e.g. Figma Pro subscription'}
                value={form.description} onChange={e => uf('description', e.target.value)}/>
            </FormGroup>
            <div className="form-grid">
              <FormGroup label="Amount"><input className="form-input" type="number" placeholder="0" value={form.amount} onChange={e => uf('amount', e.target.value)}/></FormGroup>
              <FormGroup label="Date"><input className="form-input" type="date" value={form.date} onChange={e => uf('date', e.target.value)}/></FormGroup>
              <FormGroup label="Category">
                <select className="form-select" value={form.category} onChange={e => uf('category', e.target.value)}>
                  <option value="">Select...</option>
                  {cats.map(c => <option key={c} value={c}>{c}</option>)}
                </select>
              </FormGroup>
              {tab === 'income' ? (
                <FormGroup label="Platform / Source"><input className="form-input" placeholder='e.g. Upwork, Direct' value={form.platform} onChange={e => uf('platform', e.target.value)}/></FormGroup>
              ) : (
                <FormGroup label="Notes"><input className="form-input" placeholder="Optional notes" value={form.notes} onChange={e => uf('notes', e.target.value)}/></FormGroup>
              )}
            </div>
            {error && <div style={{ color: '#ef4444', fontSize: 13, marginTop: 12, padding: '8px 12px', background: 'rgba(239,68,68,0.08)', border: '1px solid rgba(239,68,68,0.25)', borderRadius: 6 }}>{error}</div>}
          </InlineForm>

          {items.length === 0 ? (
            <EmptyState accent={mod.accent} title={`No ${tab} entries yet`} description={`Use the form above to add your first ${tab} entry`}/>
          ) : (
            <DataTable headers={[
              { label: 'Date' }, { label: 'Description' }, { label: 'Category' },
              ...(tab === 'income' ? [{ label: 'Platform' }] : []),
              { label: 'Amount', align: 'right' }, { label: '', align: 'right' }
            ]} footer={
              <><span style={{ color: 'var(--text-secondary)' }}>Total: {items.length} entries</span>
              <span style={{ color: tab === 'income' ? '#10b981' : '#ef4444', fontWeight: 600 }}>{formatCurrency(total, currency)}</span></>
            }>
              {items.map(item => (
                <tr key={item.id}>
                  <td className="mono" style={{ fontSize: 13, color: 'var(--text-tertiary)', whiteSpace: 'nowrap' }}>
                    {new Date(item.date).toLocaleDateString('en-GB', { day: '2-digit', month: 'short', year: '2-digit' })}
                  </td>
                  <td style={{ color: 'var(--text-primary)', fontWeight: 500 }}>{item.description}</td>
                  <td><Badge variant="neutral">{item.category}</Badge></td>
                  {tab === 'income' && <td style={{ color: 'var(--text-secondary)', fontSize: 13 }}>{item.platform || 'Direct'}</td>}
                  <td className="amount" style={{ color: tab === 'income' ? '#10b981' : '#ef4444' }}>{formatCurrency(item.amount, currency)}</td>
                  <td style={{ textAlign: 'right' }}>
                    <div className="table-actions" style={{ justifyContent: 'flex-end' }}>
                      <IconBtn icon="edit" onClick={() => setEditModal(item)}/>
                      <IconBtn icon="trash" onClick={() => setConfirm(item.id)}/>
                    </div>
                  </td>
                </tr>
              ))}
            </DataTable>
          )}
        </div>
      )}

      {editModal && <BudgetEditModal tab={tab} entry={editModal} cats={cats} onSave={handleEditSave} onClose={() => setEditModal(null)} accent={mod.accent}/>}
      {confirm && <ConfirmDialog title="Delete Entry" message="Are you sure? This cannot be undone." danger onConfirm={() => handleDelete(confirm)} onCancel={() => setConfirm(null)}/>}
    </div>
  );
};

const BudgetEditModal = ({ tab, entry, cats, onSave, onClose, accent }) => {
  const [f, setF] = React.useState({ ...entry, amount: String(entry.amount) });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  return (
    <Modal title="Edit Entry" onClose={onClose}>
      <FormGroup label="Description"><input className="form-input" value={f.description} onChange={e => u('description', e.target.value)}/></FormGroup>
      <div className="form-row">
        <FormGroup label="Amount"><input className="form-input" type="number" value={f.amount} onChange={e => u('amount', e.target.value)}/></FormGroup>
        <FormGroup label="Date"><input className="form-input" type="date" value={f.date} onChange={e => u('date', e.target.value)}/></FormGroup>
      </div>
      <FormGroup label="Category">
        <select className="form-select" value={f.category} onChange={e => u('category', e.target.value)}>
          <option value="">Select...</option>
          {cats.map(c => <option key={c} value={c}>{c}</option>)}
        </select>
      </FormGroup>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, amount: Number(f.amount) || 0 })}>Update</Btn>
      </div>
    </Modal>
  );
};

Object.assign(window, { BudgetModule, BudgetEditModal });
</script>

<script type="text/babel">
/* ═══════════════ CLIENTS MODULE ═══════════════ */
const ClientsModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[2];
  const cc = cardClass || '';
  const [tab, setTab] = React.useState('clients');
  const [modal, setModal] = React.useState(null);
  const [confirm, setConfirm] = React.useState(null);
  const [search, setSearch] = React.useState('');

  const filteredClients = data.clients.filter(c =>
    c.name.toLowerCase().includes(search.toLowerCase()) ||
    (c.company || '').toLowerCase().includes(search.toLowerCase())
  );

  const handleSaveClient = (client) => {
    if (modal.type === 'edit') onUpdate('clients', data.clients.map(c => c.id === client.id ? client : c));
    else onUpdate('clients', [...data.clients, { ...client, id: Date.now(), totalBilled: 0 }]);
    setModal(null);
  };
  const handleSaveProject = (project) => {
    if (modal.type === 'edit') onUpdate('projects', data.projects.map(p => p.id === project.id ? project : p));
    else onUpdate('projects', [...data.projects, { ...project, id: Date.now() }]);
    setModal(null);
  };

  const statusColors = { active: 'success', inactive: 'neutral', prospect: 'info', lead: 'info', churned: 'danger' };
  const projStatusColors = { 'in-progress': 'info', completed: 'success', 'on-hold': 'orange', cancelled: 'danger' };

  return (
    <div>
      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 20, flexWrap: 'wrap', gap: 12 }}>
        <SubTabs accent={mod.accent} tabs={[
          { id: 'clients', label: 'Clients', count: data.clients.length },
          { id: 'projects', label: 'Projects', count: (data.projects || []).length },
        ]} active={tab} onChange={setTab}/>
        <Btn variant="primary" accent={mod.accent} onClick={() => setModal({ type: 'add' })}>
          <OrbitIcons.plus size={16}/> Add {tab === 'clients' ? 'Client' : 'Project'}
        </Btn>
      </div>

      {tab === 'clients' ? (
        <div>
          <div style={{ marginBottom: 20, position: 'relative', maxWidth: 360 }}>
            <OrbitIcons.search size={16} style={{ position: 'absolute', left: 12, top: 11, color: 'var(--text-tertiary)' }}/>
            <input className="form-input" placeholder="Search clients..." value={search}
              onChange={e => setSearch(e.target.value)} style={{ paddingLeft: 36 }}/>
          </div>
          {filteredClients.length === 0 ? (
            <EmptyState accent={mod.accent} title="No clients found" description="Add your first client to start tracking relationships"
              actionLabel="Add Client" onAction={() => setModal({ type: 'add' })}/>
          ) : (
            <DataTable headers={[
              { label: '' }, { label: 'Name' }, { label: 'Industry' }, { label: 'Status' },
              { label: 'Projects' }, { label: 'Total Earned', align: 'right' }, { label: '', align: 'right' }
            ]}>
              {filteredClients.map(c => {
                const projCount = (data.projects || []).filter(p => p.clientId === c.id).length;
                return (
                  <tr key={c.id}>
                    <td style={{ width: 44 }}><AvatarCircle name={c.name} size={32}/></td>
                    <td>
                      <div style={{ fontWeight: 500, color: 'var(--text-primary)' }}>{c.name}</div>
                      <div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>{c.email}</div>
                    </td>
                    <td style={{ fontSize: 13, color: 'var(--text-secondary)' }}>{c.industry || c.company || '—'}</td>
                    <td><Badge variant={statusColors[c.status] || 'neutral'}>{c.status}</Badge></td>
                    <td style={{ fontFamily: 'var(--font-mono)', fontSize: 13 }}>{projCount}</td>
                    <td className="amount" style={{ color: mod.accent }}>{formatCurrency(c.totalBilled, currency)}</td>
                    <td style={{ textAlign: 'right' }}>
                      <div className="table-actions" style={{ justifyContent: 'flex-end' }}>
                        <IconBtn icon="edit" onClick={() => setModal({ type: 'edit', entry: c })}/>
                        <IconBtn icon="trash" onClick={() => setConfirm({ type: 'client', id: c.id })}/>
                      </div>
                    </td>
                  </tr>
                );
              })}
            </DataTable>
          )}
        </div>
      ) : (
        <div>
          {(data.projects || []).length === 0 ? (
            <EmptyState accent={mod.accent} title="No projects yet" description="Add projects linked to your clients"
              actionLabel="Add Project" onAction={() => setModal({ type: 'add' })}/>
          ) : (
            <DataTable headers={[
              { label: 'Project' }, { label: 'Client' }, { label: 'Status' },
              { label: 'Budget', align: 'right' }, { label: 'Timeline' }, { label: '', align: 'right' }
            ]}>
              {data.projects.map(p => {
                const client = data.clients.find(c => c.id === p.clientId);
                const now = new Date(); const start = new Date(p.startDate); const end = new Date(p.endDate);
                const totalDays = Math.max((end - start) / 86400000, 1);
                const elapsed = Math.min(Math.max((now - start) / 86400000, 0), totalDays);
                const pct = Math.round(elapsed / totalDays * 100);
                return (
                  <tr key={p.id}>
                    <td style={{ fontWeight: 500, color: 'var(--text-primary)' }}>{p.name}</td>
                    <td>
                      <div style={{ display: 'flex', alignItems: 'center', gap: 8 }}>
                        {client && <AvatarCircle name={client.name} size={24}/>}
                        <span style={{ fontSize: 13 }}>{client ? client.name : 'Unknown'}</span>
                      </div>
                    </td>
                    <td><Badge variant={projStatusColors[p.status] || 'neutral'}>{p.status}</Badge></td>
                    <td className="amount">{formatCurrency(p.budget, currency)}</td>
                    <td style={{ minWidth: 120 }}>
                      <div className="timeline-bar">
                        <div className="timeline-fill" style={{ width: `${pct}%`, background: p.status === 'completed' ? '#10b981' : mod.accent }}/>
                      </div>
                      <div style={{ fontSize: 11, color: 'var(--text-tertiary)', marginTop: 4, fontFamily: 'var(--font-mono)' }}>
                        {new Date(p.startDate).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })} → {new Date(p.endDate).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}
                      </div>
                    </td>
                    <td style={{ textAlign: 'right' }}>
                      <div className="table-actions" style={{ justifyContent: 'flex-end' }}>
                        <IconBtn icon="edit" onClick={() => setModal({ type: 'edit', entry: p })}/>
                        <IconBtn icon="trash" onClick={() => setConfirm({ type: 'project', id: p.id })}/>
                      </div>
                    </td>
                  </tr>
                );
              })}
            </DataTable>
          )}
        </div>
      )}

      {modal && tab === 'clients' && <ClientFormModal entry={modal.entry} onSave={handleSaveClient} onClose={() => setModal(null)} accent={mod.accent}/>}
      {modal && tab === 'projects' && <ProjectFormModal entry={modal.entry} clients={data.clients} onSave={handleSaveProject} onClose={() => setModal(null)} accent={mod.accent}/>}
      {confirm && <ConfirmDialog title={`Delete ${confirm.type}`} message="This action cannot be undone." danger
        onConfirm={() => { if (confirm.type === 'client') onUpdate('clients', data.clients.filter(c => c.id !== confirm.id)); else onUpdate('projects', data.projects.filter(p => p.id !== confirm.id)); setConfirm(null); }}
        onCancel={() => setConfirm(null)}/>}
    </div>
  );
};

const ClientFormModal = ({ entry, onSave, onClose, accent }) => {
  const [f, setF] = React.useState(entry || { name: '', email: '', company: '', phone: '', industry: '', status: 'active', notes: '' });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  return (
    <Modal title={entry ? 'Edit Client' : 'Add Client'} onClose={onClose}>
      <FormGroup label="Client Name"><input className="form-input" value={f.name} onChange={e => u('name', e.target.value)} placeholder="Full name"/></FormGroup>
      <div className="form-row">
        <FormGroup label="Email"><input className="form-input" type="email" value={f.email} onChange={e => u('email', e.target.value)}/></FormGroup>
        <FormGroup label="Phone"><input className="form-input" value={f.phone} onChange={e => u('phone', e.target.value)}/></FormGroup>
      </div>
      <div className="form-row">
        <FormGroup label="Company"><input className="form-input" value={f.company} onChange={e => u('company', e.target.value)}/></FormGroup>
        <FormGroup label="Industry"><input className="form-input" value={f.industry || ''} onChange={e => u('industry', e.target.value)} placeholder="e.g. Technology"/></FormGroup>
      </div>
      <FormGroup label="Status">
        <select className="form-select" value={f.status} onChange={e => u('status', e.target.value)}>
          <option value="active">Active</option><option value="inactive">Inactive</option>
          <option value="prospect">Prospect</option><option value="churned">Churned</option>
        </select>
      </FormGroup>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave(f)}>{entry ? 'Update' : 'Add Client'}</Btn>
      </div>
    </Modal>
  );
};

const ProjectFormModal = ({ entry, clients, onSave, onClose, accent }) => {
  const [f, setF] = React.useState(entry || { name: '', clientId: '', startDate: '', endDate: '', budget: '', status: 'in-progress', notes: '' });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  return (
    <Modal title={entry ? 'Edit Project' : 'Add Project'} onClose={onClose}>
      <FormGroup label="Project Name"><input className="form-input" value={f.name} onChange={e => u('name', e.target.value)}/></FormGroup>
      <div className="form-row">
        <FormGroup label="Client">
          <select className="form-select" value={f.clientId} onChange={e => u('clientId', Number(e.target.value))}>
            <option value="">Select client...</option>
            {clients.map(c => <option key={c.id} value={c.id}>{c.name}</option>)}
          </select>
        </FormGroup>
        <FormGroup label="Budget"><input className="form-input" type="number" value={f.budget} onChange={e => u('budget', e.target.value)}/></FormGroup>
      </div>
      <div className="form-row">
        <FormGroup label="Start Date"><input className="form-input" type="date" value={f.startDate} onChange={e => u('startDate', e.target.value)}/></FormGroup>
        <FormGroup label="End Date"><input className="form-input" type="date" value={f.endDate} onChange={e => u('endDate', e.target.value)}/></FormGroup>
      </div>
      <FormGroup label="Status">
        <select className="form-select" value={f.status} onChange={e => u('status', e.target.value)}>
          <option value="in-progress">In Progress</option><option value="completed">Completed</option>
          <option value="on-hold">On Hold</option><option value="cancelled">Cancelled</option>
        </select>
      </FormGroup>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, budget: Number(f.budget) || 0 })}>{entry ? 'Update' : 'Add'}</Btn>
      </div>
    </Modal>
  );
};

Object.assign(window, { ClientsModule, ClientFormModal, ProjectFormModal });
</script>

<script type="text/babel">
/* ═══════════════ INVOICES MODULE ═══════════════ */
const InvoicesModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[3]; const cc = cardClass || '';
  const [tab, setTab] = React.useState('all');
  const [modal, setModal] = React.useState(null);
  const [confirm, setConfirm] = React.useState(null);

  const invoices = React.useMemo(() => {
    const today = new Date().toISOString().split('T')[0];
    return data.invoices.map(inv => inv.status === 'sent' && inv.dueDate < today ? { ...inv, status: 'overdue' } : inv);
  }, [data.invoices]);

  const tabs = [
    { id: 'all', label: 'All', count: invoices.length },
    { id: 'draft', label: 'Draft', count: invoices.filter(i => i.status === 'draft').length },
    { id: 'sent', label: 'Sent', count: invoices.filter(i => i.status === 'sent').length },
    { id: 'paid', label: 'Paid', count: invoices.filter(i => i.status === 'paid').length },
    { id: 'overdue', label: 'Overdue', count: invoices.filter(i => i.status === 'overdue').length },
  ];
  const filtered = tab === 'all' ? invoices : invoices.filter(i => i.status === tab);
  const totalSent = invoices.filter(i => i.status === 'sent' || i.status === 'overdue').reduce((s, i) => s + i.amount, 0);
  const totalPaid = invoices.filter(i => i.status === 'paid').reduce((s, i) => s + i.amount, 0);
  const totalOverdue = invoices.filter(i => i.status === 'overdue').reduce((s, i) => s + i.amount, 0);
  const statusColors = { paid: 'success', sent: 'info', draft: 'neutral', overdue: 'danger' };

  const getDaysInfo = (inv) => {
    if (inv.status === 'paid' || inv.status === 'draft') return null;
    const diff = Math.ceil((new Date(inv.dueDate) - new Date()) / 86400000);
    if (diff < 0) return { text: `${Math.abs(diff)}d overdue`, color: '#ef4444', bold: true };
    if (diff === 0) return { text: 'Due today', color: '#f59e0b', bold: true };
    return { text: `${diff}d remaining`, color: '#10b981', bold: false };
  };

  const handleSave = (inv) => {
    if (modal.type === 'edit') onUpdate('invoices', data.invoices.map(i => i.id === inv.id ? inv : i));
    else { const num = `INV-${String(data.invoices.length + 1).padStart(3, '0')}`; onUpdate('invoices', [...data.invoices, { ...inv, id: Date.now(), number: num }]); }
    setModal(null);
  };
  const markPaid = (id) => onUpdate('invoices', data.invoices.map(i => i.id === id ? { ...i, status: 'paid' } : i));

  return (
    <div>
      <div className="kpi-grid" style={{ marginBottom: 20 }}>
        <div className={`card kpi-card animate-in ${cc}`}>
          <div className="kpi-label">Outstanding</div>
          <div className="kpi-value" style={{ color: '#f59e0b', fontSize: 28 }}>{formatCurrency(totalSent, currency)}</div>
          <div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>unpaid invoices</div>
        </div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.05s' }}>
          <div className="kpi-label">Paid This Month</div>
          <div className="kpi-value" style={{ color: '#10b981', fontSize: 28 }}>{formatCurrency(totalPaid, currency)}</div>
          <div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>collected</div>
        </div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '0.1s' }}>
          <div className="kpi-label">Total Overdue</div>
          <div className="kpi-value" style={{ color: '#ef4444', fontSize: 28 }}>{formatCurrency(totalOverdue, currency)}</div>
          <div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>{invoices.filter(i => i.status === 'overdue').length} invoices</div>
        </div>
      </div>

      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 20, flexWrap: 'wrap', gap: 12 }}>
        <SubTabs accent={mod.accent} tabs={tabs} active={tab} onChange={setTab}/>
        <Btn variant="primary" accent={mod.accent} onClick={() => setModal({ type: 'add' })}><OrbitIcons.plus size={16}/> Create Invoice</Btn>
      </div>

      {filtered.length === 0 ? (
        <EmptyState accent={mod.accent} title={`No ${tab === 'all' ? '' : tab + ' '}invoices`} description="Create and track invoices for your clients"
          actionLabel="Create Invoice" onAction={() => setModal({ type: 'add' })}/>
      ) : (
        <DataTable headers={[
          { label: 'Invoice' }, { label: 'Client' }, { label: 'Description' },
          { label: 'Amount', align: 'right' }, { label: 'Due' }, { label: 'Status' }, { label: '', align: 'right' }
        ]}>
          {filtered.map(inv => {
            const days = getDaysInfo(inv);
            return (
              <tr key={inv.id}>
                <td style={{ fontFamily: 'var(--font-mono)', color: mod.accent, fontWeight: 600, fontSize: 13 }}>{inv.number}</td>
                <td style={{ color: 'var(--text-primary)', fontWeight: 500 }}>{inv.clientName}</td>
                <td style={{ color: 'var(--text-secondary)', fontSize: 13, maxWidth: 200, overflow: 'hidden', textOverflow: 'ellipsis', whiteSpace: 'nowrap' }}>{inv.description}</td>
                <td className="amount" style={{ fontWeight: 600 }}>{formatCurrency(inv.amount, currency)}</td>
                <td>
                  <div className="mono" style={{ fontSize: 13, color: 'var(--text-tertiary)' }}>
                    {new Date(inv.dueDate).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}
                  </div>
                  {days && <div style={{ fontSize: 11, color: days.color, fontWeight: days.bold ? 700 : 400, fontFamily: 'var(--font-mono)' }}>{days.text}</div>}
                </td>
                <td><Badge variant={statusColors[inv.status]}>{inv.status}</Badge></td>
                <td style={{ textAlign: 'right' }}>
                  <div className="table-actions" style={{ justifyContent: 'flex-end' }}>
                    {(inv.status === 'sent' || inv.status === 'overdue') && (
                      <button className="btn-icon" title="Mark as Paid" style={{ color: '#10b981' }} onClick={() => markPaid(inv.id)}><OrbitIcons.check size={16}/></button>
                    )}
                    <IconBtn icon="edit" onClick={() => setModal({ type: 'edit', entry: inv })}/>
                    <IconBtn icon="trash" onClick={() => setConfirm(inv.id)}/>
                  </div>
                </td>
              </tr>
            );
          })}
        </DataTable>
      )}

      {modal && <InvoiceFormModal entry={modal.entry} clients={data.clients} onSave={handleSave}
        onClose={() => setModal(null)} accent={mod.accent} nextNum={`INV-${String(data.invoices.length + 1).padStart(3, '0')}`}/>}
      {confirm && <ConfirmDialog title="Delete Invoice" message="Delete this invoice permanently?"
        danger onConfirm={() => { onUpdate('invoices', data.invoices.filter(i => i.id !== confirm)); setConfirm(null); }}
        onCancel={() => setConfirm(null)}/>}
    </div>
  );
};

const InvoiceFormModal = ({ entry, clients, onSave, onClose, accent, nextNum }) => {
  const [f, setF] = React.useState(entry || { clientName: '', amount: '', date: new Date().toISOString().split('T')[0], dueDate: '', status: 'draft', description: '', number: nextNum });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  return (
    <Modal title={entry ? 'Edit Invoice' : 'Create Invoice'} onClose={onClose}>
      <FormGroup label="Invoice #"><input className="form-input" value={f.number || nextNum} onChange={e => u('number', e.target.value)} style={{ fontFamily: 'var(--font-mono)' }}/></FormGroup>
      <FormGroup label="Client">
        <select className="form-select" value={f.clientName} onChange={e => u('clientName', e.target.value)}>
          <option value="">Select client...</option>
          {clients.map(c => <option key={c.id} value={c.name}>{c.name}</option>)}
        </select>
      </FormGroup>
      <FormGroup label="Description"><input className="form-input" value={f.description} onChange={e => u('description', e.target.value)} placeholder="Project or service description"/></FormGroup>
      <div className="form-row">
        <FormGroup label="Amount"><input className="form-input" type="number" value={f.amount} onChange={e => u('amount', e.target.value)}/></FormGroup>
        <FormGroup label="Status">
          <select className="form-select" value={f.status} onChange={e => u('status', e.target.value)}>
            <option value="draft">Draft</option><option value="sent">Sent</option><option value="paid">Paid</option><option value="overdue">Overdue</option>
          </select>
        </FormGroup>
      </div>
      <div className="form-row">
        <FormGroup label="Issue Date"><input className="form-input" type="date" value={f.date} onChange={e => u('date', e.target.value)}/></FormGroup>
        <FormGroup label="Due Date"><input className="form-input" type="date" value={f.dueDate} onChange={e => u('dueDate', e.target.value)}/></FormGroup>
      </div>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, amount: Number(f.amount) || 0 })}>{entry ? 'Update' : 'Create Invoice'}</Btn>
      </div>
    </Modal>
  );
};

/* ═══════════════ SUBSCRIPTIONS MODULE ═══════════════ */
const SubscriptionsModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[4]; const cc = cardClass || '';
  const [modal, setModal] = React.useState(null);
  const [confirm, setConfirm] = React.useState(null);
  const [alertDismissed, setAlertDismissed] = React.useState(false);
  const activeSubs = data.subscriptions.filter(s => s.status !== 'cancelled');
  const monthlyTotal = activeSubs.reduce((s, e) => s + e.cost, 0);
  const expiringSubs = data.subscriptions.filter(s => { if (s.status === 'cancelled') return false; const d = new Date(s.nextBilling); return (d - new Date()) / 86400000 <= 7 && (d - new Date()) / 86400000 >= 0; });
  const renewals30 = data.subscriptions.filter(s => { if (s.status === 'cancelled') return false; const d = new Date(s.nextBilling); return (d - new Date()) / 86400000 <= 30 && (d - new Date()) / 86400000 >= 0; });
  const statusMap = { active: 'success', expiring: 'warning', cancelled: 'danger', paused: 'orange' };
  const catColors = { Design: '#ec4899', Productivity: '#7c3aed', Marketing: '#f59e0b', Dev: '#10b981', Hosting: '#06b6d4', AI: '#f43f5e', Finance: '#fb923c', Communication: '#0d9488', 'Project Mgmt': '#7c3aed', Other: '#64748b' };

  const catBreakdown = React.useMemo(() => {
    const cats = {}; activeSubs.forEach(s => { const cat = s.category || 'Other'; cats[cat] = (cats[cat] || 0) + s.cost; });
    const total = Object.values(cats).reduce((s, v) => s + v, 0) || 1;
    return Object.entries(cats).map(([cat, amt]) => ({ category: cat, amount: amt, pct: Math.round(amt / total * 100) })).sort((a, b) => b.amount - a.amount);
  }, [activeSubs]);

  const handleSave = (sub) => {
    if (modal.type === 'edit') onUpdate('subscriptions', data.subscriptions.map(s => s.id === sub.id ? sub : s));
    else onUpdate('subscriptions', [...data.subscriptions, { ...sub, id: Date.now() }]);
    setModal(null);
  };

  return (
    <div>
      {expiringSubs.length > 0 && !alertDismissed && (
        <AlertBanner type="warning" onDismiss={() => setAlertDismissed(true)}>
          <strong>{expiringSubs[0].name}</strong> renews in {Math.ceil((new Date(expiringSubs[0].nextBilling) - new Date()) / 86400000)} days — <strong>{formatCurrency(expiringSubs[0].cost, currency)}/{expiringSubs[0].frequency}</strong>
        </AlertBanner>
      )}
      <div className="kpi-grid" style={{ marginBottom: 24 }}>
        <KPICard label="Monthly Total" value={formatCurrency(monthlyTotal, currency)} accent={mod.accent} pulse animDelay={0}/>
        <KPICard label="Annual Total" value={formatCurrency(monthlyTotal * 12, currency)} accent="#7c3aed" animDelay={0.05}/>
        <KPICard label="Renewals in 30 Days" value={renewals30.length} accent={renewals30.length > 0 ? '#f59e0b' : mod.accent} animDelay={0.1}/>
        <KPICard label="Active Tools" value={activeSubs.length} accent={mod.accent} animDelay={0.15}/>
      </div>
      <div style={{ display: 'flex', justifyContent: 'flex-end', marginBottom: 20 }}>
        <Btn variant="primary" accent={mod.accent} onClick={() => setModal({ type: 'add' })}><OrbitIcons.plus size={16}/> Add Subscription</Btn>
      </div>
      {data.subscriptions.length === 0 ? (
        <EmptyState accent={mod.accent} title="No subscriptions tracked" description="Add your recurring tools and services" actionLabel="Add Subscription" onAction={() => setModal({ type: 'add' })}/>
      ) : (
        <div style={{ marginBottom: 24 }}>
          <DataTable headers={[{ label: 'Tool' }, { label: 'Category' }, { label: 'Monthly', align: 'right' }, { label: 'Annual', align: 'right' }, { label: 'Renewal' }, { label: 'Status' }, { label: '', align: 'right' }]}>
            {data.subscriptions.map(s => {
              const daysUntil = Math.ceil((new Date(s.nextBilling) - new Date()) / 86400000);
              const renewalUrgent = daysUntil >= 0 && daysUntil <= 7;
              return (
                <tr key={s.id}>
                  <td>
                    <div style={{ display: 'flex', alignItems: 'center', gap: 10 }}>
                      <div style={{ width: 32, height: 32, borderRadius: 8, background: `${catColors[s.category] || '#64748b'}18`,
                        border: `1px solid ${catColors[s.category] || '#64748b'}33`, display: 'grid', placeItems: 'center',
                        fontWeight: 700, fontSize: 13, color: catColors[s.category] || '#64748b' }}>{(s.name || '?')[0]}</div>
                      <span style={{ fontWeight: 500, color: 'var(--text-primary)' }}>{s.name}</span>
                    </div>
                  </td>
                  <td><Badge variant="neutral">{s.category}</Badge></td>
                  <td className="amount" style={{ color: mod.accent }}>{formatCurrency(s.cost, currency)}</td>
                  <td className="amount" style={{ color: 'var(--text-tertiary)' }}>{formatCurrency(s.cost * 12, currency)}</td>
                  <td>
                    <span className="mono" style={{ fontSize: 13, color: renewalUrgent ? '#ef4444' : 'var(--text-tertiary)', fontWeight: renewalUrgent ? 600 : 400 }}>
                      {new Date(s.nextBilling).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}{renewalUrgent && ` (${daysUntil}d)`}
                    </span>
                  </td>
                  <td><Badge variant={statusMap[s.status] || 'neutral'}>{s.status}</Badge></td>
                  <td style={{ textAlign: 'right' }}>
                    <div className="table-actions" style={{ justifyContent: 'flex-end' }}>
                      <IconBtn icon="edit" onClick={() => setModal({ type: 'edit', entry: s })}/>
                      <IconBtn icon="trash" onClick={() => setConfirm(s.id)}/>
                    </div>
                  </td>
                </tr>
              );
            })}
          </DataTable>
        </div>
      )}

      {catBreakdown.length > 0 && (
        <OrbitCard className={`animate-in animate-in-3 ${cc}`}>
          <div className="kpi-label" style={{ marginBottom: 16 }}>Spend by Category</div>
          <div style={{ height: 24, borderRadius: 6, overflow: 'hidden', display: 'flex', marginBottom: 16 }}>
            {catBreakdown.map((item) => (
              <div key={item.category} style={{ width: `${item.pct}%`, height: '100%', background: catColors[item.category] || '#64748b', transition: 'width 0.6s cubic-bezier(0.4,0,0.2,1)' }}/>
            ))}
          </div>
          <div style={{ display: 'flex', flexWrap: 'wrap', gap: 14 }}>
            {catBreakdown.map(item => (
              <div key={item.category} style={{ display: 'flex', alignItems: 'center', gap: 6, fontSize: 13 }}>
                <span style={{ width: 8, height: 8, borderRadius: 2, background: catColors[item.category] || '#64748b', display: 'inline-block' }}></span>
                <span style={{ color: 'var(--text-secondary)' }}>{item.category}</span>
                <span style={{ fontFamily: 'var(--font-mono)', color: 'var(--text-tertiary)', fontSize: 12 }}>{item.pct}%</span>
              </div>
            ))}
          </div>
        </OrbitCard>
      )}

      {modal && <SubFormModal entry={modal.entry} onSave={handleSave} onClose={() => setModal(null)} accent={mod.accent}/>}
      {confirm && <ConfirmDialog title="Delete Subscription" message="Remove this subscription?"
        danger onConfirm={() => { onUpdate('subscriptions', data.subscriptions.filter(s => s.id !== confirm)); setConfirm(null); }}
        onCancel={() => setConfirm(null)}/>}
    </div>
  );
};

const SubFormModal = ({ entry, onSave, onClose, accent }) => {
  const [f, setF] = React.useState(entry || { name: '', cost: '', frequency: 'month', nextBilling: '', status: 'active', category: 'Other' });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  const categories = ['Design', 'Productivity', 'Marketing', 'Dev', 'Hosting', 'AI', 'Finance', 'Communication', 'Other'];
  return (
    <Modal title={entry ? 'Edit Subscription' : 'Add Subscription'} onClose={onClose}>
      <FormGroup label="Tool / Service Name"><input className="form-input" value={f.name} onChange={e => u('name', e.target.value)} placeholder="e.g., Figma, AWS, Notion"/></FormGroup>
      <div className="form-row">
        <FormGroup label="Category">
          <select className="form-select" value={f.category} onChange={e => u('category', e.target.value)}>
            {categories.map(c => <option key={c} value={c}>{c}</option>)}
          </select>
        </FormGroup>
        <FormGroup label="Monthly Cost"><input className="form-input" type="number" value={f.cost} onChange={e => u('cost', e.target.value)}/></FormGroup>
      </div>
      <div className="form-row">
        <FormGroup label="Billing Cycle">
          <select className="form-select" value={f.frequency} onChange={e => u('frequency', e.target.value)}>
            <option value="month">Monthly</option><option value="year">Annually</option>
          </select>
        </FormGroup>
        <FormGroup label="Renewal Date"><input className="form-input" type="date" value={f.nextBilling} onChange={e => u('nextBilling', e.target.value)}/></FormGroup>
      </div>
      <FormGroup label="Status">
        <select className="form-select" value={f.status} onChange={e => u('status', e.target.value)}>
          <option value="active">Active</option><option value="paused">Paused</option>
          <option value="expiring">Expiring</option><option value="cancelled">Cancelled</option>
        </select>
      </FormGroup>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, cost: Number(f.cost) || 0 })}>{entry ? 'Update' : 'Add'}</Btn>
      </div>
    </Modal>
  );
};

Object.assign(window, { InvoicesModule, SubscriptionsModule, InvoiceFormModal, SubFormModal });
</script>

<script type="text/babel">
/* ═══════════════ TAX RESERVE MODULE ═══════════════ */
const TaxModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[5]; const cc = cardClass || '';
  const [taxRate, setTaxRate] = React.useState(25);
  const [reserveModal, setReserveModal] = React.useState(false);
  const [confirm, setConfirm] = React.useState(null);
  const totalIncome = data.income.reduce((s, e) => s + e.amount, 0);
  const totalExpenses = data.expenses.reduce((s, e) => s + e.amount, 0);
  const netTaxable = totalIncome - totalExpenses;
  const recommended = Math.round(netTaxable * taxRate / 100);
  const reserveLog = data.taxReserveLog || [];
  const reserved = reserveLog.reduce((s, e) => s + e.amount, 0);
  const shortfall = Math.max(recommended - reserved, 0);
  const coveragePct = recommended > 0 ? reserved / recommended : 0;
  const handleAddReserve = (entry) => { onUpdate('taxReserveLog', [...reserveLog, { ...entry, id: Date.now() }]); setReserveModal(false); };
  const taxEvents = [
    { date: '2026-06-15', event: 'Advance Tax Q1', status: 'upcoming', days: 27 },
    { date: '2026-07-31', event: 'ITR Filing Deadline', status: 'approaching', days: 73 },
    { date: '2026-09-15', event: 'Advance Tax Q2', status: 'scheduled', days: 119 },
    { date: '2026-12-15', event: 'Advance Tax Q3', status: 'scheduled', days: 210 },
    { date: '2027-03-15', event: 'Advance Tax Q4', status: 'scheduled', days: 300 },
  ];

  return (
    <div>
      <OrbitCard className={`animate-in ${cc}`} style={{ marginBottom: 24 }}>
        <div style={{ display: 'flex', gap: 24, alignItems: 'center', flexWrap: 'wrap' }}>
          <FormGroup label="Tax Reserve Rate">
            <div style={{ display: 'flex', alignItems: 'center', gap: 8 }}>
              <input className="form-input" type="number" value={taxRate} min={0} max={50}
                onChange={e => setTaxRate(Number(e.target.value) || 0)}
                style={{ width: 80, textAlign: 'center', fontFamily: 'var(--font-mono)' }}/>
              <span style={{ color: 'var(--text-tertiary)', fontSize: 14 }}>%</span>
            </div>
          </FormGroup>
          <FormGroup label="Financial Year">
            <select className="form-select" defaultValue="april" style={{ width: 'auto' }}>
              <option value="january">January</option><option value="february">February</option>
              <option value="march">March</option><option value="april">April</option>
              <option value="may">May</option><option value="june">June</option>
              <option value="july">July</option><option value="august">August</option>
              <option value="september">September</option><option value="october">October</option>
              <option value="november">November</option><option value="december">December</option>
            </select>
          </FormGroup>
        </div>
      </OrbitCard>

      <div className="kpi-grid" style={{ marginBottom: 24, gridTemplateColumns: 'repeat(auto-fit, minmax(200px, 1fr))' }}>
        <div className={`card kpi-card animate-in ${cc}`}><div className="kpi-label">Gross Income (FY)</div><div className="kpi-value" style={{ color: '#10b981', fontSize: 26 }}>{formatCurrency(totalIncome, currency)}</div><div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>April 2025 → now</div></div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '.05s' }}><div className="kpi-label">Expenses (FY)</div><div className="kpi-value" style={{ color: '#ef4444', fontSize: 26 }}>{formatCurrency(totalExpenses, currency)}</div><div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>deductible</div></div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '.1s' }}><div className="kpi-label">Net Taxable Profit</div><div className="kpi-value" style={{ color: '#06b6d4', fontSize: 26 }}>{formatCurrency(netTaxable, currency)}</div><div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>income − expenses</div></div>
        <div className={`card kpi-card animate-in ${cc}`} style={{ animationDelay: '.15s' }}><div className="kpi-label">Tax Reserve Needed</div><div className="kpi-value" style={{ color: mod.accent, fontSize: 26 }}>{formatCurrency(recommended, currency)}</div><div style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>{taxRate}% of net profit</div></div>
      </div>

      <OrbitCard className={`animate-in animate-in-3 ${cc}`} style={{ marginBottom: 24 }}>
        <ArcGauge value={reserved} max={recommended || 1} size={240}
          label={coveragePct >= 1 ? 'Fully Covered' : `${formatCurrency(reserved, currency)} of ${formatCurrency(recommended, currency)} reserved`}
          sublabel={shortfall > 0 ? `Under-reserved by ${formatCurrency(shortfall, currency)}` : `On track — surplus of ${formatCurrency(reserved - recommended, currency)}`}/>
        <div style={{ textAlign: 'center', marginTop: 8 }}>
          <Badge variant={coveragePct >= 0.8 ? 'success' : coveragePct >= 0.5 ? 'warning' : 'danger'}>
            {coveragePct >= 0.8 ? '● On Track' : coveragePct >= 0.5 ? '● At Risk' : '● Under-reserved'}
          </Badge>
        </div>
      </OrbitCard>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: 20, marginBottom: 24 }} className="tax-grid">
        <OrbitCard className={`animate-in animate-in-4 ${cc}`}>
          <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 14 }}>
            <div className="kpi-label">Reserve Log</div>
            <Btn size="sm" variant="primary" accent={mod.accent} onClick={() => setReserveModal(true)}><OrbitIcons.plus size={14}/> Add</Btn>
          </div>
          {reserveLog.length === 0 ? (
            <div style={{ color: 'var(--text-tertiary)', fontSize: 14, textAlign: 'center', padding: 20 }}>No entries yet</div>
          ) : (
            <div style={{ display: 'flex', flexDirection: 'column', gap: 8 }}>
              {reserveLog.map((e, i) => {
                const running = reserveLog.slice(0, i + 1).reduce((s, x) => s + x.amount, 0);
                return (
                  <div key={e.id} style={{ display: 'flex', alignItems: 'center', gap: 10, padding: '8px 12px', background: 'var(--bg-elevated)', borderRadius: 6 }}>
                    <span className="mono" style={{ fontSize: 12, color: 'var(--text-tertiary)', minWidth: 60 }}>
                      {new Date(e.date).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}
                    </span>
                    <span style={{ flex: 1, fontSize: 13, color: 'var(--text-secondary)' }}>{e.note || 'Reserve deposit'}</span>
                    <span style={{ fontFamily: 'var(--font-mono)', fontSize: 13, color: '#10b981' }}>+{formatCurrency(e.amount, currency)}</span>
                    <span style={{ fontFamily: 'var(--font-mono)', fontSize: 11, color: 'var(--text-tertiary)' }}>{'Σ'} {formatCompact(running, currency)}</span>
                    <IconBtn icon="trash" onClick={() => setConfirm(e.id)}/>
                  </div>
                );
              })}
            </div>
          )}
        </OrbitCard>

        <OrbitCard className={`animate-in animate-in-5 ${cc}`}>
          <div className="kpi-label" style={{ marginBottom: 14 }}>Tax Calendar</div>
          <div style={{ display: 'flex', flexDirection: 'column' }}>
            {taxEvents.map((ev, i) => (
              <div key={i} className="tax-event">
                <div className={`tax-dot ${ev.status}`}/>
                <div style={{ flex: 1 }}>
                  <div style={{ fontSize: 14, color: 'var(--text-primary)', fontWeight: 500 }}>{ev.event}</div>
                  <div className="mono" style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>
                    {new Date(ev.date).toLocaleDateString('en-GB', { day: '2-digit', month: 'short', year: 'numeric' })}
                  </div>
                </div>
                <Badge variant={ev.status === 'upcoming' ? 'warning' : ev.status === 'approaching' ? 'danger' : 'neutral'}>{ev.days}d</Badge>
              </div>
            ))}
          </div>
        </OrbitCard>
      </div>

      {reserveModal && (
        <Modal title="Add Reserve Entry" onClose={() => setReserveModal(false)} width="420px">
          <ReserveForm onSave={handleAddReserve} onClose={() => setReserveModal(false)} accent={mod.accent}/>
        </Modal>
      )}
      {confirm && <ConfirmDialog title="Delete Entry" message="Remove this reserve log entry?" danger
        onConfirm={() => { onUpdate('taxReserveLog', reserveLog.filter(e => e.id !== confirm)); setConfirm(null); }}
        onCancel={() => setConfirm(null)}/>}
      <style>{`.tax-grid{} @media(max-width:900px){.tax-grid{grid-template-columns:1fr !important}}`}</style>
    </div>
  );
};

const ReserveForm = ({ onSave, onClose, accent }) => {
  const [f, setF] = React.useState({ amount: '', date: new Date().toISOString().split('T')[0], note: '' });
  return (
    <>
      <FormGroup label="Amount"><input className="form-input" type="number" value={f.amount} onChange={e => setF(p => ({ ...p, amount: e.target.value }))}/></FormGroup>
      <div className="form-row">
        <FormGroup label="Date"><input className="form-input" type="date" value={f.date} onChange={e => setF(p => ({ ...p, date: e.target.value }))}/></FormGroup>
        <FormGroup label="Note"><input className="form-input" value={f.note} onChange={e => setF(p => ({ ...p, note: e.target.value }))} placeholder="e.g., Moved to savings"/></FormGroup>
      </div>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, amount: Number(f.amount) || 0 })}>Add Entry</Btn>
      </div>
    </>
  );
};

Object.assign(window, { TaxModule, ReserveForm });
</script>

<script type="text/babel">
/* ═══════════════ CASH FLOW MODULE ═══════════════ */
const MONTH_NAMES = ['January','February','March','April','May','June','July','August','September','October','November','December'];

/* Memoized single calendar day cell */
const CalDay = React.memo(({ cd, isToday, isSelected, dots, onSelect }) => (
  <div
    className={`cal-day${cd.otherMonth ? ' other-month' : ''}${isToday ? ' today' : ''}${isSelected ? ' selected' : ''}`}
    onClick={onSelect}>
    <span>{cd.day}</span>
    {dots.length > 0 && (
      <div className="cal-dots">
        {dots.slice(0, 3).map((c, j) => <div key={j} className="cal-dot" style={{ background: c }}/>)}
      </div>
    )}
  </div>
));

const CashFlowModule = ({ data, currency, cardClass }) => {
  const mod = MODULES[6]; const cc = cardClass || '';
  const today = React.useMemo(() => new Date(), []);
  const [viewMonth, setViewMonth] = React.useState(today.getMonth());
  const [viewYear, setViewYear] = React.useState(today.getFullYear());
  const [selectedDate, setSelectedDate] = React.useState(`${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`);
  const [slideDir, setSlideDir] = React.useState('');

  /* Build events once, indexed by "YYYY-MM-DD" for O(1) lookup */
  const eventsByDate = React.useMemo(() => {
    const map = {};
    const add = (date, ev) => { if (!map[date]) map[date] = []; map[date].push(ev); };
    data.invoices.filter(i => i.status === 'sent' || i.status === 'overdue').forEach(inv =>
      add(inv.dueDate, { title: `${inv.clientName} Payment Due`, amount: inv.amount, type: 'receivable', color: '#10b981' }));
    data.subscriptions.filter(s => s.status !== 'cancelled').forEach(sub =>
      add(sub.nextBilling, { title: `${sub.name} Renewal`, amount: sub.cost, type: 'payment', color: '#ef4444' }));
    add('2026-06-15', { title: 'Advance Tax Q1', amount: 31000, type: 'tax', color: '#fb923c' });
    return map;
  }, [data]);

  /* All events as flat array for upcoming 30d list */
  const allEvents = React.useMemo(() => Object.entries(eventsByDate).flatMap(([date, evs]) => evs.map(ev => ({ ...ev, date }))), [eventsByDate]);

  /* Calendar days grid — only recomputes on month/year change */
  const calDays = React.useMemo(() => {
    const firstDay = new Date(viewYear, viewMonth, 1).getDay();
    const daysInMonth = new Date(viewYear, viewMonth + 1, 0).getDate();
    const prevMonthDays = new Date(viewYear, viewMonth, 0).getDate();
    const startOffset = firstDay === 0 ? 6 : firstDay - 1;
    const days = [];
    for (let i = startOffset - 1; i >= 0; i--) days.push({ day: prevMonthDays - i, otherMonth: true });
    for (let i = 1; i <= daysInMonth; i++) days.push({ day: i, otherMonth: false });
    while (days.length < 42) days.push({ day: days.length - daysInMonth - startOffset + 1, otherMonth: true });
    return days;
  }, [viewMonth, viewYear]);

  const navigate = React.useCallback((dir) => {
    setSlideDir(dir);
    if (dir === 'left') {
      setViewMonth(m => { if (m === 0) { setViewYear(y => y - 1); return 11; } return m - 1; });
    } else {
      setViewMonth(m => { if (m === 11) { setViewYear(y => y + 1); return 0; } return m + 1; });
    }
  }, []);

  const goToToday = React.useCallback(() => {
    setSlideDir('right');
    setViewMonth(today.getMonth());
    setViewYear(today.getFullYear());
    setSelectedDate(`${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`);
  }, [today]);

  const upcoming30 = React.useMemo(() => {
    const now = new Date(); const end = new Date(now.getTime() + 30 * 86400000);
    return allEvents.filter(e => { const d = new Date(e.date); return d >= now && d <= end; }).sort((a,b) => a.date.localeCompare(b.date));
  }, [allEvents]);

  const groupByWeek = React.useCallback((items) => {
    const groups = []; let cur = null;
    items.forEach(item => {
      const d = new Date(item.date); const ws = new Date(d); ws.setDate(d.getDate() - ((d.getDay() + 6) % 7));
      const lbl = `${ws.toLocaleDateString('en-GB', { day:'2-digit', month:'short' })} – ${new Date(ws.getTime() + 6*86400000).toLocaleDateString('en-GB', { day:'2-digit', month:'short' })}`;
      if (!cur || cur.label !== lbl) { cur = { label: lbl, items: [] }; groups.push(cur); }
      cur.items.push(item);
    });
    return groups;
  }, []);

  const selectedEvents = eventsByDate[selectedDate] || [];
  const [selDay, selMonthStr, selYearStr] = [selectedDate.slice(8,10), selectedDate.slice(5,7), selectedDate.slice(0,4)];
  const selDisplay = `${parseInt(selDay)} ${MONTH_NAMES[parseInt(selMonthStr)-1]} ${selYearStr}`;

  const income30 = React.useMemo(() => upcoming30.filter(e => e.type==='receivable').reduce((s,e) => s+e.amount, 0), [upcoming30]);
  const outflow30 = React.useMemo(() => upcoming30.filter(e => e.type!=='receivable').reduce((s,e) => s+e.amount, 0), [upcoming30]);

  return (
    <div>
      <div className="kpi-grid" style={{ marginBottom: 24 }}>
        <KPICard label="Expected Income (30d)" value={formatCurrency(income30, currency)} accent="#10b981" pulse/>
        <KPICard label="Expected Outflow (30d)" value={formatCurrency(outflow30, currency)} accent="#ef4444" animDelay={0.05}/>
        <KPICard label="Net Projection" value={formatCurrency(income30 - outflow30, currency)} accent={mod.accent} animDelay={0.1}/>
      </div>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 340px', gap: 20, marginBottom: 24 }} className="cashflow-grid">
        <OrbitCard className={`animate-in animate-in-2 ${cc}`}>
          {/* Month nav */}
          <div className="cal-month-nav">
            <button className="btn-icon" onClick={() => navigate('left')}><OrbitIcons.chevronLeft size={18}/></button>
            <span className="cal-month-title" onClick={goToToday} title="Back to today">
              {MONTH_NAMES[viewMonth]} {viewYear}
            </span>
            <button className="btn-icon" onClick={() => navigate('right')}><OrbitIcons.chevronRight size={18}/></button>
          </div>

          {/* Grid with slide animation keyed to month+year */}
          <div className="cal-wrap">
            <div key={`${viewYear}-${viewMonth}`} className={`cal-slide-${slideDir || 'right'}`}>
              <div className="cal-grid">
                {['Mo','Tu','We','Th','Fr','Sa','Su'].map(d => <div key={d} className="cal-header">{d}</div>)}
                {calDays.map((cd, i) => {
                  const dateKey = cd.otherMonth ? '' : `${viewYear}-${String(viewMonth+1).padStart(2,'0')}-${String(cd.day).padStart(2,'0')}`;
                  const dots = cd.otherMonth ? [] : (eventsByDate[dateKey] || []).map(e => e.color);
                  const isToday = dateKey === `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
                  const isSelected = dateKey === selectedDate;
                  return (
                    <CalDay key={i} cd={cd} isToday={isToday} isSelected={isSelected} dots={dots}
                      onSelect={cd.otherMonth ? undefined : () => setSelectedDate(dateKey)}/>
                  );
                })}
              </div>
            </div>
          </div>

          {/* Legend */}
          <div style={{ display: 'flex', gap: 16, marginTop: 14, fontSize: 11, flexWrap: 'wrap', paddingTop: 10, borderTop: '1px solid var(--border-divider)' }}>
            {[{ label: 'Income Due', c: '#10b981' }, { label: 'Payment', c: '#ef4444' }, { label: 'Tax', c: '#fb923c' }].map(l => (
              <span key={l.label} style={{ display: 'flex', alignItems: 'center', gap: 5, color: 'var(--text-tertiary)' }}>
                <span className="cal-dot" style={{ background: l.c, width: 7, height: 7, display:'inline-block' }}/>  {l.label}
              </span>
            ))}
            <span style={{ marginLeft: 'auto', fontSize: 11, color: 'var(--text-tertiary)', cursor: 'pointer' }} onClick={goToToday}>↩ Today</span>
          </div>
        </OrbitCard>

        {/* Day detail panel */}
        <div className="cal-events-panel">
          <OrbitCard className={`animate-in animate-in-3 ${cc}`} style={{ flex: 1 }}>
            <div className="kpi-label" style={{ marginBottom: 4 }}>{selDisplay}</div>
            <div style={{ fontSize: 12, color: 'var(--text-tertiary)', marginBottom: 14 }}>
              {selectedEvents.length === 0 ? 'No events' : `${selectedEvents.length} event${selectedEvents.length > 1 ? 's' : ''}`}
            </div>
            {selectedEvents.length === 0 ? (
              <div style={{ color: 'var(--text-tertiary)', fontSize: 14, textAlign: 'center', padding: '30px 0', opacity: 0.6 }}>
                <div style={{ fontSize: 28, marginBottom: 8 }}>📭</div>
                Clear day
              </div>
            ) : (
              <div style={{ display: 'flex', flexDirection: 'column', gap: 8 }}>
                {selectedEvents.map((ev, i) => (
                  <div key={i} className="cal-event-card" style={{ '--ev-color': ev.color }}>
                    <div style={{ fontWeight: 600, fontSize: 13, color: 'var(--text-secondary)', textTransform: 'uppercase', letterSpacing: '0.5px', marginBottom: 4, fontSize: 11 }}>
                      {ev.type === 'receivable' ? '↑ INCOMING' : ev.type === 'tax' ? '⚠ TAX' : '↓ OUTGOING'}
                    </div>
                    <div style={{ fontWeight: 500, fontSize: 14, color: 'var(--text-primary)', marginBottom: 6 }}>{ev.title}</div>
                    <div style={{ fontFamily: 'var(--font-mono)', fontSize: 18, color: ev.color, fontWeight: 700 }}>
                      {ev.type === 'receivable' ? '+' : '−'}{formatCurrency(ev.amount, currency)}
                    </div>
                  </div>
                ))}
              </div>
            )}
          </OrbitCard>
        </div>
      </div>

      {/* Upcoming 30 days timeline */}
      <OrbitCard className={`animate-in animate-in-4 ${cc}`}>
        <div className="kpi-label" style={{ marginBottom: 16 }}>Upcoming 30 Days</div>
        {groupByWeek(upcoming30).map((week, wi) => (
          <div key={wi} className="week-group">
            <div className="week-label">{week.label}</div>
            {week.items.map((item, ii) => (
              <div key={ii} className="week-item" style={{ cursor: 'pointer' }}
                onClick={() => { setSelectedDate(item.date); setViewMonth(new Date(item.date).getMonth()); setViewYear(new Date(item.date).getFullYear()); }}>
                <span className="mono" style={{ fontSize: 13, color: 'var(--text-tertiary)', minWidth: 60 }}>
                  {new Date(item.date).toLocaleDateString('en-GB', { day: '2-digit', month: 'short' })}
                </span>
                <span style={{ flex: 1, color: 'var(--text-primary)', fontWeight: 500 }}>{item.title}</span>
                <span style={{ fontFamily: 'var(--font-mono)', fontSize: 14, color: item.type === 'receivable' ? '#10b981' : '#ef4444' }}>
                  {item.type === 'receivable' ? '+' : '−'}{formatCurrency(item.amount, currency)}
                </span>
              </div>
            ))}
          </div>
        ))}
        {upcoming30.length === 0 && <div style={{ color: 'var(--text-tertiary)', textAlign: 'center', padding: 20 }}>No upcoming events</div>}
      </OrbitCard>
      <style>{`@media(max-width:900px){.cashflow-grid{grid-template-columns:1fr !important}}`}</style>
    </div>
  );
};

Object.assign(window, { CashFlowModule });
</script>

<script type="text/babel">
/* ═══════════════ REVENUE GOALS MODULE ═══════════════ */
const GoalsModule = ({ data, currency, onUpdate, cardClass }) => {
  const mod = MODULES[7]; const cc = cardClass || '';
  const [modal, setModal] = React.useState(null);
  const [confirm, setConfirm] = React.useState(null);
  const totalIncome = data.income.reduce((s, e) => s + e.amount, 0);
  const monthlyTarget = 150000; const annualTarget = 2000000;
  const getProgressColor = (pct) => pct >= 71 ? '#10b981' : pct >= 41 ? '#f59e0b' : '#f43f5e';
  const getStatus = (current, target, daysLeft) => {
    const pct = current / target;
    if (pct >= 1) return { label: 'Completed', variant: 'success' };
    const dailyRate = current / (30 - daysLeft || 1);
    const projected = current + dailyRate * daysLeft;
    if (projected >= target * 0.9) return { label: 'On Track', variant: 'success' };
    if (projected >= target * 0.7) return { label: 'At Risk', variant: 'warning' };
    return { label: 'Behind', variant: 'danger' };
  };
  const milestones = [25, 50, 75, 100];
  const handleSave = (goal) => {
    if (modal.type === 'edit') onUpdate('goals', data.goals.map(g => g.id === goal.id ? goal : g));
    else onUpdate('goals', [...data.goals, { ...goal, id: Date.now() }]);
    setModal(null);
  };

  return (
    <div>
      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: 20, marginBottom: 28 }} className="goals-auto-grid">
        {[
          { title: 'Monthly Revenue Goal', subtitle: 'May 2026', current: totalIncome, target: monthlyTarget, daysLeft: 12 },
          { title: 'Annual Revenue Goal', subtitle: 'FY 2025–26', current: totalIncome * 4, target: annualTarget, daysLeft: 314 },
        ].map((g, i) => {
          const pct = Math.min(Math.round(g.current / g.target * 100), 100);
          const color = getProgressColor(pct);
          const status = getStatus(g.current, g.target, g.daysLeft);
          const remaining = Math.max(g.target - g.current, 0);
          return (
            <OrbitCard key={i} className={`animate-in animate-in-${i + 1} ${cc}`}>
              <div className="kpi-label">{g.title}</div>
              <div style={{ fontSize: 14, color: 'var(--text-secondary)', marginBottom: 16 }}>{g.subtitle}</div>
              <ProgressBar value={g.current} max={g.target} accent={color} showMarkers/>
              <div style={{ display: 'flex', justifyContent: 'space-between', marginTop: 10, fontFamily: 'var(--font-mono)', fontSize: 14 }}>
                <span style={{ color }}>{formatCurrency(g.current, currency)}</span>
                <span style={{ color: 'var(--text-tertiary)' }}>of {formatCurrency(g.target, currency)}</span>
              </div>
              <div style={{ display: 'flex', justifyContent: 'space-between', marginTop: 8, fontSize: 13 }}>
                <span style={{ color: 'var(--text-tertiary)' }}>{formatCurrency(remaining, currency)} to go · {g.daysLeft} days</span>
                <Badge variant={status.variant}>{'●'} {status.label}</Badge>
              </div>
            </OrbitCard>
          );
        })}
      </div>

      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 16 }}>
        <div className="kpi-label">Custom Goals</div>
        <Btn variant="primary" accent={mod.accent} onClick={() => setModal({ type: 'add' })}><OrbitIcons.plus size={16}/> Create Goal</Btn>
      </div>

      {data.goals.length === 0 ? (
        <EmptyState accent={mod.accent} title="No custom goals set" description="Create revenue goals to track your trajectory" actionLabel="Set a Goal" onAction={() => setModal({ type: 'add' })}/>
      ) : (
        <div style={{ display: 'flex', flexDirection: 'column', gap: 16 }}>
          {data.goals.map((g, i) => {
            const pct = Math.min(Math.round(g.current / g.target * 100), 100);
            const color = getProgressColor(pct);
            const remaining = Math.max(g.target - g.current, 0);
            const daysLeft = Math.max(Math.ceil((new Date(g.deadline) - new Date()) / 86400000), 0);
            const status = g.status === 'completed' ? { label: 'Completed', variant: 'success' } : getStatus(g.current, g.target, daysLeft);
            return (
              <OrbitCard key={g.id} accent={mod.accent} className={`animate-in animate-in-${i % 4 + 1} ${cc}`}
                style={pct >= 100 ? { animation: 'glowPulse 2s ease 3' } : {}}>
                <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'flex-start', marginBottom: 12 }}>
                  <div style={{ display: 'flex', alignItems: 'center', gap: 8 }}>
                    <OrbitIcons.target size={18} style={{ color: mod.accent }}/>
                    <span style={{ fontWeight: 600, fontSize: 16, color: 'var(--text-primary)' }}>{g.name}</span>
                  </div>
                  <div style={{ display: 'flex', alignItems: 'center', gap: 8 }}>
                    <Badge variant={status.variant}>{'●'} {status.label}</Badge>
                    <IconBtn icon="edit" onClick={() => setModal({ type: 'edit', entry: g })}/>
                    <IconBtn icon="trash" onClick={() => setConfirm(g.id)}/>
                  </div>
                </div>
                <ProgressBar value={g.current} max={g.target} accent={color} showMarkers/>
                <div style={{ display: 'flex', justifyContent: 'space-between', marginTop: 10, fontFamily: 'var(--font-mono)', fontSize: 14 }}>
                  <span style={{ color }}>{formatCurrency(g.current, currency)}</span>
                  <span style={{ color: 'var(--text-tertiary)' }}>of {formatCurrency(g.target, currency)}</span>
                </div>
                <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginTop: 10 }}>
                  <span style={{ fontSize: 12, color: 'var(--text-tertiary)' }}>{formatCurrency(remaining, currency)} to go · {daysLeft} days</span>
                </div>
                <div style={{ display: 'flex', gap: 16, marginTop: 14, paddingTop: 12, borderTop: '1px solid var(--border-divider)' }}>
                  {milestones.map(m => {
                    const hit = pct >= m;
                    return (
                      <div key={m} className={`milestone ${hit ? 'done' : ''}`}>
                        <div className="milestone-dot" style={hit ? { animation: 'milestoneHit 0.8s ease' } : {}}>
                          {hit && <OrbitIcons.check size={12}/>}
                        </div>
                        <span>{m}%</span>
                      </div>
                    );
                  })}
                </div>
              </OrbitCard>
            );
          })}
        </div>
      )}

      {modal && <GoalFormModal entry={modal.entry} onSave={handleSave} onClose={() => setModal(null)} accent={mod.accent}/>}
      {confirm && <ConfirmDialog title="Delete Goal" message="Remove this revenue goal?" danger
        onConfirm={() => { onUpdate('goals', data.goals.filter(g => g.id !== confirm)); setConfirm(null); }}
        onCancel={() => setConfirm(null)}/>}
      <style>{`@media(max-width:900px){.goals-auto-grid{grid-template-columns:1fr !important}}`}</style>
    </div>
  );
};

const GoalFormModal = ({ entry, onSave, onClose, accent }) => {
  const [f, setF] = React.useState(entry || { name: '', target: '', current: '', deadline: '', status: 'active' });
  const u = (k, v) => setF(p => ({ ...p, [k]: v }));
  return (
    <Modal title={entry ? 'Edit Goal' : 'Create Revenue Goal'} onClose={onClose}>
      <FormGroup label="Goal Name"><input className="form-input" value={f.name} onChange={e => u('name', e.target.value)} placeholder="e.g., Q2 Revenue Target"/></FormGroup>
      <div className="form-row">
        <FormGroup label="Target Amount"><input className="form-input" type="number" value={f.target} onChange={e => u('target', e.target.value)}/></FormGroup>
        <FormGroup label="Current Progress"><input className="form-input" type="number" value={f.current} onChange={e => u('current', e.target.value)}/></FormGroup>
      </div>
      <div className="form-row">
        <FormGroup label="Target Date"><input className="form-input" type="date" value={f.deadline} onChange={e => u('deadline', e.target.value)}/></FormGroup>
        <FormGroup label="Status">
          <select className="form-select" value={f.status} onChange={e => u('status', e.target.value)}>
            <option value="active">Active</option><option value="completed">Completed</option><option value="paused">Paused</option>
          </select>
        </FormGroup>
      </div>
      <div className="modal-footer">
        <Btn variant="ghost" onClick={onClose}>Cancel</Btn>
        <Btn variant="primary" accent={accent} onClick={() => onSave({ ...f, target: Number(f.target) || 0, current: Number(f.current) || 0 })}>
          {entry ? 'Update' : 'Create Goal'}
        </Btn>
      </div>
    </Modal>
  );
};

Object.assign(window, { GoalsModule, GoalFormModal });
</script>

<script type="text/babel">
/* ═══════════════ MAIN APP + SAMPLE DATA ═══════════════ */
const INITIAL_DATA = {
  income: [
    { id: 1, date: '2026-05-12', description: 'Acme Corp — Brand redesign', category: 'Freelance', amount: 50000, platform: 'Direct' },
    { id: 2, date: '2026-05-08', description: 'UI audit — Globex Industries', category: 'Consulting', amount: 28000, platform: 'Upwork' },
    { id: 3, date: '2026-05-01', description: 'Monthly retainer — Initech', category: 'Retainer', amount: 35000, platform: 'Direct' },
    { id: 4, date: '2026-04-22', description: 'Landing page — Stark Labs', category: 'Freelance', amount: 18000, platform: 'Toptal' },
    { id: 5, date: '2026-04-15', description: 'Design system — Wayne Ent.', category: 'Consulting', amount: 42000, platform: 'Direct' },
    { id: 6, date: '2026-04-05', description: 'E-commerce app — Umbrella Co', category: 'Freelance', amount: 65000, platform: 'Upwork' },
  ],
  expenses: [
    { id: 101, date: '2026-05-10', description: 'Figma Professional', category: 'Software/SaaS', amount: 1200 },
    { id: 102, date: '2026-05-05', description: 'AWS Hosting', category: 'Software/SaaS', amount: 3200 },
    { id: 103, date: '2026-05-01', description: 'Coworking space — May', category: 'Office', amount: 8000 },
    { id: 104, date: '2026-04-28', description: 'Google Workspace', category: 'Software/SaaS', amount: 900 },
    { id: 105, date: '2026-04-20', description: 'Adobe Creative Cloud', category: 'Software/SaaS', amount: 4800 },
    { id: 106, date: '2026-04-15', description: 'Facebook Ads campaign', category: 'Marketing', amount: 5500 },
    { id: 107, date: '2026-04-10', description: 'Freelance copywriter', category: 'Contractor', amount: 8000 },
  ],
  clients: [
    { id: 201, name: 'Sarah Chen', email: 'sarah@acmecorp.com', company: 'Acme Corp', industry: 'Technology', phone: '+1-555-0102', status: 'active', totalBilled: 125000, notes: '' },
    { id: 202, name: 'Marcus Obi', email: 'marcus@globex.io', company: 'Globex Industries', industry: 'Manufacturing', phone: '+1-555-0203', status: 'active', totalBilled: 84000, notes: '' },
    { id: 203, name: 'Priya Sharma', email: 'priya@initech.com', company: 'Initech', industry: 'Finance', phone: '+91-98765-43210', status: 'active', totalBilled: 210000, notes: '' },
    { id: 204, name: 'James Miller', email: 'james@starklabs.dev', company: 'Stark Labs', industry: 'Biotech', phone: '+44-7700-900100', status: 'inactive', totalBilled: 36000, notes: '' },
    { id: 205, name: 'Elena Volkov', email: 'elena@wayneent.co', company: 'Wayne Enterprises', industry: 'Conglomerate', phone: '+1-555-0304', status: 'prospect', totalBilled: 0, notes: 'Potential design system project' },
  ],
  projects: [
    { id: 601, name: 'Brand Redesign', clientId: 201, startDate: '2026-03-01', endDate: '2026-06-30', budget: 125000, status: 'in-progress', notes: '' },
    { id: 602, name: 'UI Audit Report', clientId: 202, startDate: '2026-04-15', endDate: '2026-05-15', budget: 28000, status: 'completed', notes: '' },
    { id: 603, name: 'Monthly Retainer', clientId: 203, startDate: '2026-01-01', endDate: '2026-12-31', budget: 420000, status: 'in-progress', notes: '' },
    { id: 604, name: 'Landing Page', clientId: 204, startDate: '2026-04-01', endDate: '2026-04-30', budget: 18000, status: 'completed', notes: '' },
    { id: 605, name: 'Design System', clientId: 205, startDate: '2026-05-15', endDate: '2026-09-30', budget: 200000, status: 'on-hold', notes: 'Pending contract signature' },
  ],
  invoices: [
    { id: 301, number: 'INV-001', clientName: 'Sarah Chen', amount: 50000, date: '2026-05-12', dueDate: '2026-05-26', status: 'sent', description: 'Brand redesign phase 1' },
    { id: 302, number: 'INV-002', clientName: 'Marcus Obi', amount: 28000, date: '2026-05-08', dueDate: '2026-05-22', status: 'paid', description: 'UI audit complete' },
    { id: 303, number: 'INV-003', clientName: 'Priya Sharma', amount: 35000, date: '2026-05-01', dueDate: '2026-05-15', status: 'paid', description: 'May retainer' },
    { id: 304, number: 'INV-004', clientName: 'James Miller', amount: 18000, date: '2026-04-22', dueDate: '2026-05-06', status: 'overdue', description: 'Landing page delivery' },
    { id: 305, number: 'INV-005', clientName: 'Sarah Chen', amount: 27000, date: '2026-04-10', dueDate: '2026-04-24', status: 'overdue', description: 'Brand guide addendum' },
    { id: 306, number: 'INV-006', clientName: 'Elena Volkov', amount: 42000, date: '2026-05-15', dueDate: '2026-06-15', status: 'draft', description: 'Design system proposal' },
  ],
  subscriptions: [
    { id: 401, name: 'Figma Professional', cost: 1200, frequency: 'month', nextBilling: '2026-06-01', status: 'active', category: 'Design' },
    { id: 402, name: 'AWS Services', cost: 3200, frequency: 'month', nextBilling: '2026-06-01', status: 'active', category: 'Hosting' },
    { id: 403, name: 'Notion Team', cost: 800, frequency: 'month', nextBilling: '2026-06-05', status: 'active', category: 'Productivity' },
    { id: 404, name: 'Adobe Creative Cloud', cost: 4800, frequency: 'month', nextBilling: '2026-05-22', status: 'active', category: 'Design' },
    { id: 405, name: 'Linear', cost: 640, frequency: 'month', nextBilling: '2026-06-10', status: 'active', category: 'Project Mgmt' },
    { id: 406, name: 'Slack Pro', cost: 600, frequency: 'month', nextBilling: '2026-06-01', status: 'paused', category: 'Communication' },
    { id: 407, name: 'ChatGPT Plus', cost: 1700, frequency: 'month', nextBilling: '2026-06-03', status: 'active', category: 'AI' },
  ],
  goals: [
    { id: 501, name: 'Q2 Revenue Target', target: 300000, current: 238000, deadline: '2026-06-30', status: 'active' },
    { id: 502, name: 'Annual Goal — ₹20L', target: 2000000, current: 980000, deadline: '2026-12-31', status: 'active' },
    { id: 503, name: 'Save for MacBook Pro', target: 200000, current: 134000, deadline: '2026-06-30', status: 'active' },
    { id: 504, name: 'Q1 Target', target: 250000, current: 250000, deadline: '2026-03-31', status: 'completed' },
  ],
  taxReserveLog: [
    { id: 701, date: '2026-02-01', amount: 30000, note: 'Moved to savings account' },
    { id: 702, date: '2026-03-01', amount: 25000, note: 'Monthly reserve' },
    { id: 703, date: '2026-04-01', amount: 35000, note: 'Monthly reserve' },
    { id: 704, date: '2026-05-01', amount: 28000, note: 'Monthly reserve' },
  ],
};

function loadData() {
  try { const saved = localStorage.getItem('orbit-desk-data-v2'); if (saved) { return { ...INITIAL_DATA, ...JSON.parse(saved) }; } } catch (e) {}
  return INITIAL_DATA;
}
function saveData(data) { try { localStorage.setItem('orbit-desk-data-v2', JSON.stringify(data)); } catch(e) {} }

const OrbitApp = () => {
  const [activeModule, setActiveModule] = React.useState(() => localStorage.getItem('orbit-module') || 'command');
  const [collapsed, setCollapsed] = React.useState(false);
  const [mobileOpen, setMobileOpen] = React.useState(false);
  const [currency, setCurrency] = React.useState('INR');
  const [data, setData] = React.useState(loadData);
  const [showSettings, setShowSettings] = React.useState(false);
  const [theme, setTheme] = React.useState(() => localStorage.getItem('orbit-theme') || 'dark');

  React.useEffect(() => { document.documentElement.setAttribute('data-theme', theme); localStorage.setItem('orbit-theme', theme); }, [theme]);
  const toggleTheme = React.useCallback((t) => { setTheme(t || (theme === 'dark' ? 'light' : 'dark')); }, [theme]);
  React.useEffect(() => { saveData(data); }, [data]);
  React.useEffect(() => { localStorage.setItem('orbit-module', activeModule); }, [activeModule]);

  const onUpdate = React.useCallback((key, value) => { setData(prev => ({ ...prev, [key]: value })); }, []);
  const handleModuleChange = React.useCallback((id) => { if (id === 'settings') { setShowSettings(true); return; } setActiveModule(id); }, []);

  const currentModule = MODULES.find(m => m.id === activeModule) || MODULES[0];
  const celestialMap = { command: 'celestial-command', budget: 'celestial-budget', clients: 'celestial-clients', invoices: 'celestial-invoices', subscriptions: 'celestial-subscriptions', tax: 'celestial-tax', cashflow: 'celestial-cashflow', goals: 'celestial-goals' };

  const renderModule = () => {
    const props = { data, currency, onUpdate, cardClass: '', onNavigate: handleModuleChange };
    switch (activeModule) {
      case 'command': return <CommandCenter {...props}/>;
      case 'budget': return <BudgetModule {...props}/>;
      case 'clients': return <ClientsModule {...props}/>;
      case 'invoices': return <InvoicesModule {...props}/>;
      case 'subscriptions': return <SubscriptionsModule {...props}/>;
      case 'tax': return <TaxModule {...props}/>;
      case 'cashflow': return <CashFlowModule {...props}/>;
      case 'goals': return <GoalsModule {...props}/>;
      default: return <CommandCenter {...props}/>;
    }
  };

  return (
    <>
      {Object.entries(celestialMap).map(([modId, cls]) => (
        <div key={modId} className={`celestial ${cls} ${activeModule === modId ? 'active' : ''}`}/>
      ))}
      <div className="orbit-bg"><div className="grid-overlay"/><div className="orbit-ring orbit-ring-1"/><div className="orbit-ring orbit-ring-2"/><div className="orbit-ring orbit-ring-3"/><div className="orbit-dot" style={{ top: '15%', left: '45%' }}/><div className="orbit-dot" style={{ top: '60%', left: '70%' }}/><div className="orbit-dot" style={{ top: '80%', left: '35%' }}/><div className="orbit-dot" style={{ top: '30%', left: '85%' }}/></div>
      <button className="mobile-menu-btn" onClick={() => setMobileOpen(true)}><OrbitIcons.menu size={24}/></button>
      <Sidebar activeModule={activeModule} onModuleChange={handleModuleChange} collapsed={collapsed} onToggleCollapse={() => setCollapsed(c => !c)} mobileOpen={mobileOpen} onCloseMobile={() => setMobileOpen(false)} theme={theme} onThemeToggle={toggleTheme}/>
      <main className="content-area" key={activeModule}>
        <PageHeader module={currentModule} accent={currentModule.accent} actions={
          <div style={{ display: 'flex', gap: 8, alignItems: 'center' }}>
            <button className="theme-toggle" onClick={() => toggleTheme()} title={theme === 'dark' ? 'Switch to Light' : 'Switch to Dark'}>
              {theme === 'dark' ? <OrbitIcons.sun size={18}/> : <OrbitIcons.moon size={18}/>}
            </button>
            <CurrencySelector value={currency} onChange={setCurrency}/>
          </div>
        }/>
        {renderModule()}
      </main>
      {showSettings && <SettingsModal onClose={() => setShowSettings(false)} currency={currency} theme={theme} onThemeToggle={toggleTheme} onCurrencyChange={setCurrency}/>}
    </>
  );
};

const root = ReactDOM.createRoot(document.getElementById('orbit-root'));
root.render(<OrbitApp/>);
</script>
</body>
</html>
```

---

## 📄 FILE 2 — vercel.json

> Vercel deployment config with asset caching. Save as `vercel.json` alongside `index.html`.

```json
{
  "version": 2,
  "routes": [
    {
      "src": "/assets/(.*)",
      "headers": {
        "Cache-Control": "public, max-age=86400, immutable"
      },
      "dest": "/assets/$1"
    },
    {
      "src": "/(.*)",
      "headers": {
        "Cache-Control": "public, max-age=3600"
      },
      "dest": "/$1"
    }
  ]
}

```

---

## 📄 FILE 3 — .gitignore

> Git ignore rules. Save as `.gitignore` in your project root.

```
# Claude Code session files
.claude/

# OS files
.DS_Store
Thumbs.db
desktop.ini

# Editor files
.vscode/
*.swp
*.swo

```

---

## 📄 FILE 4 — DEPLOY.md

> Full Vercel / GitHub Pages deployment guide.

# Orbit Desk — Vercel Deployment Guide

**Deploy your app live in under 5 minutes. Three methods — pick the one that suits you.**

---

## Project Structure

```
Sessions/
├── index.html          ← The entire app (single file)
├── assets/
│   ├── celestial-command.png
│   ├── celestial-budget.png
│   ├── celestial-clients.png
│   ├── celestial-invoices.png
│   ├── celestial-subscriptions.png
│   ├── celestial-tax.png
│   ├── celestial-cashflow.png
│   └── celestial-goals.png
└── DEPLOY.md           ← This file
```

> No build step. No dependencies. No server. Pure static HTML — Vercel deploys it instantly.

---

## Method 1 — Drag & Drop (Fastest, no setup needed)

1. Go to **[vercel.com](https://vercel.com)** → Sign in (free account)
2. On the dashboard click **"Add New → Project"**
3. Scroll down to **"Import Third-Party Git Repository"** and choose **"Deploy without Git"**  
   *(or look for the "Deploy from your computer" / drag-drop option)*
4. **Drag your entire `Sessions` folder** onto the upload zone
5. Vercel detects it as a static site automatically
6. Click **Deploy** → Your live URL appears in ~30 seconds

**Your app will be live at:** `https://orbit-desk-xxxx.vercel.app`

---

## Method 2 — GitHub (Recommended for updates)

This method means every time you save `index.html`, your live site updates automatically.

### Step 1 — Push to GitHub

```bash
# In your Sessions folder
git init
git add .
git commit -m "Initial deploy: Orbit Desk"

# Create a repo on github.com first, then:
git remote add origin https://github.com/YOUR_USERNAME/orbit-desk.git
git branch -M main
git push -u origin main
```

### Step 2 — Connect to Vercel

1. Go to **[vercel.com](https://vercel.com)** → **"Add New → Project"**
2. Click **"Import Git Repository"**
3. Authorize GitHub and select your `orbit-desk` repo
4. Vercel settings — **leave everything default:**

| Setting | Value |
|---|---|
| Framework Preset | **Other** |
| Root Directory | `.` (leave blank) |
| Build Command | *(leave empty)* |
| Output Directory | *(leave empty)* |
| Install Command | *(leave empty)* |

5. Click **Deploy**

**Auto-deploys:** Every `git push` to `main` will automatically update your live site within ~20 seconds.

---

## Method 3 — Vercel CLI

```bash
# Install Vercel CLI (one time)
npm install -g vercel

# In your Sessions folder
cd "C:\Users\Prathamesh\OneDrive\Claude\Sessions"

# Deploy
vercel

# Follow the prompts:
# ? Set up and deploy? Y
# ? Which scope? (your account)
# ? Link to existing project? N
# ? What's your project name? orbit-desk
# ? In which directory is your code? ./
# ? Want to override settings? N

# Your URL is printed instantly
```

To deploy to production (not preview):
```bash
vercel --prod
```

---

## Optional: vercel.json Config

Create a `vercel.json` file in your Sessions folder for cleaner URLs and caching:

```json
{
  "version": 2,
  "routes": [
    {
      "src": "/(.*)",
      "headers": {
        "Cache-Control": "public, max-age=3600"
      },
      "dest": "/$1"
    }
  ]
}
```

---

## Custom Domain (Optional)

1. On your Vercel project dashboard → **"Settings" → "Domains"**
2. Click **"Add"** and enter your domain e.g. `orbitdesk.yourdomain.com`
3. Copy the **CNAME record** Vercel shows you
4. Go to your domain registrar (GoDaddy, Namecheap, Cloudflare etc.)
5. Add the CNAME record → DNS propagates in 5–60 minutes

---

## What Works After Deployment

| Feature | Status |
|---|---|
| All 8 modules (Command Center → Revenue Goals) | ✅ |
| Dark / Light theme toggle | ✅ |
| Currency selector (INR, USD, GBP, EUR…) | ✅ |
| Data persistence | ✅ localStorage (per browser) |
| CSV Import (Upwork, Fiverr, Stripe, PayPal, Razorpay, Bank CSV) | ✅ |
| Arc Gauge (Tax Reserve) | ✅ |
| Cash Flow Calendar | ✅ |
| Sidebar collapse | ✅ |
| Mobile responsive | ✅ |
| Celestial background images | ✅ (served from assets/) |

> **Note on Data:** All user data is stored in the browser's `localStorage`. Each visitor gets their own isolated data. There is no backend database — data is private per device/browser.

---

## Troubleshooting

**Images not loading after deploy?**  
Make sure the `assets/` folder is inside the same folder as `index.html` when you upload.

**Blank page on deploy?**  
Vercel must serve `index.html` as the root. If using CLI, confirm the root directory is the `Sessions` folder (where `index.html` lives), not a parent folder.

**App works locally but not on Vercel?**  
Open browser DevTools → Console. If you see `Failed to load resource` errors for `.png` files, the `assets/` folder wasn't included in the upload.

---

## Quick Deploy Checklist

- [ ] `index.html` is in the root of the upload folder
- [ ] `assets/` folder with all 8 `.png` files is included
- [ ] No build command set (it's static)
- [ ] Framework preset set to **Other**
- [ ] Deploy clicked → URL received

---

*Orbit Desk v1.0 — Built with React + Babel (CDN), pure static, zero dependencies.*  
*Deploy time: ~30 seconds on Vercel.*


---

## 🚀 Quick Start

1. Save `index.html` and `vercel.json` to a new folder
2. Create an `assets/` subfolder and download the 8 `.png` files from GitHub
3. Open `index.html` in any browser — works immediately, no server needed
4. To go live: follow the DEPLOY.md guide above (Vercel, 30 seconds)

---

## 🔗 Links

| | |
|---|---|
| **GitHub Repo** | https://github.com/Pratham2060-ap/Claude-Code-Project1 |
| **Assets Download** | https://github.com/Pratham2060-ap/Claude-Code-Project1/tree/main/assets |

---

*Generated by Claude Code · Orbit Desk v1.0*