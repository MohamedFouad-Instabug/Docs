# Deployment

This page describes how to deploy **test-docs-workflow**, a simple React recipes website, as a static site.

## Build for Production

- Run the following command to create a production build:
  ```bash
  npm run build
  ```
- The static files will be generated in the `build/` directory.

## Deploy to GitHub Pages

1. Push your code to GitHub.
2. Use the `gh-pages` branch or GitHub Actions to deploy the `build/` folder.
3. In your repository settings, set GitHub Pages to serve from the `/build` or `/docs` folder as appropriate.

_There is no backend, database, or environment variable configuration required._ 