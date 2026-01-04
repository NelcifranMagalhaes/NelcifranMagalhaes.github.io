# NelcifranMagalhaes.github.io

My portfolio website built with Jekyll using the [cvless](https://github.com/piazzai/cvless) theme.

## About

This site uses the cvless theme with theme files included directly in the repository. This approach allows full customization and ensures compatibility with GitHub Pages using GitHub Actions for deployment.

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

This site is deployed to GitHub Pages using GitHub Actions. The workflow is defined in `.github/workflows/jekyll.yml` and automatically builds and deploys the site when changes are pushed to the main branch.

The GitHub Actions workflow supports all Jekyll plugins, including `jekyll-paginate-v2` which is required by the cvless theme but not supported by GitHub Pages' default Jekyll build.

## Adding Content

- **Blog posts**: Add new markdown files to the `_posts` directory with the format `YYYY-MM-DD-title.md`
- **CV**: Edit `cv.md` to update your curriculum vitae
- **Profile links**: Update `_config.yml` to add social media links

## Structure

- `_config.yml` - Site configuration including author info and profile links
- `_includes/` - Theme include files (particles.js, header, footer, etc.)
- `_layouts/` - Theme layout files (home, cv, post, page)
- `_sass/` - Theme Sass stylesheets
- `assets/` - Theme assets (CSS, JavaScript, fonts)
- `index.md` - Homepage with introduction and blog archive
- `cv.md` - CV page
- `posts.md` - Blog posts listing page
- `404.md` - Error page
- `_posts/` - Blog posts directory
- `Gemfile` - Ruby dependencies
- `.github/workflows/jekyll.yml` - GitHub Actions workflow for deployment
