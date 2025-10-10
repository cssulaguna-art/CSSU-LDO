# CSSU DASHBOARD — Deployment Guide

This project is a static client-side dashboard (HTML/CSS/JS) served from the project root. It currently stores data in the browser (localStorage). This README explains free hosting options and exact PowerShell commands to publish the site.

Quick summary of options:
- Temporary public demo (local): ngrok — exposes your local XAMPP server via HTTPS for demos.
- Persistent static hosting (free): GitHub Pages, Netlify, Surge.
- Shared multi-user data: requires server-side storage (PHP+MySQL or Firebase). See below.

1) Prepare a Git repository (one-time, run in PowerShell)

Set-Location -Path 'C:\xampp\htdocs\CSSU DASHBOARD'
git init
git add .
git commit -m "Initial commit - HOA dashboard"
git branch -M main
# create a repo on GitHub and replace origin URL below
git remote add origin https://github.com/<your-username>/<repo>.git
git push -u origin main

2) Deploy with GitHub Pages (free, persistent)
- I included a GitHub Actions workflow (.github/workflows/deploy-pages.yml) that will deploy the repository contents to GitHub Pages whenever you push to `main`.
- After you push the repo to GitHub, open the repository Settings → Pages (or wait a minute) and the action will publish the site at `https://<your-username>.github.io/<repo>`.

Notes: this is suitable for static front-ends. The site will continue to use localStorage per user (no shared data).

3) Quick demo via ngrok (temporary)
- Start Apache from XAMPP so your site is available at http://localhost (or http://localhost:80).
- Download and install ngrok: https://ngrok.com
- In PowerShell run:

ngrok authtoken <YOUR_NGROK_AUTHTOKEN>  # optional
ngrok http 80

- ngrok prints a public HTTPS URL you can share. When you're done close ngrok.

4) Static hosting alternatives
- Netlify: Sign up, drag & drop the project folder in Netlify's Sites UI or connect your GitHub repo for continuous deploys.
- Surge: `npm i -g surge` then `surge . your-site-name.surge.sh` (requires node/npm and surge login).

5) Make the app multi-user / shared data
- Option A: Small PHP API + MySQL (works with standard shared hosting)
  - Move data from localStorage to server endpoints (GET/POST). I can scaffold PHP endpoints and client fetch calls.
- Option B: Firebase (fast, real-time)
  - Add Firestore and Firebase Hosting, replace localStorage with Firestore reads/writes.

What I prepared for you
- A GitHub Actions workflow to auto-deploy to GitHub Pages when you push to `main`.

If you'd like, I can:
- Create the GitHub repo for you (I can't push using your credentials). I can produce the git commands and the workflow is ready.
- Scaffold a minimal PHP API and show how to update the client to use it.
- Guide you step-by-step while you execute the git push and enable the site.

Tell me which hosting option you want and I will continue with step-by-step commands or scaffold the server side if you want shared persistence.
