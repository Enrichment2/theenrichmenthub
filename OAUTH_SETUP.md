# OAuth Gateway Setup Instructions

This guide will help you set up a free Cloudflare Worker as an OAuth gateway for Sveltia CMS, enabling unlimited free posting.

## Prerequisites
- A Cloudflare account (free tier is fine)
- A GitHub account

## Step 1: Create a GitHub OAuth App

1. Go to [GitHub Settings > Developer settings > OAuth Apps](https://github.com/settings/developers)
2. Click **"New OAuth App"**
3. Fill in the details:
   - **Application name**: `TheEnrichmentHub CMS` (or any name you like)
   - **Homepage URL**: `https://enrichmetwo.win`
   - **Authorization callback URL**: `https://YOUR-WORKER-NAME.YOUR-SUBDOMAIN.workers.dev/callback`
     - (You'll update this after creating the worker in Step 2)
4. Click **"Register application"**
5. On the next page:
   - Copy the **Client ID** and save it
   - Click **"Generate a new client secret"**
   - Copy the **Client Secret** and save it (you won't see it again!)

## Step 2: Deploy the Cloudflare Worker

### Option A: Using Wrangler CLI (Recommended)

1. Install Wrangler (Cloudflare's CLI):
   ```bash
   npm install -g wrangler
   ```

2. Login to Cloudflare:
   ```bash
   wrangler login
   ```

3. Create a new worker:
   ```bash
   cd /home/enrich/theenrichmenthub
   wrangler init cms-oauth-worker
   ```
   - Choose "yes" when asked about using TypeScript (or "no" for JavaScript)
   - Choose "no" for creating a package.json (we already have one)

4. Copy the oauth-worker.js content:
   ```bash
   cp oauth-worker.js cms-oauth-worker/src/index.js
   ```

5. Deploy the worker:
   ```bash
   cd cms-oauth-worker
   wrangler deploy
   ```

6. Note the worker URL that's displayed (e.g., `https://cms-oauth-worker.your-subdomain.workers.dev`)

### Option B: Using Cloudflare Dashboard

1. Go to [Cloudflare Dashboard > Workers & Pages](https://dash.cloudflare.com/)
2. Click **"Create application"** > **"Create Worker"**
3. Name it something like `cms-oauth-worker`
4. Click **"Deploy"**
5. Click **"Edit code"**
6. Delete the default code
7. Copy and paste the entire contents of `oauth-worker.js` from this repo
8. Click **"Save and Deploy"**
9. Note the worker URL (e.g., `https://cms-oauth-worker.your-subdomain.workers.dev`)

## Step 3: Add Environment Variables to the Worker

1. In Cloudflare Dashboard, go to your worker
2. Click **"Settings"** > **"Variables"**
3. Under **"Environment Variables"**, add:
   - **Name**: `GITHUB_CLIENT_ID`, **Value**: (paste your Client ID from Step 1)
   - **Name**: `GITHUB_CLIENT_SECRET`, **Value**: (paste your Client Secret from Step 1)
4. Click **"Save and Deploy"**

## Step 4: Update GitHub OAuth App Callback URL

1. Go back to your [GitHub OAuth App settings](https://github.com/settings/developers)
2. Click on your app
3. Update the **Authorization callback URL** to:
   ```
   https://YOUR-ACTUAL-WORKER-URL.workers.dev/callback
   ```
   (Replace with the actual worker URL from Step 2)
4. Click **"Update application"**

## Step 5: Update Your CMS Config

1. Edit `admin/config.yml` in this repo
2. Update the `base_url` line:
   ```yaml
   backend:
     name: github
     repo: Enrichment2/theenrichmenthub
     branch: main
     base_url: https://YOUR-ACTUAL-WORKER-URL.workers.dev
   ```
3. Save the file
4. Commit and push:
   ```bash
   git add admin/config.yml
   git commit -m "Update OAuth worker URL"
   git push
   ```

## Step 6: Test It Out!

1. Wait for Cloudflare Pages to deploy your site
2. Go to `https://enrichmetwo.win/admin/`
3. Click **"Login with GitHub"**
4. You should be redirected to GitHub, then back to your CMS
5. Start creating unlimited posts for FREE!

## Troubleshooting

- **"OAuth error"**: Check that your environment variables are set correctly in Cloudflare
- **"Redirect mismatch"**: Make sure the callback URL in GitHub matches your worker URL exactly
- **Still seeing Netlify errors**: Clear your browser cache and try in incognito mode

## Cost

- **Cloudflare Workers Free Tier**: 100,000 requests/day (way more than you'll ever need for a personal CMS)
- **GitHub OAuth**: Completely free
- **Total cost**: $0.00/month forever 🎉
