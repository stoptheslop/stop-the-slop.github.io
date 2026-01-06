# Stop The Slop

A community-driven manifesto for genuine design and engineering. Championing craftsmanship over "slop."

## Features

- **Automated Signature Collection**: Users can sign the manifesto using a simple GitHub Issue Form.
- **Continuous Deployment**: Automated builds and deployments to GitHub Pages using GitHub Actions.
- **Configurable Content**: Site text is centralized in `_data/content.yml` for easy updates.
- **Paginated Signatories**: A robust collection-based system to display signatories while maintaining performance.
- **SEO Optimized**: Built-in SEO tags and metadata.

## Technology Stack

- **Jekyll**: Static site generator.
- **jekyll-paginate-v2**: For advanced pagination of signatories.
- **jekyll-seo-tag**: For search engine optimization.
- **GitHub Actions**: For processing signatures and site deployment.

## How to Sign

1. Click the "Sign the Manifesto" button on the website.
2. Fill out the GitHub Issue Form with your details.
3. Submit the issue.
4. The automated "Process Signature" workflow will:
   - Parse your submission.
   - Add your details to the `_signatures` collection.
   - Commit the change and close your issue.
   - Trigger a new site build.

## Project Structure

- `_signatures/`: Individual YAML/Markdown files for each signatory.
- `_data/content.yml`: Central configuration for site text (Backdrop, Manifesto items).
- `.github/workflows/`:
  - `process_signature.yml`: Automation for signatory processing.
  - `deploy-jekyll.yml`: Site build and deployment pipeline.
- `index.html`: Main site template with pagination logic.
- `assets/css/style.css`: Site styles.

## Local Development

1. Install Ruby and Bundler.
2. Run `bundle install` to install dependencies.
3. Run `bundle exec jekyll serve` to start the local development server.
