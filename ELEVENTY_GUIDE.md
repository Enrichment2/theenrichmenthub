# Eleventy + Decap CMS Setup Guide

## What Changed

Your site is now powered by Eleventy, a static site generator that makes it easy to manage content and deploy your site. Here's what was converted:

### Structure
- **Source files**: `src/` directory contains all your templates, posts, and pages
- **Output**: `_site/` directory contains the built static site
- **Posts**: Now markdown files in `src/posts/` with frontmatter metadata
- **Templates**: Nunjucks templates in `src/_layouts/` and `src/_includes/`

### Features Added
1. **Eleventy Static Site Generator**: Builds your HTML from templates and markdown
2. **Decap CMS**: Web-based CMS accessible at `/admin` - post from any device including your phone
3. **RSS Feed**: Automatically generated at `/feed.xml`

## Local Development

### Build the site
```bash
npm run build
```

### Serve locally with hot reload
```bash
npm run serve
```

Then visit http://localhost:8080

## Deployment to Cloudflare Pages

### Initial Setup
1. Go to Cloudflare Pages dashboard
2. Connect your GitHub repository
3. Configure build settings:
   - **Build command**: `npm run build`
   - **Build output directory**: `_site`
   - **Root directory**: `/`

### Enable Netlify Identity (for Decap CMS authentication)

Since you're using Cloudflare Pages, you have two options for authentication:

#### Option 1: Use Netlify Identity (Recommended for simplicity)
1. Create a free Netlify account
2. Go to Site Settings → Identity
3. Enable Identity
4. Enable Git Gateway under Identity → Services
5. Update `admin/config.yml` to use your site URL

#### Option 2: Use GitHub OAuth (More direct)
1. Update `admin/config.yml` to use GitHub backend instead of git-gateway:
```yaml
backend:
  name: github
  repo: Enrichment2/theenrichmenthub
  branch: main
```
2. Set up GitHub OAuth app in your GitHub account settings
3. Add OAuth credentials to Cloudflare Pages environment variables

## Using Decap CMS

### Accessing the CMS
- Visit `your-site.com/admin`
- Log in with your authentication method
- You can now create, edit, and delete posts from any device including your phone!

### Creating a New Post
1. Go to `/admin`
2. Click "Posts" collection
3. Click "New Post"
4. Fill in:
   - Title
   - Publish Date
   - Body content
   - Optional: Check "Neocities Era" for old posts
5. Click "Publish"
6. Changes will be committed to your GitHub repo and auto-deployed

## File Structure
```
├── src/
│   ├── _layouts/        # Page templates
│   │   ├── base.njk     # Main layout with nav/footer
│   │   └── post.njk     # Blog post layout
│   ├── _includes/       # Reusable components
│   │   ├── nav.njk
│   │   └── footer.njk
│   ├── posts/           # Blog posts (markdown files)
│   ├── index.njk        # Homepage
│   ├── all-posts.njk    # Posts listing page
│   ├── articles.njk     # Articles page
│   ├── stuff.njk        # Stuff page
│   └── feed.njk         # RSS feed template
├── admin/               # Decap CMS configuration
│   ├── index.html
│   └── config.yml       # CMS configuration
├── styles.css           # Your terminal-style CSS (unchanged)
├── .eleventy.js         # Eleventy configuration
└── package.json         # Dependencies and scripts
```

## Customization

### Adding New Pages
Create a new `.njk` file in `src/` with frontmatter:
```njk
---
layout: base.njk
title: My New Page
permalink: /new-page/
---

<div class="container">
  <h1>My New Page</h1>
  <p>Content here...</p>
</div>
```

### Modifying the Design
- Edit `styles.css` (unchanged from your original design)
- Edit templates in `src/_layouts/` and `src/_includes/`

### Adding to Decap CMS
Edit `admin/config.yml` to add new collections or fields.

## RSS Feed
Your RSS feed is automatically generated at `/feed.xml`. Readers can subscribe using any RSS reader.

## Troubleshooting

### Build fails
- Check `npm run build` output for errors
- Ensure all markdown files have proper frontmatter
- Verify `.eleventy.js` configuration

### CMS not loading
- Check authentication setup
- Ensure `admin/config.yml` has correct repository settings
- Verify Netlify Identity or GitHub OAuth is configured

### Posts not showing
- Ensure posts have `tags: posts` in frontmatter
- Check that files are in `src/posts/` directory
- Verify date format: `YYYY-MM-DDTHH:MM:SS`
