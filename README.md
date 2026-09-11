# Minimalist Backend Portfolio (Jekyll)

A clean, data-driven portfolio/CV for backend engineers.

## Quick Start

1. Install Ruby (3.1+ recommended) and Bundler.
2. Install dependencies:
   ```bash
   bundle install
   ```
3. Run locally:
   ```bash
   bundle exec jekyll serve
   ```
4. Open `http://127.0.0.1:4000`.

## Edit Your Content

- Profile, interests, communities, and education: `_data/profile.yml`
- French profile content: `_data/profile_fr.yml`
- Projects/work history: `_data/projects.yml`
- French projects content: `_data/projects_fr.yml`
- Page structure: `index.html`
- Styling: `assets/css/style.scss`
- Notes index page: `blog.md`
- Notes posts: `_posts/*.md`

## Language Routes

- English home: `/`
- French home: `/fr/`
- English blog: `/blog/`
- French blog: `/fr/blog/`

Use `lang: en` or `lang: fr` in each post front matter so it appears on the right blog page.

## Theme

Use the Light / Dark mode toggle in the top menu. The selected theme is saved in the browser with localStorage.

## Write a New Note

1. Create a file in `_posts/` named:
   `YYYY-MM-DD-title.md`
2. Add front matter:
   ```yaml
   ---
   layout: default
   title: "Post Title"
   tags: [fintech, architecture]
   ---
   ```
3. Write your note in Markdown.
4. Your post appears automatically on `/blog/` and the homepage "Notes" section.

## Deployment

You can deploy to GitHub Pages, Netlify, or Cloudflare Pages as a static Jekyll site.
