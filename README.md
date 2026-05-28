# vlumo.io static site

Three pages — home, privacy, terms — styled to match the app. Plain HTML/CSS, no build step.

## Deploy to Cloudflare Pages (10 minutes)

### 1. Push this folder to a GitHub repo

Easiest: make a new repo just for the site (so it's separate from the app).

```bash
cd C:\Users\halee\OneDrive\Documents\Vlumo\site
git init
git add .
git commit -m "Initial vlumo.io site"
```

Create a new public repo at [github.com/new](https://github.com/new) called `vlumo-site`. Then:

```bash
git branch -M main
git remote add origin https://github.com/<your-username>/vlumo-site.git
git push -u origin main
```

### 2. Connect to Cloudflare Pages

1. Log in at [dash.cloudflare.com](https://dash.cloudflare.com)
2. Left sidebar → **Workers & Pages**
3. **Create application → Pages → Connect to Git**
4. Authorize Cloudflare to access your GitHub
5. Pick the `vlumo-site` repo
6. Build settings:
   - **Framework preset**: None
   - **Build command**: leave empty
   - **Build output directory**: `/` (root)
7. Click **Save and Deploy**

First deploy takes ~30 seconds. You'll get a free `vlumo-site.pages.dev` URL.

### 3. Point vlumo.io at it

In Cloudflare:
1. Go to your Pages project → **Custom domains** tab
2. Click **Set up a custom domain** → enter `vlumo.io`
3. Cloudflare auto-configures the DNS records (because you registered the domain with them)
4. Takes about 1–2 minutes for HTTPS to provision

### 4. Set up email forwarding

So `support@vlumo.io` lands in your real inbox.

In Cloudflare:
1. Left sidebar → **Email** → **Email Routing**
2. Click **Enable Email Routing** (Cloudflare adds the MX records automatically)
3. Add a destination: your real email address (e.g., your Gmail). Confirm via the verification email Cloudflare sends.
4. Add a custom address: `support@vlumo.io` → forward to your real email
5. (Optional) Add a catch-all: `*@vlumo.io` → forward to your real email, so any typo'd address still reaches you

That's it. Send a test email to `support@vlumo.io` from a different account to verify.

---

## Updates later

Every push to `main` on the `vlumo-site` repo triggers a Cloudflare Pages rebuild automatically. Edit the HTML, push, and your site updates in ~30 seconds.

## Files

- `index.html` — Landing page with "coming to App Store soon"
- `privacy.html` — Privacy Policy (the version Apple will read during review)
- `terms.html` — Terms of Service
- `styles.css` — Shared styling, matches Vlumo app's Carbon theme

## Notes for Apple review

- The privacy policy URL goes in App Store Connect under **App Privacy → Privacy Policy URL**: `https://vlumo.io/privacy`
- The terms URL isn't strictly required but is referenced from the in-app sign-up screen
- Both pages must be live and crawlable (no login required) before submitting for review
