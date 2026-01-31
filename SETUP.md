# GitHub Pages Setup Instructions

## Enable GitHub Pages

To activate the Just the Docs theme with sidebar navigation:

### 1. Enable GitHub Pages

Visit: https://github.com/Hulupeep/mbot-help/settings/pages

Or navigate to:
- Repository → Settings → Pages (left sidebar)

### 2. Configure Source

Set the following options:

- **Source:** GitHub Actions (not "Deploy from a branch")
- The workflow will automatically trigger on every push to `main`

### 3. Wait for Deployment

- The first deployment takes 2-3 minutes
- Check the Actions tab: https://github.com/Hulupeep/mbot-help/actions
- Look for the "Deploy Jekyll site to Pages" workflow
- Green checkmark = successful deployment

### 4. Access Your Documentation

Once deployed, visit:

**https://hulupeep.github.io/mbot-help**

## What You'll See

### Navigation Structure

**Sidebar (left):**
```
🏠 Home
├─ 1. Connecting to mBot2
├─ 2. Downloading Apps
├─ 3. Adding Peripherals
└─ 4. Troubleshooting
```

**Top Bar:**
- Search box (searches all pages)
- "View on GitHub" link
- "RuVector Firmware" link

### Features Enabled

- ✅ **Sidebar navigation** - Easy browsing between guides
- ✅ **Search functionality** - Find content across all docs
- ✅ **Table of contents** - In-page navigation
- ✅ **Dark theme** - Easier on the eyes
- ✅ **Mobile responsive** - Works on phones/tablets
- ✅ **Copy code button** - One-click code copying
- ✅ **Callout boxes** - Warnings, tips, notes highlighted
- ✅ **Back to top** - Quick return to page top
- ✅ **Heading anchors** - Direct links to sections

## Customization

Edit `_config.yml` to change:

```yaml
# Change theme color
color_scheme: dark  # or: light, dark

# Change title
title: "Your Custom Title"

# Add logo
logo: "/assets/images/your-logo.png"

# Configure search
search_enabled: true

# Add Google Analytics
ga_tracking: "UA-XXXXXXXX-X"
```

## Troubleshooting

### Pages Not Deploying?

1. Check Actions tab for errors
2. Ensure Pages is enabled in Settings
3. Verify `main` branch exists
4. Check workflow file syntax

### 404 Error?

- Pages URL: `https://hulupeep.github.io/mbot-help`
- Not: `https://hulupeep.github.io/mbot-help/README`
- The home page is at `/` (index.md)

### Sidebar Not Showing?

- Ensure `nav_order` is set in front matter
- Check `_config.yml` has `nav_enabled: true`
- Verify YAML front matter syntax (3 dashes before/after)

### Search Not Working?

- Search is built during deployment
- May take 5-10 minutes after first deploy
- Refresh browser cache (Ctrl+Shift+R)

## Local Development (Optional)

To preview changes before pushing:

```bash
# Install Ruby and Bundler
gem install bundler

# Install dependencies
bundle install

# Serve locally
bundle exec jekyll serve

# Visit http://localhost:4000/mbot-help
```

## File Structure

```
mbot-help/
├── _config.yml              # Jekyll configuration
├── index.md                 # Home page (/)
├── 01-connecting-laptop-to-mbot.md
├── 02-downloading-apps-to-cyberpi.md
├── 03-adding-peripherals.md
├── 04-troubleshooting-guide.md
├── Gemfile                  # Ruby dependencies
├── .github/
│   └── workflows/
│       └── pages.yml        # Auto-deployment
└── .gitignore              # Ignored files
```

## Adding New Pages

Create a new markdown file with front matter:

```markdown
---
layout: default
title: 5. Advanced Topics
nav_order: 6
description: "Advanced integration patterns"
---

# Advanced Topics
{: .no_toc }

Content here...

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
```

Push to `main` and it will automatically appear in the sidebar!

## Support

- **Theme Docs:** https://just-the-docs.github.io/just-the-docs/
- **Jekyll Docs:** https://jekyllrb.com/docs/
- **GitHub Pages:** https://docs.github.com/pages

---

**Next Step:** Enable GitHub Pages in repository settings!
