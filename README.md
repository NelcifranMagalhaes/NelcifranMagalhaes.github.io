# NelcifranMagalhaes.github.io

My portfolio website built with Jekyll using the [cvless](https://github.com/piazzai/cvless) theme.

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
- **CV**: Edit `cv.md` to update your curriculum vitae
- **Profile links**: Update `_config.yml` to add social media links

## Structure

- `_config.yml` - Site configuration including author info and profile links
- `index.md` - Homepage with introduction and blog archive
- `cv.md` - CV page
- `posts.md` - Blog posts listing page
- `404.md` - Error page
- `_posts/` - Blog posts directory
- `Gemfile` - Ruby dependencies (cvless theme)
