# Requirements Document

## Feature: Personal Technical Blog

### Requirement 1: Site Setup and Configuration
**User Story:** As a blog author, I want a fully configured Quartz v4 static site so that I can publish Markdown content from my Obsidian vault to GitHub Pages with a single command.

#### Acceptance Criteria
1. WHEN the author clones the repository and runs `npm i` THE SYSTEM SHALL install all dependencies without errors
2. WHEN the author runs `npx quartz build` THE SYSTEM SHALL generate a complete static site in the `public/` directory
3. WHEN the author runs `npx quartz build --serve` THE SYSTEM SHALL serve the site locally at `localhost:8080` with hot reload
4. WHEN the author runs `npx quartz sync` THE SYSTEM SHALL commit all changes, push to GitHub, and trigger a GitHub Actions deployment
5. WHEN the site is deployed THE SYSTEM SHALL be accessible at `{username}.github.io/{repo-name}/`
6. THE SYSTEM SHALL configure the site title as "The Data Pipeline Doctrine" in `quartz.config.ts`
7. THE SYSTEM SHALL set `enableSPA: true`, `enablePopovers: true`, and `defaultDateType: "created"` in configuration
8. THE SYSTEM SHALL add `["private", "templates", ".obsidian", "blog-ideas.md"]` to `ignorePatterns` so draft infrastructure is never published

### Requirement 2: Content Structure and Landing Page
**User Story:** As a blog reader, I want a clean landing page with recent posts so that I can quickly find and read the latest content.

#### Acceptance Criteria
1. WHEN a reader visits the homepage THE SYSTEM SHALL display the blog title, a brief tagline, and a reverse-chronological list of published posts
2. WHEN a reader views the post list THE SYSTEM SHALL show each post's title, date, description, and tags
3. THE SYSTEM SHALL include an `index.md` landing page with a brief introduction and auto-generated recent posts listing
4. THE SYSTEM SHALL include an `about.md` page with author biography and blog purpose
5. THE SYSTEM SHALL render the sample posts provided in the `content/` directory: `why-im-starting-this-blog.md` and `til-leverage-hierarchy-for-engineering.md`
6. THE SYSTEM SHALL include a `blog-ideas.md` file with `draft: true` that is excluded from the published site

### Requirement 3: Visual Design and Custom Styling
**User Story:** As a blog author, I want a clean, professional, dark-themed design that feels distinctive without requiring ongoing design maintenance.

#### Acceptance Criteria
1. THE SYSTEM SHALL use a dark color scheme as the default theme with warm neutral tones (not pure black/white)
2. THE SYSTEM SHALL configure custom colors in `quartz.config.ts` theme section:
   - Background: `#0D0D0D` (page), `#141414` (card/surface)
   - Text: `#E8E4DF` (primary), `#9B9589` (secondary/muted)
   - Accent/links: `#CA9B5A` (warm gold)
3. THE SYSTEM SHALL apply custom typography via `custom.scss`:
   - Body font: system font stack with `Georgia` as serif fallback for article text
   - Code font: `JetBrains Mono` or system monospace
   - Comfortable line-height (1.7+ for body text)
4. THE SYSTEM SHALL add subtle custom styling for code blocks, blockquotes, and horizontal rules in `custom.scss`
5. THE SYSTEM SHALL ensure Mermaid diagrams render correctly with colors that complement the dark theme
6. THE SYSTEM SHALL ensure the site is fully readable and navigable on mobile devices

### Requirement 4: Navigation, Discovery, and SEO
**User Story:** As a blog reader, I want to discover related content through tags, backlinks, search, and RSS so that I can explore topics that interest me.

#### Acceptance Criteria
1. WHEN a reader clicks a tag THE SYSTEM SHALL display a tag index page listing all posts with that tag
2. WHEN a reader views a post THE SYSTEM SHALL display a backlinks section showing other posts that link to it
3. WHEN a reader uses the search function THE SYSTEM SHALL perform full-text search across all published content
4. THE SYSTEM SHALL generate an RSS feed at `/index.xml` that includes all published posts
5. THE SYSTEM SHALL generate a `sitemap.xml` for search engine discoverability
6. THE SYSTEM SHALL include OpenGraph meta tags on each page with `title`, `description`, and a default `og-image`
7. THE SYSTEM SHALL configure the Quartz Explorer component in the sidebar for directory-based navigation
8. THE SYSTEM SHALL configure the Quartz Graph component to show an interactive backlink graph

### Requirement 5: Obsidian Authoring Integration
**User Story:** As a blog author using Obsidian, I want my standard Obsidian workflow (wikilinks, tags, frontmatter, Mermaid) to work seamlessly so that I never think about the publishing system while writing.

#### Acceptance Criteria
1. WHEN a post contains Obsidian wikilinks (`[[page-name]]`) THE SYSTEM SHALL render them as working hyperlinks to the target page
2. WHEN a post contains YAML frontmatter with `title`, `date`, `tags`, `description`, and `draft` THE SYSTEM SHALL use these fields for rendering, indexing, and filtering
3. WHEN a post contains Mermaid code blocks THE SYSTEM SHALL render them as SVG diagrams
4. WHEN a post contains standard Markdown elements (headings, lists, code blocks, images, tables) THE SYSTEM SHALL render them correctly
5. THE SYSTEM SHALL support `draft: true` frontmatter to exclude posts from the published site while keeping them in the repository
6. THE SYSTEM SHALL include Obsidian Templater-compatible templates in a `templates/` directory for TIL, Deep Dive, and Decision Framework post types

### Requirement 6: Blog Post Templates
**User Story:** As a blog author, I want pre-built templates for my three main content types so that I can start writing in under 30 seconds.

#### Acceptance Criteria
1. THE SYSTEM SHALL include a TIL template (`templates/til-template.md`) with sections: What I was trying to do, What I discovered, Why this matters, References
2. THE SYSTEM SHALL include a Deep Dive template (`templates/deep-dive-template.md`) with sections: The problem, How it actually works, Key trade-offs, Practical implications, What I'd do differently
3. THE SYSTEM SHALL include a Decision Framework template (`templates/decision-framework-template.md`) with sections: When you face this decision, The options, The decision tree (with Mermaid placeholder), Where I've seen this go wrong, The one-liner
4. WHEN a template is used in Obsidian Templater THE SYSTEM SHALL support `{{title}}` and `{{date}}` placeholder variables in frontmatter

### Requirement 7: GitHub Actions Deployment
**User Story:** As a blog author, I want automatic deployment on every push to the main branch so that publishing requires only `npx quartz sync`.

#### Acceptance Criteria
1. WHEN code is pushed to the `v4` branch THE SYSTEM SHALL trigger a GitHub Actions workflow that builds and deploys the site
2. THE SYSTEM SHALL use the Quartz default `deploy.yml` workflow without modification
3. WHEN the build fails THE SYSTEM SHALL surface the error in GitHub Actions logs
4. THE SYSTEM SHALL complete the full build-and-deploy cycle in under 3 minutes
