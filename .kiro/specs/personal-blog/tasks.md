# Implementation Plan

- [x] 1. Initialize Quartz project and install dependencies
    - Clone the Quartz v4 repository: `git clone https://github.com/jackyzha0/quartz.git my-blog`
    - Run `npm i` to install all dependencies
    - Verify `npx quartz build` completes without errors on the default content
    - _Requirements: 1.1, 1.2_

- [x] 2. Configure site metadata in `quartz.config.ts`
    - Set `pageTitle` to `"The Data Pipeline Doctrine"`
    - Set `enableSPA: true`, `enablePopovers: true`, `defaultDateType: "created"`
    - Set `baseUrl` to the target GitHub Pages URL
    - Add `ignorePatterns: ["private", "templates", ".obsidian", "blog-ideas.md"]`
    - Set `locale` to `"en-US"`
    - _Requirements: 1.6, 1.7, 1.8_

- [x] 3. Configure dark theme colors in `quartz.config.ts`
    - Set darkMode colors: `light: "#0D0D0D"`, `lightgray: "#1A1A1A"`, `gray: "#4A4A4A"`, `darkgray: "#9B9589"`, `dark: "#E8E4DF"`, `secondary: "#CA9B5A"`, `tertiary: "#DAB06A"`, `highlight: "#CA9B5A15"`, `textHighlight: "#CA9B5A30"`
    - Set typography: header `"Instrument Serif"`, body `"DM Sans"`, code `"JetBrains Mono"`
    - Set `fontOrigin: "googleFonts"` and `cdnCaching: true`
    - _Requirements: 3.1, 3.2, 3.3_

- [x] 4. Configure plugins in `quartz.config.ts`
    - Enable transformer plugins: FrontMatter, CreatedModifiedDate (priority: frontmatter), SyntaxHighlighting (github-dark theme), ObsidianFlavoredMarkdown, GitHubFlavoredMarkdown, TableOfContents, CrawlLinks, Description, Latex (katex)
    - Enable filter plugin: RemoveDrafts
    - Enable emitter plugins: AliasRedirects, ComponentResources, ContentPage, FolderPage, TagPage, ContentIndex (with enableRSS: true, enableSiteMap: true), Assets, Static, NotFoundPage
    - _Requirements: 4.1, 4.4, 4.5, 5.1, 5.2, 5.3, 5.4, 5.5_

- [x] 5. Configure layout components in `quartz.layout.ts`
    - Set left sidebar: PageTitle, Spacer (mobile), Search, Darkmode toggle, Explorer (desktop)
    - Set right sidebar: TableOfContents (desktop), Graph (desktop)
    - Set beforeBody: Breadcrumbs, ArticleTitle, ContentMeta, TagList
    - Set afterBody: Backlinks, Graph
    - Set footer with links to GitHub profile and RSS feed (`/index.xml`)
    - _Requirements: 4.2, 4.3, 4.6, 4.7, 4.8_

- [x] 6. Create custom SCSS styling in `quartz/styles/custom.scss`
    - Set article body `line-height: 1.75` and max-width `680px`
    - Style blockquotes with `3px` left border in accent color `#CA9B5A`
    - Style code blocks with slightly lighter background (`#141414`) and subtle border
    - Style tag links as small rounded pills with accent background
    - Add paragraph spacing for scanability (`margin-bottom: 1.2em`)
    - Style horizontal rules as subtle gradient dividers
    - Ensure Mermaid diagrams render with theme-compatible colors (override `.mermaid` background)
    - Add subtle rounded corners and shadow to images
    - Verify mobile responsiveness at 375px, 768px, and 1440px
    - _Requirements: 3.4, 3.5, 3.6_

- [x] 7. Create landing page content (`content/index.md`)
    - Write frontmatter with `title: "The Data Pipeline Doctrine"`
    - Write a 3-4 sentence introduction: who the author is, what the blog covers, why it exists
    - Use Quartz's built-in `RecentNotes` component or a Dataview-style query to auto-list recent posts (Quartz handles this via the FolderPage plugin if index.md is present)
    - _Requirements: 2.1, 2.2, 2.3_

- [x] 8. Create about page (`content/about.md`)
    - Write frontmatter with `title: "About"` and a description
    - Include author biography: principal engineer, data platforms, ETL pipelines
    - Include blog purpose: media leverage, learning in public, data pipeline doctrine
    - Include contact/links section (GitHub, LinkedIn — placeholder URLs)
    - _Requirements: 2.4_

- [x] 9. Add sample blog posts to `content/`
    - Add `why-im-starting-this-blog.md` with proper frontmatter (`title`, `date: 2026-03-10`, `tags: [meta, career, writing]`, `description`, `draft: false`)
    - Add `til-leverage-hierarchy-for-engineering.md` with proper frontmatter (`title`, `date: 2026-03-10`, `tags: [til, career, systems-thinking]`, `description`, `draft: false`)
    - Add `blog-ideas.md` with `draft: true` in frontmatter — verify it is excluded from the build
    - _Requirements: 2.5, 2.6, 5.5_

- [x] 10. Create Obsidian Templater blog post templates in `templates/`
    - Create `templates/til-template.md` with: YAML frontmatter (title with `{{title}}`, date with `{{date}}`, tags with `til` placeholder, draft: false), sections for What I was trying to do / What I discovered / Why this matters / References
    - Create `templates/deep-dive-template.md` with: YAML frontmatter, sections for The problem / How it actually works / Key trade-offs / Practical implications / What I'd do differently
    - Create `templates/decision-framework-template.md` with: YAML frontmatter, sections for When you face this decision / The options / The decision tree (with Mermaid code block placeholder) / Where I've seen this go wrong / The one-liner
    - Verify all templates are excluded from the published site via `ignorePatterns`
    - _Requirements: 6.1, 6.2, 6.3, 6.4_

- [x] 11. Add static assets
    - Create or add a `static/favicon.ico` (simple data-pipeline-themed icon or placeholder)
    - Create or add a `static/og-image.png` (1200x630px with blog title for social sharing)
    - Reference og-image in Quartz Head component configuration if needed
    - _Requirements: 4.6_

- [x] 12. Set up GitHub Actions deployment
    - Verify `.github/workflows/deploy.yml` exists (Quartz ships this by default)
    - Ensure the workflow triggers on push to `v4` branch
    - Verify the workflow uses `npx quartz build` and deploys to `gh-pages` branch
    - Document in README: go to repo Settings → Pages → Source: GitHub Actions
    - _Requirements: 7.1, 7.2, 7.3, 7.4_

- [x] 13. Build verification and quality checks
    - Run `npx quartz build` and verify zero errors
    - Run `npx quartz build --serve` and manually verify:
      - Homepage renders with blog title and recent posts
      - Both sample posts render with correct formatting, tags, and dates
      - About page renders correctly
      - `blog-ideas.md` does NOT appear anywhere on the site
      - Tags link to auto-generated tag pages
      - Backlinks section appears on posts
      - Search returns results for "leverage" and "pipeline"
      - Graph view shows connections between pages
      - RSS feed is accessible at `/index.xml`
      - Site is readable on mobile (375px viewport)
      - Mermaid diagram in TIL post renders as SVG
    - _Requirements: 1.2, 1.3, 2.1, 2.5, 2.6, 3.6, 4.1, 4.2, 4.3, 4.4, 5.1, 5.3_

- [x] 14. Create README with publishing workflow
    - Document the one-command publishing workflow: write in Obsidian → `npx quartz sync`
    - Document the `publish` shell alias: `alias publish="cd ~/my-blog && npx quartz sync"`
    - Document how to create a new post using Templater templates
    - Document how to preview locally before publishing
    - Document how to add a custom domain later (CNAME file + DNS config)
    - _Requirements: 1.4, 1.5_
