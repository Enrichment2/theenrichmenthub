# The Enrichment Hub

Welcome to my personal website repository! This is the home of my online presence where I share projects, thoughts, and whatever else I'm working on.

## About

This is a personal website built with Eleventy (11ty) static site generator, featuring a clean, terminal-inspired design with a fun food-themed dark/light mode toggle. The site uses Netlify CMS for easy content management while being hosted on Cloudflare Pages for optimal performance.

## Tech Stack

- **Static Site Generator**: Eleventy (11ty)
- **Content Management**: Netlify CMS with Git Gateway
- **Hosting**: Cloudflare Pages
- **Authentication**: Netlify Identity
- **Styling**: Custom CSS with CSS variables for theming
- **Templates**: Nunjucks (.njk)

## Features

- **🍌🧀 Food-Themed Mode Toggle**: Banana emoji for dark mode, cheese emoji for light mode
- **Responsive Design**: Works great on desktop and mobile devices
- **Content Management**: Easy post creation via Netlify CMS at `/admin/`
- **RSS Feed**: Subscribe to updates at `/feed.xml`
- **Clean Navigation**: Easy-to-use navigation system across all pages
- **Terminal Aesthetic**: Dark grey and neon green color scheme

## Project Structure

```
├── src/                    # Source templates and content
│   ├── _includes/         # Reusable components (nav, footer)
│   ├── _layouts/          # Page layouts
│   └── posts/             # Blog posts (markdown)
├── admin/                 # Netlify CMS configuration
├── styles.css             # Main stylesheet
├── .eleventy.js          # Eleventy configuration
└── _site/                # Generated site (not in repo)
```

## Development

### Local Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Run development server:
   ```bash
   npm start
   ```

3. Build for production:
   ```bash
   npm run build
   ```

### Creating Posts

Posts can be created in two ways:
1. **Via CMS**: Access `/admin/` on the live site and use Netlify CMS
2. **Manually**: Add markdown files to `src/posts/` following the existing format

## Deployment

The site automatically deploys to Cloudflare Pages when changes are pushed to the `main` branch. Netlify CMS commits directly to the GitHub repository, triggering automatic rebuilds.

## Status

Currently under active development with new features and content being added regularly.

---

*Based and sus since day one* 🎮
