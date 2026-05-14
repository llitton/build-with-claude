# Build With Claude

Source for [lauralitton.github.io/build-with-claude](https://lauralitton.github.io/build-with-claude) — a beginner's guide to building real AI tools by talking to Claude.

Site structure:

- `index.md` — Home page
- `docs/101-your-first-ai-tool.md` — Level 1 tutorial (30 min)
- `docs/201-make-it-real.md` — Level 2 tutorial (a weekend)
- `docs/301-build-the-real-thing.md` — Level 3 tutorial (a few weeks)
- `docs/case-study.md` — Story of how Call Intelligence got built
- `docs/resources.md` — Tools, prompts, glossary
- `_config.yml` — Jekyll/Just-the-Docs configuration
- `assets/images/` — Screenshots (placeholders + real)

---

## Publishing for the first time

You have two paths. The fast path is push-only. The slow path lets you preview locally before pushing.

### Fast path (recommended): push and let GitHub build it

The site is configured to be built by GitHub Pages. You don't need Ruby, Jekyll, or any local tooling. **Just push to GitHub.**

#### 1. Create the GitHub repo

Go to [github.com/new](https://github.com/new) and create a new repository:

- Name: `build-with-claude`
- Public
- **Do not** initialize with a README, .gitignore, or license (this folder already has them)

After creating, you'll see GitHub's "push an existing repository" instructions. Use them, or follow the commands below.

#### 2. Push from your laptop

In Terminal, in this folder:

```bash
cd /Users/lauralitton/build-with-claude
git init
git add .
git commit -m "Initial: build-with-claude site"
git branch -M main
git remote add origin https://github.com/lauralitton/build-with-claude.git
git push -u origin main
```

#### 3. Turn on GitHub Pages

1. Go to your repo on github.com
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Build and deployment** → **Source**, select **Deploy from a branch**
4. Branch: `main`, folder: `/ (root)`. Save.
5. Wait 1-2 minutes. The first build is slow.

Your site will be live at:

```
https://lauralitton.github.io/build-with-claude/
```

GitHub Pages will rebuild automatically every time you push to `main`. Total deploy time: ~30 seconds per change after the first build.

---

### Slow path (optional): preview locally before pushing

Useful if you want to see changes before committing. Requires installing Ruby. **Skip this section if you don't care about local preview.**

#### Install Ruby (one-time)

Mac comes with an old Ruby. Install a current one via [rbenv](https://github.com/rbenv/rbenv):

```bash
brew install rbenv
rbenv init  # follow the printed instructions to update your shell config
rbenv install 3.3.0
rbenv global 3.3.0
```

Restart Terminal. Confirm with:

```bash
ruby --version  # should say 3.3.0
```

#### Install Jekyll + dependencies

In this folder:

```bash
bundle install
```

This reads `Gemfile` and installs Jekyll + Just-the-Docs theme.

#### Run the local preview

```bash
bundle exec jekyll serve
```

Open [http://localhost:4000/build-with-claude/](http://localhost:4000/build-with-claude/) in your browser.

The site rebuilds automatically as you save changes to markdown files. Refresh the page to see updates.

---

## Editing content

Every page is a Markdown file. Edit it in any text editor (Cursor works great), save, and either:

- **Local preview is running**: refresh the browser tab.
- **No local preview**: commit and push. GitHub Pages rebuilds in ~30s.

### Adding a screenshot

1. Drop your image into `assets/images/`
2. Reference it in a markdown file with:

   ```markdown
   ![Description of image](../assets/images/your-screenshot.png)
   *Caption goes here.*
   ```

3. See `assets/images/README.md` for the list of placeholder images that need real screenshots.

### Editing the navigation order

Open the file you want to reorder. At the top, change `nav_order: N` to the new position. Save.

### Adding a new page

1. Create a new file in `docs/`, e.g. `docs/whatever.md`
2. At the top, add front matter:

   ```yaml
   ---
   title: My new page
   nav_order: 7
   permalink: /docs/whatever/
   ---
   ```

3. Write content in Markdown below.

---

## How the layered ("more detail if you want it") sections work

Anywhere in the markdown, you can add:

```markdown
<details markdown="block">
<summary><strong>Want more detail on this?</strong></summary>

Hidden by default. Click the summary to expand. Full Markdown works here.

</details>
```

This is the pattern used throughout the site for progressive disclosure. Keep the visible track short. Move the deep-dive content into `<details>` blocks.

---

## Custom callouts

Used inline:

```markdown
{: .tip }
> A tip!

{: .warning }
> A warning!

{: .story }
> A "From the build" anecdote.
```

The styles are defined in `_config.yml` under `callouts`. Add more by editing that config.

---

## Mermaid diagrams

Mermaid diagrams render natively in this theme. Just write:

````markdown
```mermaid
flowchart LR
    A --> B
    B --> C
```
````

Edit live at [mermaid.live](https://mermaid.live) and paste in.

---

## Troubleshooting

**Site looks unstyled after pushing**: GitHub Pages can take a few minutes for the first build. Wait 5 minutes and refresh.

**Local preview won't start**: most often a Ruby version mismatch. Run `bundle install` again. If that fails, ask Claude — paste the error.

**Links between pages broken**: check the `permalink:` in the front matter of each file. The current scheme is `/docs/<slug>/`. Internal links from within `docs/` use `../<other-slug>/` (note: trailing slash matters).

**Mermaid diagram doesn't render**: make sure your fence is exactly `` ```mermaid `` (lowercase m, no extra space). Also check the diagram syntax at [mermaid.live](https://mermaid.live).

**Need help editing**: open the relevant `.md` file in Cursor and ask Claude. The whole site is markdown — Claude can edit any of it directly.

---

## License

Content: CC-BY-4.0 (share freely with attribution).
Site code: MIT.

Built by [Laura Litton](https://github.com/lauralitton).
