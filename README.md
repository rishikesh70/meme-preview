# MemeShare Preview (static client + mock server)

This repo contains:
- client/: React client (source)
- server/mockServer.js: in-memory mock API server (no Mongo required)
- .github/workflows/deploy-gh-pages.yml: GitHub Action to build client and publish to gh-pages

Goals:
- Preview the app UI without Mongo/Node on server side (mock API used)
- Host static client on GitHub Pages (auto-deploy via GitHub Actions)
- Run mock API locally for dynamic behavior: npm run start-mock

Quick start (local, recommended)
1. Clone or create repo locally with these files.
2. Start mock API:
   cd server
   npm install
   node mockServer.js
   # server runs at http://localhost:5000

3. Start client dev server (pointing to mock API):
   cd client
   npm install
   # mac/linux:
   REACT_APP_API_BASE=http://localhost:5000/api npm start
   # Windows (PowerShell):
   $env:REACT_APP_API_BASE="http://localhost:5000/api"; npm start

4. Open the client:
   http://localhost:3000

Build for production and preview static files locally
1. Build client:
   cd client
   npm run build

2. Serve the built static site locally (optional):
   npx serve build
   # open http://localhost:3000 (serve default port)

Deploy to GitHub (manual)
1. Create a new repo on GitHub (example: your-username/memeshare-preview).
2. In your local folder:
   git init
   git add .
   git commit -m "Initial commit — memeshare preview (client + mock server)"
   git branch -M main
   git remote add origin https://github.com/<your-username>/memeshare-preview.git
   git push -u origin main

3. The included GitHub Action (/.github/workflows/deploy-gh-pages.yml) will build the client and publish to gh-pages branch on each push to main. Enable GitHub Pages for the repository (Branch: gh-pages, root) if GitHub doesn't auto-enable it.

Mock admin credentials (mock server):
- Email: admin@example.com
- Password: password123
- Mock token (for admin endpoints if used): mock-admin-token

Notes
- The mock server accepts imageUrl strings in JSON for creating memes (no file upload).
- The mock server is in-memory: restarting it resets data.
- The GH Action uses the default GITHUB_TOKEN to push to gh-pages; no extra secrets needed.
