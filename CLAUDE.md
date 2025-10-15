# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Lalit Mishra built with Hugo static site generator and the hugo-coder theme. The site is minimal, fast, and optimized for web performance with WebP images. Deployed to Cloudflare Pages at https://lalitmishra.in.

## Development Commands

**Local Development:**
```bash
hugo server -D
```
Site runs at http://localhost:1313 with live reload

**Production Build:**
```bash
hugo --minify
```
Output in `public/` directory

## Deployment Configuration

**Cloudflare Pages Settings:**
- Build command: `hugo --minify`
- Build output directory: `public`
- Environment variable: `HUGO_VERSION=0.151.0`

## Architecture & Content Structure

### Site Pages
- **Home page** (`content/_index.md`): Avatar, bio, social links
- **Projects page** (`content/projects/_index.md`): Portfolio showcase with custom layout

The site intentionally has no About or Contact pages - all info is on the home page with social links.

### Projects System

Projects are defined in front matter in `content/projects/_index.md` using this structure:

```yaml
projects:
  - title: "Project Name"
    description: "Project description..."
    link: "https://project-url.com"
    screenshots:
      - "/images/projects/screenshot1.webp"
      - "/images/projects/screenshot2.webp"
    tags:
      - "Technology"
      - "Framework"
```

**Custom Template:** `layouts/_default/projects.html` renders projects with:
- Screenshot modal viewer with keyboard navigation (←/→ arrows, Escape to close)
- Click screenshots to open full-screen preview
- Navigate between screenshots within same project
- Responsive grid layout

**Custom Styling:** `assets/scss/custom.scss` includes:
- Project card styling
- Modal overlay and navigation
- Dark mode support
- Mobile responsive adjustments

### Image Optimization

**All images must be WebP format** for performance:
- Avatar: 400x400px, ~40KB
- Project screenshots: 1200px width, ~40-50KB each

To optimize new images:
```bash
magick input.png -resize 1200x output.webp  # for screenshots
magick input.jpg -resize 400x400 output.webp  # for avatars
```

### Configuration

**hugo.toml key settings:**
- Theme: `hugo-coder` (installed as git submodule in `themes/`)
- Custom SCSS: `assets/scss/custom.scss`
- Social links: Configured as array with Font Awesome icons
- Menu: Only "Projects" link in main navigation
- Markup: `unsafe = true` to allow inline HTML in markdown

### Theme Customization

The hugo-coder theme is extended with:
1. Custom layout override: `layouts/_default/projects.html`
2. Custom styles: `assets/scss/custom.scss` (loaded via `customSCSS` param)
3. Inline JavaScript for modal functionality in projects template

**Note:** Theme is a git submodule - do not modify theme files directly. Override via `layouts/` or `assets/`.

## Content Guidelines

- Keep images optimized (WebP, appropriate dimensions)
- Project screenshots should be descriptive of the project's UI/features
- Use semantic HTML when needed in markdown (enabled via `unsafe = true`)
- Maintain minimal, clean aesthetic matching the Coder theme
