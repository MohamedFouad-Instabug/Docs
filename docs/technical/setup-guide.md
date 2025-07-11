# Setup Guide

Follow these steps to run and configure **test-docs-workflow** locally and in production.

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
3. **Configure environment variables:**
   - Copy `.env.example` to `.env` and update values as needed.
4. **Run the application:**
   ```bash
   npm start
   ```

## Production Setup

- Ensure all environment variables are set for production.
- Use a process manager (e.g., PM2) or container orchestration (e.g., Docker, Kubernetes).
- Set up monitoring and logging for reliability. 