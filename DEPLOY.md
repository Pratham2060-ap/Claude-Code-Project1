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
