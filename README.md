# WorldWhisper — Story Studio

A responsive static creative-writing PWA. Upload an image, inspect its dominant color/light and aspect ratio locally, generate an opening-story seed, and narrate it using browser speech synthesis.

## Important capability distinction
This repository is deployable as a static GitHub Pages site. A browser-only static site cannot securely call a paid AI vision/writing API without exposing a secret key. Therefore:
- **Out of the box:** image characteristics are sampled locally with Canvas and used by a deterministic story-seed generator. It is not an AI vision model and does not semantically recognize objects or people.
- **Optional real AI:** configure a secure server endpoint in `config.js`. The app sends multipart fields `image`, `direction`, and `language`; the endpoint should return JSON `{ "mood": "...", "scene": "...", "story": "..." }`. Keep provider credentials on the server. Add authentication, rate limits, file validation, size limits, moderation and CORS controls on that backend.
- **Read Aloud:** uses the browser/device Web Speech API and its installed voices. It is not a hosted expressive AI voice service; voice choice and language availability vary by device/browser. Odia voices may not be installed on every platform.

## Run locally
For full PWA behavior use a local web server:

```bash
python -m http.server 8000
```
Open http://localhost:8000.

## Automated tests
Requires Node.js 18+:

```bash
npm test
```

## GitHub Pages deployment
1. Create a repository, e.g. `worldwhisper-story-studio`.
2. Extract the ZIP and upload all files/folders to the repository root. Keep `index.html` at root.
3. Commit to the `main` branch.
4. Open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select `main` and `/(root)`, then Save.
7. After deployment, visit `https://YOUR-USERNAME.github.io/worldwhisper-story-studio/`.

All asset paths are relative and support GitHub Pages project subpaths. Keep `.nojekyll`.

## PWA notes
Service worker registration requires HTTPS or localhost. GitHub Pages provides HTTPS. Some browsers show install UI in their own menu rather than firing the install prompt event.

## Admin demo
The admin panel shows fictional sample counts only. It has no authentication, real users, database or analytics. Add a backend before using it for real administration.
