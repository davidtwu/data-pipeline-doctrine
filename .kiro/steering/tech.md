# Technology Context

## Stack
- **Static Site Generator:** Quartz v4 (https://quartz.jzhao.xyz/)
  - Node.js/TypeScript-based SSG designed specifically for Obsidian vault publishing
  - Built-in support for: wikilinks, backlinks, graph view, full-text search, tag pages, RSS
  - Configuration via `quartz.config.ts` and `quartz.layout.ts`
  - Content lives in `content/` directory as standard Markdown with YAML frontmatter
- **Hosting:** GitHub Pages via GitHub Actions
  - Quartz ships with `.github/workflows/deploy.yml` out of the box
  - Free tier is sufficient; no custom domain initially
- **Authoring:** Obsidian
  - Markdown files with YAML frontmatter
  - Wikilinks (`[[page-name]]`) for internal linking
  - Mermaid diagram support for architecture posts
  - Templater plugin for blog post templates
- **Version Control:** Git + GitHub
  - The Quartz repo IS the blog repo
  - `npx quartz sync` handles commit + push in one command

## Key Quartz Conventions
- Content goes in `content/` directory
- Static assets go in `content/` alongside posts or in `static/` for global assets
- Configuration is in `quartz.config.ts` (site metadata) and `quartz.layout.ts` (page layout)
- Plugins are configured in `quartz.config.ts` under the `plugins` key
- Custom CSS goes in `quartz/styles/custom.scss`
- Frontmatter fields Quartz understands: `title`, `date`, `tags`, `draft`, `description`, `aliases`
- Posts with `draft: true` are excluded from the production build
- Quartz generates tag index pages automatically from frontmatter tags

## Constraints
- Do NOT use any external databases or APIs
- Do NOT require any server-side runtime (pure static output)
- Do NOT add heavy JavaScript frameworks (React, Vue, etc.) — Quartz uses Preact internally
- Do NOT modify Quartz core files unless absolutely necessary — prefer configuration and custom CSS
- All customization should be achievable through `quartz.config.ts`, `quartz.layout.ts`, and `custom.scss`
- The site must work fully without JavaScript (content readable, navigation functional)

## Development Commands
```bash
npx quartz create       # Initial setup (only run once)
npx quartz build        # Build static site to `public/`
npx quartz build --serve # Build and serve locally at localhost:8080
npx quartz sync         # Commit, push, and trigger deploy
npx quartz update       # Pull latest Quartz updates
```

## Code Style
- TypeScript for any configuration files
- Standard Markdown for all content
- SCSS for custom styling
- Prefer Quartz built-in plugins over custom solutions
- Keep configuration minimal — every added option is future maintenance debt
