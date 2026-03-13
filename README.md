# The Data Pipeline Doctrine

A personal technical blog built with [Quartz v4](https://quartz.jzhao.xyz/).

## Publishing Workflow

Write in Obsidian, publish with a single command:

```bash
npx quartz sync
```

This commits your changes, pushes to GitHub, and triggers automatic deployment.

### Quick Publish Alias

Add this to your shell profile (`~/.bashrc` or `~/.zshrc`):

```bash
alias publish="cd ~/path-to-blog && npx quartz sync"
```

Then just run `publish` from anywhere.

## Creating New Posts

1. Open Obsidian and navigate to the `content/` folder
2. Use Templater to create a new post from a template:
   - `Cmd/Ctrl + P` → "Templater: Create new note from template"
   - Choose: `til-template.md`, `deep-dive-template.md`, or `decision-framework-template.md`
3. Write your content
4. Run `npx quartz sync` to publish

## Local Preview

Preview your site before publishing:

```bash
npx quartz build --serve
```

Opens at `http://localhost:8080` with hot reload.

## GitHub Pages Setup

To enable GitHub Pages deployment:

1. Go to your repository on GitHub
2. Navigate to **Settings** → **Pages**
3. Under **Source**, select **GitHub Actions**
4. Push to the `v4` branch to trigger deployment

Your site will be available at `https://{username}.github.io/{repo-name}/`

## Custom Domain (Optional)

To add a custom domain later:

1. Create a `CNAME` file in `static/` with your domain (e.g., `blog.example.com`)
2. Configure DNS:
   - For apex domain (`example.com`): Add `A` records pointing to GitHub's IPs:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - For subdomain (`blog.example.com`): Add a `CNAME` record pointing to `{username}.github.io`
3. In GitHub repo Settings → Pages → Custom domain, enter your domain

## Development Commands

```bash
npx quartz build         # Build static site to public/
npx quartz build --serve # Build and serve locally
npx quartz sync          # Commit, push, and deploy
npx quartz update        # Pull latest Quartz updates
```
