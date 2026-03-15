# CLAUDE.md - Development Guide

## Repository Overview

This is a personal portfolio website for Kayla Patterson, built with **Jekyll** and hosted on **GitHub Pages**. It's a lightweight static site generator-based project with a clean, responsive design.

**Repository**: `kdpatters/kdpatters.github.io`
**Primary Branch**: `main`
**Tech Stack**: Jekyll, HTML5, CSS3, Markdown

---

## Project Structure

```
kdpatters.github.io/
├── _config.yml           # Jekyll configuration file
├── _layouts/
│   └── default.html      # Main page layout template with header, nav, footer
├── index.md              # Home page content
├── about.md              # About page content
├── contact.md            # Contact page content
├── style.css             # Main stylesheet (responsive design)
├── CLAUDE.md             # This file
└── .git/                 # Git repository metadata
```

---

## Key Files & Their Purpose

### `_config.yml`
- Minimal Jekyll configuration file
- Sets permalink format to `/:title` for clean URLs
- Rarely modified; only update for structural changes to URL routing

### `_layouts/default.html`
- Master template for all pages
- Contains:
  - Header with site title and decorative bar
  - Sticky navigation bar with three links (Home, About, Contact)
  - Main content area with bordered box
  - Footer with copyright and heart symbol
- Uses Jekyll templating:
  - `{{ page.title }}` - rendered page title
  - `{{ content }}` - rendered markdown content
  - Conditional CSS classes (e.g., `active` state based on `page.title`)
- **Important**: The navbar uses strict equality comparison (`==`) for active state detection

### Markdown Files (`.md`)
- `index.md`, `about.md`, `contact.md`
- All follow Jekyll front matter format:
  ```yaml
  ---
  layout: default
  title: Page Title
  ---
  Content here...
  ```
- The `layout: default` field determines which template is used
- The `title` field is used in the page header and for navbar active state

### `style.css`
- Single CSS file for all styling
- Uses CSS custom properties (variables) for consistent theming:
  - `--main-bg-color`: Orange/peach gradient color
  - `--main-bg-color2`: Violet (gradient end)
  - `--main-txt-color`: Black
- **Responsive design**:
  - Default: 50% width content centered (25% margin on each side)
  - Medium screens (≤1000px): 75% width with 12.5% margins
  - Small screens (≤550px): Full width, stacked layout
  - Low height (≤550px): Removes sticky positioning
- Styling classes:
  - `.hbar` - Horizontal bars (black, 10px min-height)
  - `.navbar` - Navigation bar styling
  - `.active` - Active nav link styling (gray background)
  - `.content` - Main content container
  - `.title` - Page header styling
  - `.textbox` - Content box with semi-transparent background
  - `.rounded` - Border radius utility (20px)
  - `.sticky` - Sticky positioning utility
  - `.bordered` - Border utility (2px solid black)

---

## Development Workflow

### Setting Up for Development

1. Clone the repository (already done if you're reading this)
2. Ensure you're on the correct feature branch (e.g., `claude/add-claude-documentation-7BRwn`)
3. No build step required - Jekyll handles this automatically on GitHub Pages

### Making Changes

**Content Changes** (Adding/Editing Pages):
1. Create or modify `.md` files in the root directory
2. Always include proper front matter with `layout` and `title` fields
3. Update navigation in `_layouts/default.html` if adding new pages
4. Test the `page.title` matches the navbar link for proper active state

**Styling Changes**:
1. Edit `style.css` directly
2. Keep responsive breakpoints in mind (1000px and 550px)
3. Use CSS custom properties for colors when possible
4. Test across desktop, tablet, and mobile sizes

**Layout Changes**:
1. Edit `_layouts/default.html` with caution
2. Preserve Jekyll template syntax (e.g., `{{ page.title }}`, `{{ content }}`)
3. Maintain semantic HTML structure
4. Update navbar links if page titles change

**Configuration Changes**:
1. Edit `_config.yml` only when changing Jekyll settings
2. Current setting: `permalink: /:title` - keeps URLs clean
3. Document any new settings with comments

### Git Workflow

All work happens on feature branches starting with `claude/` and ending with a session ID.

**Commit Messages**:
- Be descriptive and concise
- Format: `[Component] Brief description`
- Examples:
  - `[Layout] Add active state to navigation links`
  - `[Styling] Fix responsive layout for small screens`
  - `[Content] Update about page with new bio`
  - `[Config] Update Jekyll permalink format`

**Pushing Changes**:
- Always use: `git push -u origin <branch-name>`
- Branch name MUST start with `claude/` and end with session ID
- Push will fail with 403 if branch naming doesn't match convention
- If network failure occurs during push, retry with exponential backoff (2s, 4s, 8s, 16s)

**Pull Requests**:
- Create PR from feature branch to `main`
- Title should be concise and descriptive
- Include summary of changes and testing approach

---

## Jekyll & GitHub Pages

### How It Works
1. You edit markdown and HTML files
2. GitHub Pages automatically runs Jekyll
3. Jekyll processes layouts, markdown, and front matter
4. Static HTML is generated and deployed

### Local Testing (Optional)
To test locally before pushing:
```bash
jekyll serve
# Visit http://localhost:4000
```

### Front Matter Variables
- `layout` - Which template to use (required)
- `title` - Page title, used in header and navbar (required)
- Custom variables can be added and accessed via `{{ page.variable_name }}`

---

## Common Tasks for AI Assistants

### Adding a New Page
1. Create a new `.md` file in the root (e.g., `projects.md`)
2. Add front matter with `layout: default` and appropriate `title`
3. Add content in markdown
4. Update navbar in `_layouts/default.html` with new link
5. Test that the title matches the navbar link text for active state
6. Commit and push

### Updating Navigation
1. Edit navbar links in `_layouts/default.html` (around line 18-20)
2. Ensure `href` values match page titles (using lowercase or permalink format)
3. Verify that `page.title` comparison in the active state condition matches exactly

### Styling Changes
1. Edit `style.css`
2. Remember responsive breakpoints: 1000px and 550px
3. Test changes across different screen sizes
4. Use CSS custom properties for theme colors

### Content Updates
1. Edit the relevant `.md` file
2. Keep markdown formatting clean
3. Ensure front matter is valid YAML
4. No special formatting required - Jekyll handles it

### Fixing Active Navigation State
- The active state uses: `{% if page.title == 'Home' %}`
- The page title MUST match EXACTLY (case-sensitive)
- If navbar links aren't highlighting correctly, check that `page.title` in front matter matches the link text

---

## Design & Theme

### Color Scheme
- **Primary**: Orange/Peach gradient (`hsla(27, 100%, 65%, 1)`)
- **Secondary**: Violet (`violet`)
- **Text**: Black
- **Accents**: Black bars and borders

### Typography
- Body: Arial
- Headers: Lucida Console (monospace, uppercase)

### Layout Philosophy
- Clean, centered design
- Responsive across all device sizes
- Sticky navigation for easy access
- Bordered content boxes for visual hierarchy
- Semi-transparent text backgrounds for texture

---

## Standards & Conventions

### Naming Conventions
- File names: lowercase with hyphens (e.g., `contact.md`, `style.css`)
- CSS classes: lowercase with hyphens (e.g., `.navbar`, `.bordered`)
- Jekyll front matter: lowercase (e.g., `layout`, `title`)

### Code Style
- HTML: Valid HTML5, semantic tags where possible
- CSS: Use custom properties, mobile-first thinking
- Markdown: Standard markdown syntax, proper spacing

### Best Practices
1. Always test responsive design after styling changes
2. Keep templates and stylesheets DRY (don't repeat yourself)
3. Use meaningful commit messages
4. Update this guide if you change workflows or add features
5. Preserve backward compatibility with URLs (use Jekyll's permalink settings)

---

## Troubleshooting

### Issue: Navigation link isn't showing as active
**Cause**: `page.title` doesn't match the navbar condition exactly
**Fix**: Check for case sensitivity and whitespace. Update either the front matter or the HTML condition.

### Issue: Styling looks broken on mobile
**Cause**: Responsive breakpoint not being triggered
**Fix**: Check viewport meta tag in `_layouts/default.html`. Verify media queries in `style.css` cover your device size.

### Issue: Git push fails with 403
**Cause**: Branch name doesn't follow `claude/...` pattern or network issue
**Fix**: Verify branch name starts with `claude/` and ends with session ID. Retry with exponential backoff if network failure.

### Issue: Jekyll isn't building
**Cause**: Invalid YAML in front matter
**Fix**: Check for proper indentation and quoting in `.md` file front matter. Use Jekyll's error messages as guide.

---

## Current Version Info

- **Project**: Personal Portfolio Site
- **Owner**: Kayla Patterson
- **Copyright**: 2020-2025
- **Status**: Active

---

## When to Update This File

Update CLAUDE.md when:
- Adding new pages or major features
- Changing development workflow or git conventions
- Modifying the project structure
- Adding new dependencies or build tools
- Documenting new styling patterns or conventions

**Last Updated**: March 15, 2025
