# NelcifranMagalhaes.github.io

My portfolio website built with Jekyll.

## Local Development

To run this site locally:

1. Install Ruby (version 2.7 or higher)
2. Install dependencies:
   ```bash
   bundle install
   ```
3. Run the Jekyll server:
   ```bash
   bundle exec jekyll serve
   ```
4. Open your browser to `http://localhost:4000`

## Deployment

This site is automatically deployed to GitHub Pages when changes are pushed to the main branch.

## Adding Content

- **Blog posts**: Add new markdown files to the `_posts` directory with the format `YYYY-MM-DD-title.md`
- **Pages**: Create new markdown files in the root directory with appropriate front matter

## Structure

- `_config.yml` - Site configuration
- `index.md` - Homepage
- `about.md` - About page
- `_posts/` - Blog posts directory
- `Gemfile` - Ruby dependencies
