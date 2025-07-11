# Setup Guide

Follow these steps to run **test-docs-workflow** (a simple React recipes website) locally or deploy it as a static site.

## Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-org/test-docs-workflow.git
   ```
2. **Install dependencies:**
   ```bash
   cd test-docs-workflow
   npm install
   ```
3. **Start the development server:**
   ```bash
   npm start
   ```
   The app will be available at `http://localhost:3000`.

## Production/Static Deployment

- Build the static site:
  ```bash
  npm run build
  ```
- Deploy the contents of the `build/` folder to GitHub Pages or any static hosting provider.

_No backend or environment variables are required._ 