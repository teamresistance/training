# Programming Training Hub

Team Resistance programming training documentation site built with Hugo.

## Local Development

1. Install Hugo: `brew install hugo` (macOS) or download from [gohugo.io](https://gohugo.io)
2. Run development server: `hugo server -D`
3. View site at http://localhost:1313

## Building

```bash
hugo
```

Output will be in the `public/` directory.

## Deployment

This site is configured for Cloudflare Pages deployment:

- **Build command**: `hugo --minify`
- **Build output directory**: `public`
- **Root directory**: `/` (or set to `hugo-site` if in subdirectory)

## Adding Content

Create new pages in the `content/` directory:

```bash
hugo new content/page-name.md
```

Edit the markdown file and add your content. The page will automatically appear in the navigation.

## Project Structure

- `content/` - Markdown content files
- `layouts/` - HTML templates
- `static/` - Static assets (CSS, images, favicon)
- `hugo.toml` - Site configuration
