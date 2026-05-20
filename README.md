# 🪐 Orbit Desk — Mission Control for Solopreneurs

> A space-themed financial dashboard for freelancers & solopreneurs. Track income, expenses, clients, invoices, subscriptions, tax reserves, cash flow, and revenue goals — all in one place.

**[🚀 Live Demo →](https://claude-code-project1.vercel.app)**

---

## ✨ Features

| Module | What it does |
|---|---|
| **Command Center** | Dashboard overview — revenue, expenses, net profit, charts, quick actions |
| **Budget Tracker** | Log income & expenses, import from CSV (Upwork, Fiverr, Stripe, PayPal, Razorpay, Bank) |
| **Clients** | Manage client relationships, projects, billed amounts |
| **Invoices** | Create, send, track invoices — paid / overdue / draft |
| **Subscriptions** | Monitor recurring SaaS costs, renewal alerts |
| **Tax Reserve** | Arc gauge showing how much tax you've set aside vs needed |
| **Cash Flow** | Interactive calendar with income & payment events |
| **Revenue Goals** | Set targets, track milestone progress |

---

## 🛠️ Tech Stack

- **Pure HTML + CSS + Vanilla JS** — zero build step, zero dependencies
- **React 18** via CDN (no npm needed)
- **Babel** for JSX transpilation in-browser
- **Fonts:** Orbitron, Exo 2, JetBrains Mono (Google Fonts)
- **Storage:** Browser `localStorage` — all data stays on your device

---

## 🚀 Deploy Your Own

### Option 1 — Vercel (Recommended)

1. Fork this repo
2. Go to [vercel.com](https://vercel.com) → **New Project** → Import your fork
3. Framework: **Other** | Build command: *(empty)* | Output: *(empty)*
4. Click **Deploy** → live in 30 seconds ✅

### Option 2 — GitHub Pages

1. Fork this repo
2. Go to **Settings → Pages**
3. Source: **Deploy from branch** → `main` → `/ (root)`
4. Click **Save** → live at `https://YOUR_USERNAME.github.io/Claude-Code-Project1`

### Option 3 — Run Locally

```bash
git clone https://github.com/Pratham2060-ap/Claude-Code-Project1.git
cd Claude-Code-Project1
npx serve .
# Open http://localhost:3000
```

---

## 📸 Screenshots

### Command Center
![Command Center](assets/celestial-command.png)

### Budget Tracker with CSV Import
Supports Upwork, Fiverr, Stripe, PayPal, Razorpay, Bank CSV — 3-step wizard with platform auto-detection.

---

## 📁 Project Structure

```
.
├── index.html          # The entire app (~2600 lines, self-contained)
├── assets/             # Celestial background images (8 modules)
│   ├── celestial-command.png
│   ├── celestial-budget.png
│   └── ...
├── vercel.json         # Vercel caching config
├── DEPLOY.md           # Detailed deployment guide
└── README.md           # This file
```

---

## 💡 Key Design Decisions

- **No conversion** — Currency selector changes symbol only; amounts stored as-is
- **localStorage** — All data private per browser, no backend needed
- **Single file** — Entire app in one `index.html` for easy hosting anywhere
- **CSV Import** — Browser-side FileReader API; files never leave your device

---

*Built with [Claude Code](https://claude.ai/claude-code) — Anthropic's AI coding assistant*
