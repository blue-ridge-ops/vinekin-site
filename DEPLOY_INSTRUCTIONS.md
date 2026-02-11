# Deploying VineKin to GitHub Pages + GoDaddy

## Step 1: Create the repo on GitHub (1 minute)

1. Go to **https://github.com/new**
2. Owner: **blue-ridge-ops**
3. Repo name: **vinekin-website**
4. Set to **Public** (required for free GitHub Pages)
5. Click **Create repository**

---

## Step 2: Push the site files (2 minutes)

Extract the zip, then from your terminal:

```bash
cd vinekin-website

git init
git add .
git commit -m "Initial VineKin marketing site"
git branch -M main
git remote add origin https://github.com/blue-ridge-ops/vinekin-website.git
git push -u origin main
```

---

## Step 3: Enable GitHub Pages (1 minute)

1. Go to **https://github.com/blue-ridge-ops/vinekin-website/settings/pages**
2. Under **"Build and deployment"**:
   - Source: **Deploy from a branch**
   - Branch: **main**
   - Folder: **/ (root)**
3. Click **Save**

GitHub will build in ~60 seconds. Your site will first be available at:
`https://blue-ridge-ops.github.io/vinekin-website/`

---

## Step 4: Point GoDaddy DNS to GitHub (5 minutes)

1. Log into **GoDaddy** → **My Domains** → **vinekin.com** → **DNS**
2. **Remove** any existing A records or forwarding rules
3. **Add these 4 A records**:

   | Type | Name | Value           | TTL    |
   |------|------|-----------------|--------|
   | A    | @    | 185.199.108.153 | 1 hour |
   | A    | @    | 185.199.109.153 | 1 hour |
   | A    | @    | 185.199.110.153 | 1 hour |
   | A    | @    | 185.199.111.153 | 1 hour |

4. **Add (or update) a CNAME** for www:

   | Type  | Name | Value                            | TTL    |
   |-------|------|----------------------------------|--------|
   | CNAME | www  | blue-ridge-ops.github.io         | 1 hour |

5. **Save**

---

## Step 5: Enable HTTPS (after DNS propagates)

DNS usually takes 5–30 minutes. Once it's ready:

1. Go to **https://github.com/blue-ridge-ops/vinekin-website/settings/pages**
2. Under **Custom domain**, type: `vinekin.com`
3. Click **Save**
4. Wait for the DNS check to pass (green checkmark)
5. Check **"Enforce HTTPS"**

---

## Done! 🌿

Your site is now live at:
- **https://vinekin.com**
- **https://www.vinekin.com**

Future updates: edit files → commit → push → auto-deploys in ~60 seconds.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "DNS check unsuccessful" | Wait 15-30 min for propagation, then retry |
| GitHub 404 page | Make sure Pages source is set to **/ (root)**, not /docs |
| Images broken | Verify `images/` folder is present and paths are relative |
| HTTPS checkbox missing | Only appears after GitHub verifies DNS — wait for green check |
