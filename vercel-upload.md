# Deploying PQ-Stego to Vercel

## ✅ Is This Possible?

**Yes — 100%.** This project is a pure static website:
- Single `index.html` file
- Vanilla CSS & JavaScript (inline, no build step)
- Local image assets in `/images/`
- No Node.js, no npm, no framework, no backend

Vercel handles static sites natively with **zero configuration required**.
Your site will be live at a free `your-project.vercel.app` domain within minutes.

---

## Prerequisites

- A **GitHub account** → https://github.com
- A **Vercel account** → https://vercel.com (sign up free with your GitHub account)
- **Git** installed on your PC → check with `git --version` in terminal
  - Download if missing: https://git-scm.com/download/win

---

## Step 1 — Initialize Git in Your Project Folder

Open **PowerShell** or **Command Prompt**, navigate to your project, and run:

```powershell
cd "f:\research\marketting-web\pqc-steganography-project-main"
git init
git add .
git commit -m "Initial commit: PQ-Stego marketing website"
```

---

## Step 2 — Create a GitHub Repository

1. Go to **https://github.com/new**
2. Fill in the form:
   - **Repository name:** `pq-stego` (or any name you like)
   - **Visibility:** Public *(required for free Vercel deployment on the free tier)*
   - **Do NOT** check "Add a README file" — your project already has files
3. Click **"Create repository"**
4. GitHub will show you a page with commands. Copy the remote URL — it looks like:
   ```
   https://github.com/YOUR-USERNAME/pq-stego.git
   ```

---

## Step 3 — Push Your Project to GitHub

Back in your terminal (still inside the project folder), run:

```powershell
git remote add origin https://github.com/YOUR-USERNAME/pq-stego.git
git branch -M main
git push -u origin main
```

> Replace `YOUR-USERNAME` with your actual GitHub username.
> If prompted for credentials, enter your GitHub username and a **Personal Access Token**
> (not your password). Create one at: https://github.com/settings/tokens → "Generate new token (classic)" → check `repo` scope.

After this, refresh your GitHub repo page — you should see all your files there including `index.html` and the `images/` folder.

---

## Step 4 — Deploy on Vercel

1. Go to **https://vercel.com** and sign in (use "Continue with GitHub")
2. On your Vercel dashboard, click **"Add New Project"**
3. Under **"Import Git Repository"**, find and select your `pq-stego` repo
   - If you don't see it, click **"Adjust GitHub App Permissions"** and grant access
4. Vercel will show a configuration screen. **Leave everything at defaults:**
   - Framework Preset: **Other**
   - Root Directory: `./`
   - Build Command: *(leave empty)*
   - Output Directory: *(leave empty)*
5. Click **"Deploy"**

Vercel will deploy in about 30–60 seconds. Done.

---

## Step 5 — Get Your Live URL

Once deployed, Vercel gives you a permanent URL like:

```
https://pq-stego.vercel.app
```

or if that name is taken:

```
https://pq-stego-yourname.vercel.app
```

You can find and share this URL from your **Vercel Project Dashboard → Domains**.

---

## Step 6 — Every Future Update (Re-deploy)

Vercel automatically re-deploys whenever you push to GitHub. So your workflow for any future change is simply:

```powershell
cd "f:\research\marketting-web\pqc-steganography-project-main"
git add .
git commit -m "Update: describe your change here"
git push
```

Vercel detects the push and re-deploys within ~30 seconds. No manual action needed.

---

## Optional — Rename Your Vercel Domain

By default Vercel auto-generates a domain name from your repo. To set a custom subdomain:

1. Open your project on Vercel dashboard
2. Go to **Settings → Domains**
3. Type a preferred name like `pq-stego-research` → Save
4. Your site will be live at `https://pq-stego-research.vercel.app`

---

## Troubleshooting

| Issue | Fix |
|---|---|
| Images not loading after deploy | Make sure all image paths in `index.html` are relative (e.g. `images/hero-bg.jpg`, not `C:\...`) — they already are ✓ |
| Repo not visible in Vercel | Click "Adjust GitHub App Permissions" and grant Vercel access to the repo |
| Push rejected (authentication) | Use a GitHub Personal Access Token instead of your password |
| Site shows old version | Hard refresh browser: `Ctrl + Shift + R` |
| Fonts not loading | Fonts load from Google CDN — requires internet connection ✓ |

---

## Summary

```
Local files  →  git push  →  GitHub repo  →  Vercel auto-deploy  →  Live URL
```

Total time from zero to live: **~10 minutes.**
